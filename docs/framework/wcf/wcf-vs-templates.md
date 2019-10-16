---
title: WCF Visual Studio 템플릿
ms.date: 03/30/2017
ms.assetid: 6a608575-3535-4190-89da-911e24c8374f
ms.openlocfilehash: 8f7eb9ef5175c41a3378201f2f25f1fd914aef55
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69916785"
---
# <a name="wcf-visual-studio-templates"></a>WCF Visual Studio 템플릿
WCF (Windows Communication Foundation) Visual Studio 템플릿은 Visual Studio에서 WCF 서비스 및 주변 응용 프로그램을 신속 하 게 빌드하기 위해 사용할 수 있는 미리 정의 된 프로젝트 및 항목 템플릿입니다.  
  
## <a name="using-the-wcf-templates"></a>WCF 템플릿 사용  
 WCF Visual Studio 템플릿은 서비스 개발을 위한 기본 클래스 구조를 제공 합니다. 특히 이러한 템플릿은 서비스 계약, 데이터 계약, 서비스 구현 및 구성에 대한 기본 정의를 제공합니다. 이러한 템플릿을 사용하여 최소의 코드 상호 작용만으로 간단한 서비스를 만들 수 있을 뿐만 아니라 고급 서비스에 대한 빌딩 블록을 만들 수 있습니다.  
  
### <a name="wcf-service-library-project-template"></a>WCF 서비스 라이브러리 프로젝트 템플릿  
 WCF 서비스 라이브러리 프로젝트 템플릿은 **visual C#\Wcf** 및 **visual basic\wcf**의 새 프로젝트 대화 상자에서 사용할 수 있습니다.  
  
 **WCF 서비스** 템플릿을 사용 하 여 새 프로젝트를 만들면 새 프로젝트에 자동으로 다음 세 개의 파일이 포함 됩니다.  
  
- 서비스 계약 파일(IService1.cs 또는 IService1.vb). 서비스 계약 파일은 WCF 서비스 특성이 적용 되는 인터페이스입니다. 이 파일은 서비스를 정의하는 방법을 보여 주는 간단한 서비스 정의를 제공하고 매개 변수 기반 작업과 간단한 데이터 계약 샘플을 포함합니다. 이 파일은 WCF 서비스 프로젝트를 만든 후 코드 편집기에 표시 되는 기본 파일입니다.  
  
- 서비스 구현 파일(Service1.cs 또는 Service1.vb). 서비스 구현 파일은 서비스 계약 파일에 정의된 계약을 구현합니다.  
  
- 애플리케이션 구성 파일(App.config). 구성 파일은 보안 HTTP 바인딩을 사용 하 여 WCF 서비스 모델의 기본 요소를 제공 합니다. 또한 서비스에 대한 엔드포인트를 포함하고 메타데이터 교환을 활성화합니다.  
  
> [!NOTE]
> Visual Studio는 기본 구성 인 [WCF 서비스 호스트 (wcfsvchost.exe)](../../../docs/framework/wcf/wcf-service-host-wcfsvchost-exe.md)를 사용 하 여 실행할 때 app.config 파일을 프로젝트에 대 한 구성 파일로 인식 하도록 구성 되어 있습니다. 실행 파일에서 서비스 라이브러리를 호스팅할 경우 DLL의 구성 파일이 유효하지 않게 되므로 구성 코드를 실행 파일의 구성 파일로 이동해야 합니다.  
  
### <a name="wcf-service-application-template"></a>WCF 서비스 애플리케이션 템플릿  
 WCF 서비스 응용 프로그램 템플릿은 **visual C#\Wcf** 및 **Visual Basic\wcf**의 새 프로젝트 대화 상자에서 사용할 수 있습니다.  
  
 **WCF 웹 응용 프로그램 서비스** 템플릿을 사용 하 여 새 프로젝트를 만들 때 프로젝트에는 다음 4 개의 파일이 포함 됩니다.  
  
- 서비스 호스트 파일(service1.svc)  
  
- 서비스 계약 파일(IService1.cs 또는 IService1.vb).  
  
- 서비스 구현 파일(Service1.svc.cs 또는 Service1.svc.vb)  
  
- 웹 구성 파일(Web.config)  
  
 템플릿은 가상 디렉터리에 배포할 웹 사이트를 자동으로 만들고 해당 디렉터리에 서비스를 호스트합니다.  
  
### <a name="wcf-web-site-template"></a>WCF 웹 사이트 템플릿  
 WCF 웹 사이트 템플릿은 **visual C#\Web site\wcf 서비스** 및 **visual Basic\web Site\wcf 서비스**의 새 프로젝트 대화 상자에서 사용할 수 있습니다. 이 템플릿은 WCF 서비스 애플리케이션 템플릿과 같은 파일을 만들지만 ASP.NET 웹 사이트인 것처럼 정리합니다. App_Code 및 App_Data 폴더가 생성됩니다.  
  
### <a name="wcf-service-item-template"></a>WCF 서비스 항목 템플릿  
 WCF 서비스 항목 템플릿은 기존 Visual Studio 프로젝트에 WCF 서비스를 신속 하 게 추가 하는 방법을 제공 하는 사용자 지정 템플릿입니다.  
  
 이 템플릿을 사용 하려면 **솔루션 탐색기** 창으로 이동 하 여 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 **추가**를 가리킨 다음 **새 항목** 을 클릭 하 여 **새 항목 추가** 대화 상자를 시작 합니다.  
  
 서비스 인터페이스와 구현 파일은 루트 프로젝트 폴더에 있습니다.  
  
 템플릿은 새 서비스의 구성 섹션과 기존 구성 파일이 호환 가능한 형식인 경우 서로 병합하려고 합니다.  
  
 기존 프로젝트가 웹 프로젝트인 경우 서비스 호스트 파일(service1.svc)도 만들어집니다.  
  
### <a name="wcf-wf-service-project-and-item-template"></a>WCF WF 서비스 프로젝트 및 항목 템플릿.  
 이러한 템플릿은 웹 서비스 처럼 액세스할 수 있는 워크플로 인 워크플로 서비스를 호스팅하는 WCF 서비스를 만듭니다. XAML 또는 필수 프로그래밍 모델에 대한 별도의 템플릿이 존재합니다. 이 템플릿을 사용하여 순차 또는 상태 시스템 워크플로를 만들 수 있습니다. 이러한 유형의 워크플로에 [대 한 자세한 내용은 방법: 워크플로](../windows-workflow-foundation/how-to-create-a-workflow.md)를 만듭니다. 워크플로 프로젝트를 만드는 방법에 대 한 자세한 내용은 [레거시 워크플로 프로젝트 만들기](/visualstudio/workflow-designer/creating-legacy-workflow-projects)를 참조 하세요.  
  
 Visual Studio designer는 코드 기반 항목 대신 XOML 형식 워크플로를 사용 하는 경우 더욱 응답성이 향상 됩니다. 만들어지는 기본 워크플로 형식은 XOML 워크플로입니다.  
  
### <a name="wcf-syndication-service-library-template"></a>WCF 배포 서비스 라이브러리 템플릿  
 이 템플릿을 사용 하면 RSS 또는 ATOM 형식의 피드를 WCF 서비스로 노출할 수 있습니다. 자세한 내용은 [WCF 배포](../../../docs/framework/wcf/feature-details/wcf-syndication.md)를 참조 하세요.  
  
#### <a name="changing-the-address-of-the-feed"></a>피드의 주소 변경  
 배포 템플릿은 실행 중에 Internet Explorer를 사용합니다. Visual Studio의 **솔루션 탐색기** 에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택한 다음 **디버그** 탭을 선택 하면 템플릿의 기본 주소를 볼 수 있습니다. Internet Explorer는 이 주소에서 피드를 열려고 합니다.  
  
 피드의 주소를 변경 하는 경우에는 **디버그** 탭 에서도 주소를 변경 해야 합니다. 이와 같이 하지 않으면 Internet Explorer는 기본 주소에서 피드를 열려고 시도한 다음 실패합니다.  
  
### <a name="ajax-enabled-wcf-service-item-template"></a>AJAX 사용 WCF 서비스 항목 템플릿  
 이 템플릿은 AJAX 컨트롤을 WCF 서비스로 노출 합니다. AJAX 컨트롤에 대 한 자세한 내용은 [ajax 컨트롤 설명서](https://go.microsoft.com/fwlink/?LinkId=96717)를 참조 하세요.  
  
### <a name="silverlight-enabled-wcf-service-item-template"></a>Silverlight 사용 WCF 서비스 항목 템플릿  
 이 템플릿은 Silverlight 클라이언트 또는 프런트 엔드에 데이터를 제공하는 웹 서비스를 만듭니다. 웹 사이트 또는 웹 응용 프로그램 프로젝트에 템플릿을 추가 하 여 WCF 서비스를 만들 수 있습니다. 여기에는 Silverlight 클라이언트와의 통신을 지 원하는 서비스 코드와 구성이 포함 됩니다. 그런 다음 **서비스 참조 추가** 를 사용 하 여 서비스의 클라이언트 프록시를 클라이언트에 추가 하 고 silverlight 클라이언트와 SILVERLIGHT 사용 WCF 서비스 간에 데이터를 교환할 수 있습니다.  
  
 이 템플릿에 액세스 하려면 **솔루션 탐색기**에서 웹 사이트 또는 웹 응용 프로그램 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **새 항목 추가**를 클릭 한 다음 **Silverlight 사용 WCF 서비스**를 클릭 합니다.  
  
> [!NOTE]
> Silverlight 사용 WCF 서비스는 보안 설정을 사용하지 않고 `basicHttpBinding` 엔드포인트를 노출합니다. 따라서 이 서비스에 연결하는 모든 클라이언트가 서비스에 대한 정보를 얻을 수 있습니다. 서비스와 클라이언트 간에 교환되는 메시지도 서명되거나 암호화되지 않습니다. 엔드포인트를 올바르게 보안하려면 ASP.NET 인증, HTTPS 또는 기타 메커니즘을 사용해야 합니다.  
  
## <a name="see-also"></a>참고자료

- [WCF 서비스 호스트(WcfSvcHost.exe)](../../../docs/framework/wcf/wcf-service-host-wcfsvchost-exe.md)
- [WCF 테스트 클라이언트(WcfTestClient.exe)](../../../docs/framework/wcf/wcf-test-client-wcftestclient-exe.md)
