---
title: 비교 연산자(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.<>
- vb.>=
- vb.<=
- vb.>
- vb.<
helpviewer_keywords:
- greater than or equal to operator [Visual Basic]
- '>= operator [Visual Basic]'
- = operator [Visual Basic]
- < operator [Visual Basic]
- less than operator [Visual Basic]
- relational operators [Visual Basic], syntax
- Like operator [Visual Basic]
- <> operator [Visual Basic]
- '> operator [Visual Basic]'
- equal operator [Visual Basic]
- less than or equal to operator [Visual Basic]
- symbols, operators
- greater than operator [Visual Basic]
- comparing values [Visual Basic]
- operators [Visual Basic], relational
- string comparison [Visual Basic]
- not equal to comparison operator [Visual Basic]
- <= operator [Visual Basic]
- operators [Visual Basic], comparison
- Is operator [Visual Basic]
- comparison operators [Visual Basic], Visual Basic
ms.assetid: d6cb12a8-e52e-46a7-8aaf-f804d634a825
ms.openlocfilehash: ddb07bdf5f67e281847082ba4487568e9ba3c9f5
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69962241"
---
# <a name="comparison-operators-visual-basic"></a>비교 연산자(Visual Basic)
다음은 Visual Basic에 정의 된 비교 연산자입니다.

 `<`연산자

 `<=`연산자

 `>`연산자

 `>=`연산자

 `=`연산자

 `<>`연산자

 [Is 연산자](../../../visual-basic/language-reference/operators/is-operator.md)

 [IsNot 연산자](../../../visual-basic/language-reference/operators/isnot-operator.md)

 [Like 연산자](../../../visual-basic/language-reference/operators/like-operator.md)

 이러한 연산자는 두 식을 비교 하 여 같은지 여부와 그렇지 않은 경우의 차이점을 확인 합니다. `Is`, `IsNot` 및`Like` 은 별도의 도움말 페이지에 자세히 설명 되어 있습니다. 관계형 비교 연산자에 대해서는이 페이지에서 자세히 설명 합니다.

## <a name="syntax"></a>구문
  
```vb
result = expression1 comparisonoperator expression2  
result = object1 [Is | IsNot] object2  
result = string Like pattern  
```  
  
## <a name="parts"></a>요소
 `result`  
 필수 요소. 비교 결과를 나타내는 값입니다.`Boolean`

 `expression1`, `expression2`  
 필수 요소. 임의의 식입니다.

 `comparisonoperator`  
 필수 요소. 모든 관계형 비교 연산자입니다.

 `object1`, `object2`  
 필수 요소. 참조 개체 이름입니다.

 `string`  
 필수 요소. 임의의 `String` 식입니다.

 `pattern`  
 필수 요소. 모든 `String` 식 또는 문자 범위입니다.

## <a name="remarks"></a>설명
 다음 표에는 관계 비교 연산자 목록 및 `result` `False`가 `True` 인지 여부를 결정 하는 조건이 포함 되어 있습니다.

|연산자|`True`|`False`|
|--------------|---------------|----------------|
|`<`(보다 작음)|`expression1` < `expression2`|`expression1` >= `expression2`|
|`<=`(작거나 같음)|`expression1` <= `expression2`|`expression1` > `expression2`|
|`>`(보다 큼)|`expression1` > `expression2`|`expression1` <= `expression2`|
|`>=`(크거나 같음)|`expression1` >= `expression2`|`expression1` < `expression2`|
|`=`(같음)|`expression1` = `expression2`|`expression1` <> `expression2`|
|`<>`(같지 않음)|`expression1` <> `expression2`|`expression1` = `expression2`|

> [!NOTE]
> [= 연산자](../../../visual-basic/language-reference/operators/assignment-operator.md) 는 할당 연산자로도 사용 됩니다.

 연산자, 연산자 및`Like` 연산자에는 위의 표에 있는 연산자와 다른 특정 비교 기능이 있습니다. `IsNot` `Is`

## <a name="comparing-numbers"></a>숫자 비교
 형식의 `Single` 식을 형식 `Double` 중하`Double`나와 비교 하는 경우 식이로변환됩니다.`Single` 이 동작은 Visual Basic 6에서 발견 된 동작과 반대입니다.

 마찬가지로 `Decimal` 형식의 식을 or `Single` `Double` 형식의식과`Single` 비교할 때 `Double`식이 또는로 변환 됩니다. `Decimal` 식 `Decimal` 의 경우 1e-28 보다 작은 모든 소수 자릿수가 손실 될 수 있습니다. 이러한 소수 자릿수 값이 손실 되 면 두 값이 일치 하지 않는 것으로 간주 될 수 있습니다. 이러한 이유로 같음 (`=`)을 사용 하 여 두 개의 부동 소수점 변수를 비교할 때 주의 해야 합니다. 두 숫자 간의 차이에 대 한 절대값은 허용 가능한 작은 허용 오차 보다 작음을 테스트 하는 것이 더 안전 합니다.

### <a name="floating-point-imprecision"></a>부동 소수점 부정확
 부동 소수점 숫자를 사용 하는 경우 항상 메모리에 정확한 표현이 없다는 점에 유의 하세요. 이로 인해 값 비교 및 [Mod 연산자](../../../visual-basic/language-reference/operators/mod-operator.md)와 같은 특정 작업에서 예기치 않은 결과가 발생할 수 있습니다. 자세한 내용은 [데이터 형식 문제 해결](../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)을 참조 하세요.

## <a name="comparing-strings"></a>문자열 비교
 문자열을 비교 하는 경우 문자열 식은 `Option Compare` 설정에 따라 사전순 정렬 순서에 따라 평가 됩니다.

 `Option Compare Binary`문자에 대 한 내부 이진 표현에서 파생 된 정렬 순서에 대 한 문자열 비교를 기준으로 합니다. 정렬 순서는 코드 페이지에 의해 결정 됩니다. 다음 예제에서는 일반적인 이진 정렬 순서를 보여 줍니다.

 `A < B < E < Z < a < b < e < z < À < Ê < Ø < à < ê < ø`

 `Option Compare Text`응용 프로그램 로캘로 결정 되는 대/소문자를 구분 하지 않는 텍스트 정렬 순서에 대 한 문자열 비교를 기준으로 합니다. 앞의 예제 `Option Compare Text` 에서 문자를 설정 하 고 정렬 하는 경우 다음 텍스트 정렬 순서가 적용 됩니다.

 `(A=a) < (À= à) < (B=b) < (E=e) < (Ê= ê) < (Ø = ø) < (Z=z)`

### <a name="locale-dependence"></a>로캘 종속성
 를 설정 `Option Compare Text`하는 경우 문자열 비교의 결과는 응용 프로그램이 실행 되 고 있는 로캘에 따라 달라질 수 있습니다. 두 문자는 한 로캘에서 동일 하 게 비교 될 수 있지만 다른 로캘에서는 동일 하지 않을 수 있습니다. 문자열 비교를 사용 하 여 로그온 시도를 수락할지 여부와 같은 중요 한 결정을 내리는 경우 로캘 민감도에 대 한 경고를 표시 해야 합니다. 로캘을 고려 하 `Option Compare Binary` 여를 설정 <xref:Microsoft.VisualBasic.Strings.StrComp%2A>하거나 호출 하는 것이 좋습니다.

## <a name="typeless-programming-with-relational-comparison-operators"></a>관계형 비교 연산자를 사용한 관대 한 형식의 프로그래밍
 `Object` 에서`Option Strict On`식에 관계 비교 연산자를 사용할 수 없습니다. 가 `Option Strict` 이 `Off` 고`expression1` 또는 가식인경우런타임형식에따라비교방법이결정됩니다.`expression2` `Object` 다음 표에서는 피연산자의 런타임 형식에 따라 식을 비교 하 고 비교 결과를 보여 줍니다.

|피연산자가|비교|
|---------------------|-------------------|
|양방향`String`|문자열 정렬 특성을 기반으로 하는 정렬 비교|
|두 숫자|숫자 비교로 `Double`변환 된 개체입니다.|
|숫자 1 개`String`|는로 변환 `String` 되 고`Double` 숫자 비교가 수행 됩니다. 을 로`Double` `String` 변환할수없으면<xref:System.InvalidCastException> 이 throw 됩니다.|
|둘 중 하나 또는 둘 다가 아닌 참조 형식입니다.`String`|<xref:System.InvalidCastException>이 throw됩니다.|

 숫자 비교는 `Nothing` 0으로 처리 됩니다. 문자열 비교는 `Nothing` ( `""` 빈 문자열)로 처리 됩니다.

## <a name="overloading"></a>오버로딩
 관계형 비교 연산자 (`<`. `<=``>` ,,`<>`,,)를 오버 로드할 수 있습니다. 즉, 피연산자가 해당 클래스 또는 구조체의 형식일 때 클래스 또는 구조체에서 해당 동작을 재정의할 수 있습니다. `=` `>=` 코드가 이러한 클래스 또는 구조체에서 이러한 연산자를 사용 하는 경우 다시 정의 된 동작을 이해 해야 합니다. 자세한 내용은 [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)을 참조하세요.

 [= 연산자](../../../visual-basic/language-reference/operators/assignment-operator.md) 는 할당 연산자가 아닌 관계형 비교 연산자로만 오버 로드 될 수 있습니다.

## <a name="example"></a>예제
 다음 예에서는 식을 비교 하는 데 사용 하는 다양 한 관계형 비교 연산자 사용을 보여 줍니다. 관계형 비교 연산자는 명시 `Boolean` 된 식이로 `True`계산 되는지 여부를 나타내는 결과를 반환 합니다. 문자열에 `>` 및 `<` 연산자를 적용 하는 경우 문자열의 일반적인 사전순 정렬 순서를 사용 하 여 비교가 수행 됩니다. 이 순서는 로캘 설정에 따라 달라질 수 있습니다. 정렬에서 대/소문자를 구분 하는지 여부는 [옵션 비교](../../../visual-basic/language-reference/statements/option-compare-statement.md) 설정에 따라 달라 집니다.

 [!code-vb[VbVbalrOperators#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#1)]

 앞의 예제에서 첫 번째 비교는을 `False` 반환 하 고 나머지 `True`비교는를 반환 합니다.

## <a name="see-also"></a>참고자료

- <xref:System.InvalidCastException>
- [= 연산자](../../../visual-basic/language-reference/operators/assignment-operator.md)
- [Visual Basic에서의 연산자 우선 순위](../../../visual-basic/language-reference/operators/operator-precedence.md)
- [기능별 연산자 목록](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)
- [데이터 형식 문제 해결](../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)
- [Visual Basic의 비교 연산자](../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)
