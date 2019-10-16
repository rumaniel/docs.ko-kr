---
title: '방법: 명시적으로 예외 Throw'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- exceptions, try/catch blocks
- FileNotFoundException class
- try/catch blocks
- exceptions, throwing
- implicitly throwing exceptions
ms.assetid: 72bdd157-caa9-4478-9ee3-cb4500b84528
author: mairaw
ms.author: mairaw
ms.openlocfilehash: a71cefc0a6483dbbe6513a64d8111a07a2e5af42
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71696736"
---
# <a name="how-to-explicitly-throw-exceptions"></a>명시적으로 예외를 throw하는 방법

C# [`throw`](../../csharp/language-reference/keywords/throw.md) 또는 Visual Basic [`Throw`](../../visual-basic/language-reference/statements/throw-statement.md) 문을 사용하여 명시적으로 예외를 throw할 수 있습니다. `throw` 문을 사용하여 catch된 예외를 다시 throw할 수도 있습니다. 디버그 시 자세한 정보를 제공하기 위해 다시 throw되는 예외에 정보를 추가하는 것은 좋은 코딩 방법입니다.

다음 코드 예제에서는 `try`/`catch` 블록을 사용하여 가능한 <xref:System.IO.FileNotFoundException>을 catch합니다. `try` 블록 뒤에는 <xref:System.IO.FileNotFoundException>을 catch하고 데이터 파일을 찾을 수 없는 경우 콘솔에 메시지를 쓰는 `catch` 블록이 있습니다. 다음 문은 새 <xref:System.IO.FileNotFoundException>을 throw하고 예외에 텍스트 정보를 추가하는 `throw` 문입니다.

[!code-csharp[Exception.Throwing#1](~/samples/snippets/csharp/VS_Snippets_CLR/Exception.Throwing/CS/throw.cs#1)]
[!code-vb[Exception.Throwing#1](~/samples/snippets/visualbasic/VS_Snippets_CLR/Exception.Throwing/VB/throw.vb#1)]  

## <a name="see-also"></a>참고 항목

- [예외](index.md)
