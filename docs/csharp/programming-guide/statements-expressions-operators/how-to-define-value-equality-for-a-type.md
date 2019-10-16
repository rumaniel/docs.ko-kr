---
title: '방법: 형식에 대한 값 일치 정의 - C# 프로그래밍 가이드'
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- overriding Equals method [C#]
- object equivalence [C#]
- Equals method [C#], overriding
- value equality [C#]
- equivalence [C#]
ms.assetid: 4084581e-b931-498b-9534-cf7ef5b68690
ms.openlocfilehash: 0e1c736c7a2826c1218cb078a6e9f874b3b72c3c
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64755014"
---
# <a name="how-to-define-value-equality-for-a-type-c-programming-guide"></a>방법: 형식에 대한 값 일치 정의(C# 프로그래밍 가이드)

클래스 또는 구조체를 정의할 때 형식에 대한 값 같음(또는 동등)의 사용자 지정 정의를 만드는 것이 적합한지 결정합니다. 일반적으로 형식의 개체를 일종의 컬렉션에 추가해야 하는 경우 또는 주요 용도가 필드 또는 속성 집합 저장인 경우 값 같음을 구현합니다. 형식의 모든 필드 및 속성 비교를 기준으로 값 같음의 정의를 만들거나, 하위 집합을 기준으로 정의를 만들 수 있습니다. 그러나 두 경우 모두, 클래스와 구조체 둘 다에서 구현이 동등의 5가지 사항을 따라야 합니다.  
  
1. `x.Equals(x)`가 `true`를 반환하는 경우 이를 반사 속성이라고 합니다.  
  
2. `x.Equals(y)`는 `y.Equals(x)`와 동일한 값을 반환합니다. 이를 대칭 속성이라고 합니다.  
  
3. `(x.Equals(y) && y.Equals(z))`가 `true`를 반환하면 `x.Equals(z)`가 `true`를 반환합니다. 이를 전이적 속성이라고 합니다.  
  
4. `x.Equals(y)`의 연속 호출은 x 및 y에서 참조하는 개체가 수정되지 않는 한 동일한 값이 반환됩니다.  
  
5. `x.Equals(null)`가 `false`를 반환하는 경우 그러나 `null.Equals(null)`는 예외를 throw하고 위의 규칙 번호 2를 따르지 않습니다.  
  
 정의하는 모든 구조체에는 <xref:System.Object.Equals%28System.Object%29?displayProperty=nameWithType> 메서드의 <xref:System.ValueType?displayProperty=nameWithType> 재정의에서 상속하는 값 같음의 기본 구현이 이미 있습니다. 이 구현은 리플렉션을 사용하여 형식의 모든 필드와 속성을 검사합니다. 이 구현은 올바른 결과를 생성하지만 해당 형식에 맞게 작성한 사용자 지정 구현에 비해 비교적 속도가 느립니다.  
  
 값 같음에 대한 구현 세부 정보는 클래스 및 구조체에서 서로 다릅니다. 그러나 클래스와 구조체는 둘 다 같음 구현을 위해 동일한 기본 단계가 필요합니다.  
  
1. [virtual](../../language-reference/keywords/virtual.md) <xref:System.Object.Equals%28System.Object%29?displayProperty=nameWithType> 메서드를 재정의합니다. 대부분의 경우 `bool Equals( object obj )` 구현에서 <xref:System.IEquatable%601?displayProperty=nameWithType> 인터페이스 구현인 형식별 `Equals` 메서드만 호출하면 됩니다. 2단계를 참조하세요.  
  
2. 형식별 `Equals` 메서드를 제공하여 <xref:System.IEquatable%601?displayProperty=nameWithType> 인터페이스를 구현합니다. 여기서 실제 동등 비교가 수행됩니다. 예를 들어 형식에서 한 개나 두 개의 필드만 비교하여 같음 정의를 결정할 수도 있습니다. `Equals`에서 예외를 throw하지 않습니다. 클래스만 해당: 이 메서드는 클래스에 선언된 필드만 검사해야 합니다. `base.Equals`를 호출하여 기본 클래스에 있는 필드를 검사해야 합니다. 형식이 <xref:System.Object>에서 직접 상속하는 경우에는 이 작업을 수행하지 마세요. <xref:System.Object.Equals%28System.Object%29?displayProperty=nameWithType>의 <xref:System.Object> 구현에서 참조 같음 검사를 수행합니다.  
  
3. 선택 사항이지만 권장됨: [==](../../language-reference/operators/equality-operators.md#equality-operator-) 및 [!=](../../language-reference/operators/equality-operators.md#inequality-operator-) 연산자를 오버로드합니다.  
  
4. 값이 같은 두 개체가 동일한 해시 코드를 생성하도록 <xref:System.Object.GetHashCode%2A?displayProperty=nameWithType>를 재정의합니다.  
  
5. 선택 사항: “보다 큼” 또는 “보다 작음”에 대한 정의를 지원하기 위해 형식에 대한 <xref:System.IComparable%601> 인터페이스를 구현하고 [<=](../../language-reference/operators/comparison-operators.md#less-than-or-equal-operator-) 및 [>=](../../language-reference/operators/comparison-operators.md#greater-than-or-equal-operator-) 연산자도 오버로드합니다.  
  
 뒤에 오는 첫 번째 예제에서는 클래스의 구현 방법을 보여 줍니다. 두 번째 예제에서는 구조체의 구현 방법을 보여 줍니다.  

## <a name="example"></a>예제

 다음 예제에서는 클래스(참조 형식)에서 값 같음을 구현하는 방법을 보여 줍니다.  
  
 [!code-csharp[csProgGuideStatements#19](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#19)]  
  
 클래스(참조 형식)에서 두 <xref:System.Object.Equals%28System.Object%29?displayProperty=nameWithType> 메서드의 기본 구현은 값이 같은지 검사하지 않고 참조가 같은지 비교합니다. 구현자가 가상 메서드를 재정의하는 경우 값 같음 의미 체계를 제공하기 위한 것입니다.  
  
 클래스에서 재정의하지 않는 경우에도 `==` 및 `!=` 연산자를 클래스와 함께 사용할 수 있습니다. 그러나 기본 동작은 참조가 같은지 검사하는 것입니다. 클래스에서 `Equals` 메서드를 오버로드하는 경우 `==` 및 `!=` 연산자를 오버로드해야 하지만 필수는 아닙니다.  

## <a name="example"></a>예제

 다음 예제에서는 구조체(값 형식)에서 값 같음을 구현하는 방법을 보여 줍니다.  
  
 [!code-csharp[csProgGuideStatements#20](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideStatements/CS/Statements.cs#20)]  
  
 구조체의 경우 <xref:System.Object.Equals%28System.Object%29?displayProperty=nameWithType>의 기본 구현(<xref:System.ValueType?displayProperty=nameWithType>의 재정의된 버전)에서 리플렉션을 통해 형식에 있는 모든 필드의 값을 비교하여 값이 같은지 검사합니다. 구현자가 구조체의 가상 `Equals` 메서드를 재정의하는 경우 값이 같은지 검사하는 보다 효율적인 수단을 제공하고 필요에 따라 구조체 필드 또는 속성의 하위 집합을 기준으로 비교하기 위한 것입니다.  
  
 [==](../../language-reference/operators/equality-operators.md#equality-operator-) 및 [!=](../../language-reference/operators/equality-operators.md#inequality-operator-) 연산자는 구조체에서 명시적으로 오버로드하지 않는 한 구조체에 대해 연산을 수행할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목

- [같음 비교](equality-comparisons.md)
- [C# 프로그래밍 가이드](../index.md)
