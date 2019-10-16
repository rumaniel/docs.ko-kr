---
title: WSHttpBinding
ms.date: 03/30/2017
helpviewer_keywords:
- WS Profile binding
ms.assetid: 22d85b19-0135-4141-9179-a0e9c343ad73
ms.openlocfilehash: 7751e40762a99711302681f28a88d451087e4980
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70044503"
---
# <a name="wshttpbinding"></a>WSHttpBinding
이 샘플에서는 WCF (Windows Communication Foundation)를 사용 하 여 일반 서비스와 일반 클라이언트를 구현 하는 방법을 보여 줍니다. 이 샘플은 인터넷 정보 서비스(IIS)에 의해 호스팅되는 클라이언트 콘솔 프로그램(client.exe)과 서비스 라이브러리로 구성됩니다. 이 서비스는 요청-회신 통신 패턴을 정의하는 계약을 구현합니다. 계약은 수학 연산(Add, Subtract, Multiply 및 Divide)을 노출시키는 `ICalculator` 인터페이스에 의해 정의됩니다. 클라이언트에서 지정된 수학 작업을 동기적으로 요청하면 서비스에서 결과로 회신합니다. 콘솔 창에는 클라이언트 동작이 표시됩니다.  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Binding\WS\wsHttp`  
  
> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.  
  
 이 샘플에서는 `ICalculator` [ \<wsHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md)를 사용 하 여 계약을 노출 합니다. 이 바인딩의 구성은 Web.config 파일에서 확장되었습니다.  
  
```xml
<bindings>  
  <wsHttpBinding>  
    <!--The following is the expanded configuration section for a-->  
    <!--WSHttpBinding. Each property is configured with the default-->   
    <!--value. See the ReliableSession, TransactionFlow, -->  
    <!--TransportSecurity, and MessageSecurity samples in the WS -->  
    <!--directory to learn how to configure these features. -->  
    <binding name="Binding1"  
              bypassProxyOnLocal="false"   
              transactionFlow="false"   
              hostNameComparisonMode="StrongWildcard"  
              maxBufferPoolSize="524288"   
              maxReceivedMessageSize="65536"  
              messageEncoding="Text"   
              textEncoding="utf-8"   
              useDefaultWebProxy="true"  
              allowCookies="false">  
      <reliableSession ordered="true"   
                       inactivityTimeout="00:10:00"  
                       enabled="false" />  
      <security mode="Message">  
        <message clientCredentialType="Windows"   
                 negotiateServiceCredential="true"  
                 algorithmSuite="Default"   
                 establishSecurityContext="true" />  
      </security>  
    </binding>  
  </wsHttpBinding>  
</bindings>  
```  
  
 기본 `binding` 요소에서 `maxReceivedMessageSize` 값을 사용하면 들어오는 메시지의 최대 크기를 바이트 단위로 구성할 수 있습니다. `hostNameComparisonMode` 값을 사용하면 메시지를 서비스로 역 멀티플렉싱할 때 호스트 이름이 고려되는지 여부를 구성할 수 있습니다. `messageEncoding` 값을 사용하면 메시지에 텍스트 또는 MTOM 인코딩 중 어느 것을 사용할지 구성할 수 있습니다. `textEncoding` 값을 사용하면 메시지의 문자 인코딩을 구성할 수 있습니다. `bypassProxyOnLocal` 값을 사용하면 로컬 통신에 HTTP 프록시를 사용할지 여부를 구성할 수 있습니다. `transactionFlow` 값을 사용하면 현재 트랜잭션의 흐름 여부를 알 수 있습니다(작업이 트랜잭션 흐름용으로 구성된 경우).  
  
 ReliableSession > 요소에서 사용 하도록 설정 된 부울 값은 신뢰할 수 있는 세션을 사용할지 여부를 구성 합니다. [ \<](../../../../docs/framework/configure-apps/file-schema/wcf/reliablesession.md) `ordered` 값을 사용하면 메시지 순서의 보존 여부를 구성할 수 있습니다. `inactivityTimeout` 값은 세션에 오류가 발생할 때까지 유휴 상태로 남을 수 있는 시간을 구성합니다.  
  
 보안 > 값은 `mode` 사용 해야 하는 보안 모드를 구성 합니다. [ \<](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-wshttpbinding.md) 이 샘플에서는 메시지 보안을 사용 하 여 [ \<](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-wshttpbinding.md) [ \<](../../../../docs/framework/configure-apps/file-schema/wcf/message-of-wshttpbinding.md) 보안 > 내부에 메시지 > 지정 합니다.  
  
 샘플을 실행하면 작업 요청 및 응답이 클라이언트 콘솔 창에 표시됩니다. 클라이언트를 종료하려면 클라이언트 창에서 Enter 키를 누릅니다.  
  
```  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Press <ENTER> to terminate client.  
```  
  
### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. 다음 명령을 사용 하 여 ASP.NET 4.0을 설치 합니다.  
  
    ```  
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable  
    ```  
  
2. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.  
  
3. C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.  
  
4. 단일 컴퓨터 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)의 지침을 따르세요.  
