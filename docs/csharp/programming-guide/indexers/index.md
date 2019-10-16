---
title: 인덱서 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 03/10/2017
f1_keywords:
- cs.indexers
helpviewer_keywords:
- indexers [C#]
- C# language, indexers
ms.assetid: 022cd27d-d5e0-4cfe-8b97-dc018cc3355d
ms.openlocfilehash: f0df3170289d780852ee14232e92c3b71412c548
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392371"
---
# <a name="indexers-c-programming-guide"></a>인덱서(C# 프로그래밍 가이드)

인덱서에서는 클래스나 구조체의 인스턴스를 배열처럼 인덱싱할 수 있습니다. 인덱싱 값은 형식이나 인스턴스 멤버를 명시적으로 지정하지 않고도 설정하거나 검색할 수 있습니다. 인덱서는 해당 접근자가 매개 변수를 사용한다는 점을 제외하면 [속성](../classes-and-structs/properties.md)과 유사합니다.  

 다음 예제에서는 간단한 [get](../../language-reference/keywords/get.md) 및 [set](../../language-reference/keywords/set.md) 접근자 메서드를 사용해서 값을 할당하거나 검색하는 제네릭 클래스를 정의합니다. `Program` 클래스는 이 클래스의 인스턴스를 만들어 문자열을 저장합니다.  
  
 [!code-csharp[indexers#1](../../../../samples/snippets/csharp/programming-guide/indexers/indexer-1.cs)]  
  
> [!NOTE]
> 추가 예제는 [관련 섹션](./index.md#BKMK_RelatedSections)을 참조하세요.  
  
## <a name="expression-body-definitions"></a>식 본문 정의  
 
인덱서의 get 또는 set 접근자는 값을 반환하거나 설정하는 단일 문으로 구성되는 것이 일반적입니다. 식 본문이 있는 멤버는 이 시나리오를 지원하기 위해 간단한 구문을 제공합니다. C# 6부터 읽기 전용 인덱서는 다음 예제와 같이 식 본문이 있는 멤버로 구현할 수 있습니다.

[!code-csharp[indexers#2](../../../../samples/snippets/csharp/programming-guide/indexers/indexer-2.cs)]  

`=>`에서 식 본문을 도입하며 `get` 키워드는 사용되지 않습니다. 

C# 7.0부터 get 및 set 접근자 모두를 식 본문 멤버로 구현할 수 있습니다. 이 경우 `get` 및 `set` 키워드를 둘 다 사용해야 합니다. 예:

[!code-csharp[indexers#3](../../../../samples/snippets/csharp/programming-guide/indexers/indexer-3.cs)]  
  
## <a name="indexers-overview"></a>인덱서 개요  
  
- 인덱서를 사용하면 배열과 유사한 방식으로 개체를 인덱싱할 수 있습니다.  
  
- `get` 접근자는 값을 반환합니다. `set` 접근자는 값을 할당합니다.  
  
- [this](../../language-reference/keywords/this.md) 키워드는 인덱서를 정의하는 데 사용됩니다.  
  
- [value](../../language-reference/keywords/value.md) 키워드는 `set` 인덱서에서 할당하는 값을 정의하는 데 사용됩니다.  
  
- 인덱서는 정수 값으로 인덱싱될 필요가 없으며, 특정 조회 메커니즘을 정의하는 방법을 결정해야 합니다.  
  
- 인덱서는 오버로드될 수 있습니다.  
  
- 예를 들어 인덱서는 2차원 배열에 액세스하는 경우 둘 이상의 정식 매개 변수를 사용할 수 있습니다.  
  
## <a name="BKMK_RelatedSections"></a> 관련 섹션  
  
- [인덱서 사용](./using-indexers.md)  
  
- [인터페이스의 인덱서](./indexers-in-interfaces.md)  
  
- [속성 및 인덱서 비교](./comparison-between-properties-and-indexers.md)  
  
- [접근자 접근성 제한](../classes-and-structs/restricting-accessor-accessibility.md)  
  
## <a name="c-language-specification"></a>C# 언어 사양  

자세한 내용은 [C# 언어 사양](../../language-reference/language-specification/index.md)의 [인덱서](~/_csharplang/spec/classes.md#indexers)를 참조하세요. 언어 사양은 C# 구문 및 사용법에 대 한 신뢰할 수 있는 소스 됩니다.
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [속성](../classes-and-structs/properties.md)
