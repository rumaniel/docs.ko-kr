---
title: 비동기 파일 I/O
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- streams, synchronous streams
- asynchronous I/O
- synchronous I/O
- streams, asynchronous streams
- I/O [.NET Framework], asynchronous I/O
- Stream class, synchronous I/O
- data streams, asynchronous streams
- Stream class, asynchronous I/O
- multiple I/O requests
- data streams, synchronous streams
ms.assetid: dbdd55e7-d6b9-4f9e-8abb-ab0edd4457f7
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 1c6e1db7d1edacfd0ce8770b9cc7b7f3f9c8ca2a
ms.sourcegitcommit: ea00c05e0995dae928d48ead99ddab6296097b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48025323"
---
# <a name="asynchronous-file-io"></a>비동기 파일 I/O

비동기 작업을 사용하면 주 스레드를 차단하지 않고 리소스 집중형 I/O 작업을 수행할 수 있습니다. 이 성능 고려 사항은 특히 시간이 소비되는 스트림 작업이 UI 스레드를 차단하고 응용 프로그램이 작동하지 않는 것처럼 표시할 수 있는 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 응용 프로그램 또는 [!INCLUDE[desktop_appname](../../../includes/desktop-appname-md.md)] 응용 프로그램에서 중요합니다.

[!INCLUDE[net_v45](../../../includes/net-v45-md.md)]부터 I/O 형식은 비동기 메서드를 포함하여 비동기 작업을 단순화합니다. 비동기 메서드의 이름에는 `Async` 가 포함합니다(예: <xref:System.IO.Stream.ReadAsync%2A>, <xref:System.IO.Stream.WriteAsync%2A>, <xref:System.IO.Stream.CopyToAsync%2A>, <xref:System.IO.Stream.FlushAsync%2A>, <xref:System.IO.TextReader.ReadLineAsync%2A>및 <xref:System.IO.TextReader.ReadToEndAsync%2A>). 이러한 비동기 메서드는 스트림 클래스(예: <xref:System.IO.Stream>, <xref:System.IO.FileStream>및 <xref:System.IO.MemoryStream>)에 구현되거나, 스트림에서 읽거나 스트림에 쓰는 데 사용되는 클래스(예: <xref:System.IO.TextReader> 및 <xref:System.IO.TextWriter>)에 구현됩니다.

.NET Framework 4 및 이전 버전에서 비동기 I/O 작업을 구현하려면 <xref:System.IO.Stream.BeginRead%2A> 및 <xref:System.IO.Stream.EndRead%2A> 와 같은 메서드를 사용해야 합니다. 이러한 메서드는 여전히 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 에서 사용하여 레거시 코드를 지원할 수 있지만, 비동기 메서드는 비동기 I/O 작업을 보다 쉽게 구현하도록 도와줍니다.

C# 및 Visual Basic에는 각각 비동기 프로그래밍을 위한 다음 두 개의 키워드가 있습니다.

- 비동기 작업을 포함하는 메서드를 표시하는 데 사용되는`Async` (Visual Basic) 또는 `async` (C#) 한정자.

- 비동기 메서드의 결과에 적용되는`Await` (Visual Basic) 또는 `await` (C#) 연산자.

비동기 I/O 작업을 구현하려면 다음 예제와 같이 이러한 키워드를 비동기 메서드와 함께 사용합니다. 자세한 내용은 [Async 및 Await를 사용한 비동기 프로그래밍](https://msdn.microsoft.com/library/db854f91-ccef-4035-ae4d-0911fde808c7)을 참조하세요.

다음 예제에서는 두 가지 <xref:System.IO.FileStream> 개체를 사용하여 한 디렉터리에서 다른 디렉터리로 파일을 비동기적으로 복사하는 방법을 보여 줍니다. <xref:System.Web.UI.WebControls.Button.Click> 컨트롤에 대한 <xref:System.Windows.Controls.Button> 이벤트 처리기는 비동기 메서드를 호출하므로 `async` 한정자로 표시됩니다.

[!code-csharp[Asynchronous_File_IO_async#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Asynchronous_File_IO_async/cs/example.cs#1)]
[!code-vb[Asynchronous_File_IO_async#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Asynchronous_File_IO_async/vb/example.vb#1)]

다음 예제는 이전과 유사하지만, <xref:System.IO.StreamReader> 및 <xref:System.IO.StreamWriter> 개체를 사용하여 텍스트 파일의 내용을 비동기적으로 읽고 씁니다.

[!code-csharp[Asynchronous_File_IO_async#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Asynchronous_File_IO_async/cs/example2.cs#2)]
[!code-vb[Asynchronous_File_IO_async#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Asynchronous_File_IO_async/vb/example2.vb#2)]

다음 예제에서는 <xref:System.IO.Stream> 응용 프로그램에서 파일을 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 으로 열고 <xref:System.IO.StreamReader> 클래스의 인스턴스를 사용하여 해당 내용을 읽는 데 사용되는 코드 숨김 파일 및 XAML 파일을 보여 줍니다. 비동기 메서드를 사용하여 파일을 스트림으로 열고 해당 내용을 읽습니다.

[!code-csharp[System.IO.WindowsRuntimeStorageExtensions#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.windowsruntimestorageextensions/cs/blankpage.xaml.cs#2)]
[!code-vb[System.IO.WindowsRuntimeStorageExtensions#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.windowsruntimestorageextensions/vb/blankpage.xaml.vb#2)]

[!code-xaml[System.IO.WindowsRuntimeStorageExtensions#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.windowsruntimestorageextensions/cs/blankpage.xaml#1)]

## <a name="see-also"></a>참고 항목

- <xref:System.IO.Stream>
- [파일 및 스트림 I/O](../../../docs/standard/io/index.md)
- [Async 및 Await를 사용한 비동기 프로그래밍](https://msdn.microsoft.com/library/db854f91-ccef-4035-ae4d-0911fde808c7)
