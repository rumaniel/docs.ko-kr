---
title: '방법: Windows Server App Fabric을 사용하여 워크플로 서비스 호스팅'
ms.date: 03/30/2017
ms.assetid: 83b62cce-5fc2-4c6d-b27c-5742ba3bac73
ms.openlocfilehash: d1042aca7e4127c39e59bf0bf400974f0cecb1e8
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62039507"
---
# <a name="how-to-host-a-workflow-service-with-windows-server-app-fabric"></a>방법: Windows Server App Fabric을 사용하여 워크플로 서비스 호스팅
AppFabric에서 워크플로 서비스를 호스팅하는 것은 IIS/WAS에서 호스팅하는 것과 유사합니다. 유일한 차이점은 AppFabric에서 워크플로 서비스의 배포, 모니터링 및 관리를 위해 제공하는 도구입니다. 이 항목에서 만든 워크플로 서비스를 사용 합니다 [장기 실행 워크플로 서비스를 만드는](../../../../docs/framework/wcf/feature-details/creating-a-long-running-workflow-service.md)합니다. 이 항목에서는 워크플로 서비스를 만드는 방법을 안내하며, AppFabric을 사용하여 워크플로 서비스를 호스팅하는 방법을 설명합니다. Windows Server Appfabric에 대 한 자세한 내용은 참조 하세요. [Windows Server Appfabric](https://go.microsoft.com/fwlink/?LinkID=193037&clcid=0x409)합니다. 아래의 단계를 완료하기 전에 Windows Server AppFabric이 설치되어 있는지 확인합니다.  이 오픈 인터넷 정보 서비스 (inetmgr.exe)를 수행 하려면 서버 이름을 클릭 합니다 **연결** 사이트를 클릭 하 고 클릭 **기본 웹 사이트**합니다. 화면 오른쪽에 있는 이라는 섹션이 나타납니다 **App Fabric**합니다. 이 섹션(오른쪽 창의 맨 위에 있음)이 없으면 AppFabric이 설치되지 않은 것입니다. Windows Server Appfabric을 설치 하는 방법에 대 한 자세한 내용은 참조 하세요. [Windows Server App Fabric 설치](https://go.microsoft.com/fwlink/?LinkId=193136)합니다.  
  
### <a name="creating-a-simple-workflow-service"></a>간단한 워크플로 서비스 만들기  
  
1. Visual Studio 2012를 열고에서 만든 OrderProcessing 솔루션을 로드 합니다 [장기 실행 워크플로 서비스를 만드는](../../../../docs/framework/wcf/feature-details/creating-a-long-running-workflow-service.md) 항목입니다.  
  
2. 마우스 오른쪽 단추로 클릭 합니다 **OrderService** 프로젝트를 마우스 **속성** 선택 합니다 **웹** 탭 합니다.  
  
3. 에 **시작 작업** 속성 페이지의 섹션 선택 **특정 페이지** 편집 상자에 Service1.xamlx를 입력 합니다.  
  
4. 에 **서버** 속성 페이지의 섹션을 선택 **사용 하 여 로컬 IIS 웹 서버** 하 고 다음 URL 입력: `http://localhost/OrderService`합니다.  
  
5. 클릭 합니다 **가상 디렉터리 만들기** 단추입니다. 새 가상 디렉터리가 만들어지고 프로젝트가 빌드될 때 이 가상 디렉터리에 필요한 파일을 복사하도록 프로젝트가 설정됩니다.  또는 .xamlx, web.config 및 필요한 DLL을 가상 디렉터리에 수동으로 복사할 수 있습니다.  
  
### <a name="configuring-a-workflow-service-hosted-in-windows-server-app-fabric"></a>Windows Server AppFabric에서 호스팅되는 워크플로 서비스 구성  
  
1. 인터넷 정보 서비스 관리자(inetmgr.exe)를 엽니다.  
  
2. OrderService 가상 디렉터리로 이동 합니다 **연결** 창입니다.  
  
3. OrderService를 마우스 오른쪽 단추로 클릭 하 고 선택 **WCF 및 WF 서비스 관리**, **구성 하는 중...** . 합니다 **WCF 및 WF 응용 프로그램에 대 한 구성** 대화 상자가 표시 됩니다.  
  
4. 선택 된 **일반** 다음 스크린샷에 표시 된 대로 응용 프로그램에 대 한 일반 정보를 표시 하려면 탭 합니다.  
  
     ![App Fabric 구성 대화 상자의 일반 탭](../../../../docs/framework/wcf/feature-details/media/appfabricconfiguration-general.gif "AppFabricConfiguration-일반")  
  
5. 선택 된 **모니터링** 탭 합니다. 다음 스크린샷에 표시 된 대로 다양 한 모니터링 설정을 보여 줍니다.  
  
     ![App Fabric Configuration Monitoring 탭](../../../../docs/framework/wcf/feature-details/media/appfabricconfiguration-monitoring.gif "AppFabricConfiguration 모니터링")  
  
     워크플로 서비스를 구성 하는 방법에 대 한 자세한 내용은 참조 App Fabric의 모니터링 [App Fabric을 사용 하 여 모니터링 구성](https://go.microsoft.com/fwlink/?LinkId=193153)합니다.  
  
6. 선택 된 **워크플로 지 속성** 탭 합니다. 이 옵션을 사용 하면 다음 스크린샷에 표시 된 대로 App Fabric의 기본 지 속성 공급자를 사용 하도록 응용 프로그램을 구성할 수 있습니다.  
  
     ![App Fabric 구성 &#45; 지 속성](../../../../docs/framework/wcf/feature-details/media/appfabricconfiguration-persistence.gif "AppFabricConfiguration 지 속성")  
  
     Windows Server Appfabric에서 워크플로 지 속성을 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [Appfabric에서 워크플로 지 속성 구성](https://go.microsoft.com/fwlink/?LinkId=193148)합니다.  
  
7. 선택 된 **워크플로 호스트 관리** 탭 합니다. 이 옵션을 사용 하면 유휴 워크플로 서비스 인스턴스가 언로드되고 다음 스크린샷에 표시 된 대로 유지 하는 경우를 지정할 수 있습니다.  
  
     ![App Fabric 구성 워크플로 호스트 관리](../../../../docs/framework/wcf/feature-details/media/appfabricconfiguration-management.gif "AppFabricConfiguration 관리")  
  
     워크플로 호스트 관리 구성에 대 한 자세한 내용은 참조 하세요 [Appfabric에서 워크플로 호스트 관리 구성](https://go.microsoft.com/fwlink/?LinkId=193151)합니다.  
  
8. 선택 된 **자동 시작** 탭 합니다. 이 옵션을 사용 하면 다음 스크린샷에 표시 된 대로 응용 프로그램에서 워크플로 서비스에 대 한 자동 시작 설정을 지정할 수 있습니다.  
  
     ![App Fabric 자동을 보여주는 스크린 샷&#45;구성을 시작 합니다.](./media/how-to-host-a-workflow-service-with-windows-server-app-fabric/app-fabric-auto-start-configuration.gif)  
  
     자동 시작 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [구성 자동 시작 App Fabric을 사용 하 여](https://go.microsoft.com/fwlink/?LinkId=193150)입니다.  
  
9. 선택 된 **제한** 탭 합니다. 이 옵션을 사용 하면 다음 스크린샷에 표시 된 대로 워크플로 서비스에 대 한 제한 설정을 구성할 수 있습니다.  
  
     ![App Fabric 구성 제한를 보여주는 스크린샷.](./media/how-to-host-a-workflow-service-with-windows-server-app-fabric/app-fabric-throttling-configuration.gif)  
  
     제한을 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [Appfabric 제한 구성](https://go.microsoft.com/fwlink/?LinkId=193149)합니다.  
  
10. 선택 된 **보안** 탭 합니다. 이 옵션을 사용 하면 다음 스크린샷에 표시 된 것과 같이 응용 프로그램에 대 한 보안 설정을 구성할 수 있습니다.  
  
     ![App Fabric 보안 구성](../../../../docs/framework/wcf/feature-details/media/appfabricconfiguration-security.gif "AppFabricConfiguration 보안")  
  
     Windows Server App Fabric을 사용 하 여 보안을 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [App Fabric을 사용 하 여 보안 구성](https://go.microsoft.com/fwlink/?LinkId=193152)합니다.  
  
### <a name="using-windows-server-app-fabric"></a>Windows Server AppFabric 사용  
  
1. 솔루션을 빌드하여 필요한 파일을 가상 디렉터리에 복사합니다.  
  
2. OrderClient 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 선택 **디버그**하십시오 **새 인스턴스 시작** 클라이언트 응용 프로그램을 시작 합니다.  
  
3. 클라이언트를 실행 하 고 Visual Studio에서 표시는 **연결 보안 경고** 대화 상자를 클릭 합니다 **연결 안 함** 단추. 이렇게 하면 Visual Studio에서 디버깅을 위해 IIS 프로세스에 연결하지 않습니다.  
  
4. 클라이언트 애플리케이션은 워크플로 서비스를 즉시 호출한 다음 기다립니다. 워크플로 서비스는 유휴 상태가 되고 유지됩니다. 인터넷 정보 서비스(inetmgr.exe)를 시작하고 연결 창에서 OrderService로 이동한 다음 선택하여 이를 확인할 수 있습니다. 그런 다음 오른쪽 창에서 AppFabric 대시보드 아이콘을 클릭합니다. 지속 된 WF 인스턴스 아래에서 다음 스크린샷에 표시 된 것 처럼 하나의 지속형된 워크플로 서비스 인스턴스가 표시 됩니다.  
  
     ![App Fabric 대시보드를 보여 주는 스크린샷.](./media/how-to-host-a-workflow-service-with-windows-server-app-fabric/app-fabric-dashboard.gif)  
  
     합니다 **WF 인스턴스 기록** 워크플로 서비스 정품 인증 수, 워크플로 서비스 인스턴스 완료 수 및 오류가 있는 워크플로 인스턴스 수와 같은 워크플로 서비스에 대 한 정보를 나열 합니다. 링크를 표시할 활성 또는 유휴 인스턴스 아래에서 링크를 클릭 하면 다음 스크린샷에 표시 된 것과 같이 유휴 워크플로 인스턴스에 대 한 자세한 내용은 표시 됩니다.  
  
     ![지속형 워크플로 인스턴스 세부 정보를 보여 주는 스크린샷.](./media/how-to-host-a-workflow-service-with-windows-server-app-fabric/persisted-workflow-instance-detail.gif)  
  
     자세한 내용은 Windows Server App Fabric 기능과 사용 하는 방법 참조 [Windows Server App Fabric 호스팅 기능](https://go.microsoft.com/fwlink/?LinkID=193143&clcid=0x409)  
  
## <a name="see-also"></a>참고자료

- [장기 실행 워크플로 서비스 만들기](../../../../docs/framework/wcf/feature-details/creating-a-long-running-workflow-service.md)
- [Windows Server App Fabric 호스팅 기능](https://go.microsoft.com/fwlink/?LinkId=193143)
- [Windows Server Appfabric 설치](https://go.microsoft.com/fwlink/?LinkId=193136)
- [Windows Server App Fabric 설명서](https://go.microsoft.com/fwlink/?LinkID=193037&clcid=0x409)
