---
title: '방법: 워크플로 및 워크플로 서비스에 지속성 사용'
ms.date: 03/30/2017
ms.assetid: 2b1c8bf3-9866-45a4-b06d-ee562393e503
ms.openlocfilehash: 9357098318342d15ad7eead32cbc7218af095f6e
ms.sourcegitcommit: 9b1ac36b6c80176fd4e20eb5bfcbd9d56c3264cf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425344"
---
# <a name="how-to-enable-persistence-for-workflows-and-workflow-services"></a>방법: 워크플로 및 워크플로 서비스에 지속성 사용

이 항목에서는 워크플로 및 워크플로 서비스에 대해 지속성을 사용하도록 설정하는 방법에 대해 설명합니다.

## <a name="enable-persistence-for-workflows"></a>워크플로에 대해 지속성 사용

인스턴스 저장소를 연결할 수 있습니다는 **WorkflowApplication** 를 사용 하 여는 <xref:System.Activities.WorkflowApplication.InstanceStore%2A> 의 속성을 <xref:System.Activities.WorkflowApplication> 클래스. <xref:System.Activities.WorkflowApplication.Persist%2A> 메서드는 애플리케이션에 연결된 인스턴스 스토리지에 워크플로를 저장하거나 유지합니다. <xref:System.Activities.WorkflowApplication.Unload%2A> 메서드는 인스턴스 저장소에 워크플로를 유지한 다음 메모리에서 인스턴스를 언로드합니다. 합니다 **부하** 메서드는 워크플로 인스턴스 지 속성 저장소에 저장 된 워크플로 데이터를 사용 하 여 메모리에 로드 합니다.

합니다 **Persist** 메서드는 다음 단계를 수행 합니다.

1. 워크플로 스케줄러를 일시 중지하고 워크플로가 유휴 상태로 전환될 때까지 기다립니다.

2. 워크플로를 지속성 저장소에 유지하거나 저장합니다.

3. 워크플로 스케줄러를 다시 시작합니다.

 합니다 **언로드** 메서드는 다음 단계를 수행 합니다.

1. 워크플로 스케줄러를 일시 중지하고 워크플로가 유휴 상태로 전환될 때까지 기다립니다.

2. 워크플로를 지속성 저장소에 유지하거나 저장합니다.

3. 워크플로 인스턴스를 메모리에서 삭제합니다.

모두를 **Persist** 하 고 **언로드** 메서드는 워크플로가 비지 속성 영역이 종료 될 때까지 비지 속성 영역의 워크플로 차단 됩니다. 비지속성 영역이 완료되면 메서드에서 지속 또는 언로드 작업을 계속합니다. 제한 시간이 경과할 때까지 비지속성 영역이 완료되지 않거나 지속성 프로세스가 너무 오래 걸릴 경우 TimeoutException이 throw됩니다.

## <a name="enable-persistence-for-workflow-services-in-code"></a>코드에서 워크플로 서비스에 대해 지속성 사용

**DurableInstancingOptions** 의 멤버는 <xref:System.ServiceModel.WorkflowServiceHost> 클래스 라는 속성이 **InstanceStore** 사용 하 여 인스턴스 저장소에 연결할 사용할 수 있는 **WorkflowServiceHost** .

```csharp
// wsh is an instance of WorkflowServiceHost class
wsh.DurableInstancingOptions.InstanceStore = new SqlWorkflowInstanceStore();
```

경우는 **WorkflowServiceHost** 은 열, 지 속성은 자동으로 활성화 하는 경우를 **DurableInstancingOptions.InstanceStore** null이 아닙니다.

일반적으로 서비스 동작을 사용 하 여 워크플로 서비스 호스트에 사용할 구체적인 인스턴스 저장소를 제공 합니다 **InstanceStore** 속성입니다. 예를 들어 SqlWorkflowInstanceStoreBehavior의 인스턴스를 만듭니다는 **SqlWorkflowInstanceStore**를 구성 하 고 할당 합니다 **DurableInstancingOptions.InstanceStore**합니다.

## <a name="enable-persistence-for-workflow-services-using-an-application-configuration-file"></a>애플리케이션 구성 파일을 사용하여 워크플로 서비스에 지속성 허용

다음 코드를 app.config 또는 web.config 파일에 추가하여 애플리케이션 구성 파일을 통해 지속성을 사용하도록 설정할 수 있습니다.

```xml
<configuration>
  <system.serviceModel>
    <behaviors>
      <serviceBehaviors>
        <behavior name="myBehavior">
          <SqlWorkflowInstanceStore connectionString="Data Source=myDatabaseServer;Initial Catalog=myPersistenceDatabase">
        </behavior>
      </serviceBehaviors>
    <behaviors>
  </system.serviceModel>
</configuration>
```
