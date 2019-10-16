---
title: 속성 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 03/10/2017
f1_keywords:
- cs.properties
helpviewer_keywords:
- properties [C#]
- C# language, properties
ms.assetid: e295a8a2-b357-4ee7-a12e-385a44146fa8
ms.openlocfilehash: dec4d4239fd1a953da6e64a1e1aff9593e2863e2
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69596145"
---
# <a name="properties-c-programming-guide"></a>속성(C# 프로그래밍 가이드)

속성은 전용 필드의 값을 읽거나 쓰거나 계산하는 유연한 메커니즘을 제공하는 멤버입니다. 공용 데이터 멤버인 것처럼 속성을 사용할 수 있지만, 실제로 *접근자*라는 특수 메서드입니다. 이렇게 하면 데이터에 쉽게 액세스할 수 있으며 메서드의 안전성과 유연성 수준을 올리는 데에도 도움이 됩니다.  

## <a name="properties-overview"></a>속성 개요  
  
- 속성을 사용하면 클래스가 구현 또는 검증 코드를 숨기는 동시에 값을 가져오고 설정하는 방법을 공개적으로 노출할 수 있습니다.  
  
- [get](../../language-reference/keywords/get.md) 속성 접근자는 속성 값을 반환하는 데 사용되고 [set](../../language-reference/keywords/set.md) 속성 접근자는 새 값을 할당하는 데 사용됩니다. 이러한 접근자는 각기 다른 액세스 수준을 가질 수 있습니다. 자세한 내용은 [접근자 액세스 가능성 제한](./restricting-accessor-accessibility.md)을 참조하세요.  
  
- [value](../../language-reference/keywords/value.md) 키워드는 `set` 접근자가 할당하는 값을 정의하는 데 사용됩니다.  
- 속성은 *읽기/쓰기*(`get` 및 `set` 접근자 모두 포함), *읽기 전용*(`get` 접근자는 포함하지만 `set` 접근자는 포함 안 함) 또는 *쓰기 전용*(`set` 접근자는 포함하지만 `get` 접근자는 포함 안 함)일 수 있습니다. 쓰기 전용 속성은 거의 없으며 주로 중요한 데이터에 대한 액세스를 제한하는 데 사용됩니다.

- 사용자 지정 접근자 코드가 필요 없는 단순한 속성은 식 본문 정의나 [자동 구현 속성](./auto-implemented-properties.md)으로 구현할 수 있습니다.
 
## <a name="properties-with-backing-fields"></a>지원 필드가 있는 속성

속성을 구현하는 한 가지 기본 패턴에는 private 지원 필드를 사용하여 속성 값을 설정 및 검색하는 작업이 포함됩니다. `get` 접근자는 private 필드의 값을 반환하고 `set` 접근자는 private 필드에 값을 할당하기 전에 데이터 유효성 검사를 수행할 수 있습니다. 또한 두 접근자 모두 데이터를 저장 또는 반환하기 전에 데이터에 대한 변환이나 계산을 수행할 수도 있습니다.

다음 예제에서 이 방법을 보여 줍니다. 이 예제에서 `TimePeriod` 클래스는 시간 간격을 나타냅니다. 내부적으로 이 클래스는 `_seconds`라는 private 필드에 시간 간격을 초 단위로 저장합니다. `Hours`라는 읽기/쓰기 속성을 사용하면 고객이 시간 간격을 시간 단위로 지정할 수 있습니다. `get` 및 `set` 접근자 모두 필요에 따라 시간 및 초 간의 변환을 수행합니다. 또한 `set` 접근자는 데이터의 유효성을 검사하고 시간(시)이 잘못된 경우 <xref:System.ArgumentOutOfRangeException>을 throw합니다. 
   
 [!code-csharp[Properties#1](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/properties-1.cs)]  
  
## <a name="expression-body-definitions"></a>식 본문 정의  

 속성 접근자는 식의 결과를 할당하거나 반환하기만 하는 한 줄로 된 문으로 구성되는 경우가 많습니다. 이러한 속성은 식 본문 멤버로 구현할 수 있습니다. 식 본문 정의는 `=>` 기호와 속성에 할당하거나 속성에서 검색할 식으로 구성됩니다.

 C# 6부터 읽기 전용 속성에서 `get` 접근자를 식 본문 멤버로 구현할 수 있습니다. 이 경우 `get` 접근자 키워드나 `return` 키워드를 모두 사용하지 않습니다. 다음 예제에서는 읽기 전용 `Name` 속성을 식 본문 멤버로 구현합니다.

 [!code-csharp[Properties#2](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/properties-2.cs)]  

 C# 7.0부터 `get` 및 `set` 접근자 모두를 식 본문 멤버로 구현할 수 있습니다. 이 경우 `get` 및 `set` 키워드가 있어야 합니다. 다음 예제에서는 두 접근자에 대해 식 본문 정의를 사용하는 방법을 보여 줍니다. `return` 키워드는 `get` 접근자와 함께 사용하지 않습니다.
 
  [!code-csharp[Properties#3](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/properties-3.cs)]  

## <a name="auto-implemented-properties"></a>자동으로 구현된 속성

경우에 따라 `get` 속성과 `set` 접근자에서 지원 필드에 값을 할당하거나 지원 필드에서 값을 검색하기만 하고 추가 논리를 포함하지 않을 수 있습니다. 자동 구현 속성을 사용하면 코드를 간소화할 수 있을 뿐 아니라 C# 컴파일러에서 지원 필드를 투명하게 제공하도록 할 수 있습니다. 

속성에 `get` 및 `set` 접근자가 모두 포함된 경우 두 접근자를 모두 자동 구현해야 합니다. 구현을 제공하지 않고 `get` 및 `set` 키워드를 사용하여 자동 구현 속성을 정의합니다. 다음 예제에서는 `Name` 및 `Price`가 자동 구현 속성인 점만 제외하고 이전 예제와 동일합니다. 이 예제에서는 매개 변수화된 생성자도 제거하므로 이제 `SaleItem` 개체가 매개 변수 없는 생성자 및 [개체 이니셜라이저](object-and-collection-initializers.md)에 대한 호출을 통해 초기화됩니다.

  [!code-csharp[Properties#4](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/properties-4.cs)]  

## <a name="related-sections"></a>관련 단원  
  
- [속성 사용](./using-properties.md)  
  
- [인터페이스 속성](./interface-properties.md)  
  
- [속성 및 인덱서 비교](../indexers/comparison-between-properties-and-indexers.md)  
  
- [접근자 접근성 제한](./restricting-accessor-accessibility.md)  
  
- [자동으로 구현된 속성](./auto-implemented-properties.md)  
  
## <a name="c-language-specification"></a>C# 언어 사양  

자세한 내용은 [C# 언어 사양](../../language-reference/language-specification/index.md)의 [속성](~/_csharplang/spec/classes.md#properties)을 참조하세요. 언어 사양은 C# 구문 및 사용법에 대 한 신뢰할 수 있는 소스 됩니다.
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [속성 사용](./using-properties.md)
- [인덱서](../indexers/index.md)
- [get 키워드](../../language-reference/keywords/get.md)
- [set 키워드](../../language-reference/keywords/set.md)
