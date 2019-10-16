---
title: 예외 및 예외 처리 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- exception handling [C#]
- exceptions [C#]
- C# language, exceptions
ms.assetid: 0001887f-4fa2-47e2-8034-2819477e2344
ms.openlocfilehash: 1442daf646a29c3822d06d0b649f462b37523fe2
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72002119"
---
# <a name="exceptions-and-exception-handling-c-programming-guide"></a>예외 및 예외 처리(C# 프로그래밍 가이드)

C# 언어의 예외 처리 기능은 프로그램이 실행 중일 때 발생하는 예기치 않은 문제나 예외 상황을 처리하는 데 도움이 됩니다. 예외 처리는 `try`, `catch` 및 `finally` 키워드를 사용하여 실패했을 수 있는 작업을 시도하고, 실패를 처리하는 것이 적절하다고 판단될 때 처리하고, 리소스를 정리합니다. 예외는 CLR(공용 언어 런타임), .NET Framework, 타사 라이브러리 또는 애플리케이션 코드에서 생성될 수 있습니다. 예외는 `throw` 키워드를 사용하여 생성됩니다.

대부분의 경우 코드에서 직접 호출한 메서드가 아니라 호출 스택에서 추가로 작동 중단된 다른 메서드에 의해 예외가 throw될 수 있습니다. 이 경우 CLR에서는 스택을 해제하고 특정 예외 형식에 대해 `catch` 블록이 있는 메서드를 찾은 다음 이러한 `catch` 블록을 먼저 실행합니다. 호출 스택에서 적절한 `catch` 블록을 찾지 못하면 프로세스를 종료하고 사용자에게 메시지를 표시합니다.

이 예제에서 메서드는 0으로 나누기를 테스트하고 오류를 catch합니다. 예외 처리를 사용하지 않을 경우 이 프로그램은 **DivideByZeroException이(가) 처리되지 않았습니다.** 오류를 나타내며 종료됩니다.

[!code-csharp[csProgGuideExceptions#18](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideExceptions/CS/Exceptions.cs#18)]

## <a name="exceptions-overview"></a>예외 개요

예외는 다음과 같은 속성을 갖습니다.  

- 모든 예외는 궁극적으로 `System.Exception`에서 파생되는 형식입니다.
- 예외를 throw할 수 있는 문 주위에 `try` 블록을 사용합니다.
- `try` 블록에서 예외가 발생하면 제어 흐름이 호출 스택에 있는 첫 번째 관련 예외 처리기로 이동됩니다. C#에서 `catch` 키워드는 예외 처리기를 정의하는 데 사용됩니다.
- 지정된 예외에 대한 예외 처리기가 없으면 프로그램은 오류 메시지를 나타내며 실행을 중지합니다.
- 예외를 처리하고 애플리케이션을 알려진 상태로 둘 수 없으면 예외를 catch하지 마세요. `System.Exception`을 catch하는 경우 `catch` 블록 끝에서 `throw` 키워드를 사용하여 다시 throw하세요.
- `catch` 블록이 예외 변수를 정의하는 경우 이 변수를 사용하여 발생한 예외 형식에 대한 추가 정보를 얻을 수 있습니다.
- `throw` 키워드를 사용하여 프로그램에서 명시적으로 예외를 생성할 수 있습니다.
- 예외 개체는 호출 스택의 상태 및 오류에 대한 텍스트 설명 같은 오류에 대한 자세한 정보를 포함합니다.
- `finally` 블록의 코드는 예외가 throw되더라도 실행됩니다. `finally` 블록을 사용하여 `try` 블록에서 열려 있는 스트림이나 파일을 닫는 것처럼 리소스를 해제합니다.
- .NET Framework의 관리되는 예외는 Win32 구조적 예외 처리 메커니즘을 토대로 구현됩니다. 자세한 내용은 [구조적 예외 처리(C/C++)](/cpp/cpp/structured-exception-handling-c-cpp) 및 [Win32 구조적 예외 처리에 대한 집중 과정](https://bytepointer.com/resources/pietrek_crash_course_depths_of_win32_seh.htm)을 참조하세요.

## <a name="related-sections"></a>관련 단원

예외 및 예외 처리에 대한 자세한 내용은 다음 아티클을 참조하세요.

- [예외 사용](using-exceptions.md)
- [예외 처리](exception-handling.md)
- [예외 만들기 및 Throw](creating-and-throwing-exceptions.md)
- [컴파일러 생성 예외](compiler-generated-exceptions.md)
- [방법: try/catch를 사용하여 예외 처리(C# 프로그래밍 가이드)](how-to-handle-an-exception-using-try-catch.md)
- [방법: finally를 사용하여 정리 코드 실행](how-to-execute-cleanup-code-using-finally.md)
- [방법: CLS 규격이 아닌 예외 catch](how-to-catch-a-non-cls-exception.md)를 참조하세요.

## <a name="c-language-specification"></a>C# 언어 사양

자세한 내용은 [C# 언어 사양](../../language-reference/language-specification/index.md)의 [예외](~/_csharplang/spec/exceptions.md)를 참조하세요. 언어 사양은 C# 구문 및 사용법에 대 한 신뢰할 수 있는 소스 됩니다.

## <a name="see-also"></a>참고 항목

- <xref:System.SystemException>
- [C# 프로그래밍 가이드](../index.md)
- [C# 키워드](../../language-reference/keywords/index.md)
- [throw](../../language-reference/keywords/throw.md)
- [try-catch](../../language-reference/keywords/try-catch.md)
- [try-finally](../../language-reference/keywords/try-finally.md)
- [try-catch-finally](../../language-reference/keywords/try-catch-finally.md)
- [예외](../../../standard/exceptions/index.md)
