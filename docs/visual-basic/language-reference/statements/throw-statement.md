---
title: Throw 문(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Throw
helpviewer_keywords:
- structured exception handling, throw statements
- try-catch exception handling, throw statements
- throw statement [Visual Basic], about throw statements
- throwing exceptions, throw statement
- exception handling, throw statement
- On Error statement [Visual Basic], throwing exceptions
- throwing exceptions
- exception handling, unstructured
- throw statement [Visual Basic]
ms.assetid: a6e07406-5c8a-4498-87a2-8339f3651d62
ms.openlocfilehash: 9680700267f17c8e316de351fead61f1dc4aded0
ms.sourcegitcommit: 9ee6cd851b6e176a5811ea28ed0d5935c71950f9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68869017"
---
# <a name="throw-statement-visual-basic"></a>Throw 문(Visual Basic)

프로시저 내에서 예외를 throw 합니다.

## <a name="syntax"></a>구문

```vb
Throw [ expression ]
```

## <a name="part"></a>부분

`expression`\
Throw 되는 예외에 대 한 정보를 제공 합니다. `Catch` 문에 있으면 선택 사항이 고, 그렇지 않으면 필수입니다.

## <a name="remarks"></a>설명

문은 구조화 된 예외 처리 코드로 처리할 수 있는 예외를 throw 합니다 (`Try`... `Throw` `Catch`... ) 또는 비구조적 예외 처리 코드 (`On Error GoTo`)를 처리 합니다. `Finally` Visual Basic은 적절 한 `Throw` 예외 처리 코드를 찾을 때까지 호출 스택 위로 이동 하기 때문에 문을 사용 하 여 코드 내에서 오류를 트래핑할 수 있습니다.

식이 없는 `Catch` 문은문에서`Catch` 만 사용할 수 있으며,이 경우 문은 문에 의해 현재 처리 되 고 있는 예외를 다시 throw 합니다. `Throw`

`Throw` 문은 예외`expression` 에 대 한 호출 스택을 다시 설정 합니다. 을 `expression` 지정 하지 않으면 호출 스택이 변경 되지 않고 그대로 유지 됩니다. 속성을 <xref:System.Exception.StackTrace%2A> 통해 예외에 대 한 호출 스택에 액세스할 수 있습니다.

## <a name="example"></a>예제

다음 코드에서는 `Throw` 문을 사용 하 여 예외를 throw 합니다.

[!code-vb[VbVbalrStatements#84](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#84)]

## <a name="see-also"></a>참고자료

- [Try...Catch...Finally 문](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)
- [On Error 문](../../../visual-basic/language-reference/statements/on-error-statement.md)
