---
title: 서비스 호스팅
ms.date: 03/30/2017
helpviewer_keywords:
- hosting services [WCF]
ms.assetid: 192be927-6be2-4fda-98f0-e513c4881acc
ms.openlocfilehash: b1a0a07876e9cc111e8c5eef56f208d7bf2cb49f
ms.sourcegitcommit: 2d42b7ae4252cfe1232777f501ea9ac97df31b63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2019
ms.locfileid: "67487707"
---
# <a name="hosting-services"></a>서비스 호스팅
활성화할 서비스는 서비스를 만들고 컨텍스트와 수명을 제어하는 런타임 환경에 호스팅해야 합니다. Windows Communication Foundation (WCF) 서비스는 관리 코드를 지 모든 Windows 프로세스에서 실행 되도록 설계 되었습니다.  
  
 WCF는 서비스 지향 응용 프로그램을 빌드하기 위한 통합된 프로그래밍 모델을 제공 합니다. 이 프로그래밍 모델은 일관적이며 서비스가 배포되는 런타임 환경에 독립적입니다. 즉, 서비스 코드는 사실상 서비스 호스팅 옵션에 관계없이 거의 동일합니다.  
  
 서비스 호스팅 옵션은 콘솔 애플리케이션 내에서 실행하는 경우부터 서버 환경에 이르기까지 다양합니다. 서버 환경의 예를 들면 IIS(인터넷 정보 서비스) 또는 WAS(Windows Process Activation Service)에서 관리하는 작업자 프로세스 내에서 실행되는 Windows 서비스가 있습니다. 개발자는 서비스의 배포 요구 사항을 만족하는 호스팅 환경을 선택합니다. 이러한 요구 사항은 애플리케이션이 배포되는 플랫폼, 메시지를 보내고 받는 데 필요한 전송, 충분한 가용성을 보장하는 데 필요한 프로세스 재활용 유형 및 기타 프로세스 관리 유형, 기타 관리 또는 안정성 요구 사항에 따라 달라집니다. 다음 단원에서는 호스팅 옵션에 대한 정보 및 지침을 제공합니다.  
  
## <a name="hosting-options"></a>호스팅 옵션  
  
#### <a name="self-hosting-in-a-managed-application"></a>관리되는 애플리케이션에서의 자체 호스팅  
 모든 관리 되는 응용 프로그램에서 WCF 서비스를 호스트할 수 있습니다. 이 경우 배포하는 데 있어 최소한의 인프라를 필요하므로 가장 유연한 옵션입니다. 관리되는 애플리케이션 코드 내에 서비스 코드를 포함시킨 다음 서비스를 사용할 수 있도록 <xref:System.ServiceModel.ServiceHost> 의 인스턴스를 만들고 엽니다. 자세한 내용은 [방법: 관리 되는 응용 프로그램에서 WCF 서비스 호스팅](../../../docs/framework/wcf/how-to-host-a-wcf-service-in-a-managed-application.md)합니다.  
  
 이 옵션을 사용 하면 두 가지 일반적인 시나리오: 콘솔 응용 프로그램 및 Windows Presentation Foundation (WPF) 또는 Windows Forms (WinForms)에 따라 같은 리치 클라이언트 응용 프로그램 내에서 실행 되는 WCF 서비스입니다. 콘솔 응용 프로그램 내에서 WCF 서비스를 호스팅하는 응용 프로그램의 개발 단계 중 일반적으로 유용 합니다. 이 경우 쉽게 디버깅을 수행할 수 있으며, 애플리케이션 내에서 발생하는 상황을 확인하기 위한 추적 정보를 손쉽게 얻을 수 있으며, 새 위치에 서비스를 복사하여 이동하기 용이합니다. 이 호스팅 옵션 또한 쉽게 리치 클라이언트 응용 프로그램의 경우 WPF 및 WinForms 응용 프로그램과 같은 외부 세계와 통신할 수 있습니다. 예를 들어, 해당 사용자 인터페이스에 대 한 WPF를 사용 하 고 또한 다른 클라이언트가 연결 하 고 정보를 공유할 수 있도록 WCF 서비스를 호스팅하는 피어-투-피어 공동 작업 클라이언트가 있습니다.  
  
#### <a name="managed-windows-services"></a>관리되는 Windows 서비스  
 이 호스팅 옵션에 대 한 서비스의 프로세스 수명은 서비스 제어 관리자 (SCM)에 의해 제어 됩니다 있도록 하는 WCF 서비스 (이전의 NT 서비스) 관리 되는 Windows 서비스로 호스팅하는 응용 프로그램 도메인 (AppDomain) 등록 구성 Windows 서비스입니다. 자체 호스팅 옵션과 같이 이러한 유형의 호스팅 환경에서는 일부 호스팅 코드를 애플리케이션의 일부로 작성해야 합니다. 서비스는 모두 Windows 서비스와 WCF 서비스로 상속 하 여 구현 됩니다는 <xref:System.ServiceProcess.ServiceBase> 클래스 뿐만 아니라는 WCF에서 서비스 계약 인터페이스. 그러면 <xref:System.ServiceModel.ServiceHost> 가 만들어지고, 재정의된 <xref:System.ServiceProcess.ServiceBase.OnStart%28System.String%5B%5D%29> 메서드 내에서 열리고 재정의된 <xref:System.ServiceProcess.ServiceBase.OnStop> 메서드 내에서 닫힙니다. Installutil.exe 도구를 사용하여 프로그램을 Windows 서비스로 설치하려면 <xref:System.Configuration.Install.Installer> 에서 상속되는 설치 관리자 클래스를 구현해야 합니다. 자세한 내용은 [방법: 관리 되는 Windows 서비스에서 WCF 서비스 호스팅](../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-a-managed-windows-service.md)합니다. 관리 되는 Windows 서비스 호스팅 옵션에서 사용할 수 있는 시나리오에는 메시지가 활성화 되지 않은 보안 환경의 IIS 외부에서 호스팅되는 장기 실행 WCF 서비스의 경우 서비스 수명은 대신 운영 체제에 의해 제어됩니다. 모든 버전의 Windows에서 이 호스팅 옵션을 사용할 수 있습니다.  
  
#### <a name="internet-information-services-iis"></a>IIS(인터넷 정보 서비스)  
 IIS 호스팅 옵션 ASP.NET과 통합 되어 있으며 이러한 기술은, 프로세스 재활용, 유휴 상태 이면 종료, 프로세스 상태 모니터링 및 메시지 기반 활성화 같은 기능을 사용 합니다. [!INCLUDE[wxp](../../../includes/wxp-md.md)] 및 [!INCLUDE[ws2003](../../../includes/ws2003-md.md)] 운영 체제에서 이 옵션은 높은 가용성 및 확장성을 필요로 하는 웹 서비스 응용 프로그램을 호스팅하는 기본 솔루션입니다. IIS는 또한 고객이 엔터프라이즈 수준의 서버 제품에서 기대하는 통합된 관리 효율성을 제공합니다. 이 호스팅 옵션을 사용하려면 IIS를 적절히 구성해야 하지만 호스팅 코드를 애플리케이션의 일부로 작성하지 않아도 됩니다. IIS를 구성 하는 방법에 대 한 자세한 내용은 참조는 WCF 서비스에 대 한 호스팅 [방법: IIS에서 WCF 서비스 호스팅](../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-iis.md)합니다.  
  
 IIS에서 호스팅되는 서비스는 HTTP 전송만 사용할 수 있습니다. IIS 5.1에서의 서비스 구현 시 [!INCLUDE[wxp](../../../includes/wxp-md.md)]의 경우 몇 가지 제한이 있습니다. IIS 5.1에서 WCF 서비스에 대해 제공 되는 메시지 기반 활성화 [!INCLUDE[wxp](../../../includes/wxp-md.md)] 통신할 포트 80을 사용 하 여 동일한 컴퓨터에서 자체 호스팅된 WCF 서비스를 차단 합니다. WCF 서비스는 IIS 6.0에서 호스팅되는 경우 다른 응용 프로그램과 동일한 AppDomain/응용 프로그램 풀/작업자 프로세스에서 실행할 수 있습니다 [!INCLUDE[ws2003](../../../includes/ws2003-md.md)]합니다. 하지만 WCF 및 IIS 6.0 모두 커널 모드 HTTP 스택 (HTTP.sys)를 사용 하므로 IIS 6.0 IIS 5.1과 달리 동일한 컴퓨터에서 실행 되는 다른 자체 호스팅된 WCF 서비스를 사용 하 여 포트 80를 공유할 수 있습니다.  
  
#### <a name="windows-process-activation-service-was"></a>WAS(Windows Process Activation Service)  
 WAS(Windows Process Activation Service)는 [!INCLUDE[lserver](../../../includes/lserver-md.md)] 에서도 사용할 수 있는 [!INCLUDE[wv](../../../includes/wv-md.md)]을 위한 새 프로세스 활성화 메커니즘입니다. 친숙 한 IIS 6.0 프로세스 모델 (응용 프로그램 풀 및 메시지 기반 프로세스 활성화)는 그대로 유지 하 고 활성화에서 HTTP에 대 한 종속성을 제거 하지만 기능 (예: 오류 로부터 신속한 보호, 상태 모니터링 및 재활용), 호스팅 아키텍처입니다. IIS 7.0 WAS를 사용 하 여 HTTP를 통한 메시지 기반 활성화를 수행. 또한 WCF 구성 요소를 추가 WCF 지 원하는 다른 프로토콜을 통해, TCP, MSMQ 및 명명 된 파이프와 같은 메시지 기반 활성화를 제공 하도록 WAS 꽂습니다. 이렇게 하면 통신 프로토콜을 사용하는 애플리케이션에서 프로세스 재활용, 오류로부터 신속한 보호 및 일반적인 구성 시스템과 같은 HTTP 기반 애플리케이션에서만 사용할 수 있었던 IIS 기능을 사용할 수 있습니다.  
  
 이 호스팅 옵션을 사용하려면 IIS를 적절히 구성해야 하지만 호스팅 코드를 애플리케이션의 일부로 작성하지 않아도 됩니다. 구성 하는 방법에 대 한 자세한 내용은 WAS 호스팅을 참조 [방법: WAS에서 WCF 서비스 호스팅](../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-was.md)합니다.  
  
## <a name="choosing-a-hosting-environment"></a>호스팅 환경 선택  
 다음 표에서는 각 호스팅 옵션과 관련된 몇 가지 주요 이점 및 시나리오를 요약하여 설명합니다.  
  
|호스팅 환경|일반적인 시나리오|주요 이점 및 제한|  
|-------------------------|----------------------|----------------------------------|  
|관리되는 애플리케이션("자체 호스팅")|콘솔 응용 프로그램 개발 중에 사용 합니다.<br />-리치 WinForm 및 WPF 클라이언트 응용 프로그램 서비스에 액세스 합니다.|-유연 합니다.<br />-쉽게 배포할 수 있습니다.<br />-서비스에 대 한 엔터프라이즈 솔루션입니다.|  
|Windows 서비스(이전의 NT 서비스)|IIS 외부에서 호스팅된-장기 실행 WCF 서비스입니다.|메시지가 활성화 되지 운영 체제에 의해 제어 되는 서비스 프로세스 수명입니다.<br />Windows의 모든 버전에서 지원 합니다.<br />-보안 환경입니다.|  
|IIS 5.1, IIS 6.0|-WCF 서비스 side-by-side-ASP.NET 콘텐츠를 사용 하 여 인터넷을 통해 실행 HTTP 프로토콜을 사용 합니다.|-프로세스 재활용 합니다.<br />-유휴 상태 이면 종료 합니다.<br />-상태 모니터링을 처리 합니다.<br />-메시지 기반 활성화 합니다.<br />-HTTP에만 해당 합니다.|  
|WAS(Windows Process Activation Service)|-다양 한 전송 프로토콜을 사용 하 여 인터넷에서 IIS를 설치 하지 않고 WCF 서비스를 실행 합니다.|-IIS 필요 하지 않습니다.<br />-프로세스 재활용 합니다.<br />-유휴 상태 이면 종료 합니다.<br />-상태 모니터링을 처리 합니다.<br />-메시지 기반 활성화 합니다.<br />-HTTP, TCP, 명명 된 파이프 및 MSMQ를 사용 하 여 작동 합니다.|  
|IIS 7.0|-ASP.NET 콘텐츠를 사용 하 여 WCF 서비스를 실행 합니다.<br />-다양 한 전송 프로토콜을 사용 하 여 인터넷을 통해 WCF 서비스를 실행 합니다.|-혜택 이었습니다.<br />ASP.NET 및 IIS 콘텐츠와 통합 합니다.|  
  
 애플리케이션이 배포되는 Windows 버전, 메시지를 보내는 데 필요한 전송, 애플리케이션에서 필요로 하는 프로세스와 애플리케이션 도메인 재활용 유형에 따라 선택하는 호스팅 환경이 달라집니다. 다음 표에서는 이러한 요구 사항과 관련된 데이터를 요약하여 설명합니다.  
  
|호스팅 환경|사용 가능한 플랫폼|지원되는 전송|프로세스 및 AppDomain 재활용|  
|-------------------------|---------------------------|--------------------------|-------------------------------------|  
|관리되는 애플리케이션("자체 호스팅")|[!INCLUDE[wxp](../../../includes/wxp-md.md)], [!INCLUDE[ws2003](../../../includes/ws2003-md.md)], [!INCLUDE[wv](../../../includes/wv-md.md)],<br /><br /> [!INCLUDE[lserver](../../../includes/lserver-md.md)]|HTTP,<br /><br /> net.tcp,<br /><br /> net.pipe,<br /><br /> net.msmq|아니요|  
|Windows 서비스(이전의 NT 서비스)|[!INCLUDE[wxp](../../../includes/wxp-md.md)], [!INCLUDE[ws2003](../../../includes/ws2003-md.md)], [!INCLUDE[wv](../../../includes/wv-md.md)],<br /><br /> [!INCLUDE[lserver](../../../includes/lserver-md.md)]|HTTP,<br /><br /> net.tcp,<br /><br /> net.pipe,<br /><br /> net.msmq|아니요|  
|IIS 5.1|[!INCLUDE[wxp](../../../includes/wxp-md.md)]|HTTP|예|  
|IIS 6.0|[!INCLUDE[ws2003](../../../includes/ws2003-md.md)]|HTTP|예|  
|WAS(Windows Process Activation Service)|[!INCLUDE[wv](../../../includes/wv-md.md)], [!INCLUDE[lserver](../../../includes/lserver-md.md)]|HTTP,<br /><br /> net.tcp,<br /><br /> net.pipe,<br /><br /> net.msmq|예|  
  
 신뢰할 수 없는 호스트에서 서비스나 확장을 실행하면 보안이 손상된다는 점에 주의해야 합니다. 또한 가장하여 <xref:System.ServiceModel.ServiceHost> 를 열 때 애플리케이션에서 사용자의 <xref:System.Security.Principal.WindowsIdentity> 를 캐싱하여 사용자가 로그오프되었는지 확인해야 합니다.  
  
## <a name="see-also"></a>참고자료

- [시스템 요구 사항](../../../docs/framework/wcf/wcf-system-requirements.md)
- [기본 프로그래밍 수명 주기](../../../docs/framework/wcf/basic-programming-lifecycle.md)
- [서비스 계약 구현](../../../docs/framework/wcf/implementing-service-contracts.md)
- [방법: IIS에서 WCF 서비스 호스팅](../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-iis.md)
- [방법: WAS에서 WCF 서비스 호스팅](../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-was.md)
- [방법: Host a WCF Service in a Managed Windows Service](../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-a-managed-windows-service.md)
- [방법: 관리 되는 응용 프로그램에서 WCF 서비스 호스팅](../../../docs/framework/wcf/how-to-host-a-wcf-service-in-a-managed-application.md)
