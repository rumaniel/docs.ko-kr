---
title: Net.TCP Port Sharing Service 구성
ms.date: 03/30/2017
ms.assetid: b6dd81fa-68b7-4e1b-868e-88e5901b7ea0
ms.openlocfilehash: 70ebaeb8b41b0191e0352b5ef6a4b1913994100c
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69988222"
---
# <a name="configuring-the-nettcp-port-sharing-service"></a>Net.TCP Port Sharing Service 구성
Net.TCP 전송을 사용하는 자체 호스팅 서비스는 네트워크 통신에 사용되는 기본 TCP 소켓의 동작을 제어하는 `ListenBacklog` 및 `MaxPendingAccepts` 등 여러 고급 설정을 제어할 수 있습니다. 그러나 전송 바인딩이 기본적으로 활성화되는 포트 공유를 사용할 수 없도록 설정한 경우 각 소켓에 대한 이러한 설정은 바인딩 수준에서만 적용됩니다.  
  
 net.tcp 바인딩이 전송 바인딩 요소에서 `portSharingEnabled =true`로 설정하여 포트 공유를 사용할 수 있는 경우 암시적으로 외부 프로세스(즉, Net.TCP Port Sharing Service를 호스트하는 SMSvcHost.exe)가 net.tcp 바인딩 대신 TCP 소켓을 관리할 수 있도록 합니다. 예를 들어, TCP를 사용하는 경우 다음을 지정합니다.  
  
```xml  
<tcpTransport portSharingEnabled="true"  />  
```  
  
 이 방법으로 구성된 경우 서비스 전송 바인딩 요소에 지정된 소켓 설정은 SMSvcHost.exe에서 지정한 소켓 설정으로 인해 무시됩니다.  
  
 SMSvcHost.exe를 구성하려면 SmSvcHost.exe.config라고 하는 XML 구성 파일을 만들어 SMSvcHost.exe 실행 파일과 동일한 실제 디렉터리(예: C:\Windows\Microsoft.NET\Framework\v4.5)에 저장합니다.  
  
 다음 예제에서는 명시적으로 지정된 모든 구성 가능한 값에 대한 기본 설정을 사용하여 샘플 SMSvcHost.exe.config를 보여 줍니다.  
  
```xml  
<configuration>  
   <system.serviceModel.activation>  
       <net.tcp listenBacklog="16" <!--16 * # of processors -->  
          maxPendingAccepts="4"<!-- 4 * # of processors -->  
          maxPendingConnections="100"  
          receiveTimeout="00:00:30" <!--30 seconds -->  
          teredoEnabled="false">  
          <allowAccounts>  
             <!-- LocalSystem account -->  
             <add securityIdentifier="S-1-5-18"/>  
             <!-- LocalService account -->  
             <add securityIdentifier="S-1-5-19"/>  
             <!-- Administrators account -->  
             <add securityIdentifier="S-1-5-20"/>  
             <!-- Network Service account -->  
             <add securityIdentifier="S-1-5-32-544" />  
             <!-- IIS_IUSRS account (Vista only) -->  
             <add securityIdentifier="S-1-5-32-568"/>  
           </allowAccounts>  
       </net.tcp>  
</configuration>  
```  
  
## <a name="when-to-modify-smsvchostexeconfig"></a>SMSvcHost.exe.config 수정 시기  
 일반적으로 SMSvcHost.exe.config 파일에 지정된 구성 설정은 Net.TCP Port Sharing Service를 사용하는 컴퓨터의 모든 서비스에 영향을 주기 때문에 이 파일의 내용을 수정하는 경우 주의해야 합니다. 여기에는 WAS(Windows Process Activation Service)의 TCP 활성화 기능을 사용하는 [!INCLUDE[wv](../../../../includes/wv-md.md)]의 애플리케이션이 포함됩니다.  
  
 그러나 Net.TCP Port Sharing Service의 기본 구성을 변경해야 하는 경우도 있습니다. 예를 들어 `maxPendingAccepts`의 기본값은 4 * 프로세서 개수입니다. 포트 공유를 사용하는 여러 서비스를 호스트하는 서버의 경우 최대 처리량을 달성하려면 이 값을 높여야 할 수 있습니다. `maxPendingConnections`의 기본값은 100입니다. 서비스를 호출하는 동시 클라이언트가 여러 개이고 서비스가 클라이언트 연결을 차단하는 경우에도 이 값을 높일 수 있습니다.  
  
 또한 SMSvcHost.exe.config에는 포트 공유 서비스를 사용할 수 있는 프로세스 ID에 대한 정보가 포함되어 있습니다. 프로세스가 공유 TCP 포트를 사용하기 위해 포트 공유 서비스에 연결된 경우 포트 공유 서비스를 사용하도록 허용된 ID 목록과 비교하여 연결 프로세스의 프로세스 ID를 검사합니다. 이러한 id는 smsvchost.exe 파일의 \<allowaccounts > 섹션에서 sid (보안 식별자)로 지정 됩니다. 기본적으로 포트 공유 서비스를 사용할 수 있는 권한이 Administrators 그룹의 구성원뿐만 아니라 시스템 계정(LocalService, LocalSystem 및 NetworkService)에 부여됩니다. 포트 공유 서비스에 연결하기 위해 다른 ID(예를 들어 사용자 ID)로 프로세스를 실행할 수 있는 애플리케이션은 명시적으로 해당 SID를 SMSvcHost.exe.config에 추가해야 합니다. 이러한 변경 사항은 SMSvc.exe 프로세스를 다시 시작할 때까지 적용되지 않습니다.  
  
> [!NOTE]
> UAC(사용자 계정 컨트롤)가 활성화된 상태의 [!INCLUDE[wv](../../../../includes/wv-md.md)] 시스템에서 로컬 사용자는 해당 계정이 Administrators 그룹의 구성원인 경우에도 상승된 권한이 필요합니다. 이러한 사용자가 권한 상승 없이 포트 공유 서비스를 사용할 수 있게 하려면 사용자의 sid (또는 사용자가 구성원 인 그룹의 sid)가 smsvchost.exe의 \<allowaccounts > 섹션에 명시적으로 추가 되어야 합니다.  
  
> [!WARNING]
> 기본 SMSvcHost.exe.config 파일은 사용자 지정 `etwProviderId`를 지정하여 SMSvcHost.exe 추적이 서비스 추적을 방해하지 않도록 합니다.  
  
## <a name="see-also"></a>참고자료

- [\<net.tcp>](../../../../docs/framework/configure-apps/file-schema/wcf/net-tcp.md)
