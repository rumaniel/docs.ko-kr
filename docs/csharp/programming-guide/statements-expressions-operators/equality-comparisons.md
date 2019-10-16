---
title: 같음 비교 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- object equality [C#]
ms.assetid: 10b865ea-4e7b-4127-9242-c9b8f57d9f04
ms.openlocfilehash: bc3ce4b94bfc72e058d4660d01eb16ef0e0f11db
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69588711"
---
# <a name="equality-comparisons-c-programming-guide"></a>같음 비교(C# 프로그래밍 가이드)

두 값이 같은지를 비교해야 하는 경우가 있습니다. 때로는 두 변수에 포함된 값이 같음을 의미하는 *값 같음*(*동등*이라고도 함)을 테스트합니다. 다른 경우에는 두 변수가 메모리에서 동일한 기본 개체를 참조하는지 여부를 확인해야 합니다. 이 유형의 같음을 *참조 같음* 또는 *ID*라고 합니다. 이 항목에서는 이러한 두 종류의 같음을 설명하고 자세한 정보가 있는 다른 항목에 대한 링크를 제공합니다.  
  
## <a name="reference-equality"></a>참조 같음

 참조 같음은 두 개체 참조가 동일한 기본 개체를 참조함을 의미합니다. 이러한 상황은 다음 예제와 같이 단순 할당을 통해 발생할 수 있습니다.  
  
 [!code-csharp[csProgGuideStatements#18](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#18)]  
  
 이 코드에서는 두 개체가 생성되지만 대입문 이후 두 참조가 동일한 개체를 참조합니다. 따라서 참조 같음이 있습니다. 두 참조가 동일한 개체를 참조하는지 확인하려면 <xref:System.Object.ReferenceEquals%2A> 메서드를 사용합니다.  
  
 참조 같음의 개념은 참조 형식에만 적용됩니다. 값 형식의 인스턴스가 변수에 할당될 때 값의 복사본이 생성되기 때문에 값 형식 개체에는 참조 같음이 있을 수 없습니다. 따라서 메모리의 동일한 위치를 참조하는 두 개의 unboxed 구조체가 있을 수 없습니다. 또한 <xref:System.Object.ReferenceEquals%2A>를 사용하여 두 개의 값 형식을 비교하는 경우 개체에 포함된 값이 모두 동일한 경우에도 결과는 항상 `false`입니다. 각 변수가 별도의 개체 인스턴스에 boxed되기 때문입니다. 자세한 내용은 [방법: 참조 같음(ID) 테스트](./how-to-test-for-reference-equality-identity.md)를 참조하세요.  

## <a name="value-equality"></a>값 같음

 값 같음은 두 개체에 동일한 값이 포함되어 있음을 의미합니다. [int](../../language-reference/builtin-types/integral-numeric-types.md) 또는 [bool](../../language-reference/keywords/bool.md)과 같은 기본 값 형식의 경우 값 같음 테스트가 간단합니다. 다음 예제와 같이 [==](../../language-reference/operators/equality-operators.md#equality-operator-) 연산자를 사용할 수 있습니다.  
  
```csharp  
int a = GetOriginalValue();  
int b = GetCurrentValue();  
  
// Test for value equality.   
if( b == a)   
{  
    // The two integers are equal.  
}  
```  
  
 대부분의 다른 형식에서는 값 같음 테스트가 더 복잡한데, 형식에서 정의된 방식을 알아야 하기 때문입니다. 여러 필드나 속성이 있는 클래스 및 구조체의 경우 값 같음은 대체로 모든 필드 또는 속성에 동일한 값이 있다는 의미로 정의됩니다. 예를 들어 pointA.X가 pointB.X와 같고 pointA.Y가 pointB.Y와 같으면 두 `Point` 개체가 동일한 것으로 정의할 수 있습니다.  
  
 그러나 동등이 형식의 모든 필드를 기반으로 해야 한다는 요구 사항은 없습니다. 하위 집합을 기반으로 할 수도 있습니다. 소유하지 않은 형식을 비교하는 경우 해당 형식에 대해 동등이 정의된 방식을 구체적으로 알아야 합니다. 사용자 고유의 클래스 및 구조체에서 값 같음을 정의하는 방법에 대한 자세한 내용은 [방법: 형식의 값 일치 정의](./how-to-define-value-equality-for-a-type.md)를 참조하세요.  
  
### <a name="value-equality-for-floating-point-values"></a>부동 소수점 값에 대한 값 같음

 이진 컴퓨터의 부정확한 부동 소수점 연산 때문에 부동 소수점 값([double](../../language-reference/builtin-types/floating-point-numeric-types.md) 및 [float](../../language-reference/builtin-types/floating-point-numeric-types.md))의 같음 비교에서 문제가 발생합니다. 자세한 내용은 <xref:System.Double?displayProperty=nameWithType> 항목의 설명을 참조하세요.  
  
## <a name="related-topics"></a>관련 항목  
  
|제목|설명|  
|-----------|-----------------|  
|[방법: 참조 같음(ID) 테스트](./how-to-test-for-reference-equality-identity.md)|두 변수에 참조 같음이 있는지를 확인하는 방법을 설명 합니다.|  
|[방법: 형식의 값 일치 정의](./how-to-define-value-equality-for-a-type.md)|형식에 대한 값 같음의 사용자 지정 정의를 제공하는 방법을 설명합니다.|  
|[C# 프로그래밍 가이드](../index.md)|.NET Framework를 통해 C#에 제공되는 기능 및 중요한 C# 언어 기능에 대한 자세한 정보 링크를 제공합니다.|  
|[유형](../types/index.md)|C# 형식 시스템에 대한 정보 및 추가 정보 링크를 제공합니다.|  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
