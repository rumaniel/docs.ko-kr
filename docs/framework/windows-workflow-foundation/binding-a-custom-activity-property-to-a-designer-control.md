---
title: 사용자 지정 작업 속성을 디자이너 컨트롤에 바인딩
ms.date: 03/30/2017
ms.assetid: 2e8061ea-10f5-407c-a31f-d0d74ce12f27
ms.openlocfilehash: 142a9eb273a98d3a2d83a1239d6d7c891d5cc305
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61945901"
---
# <a name="binding-a-custom-activity-property-to-a-designer-control"></a>사용자 지정 작업 속성을 디자이너 컨트롤에 바인딩

텍스트 상자 디자이너 컨트롤을 작업 인수에 바인딩하는 작업은 비교적 간단하지만 복잡한 디자이너 컨트롤(예: 콤보 상자)을 작업 인수에 바인딩하는 작업은 까다로울 수 있습니다. 이 항목에서는 사용자 지정 작업 디자이너에서 작업 인수를 콤보 상자 컨트롤에 바인딩하는 방법에 대해 설명합니다.

## <a name="creating-the-combo-box-item-converter"></a>콤보 상자 항목 변환기 만들기

1. Visual Studio에서 CustomProperty라는 빈 솔루션을 새로 만듭니다.

2. ComboBoxItemConverter라는 새 클래스를 만듭니다. System.Windows.Data에 대한 참조를 추가하고 클래스가 <xref:System.Windows.Data.IValueConverter>에서 파생되도록 합니다. Visual Studio에서 `Convert` 및 `ConvertBack`에 대한 스텁을 생성하는 인터페이스를 구현하도록 합니다.

3. `Convert` 메서드에 다음 코드를 추가합니다. 이 코드는 작업의 <xref:System.Activities.InArgument%601> 형식 <xref:System.String>를 디자이너에 배치할 값으로 변환합니다.

    ```csharp
    ModelItem modelItem = value as ModelItem;
    if (value != null)
    {
        InArgument<string> inArgument = modelItem.GetCurrentValue() as InArgument<string>;

        if (inArgument != null)
        {
            Activity<string> expression = inArgument.Expression;
            VisualBasicValue<string> vbexpression = expression as VisualBasicValue<string>;
            Literal<string> literal = expression as Literal<string>;

            if (literal != null)
            {
                return "\"" + literal.Value + "\"";
            }
            else if (vbexpression != null)
            {
                return vbexpression.ExpressionText;
            }
        }
    }
    return null;
    ```

     위의 코드 조각에서 <xref:Microsoft.CSharp.Activities.CSharpValue%601> 대신 <xref:Microsoft.VisualBasic.Activities.VisualBasicValue%601>을 사용하여 식을 만들 수도 있습니다.

    ```csharp
    ModelItem modelItem = value as ModelItem;
    if (value != null)
    {
        InArgument<string> inArgument = modelItem.GetCurrentValue() as InArgument<string>;

        if (inArgument != null)
        {
            Activity<string> expression = inArgument.Expression;
            CSharpValue<string> csexpression = expression as CSharpValue<string>;
            Literal<string> literal = expression as Literal<string>;

            if (literal != null)
            {
                return "\"" + literal.Value + "\"";
            }
            else if (csexpression != null)
            {
                return csexpression.ExpressionText;
            }
        }
    }
    return null;
    ```

4. `ConvertBack` 메서드에 다음 코드를 추가합니다. 이 코드는 들어오는 콤보 상자 항목을 <xref:System.Activities.InArgument%601>로 다시 변환합니다.

    ```csharp
    // Convert combo box value to InArgument<string>
                string itemContent = (string)((ComboBoxItem)value).Content;
                VisualBasicValue<string> vbArgument = new VisualBasicValue<string>(itemContent);
                InArgument<string> inArgument = new InArgument<string>(vbArgument);
                return inArgument;
    ```

     위의 코드 조각에서 <xref:Microsoft.CSharp.Activities.CSharpValue%601> 대신 <xref:Microsoft.VisualBasic.Activities.VisualBasicValue%601>을 사용하여 식을 만들 수도 있습니다.

    ```csharp
    // Convert combo box value to InArgument<string>
                string itemContent = (string)((ComboBoxItem)value).Content;
                CSharpValue<string> csArgument = new CSharpValue<string>(itemContent);
                InArgument<string> inArgument = new InArgument<string>(csArgument);
                return inArgument;
    ```

## <a name="adding-the-comboboxitemconverter-to-the-custom-designer-of-an-activity"></a>작업의 사용자 지정 디자이너에 ComboBoxItemConverter 추가

1. 프로젝트에 새 항목을 추가합니다. 새 항목 대화 상자에서 워크플로 노드를 선택한 다음 새 항목의 형식으로 작업 디자이너를 선택합니다. 항목의 이름을 CustomPropertyDesigner로 지정합니다.

2. 새 디자이너에 콤보 상자를 추가합니다. Items 속성에서 Content 값을 "Item1" 및 'Item2"로 지정하여 항목 두 개를 콤보 상자에 추가합니다.

3. 콤보 상자의 XAML을 수정하여 콤보 상자에 사용할 항목 변환기로 새 항목 변환기를 추가합니다. 변환기가 ActivityDesigner.Resources 세그먼트에 리소스로 추가되고 <xref:System.Windows.Controls.ComboBox>에 대한 Converter 특성의 변환기를 지정합니다. 프로젝트의 네임스페이스는 작업 디자이너의 네임스페이스 특성에서 지정됩니다. 다른 프로젝트에서 디자이너를 사용하려는 경우 이 네임스페이스를 변경해야 합니다.

    ```xaml
    <sap:ActivityDesigner x:Class="CustomProperty.CustomPropertyDesigner"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:c="clr-namespace:CustomProperty"
        xmlns:sap="clr-namespace:System.Activities.Presentation;assembly=System.Activities.Presentation"
        xmlns:sapv="clr-namespace:System.Activities.Presentation.View;assembly=System.Activities.Presentation">

        <sap:ActivityDesigner.Resources>
            <ResourceDictionary>
                <c:ComboBoxItemConverter x:Key="comboBoxItemConverter"/>
            </ResourceDictionary>
        </sap:ActivityDesigner.Resources>
        <Grid>
            <ComboBox SelectedValue="{Binding Path=ModelItem.Text, Mode=TwoWay, Converter={StaticResource comboBoxItemConverter}}"  Height="23" HorizontalAlignment="Left" Margin="132,5,0,0" Name="comboBox1" VerticalAlignment="Top" Width="120" ItemsSource="{Binding}">
                <ComboBoxItem>item1</ComboBoxItem>
                <ComboBoxItem>item2</ComboBoxItem>
            </ComboBox>
        </Grid>
    </sap:ActivityDesigner>
    ```

4. <xref:System.Activities.CodeActivity> 형식의 새 항목을 만듭니다. 이 예제에는 IDE에서 작업에 대해 만드는 기본 코드만으로 충분합니다.

5. 클래스 정의에 다음 특성을 추가합니다.

    ```csharp
    [Designer(typeof(CustomPropertyDesigner))]
    ```

     이 줄에서는 새 디자이너를 새 클래스에 연결합니다.

 이제 새 작업이 디자이너에 연결됩니다. 새 작업을 테스트하려면 워크플로에 작업을 추가하고 콤보 상자를 두 개의 값으로 설정합니다. 속성 창이 업데이트되어 콤보 상자 값을 반영합니다.
