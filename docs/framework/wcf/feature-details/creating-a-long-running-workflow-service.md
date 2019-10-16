---
title: 장기 실행 워크플로 서비스 만들기
ms.date: 03/30/2017
ms.assetid: 4c39bd04-5b8a-4562-a343-2c63c2821345
ms.openlocfilehash: ceda43cc41ceb3381b4700d6ea8b1871e368dccc
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70856197"
---
# <a name="creating-a-long-running-workflow-service"></a>장기 실행 워크플로 서비스 만들기

이 항목에서는 장기 실행 워크플로 서비스를 만드는 방법에 대해 설명합니다. 장기 실행 워크플로 서비스는 장기간 실행될 수 있습니다. 특정 지점에서 워크플로는 추가 정보를 기다리며 유휴 상태가 될 수 있습니다. 이 경우 워크플로는 SQL 데이터베이스에 유지되고 메모리에서 제거됩니다. 추가 정보를 사용할 수 있으면 워크플로 인스턴스가 다시 메모리에 로드되어 계속 실행됩니다.  이 시나리오에서는 매우 간단한 주문 시스템을 구현합니다.  클라이언트가 워크플로 서비스에 초기 메시지를 보내 주문을 시작하고, 워크플로 서비스는 주문 ID를 클라이언트에 반환합니다. 이 시점에서 워크플로 서비스가 클라이언트에서 다른 메시지를 기다리며 유휴 상태가 되고 SQL Server 데이터베이스에 유지됩니다.  클라이언트가 품목을 주문하기 위해 다음 메시지를 보내면 워크플로 서비스는 메모리에 다시 로드되고 주문 처리를 마칩니다. 코드 샘플에서 워크플로 서비스는 품목이 주문에 추가되었음을 나타내는 문자열을 반환합니다. 코드 샘플은 이 기술의 실제 애플리케이션이라기보다는 장기 실행 워크플로 서비스를 보여 주는 간단한 샘플입니다. 이 항목에서는 Visual Studio 2012 프로젝트 및 솔루션을 만드는 방법을 알고 있다고 가정 합니다.

## <a name="prerequisites"></a>전제 조건

이 연습을 사용하려면 다음 소프트웨어를 설치해야 합니다.

1. Microsoft SQL Server 2008

2. Visual Studio 2012

3. Microsoft [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)]

4. WCF 및 Visual Studio 2012에 익숙하고 프로젝트/솔루션을 만드는 방법을 알고 있어야 합니다.

### <a name="to-setup-the-sql-database"></a>SQL 데이터베이스를 설정하려면

1. 워크플로 서비스 인스턴스가 유지되려면 Microsoft SQL Server가 설치되어 있어야 하고 유지된 워크플로 인스턴스를 저장하도록 데이터베이스를 구성해야 합니다. **시작** 단추를 클릭 하 고 **모든 프로그램**, **Microsoft SQL Server 2008**및 **Microsoft SQL Management Studio**를 선택 하 여 microsoft sql Management Studio를 실행 합니다.

2. **연결** 단추를 클릭 하 여 SQL Server 인스턴스에 로그온 합니다.

3. 트리 뷰에서 **데이터베이스** 를 마우스 오른쪽 단추로 클릭 하 고 **새 데이터베이스를** 선택 합니다. 를 호출 하 여 라는 `SQLPersistenceStore`새 데이터베이스를 만듭니다.

4. SQLPersistenceStore 데이터베이스의 C:\Windows\Microsoft.NET\Framework\v4.0\SQL\en 디렉터리에 있는 SqlWorkflowInstanceStoreSchema.sql 스크립트 파일을 실행하여 필요한 데이터베이스 스키마를 설정합니다.

5. SQLPersistenceStore 데이터베이스의 C:\Windows\Microsoft.NET\Framework\v4.0\SQL\en 디렉터리에 있는 SqlWorkflowInstanceStoreLogic.sql 스크립트 파일을 실행하여 필요한 데이터베이스 논리를 설정합니다.

### <a name="to-create-the-web-hosted-workflow-service"></a>웹 호스팅 워크플로 서비스를 만들려면

1. 빈 Visual Studio 2012 솔루션을 만들고 이름을 `OrderProcessing`로 표시 합니다.

2. `OrderService`라는 새 WCF 워크플로 서비스 애플리케이션 프로젝트를 솔루션에 추가합니다.

3. 프로젝트 속성 대화 상자에서 **웹** 탭을 선택 합니다.

    1. **시작 작업** 에서 **특정 페이지** 를 선택 하 `Service1.xamlx`고를 지정 합니다.

        ![워크플로 서비스 프로젝트 웹 속성](./media/creating-a-long-running-workflow-service/start-action-specific-page-option.png "웹 호스팅 워크플로 서비스별 페이지 옵션 만들기")

    2. **서버** 에서 **로컬 IIS 웹 서버 사용**을 선택 합니다.

        ![로컬 웹 서버 설정](./media/creating-a-long-running-workflow-service/use-local-web-server.png "웹 호스팅 워크플로 서비스 만들기-로컬 IIS 웹 서버 사용 옵션")

        > [!WARNING]
        > 이 설정을 지정 하려면 관리자 모드에서 Visual Studio 2012을 실행 해야 합니다.

        이러한 두 단계에서는 IIS에서 호스팅하도록 워크플로 서비스 프로젝트를 구성합니다.

4. 아직 `Service1.xamlx` 열려 있지 않으면를 열고 기존 **ReceiveRequest** 및 **sendresponse** 활동을 삭제 합니다.

5. **순차 서비스** 활동을 선택 하 고 **변수** 링크를 클릭 하 여 다음 그림에 표시 된 변수를 추가 합니다. 이렇게 하면 워크플로 서비스에서 나중에 사용할 일부 변수가 추가됩니다.

    > [!NOTE]
    > CorrelationHandle가 변수 형식 드롭다운에 없으면 드롭다운에서 **형식 찾아보기** 를 선택 합니다. **유형 이름** 상자에 CorrelationHandle를 입력 하 고 목록 상자에서 CorrelationHandle를 선택한 다음 **확인**을 클릭 합니다.

    ![변수 추가](./media/creating-a-long-running-workflow-service/add-variables-sequential-service-activity.gif "순차 서비스 활동에 변수를 추가 합니다.")

6. **ReceiveAndSendReply** 활동 템플릿을 **순차적 서비스** 활동으로 끌어 놓습니다. 이 활동 집합은 클라이언트에서 메시지를 받고 회신을 보냅니다.

    1. **Receive** 활동을 선택 하 고 다음 그림에 강조 표시 된 속성을 설정 합니다.

        ![Receive 활동 속성 설정](./media/creating-a-long-running-workflow-service/set-receive-activity-properties.png "Receive 활동 속성을 설정 합니다.")

        DisplayName 속성은 디자이너에서 표시되는 Receive 활동의 이름을 설정합니다. ServiceContractName 및 OperationName 속성은 Receive 활동으로 구현되는 서비스 계약 및 작업의 이름을 지정합니다. 워크플로 서비스에서 계약을 사용 하는 방법에 대 한 자세한 내용은 [워크플로에서 계약 사용](../../../../docs/framework/wcf/feature-details/using-contracts-in-workflow.md)을 참조 하세요.

    2. **ReceiveStartOrder** 활동의 **정의 ...** 링크를 클릭 하 고 다음 그림에 표시 된 속성을 설정 합니다.  **매개 변수** 라디오 단추가 선택 되어 `p_customerName` `customerName` 있고 라는 매개 변수가 변수에 바인딩되어 있는지 확인 합니다. 이렇게 하면 일부 데이터를 수신 하 고 해당 데이터를 로컬 변수에 바인딩하기 위한 **수신** 작업이 구성 됩니다.

        ![Receive 작업에서 수신 하는 데이터 설정](./media/creating-a-long-running-workflow-service/set-properties-for-receive-content.png "수신 작업에서 수신 하는 데이터에 대 한 속성을 설정 합니다.")

    3. **SendReplyToReceive** 활동을 선택 하 고 다음 그림에 표시 된 것 처럼 강조 표시 된 속성을 설정 합니다.

        ![SendReply 활동의 속성 설정](./media/creating-a-long-running-workflow-service/set-properties-for-reply-activities.png "SetReplyProperties")

    4. **SendReplyToStartOrder** 활동의 **정의 ...** 링크를 클릭 하 고 다음 그림에 표시 된 속성을 설정 합니다. **매개 변수** 라디오 단추가 선택 되어 있는지 확인 합니다. 이라는 `p_orderId` 매개 변수는 `orderId` 변수에 바인딩됩니다. 이 설정은 SendReplyToStartOrder 활동이 문자열 형식의 값을 호출자에게 반환하도록 지정합니다.

        ![SendReply 활동 콘텐츠 데이터 구성](./media/creating-a-long-running-workflow-service/setreplycontent-for-sendreplytostartorder-activity.png "SetReplyToStartOrder 활동에 대 한 설정을 구성 합니다.")

    5. **Receive** 작업과 **SendReply** 활동 간에 Assign 활동을 끌어서 놓고 다음 그림과 같이 속성을 설정 합니다.

        ![Assign 활동 추가](./media/creating-a-long-running-workflow-service/add-an-assign-activity.png "Assign 활동을 추가 합니다.")

        이렇게 하면 새 주문 ID가 만들어지고 orderId 변수에 값이 배치됩니다.

    6. **ReplyToStartOrder** 활동을 선택 합니다. 속성 창에서 **CorrelationInitializers**에 대 한 줄임표 단추를 클릭 합니다. **이니셜라이저 추가** 링크를 선택 하 고 `orderIdHandle` 이니셜라이저 텍스트 상자에를 입력 한 다음 상관 관계 형식에 대해 쿼리 상관 관계 이니셜라이저를 선택 하 고 XPATH 쿼리 드롭다운 상자에서 p_orderId을 선택 합니다. 이러한 설정이 다음 그림에 나와 있습니다. **확인**을 클릭합니다.  클라이언트와 이 워크플로 서비스 인스턴스 간에 상관 관계가 초기화됩니다. 이 주문 ID가 포함된 메시지가 수신되면 이 워크플로 서비스 인스턴스로 라우팅됩니다.

        ![상관 관계 이니셜라이저 추가](./media/creating-a-long-running-workflow-service/add-correlationinitializers.png "상관 관계 이니셜라이저를 추가 합니다.")

7. 다른 **ReceiveAndSendReply** 활동을 워크플로 끝 (첫 번째 **Receive** 및 **SendReply** 활동이 포함 된 **시퀀스** 의 외부)에 끌어다 놓습니다. 이 활동은 클라이언트에서 보낸 두 번째 메시지를 받고 응답합니다.

    1. 새로 추가 된 **Receive** 및 **SendReply** 활동이 포함 된 **시퀀스** 를 선택 하 고 **변수** 단추를 클릭 합니다. 다음 그림에 강조 표시된 변수를 추가합니다.

        ![새 변수 추가](./media/creating-a-long-running-workflow-service/add-the-itemid-variable.png "ItemId 변수를 추가 합니다.")

        또한 `orderResult` 범위`Sequence` 에 **문자열** 을 추가 합니다.

    2. **Receive** 활동을 선택 하 고 다음 그림에 표시 된 속성을 설정 합니다.

        ![Receive 활동 속성 설정](./media/creating-a-long-running-workflow-service/set-receive-activities-properties.png "수신 작업 속성을 설정 합니다.")

        > [!NOTE]
        > **ServiceContractName** 필드를로 `../IAddItem`변경 해야 합니다.

    3. **ReceiveAddItem** 활동의 **정의 ...** 링크를 클릭 하 고 다음 그림에 표시 된 매개 변수를 추가 합니다 .이 작업은 두 개의 매개 변수, 즉 주문 id와 주문 된 항목의 id를 수락 하도록 수신 작업을 구성 합니다.

        ![두 번째 수신에 대 한 매개 변수 지정](./media/creating-a-long-running-workflow-service/add-receive-two-parameters.png "두 개의 매개 변수를 받도록 receive 작업을 구성 합니다.")

    4. **CorrelateOn** 줄임표 단추를 클릭 하 고 `orderIdHandle`을 입력 합니다. **XPath 쿼리**아래에서 드롭다운 화살표를 클릭 하 고를 `p_orderId`선택 합니다. 이렇게 하면 두 번째 Receive 활동에 대한 상관 관계가 구성됩니다. 상관 관계에 대 한 자세한 내용은 참조 하세요 [상관 관계](../../../../docs/framework/wcf/feature-details/correlation.md)합니다.

        ![CorrelatesOn 속성 설정](./media/creating-a-long-running-workflow-service/correlateson-setting.png "CorrelatesOn 속성을 설정 합니다.")

    5. **ReceiveAddItem** 활동 바로 뒤에 **If** 활동을 끌어 놓습니다. 이 활동은 if 문처럼 작동합니다.

        1. **Condition** 속성을로 설정 합니다.`itemId=="Zune HD" (itemId="Zune HD" for Visual Basic)`

        2. 다음 그림에 표시 된 것 처럼 **assign** 활동을 **Then** 섹션에 끌어서 놓고 **Else** 섹션에 다른 **할당** 활동의 속성을 설정 합니다.

            ![서비스 호출 결과 할당](./media/creating-a-long-running-workflow-service/assign-result-of-service-call.png "서비스 호출의 결과를 할당 합니다.")

            조건이 `true` 이면 **then** 섹션이 실행 됩니다. 조건이 `false` **Else** 섹션이 실행 되 면이 고,

        3. **SendReplyToReceive** 활동을 선택 하 고 다음 그림에 표시 된 **DisplayName** 속성을 설정 합니다.

            ![SendReply 활동 속성 설정](./media/creating-a-long-running-workflow-service/send-reply-activity-property.png "SendReply 활동 속성을 설정 합니다.")

        4. **SetReplyToAddItem** 활동의 **정의 ...** 링크를 클릭 하 고 다음 그림과 같이 구성 합니다. 이렇게 하면 `orderResult` 변수의 값을 반환 하도록 **SendReplyToAddItem** 활동을 구성 합니다.

            ![SendReply 활동에 대 한 데이터 바인딩 설정](./media/creating-a-long-running-workflow-service/set-property-for-sendreplytoadditem.gif "SendReplyToAddItem 활동에 대 한 속성을 설정 합니다.")

8. Web.config 파일을 열고 \<동작 > 섹션에 다음 요소를 추가 하 여 워크플로 지 속성을 사용 하도록 설정 합니다.

    ```xml
    <sqlWorkflowInstanceStore connectionString="Data Source=your-machine\SQLExpress;Initial Catalog=SQLPersistenceStore;Integrated Security=True;Asynchronous Processing=True" instanceEncodingOption="None" instanceCompletionAction="DeleteAll" instanceLockedExceptionAction="BasicRetry" hostLockRenewalPeriod="00:00:30" runnableInstancesDetectionPeriod="00:00:02" />
              <workflowIdle timeToUnload="0"/>
    ```

    > [!WARNING]
    > 이전 코드 조각의 호스트 및 SQL Server 인스턴스 이름을 바꿔야 합니다.

9. 솔루션을 빌드합니다.

### <a name="to-create-a-client-application-to-call-the-workflow-service"></a>클라이언트 애플리케이션을 만들어 워크플로 서비스를 호출하려면

1. 솔루션에 `OrderClient`라는 새 콘솔 애플리케이션 프로젝트를 추가합니다.

2. 다음 어셈블리에 대한 참조를 `OrderClient` 프로젝트에 추가합니다.

    1. System.ServiceModel.dll

    2. System.ServiceModel.Activities.dll

3. 서비스 참조를 워크플로 서비스에 추가하고 `OrderService`를 네임스페이스로 지정합니다.

4. 클라이언트 프로젝트의 `Main()` 메서드에서 다음 코드를 추가합니다.

    ```csharp
    static void Main(string[] args)
    {
       // Send initial message to start the workflow service
       Console.WriteLine("Sending start message");
       StartOrderClient startProxy = new StartOrderClient();
       string orderId = startProxy.StartOrder("Kim Abercrombie");

       // The workflow service is now waiting for the second message to be sent
       Console.WriteLine("Workflow service is idle...");
       Console.WriteLine("Press [ENTER] to send an add item message to reactivate the workflow service...");
       Console.ReadLine();

       // Send the second message
       Console.WriteLine("Sending add item message");
       AddItemClient addProxy = new AddItemClient();
       AddItem item = new AddItem();
       item.p_itemId = "Zune HD";
       item.p_orderId = orderId;

       string orderResult = addProxy.AddItem(item);
       Console.WriteLine("Service returned: " + orderResult);
    }
    ```

5. 솔루션을 빌드하고 `OrderClient` 애플리케이션을 실행합니다. 클라이언트에서 다음 텍스트가 표시됩니다.

    ```output
    Sending start messageWorkflow service is idle...Press [ENTER] to send an add item message to reactivate the workflow service...
    ```

6. 워크플로 서비스가 지속 되었는지 확인 하려면 **시작** 메뉴로 이동 하 여 **모든 프로그램**, **Microsoft SQL Server 2008** **SQL Server Management Studio**를 선택 하 여 SQL Server Management Studio를 시작 합니다.

    1. 왼쪽 창에서 **데이터베이스**, **SQLPersistenceStore**, **뷰** 를 확장 하 고 **DurableInstancing** 를 마우스 오른쪽 단추로 클릭 한 다음 **상위 1000 행 선택**을 선택 합니다. **결과** 창에서 하나 이상의 인스턴스가 나열 되는지 확인 합니다. 실행하는 동안 예외가 발생한 경우 이전 실행의 다른 인스턴스가 있을 수 있습니다. **DurableInstancing** 를 마우스 오른쪽 단추로 클릭 하 고 **상위 200 행 편집**을 선택한 다음 **실행** 단추를 누르고 결과 창에서 모든 행을 선택한 다음 **삭제**를 선택 하 여 기존 행을 삭제할 수 있습니다.  데이터베이스에 표시되는 인스턴스가 애플리케이션에서 만든 인스턴스인지 확인하려면 클라이언트를 실행하기 전에 인스턴스 뷰가 비어 있는지 확인합니다. 클라이언트가 실행되고 있으면 쿼리(상위 1000개의 행 선택)를 다시 실행하고 새 인스턴스가 추가되었는지 확인합니다.

7. Enter 키를 눌러 워크플로 서비스에 품목 추가 메시지를 보냅니다. 클라이언트에서 다음 텍스트가 표시됩니다.

    ```output
    Sending add item messageService returned: Item added to orderPress any key to continue . . .
    ```

## <a name="see-also"></a>참고자료

- [워크플로 서비스](../../../../docs/framework/wcf/feature-details/workflow-services.md)
