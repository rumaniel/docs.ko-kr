---
title: 동적 형식 생성을 위해 수집 가능한 어셈블리
description: ''
ms.date: 08/29/2017
helpviewer_keywords:
- reflection, dynamic assembly
- assemblies, collectible
- collectible assemblies, retrieving
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b26da264b2da40e19db4bc5e3b3575505f5c979c
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54637744"
---
# <a name="collectible-assemblies-for-dynamic-type-generation"></a>동적 형식 생성을 위해 수집 가능한 어셈블리

*수집 가능한 어셈블리*는 만들어진 애플리케이션 도메인을 언로드하지 않고 언로드할 수 있는 동적 어셈블리입니다. 수집 가능한 어셈블리에서 사용되는 모든 관리 및 관리되지 않는 메모리 및 포함하는 형식은 회수될 수 있습니다. 어셈블리 이름 등의 정보는 내부 테이블에서 제거됩니다.

언로드를 활성화하려면 동적 어셈블리를 만들 때 <xref:System.Reflection.Emit.AssemblyBuilderAccess.RunAndCollect?displayProperty=nameWithType> 플래그를 사용합니다. 어셈블리는 일시적이며(즉, 저장될 수 없음) [수집 가능한 어셈블리에 대한 제한](#restrictions-on-collectible-assemblies) 섹션에 설명된 제한 사항이 적용됩니다. CLR(공용 언어 런타임)은 어셈블리와 관련된 모든 개체를 릴리스할 때 자동으로 수집 가능한 어셈블리를 언로드합니다. 다른 모든 측면에서 수집 가능한 어셈블리는 다른 동적 어셈블리와 동일한 방식으로 생성 및 사용됩니다.

## <a name="lifetime-of-collectible-assemblies"></a>수집 가능한 어셈블리의 수명

수집 가능한 어셈블리의 수명은 포함하는 형식 및 이러한 형식에서 생성된 개체에 대한 참조의 존재 여부에 따라 제어됩니다. 공용 언어 런타임은 다음 중 하나 이상이 있는 한 어셈블리를 언로드하지 않습니다(`T`는 어셈블리에 정의된 모든 형식). 

- `T`의 인스턴스입니다.

- `T` 배열의 인스턴스입니다.
 
- 형식 인수 중 하나로 `T`를 가진 제네릭 형식의 인스턴스입니다. 해당 컬렉션이 비어 있는 경우에도 `T`의 제네릭 컬렉션을 포함합니다.

- `T`를 나타내는 <xref:System.Type> 또는 <xref:System.Reflection.Emit.TypeBuilder>의 인스턴스입니다. 

   > [!IMPORTANT]
   > 어셈블리의 부분을 나타내는 모든 개체를 릴리스해야 합니다. `T`를 정의하는 <xref:System.Reflection.Emit.ModuleBuilder>는 <xref:System.Reflection.Emit.TypeBuilder>에 대한 참조를 유지하고, <xref:System.Reflection.Emit.AssemblyBuilder> 개체는 <xref:System.Reflection.Emit.ModuleBuilder>에 대한 참조를 유지하므로 이러한 개체에 대한 참조를 릴리스해야 합니다. `T`의 생성에 사용되는 <xref:System.Reflection.Emit.LocalBuilder> 또는 <xref:System.Reflection.Emit.ILGenerator>의 존재는 언로드를 방지합니다.

- 코드를 실행하여 계속 연결할 수 있는 다른 동적으로 정의된 유형 `T1`별 `T`에 대한 정적 참조입니다. 예를 들어 `T1`은 `T`에서 파생될 수 있거나 `T`는 `T1`의 메서드에서 매개 변수의 형식이 될 수 있습니다.
 
- `T`에 속해 있는 정적 필드에 대한 **ByRef**입니다.

- `T`를 참조하는 <xref:System.RuntimeTypeHandle>, <xref:System.RuntimeFieldHandle> 또는 <xref:System.RuntimeMethodHandle>, 또는 `T`의 구성 요소에 대한 것입니다.

- `T`를 나타내는 <xref:System.Type> 개체에 대한 액세스에 간접적 또는 직접적으로 사용될 수 있는 모든 리플렉션 개체의 인스턴스입니다. 예를 들어 `T`에 대한 <xref:System.Type> 개체는 요소 형식이 `T`인 배열 형식에서 또는 형식 인수로 `T`를 가진 제네릭 형식에서 얻을 수 있습니다. 

- `M`이 `T`의 메서드이거나 어셈블리에 정의된 모듈 수준 메서드인 모든 스레드의 호출 스택에 있는 메서드 `M`입니다.

- 어셈블리의 모듈에 정의된 정적 메서드에 대한 대리자입니다.

이 목록의 한 항목만 어셈블리에서 하나의 형식 또는 한 개의 메서드에 대해 있는 경우 런타임은 어셈블리를 언로드할 수 없습니다.

> [!NOTE]
> 런타임은 종료자가 목록의 모든 항목에 대해 실행될 때까지 어셈블리를 실제로 언로드하지 않습니다.

수명 추적을 위해 수집 가능한 어셈블리의 생성에서 만들어지고 사용된 `List<int>`(C#에서) 또는 `List(Of Integer)`(Visual Basic에서)와 같은 생성된 제네릭 형식은 제네릭 형식 정의를 포함하는 어셈블리 또는 해당 형식 인수 중 하나의 정의를 포함하는 어셈블리에서 정의된 것으로 간주됩니다. 사용되는 정확한 어셈블리는 구현 세부 정보이며 변경될 수 있습니다.
 
## <a name="restrictions-on-collectible-assemblies"></a>수집 가능한 어셈블리에 대한 제한 사항

수집 가능한 어셈블리에는 다음과 같은 제약 조건이 적용됩니다. 

- **정적 참조**   
  일반 동적 어셈블리의 형식은 수집 가능한 어셈블리에서 정의된 형식에 대한 정적 참조를 가질 수 없습니다. 예를 들어 수집 가능한 어셈블리의 형식에서 상속되는 일반 형식을 정의하는 경우는 <xref:System.NotSupportedException> 예외가 throw됩니다. 수집 가능한 어셈블리의 형식은 다른 수집 가능한 어셈블리의 형식에 대한 정적 참조를 가질 수 있지만 이는 참조된 어셈블리의 수명을 참조하는 어셈블리의 수명으로 연장합니다.

- **COM interop**   
   COM 인터페이스는 수집 가능한 어셈블리 내에서 정의될 수 없으며 수집 가능한 어셈블리 내의 형식 인스턴스는 COM 개체로 변환될 수 없습니다. 수집 가능한 어셈블리의 형식은 CCW(COM 호출 가능 래퍼) 또는 RCW(런타임 호출 가능 래퍼)로 처리할 수 없습니다. 그러나 수집 가능한 어셈블리의 형식은 COM 인터페이스를 구현하는 개체를 사용할 수 있습니다.

- **플랫폼 호출**   
   <xref:System.Runtime.InteropServices.DllImportAttribute> 특성이 있는 메서드는 수집 가능한 어셈블리에서 선언될 때 컴파일하지 않습니다. <xref:System.Reflection.Emit.OpCodes.Calli?displayProperty=nameWithType> 명령은 수집 가능한 어셈블리에서 형식의 구현에 사용할 수 없으며 이러한 형식은 비관리 코드로 마샬링될 수 없습니다. 그러나 수집 불가능한 어셈블리에서 선언된 진입점을 사용하여 네이티브 코드로 호출할 수 있습니다.
 
- **마샬링**   
   수집 가능한 어셈블리에서 정의된 개체(특히 대리자)는 마샬링될 수 없습니다. 이는 모든 임시 내보낸 형식에 대한 제한입니다.

- **어셈블리 로딩**   
   리플렉션 내보내기는 수집 가능한 어셈블리 로드에 대해 지원되는 유일한 메커니즘입니다. 다른 형태의 어셈블리 로드를 사용하여 로드되는 어셈블리를 언로드할 수 없습니다.
 
- **컨텍스트 바인딩 개체**    
   컨텍스트 정적 변수는 지원되지 않습니다. 수집 가능한 어셈블리의 형식은 <xref:System.ContextBoundObject>를 확장할 수 없습니다. 그러나 수집 가능한 어셈블리의 코드는 다른 곳에서 정의된 컨텍스트 바인딩 개체를 사용할 수 있습니다.

- **스레드 정적 데이터**       
   스레드 정적 변수는 지원되지 않습니다.

## <a name="see-also"></a>참고 항목

- [동적 메서드 및 어셈블리 내보내기](emitting-dynamic-methods-and-assemblies.md)
