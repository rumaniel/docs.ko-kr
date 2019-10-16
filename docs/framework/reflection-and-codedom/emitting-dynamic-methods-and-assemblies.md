---
title: 동적 메서드 및 어셈블리 생성
ms.date: 08/30/2017
helpviewer_keywords:
- reflection emit
- dynamic assemblies
- metadata, emit interfaces
- reflection emit, overview
- assemblies [.NET Framework], emitting dynamic assemblies
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d8e2b9aeb8c632efcbf8c506da4da7c6e7b408e1
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71046080"
---
# <a name="emitting-dynamic-methods-and-assemblies"></a>동적 메서드 및 어셈블리 생성

이 섹션에서는 컴파일러 또는 도구가 런타임에 메타데이터 및 MSIL(Microsoft Intermediate Language)을 내보내고 선택적으로 디스크에서 PE(이식 가능한 실행) 파일을 생성할 수 있게 해주는 <xref:System.Reflection.Emit> 네임스페이스의 관리되는 형식 집합을 설명합니다. 스크립트 엔진과 컴파일러는 이 네임스페이스의 주 사용자입니다. 이 섹션에서는 <xref:System.Reflection.Emit> 네임스페이스에서 제공하는 기능을 리플렉션 내보내기라고 합니다.  
  
리플렉션 내보내기는 다음 기능을 제공합니다.  
  
- 런타임에 <xref:System.Reflection.Emit.DynamicMethod> 클래스를 사용하여 간단한 전역 메서드를 정의하고 대리자를 사용하여 실행합니다.  
  
- 런타임에 어셈블리를 정의하고 실행하거나 디스크에 저장합니다.  
  
- 런타임에 어셈블리를 정의하고 실행한 다음 언로드하고 가비지 수집에서 해당 리소스를 회수할 수 있게 합니다.  
  
- 런타임에 새 어셈블리에서 모듈을 정의하고 실행하거나 디스크에 저장합니다.  
  
- 런타임에 모듈에서 형식을 정의하고 이러한 형식의 인스턴스를 만든 다음 해당 메서드를 호출합니다.  
  
- 디버거 및 코드 프로파일러와 같은 도구에서 사용할 수 있는 정의된 모듈에 대한 기호 정보를 정의합니다.  
  
<xref:System.Reflection.Emit> 네임스페이스의 관리되는 형식 외에도 [메타데이터 인터페이스](../unmanaged-api/metadata/metadata-interfaces.md) 참조 설명서에서 설명하는 관리되지 않는 메타데이터 인터페이스가 있습니다. 관리되는 리플렉션 내보내기는 관리되지 않는 메타데이터 인터페이스 보다 강력한 의미 체계 오류 검사 및 높은 수준의 메타데이터 추상화를 제공합니다.  
  
메타데이터 및 MSIL 작업을 위한 다른 유용한 리소스는 CLI(공용 언어 인프라) 설명서, 특히 "Partition II: 메타데이터 정의 및 의미 체계" "파티션 III: CIL 명령 집합"을 참조하세요. 이 설명서는 [MSDN](https://go.microsoft.com/fwlink/?LinkID=65555) 및 [Ecma 웹 사이트](https://go.microsoft.com/fwlink/?LinkId=116487)에서 온라인으로 제공됩니다.  
  
## <a name="in-this-section"></a>섹션 내용
  
[리플렉션 내보내기의 보안 문제점](security-issues-in-reflection-emit.md)  
리플렉션 내보내기를 사용하여 동적 어셈블리를 만드는 경우와 관련된 보안 문제를 설명합니다.  

[방법: 동적 메서드 정의 및 실행](how-to-define-and-execute-dynamic-methods.md)   
간단한 동적 메서드 및 클래스 인스턴스에 바인딩된 동적 메서드를 실행하는 방법을 보여 줍니다.

[방법: 리플렉션 내보내기를 사용하여 제네릭 형식 정의](how-to-define-a-generic-type-with-reflection-emit.md)   
두 개의 형식 매개 변수가 있는 간단한 제네릭 형식을 만드는 방법, 형식 매개 변수에 클래스, 인터페이스 및 특수 제약 조건을 적용하는 방법, 클래스의 형식 매개 변수를 매개 변수 형식 및 반환 형식으로 사용하는 멤버를 만드는 방법을 보여줍니다.

[방법: 리플렉션 내보내기를 사용하여 제네릭 메서드 정의](how-to-define-a-generic-method-with-reflection-emit.md)   
간단한 제네릭 메서드를 만들고, 내보내고, 호출하는 방법을 보여 줍니다.

[동적 형식 생성을 위해 수집 가능한 어셈블리](collectible-assemblies.md)   
만들어진 애플리케이션 도메인을 언로드하지 않고 언로드할 수 있는 동적 어셈블리인 수집 가능한 어셈블리를 소개합니다.
  
## <a name="reference"></a>참조  

<xref:System.Reflection.Emit.OpCodes>  
메서드 본문을 작성하는 데 사용할 수 있는 MSIL 명령 코드의 카탈로그를 작성합니다.  
  
<xref:System.Reflection.Emit>  
동적 메서드, 어셈블리 및 형식을 내보내는 데 사용되는 관리되는 클래스를 포함합니다.  
  
<xref:System.Type>  
관리되는 리플렉션 및 리플렉션 내보내기에서 형식을 나타내며 이러한 기술 사용의 핵심 요소인 <xref:System.Type> 클래스를 설명합니다.  
  
<xref:System.Reflection>  
메타데이터와 관리 코드를 탐색하는 데 사용되는 관리되는 클래스를 포함합니다.  
  
## <a name="related-sections"></a>관련 단원  

[리플렉션](reflection.md)  
메타데이터와 관리 코드를 탐색하는 방법을 설명합니다.  
  
[.NET 어셈블리](../../standard/assembly/index.md)  
.NET 구현에서 어셈블리에 대해 간략하게 설명합니다.
