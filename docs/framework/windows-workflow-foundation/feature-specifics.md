---
title: Windows Workflow Foundation 기능 특성
ms.date: 03/30/2017
ms.assetid: e84d12da-a055-45f6-b4d1-878d127b46b6
ms.openlocfilehash: 063d2472443431423cea9b164831cd1e7a669408
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64753725"
---
# <a name="windows-workflow-foundation-feature-specifics"></a>Windows Workflow Foundation 기능 특성

[!INCLUDE[netfx40_long](../../../includes/netfx40-long-md.md)]에서는 Windows Workflow Foundation에 많은 기능을 추가합니다. 이 문서에서는 여러 새로운 기능을 설명하고 이러한 기능이 유용할 수 있는 시나리오에 대한 세부 정보를 제공합니다.

## <a name="messaging-activities"></a>메시징 활동

메시징 활동 (<xref:System.ServiceModel.Activities.Receive>, <xref:System.ServiceModel.Activities.SendReply>를 <xref:System.ServiceModel.Activities.Send>, <xref:System.ServiceModel.Activities.ReceiveReply>) 워크플로에서 WCF 메시지를 송수신 하는 데 사용 됩니다. <xref:System.ServiceModel.Activities.Receive> 및 <xref:System.ServiceModel.Activities.SendReply> 활동 표준 WCF 웹 서비스와 마찬가지로 WSDL을 통해 노출 되는 Windows Communication Foundation (WCF) 서비스 작업을 만드는 데 사용 됩니다. <xref:System.ServiceModel.Activities.Send> 및 <xref:System.ServiceModel.Activities.ReceiveReply> 유사한 WCF 웹 서비스를 사용 하는 데 사용 됩니다 <xref:System.ServiceModel.ChannelFactory>입니다 **서비스 참조 추가** Workflow foundation의 미리 구성 된 작업을 생성 하는 환경도 있습니다.

### <a name="getting-started-with-messaging-activities"></a>메시징 작업 시작

- Visual Studio 2012에서 WCF 워크플로 서비스 응용 프로그램 프로젝트를 만듭니다. <xref:System.ServiceModel.Activities.Receive> 및 <xref:System.ServiceModel.Activities.SendReply> 쌍이 캔버스에 배치됩니다.

- 프로젝트를 마우스 오른쪽 단추로 클릭 **서비스 참조 추가**합니다. 기존 웹 서비스 WSDL 가리키고 클릭 **확인**합니다. 생성된 된 활동을 표시 하려면 프로젝트를 빌드합니다 (사용 하 여 구현 <xref:System.ServiceModel.Activities.Send> 및 <xref:System.ServiceModel.Activities.ReceiveReply>) 도구 상자에 있습니다.

- [워크플로 서비스 설명서](../wcf/feature-details/workflow-services.md)

### <a name="messaging-activities-example-scenario"></a>메시징 작업 예제 시나리오

`BestPriceFinder` 특정 경로 대 한 최상의 티켓 가격을 찾기 위해 여러 항공사 서비스 서비스를 호출 합니다. 이 시나리오를 구현 해야 메시지 작업을 사용 하 여 가격 요청을 받고, 백 엔드 서비스에서 가격을 검색, 최상의 가격으로 가격 요청에 회신 하를 수 있습니다. 또한 해야 하므로 최상의 가격을 계산 하는 것에 대 한 비즈니스 논리를 만드는 다른 기본 제공 활동을 사용 하 합니다.

## <a name="workflowservicehost"></a>WorkflowServiceHost

<xref:System.ServiceModel.WorkflowServiceHost> 여러 인스턴스, 구성 및 WCF 메시징 (워크플로가 호스팅되기 위해 메시징을 사용할 필요 하지 않음) 하지만 지 원하는 기본 제공 워크플로 호스트 됩니다. 서비스 동작의 집합을 통해 지속성, 추적 및 인스턴스 제어와 통합됩니다. WCF의와 마찬가지로 <xref:System.ServiceModel.ServiceHost>, <xref:System.ServiceModel.WorkflowServiceHost> 콘솔/WinForms/WPF 응용 프로그램 또는 Windows 서비스에서 자체 호스트 되거나 (.xamlx 파일로) 웹 호스트 될 수 IIS 또는 WAS에서.

### <a name="getting-started-with-workflow-service-host"></a>워크플로 서비스 호스트 시작

- Visual Studio 2010에서 WCF 워크플로 서비스 응용 프로그램 프로젝트를 만듭니다:이 프로젝트 사용 하도록 설정 됩니다 <xref:System.ServiceModel.WorkflowServiceHost> 웹 호스트 환경에서.

- 메시징이 아닌 워크플로를 호스트하려면 메시지를 기반으로 하는 인스턴스를 만들 사용자 지정 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint>를 추가합니다.

- <xref:System.ServiceModel.Activities.WorkflowControlEndpoint>에 <xref:System.ServiceModel.WorkflowServiceHost>를 추가한 다음 <xref:System.ServiceModel.Activities.WorkflowControlClient>를 사용하여 워크플로 인스턴스를 제어(예: 일시 중단 또는 종료)할 수 있습니다.

- <xref:System.ServiceModel.WorkflowServiceHost>에 대한 샘플은 다음 단원에서 확인할 수 있습니다.

  - [실행](./samples/execution.md)

  - 응용 프로그램: [일시 중단된 인스턴스 관리](./samples/suspended-instance-management.md)

- [워크플로 서비스 호스팅 개요](../wcf/feature-details/hosting-workflow-services-overview.md)

### <a name="workflowservicehost-scenario"></a>WorkflowServiceHost 시나리오

BestPriceFinder 서비스는 특정 경로 대 한 최상의 티켓 가격을 찾기 위해 여러 항공사 서비스를 호출 합니다. 이 시나리오를 구현 해야 하므로의 워크플로 호스트 <xref:System.ServiceModel.WorkflowServiceHost>합니다. 메시지 작업 가격 요청을 수신 하 고, 백 엔드 서비스에서 가격을 검색, 최상의 가격으로 가격 요청에 회신에 사용할 것입니다.

## <a name="correlation"></a>상관 관계

상관 관계는 다음 두 가지 중 하나입니다.

- 메시지를 그룹화하는 방법(즉, 요청 메시지와 회신 간의 관계)

- 데이터를 서비스 인스턴스에 매핑하는 방법

### <a name="getting-started"></a>시작

- 상관 관계를 시작하려면 Visual Studio에서 새 프로젝트를 만듭니다. <xref:System.ServiceModel.Activities.CorrelationHandle> 형식의 변수를 만듭니다.

- 메시지를 그룹화하는 데 사용되는 상관 관계의 예로 메시지를 그룹화하는 요청-회신 상관 관계가 있습니다.

  - 에 <xref:System.ServiceModel.Activities.Receive> 활동을 클릭 합니다 <xref:System.ServiceModel.Activities.Receive.CorrelationInitializers%2A> 속성 추가 <xref:System.ServiceModel.Activities.RequestReplyCorrelationInitializer> 위의 첫 번째 단계에서 만든 CorrelationHandle을 사용 하 여.

  - 만들기를 <xref:System.ServiceModel.Activities.SendReply> 마우스 오른쪽 단추로 클릭 하 여 활동은 <xref:System.ServiceModel.Activities.Receive> "SendReply 만들기"를 클릭 합니다. 워크플로에서 <xref:System.ServiceModel.Activities.Receive> 작업 뒤에 이 작업을 붙여 넣습니다.

- 데이터를 서비스 인스턴스에 매핑하는 예로 데이터(예: 주문 ID)를 특정 워크플로 인스턴스에 매핑하는 콘텐츠 기반 상관 관계가 있습니다.

  - 아무 메시징 작업에서나 `CorrelationInitializers` 속성을 클릭하고 위에서 만든 <xref:System.ServiceModel.Activities.QueryCorrelationInitializer> 변수를 사용하여 <xref:System.ServiceModel.Activities.CorrelationHandle>를 추가합니다. 드롭다운 메뉴에서 원하는 메시지 속성(예: OrderID)을 두 번 클릭합니다. `CorrelatesWith` 속성을 위에서 사용한 <xref:System.ServiceModel.Activities.CorrelationHandle> 변수로 설정합니다.

- [상관 관계 개념 설명서](../wcf/feature-details/correlation.md)

### <a name="correlation-scenario"></a>상관 관계 시나리오

새 주문 만들기 및 진행 중인 기존 주문을 업데이트를 처리 하는 주문 처리 워크플로 사용 됩니다. 이 시나리오를 구현 해야 하므로의 워크플로 호스트 <xref:System.ServiceModel.WorkflowServiceHost> 메시징 활동을 사용 합니다. 또한 상관 관계에 따라 필요는 `orderId` 에 올바른 워크플로가 업데이트 되도록 합니다.

## <a name="simplified-configuration"></a>단순화된 구성

WCF 구성 스키마 복잡 하며 기능 찾기 어려운 여러 사용자를 제공 합니다. [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)], WCF 사용자에 게 다음 기능을 통해 해당 서비스를 구성할 수 있도록 지원에 집중 했습니다.

- 서비스별 명시적 구성의 필요성을 제거합니다. 구성 하지 않은 경우 \<서비스 > 끝점 집합에 자동으로 추가할 서비스 기본 주소 및 계약 당 하나의 서비스에 다음 서비스 및 서비스에 대 한 요소는 모든 끝점에 프로그래밍 방식으로 정의 하지 않습니다 서비스에 의해 구현 됩니다.

- 사용자가 명시적 구성 없이 서비스에 적용될 WCF 바인딩 및 동작의 기본값을 정의할 수 있도록 합니다.

- 표준 엔드포인트는 하나 이상의 엔드포인트 속성(주소, 바인딩 및 계약)에 대한 고정 값이 있는 미리 구성된 다시 사용 가능 엔드포인트를 정의하며 사용자 지정 속성 정의를 허용합니다.

- 마지막으로 <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601> 구성이 있는 선택 되거나 응용 프로그램 도메인 로드 시간 후에 변경 하는 시나리오에서 유용 WCF 클라이언트 구성의 중앙 관리를 수행할 수 있습니다.

### <a name="getting-started"></a>시작

- [Wcf 4.0 개발자 가이드](https://go.microsoft.com/fwlink/?LinkId=204940)

- [구성 채널 팩터리](https://go.microsoft.com/fwlink/?LinkId=204941)

- [표준 끝점 요소](https://go.microsoft.com/fwlink/?LinkId=204942)

- [.NET Framework 4의 서비스 구성 개선 사항](https://go.microsoft.com/fwlink/?LinkId=204943)

- [.NET 4의에서 일반적인 사용자 실수: WF/WCF 서비스 구성 이름을 잘못 입력](https://go.microsoft.com/fwlink/?LinkId=204944)

### <a name="simplified-configuration-scenarios"></a>단순화된 구성 시나리오

- 숙련된 된 ASMX 개발자는 WCF를 사용 하 여 시작 하려고 합니다. 그러나 WCF는 너무 복잡 한 것 같습니다. 구성 파일을 작성하는 데 필요한 모든 정보는 무엇입니까? .NET 4에서는 구성 파일을 전혀 사용하지 않을 수도 있습니다.

- 기존의 WCF 서비스 집합은 구성 및 유지 관리가 매우 어려웠습니다. 구성 파일에는 수천 줄의 XML 코드가 있으며 수정하는 것이 매우 위험합니다. 관리하기 쉽도록 코드 양을 줄이기 위한 도움이 필요합니다.

## <a name="data-contract-resolver"></a>데이터 계약 확인자

.NET 3.5의 알려진 형식 디자인에는 몇 가지 제한이 있었습니다.

- serialization 및 deserialization 중에 알려진 형식을 동적으로 추가할 수 없었습니다.

- 직렬 변환기에서 알 수 없는 xsi:type 정보를 처리할 수 없었습니다.

- 사용자가 회선의 serialization 인스턴스 크기를 더 작게 만들기 위해 회선에 표시할 xsi:type을 지정할 수 없었습니다.

합니다 [DataContractResolver](../wcf/samples/datacontractresolver.md) .NET 4.5에서 이러한 문제를 해결 합니다.

### <a name="getting-started"></a>시작

- [데이터 계약 확인자 API 설명서](https://go.microsoft.com/fwlink/?LinkId=204946)

- [데이터 계약 확인자 소개](https://go.microsoft.com/fwlink/?LinkId=204947)

- 샘플:

  - [DataContractResolver](../wcf/samples/datacontractresolver.md)

  - [KnownAssemblyAttribute](../wcf/samples/knownassemblyattribute.md)

### <a name="data-contract-resolver-scenarios"></a>데이터 계약 확인자 시나리오

- 서비스에서 수십 개의 <xref:System.Runtime.Serialization.KnownTypeAttribute> 개체를 선언할 필요가 없도록 합니다.

- XML blob의 크기를 줄입니다.

## <a name="flowchart"></a>Flowchart

순서도는 도메인 문제를 시각적으로 나타내는 잘 알려진 패러다임입니다. .NET 4에서 도입된 새 제어 흐름 스타일입니다. 순서도의 핵심 특성은 주어진 시간에 항상 작업 한 개만 실행된다는 것입니다. 순서도는 루프 및 대체 결과를 표현할 수 있지만 여러 노드의 동시 실행은 기본적으로 표현할 수 없습니다.

### <a name="getting-started"></a>시작

- Visual Studio 2012 워크플로 콘솔 응용 프로그램을 만듭니다. 워크플로 디자이너에서 순서도를 추가합니다.

- 순서도 기능은 다음 클래스를 사용합니다.

  - <xref:System.Activities.Statements.Flowchart>

  - <xref:System.Activities.Statements.FlowNode>

  - <xref:System.Activities.Statements.FlowDecision>

  - <xref:System.Activities.Statements.FlowStep>

  - <xref:System.Activities.Statements.FlowSwitch%601>

- 샘플:

  - [Flowchart 작업에서 TryCatch를 사용하여 오류 처리](./samples/fault-handling-in-a-flowchart-activity-using-trycatch.md)

  - [채용 프로세스](./samples/hiring-process.md)

- 디자이너 설명서:

  - [순서도 활동 디자이너](/visualstudio/workflow-designer/flowchart-activity-designers)

### <a name="flowchart-scenarios"></a>순서도 시나리오

순서도 작업을 사용하여 추측 게임을 구현할 수 있습니다. 추측 게임은 매우 단순합니다. 컴퓨터가 임의 숫자를 선택하고 플레이어가 해당 숫자를 추측해야 합니다. 플레이어가 각 추측을 제출 하는 경우 컴퓨터 (예: "시도 낮은 숫자를") 힌트를 표시 합니다. 플레이어가 7회 미만의 시도에서 숫자를 찾으면 컴퓨터에서 특별한 축하 화면이 표시됩니다. 다음 절차 작업의 조합을 통해 이 게임을 구현할 수 있습니다.

- <xref:System.Activities.Statements.Sequence>

- <xref:System.Activities.Statements.While>

- <xref:System.Activities.Statements.Switch%601>

- <xref:System.Activities.Statements.TryCatch>

- <xref:System.Activities.Statements.Assign%601>

- <xref:System.Activities.Statements.If>

## <a name="procedural-activities-sequence-if-foreach-switch-assign-dowhile-while"></a>절차 작업(Sequence, If, ForEach, Switch, Assign, DoWhile, While)

절차 작업은 프로그래머에게 익숙한 개념을 사용하여 순차 제어 흐름을 모델링하는 메커니즘을 제공합니다. 이러한 작업은 일반적으로 구조적 프로그래밍 언어 구문을 활성화하며, 해당하는 경우 C#/VB와 같은 일반적인 절차 언어를 언어 패리티에 제공합니다.

### <a name="getting-started"></a>시작

- Visual Studio 2012 워크플로 콘솔 응용 프로그램을 만듭니다. Workflow Designer에서 절차 작업을 추가합니다.

- 샘플:

  - [채용 프로세스](./samples/hiring-process.md)

  - [기업 구매 프로세스](./samples/corporate-purchase-process.md)

- 디자이너 설명서:

  - [Parallel 활동 디자이너](/visualstudio/workflow-designer/parallel-activity-designer)

  - [ParallelForEach\<T > 활동 디자이너](/visualstudio/workflow-designer/parallelforeach-t-activity-designer)

### <a name="procedural-activity-scenarios"></a>절차 작업 시나리오

- <xref:System.Activities.Statements.Parallel>: 인트라넷 문서 관리 시스템에 문서 승인 워크플로가 있습니다. 여러 부서의 사용자가 문서를 승인해야 인트라넷에 게시할 수 있습니다. 승인; 설정 된 순서는 없습니다. 문서가 "승인 보류 중" 단계에 있는 동안 언제 든 지 발생할 수 있습니다. 사용자가 검토를 위해 문서를 전송하면 직속 관리자, 인트라넷 관리자 및 내부 통신 관리자가 문서를 승인해야 합니다.

- <xref:System.Activities.Statements.ParallelForEach%601>: WF 응용 프로그램이 대기업 내의 회사를 관리합니다. 회사 규칙은 모든 구매 작업을 계획하기 전에 3개 공급업체를 평가하도록 규정합니다. 구매 부서의 직원이 회사 공급업체 목록에서 3개 공급업체를 선택합니다. 공급업체를 선택하고 알린 후 회사는 합리적 제안서를 기다립니다. 제안서는 임의 순서로 도착할 수 있습니다. WF에서 이 시나리오를 구현하기 위해 공급업체 컬렉션을 반복하고 합리적 제안서를 요청하는 <xref:System.Activities.Statements.ParallelForEach%601>를 사용합니다. 모든 제안이 수집된 후 최상의 제안이 선택되고 표시됩니다.

## <a name="invokemethod"></a>InvokeMethod

<xref:System.Activities.Statements.InvokeMethod> 작업을 사용하면 범위 내의 개체나 형식에서 공용 메서드를 호출할 수 있습니다. 이 작업은 매개 변수(매개 변수 배열 포함)를 사용하거나 사용하지 않는 인스턴스 및 정적 메서드 호출과 제네릭 메서드 호출을 지원합니다. 동기 및 비동기로 메서드를 실행할 수도 있습니다.

### <a name="getting-started"></a>시작

- Visual Studio 2012 워크플로 콘솔 응용 프로그램을 만듭니다. 워크플로 디자이너에서 <xref:System.Activities.Statements.InvokeMethod> 작업을 추가하고 정적 및 인스턴스 메서드를 구성합니다.

- 디자이너 설명서: [InvokeMethod 활동 디자이너](/visualstudio/workflow-designer/invokemethod-activity-designer)

### <a name="invokemethod-scenarios"></a>InvokeMethod 시나리오

- 범위 내의 개체에서 메서드를 호출해야 합니다. 예를 들어, 사전에 값을 추가해야 합니다. 사전 인스턴스의 Add 메서드가 호출되고 키와 값이 제공됩니다.

- 레거시 CLR 개체에서 메서드를 호출해야 합니다. 레거시 클래스 호출을 래핑할 사용자 지정 작업을 만드는 대신 워크플로 실행 중에 범위 내에 있는 경우 <xref:System.Activities.Statements.InvokeMethod>를 사용할 수 있습니다.

## <a name="error-handling-activities"></a>오류 처리 작업

<xref:System.Activities.Statements.TryCatch> 작업은 일련의 포함된 작업을 실행하는 동안 발생하는 예외를 catch하기 위한 메커니즘을 제공합니다(C#/VB의 Try/Catch 구문과 유사함). <xref:System.Activities.Statements.TryCatch>는 워크플로 수준에서 예외 처리를 제공합니다. 처리되지 않은 예외가 throw되면 워크플로가 중단되고 Finally 블록이 실행되지 않습니다. 이 동작은 C#과 일치합니다.

### <a name="getting-started"></a>시작

- Visual Studio 2012 워크플로 콘솔 응용 프로그램을 만듭니다. Workflow Designer에서 <xref:System.Activities.Statements.TryCatch> 작업을 추가합니다.

- 예제: [Flowchart 작업에서 TryCatch를 사용하여 오류 처리](./samples/fault-handling-in-a-flowchart-activity-using-trycatch.md)

- 디자이너 설명서: [오류 처리 활동 디자이너](/visualstudio/workflow-designer/error-handling-activity-designers)

### <a name="error-handling-scenarios"></a>오류 처리 시나리오

일련의 작업을 실행해야 하며, 오류가 발생할 경우 특정 논리를 실행해야 합니다. 오류 처리 논리 중에 오류를 복구할 수 없다는 것이 발견되면 예외가 다시 throw되고 부모 작업(또는 호스트)이 문제를 처리합니다.

## <a name="pick-activity"></a>Pick 작업

<xref:System.Activities.Statements.Pick> 작업은 WF에서 이벤트 기반 제어 흐름 모델링을 제공합니다. <xref:System.Activities.Statements.Pick>에는 각 분기가 실행되기 전에 특정 이벤트의 발생을 기다리는 많은 분기가 포함되어 있습니다. 이 설치에서 <xref:System.Activities.Statements.Pick>은 작업이 수신 대기 중인 이벤트 집합 중 하나만 실행하는 <xref:System.Activities.Statements.Switch%601>와 유사하게 동작합니다. 각 분기는 이벤트 구동 방식이며 처음 발생하는 이벤트는 해당 분기를 실행합니다. 다른 분기는 모두 이벤트 수신 대기를 취소하고 중지합니다.

### <a name="getting-started"></a>시작

- Visual Studio 2012 워크플로 콘솔 응용 프로그램을 만듭니다. Workflow Designer에서 <xref:System.Activities.Statements.Pick> 작업을 추가합니다.

- 예제: [Pick 작업 사용](./samples/using-the-pick-activity.md)

- 디자이너 설명서: [Pick 활동 디자이너](/visualstudio/workflow-designer/pick-activity-designer)

### <a name="pick-scenario"></a>Pick 시나리오

사용자에게 입력을 요청하는 메시지를 표시해야 합니다. 정상적인 상황에서는 개발자가 <xref:System.Console.ReadLine%2A>과 같은 메서드 호출을 사용하여 사용자 입력을 요청합니다. 이 설치와 관련된 문제는 사용자가 입력할 때까지 프로그램이 기다린다는 것입니다. 이 시나리오에서는 차단 작업의 차단을 해제하기 위해 시간 제한이 필요합니다. 일반적인 시나리오에서는 지정된 기간 내에 작업을 완료해야 합니다. 차단 작업 시간 초과는 Pick에서 많은 값을 추가하는 시나리오입니다.

## <a name="wcf-routing-service"></a>WCF 라우팅 서비스

라우팅 서비스는 일반 소프트웨어 클라이언트와 서비스 사이 WCF 메시지 흐름 방식을 제어할 수 있는 라우터 되도록 설계 되었습니다. 라우팅 서비스 수 있습니다 서비스에서 클라이언트를 분리 구성 측면에서 훨씬 더 자유롭게 제공 하는 유연 해야 서비스를 호스트 하는 방법을 고려 하는 경우를 지원할 수 있습니다. .NET 3.5에서는 클라이언트 및 서비스 된 밀접 하 게; 클라이언트가 서비스와 통신 하는 데 필요한 것 이며 있던 위치 모두에 대해 알아야 했습니다. 또한.NET Framework 3.5의 WCF에는 다음과 같은 제한 사항이 있었습니다.

- 이 논리를 클라이언트 프로그램에 하드 코딩해야 했으므로 오류 처리가 복잡했습니다.

- 클라이언트와 서비스에서 항상 동일한 바인딩을 사용해야 했습니다.

- 서비스가 제대로 팩터링되지 않았습니다. 클라이언트가 여러 서비스 중에서 선택하는 대신 모든 기능을 구현하는 서비스 하나에 통신하도록 하는 것이 더 쉽습니다.

.NET 4의 라우팅 서비스는 이러한 문제를 보다 쉽게 해결 하도록 설계 되었습니다. 새 라우팅 서비스에는 다음과 같은 기능이 있습니다.

1. 콘텐츠 기반 라우팅(<xref:System.ServiceModel.Dispatcher.MessageFilter> 개체가 메시지를 검사하여 보낼 위치를 결정함)

2. 프로토콜 브리징 (전송 및 메시지)

3. 오류 처리(라우터가 통신 예외를 catch하고 백업 엔드포인트로 장애 조치됨)

4. <xref:System.ServiceModel.Dispatcher.MessageFilterTable%601> 및 라우팅 구성의 동적(메모리 내) 업데이트

### <a name="getting-started"></a>시작

1. 설명서: [라우팅](../wcf/feature-details/routing.md)

2. 샘플: [라우팅 서비스 &#91;WCF 샘플&#93;](../wcf/samples/routing-services.md)

3. 블로그: [라우팅 규칙!](https://go.microsoft.com/fwlink/?LinkId=204956)

### <a name="routing-scenarios"></a>라우팅 시나리오

라우팅 서비스는 다음과 같은 시나리오에서 유용합니다.

- 클라이언트가 직접 주소를 모두 지정하지 않고 여러 서비스에 통신할 수 있습니다.

- 클라이언트가 클라이언트 요청에서 추가 논리를 수행하여 라우팅 위치를 결정할 수 있습니다.

- 클라이언트를 리팩터링하지 않고 클라이언트가 수행하는 작업을 여러 서비스 구현으로 분해합니다.

- 클라이언트와 서비스가 서로 다른 보안 설정으로 서로 다른 바인딩을 통신할 수 있습니다.

- 클라이언트가 서비스를 사용할 수 없는 경우나 오류에 대해 보다 강력하도록 설정할 수 있습니다.

## <a name="wcf-discovery"></a>WCF 검색

WCF Discovery는 검색 메커니즘을 응용 프로그램 인프라에 통합할 수 있는 프레임 워크 기술입니다. 이 기술을 사용하여 서비스를 검색 가능하게 만들고 서비스를 검색하도록 클라이언트를 구성할 수 있습니다. 엔드포인트를 사용하여 클라이언트를 더 이상 하드 코딩할 필요가 없으므로 애플리케이션의 견고성과 내결함성이 강화됩니다. Discovery는 자동 구성 기능을 애플리케이션에 빌드하는 완벽한 플랫폼입니다.

이 제품은 WS-Discovery 표준을 기반으로 하며 상호 운용 및 확장 가능한 제네릭으로 디자인되었습니다. 이 제품에서는 다음 두 가지 작업 모드가 지원됩니다.

1. 관리: 네트워크에 기존 서비스에 대해 알고 있는 엔터티가 있는 경우 클라이언트가 직접 정보를 쿼리합니다. 이것은 Active Directory와 유사합니다.

2. 임시: 클라이언트가 멀티캐스트 메시지를 사용하여 서비스를 찾습니다.

또한 검색 메시지는 네트워크 프로토콜에 관계없이 작동하므로 모드 요구 사항을 지원하는 모든 프로토콜에서 사용할 수 있습니다. 예를 들어 검색 UDP 채널이 나 멀티 캐스트 메시징을 지 원하는 다른 네트워크를 통해 멀티 캐스트 메시지를 보낼 수 있습니다. 이러한 디자인 요소는 검색 솔루션에 맞게 조정할 수 있도록 기능 유연성과 결합 합니다.

### <a name="getting-started"></a>시작

- 설명서: [WCF 검색](../wcf/feature-details/wcf-discovery.md)

- 샘플: [검색 (샘플)](../wcf/samples/discovery-samples.md)

### <a name="discovery-scenarios"></a>Discovery 시나리오

서비스를 사용할 수 있게 될 시기를 알 수 없기 때문에 개발자가 엔드포인트를 하드 코딩하는 대신 런타임에 서비스를 선택하려고 합니다. 애플리케이션 구성 요소 간에 분리, 견고성 및 자동 구성이 더 필요합니다.

## <a name="tracking"></a>추적

워크플로 추적 워크플로 인스턴스 실행에 대 한 정보를 제공 합니다. 추적 이벤트를 워크플로 인스턴스 수준 및 워크플로 내의 작업이 실행 될 때 워크플로에서 내보냅니다. 추적 레코드를 구독하려면 워크플로 추적 참가자를 워크플로 호스트에 추가해야 합니다. 추적 레코드는 추적 프로필을 사용하여 필터링됩니다. .NET Framework는 ETW (이벤트 추적에 대 한 Windows) 추적 참가자가 제공 및 기본 프로필을 machine.config 파일에 설치 됩니다.

### <a name="getting-started"></a>시작

1. Visual Studio 2010에서 WCF 워크플로 서비스 애플리케이션 프로젝트를 만듭니다. 먼저 <xref:System.ServiceModel.Activities.Receive> 및 <xref:System.ServiceModel.Activities.SendReply> 쌍이 캔버스에 배치됩니다.

2. web.config를 열고 프로필 없이 ETW 추적 동작을 추가합니다.

    1. 기본 프로필이 사용됩니다.

    2. 이벤트 뷰어를 열고 다음 노드에서 분석 채널을 사용 하도록 설정 합니다. **이벤트 뷰어**, **Applications and Services Logs**, **Microsoft**하십시오 **Windows**, **응용 프로그램 서버-응용 프로그램**. 마우스 오른쪽 단추로 클릭 **분석** 선택한 **로그 사용**합니다.

    3. 워크플로 서비스를 실행합니다.

    4. 이벤트 뷰어에서 워크플로 추적 이벤트를 확인합니다.

3. 샘플: [추적](./samples/tracking.md)

4. 개념 설명서: [워크플로 추적](workflow-tracking-and-tracing.md)

## <a name="sql-workflow-instance-store"></a>SQL 워크플로 인스턴스 저장소

<xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>는 인스턴스 저장소의 SQL Server 기반 구현입니다. 인스턴스 저장소는 해당 인스턴스를 로드하고 다시 시작하는 데 필요한 모든 데이터와 함께 실행 중인 인스턴스의 상태를 저장합니다. 서비스 호스트는 워크플로가 유지되는 경우 인스턴스 상태를 저장하도록 인스턴스 저장소에 지시하고, 해당 인스턴스에 대한 메시지가 도착하거나 지연 작업이 만료되면 인스턴스 상태를 로드하도록 인스턴스 저장소에 지시합니다.

### <a name="getting-started"></a>시작

1. Visual Studio 2012에서 암시적 또는 명시적를 포함 하는 워크플로 만드는 <xref:System.Activities.Statements.Persist> 활동입니다. 워크플로 서비스 호스트에 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> 동작을 추가합니다. 이 작업은 코드나 애플리케이션 구성 파일에서 수행할 수 있습니다.

2. 샘플: [지속성](./samples/persistence.md)

3. 개념 설명서: [SQL 워크플로 인스턴스 저장소](sql-workflow-instance-store.md)합니다.
