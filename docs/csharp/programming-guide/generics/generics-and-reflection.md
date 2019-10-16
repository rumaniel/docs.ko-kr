---
title: 제네릭 및 리플렉션 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- generics [C#], reflection
- reflection [C#], generic types
ms.assetid: 162fd9b4-dd5b-4abb-8c9b-e44e21e2f451
ms.openlocfilehash: be4b72414af8e5a18145330f5c44ae9a79a567cb
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69659882"
---
# <a name="generics-and-reflection-c-programming-guide"></a>제네릭 및 리플렉션(C# 프로그래밍 가이드)
CLR(공용 언어 런타임)은 런타임에 제네릭 형식 정보에 액세스할 수 있으므로 제네릭이 아닌 형식에 대한 방법과 동일한 방법으로 리플렉션을 사용하여 제네릭 형식에 대한 정보를 가져올 수 있습니다. 자세한 내용은 [런타임의 제네릭](./generics-in-the-run-time.md)을 참조하세요.  
  
 .NET Framework 2.0에서는 제네릭 형식에 대한 런타임 정보를 사용할 수 있도록 <xref:System.Type> 클래스에 여러 개의 새 멤버가 추가되었습니다. 이러한 메서드 및 속성을 사용하는 방법에 대한 자세한 내용은 이러한 클래스에 대한 설명서를 참조하세요. <xref:System.Reflection.Emit> 네임스페이스에도 제네릭을 지원하는 새 멤버가 포함되어 있습니다. [방법: 리플렉션 내보내기를 사용하여 제네릭 형식 정의](../../../framework/reflection-and-codedom/how-to-define-a-generic-type-with-reflection-emit.md)를 참조하세요.  
  
 제네릭 리플렉션에 사용되는 용어의 고정 조건 목록은 <xref:System.Type.IsGenericType%2A> 속성 설명을 참조하세요.  
  
|System.Type 멤버 이름|설명|  
|-----------------------------|-----------------|  
|<xref:System.Type.IsGenericType%2A>|형식이 제네릭이면 true를 반환합니다.|  
|<xref:System.Type.GetGenericArguments%2A>|생성된 형식에 제공된 형식 인수 또는 제네릭 형식 정의의 형식 매개 변수를 나타내는 `Type` 개체의 배열을 반환합니다.|  
|<xref:System.Type.GetGenericTypeDefinition%2A>|현재 생성된 형식에 대 한 기본 제네릭 형식 정의 반환합니다.|  
|<xref:System.Type.GetGenericParameterConstraints%2A>|현재 제네릭 형식 매개 변수에 대한 제약 조건을 나타내는 `Type` 개체의 배열을 반환합니다.|  
|<xref:System.Type.ContainsGenericParameters%2A>|형식 또는 바깥쪽 형식이나 메서드에 제공되지 않은 특정 형식에 대한 형식 매개 변수가 포함된 경우 true를 반환합니다.|  
|<xref:System.Type.GenericParameterAttributes%2A>|현재 제네릭 형식 매개 변수의 특수 제약 조건을 설명하는 `GenericParameterAttributes` 플래그의 조합을 가져옵니다.|  
|<xref:System.Type.GenericParameterPosition%2A>|`Type` 개체가 형식 매개 변수를 나타내는 경우 형식 매개 변수를 선언한 제네릭 형식 정의 또는 제네릭 메서드 정의의 형식 매개 변수 목록에서 해당 형식 매개 변수의 위치를 가져옵니다.|  
|<xref:System.Type.IsGenericParameter%2A>|현재 `Type`이 제네릭 형식 또는 메서드 정의의 형식 매개 변수를 나타내는지를 나타내는 값을 가져옵니다.|  
|<xref:System.Type.IsGenericTypeDefinition%2A>|현재 <xref:System.Type>이 다른 제네릭 형식을 생성하는 데 사용될 수 있는 제네릭 형식 정의를 나타내는지 여부를 가리키는 값을 가져옵니다. 형식이 제네릭 형식의 정의를 나타내는 경우 true를 반환합니다.|  
|<xref:System.Type.DeclaringMethod%2A>|현재 제네릭 형식 매개 변수를 정의한 제네릭 메서드를 반환하거나 형식 매개 변수가 제네릭 메서드에 의해 정의되지 않은 경우 null을 반환합니다.|  
|<xref:System.Type.MakeGenericType%2A>|형식 배열의 요소를 현재 제네릭 형식 정의의 형식 매개 변수로 대체하고 생성된 형식을 나타내는 <xref:System.Type> 개체를 반환합니다.|  
  
 또한 <xref:System.Reflection.MethodInfo> 클래스에 새 멤버는 제네릭 메서드에 대한 런타임 정보를 사용하도록 설정합니다. 제네릭 메서드를 반영하는 데 사용되는 용어에 대한 고정 조건 목록은 <xref:System.Reflection.MethodBase.IsGenericMethod%2A> 속성 설명을 참조하세요.  
  
|System.Reflection.MemberInfo 멤버 이름|설명|  
|----------------------------------------------|-----------------|  
|<xref:System.Reflection.MethodBase.IsGenericMethod%2A>|메서드가 제네릭인 경우 true를 반환합니다.|  
|<xref:System.Reflection.MethodInfo.GetGenericArguments%2A>|생성된 제네릭 메서드의 형식 인수나 제네릭 메서드 정의의 형식 매개 변수를 나타내는 Type 개체의 배열을 반환합니다.|  
|<xref:System.Reflection.MethodInfo.GetGenericMethodDefinition%2A>|현재 생성된 메서드에 대한 기본 제네릭 메서드 정의를 반환합니다.|  
|<xref:System.Reflection.MethodBase.ContainsGenericParameters%2A>|메서드 또는 바깥쪽 형식에 제공되지 않은 특정 형식에 대한 형식 매개 변수가 포함된 경우 true를 반환합니다.|  
|<xref:System.Reflection.MethodBase.IsGenericMethodDefinition%2A>|현재 <xref:System.Reflection.MethodInfo>가 제네릭 메서드의 정의를 나타내는 경우 true를 반환합니다.|  
|<xref:System.Reflection.MethodInfo.MakeGenericMethod%2A>|현재 제네릭 메서드 정의의 형식 매개 변수를 형식 배열의 요소로 대체하고, 결과로 생성된 메서드를 나타내는 <xref:System.Reflection.MethodInfo> 개체를 반환합니다.|  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [제네릭](./index.md)
- [리플렉션 및 제네릭 형식](../../../framework/reflection-and-codedom/reflection-and-generic-types.md)
- [제네릭](../../../standard/generics/index.md)
