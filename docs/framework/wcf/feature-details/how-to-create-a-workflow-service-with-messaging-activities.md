---
title: '방법: 메시징 활동을 사용하여 워크플로 서비스 만들기'
ms.date: 03/30/2017
ms.assetid: 53d094e2-6901-4aa1-88b8-024b27ccf78b
ms.openlocfilehash: f5bb8df5936be1890bf744300daa7ccb68e341e3
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61787848"
---
# <a name="how-to-create-a-workflow-service-with-messaging-activities"></a>방법: 메시징 활동을 사용하여 워크플로 서비스 만들기
이 항목에서는 메시징 작업을 사용하여 간단한 워크플로 서비스를 만드는 방법을 보여 줍니다. 이 항목에서는 서비스가 메시징 작업만으로 구성된 워크플로 서비스를 만드는 방법에 중점을 둡니다. 실제 서비스의 워크플로에는 다른 많은 작업이 포함되어 있습니다. 이 항목의 서비스에서는 문자열을 받아서 호출자에게 반환하는 Echo라는 하나의 작업을 구현합니다. 이 항목은 시리즈로 된 두 항목 중 첫 번째 항목입니다. 다음 항목에서는 [방법: 서비스는 워크플로 응용 프로그램에서 액세스](../../../../docs/framework/wcf/feature-details/how-to-access-a-service-from-a-workflow-application.md) 이 항목에서 만든 서비스를 호출할 수 있는 워크플로 응용 프로그램을 만드는 방법에 설명 합니다.  
  
### <a name="to-create-a-workflow-service-project"></a>워크플로 서비스 프로젝트를 만들려면  
  
1. Start Visual Studio 2012.  
  
2. 클릭 합니다 **파일** 메뉴에서 **새로 만들기**를 차례로 **프로젝트** 표시할를 **새 프로젝트 대화 상자**. 선택 **워크플로** 설치 된 템플릿 목록에서 및 **WCF 워크플로 서비스 응용 프로그램** 프로젝트 형식 목록에서. 프로젝트 이름을 `MyWFService` 하 고 다음 그림에 나와 있는 것 처럼 기본 위치를 사용 합니다.  
  
     클릭 합니다 **확인** 해제 하려면 단추를 **새 프로젝트 대화 상자**합니다.  
  
3. 프로젝트가 생성되면 다음 그림과 같이 Service1.xamlx 파일이 디자이너에서 열립니다.  
  
     ![스크린샷은은 디자이너에서 Service1.xamlx 파일 열기를 보여 줍니다.](./media/how-to-create-a-workflow-service-with-messaging-activities/default-workflow-service.jpg)  
  
     레이블이 지정 된 활동을 마우스 오른쪽 단추로 클릭 **순차 서비스** 선택한 **삭제**합니다.  
  
### <a name="to-implement-the-workflow-service"></a>워크플로 서비스를 구현하려면  
  
1. 선택 된 **도구 상자** 도구 상자를 표시 된 창을 열어 압정을 클릭 하 고 화면 왼쪽에 탭 합니다. 확장 된 **메시징** 다음 그림과에서 같이 메시징 작업과 메시징 작업 템플릿을 표시 하려면 도구 상자의 섹션입니다.  
  
     ![확장 된 메시징 섹션을 사용 하 여 도구 상자를 보여 주는 스크린샷.](./media/how-to-create-a-workflow-service-with-messaging-activities/toolbox-messaging-section.jpg)  
  
2. 끌어서 놓기는 **ReceiveAndSendReply** 템플릿을 워크플로 디자이너로 합니다. 이렇게를 <xref:System.Activities.Statements.Sequence> 활동을 **수신** 작업과 그 뒤를 <xref:System.ServiceModel.Activities.SendReply> 다음 그림과에서 같이 작업 합니다.  
  
     ![ReceiveAndSendReply 템플릿의 보여주는 스크린샷.](./media/how-to-create-a-workflow-service-with-messaging-activities/receiveandsendreply-template.jpg)  
  
     <xref:System.ServiceModel.Activities.SendReply> 작업의 <xref:System.ServiceModel.Activities.SendReply.Request%2A> 속성이 `Receive` 작업이 회신하는 <xref:System.ServiceModel.Activities.Receive> 작업의 이름인 <xref:System.ServiceModel.Activities.SendReply>로 설정됩니다.  
  
3. 에 <xref:System.ServiceModel.Activities.Receive> 활동 유형 `Echo` 레이블이 지정 된 텍스트 상자에 **OperationName**합니다. 그러면 서비스가 구현하는 작업의 이름이 정의됩니다.  
  
     ![작업 이름을 지정 하는 위치를 보여 주는 스크린샷.](./media/how-to-create-a-workflow-service-with-messaging-activities/define-operation-name.jpg)  
  
4. 사용 하 여는 <xref:System.ServiceModel.Activities.Receive> 작업이 선택 속성 창을 클릭 하 여 열려 있지 않으면 합니다 **보기** 메뉴에서 **속성 창**합니다. 에 **속성 창** 표시 될 때까지 아래로 스크롤하여 **CanCreateInstance** 다음 그림에 나와 있는 것 처럼 확인란을 클릭 합니다. 이렇게 설정하면 메시지를 받을 때 필요한 경우 워크플로 서비스 호스트가 서비스의 새 인스턴스를 만들 수 있습니다.  
  
     ![CanCreateInstance 속성을 보여 주는 스크린샷.](./media/how-to-create-a-workflow-service-with-messaging-activities/cancreateinstance-property.jpg)  
  
5. 선택 합니다 <xref:System.Activities.Statements.Sequence> 활동을 클릭 합니다 **변수** 디자이너의 왼쪽된 아래 모퉁이의 단추입니다. 그러면 변수 편집기가 표시됩니다. 클릭 합니다 **변수 만들기** 작업에 보내진 문자열을 저장 하는 변수를 추가 합니다. 변수 이름을 `msg` 설정 및 해당 **변수** 다음 그림에 나와 있는 것 처럼 문자열을 입력 합니다.  
  
     ![변수를 추가 하는 방법을 보여 주는 스크린샷.](./media/how-to-create-a-workflow-service-with-messaging-activities/add-variable-msg-string.jpg)  
  
     클릭 합니다 **변수** 하려면 단추를 다시 변수 편집기를 닫습니다.  
  
6. 클릭 된 **정의...** 링크는 **콘텐츠** 텍스트 상자에 <xref:System.ServiceModel.Activities.Receive> 표시 하도록 작업을 **콘텐츠 정의** 대화 합니다. 선택는 **매개 변수** 라디오 단추를 클릭 합니다 **새 매개 변수를 추가** 링크를 입력 `inMsg` 에 **이름** 텍스트 상자에서 **문자열**에 **형식** 드롭다운 목록 상자 및 형식 목록 `msg` 에 **에 할당** 다음 그림에 표시 된 것과 같이 입력란.  
  
     ![추가 매개 변수 콘텐츠를 보여 주는 스크린샷.](./media/how-to-create-a-workflow-service-with-messaging-activities/adding-parameters-content.jpg)  
  
     그러면 받기 작업이 문자열 매개 변수를 받고 데이터가 `msg` 변수에 바인딩되도록 지정됩니다. 클릭 **확인** 닫으려면 합니다 **콘텐츠 정의** 대화 합니다.  
  
7. 클릭 된 **정의 하는 중...**  링크를 **콘텐츠** 상자에 <xref:System.ServiceModel.Activities.SendReply> 표시 하도록 작업을 **콘텐츠 정의** 대화 합니다. 선택를 **매개 변수** 라디오 단추를 클릭 합니다 **새 매개 변수를 추가** 링크를 입력 `outMsg` 에 **이름** 텍스트 상자 선택 **문자열**에 **형식** 드롭다운 목록 상자 및 `msg` 에 **값** 다음 그림에 나와 있는 것 처럼 텍스트 상자.  
  
     ![OutMsg 매개 변수를 추가 하는 방법을 보여주는 스크린샷.](./media/how-to-create-a-workflow-service-with-messaging-activities/outmsg-parameters-content.jpg)  
  
     그러면 <xref:System.ServiceModel.Activities.SendReply> 작업이 메시지 또는 메시지 계약 형식을 보내고 데이터가 `msg` 변수에 바인딩되도록 지정됩니다. 이 작업이 <xref:System.ServiceModel.Activities.SendReply> 작업이므로 이는 이 작업이 클라이언트에 다시 보내는 메시지를 채우는 데 `msg`의 데이터가 사용됨을 의미합니다. 클릭 **확인** 닫으려면 합니다 **콘텐츠 정의** 대화 합니다.  
  
8. 저장 하 고 클릭 하 여 솔루션을 빌드합니다 합니다 **빌드** 메뉴에서 **솔루션 빌드**합니다.  
  
## <a name="configure-the-workflow-service-project"></a>워크플로 서비스 프로젝트 구성  
 워크플로 서비스가 완료되었으므로 이 단원에서는 워크플로 서비스 솔루션을 손쉽게 호스팅하고 실행할 수 있도록 구성하는 방법에 대해 설명합니다. 이 솔루션은 ASP.NET Development Server를 사용하여 서비스를 호스팅합니다.  
  
#### <a name="to-set-project-start-up-options"></a>프로젝트 시작 옵션을 설정하려면  
  
1. 에 **솔루션 탐색기**, 마우스 오른쪽 단추로 클릭 **MyWFService** 선택한 **속성** 표시할 합니다 **프로젝트 속성** 대화 합니다.  
  
2. 선택 합니다 **웹** 탭을 선택한 **특정 페이지** 아래에 있는 **시작 작업** 유형과 `Service1.xamlx` 다음 그림에 나와 있는 것 처럼 텍스트 상자에 합니다.  
  
     ![프로젝트 속성 대화 상자를 보여 주는 스크린샷.](./media/how-to-create-a-workflow-service-with-messaging-activities/project-properties-dialog.jpg)  
  
     그러면 ASP.NET Development Server에서 Service1.xamlx에 정의된 서비스가 호스팅됩니다.  
  
3. Ctrl+F5를 눌러 서비스를 시작합니다. 그러면 다음 그림과 같이 바탕 화면의 오른쪽 아래에 ASP.NET Development Server 아이콘이 표시됩니다.  
  
     ![ASP.NET Developer Server 아이콘을 보여주는 스크린샷.](./media/how-to-create-a-workflow-service-with-messaging-activities/asp-net-dev-server-icon.jpg)  
  
     또한 Internet Explorer에 서비스에 대한 WCF 서비스 도움말 페이지가 표시됩니다.  
  
     ![WCF 서비스 도움말 페이지를 보여 주는 스크린샷.](./media/how-to-create-a-workflow-service-with-messaging-activities/wcf-service-help-page.jpg)  
  
4. 계속 진행 합니다 [방법: 서비스는 워크플로 응용 프로그램에서 액세스](../../../../docs/framework/wcf/feature-details/how-to-access-a-service-from-a-workflow-application.md) 항목에서는이 서비스를 호출 하는 워크플로 클라이언트를 만듭니다.  
  
## <a name="see-also"></a>참고자료

- [워크플로 서비스](../../../../docs/framework/wcf/feature-details/workflow-services.md)
- [워크플로 서비스 호스팅 개요](../../../../docs/framework/wcf/feature-details/hosting-workflow-services-overview.md)
- [메시징 작업](../../../../docs/framework/wcf/feature-details/messaging-activities.md)
