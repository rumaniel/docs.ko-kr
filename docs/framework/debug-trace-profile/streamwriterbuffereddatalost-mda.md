---
title: streamWriterBufferedDataLost MDA
ms.date: 03/30/2017
helpviewer_keywords:
- StreamWriter class, data buffering problems
- managed debugging assistants (MDAs), StreamWriter data buffering
- buffers, StreamWriter problems
- MDAs (managed debugging assistants), StreamWriter data buffering
- StreamWriter buffered data lost
- data buffering problems
- streamWriterBufferedDataLost MDA
ms.assetid: 6e5c07be-bc5b-437a-8398-8779e23126ab
author: mairaw
ms.author: mairaw
ms.openlocfilehash: c3dcdd329318d48efa203d2b9dcbfe3501d94b3e
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052277"
---
# <a name="streamwriterbuffereddatalost-mda"></a>streamWriterBufferedDataLost MDA
`streamWriterBufferedDataLost` MDA(관리 디버깅 도우미)는 <xref:System.IO.StreamWriter>가 기록될 때 활성화되지만 <xref:System.IO.StreamWriter> 인스턴스가 소멸되기 전에 <xref:System.IO.StreamWriter.Flush%2A> 또는 <xref:System.IO.StreamWriter.Close%2A> 메서드가 이후에 호출되지 않습니다. 이 MDA를 사용하도록 설정하면 런타임이 버퍼링된 데이터가 여전히 <xref:System.IO.StreamWriter> 내에 있는지 여부를 확인합니다. 버퍼링된 데이터가 있으면 MDA가 활성화됩니다. <xref:System.GC.Collect%2A> 및 <xref:System.GC.WaitForPendingFinalizers%2A> 메서드를 호출하면 종료자를 강제로 실행할 수 있습니다. 그러지 않으면 종료자가 임의 시간에 실행되고 프로세스 종료 시 실행되지 않을 수 있습니다. 이 MDA를 사용하도록 설정하여 명시적으로 종료자를 실행하면 이러한 유형의 문제를 보다 안정적으로 재현하는 데 도움이 됩니다.  
  
## <a name="symptoms"></a>증상  
 <xref:System.IO.StreamWriter>는 마지막 1-4KB의 데이터를 파일에 쓰지 않습니다.  
  
## <a name="cause"></a>원인  
 <xref:System.IO.StreamWriter>는 내부적으로 데이터를 버퍼링하므로, 기본 데이터 저장소에 버퍼링된 데이터를 쓰기 위해 <xref:System.IO.StreamWriter.Close%2A> 또는 <xref:System.IO.StreamWriter.Flush%2A> 메서드를 호출해야 합니다. <xref:System.IO.StreamWriter.Close%2A> 또는 <xref:System.IO.StreamWriter.Flush%2A>를 적절하게 호출하지 않으면 <xref:System.IO.StreamWriter> 인스턴스에 버퍼링된 데이터가 예상대로 작성되지 않을 수 있습니다.  
  
 다음은 이 MDA가 catch해야 하는 잘못 작성된 코드 예제입니다.  
  
```csharp  
// Poorly written code.  
void Write()   
{  
    StreamWriter sw = new StreamWriter("file.txt");  
    sw.WriteLine("Data");  
    // Problem: forgot to close the StreamWriter.  
}  
```  
  
 위의 코드는 가비지 수집이 트리거된 다음 종료자가 완료될 때까지 일시 중지되는 경우 이 MDA를 보다 안정적으로 활성화합니다. 이러한 유형의 문제를 추적하기 위해 디버그 빌드에서 이전 메서드의 끝에 다음 코드를 추가할 수 있습니다. 이렇게 하면 MDA가 안정적으로 활성화되지만, 물론 문제의 원인이 수정되지는 않습니다.  
  
```csharp
GC.Collect();  
GC.WaitForPendingFinalizers();  
```  
  
## <a name="resolution"></a>해결 방법  
 <xref:System.IO.StreamWriter> 인스턴스가 있는 코드 블록이나 애플리케이션을 닫기 전에 <xref:System.IO.StreamWriter>에서 <xref:System.IO.StreamWriter.Close%2A> 또는 <xref:System.IO.StreamWriter.Flush%2A>를 호출해야 합니다. 이 작업을 수행하기 위한 최상의 메커니즘 중 하나는 C# `using` 블록(Visual Basic의 `Using` 블록)으로 인스턴스를 만드는 것이며, 이렇게 하면 작성기에 대한 <xref:System.IO.StreamWriter.Dispose%2A> 메서드가 호출되어 인스턴스가 올바르게 닫힙니다.  
  
```csharp
using(StreamWriter sw = new StreamWriter("file.txt"))   
{  
    sw.WriteLine("Data");  
}  
```  
  
 다음 코드에서는 `using` 대신 `try/finally`를 사용하여 동일한 솔루션을 보여 줍니다.  
  
```csharp
StreamWriter sw;  
try   
{  
    sw = new StreamWriter("file.txt"));  
    sw.WriteLine("Data");  
}  
finally   
{  
    if (sw != null)  
        sw.Close();  
}  
```  
  
 이러한 솔루션을 사용할 수 없는 경우(예를 들어 <xref:System.IO.StreamWriter>가 정적 변수에 저장되어 있고 수명이 끝날 때 코드를 쉽게 실행할 수 없는 경우), 마지막 사용 후 <xref:System.IO.StreamWriter>에서 <xref:System.IO.StreamWriter.Flush%2A>를 호출하거나 처음 사용하기 전에 <xref:System.IO.StreamWriter.AutoFlush%2A> 속성을 `true`로 설정하면 이 문제를 방지할 수 있습니다.  
  
```csharp
private static StreamWriter log;  
// static class constructor.  
static WriteToFile()   
{  
    StreamWriter sw = new StreamWriter("log.txt");  
    sw.AutoFlush = true;  
  
    // Publish the StreamWriter for other threads.  
    log = sw;  
}  
```  
  
## <a name="effect-on-the-runtime"></a>런타임에 대한 영향  
 이 MDA는 런타임에 아무런 영향을 미치지 않습니다.  
  
## <a name="output"></a>출력  
 이 위반이 발생했음을 나타내는 메시지입니다.  
  
## <a name="configuration"></a>Configuration  
  
```xml  
<mdaConfig>  
  <assistants>  
    <streamWriterBufferedDataLost />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.IO.StreamWriter>
- [관리 디버깅 도우미를 사용하여 오류 진단](diagnosing-errors-with-managed-debugging-assistants.md)
