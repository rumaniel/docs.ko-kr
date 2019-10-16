---
title: Do...Loop 문(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Do
- vb.Loop
- vb.Until
helpviewer_keywords:
- conditional statements [Visual Basic], Do�Loop
- while statement [Visual Basic], Do...Loop
- execution [Visual Basic], conditional
- Do loops
- Until keyword [Visual Basic], Do...Loop statement
- Do...Loop statement
- instructions, repeating
- Do statement [Visual Basic]
- Exit statement [Visual Basic], in Do...Loop statements
- loop structures [Visual Basic], Do�Loop statements
- do-while statements [Visual Basic]
- loops, exiting
- Loop keyword [Visual Basic], Do...Loop statement
ms.assetid: 892f9096-b3e2-4aee-834d-83bc4e2c379d
ms.openlocfilehash: 75a2129a9f332024831d97021e381f1b3d4fa048
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69942990"
---
# <a name="doloop-statement-visual-basic"></a>Do...Loop 문(Visual Basic)
조건이 이거나 조건이이 될 때까지 문 블록을반복합니다.`True` `True` `Boolean`  
  
## <a name="syntax"></a>구문  
  
```  
Do { While | Until } condition  
    [ statements ]  
    [ Continue Do ]  
    [ statements ]  
    [ Exit Do ]  
    [ statements ]  
Loop  
-or-  
Do  
    [ statements ]  
    [ Continue Do ]  
    [ statements ]  
    [ Exit Do ]  
    [ statements ]  
Loop { While | Until } condition  
```  
  
## <a name="parts"></a>요소  
  
|용어|정의|  
|---|---|  
|`Do`|필수 요소. `Do` 루프의 정의를 시작 합니다.|  
|`While`|`Until`를 사용하는 경우를 제외하고는 필수입니다. 가가 `condition` `False`될 때까지 루프를 반복 합니다.|  
|`Until`|`While`를 사용하는 경우를 제외하고는 필수입니다. 가가 `condition` `True`될 때까지 루프를 반복 합니다.|  
|`condition`|선택 사항입니다. `Boolean` 식입니다. 가 이면 Visual Basic는로 `False`처리 합니다. `Nothing` `condition`|  
|`statements`|선택 사항입니다. 또는 `condition` 가 인 `True`동안 반복 되는 하나 이상의 문입니다.|  
|`Continue Do`|선택 사항입니다. `Do` 루프의 다음 반복으로 제어를 전달 합니다.|  
|`Exit Do`|선택 사항입니다. `Do` 루프 외부로 제어를 전달 합니다.|  
|`Loop`|필수 요소. `Do` 루프의 정의를 종료 합니다.|  
  
## <a name="remarks"></a>설명  
 조건을 만족할 `Do...Loop` 때까지 문 집합을 무한 횟수로 반복 하려는 경우 구조를 사용 합니다. 이 문을 설정 된 횟수 만큼 반복 하려면 [For ... 다음 문을](../../../visual-basic/language-reference/statements/for-next-statement.md) 일반적으로 선택 하는 것이 좋습니다.  
  
 `condition`또는 `While` 중하나를사용하여`Until` 지정할 수 있습니다.  
  
 루프의 시작 `condition` 또는 끝에서 한 번만 테스트할 수 있습니다. 루프의 시작 `condition` 부분에서 테스트 하는 경우 ( `Do` 문에서) 루프가 한 번도 실행 되지 않을 수 있습니다. `Loop` 문에서 루프의 끝 부분에서 테스트 하는 경우 루프는 항상 한 번 이상 실행 됩니다.  
  
 조건은 일반적으로 두 값을 비교 하 여 발생 하지만 [부울 데이터 형식](../../../visual-basic/language-reference/data-types/boolean-data-type.md) 값 (`True` 또는 `False`)으로 계산 되는 모든 식일 수 있습니다. 여기에는로 `Boolean`변환 된 숫자 형식과 같은 다른 데이터 형식의 값이 포함 됩니다.  
  
 루프 하나를 `Do` 다른 루프에 배치 하 여 루프를 중첩할 수 있습니다. 서로 다른 종류의 제어 구조를 중첩할 수도 있습니다. 자세한 내용은 [중첩 컨트롤 구조](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)를 참조 하세요.  
  
> [!NOTE]
> 구조 `Do...Loop` 를 사용 하면 보다 유연성이 향상 됩니다. [ End While 문을](../../../visual-basic/language-reference/statements/while-end-while-statement.md) 사용 하면가 중지 `condition` `True` 될 때 루프를 종료할 것인지 아니면 처음 `True`에가 될 때 루프를 종료할 것인지를 결정할 수 있습니다. 또한 루프의 시작 또는 끝 `condition` 에서 테스트할 수 있습니다.  
  
## <a name="exit-do"></a>종료  
 [Exit Do](../../../visual-basic/language-reference/statements/exit-statement.md) 문은를 `Do…Loop`종료 하는 다른 방법을 제공할 수 있습니다. `Exit Do``Loop` 문 다음에 오는 문으로 제어를 즉시 전달 합니다.  
  
 `Exit Do`는 `If...Then...Else` 구조체와 같이 일부 조건을 평가한 후에 사용 되는 경우가 많습니다. 오류가 발생 하거나 종료 요청 등의 반복을 계속할 수 없게 하는 조건을 감지 하는 경우 루프를 종료할 수 있습니다. 를 사용 `Exit Do` 하는 한 가지 방법은 *무한 루프*를 발생 시킬 수 있는 조건을 테스트 하는 것입니다 .이는 무한 하거나 무한 한 횟수를 실행할 수 있는 루프입니다. 를 사용 `Exit Do` 하 여 루프를 이스케이프할 수 있습니다.  
  
 에는 `Exit Do` `Do…Loop`임의 개수의 문을 포함할 수 있습니다.  
  
 중첩 `Do` 된 루프 내에서 사용 `Exit Do` 되는 경우 가장 안쪽의 루프와 그 다음으로 높은 중첩 수준으로 제어를 전달 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서 루프의 문은 `index` 변수가 10 보다 클 때까지 계속 실행 됩니다. `Until` 절이 루프의 끝에 있습니다.  
  
 [!code-vb[VbVbalrStatements#131](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class10.vb#131)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 `Until` 절 대신 `While` 절을 사용 하 고 `condition` 끝이 아닌 루프의 시작 부분에서 테스트 됩니다.  
  
 [!code-vb[VbVbalrStatements#132](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class10.vb#132)]  
  
## <a name="example"></a>예제  
 다음 예제 `condition` 에서는 `index` 변수가 100 보다 큰 경우 루프를 중지 합니다. 그러나 루프의 문은 인덱스 변수가 10 보다 클 경우 문이루프를중지하도록합니다.`Exit Do` `If`  
  
 [!code-vb[VbVbalrStatements#133](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class10.vb#133)]  
  
## <a name="example"></a>예제  
 다음 예에서는 텍스트 파일의 모든 줄을 읽습니다. 메서드 <xref:System.IO.File.OpenText%2A> 는 파일을 열고 문자를 읽는 <xref:System.IO.StreamReader> 를 반환 합니다. 조건에서 <xref:System.IO.StreamReader.Peek%2A> 의`StreamReader` 메서드는 추가 문자가 있는지 여부를 확인 합니다. `Do...Loop`  
  
 [!code-vb[VbVbalrStatements#134](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class10.vb#134)]  
  
## <a name="see-also"></a>참고자료

- [루프 구조](../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)
- [For...Next 문](../../../visual-basic/language-reference/statements/for-next-statement.md)
- [Boolean 데이터 형식](../../../visual-basic/language-reference/data-types/boolean-data-type.md)
- [중첩 제어 구조](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)
- [Exit 문](../../../visual-basic/language-reference/statements/exit-statement.md)
- [While...End While 문](../../../visual-basic/language-reference/statements/while-end-while-statement.md)
