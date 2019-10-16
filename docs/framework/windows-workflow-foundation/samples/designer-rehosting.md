---
title: 디자이너 재호스팅
ms.date: 03/30/2017
ms.assetid: b676ad31-5f64-4d84-9a36-b4d7113a2f4d
ms.openlocfilehash: ecbea5822825cca5f3f5cf40e20d5d249b17b07c
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70038185"
---
# <a name="designer-rehosting"></a>디자이너 재호스팅
디자이너 재호스팅은 사용자 지정 응용 프로그램 내에 워크플로 디자인 캔버스를 호스트하는 방식을 가리키는 일반적인 시나리오입니다. 대부분의 사람들이 가장 잘 알고 있는 호스팅 응용 프로그램은 Visual Studio이지만, 응용 프로그램에 Workflow Designer를 표시하는 것이 유용할 수 있는 시나리오는 그 밖에도 여러 가지가 있습니다.  
  
- 최종 사용자가 현재 활성 상태 등 프로세스에 대한 런타임 데이터와 프로세스를 시각화하고 실행 시간 데이터 또는 워크플로 인스턴스에 대한 기타 정보를 집계하는 데 사용할 수 있는 모니터링 응용 프로그램  
  
- 한정된 활동 집합으로 프로세스를 사용자 지정하는 데 사용할 수 있는 응용 프로그램  
  
 이러한 유형의 응용 프로그램을 지원하기 위해 .NET Framework 내에 Workflow Designer가 함께 제공되며, 이 Workflow Designer를 WPF 응용 프로그램 내에 호스트하거나 적절한 WPF 호스팅 코드를 사용하여 WinForms 응용 프로그램에 호스트할 수 있습니다. 이 샘플에서는 다음 작업을 수행하는 방법을 보여 줍니다.  
  
- WF 디자이너 재호스팅  
  
- 재호스트된 도구 상자 및 속성 표 사용  
  
## <a name="rehosting-the-designer"></a>디자이너 재호스팅  
 이 샘플에서는 다음과 같은 표 레이아웃에 표시되는 디자이너를 포함할 WPF 레이아웃을 만드는 방법을 보여 줍니다. (공간의 제약 때문에 도구 상자 코드는 생략했습니다.) 여기에서는 디자이너와 속성 표가 포함되는 테두리의 이름에 주목할 필요가 있습니다.  
  
```xaml  
<Grid>  
    <Grid.ColumnDefinitions>  
        <ColumnDefinition Width="2*"/>  
        <ColumnDefinition Width="7*"/>  
        <ColumnDefinition Width="3*"/>  
    </Grid.ColumnDefinitions>  
    <Border Grid.Column="0">  
        <sapt:ToolboxControl>...</sapt:ToolboxControl>  
    </Border>  
    <Border Grid.Column="1" Name="DesignerBorder"/>  
    <Border Grid.Column="2" Name="PropertyBorder"/>  
</Grid>  
```  
  
 다음으로 이 샘플에서는 디자이너를 만들고 해당 기본 <xref:System.Activities.Presentation.WorkflowDesigner.View%2A> 및 <xref:System.Activities.Presentation.WorkflowDesigner.PropertyInspectorView%2A>를 사용자 인터페이스의 적절한 컨테이너와 연결합니다. 아래에 추가로 나와 있는 몇몇 코드 줄에 대해서는 약간의 설명이 필요합니다. .NET Framework와 함께 제공 되는 작업에 대 한 기본 활동 디자이너를 연결 하려면 호출이필요합니다.<xref:System.Activities.Core.Presentation.DesignerMetadata.Register%2A> <xref:System.Activities.Presentation.WorkflowDesigner.Load%2A>는 편집할 WF 항목을 전달하기 위해 호출됩니다. 마지막으로, <xref:System.Activities.Presentation.WorkflowDesigner.View%2A>(기본 캔버스) 및 <xref:System.Activities.Presentation.WorkflowDesigner.PropertyInspectorView%2A>(속성 표)가 사용자 인터페이스 화면에 배치됩니다.  
  
```csharp  
protected override void OnInitialized(EventArgs e)  
{  
   base.OnInitialized(e);  
   // register metadata  
   (new DesignerMetadata()).Register();  
  
   // create the workflow designer  
   WorkflowDesigner wd = new WorkflowDesigner();  
   wd.Load(new Sequence());  
   DesignerBorder.Child = wd.View;  
   PropertyBorder.Child = wd.PropertyInspectorView;  
}  
```  
  
## <a name="using-the-rehosted-toolbox"></a>재호스트된 도구 상자 사용  
 이 샘플에서는 재호스트된 도구 상자 컨트롤을 XAML에 선언적으로 사용합니다. 코드에서 <xref:System.Activities.Presentation.Toolbox.ToolboxItemWrapper> 생성자에 형식을 전달할 수 있습니다.  
  
```xaml  
<!-- Copyright (c) Microsoft Corporation. All rights reserved-->  
<Window x:Class="Microsoft.Samples.DesignerRehosting.RehostingWfDesigner"  
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
        xmlns:sapt="clr-namespace:System.Activities.Presentation.Toolbox;assembly=System.Activities.Presentation"  
        xmlns:sys="clr-namespace:System;assembly=mscorlib"  
        Title="Window1" Height="600" Width="900">  
    <Window.Resources>  
        <sys:String x:Key="AssemblyName">System.Activities, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35</sys:String>  
    </Window.Resources>  
    <Grid>  
        <Grid.ColumnDefinitions>  
            <ColumnDefinition Width="2*"/>  
            <ColumnDefinition Width="7*"/>  
            <ColumnDefinition Width="3*"/>  
        </Grid.ColumnDefinitions>  
        <Border Grid.Column="0">  
            <sapt:ToolboxControl>  
                <sapt:ToolboxCategory CategoryName="Basic">  
                    <sapt:ToolboxItemWrapper AssemblyName="{StaticResource AssemblyName}" >  
                        <sapt:ToolboxItemWrapper.ToolName>  
                            System.Activities.Statements.Sequence  
                        </sapt:ToolboxItemWrapper.ToolName>  
                       </sapt:ToolboxItemWrapper>  
                    <sapt:ToolboxItemWrapper  AssemblyName="{StaticResource AssemblyName}">  
                        <sapt:ToolboxItemWrapper.ToolName>  
                            System.Activities.Statements.WriteLine  
                        </sapt:ToolboxItemWrapper.ToolName>  
  
                    </sapt:ToolboxItemWrapper>  
                    <sapt:ToolboxItemWrapper  AssemblyName="{StaticResource AssemblyName}">  
                        <sapt:ToolboxItemWrapper.ToolName>  
                            System.Activities.Statements.If  
                        </sapt:ToolboxItemWrapper.ToolName>  
  
                    </sapt:ToolboxItemWrapper>  
                    <sapt:ToolboxItemWrapper  AssemblyName="{StaticResource AssemblyName}">  
                        <sapt:ToolboxItemWrapper.ToolName>  
                            System.Activities.Statements.While  
                        </sapt:ToolboxItemWrapper.ToolName>  
  
                    </sapt:ToolboxItemWrapper>  
                </sapt:ToolboxCategory>  
            </sapt:ToolboxControl>  
        </Border>  
        <Border Grid.Column="1" Name="DesignerBorder"/>  
        <Border Grid.Column="2" Name="PropertyBorder"/>  
    </Grid>  
</Window>  
```  
  
#### <a name="using-the-sample"></a>샘플 사용  
  
1. Visual Studio 2010에서 DesignerRehosting 솔루션을 엽니다.  
  
2. F5 키를 눌러 애플리케이션을 컴파일하고 실행합니다.  
  
3. 재호스트된 디자이너와 함께 WPF 응용 프로그램이 시작됩니다.  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WF\Basic\DesignerRehosting\Basic`
