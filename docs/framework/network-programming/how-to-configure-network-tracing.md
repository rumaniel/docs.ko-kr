---
title: '방법: 네트워크 추적 구성'
ms.date: 03/30/2017
helpviewer_keywords:
- formatting [.NET Framework], network tracing
- network tracing, configuring
- level attribute
- app.config files, network tracing
- configuration files [.NET Framework], network tracing
- protocol-level trace output
- application configuration files, network tracing
- sockets, trace output
ms.assetid: 5ef9fe4b-8d3d-490e-9259-1d014b2181af
ms.openlocfilehash: 257f417fa573577ca8e8ceb4edc9c4f481af1f72
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50192449"
---
# <a name="how-to-configure-network-tracing"></a>방법: 네트워크 추적 구성
응용 프로그램 또는 컴퓨터 구성 파일은 형식과 네트워크 추적의 내용을 결정하는 설정을 유지합니다. 이 절차를 수행하기 전에 추적이 활성화되어야 합니다. 추적을 사용하는 방법에 대한 자세한 내용은 [네트워크 추적 사용](../../../docs/framework/network-programming/enabling-network-tracing.md)을 참조하세요.  
  
 컴퓨터 구성 파일인 machine.config는 Windows가 설치된 디렉터리의 %Windir%\Microsoft.NET\Framework 폴더에 저장됩니다. 컴퓨터에 설치된 .NET Framework의 각 버전에 해당하는 %Windir%\Microsoft.NET\Framework 아래의 폴더에는 개별 machine.config 파일이 있습니다(예: C:\WINDOWS\Microsoft.NET\Framework\v2.0.50727\machine.config 또는 C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config).  
  
 이러한 설정은 컴퓨터 구성 파일보다 우선하는 응용 프로그램의 구성 파일에서 만들 수도 있습니다.  
  
### <a name="to-configure-network-tracing"></a>네트워크 추적을 구성하려면  
  
-   알맞은 구성 파일에 다음 줄을 추가합니다. 이런 설정을 위한 값과 옵션은 아래 표에 설명되어 있습니다.  
  
    ```xml  
    <configuration>  
      <system.diagnostics>  
        <sources>  
          <source name="System.Net" tracemode="includehex" maxdatasize="1024">  
            <listeners>  
              <add name="System.Net"/>  
            </listeners>  
          </source>  
          <source name="System.Net.Cache">  
            <listeners>  
              <add name="System.Net"/>  
            </listeners>  
          </source>  
          <source name="System.Net.Http">  
            <listeners>  
              <add name="System.Net"/>  
            </listeners>  
          </source>  
          <source name="System.Net.Sockets">  
            <listeners>  
              <add name="System.Net"/>  
            </listeners>  
          </source>  
          <source name="System.Net.WebSockets">  
            <listeners>  
              <add name="System.Net"/>  
            </listeners>  
          </source>  
        </sources>  
        <switches>  
          <add name="System.Net" value="Verbose"/>  
          <add name="System.Net.Cache" value="Verbose"/>  
          <add name="System.Net.Http" value="Verbose"/>  
          <add name="System.Net.Sockets" value="Verbose"/>  
          <add name="System.Net.WebSockets" value="Verbose"/>  
        </switches>  
        <sharedListeners>  
          <add name="System.Net"  
            type="System.Diagnostics.TextWriterTraceListener"  
            initializeData="network.log"  
          />  
        </sharedListeners>  
        <trace autoflush="true"/>  
      </system.diagnostics>  
    </configuration>  
    ```  
  
 `<switches>` 블록에 이름을 추가할 때, 추적 출력에는 이름과 관련된 일부 메서드에서 가져온 정보가 포함됩니다. 다음 표에서는 출력에 대해 설명합니다.  
  
|name|출력되는 위치|  
|----------|-----------------|  
|`System.Net.Sockets`|<xref:System.Net.Sockets.Socket>, <xref:System.Net.Sockets.TcpListener>, <xref:System.Net.Sockets.TcpClient> 및 <xref:System.Net.Dns> 클래스의 일부 공용 메서드|  
|`System.Net`|<xref:System.Net.HttpWebRequest>, <xref:System.Net.HttpWebResponse>, <xref:System.Net.FtpWebRequest> 및 <xref:System.Net.FtpWebResponse> 클래스의 일부 공용 메서드와 SSL 디버그 정보(잘못된 인증서, 누락된 발급자 목록 및 클라이언트 인증서 오류)|  
|`System.Net.HttpListener`|<xref:System.Net.HttpListener>, <xref:System.Net.HttpListenerRequest> 및 <xref:System.Net.HttpListenerResponse> 클래스의 일부 공용 메서드.|  
|`System.Net.Cache`|`System.Net.Cache`의 일부 개인 및 내부 메서드|  
|`System.Net.Http`|<xref:System.Net.Http.HttpClient>, <xref:System.Net.Http.DelegatingHandler>, <xref:System.Net.Http.HttpClientHandler>, <xref:System.Net.Http.HttpMessageHandler>, <xref:System.Net.Http.MessageProcessingHandler> 및 <xref:System.Net.Http.WebRequestHandler> 클래스의 일부 공용 메서드.|  
|`System.Net.WebSockets.WebSocket`|<xref:System.Net.WebSockets.ClientWebSocket> 및 <xref:System.Net.WebSockets.WebSocket> 클래스의 일부 공용 메서드.|  
  
 다음 표에 나열된 특성이 추적 출력을 구성합니다.  
  
|특성 이름|특성 값|  
|--------------------|---------------------|  
|`Value`|필수 <xref:System.String> 특성입니다. 출력의 자세한 정도를 설정합니다. 올바른 값은 `Critical`, `Error`, `Verbose`, `Warning`, `Information`입니다.<br /><br /> 예제에 나타낸 것처럼, \<switches> 요소의 \<add name> 요소에 대해 이 특성을 설정해야 합니다. 이 특성이 \<source> 요소에 대해 설정되어 있는 경우 예외가 throw됩니다.|  
|`maxdatasize`|선택적 <xref:System.Int32> 특성입니다. 각 줄 추적에 포함된 네트워크 데이터의 최대 바이트 수를 설정합니다. 기본값은 1024입니다.<br /><br /> 예제에 나타낸 것처럼, \<source> 요소에 대해 이 특성을 설정해야 합니다. 이 특성이 \<switches> 요소 아래의 요소에 대해 설정되어 있는 경우 예외가 throw됩니다.|  
|`Tracemode`|선택적 <xref:System.String> 특성입니다. 16진수 및 텍스트 형식으로 프로토콜 추적을 표시하려면 `includehex`로 설정합니다. 텍스트만 표시하려면 `protocolonly`로 설정합니다. 기본값은 `includehex`입니다.<br /><br /> 예제에 나타낸 것처럼, \<switches> 요소에 대해 이 특성을 설정해야 합니다. 이 특성이 \<source> 요소 아래의 요소에 대해 설정되어 있는 경우 예외가 throw됩니다.|  
  
## <a name="see-also"></a>참고 항목  
 [네트워크 추적 해석](../../../docs/framework/network-programming/interpreting-network-tracing.md)  
 [.NET Framework의 네트워크 추적](../../../docs/framework/network-programming/network-tracing.md)  
 [네트워크 추적 사용](../../../docs/framework/network-programming/enabling-network-tracing.md)  
 [응용 프로그램 추적 및 조율](../../../docs/framework/debug-trace-profile/tracing-and-instrumenting-applications.md)
