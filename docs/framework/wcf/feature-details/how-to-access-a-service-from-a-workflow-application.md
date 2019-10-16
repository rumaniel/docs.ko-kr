---
title: '방법: 워크플로 애플리케이션에서 서비스 액세스'
ms.date: 03/30/2017
ms.assetid: 925ef8ea-5550-4c9d-bb7b-209e20c280ad
ms.openlocfilehash: 178fb04244cb3e5075722877fdd3e2b5a92b8502
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61779643"
---
# <a name="how-to-access-a-service-from-a-workflow-application"></a>방법: 워크플로 애플리케이션에서 서비스 액세스
이 항목에서는 워크플로 콘솔 애플리케이션에서 워크플로 서비스를 호출하는 방법에 대해 설명합니다. 완료에 종속 된 [방법: 메시징 작업을 사용 하 여 워크플로 서비스 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-workflow-service-with-messaging-activities.md) 항목입니다. 이 항목에서는 워크플로 응용 프로그램에서 워크플로 서비스를 호출 하는 방법을 설명 합니다 하지만 동일한 방법은 워크플로 응용 프로그램에서 모든 Windows Communication Foundation (WCF) 서비스를 호출 하려면 사용할 수 있습니다.

### <a name="create-a-workflow-console-application-project"></a>워크플로 콘솔 애플리케이션 프로젝트 만들기

1. Start Visual Studio 2012.

2. 만든 MyWFService 프로젝트를 로드 합니다 [방법: 메시징 작업을 사용 하 여 워크플로 서비스 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-workflow-service-with-messaging-activities.md) 항목입니다.

3. 마우스 오른쪽 단추로 클릭 합니다 **MyWFService** 솔루션에는 **솔루션 탐색기** 선택한 **추가**, **새 프로젝트**합니다. 선택 **워크플로** 에 **설치 된 템플릿** 하 고 **워크플로 콘솔 응용 프로그램** 프로젝트 형식 목록에서. 다음 그림과 같이 프로젝트 이름을 MyWFClient로 지정하고 기본 위치를 사용합니다.

     ![새 프로젝트 추가 대화 상자](./media/how-to-access-a-service-from-a-workflow-application/add-new-project-dialog.jpg)

     클릭 합니다 **확인** 해제 하려면 단추를 **새 프로젝트 추가 대화 상자**합니다.

4. 프로젝트가 만들어진 후 디자이너에서 Workflow1.xaml 파일이 열립니다. 클릭 합니다 **도구 상자** 이미 열고 압정을 도구 상자 창을 열어 없으면 도구 상자를 열려면 탭 합니다.

5. 키를 눌러 **Ctrl**+**F5** 를 빌드하고 서비스를 시작 합니다. 이전과 마찬가지로 ASP.NET Development Server가 시작되고 Internet Explorer에 WCF 도움말 페이지가 표시됩니다. 이 페이지의 URI는 다음 단계에서도 사용됩니다.

     ![WCF 도움말 페이지 및 URI를 표시 하는 IE](./media/how-to-access-a-service-from-a-workflow-application/ie-wcf-help-page-uri.jpg)

6. 마우스 오른쪽 단추로 클릭 합니다 **MyWFClient** 프로젝트를 **솔루션 탐색기** 선택한 **추가** > **서비스 참조**합니다. 클릭 합니다 **Discover** 모든 서비스에 대 한 현재 솔루션을 검색 하는 단추입니다. 서비스 목록에서 Service1.xamlx 옆에 있는 삼각형을 클릭합니다. Service1 옆에 있는 삼각형을 클릭하여 Service1 서비스에 의해 구현되는 계약을 나열합니다. 확장을 **Service1** 에서 노드를 **Services** 목록입니다. Echo 작업에 표시 되는 **Operations** 다음 그림과에서 같이 목록입니다.

     ![서비스 참조 추가 대화 상자](./media/how-to-access-a-service-from-a-workflow-application/add-service-reference.jpg)

     기본 네임 스페이스를 유지 하 고 클릭 **확인** 해제 하는 **서비스 참조 추가** 대화 합니다. 다음 대화 상자가 표시됩니다.

     ![서비스 참조 알림 대화 상자를 추가 합니다.](./media/how-to-access-a-service-from-a-workflow-application/add-service-reference-dialog.jpg)

     클릭 **확인** 에 대화 상자를 닫습니다. 그런 다음 Ctrl+Shift+B를 눌러 솔루션을 빌드합니다. 라는 새 섹션이 추가 되었습니다 도구 상자에 공지 **MyWFClient.ServiceReference1.Activities**합니다. 다음 그림과 같이 이 섹션을 확장하고 추가된 Echo 작업을 확인합니다.

     ![도구 상자의 에코 작업](./media/how-to-access-a-service-from-a-workflow-application/echo-activity-toolbox.jpg)

7. 디자이너 화면으로 <xref:System.Activities.Statements.Sequence> 작업을 끌어서 놓습니다. 아래에 있는 것은 **제어 흐름** 도구 상자의 섹션입니다.

8. 사용 하 여 합니다 <xref:System.Activities.Statements.Sequence> 활동에 포커스를 클릭 합니다 **변수** 에 연결 하 고 이라는 문자열 변수를 추가 `inString`합니다. 기본값은 변수를 제공 `"Hello, world"` 이라는 문자열 변수 뿐만 아니라 `outString` 다음 다이어그램에 표시 된 대로 합니다.

     ![InString 변수를 추가합니다.](./media/how-to-access-a-service-from-a-workflow-application/add-instring-variable.jpg)

9. 끌어서 놓기는 **Echo** 활동을 <xref:System.Activities.Statements.Sequence>입니다. 속성 창에서 바인딩를 `inMsg` 인수를 `inString` 변수 및 `outMsg` 인수를는 `outString` 다음 그림에 나와 있는 것 처럼 변수. 그러면 `inString` 변수의 값이 작업에 전달되고 반환 값이 `outString` 변수에 추가됩니다.

     ![변수에 인수 바인딩](./media/how-to-access-a-service-from-a-workflow-application/bind-arguments-variables.jpg)

10. 끌어서 놓기는 **WriteLine** 활동 아래 합니다 **Echo** 서비스 호출에 의해 반환 된 문자열을 표시 하는 작업. 합니다 **WriteLine** 활동에는 **기본형** 도구 상자에서 노드. 바인딩를 **텍스트** 인수를 **WriteLine** 활동을는 `outString` 입력 하 여 변수 `outString` 에 있는 텍스트 상자에는 **WriteLine** 활동 합니다. 그러면 워크플로가 다음 그림과 같이 표시됩니다.

     ![완료된 클라이언트 워크플로](./media/how-to-access-a-service-from-a-workflow-application/complete-client-workflow.jpg)

11. MyWFService 솔루션을 마우스 오른쪽 단추로 클릭 하 고 선택 **시작 프로젝트 설정...** . 선택 합니다 **여러 개의 시작 프로젝트** 라디오 단추를 선택 **시작** 각 프로젝트에 대 한 합니다 **작업** 다음 그림에 나와 있는 것 처럼 열.

     ![시작 프로젝트 옵션](./media/how-to-access-a-service-from-a-workflow-application/startup-project-options.jpg)

12. Ctrl+F5를 눌러 서비스와 클라이언트를 둘 다 시작합니다. ASP.NET Development Server는 서비스를 호스트, Internet Explorer에 WCF 도움말 페이지가 표시 및 클라이언트 워크플로 응용 프로그램 콘솔 창에서 시작 되 고 ("Hello, world") 서비스에서 반환 된 문자열을 표시 합니다.

## <a name="see-also"></a>참고자료

- [워크플로 서비스](../../../../docs/framework/wcf/feature-details/workflow-services.md)
- [방법: 메시징 활동을 사용 하 여 워크플로 서비스 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-workflow-service-with-messaging-activities.md)
- [웹 프로젝트의 워크플로에서 WCF 서비스 사용](https://go.microsoft.com/fwlink/?LinkId=207725)
