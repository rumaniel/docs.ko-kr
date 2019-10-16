---
title: Discovery Security 샘플
ms.date: 03/30/2017
ms.assetid: b8db01f4-b4a1-43fe-8e31-26d4e9304a65
ms.openlocfilehash: dfc0dfcd3b4d814a158b328ef202d5438e583a8c
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70039811"
---
# <a name="discovery-security-sample"></a>Discovery Security 샘플
검색 사양에서는 검색 프로세스에 참여하는 엔드포인트를 보호하도록 요구하지 않습니다. 그러나 검색 메시지의 보안을 강화하면 메시지 변경, 서비스 거부, 재생, 스푸핑 같은 다양한 형식의 공격을 완화할 수 있습니다. 이 샘플에서는 WS-Discovery 사양의 8.2단원에 설명된 압축 서명 형식을 사용하여 메시지 서명을 컴퓨팅 및 확인하는 사용자 지정 채널을 구현합니다. 이 샘플에서는 [2005 검색 사양과](https://go.microsoft.com/fwlink/?LinkId=177912) [1.1 버전](https://go.microsoft.com/fwlink/?LinkId=179677)을 모두 지원 합니다.  
  
 사용자 지정 채널은 검색 및 알림 엔드포인트의 기존 채널 스택 맨 위에서 적용됩니다. 이렇게 하면 서명 헤더가 보내는 모든 메시지에 적용됩니다. 서명은 받은 메시지에서 확인되며 서명이 일치하지 않거나 서명이 없는 메시지는 삭제됩니다. 메시지 서명 및 확인을 위해 이 샘플에서는 인증서를 사용합니다.  
  
## <a name="discussion"></a>토론  
 WCF는 확장성이 우수하므로 사용자가 채널을 원하는 대로 사용자 지정할 수 있습니다. 이 샘플에서는 보안 채널을 빌드하는 검색 보안 바인딩 요소를 구현합니다. 보안 채널에서는 메시지 서명을 적용 및 확인하며 현재 스택의 맨 위에서 적용됩니다.  
  
 보안 바인딩 요소는 보안 채널 팩터리 및 채널 수신기를 빌드합니다.  
  
## <a name="secure-channel-factory"></a>보안 채널 팩터리  
 보안 채널 팩터리는 메시지 헤더에 압축 서명을 추가하는 이중 채널 또는 출력을 만듭니다. 메시지를 가능한 한 작게 유지하기 위해 압축 서명 형식이 사용됩니다. 다음 예제에서는 압축 서명의 구조를 보여 줍니다.  
  
```xml  
<d:Security ... >   
  [<d:Sig Scheme="xs:anyURI"   
         [KeyId="xs:base64Binary"]?  
          Refs="..."  
         [PrefixList]="xs:NMTOKENS"   
          Sig="xs:base64Binary"   
          ... />]?  
  ...   
</d:Security>  
```  
  
> [!NOTE]
> 2008 검색 버전 프로토콜에는 `PrefixList`가 추가되었습니다.  
  
 서명을 컴퓨팅하기 위해 이 샘플에서는 확장된 서명 항목을 확인합니다. XML 서명(`SignedInfo`)은 WS-Discovery 사양에서 요구하는 대로 `ds` 네임스페이스 접두사를 사용하여 만듭니다. 검색 및 주소 지정 네임스페이스의 본문과 모든 헤더는 서명에서 참조되므로 변경할 수 없습니다. 참조 되는 각 요소는 배타적 정식화 (http://www.w3.org/2001/10/xml-exc-c14n# )를 사용 하 여 변환 된 다음 sha-1 다이제스트 값 (http://www.w3.org/2000/09/xmldsig#sha1 )이 계산 됩니다. 참조 되는 모든 요소 및 해당 다이제스트 값에 따라 서명 값은 RSA 알고리즘 (http://www.w3.org/2000/09/xmldsig#rsa-sha1 )을 사용 하 여 계산 됩니다.  
  
 메시지는 클라이언트에서 지정한 인증서를 사용하여 서명됩니다. 저장소 위치, 이름 및 인증서 주체 이름은 바인딩 요소를 만들 때 지정해야 합니다. 압축 서명의 `KeyId`는 서명 토큰의 키 식별자를 나타내며 서명 토큰의 SKI(주체 키 식별자)나 서명 토큰의 공개 키에 대한 SHA-1 해시(SKI가 없는 경우)입니다.  
  
## <a name="secure-channel-listener"></a>보안 채널 수신기  
 보안 채널 수신기에서는 받은 메시지의 압축 서명을 확인하는 이중 채널 또는 입력을 만듭니다. 서명을 확인하려면 메시지에 첨부된 압축 서명에 지정된 `KeyId`를 사용하여 지정된 저장소에서 인증서를 선택합니다. 서명이 없거나 서명 확인에 실패한 메시지는 삭제됩니다. 보안 바인딩을 사용하기 위해 이 샘플에서는 추가된 검색 보안 바인딩 요소를 사용하여 사용자 지정 <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint> 및 <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint>를 만드는 팩터리를 정의합니다. 이 보안 엔드포인트는 검색 알림 수신기와 검색 가능한 서비스에서 사용할 수 있습니다.  
  
## <a name="sample-details"></a>샘플 세부 정보  
 이 샘플에는 한 개의 라이브러리와 네 개의 콘솔 응용 프로그램이 포함되어 있습니다.  
  
- **DiscoverySecurityChannels**: 보안 바인딩을 노출 하는 라이브러리입니다. 라이브러리에서는 들어오고 나가는 메시지의 압축 서명을 계산하고 확인합니다.  
  
- **서비스**: 자체 호스트 된 ICalculatorService 계약을 노출 하는 서비스입니다. 이 서비스는 검색 가능한 것으로 표시됩니다. 사용자는 인증서에 대한 저장소 위치, 이름, 주체 이름 또는 기타 고유 식별자와 클라이언트 인증서(들어오는 메시지의 서명을 확인하는 데 사용되는 인증서)가 있는 저장소를 지정하여 메시지에 서명하는 데 사용되는 인증서의 세부 정보를 지정합니다. 이러한 세부 정보를 기반으로 보안이 향상된 UdpDiscoveryEndpoint가 빌드되고 사용됩니다.  
  
- **클라이언트**: 이 클래스는 ICalculatorService를 검색 하 고 서비스에서 메서드를 호출 하려고 합니다. 이 경우에도 보안이 향상된 <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>가 빌드되고 메시지를 서명 및 확인하는 데 사용됩니다.  
  
- **AnnouncementListener**: 온라인 및 오프 라인 알림을 수신 하 고 보안 알림 끝점을 사용 하는 자체 호스팅 서비스입니다.  
  
> [!NOTE]
> Setup.bat가 여러 번 실행되는 경우 인증서 관리자는 중복 인증서가 있으므로 추가할 인증서를 선택하라는 메시지를 표시합니다. 이 경우 중복이 이미 만들어졌으므로 Setup.bat를 중단하고 Cleanup.bat를 호출해야 합니다. Cleanup.bat에서도 삭제할 인증서를 선택하라는 메시지를 표시합니다. 목록에서 인증서를 선택하고 남아 있는 인증서가 없을 때까지 Cleanup.bat를 계속 실행합니다.  
  
#### <a name="to-use-this-sample"></a>이 샘플을 사용하려면  
  
1. Visual Studio 용 개발자 명령 프롬프트에서 Setup.exe 스크립트를 실행 합니다. 이 샘플에서는 인증서를 사용하여 메시지를 서명하고 확인합니다. 이 스크립트에서는 Makecert.exe를 사용하여 인증서를 만든 다음 Certmgr.exe를 사용하여 인증서를 설치합니다. 이 스크립트는 관리자 권한으로 실행해야 합니다.  
  
2. 샘플을 빌드하고 실행 하려면 Visual Studio에서 보안 .sln 파일을 열고 **모두 다시 빌드**를 선택 합니다. 솔루션 속성을 업데이트 하 여 여러 프로젝트 시작: DiscoverySecureChannels을 제외한 모든 프로젝트에 대해 **시작** 을 선택 합니다. 솔루션을 정상적으로 실행합니다.  
  
3. 샘플을 사용하여 작업을 수행한 후 이 샘플에 대해 만들어진 인증서를 제거하는 Cleanup.bat 스크립트를 실행합니다.  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Scenario\DiscoveryScenario`  
