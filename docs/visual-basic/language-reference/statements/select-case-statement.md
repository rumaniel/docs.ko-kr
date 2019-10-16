---
title: Select...Case 문(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Select
- vb.Case
helpviewer_keywords:
- Select statement [Visual Basic]
- Case statement [Visual Basic]
- Select...Case statements
- conditional statements [Visual Basic], Select Case
- control flow [Visual Basic], branching
- Else keyword [Visual Basic], in Select...Case statements
- execution [Visual Basic], conditional
- To keyword [Visual Basic], in Select...Case statements
- Select Case statement [Visual Basic], Select...Case
- Select statement [Visual Basic], Select...Case
- Is operator [Visual Basic], in Select...Case statements
- branching [Visual Basic], conditional
- Case Else statement [Visual Basic], Select...Case
- End keyword [Visual Basic], Select Case statements
- Case statement [Visual Basic], Select...Case
ms.assetid: 68877b65-5419-4bf0-a465-20cd0e4c7d44
ms.openlocfilehash: 627318677270ba4ffa8ee430febea7ddf83bd245
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69957652"
---
# <a name="selectcase-statement-visual-basic"></a>Select...Case 문(Visual Basic)
식의 값에 따라 여러 문 그룹 중 하나를 실행 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
Select [ Case ] testexpression  
    [ Case expressionlist  
        [ statements ] ]  
    [ Case Else  
        [ elsestatements ] ]  
End Select  
```  
  
## <a name="parts"></a>요소  
  
|용어|정의|  
|---|---|  
|`testexpression`|필수 요소. 식. 기본 데이터 형식 (`Boolean` ,`Integer`,, ,,`Double`,,,,,,) 중 하나로 계산 되어야 합니다. `Date` `Decimal` `Char` `Byte` `Long` `Object` `SByte` `Short` `Single`,,, `String` 및`UShort`)가 있습니다. `UInteger` `ULong`|  
|`expressionlist`|`Case` 문에 필요 합니다. 에 대해 일치 하는 값을 `testexpression`나타내는 식 절의 목록입니다. 여러 식 절은 쉼표로 구분 됩니다. 각 절은 다음 형식 중 하나를 사용할 수 있습니다.<br /><br /> -   *expression1* `To` *expression2*<br />-   [ `Is` ] *comparisonoperator* *expression*<br />-   *expression*<br /><br /> 키워드를 `To` 사용 하 여에 대 한 `testexpression`일치 값 범위의 경계를 지정 합니다. 값 `expression1` 은의 `expression2`값 보다 작거나 같아야 합니다.<br /><br /> `=` 비교연산자`<>`(, `Is` `testexpression`,, ,`<=`또는)와 함께 키워드를 사용 하 여에 대 한 일치 값에 대 한 제한을 지정 합니다. `>=` `<` `>` 키워드를 제공 하지 않으면 comparisonoperator.equals 앞에 자동으로 삽입 됩니다. `Is`<br /><br /> 만 `expression` 지정 하는 폼은 *comparisonoperator.equals* 가 등호 (`=`) 인 특수 한 경우 `Is` 로 취급 됩니다. 이 폼은로 `testexpression`  =  `expression`평가 됩니다.<br /><br /> 의 식은 `expressionlist` 의 `testexpression` 형식으로 암시적으로 변환 가능 하 고 `comparisonoperator` 해당가 사용 되는 두 가지 형식에 적합 한 경우의 모든 데이터 형식일 수 있습니다.|  
|`statements`|선택 사항입니다. `Case` 가 `testexpression` 에서 절`expressionlist`과 일치 하는 경우이 실행 되는 하나 이상의 문입니다.|  
|`elsestatements`|선택 사항입니다. 가 `Case Else` 문의에있는절`Case` `testexpression` `expressionlist` 과 일치 하지 않는 경우 실행 되는 다음 문이 하나 이상 있습니다.|  
|`End Select`|...의 `Select`정의를 종료 합니다. `Case` 생성.|  
  
## <a name="remarks"></a>설명  
 가 `testexpression` `Case` `Case Else` `End Select` 절 `Case` 과 일치 하면 해당`Case` 문 다음에 오는 문이 다음, 또는 문으로 실행 됩니다. `expressionlist` 그런 다음 제어가 다음 `End Select`문으로 전달 됩니다. 가 `testexpression` 둘 이상의 `expressionlist` `Case` 절에 있는 절과 일치 하면 첫 번째 일치 항목 다음에 오는 문만 실행 됩니다.  
  
 `testexpression` `elsestatements` 문은다른문의와`expressionlist` 절 사이에 일치 하는 항목이 없는 경우 실행할를 소개 하는 데 사용 됩니다. `Case` `Case Else` 반드시 필요한 것은 아니지만 `Case Else` `Select Case` 생성에 문을 포함 하 여 예측할 `testexpression` 수 없는 값을 처리 하는 것이 좋습니다. `Case` 일치`testexpression`하 는 `End Select`절이 없고 문이없으면다음문으로제어가전달됩니다.`Case Else` `expressionlist`  
  
 각 `Case` 절에서 여러 식이나 범위를 사용할 수 있습니다. 예를 들어 다음 줄은 유효 합니다.  
  
 `Case 1 To 4, 7 To 9, 11, 13, Is > maxNumber`  
  
> [!NOTE]
> 및 문에 사용 되는 키워드는 개체 참조 비교에 사용 되는 [is 연산자](../../../visual-basic/language-reference/operators/is-operator.md)와 동일 하지 않습니다. `Is` `Case Else` `Case`  
  
 문자 문자열에 대해 범위와 여러 식을 지정할 수 있습니다. 다음 예에서는 "사과 `Case` "와 정확히 같은 문자열을 검색 하 고, "너트"와 "수프" 사이의 값을 알파벳 순서로 포함 하거나,의 `testItem`현재 값과 정확히 같은 값을 포함 합니다.  
  
 `Case "apples", "nuts" To "soup", testItem`  
  
 의 `Option Compare` 설정은 문자열 비교에 영향을 줄 수 있습니다. 에서 "사과" 및 "사과" 문자열은 동일한 것으로 간주 `Option Compare Binary`되지만에서는 그렇지 않습니다. `Option Compare Text`  
  
> [!NOTE]
> 여러 절이 있는 문은단락이라는동작을나타낼수`Case` 있습니다. Visual Basic는 절을 왼쪽에서 오른쪽으로 계산 하 고, 일치 `testexpression`하는을 생성 하는 경우 나머지 절은 계산 되지 않습니다. 단락을 통해 성능을 향상 시킬 수 있지만의 `expressionlist` 모든 식이 계산 될 것으로 예상 되는 경우 예기치 않은 결과가 발생할 수 있습니다. 단락에 대 한 자세한 내용은 [부울 식](../../../visual-basic/programming-guide/language-features/operators-and-expressions/boolean-expressions.md)을 참조 하세요.  
  
 `Case` 또는 `Exit Select` 문 블록 내의 코드에서 블록의 문을 더 이상 실행할 필요가 없는 경우 문을 사용 하 여 블록을 종료할 수 있습니다. `Case Else` 그러면 다음 `End Select`문으로 제어가 즉시 전송 됩니다.  
  
 `Select Case`구조는 중첩 될 수 있습니다. 중첩 `Select Case` 된 각 생성에는 일치 `End Select` 하는 문이 있어야 하며 중첩 된 외부 `Select Case` 생성 `Case` 의 `Case Else` 단일 또는 문 블록 내에 완전히 포함 되어야 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 `Select Case` 생성을 사용 하 여 변수 `number`값에 해당 하는 줄을 작성 합니다. 두 번째 `Case` 문에는의 `number`현재 값과 일치 하는 값이 포함 되어 있으므로 "Between 6 ~ 8" (포함)를 쓰는 문이 실행 됩니다.  
  
 [!code-vb[VbVbalrStatements#54](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#54)]  
  
## <a name="see-also"></a>참고자료

- <xref:Microsoft.VisualBasic.Interaction.Choose%2A>
- [End 문](../../../visual-basic/language-reference/statements/end-statement.md)
- [If...Then...Else 문](../../../visual-basic/language-reference/statements/if-then-else-statement.md)
- [Option Compare 문](../../../visual-basic/language-reference/statements/option-compare-statement.md)
- [Exit 문](../../../visual-basic/language-reference/statements/exit-statement.md)
