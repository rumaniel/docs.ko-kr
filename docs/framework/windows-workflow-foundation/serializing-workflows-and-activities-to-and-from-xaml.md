---
title: 워크플로 및 활동과 XAML 간 serialize
ms.date: 03/30/2017
ms.assetid: 37685b32-24e3-4d72-88d8-45d5fcc49ec2
ms.openlocfilehash: c18afa7232adabc4f1c4e17fde993064b9189e39
ms.sourcegitcommit: 3eeea78f52ca771087a6736c23f74600cc662658
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/31/2019
ms.locfileid: "68671901"
---
# <a name="serialize-workflows-and-activities-to-and-from-xaml"></a>워크플로 및 활동을 XAML로 Serialize

어셈블리에 포함되어 있는 형식으로 컴파일하는 것 외에 워크플로 정의를 XAML로 serialize할 수도 있습니다. serialize된 이 정의를 다시 로드하여 편집 또는 검사하거나, 빌드 시스템에 전달하여 컴파일하거나, 로드 및 호출할 수 있습니다. 이 항목에서는 워크플로 정의의 serialize와 XAML 워크플로 정의의 사용에 대해 간략하게 설명합니다.

## <a name="work-with-xaml-workflow-definitions"></a>XAML 워크플로 정의 작업

<xref:System.Activities.ActivityBuilder> 클래스를 사용하여 serialization에 대한 워크플로 정의를 만듭니다. <xref:System.Activities.ActivityBuilder>를 만드는 방법은 <xref:System.Activities.DynamicActivity>를 만드는 방법과 매우 비슷합니다. 필요한 모든 인수를 지정하고 동작을 구성하는 활동을 구성합니다. 다음 예제에서는 두 개의 인수를 가져와서 두 인수를 함께 추가하고 결과를 반환하는 `Add` 활동을 만듭니다. 이 활동은 결과를 반환하므로 제네릭 <xref:System.Activities.ActivityBuilder%601> 클래스가 사용됩니다.

[!code-csharp[CFX_WorkflowApplicationExample#41](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#41)]

각각의 <xref:System.Activities.DynamicActivityProperty> 인스턴스는 워크플로에 대한 입력 인수 중 하나를 나타내며 <xref:System.Activities.ActivityBuilder.Implementation%2A>에는 워크플로의 논리를 구성하는 활동이 포함되어 있습니다. 이 예제의 r-value 식은 Visual Basic 식입니다. 람다 식은 <xref:System.Activities.Expressions.ExpressionServices.Convert%2A>를 사용하지 않으면 XAML로 serialize할 수 없습니다. Serialize 된 워크플로를 workflow designer에서 열거나 편집 하려면 Visual Basic 식을 사용 해야 합니다. 자세한 내용은 [명령적 코드를 사용 하 여 워크플로, 활동 및 식 작성](authoring-workflows-activities-and-expressions-using-imperative-code.md)을 참조 하세요.

<xref:System.Activities.ActivityBuilder> 인스턴스가 나타내는 워크플로 정의를 XAML로 serialize하려면 <xref:System.Activities.XamlIntegration.ActivityXamlServices>를 사용하여 <xref:System.Xaml.XamlWriter>를 만든 다음, <xref:System.Xaml.XamlServices>를 사용하여 <xref:System.Xaml.XamlWriter>를 통해 워크플로 정의를 serialize합니다. <xref:System.Activities.XamlIntegration.ActivityXamlServices>에는 인스턴스를 <xref:System.Activities.ActivityBuilder> xaml로 매핑하고 xaml에서 xaml 워크플로를 로드 하 고 호출할 수 <xref:System.Activities.DynamicActivity> 있는를 반환 하는 메서드가 있습니다. 다음 예 <xref:System.Activities.ActivityBuilder> 에서는 이전 예제의 인스턴스가 문자열로 직렬화 되 고 파일에 저장 됩니다.

```csharp
// Serialize the workflow to XAML and store it in a string.
StringBuilder sb = new StringBuilder();
StringWriter tw = new StringWriter(sb);
XamlWriter xw = ActivityXamlServices.CreateBuilderWriter(new XamlXmlWriter(tw, new XamlSchemaContext()));
XamlServices.Save(xw, ab);
string serializedAB = sb.ToString();

// Display the XAML to the console.
Console.WriteLine(serializedAB);

// Serialize the workflow to XAML and save it to a file.
StreamWriter sw = File.CreateText(@"C:\Workflows\add.xaml");
XamlWriter xw2 = ActivityXamlServices.CreateBuilderWriter(new XamlXmlWriter(sw, new XamlSchemaContext()));
XamlServices.Save(xw2, ab);
sw.Close();
```

다음 예제에서는 serialize된 워크플로를 나타냅니다.

```xaml
<Activity
  x:TypeArguments="x:Int32"
  x:Class="Add"
  xmlns="http://schemas.microsoft.com/netfx/2009/xaml/activities"
  xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">
  <x:Members>
    <x:Property Name="Operand1" Type="InArgument(x:Int32)" />
    <x:Property Name="Operand2" Type="InArgument(x:Int32)" />
  </x:Members>
  <Sequence>
    <WriteLine Text="[Operand1.ToString() + " + " + Operand2.ToString()]" />
    <Assign x:TypeArguments="x:Int32" Value="[Operand1 + Operand2]">
      <Assign.To>
        <OutArgument x:TypeArguments="x:Int32">
          <ArgumentReference x:TypeArguments="x:Int32" ArgumentName="Result" />
          </OutArgument>
      </Assign.To>
    </Assign>
  </Sequence>
</Activity>
```

Serialize 된 워크플로를 로드 하려면 <xref:System.Activities.XamlIntegration.ActivityXamlServices> <xref:System.Activities.XamlIntegration.ActivityXamlServices.Load%2A> 메서드를 사용 합니다. 이 메서드는 serialize된 워크플로 정의를 사용하고 워크플로 정의를 나타내는 <xref:System.Activities.DynamicActivity>를 반환합니다. 유효성 검사 프로세스가 진행되는 동안 <xref:System.Activities.Activity.CacheMetadata%2A>의 본문에서 <xref:System.Activities.DynamicActivity>를 호출할 때까지는 XAML이 deserialize되지 않습니다. 유효성 검사를 명시적으로 호출 하지 않으면 워크플로가 호출 될 때 수행 됩니다. XAML 워크플로 정의가 잘못된 경우 <xref:System.ArgumentException> 예외가 throw됩니다. <xref:System.Activities.Activity.CacheMetadata%2A>에서 throw된 예외는 모두 <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A>에 대한 호출에서 이스케이프되며 호출자가 처리해야 합니다. 다음 예제에서는 이전 예제에서 serialize된 워크플로를 로드하고 <xref:System.Activities.WorkflowInvoker>를 사용하여 호출합니다.

[!code-csharp[CFX_WorkflowApplicationExample#43](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#43)]

이 워크플로가 호출되면 다음 출력이 콘솔에 표시됩니다.

**25 + 15**\
**40**

> [!NOTE]
> 입력 및 출력 인수를 사용 하 여 워크플로를 호출 하는 방법에 대 한 자세한 내용은 <xref:System.Activities.WorkflowInvoker.Invoke%2A> [Workflowinvoker 및 WorkflowApplication 및 사용](using-workflowinvoker-and-workflowapplication.md) 을 참조 하세요.

Serialize 된 워크플로에 식이 C# <xref:System.Activities.XamlIntegration.ActivityXamlServicesSettings> 포함 된 경우 <xref:System.Activities.XamlIntegration.ActivityXamlServicesSettings.CompileExpressions%2A> 속성이로 `true` 설정 된 인스턴스는에 대 <xref:System.Activities.XamlIntegration.ActivityXamlServices.Load%2A?displayProperty=nameWithType>한 매개 변수로 전달 되어야 <xref:System.NotSupportedException> 합니다. 그렇지 않으면와 유사한 메시지와 함께이 throw 됩니다. 다음과 같이 합니다. **식 작업 형식 ' CSharpValue ' 1 '을 실행 하려면 컴파일이 필요 합니다.  워크플로가 컴파일 되었는지 확인 하세요.**

```csharp
ActivityXamlServicesSettings settings = new ActivityXamlServicesSettings
{
    CompileExpressions = true
};

DynamicActivity<int> wf = ActivityXamlServices.Load(new StringReader(serializedAB), settings) as DynamicActivity<int>;
```

자세한 내용은 [ C# 식](csharp-expressions.md)을 참조 하세요.

메서드를 <xref:System.Activities.ActivityBuilder> <xref:System.Activities.XamlIntegration.ActivityXamlServices> 사용 하여serialize된워크플로정의를인스턴스로로드할수도있습니다.<xref:System.Activities.XamlIntegration.ActivityXamlServices.CreateBuilderReader%2A> Serialize 된 워크플로를 <xref:System.Activities.ActivityBuilder> 인스턴스에 로드 한 후에는이를 검사 하 고 수정할 수 있습니다. 이 방법은 사용자 지정 워크플로 디자이너 작성자에게 유용하며, 디자인 프로세스가 진행되는 동안 워크플로 정의를 저장하고 다시 로드하기 위한 메커니즘을 제공합니다. 다음 예제에서는 이전 예제에서 serialize된 워크플로 정의를 로드하고 해당 속성을 검사합니다.

[!code-csharp[CFX_WorkflowApplicationExample#44](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#44)]
