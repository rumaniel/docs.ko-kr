---
title: 오류 형식(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- exceptions, types
- errors [Visual Basic], types
- errors [Visual Basic], logic
- errors [Visual Basic], syntax
- logic errors [Visual Basic], Visual Basic
- run-time errors [Visual Basic], types of errors
- syntax errors [Visual Basic], Visual Basic
ms.assetid: 3048aabf-8c97-4e13-9150-853769cb5f6f
ms.openlocfilehash: ab554b60f7ba44ee0b92b76e1362ffdbb25f2afb
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69965364"
---
# <a name="error-types-visual-basic"></a>오류 형식(Visual Basic)
Visual Basic 오류는 구문 오류, 런타임 오류 및 논리 오류의 세 가지 범주 중 하나에 속합니다.

## <a name="syntax-errors"></a>구문 오류
 *구문 오류* 는 코드를 작성 하는 동안 표시 되는 오류입니다. Visual Studio를 사용 하는 경우 코드 **편집기** 창에서 코드 Visual Basic를 입력할 때 코드를 확인 하 고 단어의 철자를 잘못 입력 하거나 언어 요소를 잘못 사용 하는 등 실수를 할 수 있습니다. 명령줄에서 컴파일하는 경우 Visual Basic 구문 오류에 대 한 정보와 함께 컴파일러 오류가 표시 됩니다. 구문 오류는 가장 일반적인 오류 유형입니다. 코딩 환경에서이를 쉽게 수정할 수 있습니다.

> [!NOTE]
> 문은 `Option Explicit` 구문 오류를 방지 하는 한 가지 방법입니다. 응용 프로그램에서 사용 되는 모든 변수를 미리 선언 합니다. 따라서 코드에서 이러한 변수를 사용 하는 경우에는 모든 입력 오류를 즉시 catch 하 고 수정할 수 있습니다.

## <a name="run-time-errors"></a>런타임 오류
 *런타임 오류* 는 코드를 컴파일하고 실행 한 후에만 표시 되는 오류입니다. 여기에는 구문 오류가 없지만 실행 되지 않는 것 처럼 보이는 코드가 포함 됩니다. 예를 들어 파일을 여는 코드 줄을 올바르게 작성할 수 있습니다. 그러나 파일이 없으면 응용 프로그램에서 파일을 열 수 없으며 예외를 throw 합니다. 잘못 된 코드를 다시 작성 하거나 [예외 처리](../../language-reference/statements/try-catch-finally-statement.md)를 사용 하 여 대부분의 런타임 오류를 수정한 다음 다시 컴파일하고 다시 실행할 수 있습니다.
  
## <a name="logic-errors"></a>논리 오류
 *논리 오류* 는 응용 프로그램을 사용 하 고 있는 경우 표시 되는 오류입니다. 대부분의 경우 개발자가 수행 하는 가장 일반적인 잘못 된 가정과 사용자 동작에 대 한 응답으로 원치 않거나 예기치 않은 결과가 발생 합니다. 예를 들어 잘못 입력 한 키는 메서드에 잘못 된 정보를 제공할 수 있으며, 그렇지 않은 경우에는 메서드에 올바른 값이 항상 제공 된다고 가정할 수 있습니다. [예외 처리](../../language-reference/statements/try-catch-finally-statement.md) 를 사용 하 여 논리 오류를 처리할 수 있지만 (예: 인수가 `Nothing` <xref:System.ArgumentNullException>인지 여부를 테스트 하는 경우), 가장 일반적으로 논리 오류를 수정 하 고 다시 컴파일하면 프로그램별.

## <a name="see-also"></a>참고자료

- [Try...Catch...Finally 문](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)
- [디버거 기본 사항](/visualstudio/debugger/debugger-basics)
