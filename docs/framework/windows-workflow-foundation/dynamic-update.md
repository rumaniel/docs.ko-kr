---
title: 동적 업데이트
ms.date: 03/30/2017
ms.assetid: 8b6ef19b-9691-4b4b-824c-3c651a9db96e
ms.openlocfilehash: 2553e6a29f498a9b53752d6c191df21a391dee34
ms.sourcegitcommit: 4735bb7741555bcb870d7b42964d3774f4897a6e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/30/2019
ms.locfileid: "66378285"
---
# <a name="dynamic-update"></a>동적 업데이트

동적 업데이트는 워크플로 애플리케이션 개발자가 지속형 워크플로 인스턴스의 워크플로 정의를 업데이트하기 위한 메커니즘을 제공합니다. 이를 통해 버그 수정 또는 새 요구 사항을 구현하거나 예기치 않은 변경 내용을 수용할 수 있습니다. 이 항목에서는.NET Framework 4.5에서 도입 된 동적 업데이트 기능의 개요를 제공 합니다.

## <a name="dynamic-update"></a>동적 업데이트

지속형 워크플로 인스턴스에 동적 업데이트를 적용하려면 지속형 워크플로 인스턴스를 수정하여 필요한 변경 내용을 반영하는 방법을 설명하는 런타임 지침이 포함된 <xref:System.Activities.DynamicUpdate.DynamicUpdateMap>을 만듭니다. 업데이트 맵을 만든 후에는 원하는 지속형 워크플로 인스턴스에 이 업데이트 맵을 적용합니다. 동적 업데이트를 적용한 후에는 새로 업데이트한 워크플로 정의를 사용하여 워크플로 인스턴스를 다시 시작할 수 있습니다. 업데이트 맵을 만들어 적용하는 데 필요한 네 가지 단계는 다음과 같습니다.

1. [동적 업데이트에 대 한 워크플로 정의 준비 합니다.](dynamic-update.md#Prepare)

2. [원하는 변경 내용을 반영 하도록 워크플로 정의 업데이트 합니다.](dynamic-update.md#Update)

3. [업데이트 맵을 만듭니다.](dynamic-update.md#Create)

4. [원하는 지속형된 워크플로 인스턴스에 업데이트 맵을 적용합니다](dynamic-update.md#Apply)

> [!NOTE]
> 업데이트 맵을 만드는 1~3단계와 업데이트를 적용하는 단계는 서로 독립적으로 수행할 수 있습니다. 일반적인 시나리오는 워크플로 개발자 업데이트 맵을 오프 라인으로 만들어지고 다음 관리자는 나중에 업데이트를 적용 합니다.

이 항목에서는 컴파일된 XAML 워크플로의 지속형 인스턴스에 새 활동을 추가하는 동적 업데이트 프로세스에 대해 간략하게 설명합니다.

### <a name="Prepare"></a> 동적 업데이트에 대 한 워크플로 정의 준비 합니다.

동적 업데이트 프로세스의 첫 번째 단계는 원하는 워크플로 정의를 업데이트할 수 있도록 준비하는 것입니다. 이를 위해서는 <xref:System.Activities.DynamicUpdate.DynamicUpdateServices.PrepareForUpdate%2A?displayProperty=nameWithType> 메서드를 호출하고 수정할 워크플로 정의를 전달합니다. 이 메서드는 유효성을 검사한 다음 나중에 수정된 워크플로 정의와 비교할 수 있도록 워크플로 트리에서 태그가 지정되어야 하는 공용 활동 및 변수와 같은 모든 개체를 식별합니다. 이 작업이 완료되면 워크플로 트리가 복제되어 원래 워크플로 정의에 연결됩니다. 업데이트 맵을 만들 때는 워크플로 정의의 업데이트 버전과 원래 워크플로 정의를 비교하여 그 차이에 따라 업데이트 맵이 생성됩니다.

XAML 워크플로를 동적으로 업데이트할 수 있도록 준비하려면 해당 워크플로를 <xref:System.Activities.ActivityBuilder>에 로드한 후 <xref:System.Activities.ActivityBuilder>에 <xref:System.Activities.DynamicUpdate.DynamicUpdateServices.PrepareForUpdate%2A?displayProperty=nameWithType>를 전달합니다.

> [!NOTE]
> Serialize 된 워크플로 작업에 대 한 자세한 내용은 및 <xref:System.Activities.ActivityBuilder>를 참조 하세요 [직렬화 워크플로 및 활동을 XAML에서](serializing-workflows-and-activities-to-and-from-xaml.md)합니다.

다음 예제에서는 여러 자식 활동과 `MortgageWorkflow`로 구성된 <xref:System.Activities.Statements.Sequence> 정의를 <xref:System.Activities.ActivityBuilder>에 로드한 후 동적 업데이트를 준비합니다. 메서드가 반환한 후 <xref:System.Activities.ActivityBuilder>는 원래 워크플로 정의와 복사본이 포함되어 있습니다.

```csharp
// Load the MortgageWorkflow definition from Xaml into
// an ActivityBuilder.
XamlXmlReaderSettings readerSettings = new XamlXmlReaderSettings()
{
    LocalAssembly = Assembly.GetExecutingAssembly()
};

XamlXmlReader xamlReader = new XamlXmlReader(@"C:\WorkflowDefinitions\MortgageWorkflow.xaml",
    readerSettings);

ActivityBuilder ab = XamlServices.Load(
    ActivityXamlServices.CreateBuilderReader(xamlReader)) as ActivityBuilder;

// Prepare the workflow definition for dynamic update.
DynamicUpdateServices.PrepareForUpdate(ab);
```

> [!NOTE]
> 이 항목과 관련 된 샘플 코드를 다운로드 하려면 [동적 업데이트 샘플 코드](https://go.microsoft.com/fwlink/?LinkId=227905)합니다.

### <a name="Update"></a> 원하는 변경 내용을 반영 하도록 워크플로 정의 업데이트 합니다.

워크플로 정의를 업데이트할 준비가 되면 원하는 변경 작업을 수행할 수 있습니다. 활동 추가 또는 제거, 공용 변수 추가, 이동 또는 삭제, 인수 추가 또는 제거, 활동 대리자의 시그니처 변경 같은 작업을 수행할 수 있습니다. 실행 중인 활동을 제거하거나 실행 중인 대리자의 시그니처를 변경할 수는 없습니다. 이러한 변경 작업은 코드를 사용하거나 재호스트된 워크플로 디자이너를 사용하여 수행할 수 있습니다. 다음 예제에서는 이전 예제에서 사용한 `VerifyAppraisal`의 본문을 구성하는 Sequence에 사용자 지정 `MortgageWorkflow` 활동을 추가합니다.

```csharp
// Make desired changes to the definition. In this example, we are
// inserting a new VerifyAppraisal activity as the 3rd child of the root Sequence.
VerifyAppraisal va = new VerifyAppraisal
{
    Result = new VisualBasicReference<bool>("LoanCriteria")
};

// Get the Sequence that makes up the body of the workflow.
Sequence s = ab.Implementation as Sequence;

// Insert the new activity into the Sequence.
s.Activities.Insert(2, va);
```

### <a name="Create"></a> 업데이트 맵을 만듭니다.

업데이트할 준비가 된 워크플로 정의를 수정한 후에는 업데이트 맵을 만들 수 있습니다. 동적 업데이트 맵을 만들려면 <xref:System.Activities.DynamicUpdate.DynamicUpdateServices.CreateUpdateMap%2A?displayProperty=nameWithType> 메서드를 호출합니다. 이 메서드는 런타임에 새 워크플로 정의를 사용하여 지속형 워크플로 인스턴스를 로드하고 다시 시작할 수 있도록 런타임에 해당 인스턴스를 수정하는 데 필요한 정보가 포함된 <xref:System.Activities.DynamicUpdate.DynamicUpdateMap>을 반환합니다. 다음 예제에서는 이전 예제에서 수정된 `MortgageWorkflow` 정의에 대해 동적 맵을 만듭니다.

```csharp
// Create the update map.
DynamicUpdateMap map = DynamicUpdateServices.CreateUpdateMap(ab);
```

이 업데이트 맵은 지속형 워크플로 인스턴스를 수정하는 데 즉시 사용할 수 있으며, 보다 일반적인 방법으로는 이를 저장했다가 나중에 업데이트를 적용할 수 있습니다. 업데이트 맵을 저장하는 한 가지 방법은 다음 예제와 같이 파일에 serialize하는 것입니다.

```csharp
// Serialize the update map to a file.
DataContractSerializer serializer = new DataContractSerializer(typeof(DynamicUpdateMap));
using (FileStream fs = System.IO.File.Open(@"C:\WorkflowDefinitions\MortgageWorkflow.map", FileMode.Create))
{
    serializer.WriteObject(fs, map);
}
```

<xref:System.Activities.DynamicUpdate.DynamicUpdateServices.CreateUpdateMap%2A?displayProperty=nameWithType>이 결과를 반환하면 복제된 워크플로 정의와 <xref:System.Activities.DynamicUpdate.DynamicUpdateServices.PrepareForUpdate%2A?displayProperty=nameWithType>에 대한 호출에 추가된 기타 동적 업데이트 정보는 제거되고, 수정된 워크플로 정의는 나중에 업데이트된 워크플로 인스턴스를 다시 시작할 때 사용할 수 있도록 저장될 수 있습니다. 다음 예제에서는 수정된 워크플로 정의를 `MortgageWorkflow_v1.1.xaml`에 저장합니다.

```csharp
// Save the modified workflow definition.
StreamWriter sw = File.CreateText(@"C:\WorkflowDefinitions\MortgageWorkflow_v1.1.xaml");
XamlWriter xw = ActivityXamlServices.CreateBuilderWriter(new XamlXmlWriter(sw, new XamlSchemaContext()));
XamlServices.Save(xw, ab);
sw.Close();
```

### <a name="Apply"></a> 원하는 지속형된 워크플로 인스턴스에 업데이트 맵을 적용합니다

업데이트 맵을 만든 후 언제든지 업데이트 맵을 적용할 수 있습니다. 이 작업은 <xref:System.Activities.DynamicUpdate.DynamicUpdateMap>에서 반환된 <xref:System.Activities.DynamicUpdate.DynamicUpdateServices.CreateUpdateMap%2A?displayProperty=nameWithType> 인스턴스를 사용하여 바로 수행하거나, 저장된 업데이트 맵 복사본을 사용하여 나중에 수행할 수 있습니다. 워크플로 인스턴스를 업데이트하려면 <xref:System.Activities.WorkflowApplicationInstance>를 사용하여 해당 인스턴스를 <xref:System.Activities.WorkflowApplication.GetInstance%2A?displayProperty=nameWithType>에 로드합니다. 다음으로 업데이트된 워크플로 정의 및 원하는 <xref:System.Activities.WorkflowApplication>를 사용하여 <xref:System.Activities.WorkflowIdentity>을 만듭니다. 이 <xref:System.Activities.WorkflowIdentity>는 원래 워크플로를 유지하는 데 사용된 것과 다를 수 있으며, 일반적으로 지속형 인스턴스가 수정되었음을 반영하기 위해 사용됩니다. <xref:System.Activities.WorkflowApplication>을 만든 후에는 <xref:System.Activities.WorkflowApplication.Load%2A?displayProperty=nameWithType>을 사용하는 <xref:System.Activities.DynamicUpdate.DynamicUpdateMap>의 오버로드를 사용하여 이를 로드한 다음 <xref:System.Activities.WorkflowApplication.Unload%2A?displayProperty=nameWithType>를 호출하여 언로드합니다. 그러면 동적 업데이트가 적용되고 업데이트된 워크플로 인스턴스가 유지됩니다.

```csharp
// Load the serialized update map.
DynamicUpdateMap map;
using (FileStream fs = File.Open(@"C:\WorkflowDefinitions\MortgageWorkflow.map", FileMode.Open))
{
    DataContractSerializer serializer = new DataContractSerializer(typeof(DynamicUpdateMap));
    object updateMap = serializer.ReadObject(fs);
    if (updateMap == null)
    {
        throw new ApplicationException("DynamicUpdateMap is null.");
    }

    map = (DynamicUpdateMap)updateMap;
}

// Retrieve a list of workflow instance ids that corresponds to the
// workflow instances to update. This step is the responsibility of
// the application developer.
List<Guid> ids = GetPersistedWorkflowIds();
foreach (Guid id in ids)
{
    // Get a proxy to the persisted workflow instance.
    SqlWorkflowInstanceStore store = new SqlWorkflowInstanceStore(connectionString);
    WorkflowApplicationInstance instance = WorkflowApplication.GetInstance(id, store);

    // If desired, you can inspect the WorkflowIdentity of the instance
    // using the DefinitionIdentity property to determine whether to apply
    // the update.
    Console.WriteLine(instance.DefinitionIdentity);

    // Create a workflow application. You must specify the updated workflow definition, and
    // you may provide an updated WorkflowIdentity if desired to reflect the update.
    WorkflowIdentity identity = new WorkflowIdentity
    {
        Name = "MortgageWorkflow v1.1",
        Version = new Version(1, 1, 0, 0)
    };

    // Load the persisted workflow instance using the updated workflow definition
    // and with an updated WorkflowIdentity. In this example the MortgageWorkflow class
    // contains the updated definition.
    WorkflowApplication wfApp = new WorkflowApplication(new MortgageWorkflow(), identity);

    // Apply the dynamic update on the loaded instance.
    wfApp.Load(instance, map);

    // Unload the updated instance.
    wfApp.Unload();
}
```

### <a name="resuming-an-updated-workflow-instance"></a>업데이트된 워크플로 인스턴스 다시 시작

동적 업데이트를 적용한 후에는 워크플로 인스턴스를 다시 시작할 수 있습니다. 이때 새로 업데이트된 정의와 <xref:System.Activities.WorkflowIdentity>를 사용해야 합니다.

> [!NOTE]
> 작업에 대 한 자세한 내용은 <xref:System.Activities.WorkflowApplication> 하 고 <xref:System.Activities.WorkflowIdentity>를 참조 하세요 [를 사용 하 여 WorkflowIdentity 및 버전 관리](using-workflowidentity-and-versioning.md).

다음 예제에서는 이전 예제에서 컴파일된 `MortgageWorkflow_v1.1.xaml` 워크플로를 업데이트된 워크플로 정의를 사용하여 로드하고 다시 시작합니다.

```csharp
// Load the persisted workflow instance using the updated workflow definition
// and updated WorkflowIdentity.
WorkflowIdentity identity = new WorkflowIdentity
{
    Name = "MortgageWorkflow v1.1",
    Version = new Version(1, 1, 0, 0)
};

WorkflowApplication wfApp = new WorkflowApplication(new MortgageWorkflow(), identity);

// Configure persistence and desired workflow event handlers.
// (Omitted for brevity.)
ConfigureWorkflowApplication(wfApp);

// Load the persisted workflow instance.
wfApp.Load(InstanceId);

// Resume the workflow.
// wfApp.ResumeBookmark(...);
```

> [!NOTE]
> 이 항목과 관련 된 샘플 코드를 다운로드 하려면 [동적 업데이트 샘플 코드](https://go.microsoft.com/fwlink/?LinkId=227905)합니다.
