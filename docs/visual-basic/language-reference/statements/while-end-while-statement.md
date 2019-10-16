---
title: While...End While 문(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.While
- vb.While...EndWhile
helpviewer_keywords:
- While statement [Visual Basic], While...End While
- While statement [Visual Basic]
- While...End While statements [Visual Basic]
ms.assetid: b931d1ce-e8ed-44d8-a13d-92a4f5458a1e
ms.openlocfilehash: 7ea0814c587f65ddc1f114d2314ac7147143d40d
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69965808"
---
# <a name="whileend-while-statement-visual-basic"></a>While...End While 문(Visual Basic)
지정 된 조건이 인 `True`동안 일련의 문을 실행 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
While condition  
    [ statements ]  
    [ Continue While ]  
    [ statements ]  
    [ Exit While ]  
    [ statements ]  
End While  
```  
  
## <a name="parts"></a>요소  
  
|용어|정의|  
|---|---|  
|`condition`|필수 요소. `Boolean` 식입니다. 가 이면 Visual Basic는로 `False`처리 합니다. `Nothing` `condition`|  
|`statements`|선택 사항입니다. 다음 `While`에 실행 되는 하나 이상의 문 ( `condition` 가 일 `True`때마다 실행 됨)|  
|`Continue While`|선택 사항입니다. `While` 블록의 다음 반복으로 제어를 전달 합니다.|  
|`Exit While`|선택 사항입니다. `While` 블록 밖으로 제어를 전송 합니다.|  
|`End While`|필수 요소. `While` 블록의 정의를 종료합니다.|  
  
## <a name="remarks"></a>설명  
 조건이 유지 `While...End While` `True`되는 한 문 집합을 무한 횟수로 반복 하려는 경우 구조를 사용 합니다. 조건을 테스트 하는 위치 또는 테스트 결과를 보다 유연 하 게 하려는 경우 다음을 수행 하는 것이 좋습니다. [ Loop 문](../../../visual-basic/language-reference/statements/do-loop-statement.md). 이 문을 설정 된 횟수 만큼 반복 하려면 [For ... 다음 문을](../../../visual-basic/language-reference/statements/for-next-statement.md) 일반적으로 선택 하는 것이 좋습니다.  
  
> [!NOTE]
> `While` 키워드는 다음에도 사용 됩니다. [ Loop 문](../../../visual-basic/language-reference/statements/do-loop-statement.md), [Skip while 절](../../../visual-basic/language-reference/queries/skip-while-clause.md) 및 [Take while 절](../../../visual-basic/language-reference/queries/take-while-clause.md)  
  
 가 이면 문이 발생할 때까지 `statements` 모든가 실행 됩니다. `End While` `True` `condition` 그런 다음 제어가 `While` 문으로 반환 되 고 `condition` 다시 검사 됩니다. `condition` 가 여전히`True`이면 프로세스가 반복 됩니다. 인 경우 제어는 `End While` 문 다음에 오는 문으로 전달 됩니다. `False`  
  
 `While` 문은 루프를 시작 하기 전에 항상 조건을 확인 합니다. 조건이 유지 `True`되는 동안 반복이 계속 됩니다. 루프 `condition` 를 `False` 처음 입력할 때가 이면 한 번도 실행 되지 않습니다.  
  
 는 `condition` 일반적으로 두 값을 비교 하 여 발생 하지만 [부울 데이터 형식](../../../visual-basic/language-reference/data-types/boolean-data-type.md) 값 (`True` 또는 `False`)으로 계산 되는 모든 식일 수 있습니다. 이 식에는로 `Boolean`변환 된 숫자 형식과 같은 다른 데이터 형식의 값이 포함 될 수 있습니다.  
  
 루프 하나를 `While` 다른 루프에 배치 하 여 루프를 중첩할 수 있습니다. 서로 다른 종류의 제어 구조를 중첩할 수도 있습니다. 자세한 내용은 [중첩 컨트롤 구조](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)를 참조 하세요.  
  
## <a name="exit-while"></a>종료 중  
 [Exit While](../../../visual-basic/language-reference/statements/exit-statement.md) 문은 루프를 `While` 종료 하는 다른 방법을 제공할 수 있습니다. `Exit While``End While` 문 다음에 오는 문으로 제어를 즉시 전송 합니다.  
  
 특정 조건 ( `Exit While` 예: `If...Then...Else` 구조체)을 평가한 후에 일반적으로를 사용 합니다. 오류가 발생 하거나 종료 요청 등의 반복을 계속할 수 없게 하는 조건을 감지 하는 경우 루프를 종료할 수 있습니다. 매우 크거나 무한 `Exit While` 한 번 실행 될 수 있는 루프로 *무한 루프*를 발생 시킬 수 있는 조건을 테스트할 때를 사용할 수 있습니다. 그런 다음를 사용 `Exit While` 하 여 루프를 이스케이프할 수 있습니다.  
  
 루프의 어디에 든 원하는 `Exit While` 개수의 문을 넣을 수 있습니다. `While`  
  
 중첩 `While` 된 루프 내에서 사용 `Exit While` 되는 경우 가장 안쪽의 루프와 그 다음으로 높은 중첩 수준으로 제어를 전달 합니다.  
  
 `Continue While` 문은 즉시 루프의 다음 반복으로 제어를 전달 합니다. 자세한 내용은 [Continue 문](../../../visual-basic/language-reference/statements/continue-statement.md)을 참조 하세요.  
  
## <a name="example"></a>예제  
 다음 예제에서 루프의 문은 `index` 변수가 10 보다 클 때까지 계속 실행 됩니다.  
  
 [!code-vb[VbVbalrStatements#171](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class14.vb#171)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 `Continue While` 및 `Exit While` 문을 사용 하는 방법을 보여 줍니다.  
  
 [!code-vb[VbVbalrStatements#172](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class14.vb#172)]  
  
## <a name="example"></a>예제  
 다음 예에서는 텍스트 파일의 모든 줄을 읽습니다. 메서드 <xref:System.IO.File.OpenText%2A> 는 파일을 열고 문자를 읽는 <xref:System.IO.StreamReader> 를 반환 합니다. 조건에서 <xref:System.IO.StreamReader.Peek%2A> 의`StreamReader` 메서드는 파일이 추가 문자를 포함 하는지 여부를 확인 합니다. `While`  
  
 [!code-vb[VbVbalrStatements#173](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class14.vb#173)]  
  
## <a name="see-also"></a>참고자료

- [루프 구조](../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)
- [Do...Loop 문](../../../visual-basic/language-reference/statements/do-loop-statement.md)
- [For...Next 문](../../../visual-basic/language-reference/statements/for-next-statement.md)
- [Boolean 데이터 형식](../../../visual-basic/language-reference/data-types/boolean-data-type.md)
- [중첩 제어 구조](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)
- [Exit 문](../../../visual-basic/language-reference/statements/exit-statement.md)
- [Continue 문](../../../visual-basic/language-reference/statements/continue-statement.md)
