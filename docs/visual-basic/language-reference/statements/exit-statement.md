---
title: Exit 문(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Exit
helpviewer_keywords:
- execution [Visual Basic], ending
- files [Visual Basic], closing
- programs [Visual Basic], quitting
- code, exiting
- Exit statement [Visual Basic]
- program termination
- execution [Visual Basic], stopping
ms.assetid: 760bfb32-5c3f-4bdb-a432-9a6001c92db7
ms.openlocfilehash: 9c25653809c51662ea5b606ab97be6a9b50d5986
ms.sourcegitcommit: 7bfe1682d9368cf88d43e895d1e80ba2d88c3a99
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71956939"
---
# <a name="exit-statement-visual-basic"></a>Exit 문(Visual Basic)

프로시저 또는 블록을 종료 하 고 프로시저 호출 또는 블록 정의 다음에 오는 문으로 제어를 즉시 전달 합니다.

## <a name="syntax"></a>구문

```vb
Exit { Do | For | Function | Property | Select | Sub | Try | While }
```

## <a name="statements"></a>문

 `Exit Do`  
 이 표시 되는 `Do` 루프가 즉시 종료 됩니다. @No__t-0 문 다음에 오는 문을 사용 하 여 실행이 계속 됩니다. `Exit Do`은 `Do` 루프 내 에서만 사용할 수 있습니다. 중첩 된 `Do` 루프 내에서 사용 하는 경우 `Exit Do`은 가장 안쪽의 루프를 종료 하 고 다음으로 높은 중첩 수준으로 제어를 전달 합니다.

 `Exit For`  
 이 표시 되는 `For` 루프가 즉시 종료 됩니다. @No__t-0 문 다음에 오는 문을 사용 하 여 실행이 계속 됩니다. `For` @no__t `Next` 또는 `For Each` ... @no__t 루프 내 에서만 사용할 수 있습니다. 중첩 된 `For` 루프 내에서 사용 하는 경우 `Exit For`은 가장 안쪽의 루프를 종료 하 고 다음으로 높은 중첩 수준으로 제어를 전달 합니다.

 `Exit Function`  
 는 표시 되는 `Function` 프로시저를 즉시 종료 합니다. @No__t-0 프로시저를 호출한 문 뒤에 오는 문에서 실행이 계속 됩니다. `Exit Function`은 `Function` 프로시저 내 에서만 사용할 수 있습니다.

 반환 값을 지정 하려면 `Exit Function` 문 앞의 줄에서 함수 이름에 값을 할당할 수 있습니다. 반환 값을 할당 하 고 한 문에서 함수를 종료 하려면 [Return 문을](return-statement.md)대신 사용할 수 있습니다.

 `Exit Property`  
 는 표시 되는 `Property` 프로시저를 즉시 종료 합니다. @No__t-0 프로시저를 호출한 문 즉, 속성의 값을 요청 하거나 설정 하는 문을 사용 하 여 실행이 계속 됩니다. `Exit Property`은 속성의 `Get` 또는 `Set` 프로시저 내 에서만 사용할 수 있습니다.

 @No__t-0 프로시저에서 반환 값을 지정 하려면 `Exit Property` 문 앞의 줄에서 함수 이름에 값을 할당할 수 있습니다. 반환 값을 할당 하 고 한 문에서 `Get` 프로시저를 종료 하려면 `Return` 문을 대신 사용할 수 있습니다.

 @No__t-0 프로시저에서 `Exit Property` 문은 `Return` 문과 동일 합니다.

 `Exit Select`  
 는 표시 되는 `Select Case` 블록을 즉시 종료 합니다. @No__t-0 문 다음에 오는 문을 사용 하 여 실행이 계속 됩니다. `Exit Select`은 `Select Case` 문 내 에서만 사용할 수 있습니다.

 `Exit Sub`  
 는 표시 되는 `Sub` 프로시저를 즉시 종료 합니다. @No__t-0 프로시저를 호출한 문 뒤에 오는 문에서 실행이 계속 됩니다. `Exit Sub`은 `Sub` 프로시저 내 에서만 사용할 수 있습니다.

 @No__t-0 프로시저에서 `Exit Sub` 문은 `Return` 문과 동일 합니다.

 `Exit Try`  
 @No__t-0 또는 `Catch` 블록이 표시 되는 즉시 종료 합니다. @No__t-0 블록 (있는 경우)을 사용 하 여 실행을 계속 하거나, `End Try` 문 뒤에 문을 사용 합니다. `Exit Try`은 `Finally` 블록 내부가 아닌 `Try` 또는 `Catch` 블록 내 에서만 사용할 수 있습니다.

 `Exit While`  
 이 표시 되는 `While` 루프가 즉시 종료 됩니다. @No__t-0 문 다음에 오는 문을 사용 하 여 실행이 계속 됩니다. `Exit While`은 `While` 루프 내 에서만 사용할 수 있습니다. 중첩 된 `While` 루프 내에서 사용 되는 경우 `Exit While`은 `Exit While`가 발생 하는 루프 위에 중첩 된 한 수준으로 제어를 전달 합니다.

## <a name="remarks"></a>설명

@No__t-0 문을 `End` 문과 혼동 하지 마십시오. `Exit`은 문의 끝을 정의 하지 않습니다.

## <a name="example"></a>예제

다음 예제에서는 `index` 변수가 100 보다 큰 경우 루프 조건이 루프를 중지 합니다. 그러나 루프의 `If` 문은 인덱스 변수가 10 보다 클 때 `Exit Do` 문이 루프를 중지 합니다.

[!code-vb[VbVbalrStatements#133](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class10.vb#133)]

## <a name="example"></a>예제

다음 예에서는-0 @no__t 함수 이름에 반환 값을 할당 한 다음 `Exit Function`을 사용 하 여 함수에서 반환 합니다.

[!code-vb[VbVbalrStatements#23](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#23)]

## <a name="example"></a>예제

다음 예에서는 [Return 문을](return-statement.md) 사용 하 여 반환 값을 할당 하 고 함수를 종료 합니다.

[!code-vb[VbVbalrStatements#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#24)]

## <a name="see-also"></a>참조

- [Continue 문](continue-statement.md)
- [Do...Loop 문](do-loop-statement.md)
- [End 문](end-statement.md)
- [For Each...Next 문](for-each-next-statement.md)
- [For...Next 문](for-next-statement.md)
- [Function 문](function-statement.md)
- [Return 문](return-statement.md)
- [Stop 문](stop-statement.md)
- [Sub 문](sub-statement.md)
- [Try...Catch...Finally 문](try-catch-finally-statement.md)
