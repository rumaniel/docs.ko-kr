---
title: IDisposable을 구현하는 개체 사용
ms.date: 04/07/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Dispose method
- try/finally block
- garbage collection, encapsulating resources
ms.assetid: 81b2cdb5-c91a-4a31-9c83-eadc52da5cf0
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9f165ab5b79abbc2b5464f40a27a580d26af163a
ms.sourcegitcommit: 6f28b709592503d27077b16fff2e2eacca569992
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2019
ms.locfileid: "70106946"
---
# <a name="using-objects-that-implement-idisposable"></a>IDisposable을 구현하는 개체 사용

공용 언어 런타임의 가비지 수집기는 관리되는 개체에서 사용하는 메모리를 회수하지만, 관리되지 않는 리소스를 사용하는 유형에서는 관리되지 않는 이러한 리소스에 할당된 메모리를 회수할 수 있게 하는 <xref:System.IDisposable> 인터페이스를 구현합니다. <xref:System.IDisposable>을 구현하는 개체의 사용을 마치면 해당 개체의 <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType> 구현을 호출해야 합니다. 이 작업은 다음 두 가지 방법 중 하나로 수행할 수 있습니다.  
  
- C# `using` 문 또는 Visual Basic `Using` 문 사용  
  
- `try/finally` 블록 구현  

## <a name="the-using-statement"></a>using 문

C#의 `using` 문과 Visual Basic의 `Using` 문은 개체를 만들고 정리하기 위해 작성해야 하는 코드를 단순화합니다. `using` 문은 하나 이상의 리소스를 가져와서, 사용자가 지정하는 문을 실행한 다음, 개체를 자동으로 삭제합니다. 그러나 `using` 문은 개체가 생성된 메서드의 범위 내에서 사용되는 개체에만 유용합니다.  
  
다음 예제에서는 `using` 문을 사용하여 <xref:System.IO.StreamReader?displayProperty=nameWithType> 개체를 만들고 해제합니다.  
  
[!code-csharp[Conceptual.Disposable#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/using1.cs#1)]
[!code-vb[Conceptual.Disposable#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/using1.vb#1)]  
  
<xref:System.IO.StreamReader> 클래스가 <xref:System.IDisposable> 인터페이스를 구현하며, 이는 관리되지 않는 리소스를 사용함을 나타내지만 예제에서는 <xref:System.IO.StreamReader.Dispose%2A?displayProperty=nameWithType> 메서드를 명시적으로 호출하지 않습니다. C# 또는 Visual Basic 컴파일러가 `using` 문을 발견하면 `try/finally` 블록을 명시적으로 포함하는 다음 코드와 동일한 중간 언어(IL)를 표시합니다.  
  
[!code-csharp[Conceptual.Disposable#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/using3.cs#3)]
[!code-vb[Conceptual.Disposable#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/using3.vb#3)]  
  
또한 C# `using` 문을 사용하면 단일 문으로 여러 리소스를 가져올 수 있으며, 이는 중첩된 `using` 문의 기능과 내부적으로 동일합니다. 다음 예제에서는 서로 다른 두 파일의 내용을 읽을 수 있도록 두 개의 <xref:System.IO.StreamReader> 개체를 인스턴스화합니다.  
  
[!code-csharp[Conceptual.Disposable#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/using4.cs#4)]

## <a name="tryfinally-block"></a>Try/finally 블록

`using` 문에서 `try/finally` 블록을 래핑하는 대신 `try/finally` 블록을 직접 구현하도록 선택할 수 있습니다. 개인적인 코딩 스타일에 따라서 또는 다음 이유 중 하나로 인해 이를 수행할 수 있습니다.  
  
- `catch` 블록에서 throw된 모든 예외를 처리하기 위해 `try` 블록을 포함하려는 경우 그렇지 않으면, `using` 문에서 throw된 예외가 `try/catch` 블록이 없는 경우 `using` 블록 내에 throw되는 예외와 마찬가지로 처리됩니다.  
  
- 범위가 선언된 범위 내의 블록에 대해 로컬이 아닌 <xref:System.IDisposable>을 구현하는 개체를 인스턴스화하려는 경우  
  
`try/catch/finally` 블록을 사용하여 <xref:System.IO.StreamReader> 개체를 인스턴스화, 사용 및 삭제하고 <xref:System.IO.StreamReader> 생성자 및 해당 <xref:System.IO.StreamReader.ReadToEnd%2A> 메서드에서 throw된 예외를 처리한다는 점을 제외하면 다음 예제는 이전 예제와 유사합니다. `finally` 블록의 코드가 <xref:System.IDisposable> 메서드를 호출하기 전에 `null`을 구현하는 개체가 <xref:System.IDisposable.Dispose%2A>이 아닌지 확인합니다. 이렇게 하지 않으면 런타임에 <xref:System.NullReferenceException> 예외가 발생할 수 있습니다.  
  
[!code-csharp[Conceptual.Disposable#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.disposable/cs/using5.cs#6)]
[!code-vb[Conceptual.Disposable#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.disposable/vb/using5.vb#6)]  
  
프로그래밍 언어가 `using` 문을 지원하지 않지만, <xref:System.IDisposable.Dispose%2A> 메서드에 대한 직접 호출을 허용하므로 `try/finally` 블록을 구현하도록 선택하거나 구현해야 하는 경우 이 기본 패턴을 따를 수 있습니다. 
  
## <a name="see-also"></a>참고 항목

- [관리되지 않는 리소스 정리](../../../docs/standard/garbage-collection/unmanaged.md)
- [using 문(C# 참조)](../../csharp/language-reference/keywords/using-statement.md)
- [Using 문(Visual Basic)](../../visual-basic/language-reference/statements/using-statement.md)
