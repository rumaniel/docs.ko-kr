---
title: '방법: 파일에 텍스트 쓰기'
ms.date: 01/04/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- writing text to files
- I/O [.NET Framework], writing text to files
- streams, writing text to files
- data streams, writing text to files
ms.assetid: 060cbe06-2adf-4337-9e7b-961a5c840208
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 9d2fb5a30e165b78fef797bf8bfe536b66cae9a1
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65640753"
---
# <a name="how-to-write-text-to-a-file"></a>방법: 파일에 텍스트 쓰기
이 항목에서는 .NET 앱의 파일에 텍스트를 작성하는 다양한 방법을 보여줍니다. 

파일에 텍스트를 쓸 때는 일반적으로 다음 클래스 및 메서드가 사용됩니다.  
  
- <xref:System.IO.StreamWriter>에는 동기식(<xref:System.IO.StreamWriter.Write%2A> 및 <xref:System.IO.TextWriter.WriteLine%2A>) 또는 비동기식(<xref:System.IO.StreamWriter.WriteAsync%2A> 및 <xref:System.IO.StreamWriter.WriteLineAsync%2A>)으로 파일에 쓰는 메서드가 포함되어 있습니다.  
  
- <xref:System.IO.File>은 <xref:System.IO.File.WriteAllLines%2A> 및 <xref:System.IO.File.WriteAllText%2A>와 같은 파일에 텍스트를 쓰거나 <xref:System.IO.File.AppendAllLines%2A>, <xref:System.IO.File.AppendAllText%2A> 및 <xref:System.IO.File.AppendText%2A>와 같은 파일에 텍스트를 추가하는 정적 메서드를 제공합니다.  
  
- <xref:System.IO.Path>는 파일 또는 디렉터리 경로 정보가 포함된 문자열에 대한 것입니다. 파일이나 디렉터리 경로를 빌드하기 위해 문자열의 연결을 허용하는 <xref:System.IO.Path.Combine%2A> 메서드 및 .NET Core 2.1 이상에서는 <xref:System.IO.Path.Join%2A> 및 <xref:System.IO.Path.TryJoin%2A> 메서드가 포함되어 있습니다.

> [!NOTE]
> 다음 예제에서는 필요한 최소 코드 양만 보여줍니다. 실제 앱은 일반적으로 더 강력한 오류 검사 및 예외 처리 기능을 제공합니다.  
  
## <a name="example-synchronously-write-text-with-streamwriter"></a>예제: StreamWriter를 사용하여 텍스트를 동기식으로 쓰기

다음 예제에서는 <xref:System.IO.StreamWriter> 클래스를 사용하여 한 번에 한 줄씩 새 파일에 텍스트를 동기식으로 쓰는 방법을 보여줍니다. <xref:System.IO.StreamWriter> 개체는 `using` 문에서 선언되고 인스턴스화되므로 스트림을 자동으로 플러시하고 닫는 <xref:System.IO.StreamWriter.Dispose%2A> 메서드가 호출됩니다.  

[!code-csharp[Conceptual.BasicIO.TextFiles#WriteLine](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.basicio.textfiles/cs/write.cs)] 
[!code-vb[Conceptual.BasicIO.TextFiles#WriteLine](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.basicio.textfiles/vb/write.vb)]  

## <a name="example-synchronously-append-text-with-streamwriter"></a>예제: StreamWriter를 사용하여 텍스트를 동기식으로 추가

다음 예제에서는 <xref:System.IO.StreamWriter> 클래스를 사용하여 첫 번째 예제에서 만든 텍스트 파일에 텍스트를 동기식으로 추가하는 방법을 보여줍니다.   

[!code-csharp[Conceptual.BasicIO.TextFiles#WriteLine](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.basicio.textfiles/cs/append.cs)] 
[!code-vb[Conceptual.BasicIO.TextFiles#WriteLine](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.basicio.textfiles/vb/append.vb)]  

## <a name="example-asynchronously-write-text-with-streamwriter"></a>예제: StreamWriter를 사용하여 텍스트를 비동기식으로 쓰기

다음 예제에서는 <xref:System.IO.StreamWriter> 클래스를 사용하여 새 파일에 비동기적으로 텍스트를 쓰는 방법을 보여 줍니다. <xref:System.IO.StreamWriter.WriteAsync%2A> 메서드를 호출하려면 메서드 호출이 `async` 메서드 내에 있어야 합니다. C# 예제에는 C# 7.1 이상이 필요하며, 이 경우 프로그램 진입점에서 `async` 한정자에 대한 지원이 추가됩니다. 

[!code-csharp[Conceptual.BasicIO.TextFiles#WriteLine](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.basicio.textfiles/cs/async.cs)] 
[!code-vb[Conceptual.BasicIO.TextFiles#WriteLine](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.basicio.textfiles/vb/async.vb)]  

## <a name="example-write-and-append-text-with-the-file-class"></a>예제: 파일 클래스로 텍스트 쓰기 및 추가

다음 예제에서는 <xref:System.IO.File> 클래스를 사용하여 새 파일에 텍스트를 쓰고 동일한 파일에 새 텍스트 줄을 추가하는 방법을 보여 줍니다. <xref:System.IO.File.WriteAllText%2A> 및 <xref:System.IO.File.AppendAllLines%2A> 메서드는 자동으로 파일을 열고 닫습니다. <xref:System.IO.File.WriteAllText%2A> 메서드에 제공한 경로가 이미 있는 경우 파일을 덮어씁니다.  

[!code-csharp[Conceptual.BasicIO.TextFiles#WriteLine](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.basicio.textfiles/cs/file.cs)] 
[!code-vb[Conceptual.BasicIO.TextFiles#WriteLine](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.basicio.textfiles/vb/file.vb)]  

## <a name="see-also"></a>참고 항목

- <xref:System.IO.StreamWriter>
- <xref:System.IO.Path>
- <xref:System.IO.File.CreateText%2A?displayProperty=nameWithType>
- [방법: 디렉터리 및 파일 열거](../../../docs/standard/io/how-to-enumerate-directories-and-files.md)
- [방법: 새로 만든 데이터 파일 읽기 및 쓰기](../../../docs/standard/io/how-to-read-and-write-to-a-newly-created-data-file.md)
- [방법: 로그 파일 열기 및 추가](../../../docs/standard/io/how-to-open-and-append-to-a-log-file.md)
- [방법: 파일에서 텍스트 읽기](../../../docs/standard/io/how-to-read-text-from-a-file.md)
- [파일 및 스트림 I/O](../../../docs/standard/io/index.md)
