---
title: '방법: 추적 수신기 만들기 및 초기화'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- initializing trace listeners
- trace listeners, creating
- trace listeners, initializing
- tracing [.NET Framework], trace listeners
- logs, trace listeners
ms.assetid: 21726de1-61ee-4fdc-9dd0-3be49324d066
author: mairaw
ms.author: mairaw
ms.openlocfilehash: a67bd2c0daa8acc81113a1e38ea463753ae34077
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052720"
---
# <a name="how-to-create-and-initialize-trace-listeners"></a>방법: 추적 수신기 만들기 및 초기화

<xref:System.Diagnostics.Debug?displayProperty=nameWithType> 및 <xref:System.Diagnostics.Trace?displayProperty=nameWithType> 클래스는 메시지를 수신하고 처리하는 수신기라는 개체에 메시지를 보냅니다. 추적이나 디버깅을 사용하면 이러한 수신기 중 하나인 <xref:System.Diagnostics.DefaultTraceListener?displayProperty=nameWithType>가 자동으로 만들어지고 초기화됩니다. <xref:System.Diagnostics.Trace> 또는 <xref:System.Diagnostics.Debug> 출력을 추가 소스에 보내려면 추가 추적 수신기를 만들고 초기화해야 합니다.

수신기를 만들 때는 애플리케이션에 필요한 내용을 반영해야 합니다. 예를 들어 모든 추적 출력의 텍스트 레코드가 필요하면 사용될 경우 모든 출력을 새 텍스트 파일에 쓰는 <xref:System.Diagnostics.TextWriterTraceListener> 수신기를 만듭니다. 반면에 애플리케이션 실행 중에만 출력을 보려면 모든 출력을 콘솔 창으로 보내는 <xref:System.Diagnostics.ConsoleTraceListener> 수신기를 만듭니다. <xref:System.Diagnostics.EventLogTraceListener>는 추적 출력을 이벤트 로그에 보낼 수 있습니다. 자세한 내용은 [추적 수신기](trace-listeners.md)를 참조하세요.

[애플리케이션 구성 파일](../configure-apps/index.md) 또는 코드에서 추적 수신기를 만들 수 있습니다. 애플리케이션 구성 파일을 사용하면 코드를 변경할 필요 없이 추적 수신기를 추가, 수정 또는 제거할 수 있으므로 애플리케이션 구성 파일을 사용하는 것이 좋습니다.

### <a name="to-create-and-use-a-trace-listener-by-using-a-configuration-file"></a>구성 파일을 사용하여 추적 수신기를 만들고 사용하려면

1. 애플리케이션 구성 파일에서 추적 수신기를 선언합니다. 만드는 수신기에 다른 개체가 필요하면 이들 개체도 선언합니다. 다음 예제에서는 텍스트 파일을 `TextWriterOutput.log`에 쓰는 `myListener`라는 수신기를 만드는 방법을 보여 줍니다.

    ```xml
    <configuration>
      <system.diagnostics>
        <trace autoflush="false" indentsize="4">
          <listeners>
            <add name="myListener" type="System.Diagnostics.TextWriterTraceListener" initializeData="TextWriterOutput.log" />
            <remove name="Default" />
          </listeners>
        </trace>
      </system.diagnostics>
    </configuration>
    ```

2. 코드에서 <xref:System.Diagnostics.Trace> 클래스를 사용하여 추적 수신기에 메시지를 씁니다.

    ```vb
    Trace.TraceInformation("Test message.")
    ' You must close or flush the trace to empty the output buffer.
    Trace.Flush()
    ```

    ```csharp
    Trace.TraceInformation("Test message.");
    // You must close or flush the trace to empty the output buffer.
    Trace.Flush();
    ```

### <a name="to-create-and-use-a-trace-listener-in-code"></a>코드에서 추적 수신기를 만들고 사용하려면

- 추적 수신기를 <xref:System.Diagnostics.Trace.Listeners%2A> 컬렉션에 추가하고 추적 정보를 수신기에 보냅니다.

    ```vb
    Trace.Listeners.Add(New TextWriterTraceListener("TextWriterOutput.log", "myListener"))
    Trace.TraceInformation("Test message.")
    ' You must close or flush the trace to empty the output buffer.
    Trace.Flush()
    ```

    ```csharp
    Trace.Listeners.Add(new TextWriterTraceListener("TextWriterOutput.log", "myListener"));
    Trace.TraceInformation("Test message.");
    // You must close or flush the trace to empty the output buffer.
    Trace.Flush();
    ```

    \- 또는 -

- 수신기에서 추적 출력을 수신하지 않으려면 <xref:System.Diagnostics.Trace.Listeners%2A> 컬렉션에 수신기를 추가하지 마세요. 수신기의 고유한 출력 메서드를 호출하여 <xref:System.Diagnostics.Trace.Listeners%2A> 컬렉션과 관계없이 수신기를 통해 출력을 내보낼 수 있습니다. 다음 예제에서는 <xref:System.Diagnostics.Trace.Listeners%2A> 컬렉션에 없는 수신기에 줄을 쓰는 방법을 보여 줍니다.

    ```vb
    Dim myListener As New TextWriterTraceListener("TextWriterOutput.log", "myListener")
    myListener.WriteLine("Test message.")
    ' You must close or flush the trace listener to empty the output buffer.
    myListener.Flush()
    ```

    ```csharp
    TextWriterTraceListener myListener = new TextWriterTraceListener("TextWriterOutput.log", "myListener");
    myListener.WriteLine("Test message.");
    // You must close or flush the trace listener to empty the output buffer.
    myListener.Flush();
    ```

## <a name="see-also"></a>참고자료

- [추적 수신기](trace-listeners.md)
- [추적 스위치](trace-switches.md)
- [방법: 응용 프로그램 코드에 Trace 문 추가](how-to-add-trace-statements-to-application-code.md)
- [응용 프로그램 추적 및 조율](tracing-and-instrumenting-applications.md)
