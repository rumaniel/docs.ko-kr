---
title: .NET Framework의 리플렉션
ms.date: 03/30/2017
helpviewer_keywords:
- assemblies [.NET Framework], reflection
- EventInfo class, reflection
- common language runtime, reflection
- FieldInfo class, reflection
- ParameterInfo class, reflection
- ConstructorInfo class, reflection
- Assembly class, reflection
- value types, reflection
- reflection, about reflection
- modules, reflection
- runtime, reflection
- Module class, reflection
- MethodInfo class, reflection
- PropertyInfo class, reflection
- type browsers
- reflection
- discovering type information at run time
- type system, reflection
ms.assetid: d1a58e7f-fb39-4d50-bf84-e3b8f9bf9775
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 24112edc3ac28124953974463233800c51da5cfc
ms.sourcegitcommit: b22705f1540b237c566721018f974822d5cd8758
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2018
ms.locfileid: "49453085"
---
# <a name="reflection-in-the-net-framework"></a>.NET Framework의 리플렉션
<xref:System.Reflection> 네임스페이스의 클래스와 <xref:System.Type?displayProperty=nameWithType>을 함께 사용하여 로드된 [어셈블리](../../../docs/framework/app-domains/assemblies-in-the-common-language-runtime.md) 및 어셈블리 내에 정의된 형식(예: [클래스](../../../docs/standard/base-types/common-type-system.md#classes), [인터페이스](../../../docs/standard/base-types/common-type-system.md#interfaces), [값 형식](https://msdn.microsoft.com/library/c9c567f8-8ab1-4d88-834d-00f7d92418de))에 대한 정보를 가져올 수 있습니다. 리플렉션을 사용하여 런타임에 형식 인스턴스를 만들고 이 인스턴스를 호출 및 액세스할 수도 있습니다. 리플렉션의 특정 측면에 대한 항목은 이 개요의 끝부분에서 [관련 항목](#related_topics)을 참조하세요.  
  
 [공용 언어 런타임](../../../docs/standard/clr.md) 로더는 같은 응용 프로그램 범위가 포함된 개체 주위의 경계를 구성하는 [응용 프로그램 도메인](../../../docs/framework/app-domains/application-domains.md)을 관리합니다. 이 관리에는 각 어셈블리를 적절한 응용 프로그램 도메인으로 로드하는 작업과 각 어셈블리 내에서 형식 계층 구조의 메모리 레이아웃을 제어하는 작업이 포함됩니다.  
  
 [어셈블리](../../../docs/framework/app-domains/assemblies-in-the-common-language-runtime.md)에는 모듈이 포함되고, 모듈에는 형식이 포함되고, 형식에는 멤버가 포함됩니다. 리플렉션은 어셈블리, 모듈 및 형식을 캡슐화하는 개체를 제공합니다. 리플렉션을 사용하여 동적으로 형식 인스턴스를 만들거나, 형식을 기존 개체에 바인딩하거나, 기존 개체에서 형식을 가져올 수 있습니다. 그리고 나서 해당 형식의 메서드를 호출하거나 필드 및 속성에 액세스할 수 있습니다. 리플렉션의 일반적인 용도는 다음과 같습니다.  
  
-   <xref:System.Reflection.Assembly>를 사용하여 어셈블리를 정의 및 로드하고, 어셈블리 매니페스트에 나열된 모듈을 로드하고, 이 어셈블리에서 형식을 찾아 해당 인스턴스를 만듭니다.  
  
-   <xref:System.Reflection.Module>을 사용하여 모듈 및 모듈의 클래스가 포함된 어셈블리와 같은 정보를 검색합니다. 모듈에 정의된 모든 전역 메서드나 기타 특정 비전역 메서드를 가져올 수도 있습니다.  
  
-   <xref:System.Reflection.ConstructorInfo>를 사용하여 생성자의 이름, 매개 변수, 액세스 한정자(예: `public` 또는 `private`), 구현 세부 정보(예: `abstract` 또는 `virtual`)와 같은 정보를 검색합니다. <xref:System.Type>의 <xref:System.Type.GetConstructors%2A> 또는 <xref:System.Type.GetConstructor%2A> 메서드를 사용하여 특정 생성자를 호출합니다.  
  
-   <xref:System.Reflection.MethodInfo>를 사용하여 메서드의 이름, 반환 형식, 매개 변수, 액세스 한정자(예: `public` 또는 `private`), 구현 세부 정보(예: `abstract` 또는 `virtual`)와 같은 정보를 검색합니다. <xref:System.Type>의 <xref:System.Type.GetMethods%2A> 또는 <xref:System.Type.GetMethod%2A> 메서드를 사용하여 특정 메서드를 호출합니다.  
  
-   <xref:System.Reflection.FieldInfo>를 사용하여 필드의 이름, 액세스 한정자(예: `public` 또는 `private`), 구현 세부 정보(예: `static`)를 검색하고 필드 값을 가져오거나 설정합니다.  
  
-   <xref:System.Reflection.EventInfo>를 사용하여 이벤트의 이름, 이벤트 처리기 데이터 형식, 사용자 지정 특성, 선언 형식, 리플렉션 형식과 같은 정보를 검색하고 이벤트 처리기를 추가하거나 제거합니다.  
  
-   <xref:System.Reflection.PropertyInfo>를 사용하여 속성의 이름, 데이터 형식, 선언 형식, 리플렉션 형식, 읽기 전용/쓰기 가능 상태와 같은 정보를 검색하고 속성 값을 가져오거나 설정합니다.  
  
-   <xref:System.Reflection.ParameterInfo>를 사용하여 매개 변수 이름, 데이터 형식, 매개 변수가 입력 또는 출력 매개 변수인지 여부, 메서드 서명에서 매개 변수의 위치와 같은 정보를 검색합니다.  
  
-   <xref:System.Reflection.CustomAttributeData>를 사용하여 응용 프로그램 도메인의 리플렉션 전용 컨텍스트에서 작업할 때 사용자 지정 특성에 대한 정보를 검색합니다. <xref:System.Reflection.CustomAttributeData>를 사용하면 특성 인스턴스를 만들지 않고 특성을 검사할 수 있습니다.  
  
 <xref:System.Reflection.Emit> 네임스페이스의 클래스는 런타임에 빌드할 수 있는 특수한 형태의 리플렉션을 제공합니다.  
  
 리플렉션을 사용하여 사용자가 형식을 선택하고 해당 형식에 대한 정보를 볼 수 있도록 하는 형식 브라우저라는 응용 프로그램을 만들 수도 있습니다.  
  
 리플렉션의 다른 용도는 다음과 같습니다. JScript와 같은 언어용 컴파일러에서는 리플렉션을 사용하여 기호 테이블을 생성합니다. <xref:System.Runtime.Serialization> 네임스페이스의 클래스에서는 리플렉션을 사용하여 데이터에 액세스하고 보관할 필드를 결정합니다. <xref:System.Runtime.Remoting> 네임스페이스의 클래스에서는 직렬화를 통해 간접적으로 리플렉션을 사용합니다.  
  
## <a name="runtime-types-in-reflection"></a>리플렉션의 런타임 형식  
 리플렉션은 형식, 멤버, 매개 변수, 기타 코드 엔터티를 나타내는 <xref:System.Type> 및 <xref:System.Reflection.MethodInfo>와 같은 클래스를 제공합니다. 하지만 리플렉션을 사용할 때 이들 클래스를 직접 사용하지 않습니다. 이들 클래스는 대부분 추상 클래스입니다(Visual Basic의 `MustInherit`). 대신에 CLR(공용 언어 런타임)에서 제공된 형식을 사용합니다.  
  
 예를 들어 C# `typeof` 연산자(Visual Basic의 `GetType`)를 사용하여 <xref:System.Type> 개체를 가져오면 개체가 실제로 `RuntimeType`입니다. `RuntimeType`는 <xref:System.Type>에서 파생되고 모든 추상 메서드의 구현을 제공합니다.  
  
 이들 런타임 클래스는 `internal`(Visual Basic의 `Friend`)입니다. 이들 클래스의 동작은 기본 클래스 설명서에서 설명되므로 이들 클래스는 기본 클래스와 별도로 설명되지 않습니다.  
  
<a name="related_topics"></a>   
## <a name="related-topics"></a>관련 항목  
  
|제목|설명|  
|-----------|-----------------|  
|[형식 정보 보기](../../../docs/framework/reflection-and-codedom/viewing-type-information.md)|<xref:System.Type> 클래스를 설명하고 <xref:System.Type>과 여러 리플렉션 클래스를 함께 사용하여 생성자, 메서드, 필드, 속성, 이벤트에 대한 정보를 가져오는 방법을 보여 주는 코드 예제를 제공합니다.|  
|[리플렉션 및 제네릭 형식](../../../docs/framework/reflection-and-codedom/reflection-and-generic-types.md)|리플렉션이 제네릭 형식과 제네릭 메서드의 형식 매개 변수 및 형식 인수를 처리하는 방법을 설명합니다.|  
|[리플렉션의 보안 고려 사항](../../../docs/framework/reflection-and-codedom/security-considerations-for-reflection.md)|리플렉션이 형식 정보 및 액세스 형식을 검색하는 데 사용될 수 있는 정도를 결정하는 규칙을 설명합니다.|  
|[형식 동적 로드 및 사용](../../../docs/framework/reflection-and-codedom/dynamically-loading-and-using-types.md)|런타임 바인딩을 지원하는 리플렉션 사용자 지정 바인딩 인터페이스를 설명합니다.|  
|[방법: 리플렉션 전용 컨텍스트에 어셈블리 로드](../../../docs/framework/reflection-and-codedom/how-to-load-assemblies-into-the-reflection-only-context.md)|리플렉션 전용 로드 컨텍스트를 설명합니다. 어셈블리를 로드하는 방법, 컨텍스트를 테스트하는 방법, 리플렉션 전용 컨텍스트에서 어셈블리에 적용된 특성을 검사하는 방법을 보여 줍니다.|  
|[사용자 지정 특성 액세스](../../../docs/framework/reflection-and-codedom/accessing-custom-attributes.md)|리플렉션을 사용하여 특성 존재 및 값을 쿼리하는 방법을 보여 줍니다.|  
|[정규화된 형식 이름 지정](../../../docs/framework/reflection-and-codedom/specifying-fully-qualified-type-names.md)|BNF(Backus-Naur 형식) 측면에서 정규화된 형식 이름의 형식에 대해 설명하고 특수 문자, 어셈블리 이름, 포인터, 참조, 배열을 지정하는 데 필요한 구문을 설명합니다.|  
|[방법: 리플렉션을 사용하여 대리자 후크](../../../docs/framework/reflection-and-codedom/how-to-hook-up-a-delegate-using-reflection.md)|메서드의 대리자를 만들고 대리자를 이벤트에 후크하는 방법을 설명합니다. 런타임에 <xref:System.Reflection.Emit.DynamicMethod>를 사용하여 이벤트 처리 메서드를 만드는 방법을 설명합니다.|  
|[동적 메서드 및 어셈블리 내보내기](../../../docs/framework/reflection-and-codedom/emitting-dynamic-methods-and-assemblies.md)|동적 어셈블리 및 동적 메서드를 생성하는 방법을 설명합니다.|  
  
## <a name="reference"></a>참조  
 <xref:System.Type?displayProperty=nameWithType>  
  
 <xref:System.Reflection>  
  
 <xref:System.Reflection.Emit>  
  
