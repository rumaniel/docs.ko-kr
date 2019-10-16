---
title: '방법: 추적 소스 만들기 및 초기화'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- trace sources
- initializing trace sources
- configuration files [.NET Framework], trace sources
ms.assetid: f88dda6f-5fda-45be-9b3c-745a9b708c4d
author: mairaw
ms.author: mairaw
ms.openlocfilehash: cab9cc33bd5a4697cac5de85de8aa72e7eb4d6c6
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052694"
---
# <a name="how-to-create-and-initialize-trace-sources"></a>방법: 추적 소스 만들기 및 초기화
<xref:System.Diagnostics.TraceSource> 클래스는 애플리케이션과 연결될 수 있는 추적을 만들기 위해 애플리케이션에서 사용됩니다. <xref:System.Diagnostics.TraceSource>는 추적 이벤트, 추적 데이터 및 문제 정보 추적을 쉽게 할 수 있도록 추적 메서드를 제공합니다. 구성 파일을 사용하거나 사용하지 않고 <xref:System.Diagnostics.TraceSource>에서 추적 출력을 만들고 초기화할 수 있습니다. 이 항목에서는 두 가지 옵션 모두에 대한 지침을 제공합니다. 하지만 구성 파일을 사용하여 런타임에 추적 소스에 의해 생성되는 추적을 쉽게 재구성하는 것이 좋습니다.  
  
### <a name="to-create-and-initialize-a-trace-source-using-a-configuration-file"></a>구성 파일을 사용하여 추적 소스를 만들고 초기화하려면  
  
1. Visual Studio 콘솔 애플리케이션 프로젝트를 만들고 제공된 코드를 다음 코드로 바꿉니다. 이 코드는 오류 및 경고를 기록하며 그 중 일부는 콘솔에 출력하고 일부는 구성 파일의 항목에 의해 만들어진 myListener 파일에 출력합니다.  
  
     [!code-csharp[TraceSourceExample1#1](../../../samples/snippets/csharp/VS_Snippets_CLR/tracesourceexample1/cs/program.cs#1)]
     [!code-vb[TraceSourceExample1#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/tracesourceexample1/vb/program.vb#1)]  
  
2. 애플리케이션 구성 파일이 없다면 1단계의 코드 예제에서 `TraceSourceApp`이라는 추적 소스를 초기화하기 위해 프로젝트에 애플리케이션 구성 파일을 추가합니다.  
  
3. 기본 구성 파일 콘텐츠를 다음 설정으로 바꿔서 1단계에서 만든 추적 소스에 대해 콘솔 추적 수신기와 텍스트 기록기 추적 수신기를 초기화합니다.  
  
    ```xml  
    <configuration>  
      <system.diagnostics>  
        <sources>  
          <source name="TraceSourceApp"   
            switchName="sourceSwitch"   
            switchType="System.Diagnostics.SourceSwitch">  
            <listeners>  
              <add name="console"   
                type="System.Diagnostics.ConsoleTraceListener">  
                <filter type="System.Diagnostics.EventTypeFilter"   
                  initializeData="Error"/>  
              </add>  
              <add name="myListener"/>  
              <remove name="Default"/>  
            </listeners>  
          </source>  
        </sources>  
        <switches>  
          <add name="sourceSwitch" value="Error"/>  
        </switches>  
        <sharedListeners>  
          <add name="myListener"   
            type="System.Diagnostics.TextWriterTraceListener"   
            initializeData="myListener.log">  
            <filter type="System.Diagnostics.EventTypeFilter"   
              initializeData="Error"/>  
          </add>  
        </sharedListeners>  
      </system.diagnostics>  
    </configuration>  
    ```  
  
     추적 수신기의 구성 이외에도 구성 파일은 두 수신기에 대한 필터를 만들고 추적 소스에 대한 소스 스위치를 만듭니다. 추적 수신기를 추가하는 데는 두 가지 방법이 사용됩니다. 즉 수신기를 추적 소스에 직접 추가하는 방법과 수신기를 공유 컬렉션에 추가한 다음 이를 이름별로 추적 소스에 추가하는 방법이 있습니다. 두 수신기에 대해 식별된 필터는 서로 다른 소스 수준으로 초기화됩니다. 이로 인해 일부 메시지가 두 수신기 중 하나에 의해서만 기록됩니다.  
  
     구성 파일은 응용 프로그램이 초기화될 때 추적 소스에 대한 설정을 초기화합니다. 응용 프로그램은 구성 파일에서 설정되는 속성을 동적으로 변경하여 사용자가 지정한 설정을 재정의할 수 있습니다. 예를 들어, 현재의 구성 설정과 관계없이 중대 오류 메시지를 항상 텍스트 파일로 보내도록 할 수 있습니다. 예제 코드에서는 구성 파일 설정을 재정의하여 중대 오류 메시지가 추적 수신기에 출력되도록 합니다.  
  
     애플리케이션이 실행되는 동안 구성 파일 설정을 변경해도 초기 설정이 변경되지는 않습니다. 설정을 변경하려면 애플리케이션을 다시 시작하거나 <xref:System.Diagnostics.Trace.Refresh%2A?displayProperty=nameWithType> 메서드를 사용하여 애플리케이션을 프로그래밍 방식으로 새로 고쳐야 합니다.  
  
### <a name="to-initialize-trace-sources-listeners-and-filters-without-a-configuration-file"></a>구성 파일 없이 추적 소스, 수신기 및 필터를 초기화하려면  
  
- 다음 예제 코드를 사용하여 구성 파일을 사용하지 않고도 추적 소스를 통해 추적할 수 있도록 합니다. 이 방법은 권장되는 구현 방법은 아니지만, 상황에 따라 구성 파일에 의존하지 않고 추적하려는 경우가 있을 수 있습니다.  
  
     [!code-csharp[TraceSourceExample2#1](../../../samples/snippets/csharp/VS_Snippets_CLR/tracesourceexample2/cs/program.cs#1)]
     [!code-vb[TraceSourceExample2#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/tracesourceexample2/vb/program.vb#1)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Diagnostics.TraceSource>
- <xref:System.Diagnostics.TextWriterTraceListener>
- <xref:System.Diagnostics.ConsoleTraceListener>
- <xref:System.Diagnostics.EventTypeFilter>
- [응용 프로그램 추적 및 조율](tracing-and-instrumenting-applications.md)
