---
title: 메시지 흐름 개요
ms.date: 03/30/2017
ms.assetid: fb0899e1-84cc-4d90-b45b-dc5a50063943
ms.openlocfilehash: 0bfbd1523f1d5db4a94cf3af03a03779af14655d
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795971"
---
# <a name="message-flow-overview"></a>메시지 흐름 개요
상호 연결된 서비스가 포함된 분산 시스템에서는 서비스 간의 인과 관계를 확인해야 합니다. 상태 모니터링, 문제 해결 및 근본 원인 분석과 같은 중요한 시나리오를 지원하기 위해 요청 흐름의 일부인 다양한 구성 요소를 이해하는 것이 중요합니다. 다양한 서비스 간 추적을 상호 연결할 수 있도록 하기 위해 .NET Framework 4에서는 다음 기능을 통한 지원이 추가되었습니다.

- 분석 추적: ETW(Windows용 이벤트 추적) (ETW)를 사용 하는 고성능 및 낮은 자세한 정보 추적 기능입니다.

- WCF/WF 서비스용 종단 간 활동 모델: 이 기능은 <xref:System.ServiceModel> 및 <xref:System.Workflow.ComponentModel> 네임 스페이스에 의해 생성 된 추적의 상관 관계를 지원 합니다.

- WF 용 ETW 추적: 이 기능은 WF 서비스에서 생성 된 추적 레코드를 사용 하 여 워크플로의 현재 상태와 진행률에 대 한 가시성을 제공 합니다.

 추적이나 추적 레코드에 기록되는 오류를 사용하여 코드 결함이나 잘못된 형식의 메시지를 찾을 수 있습니다. 이벤트의 메시지 헤더에 있는 Correlation 노드의 ActivityId 속성을 사용하여 오류가 발생하는 활동을 확인할 수 있습니다. 활동 ID로 메시지 흐름 추적을 사용 하도록 설정 하려면 [메시지 흐름 추적 구성](./etw/configuring-message-flow-tracing.md)을 참조 하세요. 이 항목에서는 초보자를 위한 자습서에서 만든 프로젝트에서 메시지 흐름 추적을 사용하도록 설정하는 방법을 보여 줍니다.

### <a name="to-enable-message-flow-tracing-in-the-getting-started-tutorial"></a>초보자를 위한 자습서에서 메시지 흐름 추적을 사용하도록 설정하려면

1. **시작**, **실행**을 차례로 클릭 하 고를 입력 `eventvwr.exe`하 여 이벤트 뷰어를 엽니다.

2. 분석 추적을 사용 하도록 설정 하지 않은 경우 **응용 프로그램 및 서비스 로그**, **Microsoft**, **Windows**, **응용 프로그램 서버-** 응용 프로그램을 확장 합니다. **보기**, **분석 및 디버그 로그 표시**를 선택 합니다. **분석** 을 마우스 오른쪽 단추로 클릭 하 고 **로그 사용**을 선택 합니다. 추적 내용을 볼 수 있도록 이벤트 뷰어를 열어 둡니다.

3. Visual Studio 2012의 [시작 자습서](../getting-started-tutorial.md) 에서 만든 샘플을 엽니다. 서비스를 만들 수 있도록 관리자 권한으로 Visual Studio 2012을 실행 해야 합니다. WCF 샘플을 설치한 경우 자습서에서 만든 완료 된 프로젝트를 포함 하는 [시작](../samples/getting-started-sample.md)을 열 수 있습니다.

4. **서비스** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가**, **새 항목**을 차례로 선택 합니다. **응용 프로그램 구성 파일** 을 선택 하 고 **확인**을 클릭 합니다.

5. 이전 단계에서 만든 App.Config 파일에 다음 코드를 추가합니다.

    ```xml
    <system.serviceModel>
      <diagnostics>
        <endToEndTracing propagateActivity="true" messageFlowTracing="true"/>
      </diagnostics>
    </system.serviceModel>
    ```

6. Ctrl+F5를 눌러 서버 애플리케이션을 디버깅하지 않고 실행합니다. **클라이언트** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **디버그**, **새 인스턴스 시작**을 차례로 선택 하 여 클라이언트 프로젝트를 실행 합니다.

7. 클라이언트에서 서버로의 이벤트를 추적하려면 Client 프로젝트의 애플리케이션 구성 파일에 다음 코드를 추가합니다.

    ```xml
    <diagnostics>
      <endToEndTracing propagateActivity="true" messageFlowTracing="true"/>
    </diagnostics>
    ```

8. 클라이언트의 Program.cs에서 다음 Using 문을 추가합니다.

    ```csharp
    using System.Diagnostics;
    ```

9. 클라이언트 프로젝트의 program.cs 파일에 있는 Main 메서드에서 Trace GUID를 이벤트 로그에서 전파되도록 설정합니다.

    ```csharp
    Guid guid = Guid.NewGuid();
    Trace.CorrelationManager.ActivityId = guid;
    ```

10. **분석** 로그를 새로 고치고 검사 합니다.  이벤트 ID가 220인 이벤트를 찾습니다.  이벤트를 선택 하 고 미리 보기 창에서 **세부 정보** 탭을 클릭 합니다. 이 이벤트에는 호출 활동의 상관 관계 ID가 포함됩니다.

    ```xml
    <Correlation ActivityID="{A066CCF1-8AB3-459B-B62F-F79F957A5036}" />
    ```

    > [!NOTE]
    > ActivityID에서 동일한 GUID를 가진 모든 이벤트는 한 요청과 관련되어 있습니다. 이를 이용하여 특정 클라이언트에서 특정 서비스로의 메시지를 상호 연결할 수 있습니다. 클라이언트에서 또 다른 서비스를 호출한 경우 동일한 클라이언트가 ActivityID로 식별될 수 있습니다.

11. 경우에 따라 ActivityID가 원래 GUID에서 새 ActivityID로 변경될 수 있습니다. 이 경우 전송 이벤트가 내보내집니다. 이 이벤트 ID는 499이며 헤더에 다음 데이터를 포함합니다.

    ```xml
    <Event xmlns="http://schemas.microsoft.com/win/2004/08/events/event">
        <System>
            <Provider Name="Microsoft-Windows-Application Server-Applications" Guid="{c651f5f6-1c0d-492e-8ae1-b4efd7c9d503}" />
            <EventID>499</EventID>
            ...
            <Correlation ActivityID="{A066CCF1-8AB3-459B-B62F-F79F957A5036}" RelatedActivityID="{85FC0930-9C49-42DA-804B-A7368104BD1B}" />
            ...
       </System>
    </Event>
    ```

    > [!NOTE]
    > 전송 이벤트는 ActivityID로 지정된 GUID에서 RelatedActivityID로 지정된 GUID로 활성 ActivityID가 변경된 것을 기록합니다. 전송 이벤트가 내보내진 후 모든 이벤트에는 새 GUID가 ActivityID로 포함됩니다.
