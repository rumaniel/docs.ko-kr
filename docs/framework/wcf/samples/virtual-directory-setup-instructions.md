---
title: 가상 디렉터리 설치 지침
ms.date: 03/30/2017
ms.assetid: 3c62cab5-81a4-48b6-ac8c-9ce33a85a157
ms.openlocfilehash: 6dccc5174e3fb9ab67023310d8c060d598a707c9
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70038642"
---
# <a name="virtual-directory-setup-instructions"></a>가상 디렉터리 설치 지침
WCF (Windows Communication Foundation) 샘플은%SystemDrive%\inetpub\wwwroot\servicemodelsamples 폴더에 매핑되는 servicemodelsamples 라는 공용 가상 디렉터리를 공유 하기 위한 것입니다.  
  
> [!NOTE]
> %SystemDrive%는 일반적으로 C: 또는 D:이며 IIS(인터넷 정보 서비스)가 설치된 드라이브 위치에 따라 달라집니다.  
  
 [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md) 에서 setupvroot 및 cleanupvroot 파일을 실행 하 여 가상 디렉터리를 만들 수 있습니다. 가상 디렉터리를 수동으로 만들려면 다음 절차를 사용합니다.  
  
## <a name="procedures"></a>절차  
  
#### <a name="to-create-a-virtual-directory-in-iis-70-or-75"></a>IIS 7.0 또는 7.5에서 가상 디렉터리를 만들려면  
  
1. **시작** 메뉴에서 **실행**을 클릭 한 다음 **inetmgr** 을 입력 하 여 인터넷 정보 서비스 (IIS) MMC 스냅인을 엽니다.  
  
2. 왼쪽 창에서 컴퓨터의 이름이 있는 노드를 확장 한 다음 **사이트** 노드를 확장 합니다.  
  
3. **기본 웹 사이트**를 마우스 오른쪽 단추로 클릭 한 다음 **응용 프로그램 추가** 를 선택 하 여 **응용 프로그램 추가 창을**엽니다.  
  
4. 창에서, 만들고 있는 `servicemodelsamples` 가상 디렉터리의 별칭으로를 입력 합니다.  
  
5. %SystemDrive%\inetpub\wwwroot\servicemodelsamples 디렉터리를 만듭니다.  
  
6. 실제 경로를 %SystemDrive%\inetpub\wwwroot\servicemodelsamples로 설정합니다.  대부분의 WCF 샘플은 빌드 시 서비스 실행 파일을 이 위치에 복사합니다.  
  
7. **확인**을 클릭합니다. WCF 샘플에 웹 애플리케이션이 만들어집니다.  
  
    > [!NOTE]
    > 모든 WCF 샘플은 동일한 servicemodelsamples 웹 응용 프로그램을 사용 하므로이 작업은 한 번만 수행 해야 합니다.  
  
    > [!NOTE]
    > 이 문서에서는 `virtual directory`라는 용어는 `Web application`과 동의어입니다.  
  
     가상 디렉터리를 만드는 것 외에도 해당 속성을 설정 하 여 WCF 서비스를 실행할 수 있도록 해야 합니다. 자세한 내용은 아래를 참조하세요.  
  
#### <a name="to-create-a-virtual-directory-in-iis-51-or-60"></a>IIS 5.1 또는 6.0에서 가상 디렉터리를 만들려면  
  
1. 명령 프롬프트 창을 열고를 입력 `start inetmgr` 하 여 인터넷 정보 서비스 (IIS) MMC 스냅인을 엽니다.  
  
2. 왼쪽 창에서 컴퓨터의 이름이 있는 노드를 확장 한 다음 **웹 사이트** 노드를 확장 합니다.  
  
3. **기본 웹 사이트** 를 마우스 오른쪽 단추로 클릭 하 고 **새로 만들기, 가상 디렉터리** 를 선택 하 여 가상 디렉터리 만들기 마법사를 엽니다.  
  
4. 마법사에서 만들고 있는 가상 `servicemodelsamples` 디렉터리의 별칭으로를 입력 합니다.  
  
5. 경로를 %SystemDrive%\inetpub\wwwroot\servicemodelsamples로 설정합니다. 대부분의 WCF 샘플은 빌드 시 서비스 실행 파일을 이 위치에 복사합니다.  
  
6. **다음**을 클릭합니다.  
  
7. 기본적으로 다음 확인란이 선택되어 있습니다.  
  
    - **읽기**  
  
    - **스크립트 실행 (예: ASP)**  
  
8. **다음**을 클릭 한 다음 **마침** 을 클릭 하 여 마법사를 완료 합니다.  
  
    > [!NOTE]
    > 모든 WCF 샘플에서 동일한 servicemodelsamples 가상 디렉터리를 사용 하므로이 작업은 한 번만 수행 해야 합니다.  
  
#### <a name="to-set-additional-virtual-directory-properties-in-iis-70-or-75"></a>IIS 7.0 또는 7.5에서 추가 가상 디렉터리 속성을 설정 하려면  
  
1. servicemodelsamples 노드를 클릭합니다. 창 아래쪽에 두 개의 뷰가 표시됩니다. 아직 선택 하지 않은 경우 **기능 보기** 를 선택 합니다.  
  
2. **디렉터리 검색**에 대 한 항목을 두 번 클릭 합니다.  
  
3. 작업 창에서 **사용** 옵션을 선택 합니다. 이렇게 하면 Internet Explorer를 사용하는 디렉터리의 디렉터리에 액세스할 수 있어 서비스를 디버깅할 때 도움이 됩니다.  
  
 마지막으로 다른 사용자가 액세스할 수 있도록 servicemodelsamples 폴더의 보안 속성을 설정해야 합니다. 자세한 내용은 아래를 참조하세요.  
  
#### <a name="to-set-additional-virtual-directory-properties-in-iis-51-or-60"></a>IIS 5.1 또는 6.0에서 추가 가상 디렉터리 속성을 설정하려면  
  
1. Servicemodelsamples 노드를 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다.  
  
2. 기본적으로 다음 확인란이 선택되어 있습니다.  
  
    - **읽기**  
  
    - **방문 기록**  
  
    - **이 리소스 인덱싱**  
  
3. **디렉터리 검색** 확인란을 선택 합니다. 이렇게 하면 Internet Explorer를 사용하는 디렉터리의 디렉터리에 액세스할 수 있어 서비스를 디버깅할 때 도움이 됩니다.  
  
#### <a name="to-set-security-properties-of-the-folder-in-iis-70-or-75"></a>IIS 7.0 또는 7.5에서 폴더의 보안 속성을 설정 하려면  
  
1. %SystemDrive%\inetpub\wwwroot\servicemodelsamples로 이동합니다.  
  
2. Servicemodelsamples 폴더를 마우스 오른쪽 단추로 클릭 하 고 **공유** 또는 **공유를**클릭 합니다.  
  
3. **추가** 단추의 왼쪽에 있는 아래쪽 화살표를 클릭 합니다.  
  
4. **찾기** 항목을 선택 합니다. **사용자 또는 그룹 선택** 창이 열립니다.  
  
5. **고급**을 클릭합니다.  
  
6. **위치**를 클릭 합니다. 이제 **위치** 창이 열립니다.  
  
7. 사용 중인 컴퓨터에 대한 항목을 선택합니다. 표시되어 있는 도메인이나 네트워크에 대한 항목이 아닌 로컬 컴퓨터를 선택해야 합니다. 컴퓨터를 선택한 후 **확인**을 클릭 합니다.  
  
8. **지금 찾기**를 클릭 합니다. 그러면 검색 결과가 로컬 컴퓨터와 연결된 개체로 채워집니다.  
  
9. **이름 (상대 고유 이름)** 열에서 **IIS_IUSRS** 항목을 찾습니다. 해당 항목을 선택 하 고 **확인** 을 클릭 하 여 검색 결과 창을 닫습니다.  
  
10. **확인** 을 클릭 하 여 **사용자 또는 그룹 선택** 창을 닫습니다.  
  
11. **공유** 를 클릭 하 여 변경 내용을 유지 합니다.  
  
12. 공유 사용에 대 한 변경 내용이 완료 되 면 **완료** 를 클릭 하 여 **파일 공유** 창을 닫습니다.  
  
#### <a name="to-set-security-properties-of-the-folder-in-iis-51-or-60"></a>IIS 5.1 또는 6.0에서 폴더의 보안 속성을 설정하려면  
  
1. %SystemDrive%\inetpub\wwwroot\servicemodelsamples로 이동합니다.  
  
2. **Servicemodelsamples** 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **공유 및 보안을 클릭 합니다.**  
  
3. **보안** 탭을 클릭합니다.  
  
4. IIS 6.0를 사용 하는 경우 **그룹 또는 사용자 이름** 상자에 **인터넷 게스트 계정** 이 표시 되는지 확인 합니다.  
  
     인터넷 게스트 계정이 표시되어 있지 않은 경우  
  
    1. **시작**을 클릭한 다음, **제어판**을 클릭합니다.  
  
    2. **사용자 계정** 아이콘이 표시 되지 않으면 **종류별 보기로 전환을**클릭 합니다.  
  
    3. **사용자 계정** 아이콘을 클릭 합니다.  
  
    4. "제어판 아이콘을 선택 하십시오."에서 **사용자 계정**을 클릭 합니다.  
  
    5. **사용자 계정** 대화 상자에서 **고급** 탭을 클릭 합니다.  
  
    6. **고급**을 클릭합니다.  
  
    7. **로컬 사용자 및 그룹** 대화 상자에서 **사용자** 폴더를 클릭 하 여 확장 합니다.  
  
    8. 오른쪽 창에서 **인터넷 게스트 계정**을 두 번 클릭 합니다.  
  
    9. **속성** 대화 상자에서 인터넷 게스트 계정으로 사용 되는 이름을 복사 합니다. 기본적으로 이름은 "USR_" 다음에 컴퓨터의 이름이 옵니다.  
  
    10. **속성** 대화 상자를 닫습니다.  
  
    11. **로컬 사용자 및 그룹** 대화 상자를 닫습니다.  
  
    12. **사용자 계정** 대화 상자를 닫습니다.  
  
    13. 기타 **사용자 계정** 대화 상자를 닫습니다.  
  
    14. **Servicemodelsamples 속성** 대화 상자의 **보안** 탭에서 **추가**를 클릭 합니다.  
  
    15. 컴퓨터 이름 뒤에 백슬래시를 입력 한 다음 인터넷 사용자 계정 이름 (예: mymachinename\\% InternetGuestAccountName%)을 붙여 넣습니다.  
  
    16. **이름 확인** 을 클릭 하 여 추가를 확인 합니다. 이름이 올바른 경우 모두 밑줄이 있는 대문자입니다.  
  
5. IIS 6.0의 경우 **그룹 또는 사용자 이름** 상자에도 NETWORK SERVICE가 나열 되는지 확인 합니다.  
  
     NETWORK SERVICE가 표시되어 있지 않은 경우  
  
    1. **추가**를 클릭합니다.  
  
    2. **사용자 또는 그룹 선택** 대화 상자에서 컴퓨터 이름, 백슬래시를 차례로 입력 합니다.  
  
    3. 백슬래시 뒤에 **service** 를 입력 합니다 (공백 없음).  
  
    4. **이름 확인**을 클릭 합니다.  
  
    5. 여러 이름을 찾은 경우 **네트워크 서비스** 를 선택 하 고 **확인**을 클릭 합니다.  
  
    6. **확인** 을 클릭 하 여 **사용자 또는 그룹 선택** 대화 상자를 닫습니다.  
  
6. IIS 5.1에서 Windows XP s p 2를 사용 하는 경우 **그룹 또는 사용자 이름** 상자에 인터넷 게스트 계정과 ASPNET이 모두 나열 되어 있는지 확인 합니다.  
  
     ASPNET 사용자는 기본 제공 **사용자** 보안 그룹의 멤버일 수 있습니다. 이 경우 **사용자** 그룹이 대화 상자에 표시 되는 경우 허용 된 사용자 목록에 별도의 항목으로 추가할 필요가 없습니다.  
  
     ASPNET이 **Users** 보안 그룹의 일부 인지 확인 하려면 다음을 수행 합니다.  
  
    1. **시작** 메뉴에서 **제어판**을 클릭 합니다.  
  
    2. **사용자 계정** 아이콘을 클릭 합니다.  
  
    3. **그룹** 열에서 **ASPNET** 의 값이 "사용자" 인지 확인 합니다.  
  
## <a name="see-also"></a>참고자료

- [인터넷 정보 서비스 호스팅 지침](../../../../docs/framework/wcf/samples/internet-information-service-hosting-instructions.md)
