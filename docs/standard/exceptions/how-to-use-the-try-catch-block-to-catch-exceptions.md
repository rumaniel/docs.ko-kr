---
title: '방법: Try-Catch 블록을 사용하여 예외 catch'
ms.date: 02/06/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- exceptions, try/catch blocks
- try blocks
- try/catch blocks
- catch blocks
ms.assetid: a3ce6dfd-1f64-471b-8ad8-8cfaf406275d
author: mairaw
ms.author: mairaw
ms.openlocfilehash: eaa389f461e70aae41f2e09437fd725a3bcefa5e
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71696728"
---
# <a name="how-to-use-the-trycatch-block-to-catch-exceptions"></a>try/catch 블록을 사용하여 예외를 catch하는 방법

예외를 발생시키거나 throw할 수 있는 모든 코드 문을 `try` 블록에 배치하고, 예외를 처리하는 데 사용되는 명령문을 `try` 블록 아래에 있는 하나 이상의 `catch` 블록에 배치합니다. 각 `catch` 블록은 예외 형식을 포함하고 해당 예외 형식을 처리하는 데 필요한 추가 명령문을 포함할 수 있습니다.

다음 예제에서 <xref:System.IO.StreamReader>는 *data.txt*라는 파일을 열고 해당 파일에서 줄을 검색합니다. 코드는 세 가지 예외 중 하나를 throw할 수 있으므로 `try` 블록에 위치합니다. 세 개 `catch` 블록이 예외를 catch하고 콘솔에 결과를 표시하여 예외를 처리합니다.

[!code-csharp[CatchException#3](~/samples/snippets/csharp/VS_Snippets_CLR/CatchException/CS/catchexception2.cs#3)]
[!code-vb[CatchException#3](~/samples/snippets/visualbasic/VS_Snippets_CLR/CatchException/VB/catchexception2.vb#3)]

CLR(공용 언어 런타임)은 `catch` 블록에서 처리되지 않은 예외를 catch합니다. CLR에서 예외를 catch하는 경우 CLR 구성에 따라 다음 결과 중 하나가 발생할 수 있습니다.

- **디버그** 대화 상자가 나타납니다.
- 프로그램이 실행을 중지하고 예외 정보가 포함된 대화 상자가 나타납니다.
- 오류가 [표준 오류 출력 스트림](xref:System.Console.Error)으로 출력됩니다.

> [!NOTE]
> 대부분의 코드가 예외를 throw할 수 있고, <xref:System.OutOfMemoryException>과 같은 일부 예외는 언제든지 CLR에서 throw될 수 있습니다. 애플리케이션은 이러한 예외를 처리할 필요가 없지만 다른 사용자가 사용할 라이브러리를 작성하는 경우 이러한 가능성에 유의해야 합니다. `try` 블록에서 코드를 설정하는 경우에 대한 제안 사항은 [예외에 대한 모범 사례](best-practices-for-exceptions.md)를 참조하세요.

## <a name="see-also"></a>참고 항목

- [예외](index.md)
- [.NET에서 I/O 오류 처리](../io/handling-io-errors.md)
