---
title: 파일 액세스에 Async 사용(C#)
ms.date: 07/20/2015
ms.assetid: bb018fea-5313-4c80-ab3f-7c24b2145bd9
ms.openlocfilehash: e6b0370049d9b9315de6a72d0e84c080aac12481
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69595540"
---
# <a name="using-async-for-file-access-c"></a>파일 액세스에 Async 사용(C#)
파일에 액세스하는 비동기 기능을 사용할 수 있습니다. 비동기 기능을 사용하면 콜백을 사용하거나 여러 메서드 또는 람다 식에서 코드를 분할하지 않고도 비동기 메서드를 호출할 수 있습니다. 동기 코드를 비동기로 만들려면 동기 메서드 대신 비동기 메서드를 호출하고 몇 가지 키워드를 코드에 추가하면 됩니다.  
  
 파일 액세스 호출에 비동기를 추가하는 이유로 다음을 고려할 수 있습니다.  
  
- 비동기는 UI 애플리케이션의 응답성을 개선합니다. 작업을 시작하는 UI 스레드가 다른 작업을 수행할 수 있기 때문입니다. UI 스레드가 시간이 오래 걸리는(예: 50밀리초 이상) 코드를 실행해야 하는 경우, I/O가 완료되고 UI 스레드가 키보드와 마우스 입력 및 기타 이벤트를 다시 처리할 수 있을 때까지 UI가 정지할 수 있습니다.  
  
- 비동기는 스레드의 필요성을 줄임으로써 ASP.NET 및 기타 서버 기반 애플리케이션의 확장성을 개선합니다. 애플리케이션이 각 응답에 전용 스레드를 사용하고 1,000개의 요청이 동시에 처리되는 경우 수천 개의 스레드가 필요합니다. 비동기 작업은 대기 중에 종종 스레드를 사용할 필요가 없습니다. 끝날 때 기존 I/O 완료 스레드를 잠시 사용합니다.  
  
- 파일 액세스 작업의 대기 시간은 현재 조건에서 매우 낮을 수 있지만 나중에 대기 시간이 크게 늘어날 수 있습니다. 예를 들어 전 세계에 있는 서버로 파일을 이동할 수 있습니다.  
  
- 비동기 기능을 사용할 경우에는 추가되는 오버헤드가 적습니다.  
  
- 비동기 작업은 쉽게 병렬로 실행할 수 있습니다.  
  
## <a name="running-the-examples"></a>예제 실행  
 이 항목의 예제를 실행하려면 **WPF 애플리케이션** 또는 **Windows Forms 애플리케이션**을 만든 후 **단추**를 추가할 수 있습니다. 단추의 `Click` 이벤트에서 각 예제의 첫 번째 메서드에 대한 호출을 추가합니다.  
  
 다음 예제에서는 `using` 문을 포함합니다.  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.Diagnostics;  
using System.IO;  
using System.Text;  
using System.Threading.Tasks;  
```  
  
## <a name="use-of-the-filestream-class"></a>FileStream 클래스 사용  
 이 항목의 예제에서는 운영 체제 수준에서 비동기 I/O를 일으키는 옵션이 있는 <xref:System.IO.FileStream> 클래스를 사용합니다. 이 옵션을 사용하면 많은 경우 ThreadPool 스레드를 차단하지 않아도 됩니다. 이 옵션을 사용하도록 설정하려면 생성자 호출에서 `useAsync=true` 또는 `options=FileOptions.Asynchronous` 인수를 지정합니다.  
  
 파일 경로를 지정하여 직접 여는 경우에는 <xref:System.IO.StreamReader> 및 <xref:System.IO.StreamWriter>와 함께 이 옵션을 사용할 수 없습니다. 그러나 <xref:System.IO.FileStream> 클래스에서 열린 <xref:System.IO.Stream>을 제공하면 이 옵션을 사용할 수 있습니다. 대기 중에는 UI 스레드가 차단되지 않으므로, ThreadPool 스레드가 차단된 경우에도 UI 앱에서 비동기 호출이 더 빠릅니다.  
  
## <a name="writing-text"></a>텍스트 쓰기  
 다음 예제에서는 파일에 텍스트를 씁니다. 각 await 문에서 메서드가 즉시 종료됩니다. 파일 I/O가 완료되면 await 문 뒤에 오는 문에서 메서드가 다시 시작됩니다. async 한정자는 await 문을 사용하는 메서드의 정의에 있습니다.  
  
```csharp  
public async Task ProcessWriteAsync()  
{  
    string filePath = @"temp2.txt";  
    string text = "Hello World\r\n";  
  
    await WriteTextAsync(filePath, text);  
}  
  
private async Task WriteTextAsync(string filePath, string text)  
{  
    byte[] encodedText = Encoding.Unicode.GetBytes(text);  
  
    using (FileStream sourceStream = new FileStream(filePath,  
        FileMode.Append, FileAccess.Write, FileShare.None,  
        bufferSize: 4096, useAsync: true))  
    {  
        await sourceStream.WriteAsync(encodedText, 0, encodedText.Length);  
    };  
}  
```  
  
 원래 예제에 있는 `await sourceStream.WriteAsync(encodedText, 0, encodedText.Length);` 문은 다음의 두 문이 축약된 것입니다.  
  
```csharp  
Task theTask = sourceStream.WriteAsync(encodedText, 0, encodedText.Length);  
await theTask;  
```  
  
 첫 번째 문은 작업을 반환하여 파일 처리가 시작되도록 합니다. await가 있는 두 번째 문은 메서드를 즉시 종료하고 다른 작업을 반환하도록 합니다. 나중에 파일 처리가 완료되면 await 뒤에 오는 문으로 실행이 반환됩니다. 자세한 내용은 [비동기 프로그램의 제어 흐름(C#)](./control-flow-in-async-programs.md)을 참조하세요.  
  
## <a name="reading-text"></a>텍스트 읽기  
 다음 예제에서는 파일에서 텍스트를 읽습니다. 텍스트가 버퍼링되고, 이 경우 <xref:System.Text.StringBuilder>에 배치됩니다. 이전 예제와 달리 await의 계산에서 값이 생성됩니다. <xref:System.IO.Stream.ReadAsync%2A> 메서드는 <xref:System.Threading.Tasks.Task>\<<xref:System.Int32>>를 반환하므로 작업이 완료된 후 await 평가에서 `Int32` 값(`numRead`)이 생성됩니다. 자세한 내용은 [비동기 반환 형식(C#)](./async-return-types.md)을 참조하세요.  
  
```csharp  
public async Task ProcessReadAsync()  
{  
    string filePath = @"temp2.txt";  
  
    if (File.Exists(filePath) == false)  
    {  
        Debug.WriteLine("file not found: " + filePath);  
    }  
    else  
    {  
        try  
        {  
            string text = await ReadTextAsync(filePath);  
            Debug.WriteLine(text);  
        }  
        catch (Exception ex)  
        {  
            Debug.WriteLine(ex.Message);  
        }  
    }  
}  
  
private async Task<string> ReadTextAsync(string filePath)  
{  
    using (FileStream sourceStream = new FileStream(filePath,  
        FileMode.Open, FileAccess.Read, FileShare.Read,  
        bufferSize: 4096, useAsync: true))  
    {  
        StringBuilder sb = new StringBuilder();  
  
        byte[] buffer = new byte[0x1000];  
        int numRead;  
        while ((numRead = await sourceStream.ReadAsync(buffer, 0, buffer.Length)) != 0)  
        {  
            string text = Encoding.Unicode.GetString(buffer, 0, numRead);  
            sb.Append(text);  
        }  
  
        return sb.ToString();  
    }  
}  
```  
  
## <a name="parallel-asynchronous-io"></a>병렬 비동기 I/O  
 다음 예제에서는 10개의 텍스트 파일을 작성하여 병렬 처리를 보여 줍니다. 각 파일에서 <xref:System.IO.Stream.WriteAsync%2A> 메서드는 작업 목록에 추가되는 작업을 반환합니다. `await Task.WhenAll(tasks);` 문은 메서드를 종료하고, 파일 처리가 모든 작업에 대해 완료되면 메서드 내에서 다시 시작됩니다.  
  
 이 예제는 작업이 완료된 후 `finally` 블록에서 모든 <xref:System.IO.FileStream> 인스턴스를 닫습니다. 대신 `using` 문에 각 `FileStream`이 만들어진 경우 작업이 완료되기 전에 `FileStream`이 삭제될 수 있습니다.  
  
 성능 향상은 거의 대부분 비동기 처리가 아닌 병렬 처리에서 발생합니다. 비동기의 장점은 다중 스레드를 묶어 두지 않고 사용자 인터페이스 스레드를 묶어 두지 않는다는 것입니다.  
  
```csharp  
public async Task ProcessWriteMultAsync()  
{  
    string folder = @"tempfolder\";  
    List<Task> tasks = new List<Task>();  
    List<FileStream> sourceStreams = new List<FileStream>();  
  
    try  
    {  
        for (int index = 1; index <= 10; index++)  
        {  
            string text = "In file " + index.ToString() + "\r\n";  
  
            string fileName = "thefile" + index.ToString("00") + ".txt";  
            string filePath = folder + fileName;  
  
            byte[] encodedText = Encoding.Unicode.GetBytes(text);  
  
            FileStream sourceStream = new FileStream(filePath,  
                FileMode.Append, FileAccess.Write, FileShare.None,  
                bufferSize: 4096, useAsync: true);  
  
            Task theTask = sourceStream.WriteAsync(encodedText, 0, encodedText.Length);  
            sourceStreams.Add(sourceStream);  
  
            tasks.Add(theTask);  
        }  
  
        await Task.WhenAll(tasks);  
    }  
  
    finally  
    {  
        foreach (FileStream sourceStream in sourceStreams)  
        {  
            sourceStream.Close();  
        }  
    }  
}  
```  
  
 <xref:System.IO.Stream.WriteAsync%2A> 및 <xref:System.IO.Stream.ReadAsync%2A> 메서드를 사용하는 경우 중간에 작업을 취소하는 데 사용할 수 있는 <xref:System.Threading.CancellationToken>을 지정할 수 있습니다. 자세한 내용은 [비동기 애플리케이션 미세 조정(C#)](./fine-tuning-your-async-application.md) 및 [관리되는 스레드의 취소](../../../../standard/threading/cancellation-in-managed-threads.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [async 및 await를 사용한 비동기 프로그래밍(C#)](./index.md)
- [비동기 반환 형식(C#)](./async-return-types.md)
- [비동기 프로그램의 제어 흐름(C#)](./control-flow-in-async-programs.md)
