---
title: WCF 개발 도구 사용
ms.date: 03/30/2017
ms.assetid: 054adb87-c244-4d5a-83d1-0b2b44bd454b
ms.openlocfilehash: ef20d13ade41992e6babc0ebb3a985aabb686ed3
ms.sourcegitcommit: cf9515122fce716bcfb6618ba366e39b5a2eb81e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69040416"
---
# <a name="using-the-wcf-development-tools"></a>WCF 개발 도구 사용
이 섹션에서는 WCFservice 개발에 도움이 될 수 있는 Visual Studio 개발 도구에 대해 설명 합니다.  
  
 Visual Studio 템플릿을 기반으로 사용 하 여 서비스를 신속 하 게 빌드한 다음 WCF 서비스 자동 호스트 및 WCF 테스트 클라이언트를 사용 하 여 서비스를 디버깅 하 고 테스트할 수 있습니다. 이러한 도구를 함께 사용하면 디버그 및 테스트를 원활하고 빠르게 수행할 수 있으며 초기 단계에서 호스팅 모델에 주력할 필요가 없습니다.  
 
 > [!NOTE]
 > Visual Studio 2017부터 WCF 개발 도구는 기본적으로 설치 되지 않습니다. 이러한 기능을 사용 하려면 Visual Studio 설치 관리자에서 Windows Communication Foundation 구성 요소가 선택 되어 있는지 확인 해야 합니다.
  
## <a name="the-wcf-developer-tools"></a>WCF 개발자 도구  
 [WCF Visual Studio 템플릿](../../../docs/framework/wcf/wcf-vs-templates.md)  
  
 Visual Studio에서 미리 정의 된 Visual Studio 프로젝트 및 항목 템플릿을 사용 하 여 WCF 서비스와 주변 응용 프로그램을 빠르게 빌드할 수 있습니다.  
  
 [WCF 서비스 호스트(WcfSvcHost.exe)](../../../docs/framework/wcf/wcf-service-host-wcfsvchost-exe.md)  
  
 WCF 서비스 자동 호스트 (Wcfsvchost.exe)를 사용 하면 Visual Studio 디버거 (F5)를 시작 하 여 구현 된 서비스를 자동으로 호스트 하 고 테스트할 수 있습니다. 그런 다음 WCF 테스트 클라이언트 (Wcftestclient.exe) 또는 자체 클라이언트를 사용 하 여 서비스를 테스트 하 여 잠재적인 오류를 찾아 수정할 수 있습니다.  
  
 [WCF 테스트 클라이언트(WcfTestClient.exe)](../../../docs/framework/wcf/wcf-test-client-wcftestclient-exe.md)  
  
 WCF 테스트 클라이언트 (Wcftestclient.exe)는 임의 형식의 매개 변수를 입력 하 고, 해당 입력을 서비스에 제출 하 고, 서비스가 다시 보내는 응답을 볼 수 있는 GUI 도구입니다. WCF 서비스 자동 호스트와 결합 될 때 원활한 서비스 테스트 환경을 제공 합니다.  
  
 [XML에서 데이터 형식 클래스 생성](../../../docs/framework/wcf/generating-data-type-classes-from-xml.md)  
  
 클립보드에 저장된 XML 데이터는 코드 페이지로 붙여 넣을 수 있습니다. 데이터에 정의된 클래스는 코드 형식으로 변환됩니다.  
  
## <a name="using-the-tools-without-administrator-privilege"></a>관리자 권한 없이 도구 사용  
 관리자 권한이 없는 사용자가 WCF 서비스를 개발할 수 있도록 Visual Studio를 설치 하는 동안 네임 스페이스 "http://+:8731/Design_Time_Addresses"에 대 한 ACL (Access Control 목록)이 만들어집니다. ACL은 (UI)로 설정되며 시스템에 로그온한 모든 대화식 사용자를 포함합니다. 관리자는 이 ACL에서 사용자를 추가 또는 제거하거나 추가 포트를 열 수 있습니다. WCF 또는 WF 템플릿에서 이 ACL을 사용하여 데이터를 기본 구성으로 보내거나 받을 수 있습니다. 또한 사용자가 관리자 권한을 부여 하지 않고 WCF 서비스 자동 호스트 (Wcfsvchost.exe)를 사용할 수 있습니다.  
  
 [!INCLUDE[wv](../../../includes/wv-md.md)]의 강화된 관리자 계정으로 Netsh.exe를 사용하여 액세스 권한을 수정할 수 있습니다. 다음은 Netsh.exe를 사용하는 예입니다.  
  
```  
netsh http add urlacl url=http://+:8001/MyService user=<domain>\<user>  
```  
  
 Netsh.exe에 대 한 자세한 내용은 [Netsh.exe 도구 및 명령줄 스위치를 사용 하는 방법](https://go.microsoft.com/fwlink/?LinkId=97877)을 참조 하십시오.  
  
## <a name="see-also"></a>참고자료

- [WCF Visual Studio 템플릿](../../../docs/framework/wcf/wcf-vs-templates.md)
- [WCF 서비스 호스트(WcfSvcHost.exe)](../../../docs/framework/wcf/wcf-service-host-wcfsvchost-exe.md)
- [WCF 테스트 클라이언트(WcfTestClient.exe)](../../../docs/framework/wcf/wcf-test-client-wcftestclient-exe.md)
