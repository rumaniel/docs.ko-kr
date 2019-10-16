---
title: 추적 수신기
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Listener object types
- listeners
- Trace class, listeners
- trace listeners, about trace listeners
- Listeners collection
- trace listeners
- tracing [.NET Framework], trace listeners
- logs, trace listeners
ms.assetid: 444b0d33-67ea-4c36-9e94-79c50f839025
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 752a6a5f9608aa260f192ee3e9e0709b7a10e27e
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052280"
---
# <a name="trace-listeners"></a>추적 수신기
**Trace**, **Debug** 및 <xref:System.Diagnostics.TraceSource>를 사용하는 경우 전송된 메시지를 수집 및 기록하는 메커니즘이 있어야 합니다. *수신기*가 추적 메시지를 수신합니다. 수신기의 목적은 추적 메시지를 수집, 저장 및 라우팅하는 것입니다. 수신기는 추적 출력을 로그, 창 또는 텍스트 파일과 같은 적절한 대상에 보냅니다.  
  
 각각 출력을 다양한 수신기 개체에 전송할 수 있는 **Debug**, **Trace** 및 <xref:System.Diagnostics.TraceSource> 클래스에서 수신기를 사용할 수 있습니다. 일반적으로 사용되는 미리 정의된 수신기는 다음과 같습니다.  
  
- <xref:System.Diagnostics.TextWriterTraceListener>는 출력을 <xref:System.IO.TextWriter> 클래스 인스턴스 또는 <xref:System.IO.Stream> 클래스에 해당하는 항목에 전달합니다. 콘솔과 파일은 <xref:System.IO.Stream> 클래스이므로 이 수신기가 콘솔이나 파일에 쓸 수도 있습니다.  
  
- <xref:System.Diagnostics.EventLogTraceListener>는 출력을 이벤트 로그에 전달합니다.  
  
- <xref:System.Diagnostics.DefaultTraceListener>는 **Write** 및 **WriteLine** 메시지를 **OutputDebugString** 및 **Debugger.Log** 메서드에 내보냅니다. Visual Studio에서는 이를 통해 디버깅 메시지가 출력 창에 표시됩니다. **Fail** 및 실패한 **Assert** 메시지도 **OutputDebugString** Windows API 및 **Debugger.Log** 메서드에 내보내고 이를 통해 메시지 상자가 표시됩니다. 이 동작은 **Debug** 및 **Trace** 메시지에 대한 기본 동작입니다. 이는 **DefaultTraceListener**가 모든 `Listeners` 컬렉션에 자동으로 포함되고 자동으로 포함되는 유일한 수신기이기 때문입니다.  
  
- <xref:System.Diagnostics.ConsoleTraceListener>는 추적 또는 디버깅 출력을 표준 출력이나 표준 오류 스트림에 전달합니다.  
  
- <xref:System.Diagnostics.DelimitedListTraceListener>는 추적 또는 디버깅 출력을 스트림 작성기와 같은 텍스트 작성기 또는 파일 스트림과 같은 스트림으로 보냅니다. 추적 출력은 <xref:System.Diagnostics.DelimitedListTraceListener.Delimiter%2A> 속성으로 지정된 구분 기호를 사용하는 구분된 텍스트 형식입니다.  
  
- <xref:System.Diagnostics.XmlWriterTraceListener>는 추적 및 디버깅 출력을 XML로 인코딩된 데이터로 <xref:System.IO.TextWriter> 또는 <xref:System.IO.Stream>(예: <xref:System.IO.FileStream>)에 전달합니다.  
  
 <xref:System.Diagnostics.DefaultTraceListener> 이외의 수신기가 **Debug**, **Trace** 및 <xref:System.Diagnostics.TraceSource> 출력을 수신하게 하려면 수신기를 `Listeners` 컬렉션에 추가해야 합니다. 자세한 내용은 [방법: 추적 수신기](how-to-create-and-initialize-trace-listeners.md) 만들기 및 초기화 및 [방법: 추적 수신기](how-to-use-tracesource-and-filters-with-trace-listeners.md)와 함께 TraceSource 및 필터를 사용 합니다. **Listeners** 컬렉션의 모든 수신기는 추적 출력 메서드에서 같은 메시지를 가져옵니다. 예를 들어 두 가지 수신기인 **TextWriterTraceListener** 및 **EventLogTraceListener**를 설정한다고 가정합니다. 각 수신기는 같은 메시지를 수신합니다. **TextWriterTraceListener**는 출력을 스트림에 전달하고 **EventLogTraceListener**는 출력을 이벤트 로그에 전달합니다.  
  
 다음 예제에서는 출력을 **Listeners** 컬렉션에 보내는 방법을 보여 줍니다.  
  
```vb  
' Use this example when debugging.  
Debug.WriteLine("Error in Widget 42")  
' Use this example when tracing.  
Trace.WriteLine("Error in Widget 42")  
```  
  
```csharp  
// Use this example when debugging.  
System.Diagnostics.Debug.WriteLine("Error in Widget 42");  
// Use this example when tracing.  
System.Diagnostics.Trace.WriteLine("Error in Widget 42");  
```  
  
 Debug 및 Trace는 같은 **Listeners** 컬렉션을 공유하므로, 수신기 개체를 애플리케이션의 **Debug.Listeners** 컬렉션에 추가하면 **Trace.Listeners** 컬렉션에도 추가됩니다.  
  
 다음 예제에서는 수신기를 사용하여 추적 정보를 콘솔에 보내는 방법을 보여 줍니다.  
  
```vb  
Trace.Listeners.Clear()  
Trace.Listeners.Add(New TextWriterTraceListener(Console.Out))  
```  
  
```csharp  
System.Diagnostics.Trace.Listeners.Clear();  
System.Diagnostics.Trace.Listeners.Add(  
   new System.Diagnostics.TextWriterTraceListener(Console.Out));  
```  
  
## <a name="developer-defined-listeners"></a>개발자 정의 수신기  
 **TraceListener** 기본 클래스에서 상속하고 해당 메서드를 사용자 지정 메서드로 재정의하는 방식으로 고유한 수신기를 정의할 수 있습니다. 개발자 정의 수신기를 만드는 방법에 대한 자세한 내용은 .NET Framework 참조에서 <xref:System.Diagnostics.TraceListener>를 참조하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Diagnostics.TextWriterTraceListener>
- <xref:System.Diagnostics.EventLogTraceListener>
- <xref:System.Diagnostics.DefaultTraceListener>
- <xref:System.Diagnostics.TraceListener>
- [응용 프로그램 추적 및 조율](tracing-and-instrumenting-applications.md)
- [추적 스위치](trace-switches.md)
