---
title: 확장된 보호 정책
ms.date: 03/30/2017
ms.assetid: e2616a10-317e-4c34-8023-0c015a80a82f
ms.openlocfilehash: c7c2e85872c158facb2de91a7413ac5a04491d7f
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70044991"
---
# <a name="extended-protection-policy"></a>확장된 보호 정책
확장된 보호는 MITM(Man-In-The-Middle, 메시지 가로채기) 공격을 방지하기 위한 보안 이니셔티브입니다. MITM 공격은 공격자가 클라이언트의 자격 증명을 가로채 서버로 전달하는 보안 위협입니다.  
  
## <a name="demonstrates"></a>세부 항목  
 확장된 보호  
  
## <a name="discussion"></a>토론  
 애플리케이션이 Kerberos, 다이제스트 또는 NTLM(HTTPS 사용)을 사용하여 인증할 때는 TLS(전송 수준 보안) 채널이 먼저 설정된 다음 이 보안 채널을 사용하여 인증이 진행됩니다. 그러나 SSL을 통해 생성되는 세션 키와 인증 중에 생성되는 세션 키는 서로 바인딩되지 않습니다. 따라서 클라이언트와 서버 사이에 MITM이 개입하여 클라이언트로부터의 요청을 전달하기 시작할 수 있습니다. 이는 전송 채널 자체가 보안 채널인 경우에도 해당되는데, 보안 채널이 클라이언트에서 설정되었는지 MITM에서 설정되었는지를 서버에서는 알 수 있는 방법이 없기 때문입니다. 이 경우 해결 방법은 MITM이 있는 경우 서버에서 이를 감지할 수 있도록 외부 TLS 채널을 내부 인증 채널과 바인딩하는 것입니다.  
  
> [!NOTE]
> 이 샘플은 IIS에서 호스트되는 경우에만 작동하며, Cassini(Visual Studio 개발 서버)에서는 HTTPS를 지원하지 않으므로 Cassini에서는 작동하지 않습니다.  
  
> [!NOTE]
> 이 기능은 현재 Windows 7에서만 사용할 수 있습니다. 다음 단계는 Windows 7에만 해당됩니다.  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. **제어판**, **프로그램 추가/제거**, **Windows 기능**에서 인터넷 정보 서비스를 설치 합니다.  
  
2. Windows **기능**, **인터넷 정보 서비스**, **World Wide Web 서비스**, **보안**및 **windows 인증**에 **windows 인증** 을 설치 합니다.  
  
3. **Windows 기능**, **Microsoft .NET Framework 3.5.1**및 **Windows Communication Foundation http 활성화** **Windows Communication Foundation http 활성화** 를 설치 합니다.  
  
4. 이 샘플을 사용하려면 클라이언트에서 서버와의 보안 채널을 설정해야 하므로, IIS(인터넷 정보 서비스) 관리자에서 설치할 수 있는 서버 인증서가 있어야 합니다.  
  
    1. IIS 관리자를 엽니다. 루트 노드 (컴퓨터 이름)를 선택한 경우 **기능 보기** 탭에 표시 되는 **서버 인증서**를 엽니다.  
  
    2. 이 샘플을 테스트하기 위해 자체 서명된 인증서를 만듭니다. Internet Explorer에서 인증서가 안전하지 않다는 메시지가 표시되지 않도록 하려면 인증서를 신뢰할 수 있는 인증서 루트 인증 기관 저장소에 설치합니다.  
  
5. 기본 웹 사이트에 대 한 **작업** 창을 엽니다. **사이트 편집**, **바인딩**을 클릭 합니다. HTTPS가 아직 없으면 포트 번호 443을 사용하여 HTTPS를 형식으로 추가합니다. 이전 단계에서 만든 SSL 인증서를 할당합니다.  
  
6. 서비스를 빌드합니다. 그러면 IIS에 가상 디렉터리가 만들어지고 서비스를 웹에서 호스트하는 데 필요한 .dll, .svc 및 .config 파일이 복사됩니다.  
  
7. IIS 관리자를 엽니다. 이전 단계에서 만든 가상 디렉터리 (**Extendedprotection**)를 마우스 오른쪽 단추로 클릭 합니다. **응용 프로그램으로 변환을**선택 합니다.  
  
8. IIS 관리자에서이 가상 디렉터리에 대 한 **인증** 모듈을 열고 **Windows 인증**을 사용 하도록 설정 합니다.  
  
9. **Windows 인증** 에서이 가상 디렉터리에 대 한 **고급 설정** 을 열고 **필수**로 설정 합니다.  
  
10. 브라우저 창에서 정규화된 도메인 이름을 제공하여 HTTPS URL에 액세스하면 서비스를 테스트할 수 있습니다. 원격 컴퓨터에서 이 URL에 액세스하려면 들어오는 모든 HTTP 및 HTTPS 연결에 대해 방화벽이 열려 있는지 확인합니다.  
  
11. 클라이언트 구성 파일을 열고 `<<full_machine_name>>`을 대체하는 엔드포인트 주소 특성 또는 클라이언트의 정규화된 도메인 이름을 제공합니다.  
  
12. 클라이언트를 실행합니다. 클라이언트가 서비스와 통신하며, 이때 보안 채널이 설정되고 확장된 보호가 사용됩니다.  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Security\ExtendedProtection`
