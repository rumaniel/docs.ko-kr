---
title: 속성 표 확장성-WF 샘플
ms.date: 03/30/2017
ms.assetid: 3530c3a3-756d-4712-9f10-fb2897414d3a
ms.openlocfilehash: 1cc8b8b34d6236e263f95439da84994e35d627ed
ms.sourcegitcommit: a8d3504f0eae1a40bda2b06bd441ba01f1631ef0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2019
ms.locfileid: "67170361"
---
# <a name="property-grid-extensibility"></a>속성 표 확장성

개발자는 디자이너 내에서 지정된 활동을 선택할 경우 표시되는 속성 표를 사용자 지정할 수 있으므로 이를 통해 다양한 편집 환경을 만들 수 있습니다. 이 샘플에서는 이러한 작업을 수행하는 방식을 보여 줍니다.

## <a name="demonstrates"></a>세부 항목

Workflow Designer 속성 표 확장성

> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 이 디렉터리가 없으면로 이동 [Windows Communication Foundation (WCF) 및.NET Framework 4 용 Windows WF (Workflow Foundation) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 모든 Windows Communication Foundation (WCF)를 다운로드 하 고 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플. 이 샘플은 다음 디렉터리에 있습니다.
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Designer\PropertyGridExtensibility`

## <a name="discussion"></a>토론

개발자는 속성 표 편집기의 인라인 모양을 사용자 지정하거나 고급 편집 화면용으로 표시되는 대화 상자를 제공하여 속성 표를 확장할 수 있습니다. 이 샘플에 나오는 편집기는 인라인 편집기와 대화 상자 편집기, 이렇게 두 가지가 있습니다.

## <a name="inline-editor"></a>인라인 편집기

인라인 편집기 샘플에서는 다음 방법을 보여 줍니다.

- <xref:System.Activities.Presentation.PropertyEditing.PropertyValueEditor>에서 파생되는 형식을 만듭니다.

- 생성자에는 <xref:System.Activities.Presentation.PropertyEditing.PropertyValueEditor.InlineEditorTemplate%2A> 값은 Windows Presentation Foundation (WPF) 데이터 템플릿을 사용 하 여 설정 됩니다. 이 값은 XAML 템플릿에 바인딩할 수 있지만 이 샘플에서는 코드를 사용하여 데이터 바인딩을 초기화합니다.

- 데이터 템플릿에는 속성 표에서 렌더링된 항목의 <xref:System.Activities.Presentation.PropertyEditing.PropertyValue>에 대한 데이터 컨텍스트가 있습니다. CustomInlineEditor.cs에 있는 다음 코드에서는 이 컨텍스트가 `Value` 속성에 바인딩됩니다.

    ```csharp
    FrameworkElementFactory stack = new FrameworkElementFactory(typeof(StackPanel));
    FrameworkElementFactory slider = new FrameworkElementFactory(typeof(Slider));
    Binding sliderBinding = new Binding("Value");
    sliderBinding.Mode = BindingMode.TwoWay;
    slider.SetValue(Slider.MinimumProperty, 0.0);
    slider.SetValue(Slider.MaximumProperty, 100.0);
    slider.SetValue(Slider.ValueProperty, sliderBinding);
    stack.AppendChild(slider);
    ```

- 활동과 디자이너는 같은 어셈블리에 있기 때문에 활동 디자이너 특성은 SimpleCodeActivity.cs의 다음 예제와 같이 활동 자체의 정적 생성자에서 등록됩니다.

    ```csharp
    static SimpleCodeActivity()
    {
        AttributeTableBuilder builder = new AttributeTableBuilder();
        builder.AddCustomAttributes(typeof(SimpleCodeActivity), "RepeatCount", new EditorAttribute(typeof(CustomInlineEditor), typeof(PropertyValueEditor)));
        builder.AddCustomAttributes(typeof(SimpleCodeActivity), "FileName", new EditorAttribute(typeof(FilePickerEditor), typeof(DialogPropertyValueEditor)));
        MetadataStore.AddAttributeTable(builder.CreateTable());
    }
    ```

## <a name="dialog-editor"></a>대화 상자 편집기

대화 상자 편집기 샘플에서는 다음 방법을 보여 줍니다.

1. <xref:System.Activities.Presentation.PropertyEditing.DialogPropertyValueEditor>에서 파생되는 형식을 만듭니다.

2. 집합의 <xref:System.Activities.Presentation.PropertyEditing.PropertyValueEditor.InlineEditorTemplate%2A> WPF 데이터 템플릿 사용 하 여 생성자의 값입니다. 이 값을 XAML로 만들 수 있지만 이 샘플에서는 코드로 만듭니다.

3. 데이터 템플릿에는 속성 표에서 렌더링된 항목의 <xref:System.Activities.Presentation.PropertyEditing.PropertyValue>에 대한 데이터 컨텍스트가 있습니다. 다음 코드에서는 이 컨텍스트가 `Value` 속성에 바인딩됩니다. FilePickerEditor.cs에 대화 상자를 발생시키는 단추를 제공하도록 <xref:System.Activities.Presentation.PropertyEditing.EditModeSwitchButton>를 포함하는 것도 중요합니다.

    ```csharp
    this.InlineEditorTemplate = new DataTemplate();

    FrameworkElementFactory stack = new FrameworkElementFactory(typeof(StackPanel));
    stack.SetValue(StackPanel.OrientationProperty, Orientation.Horizontal);
    FrameworkElementFactory label = new FrameworkElementFactory(typeof(Label));
    Binding labelBinding = new Binding("Value");
    label.SetValue(Label.ContentProperty, labelBinding);
    label.SetValue(Label.MaxWidthProperty, 90.0);

    stack.AppendChild(label);

    FrameworkElementFactory editModeSwitch = new FrameworkElementFactory(typeof(EditModeSwitchButton));

    editModeSwitch.SetValue(EditModeSwitchButton.TargetEditModeProperty, PropertyContainerEditMode.Dialog);

    stack.AppendChild(editModeSwitch);

    this.InlineEditorTemplate.VisualTree = stack;
    ```

4. 대화 상자 표시를 처리하도록 디자이너 형식의 <xref:System.Activities.Presentation.PropertyEditing.DialogPropertyValueEditor.ShowDialog%2A> 메서드를 재정의합니다. 이 샘플에서는 기본 <xref:System.Windows.Forms.FileDialog>가 표시됩니다.

    ```csharp
    public override void ShowDialog(PropertyValue propertyValue, IInputElement commandSource)
    {
        Microsoft.Win32.OpenFileDialog ofd = new Microsoft.Win32.OpenFileDialog();
        if (ofd.ShowDialog() == true)
        {
            propertyValue.Value = ofd.FileName;
        }
    }
    ```

5. 활동과 디자이너는 같은 어셈블리에 있기 때문에 활동 디자이너 특성은 SimpleCodeActivity.cs의 다음 예제와 같이 활동 자체의 정적 생성자에서 등록됩니다.

    ```csharp
    static SimpleCodeActivity()
    {
        AttributeTableBuilder builder = new AttributeTableBuilder();
        builder.AddCustomAttributes(typeof(SimpleCodeActivity), "RepeatCount", new EditorAttribute(typeof(CustomInlineEditor), typeof(PropertyValueEditor)));
        builder.AddCustomAttributes(typeof(SimpleCodeActivity), "FileName", new EditorAttribute(typeof(FilePickerEditor), typeof(DialogPropertyValueEditor)));
        MetadataStore.AddAttributeTable(builder.CreateTable());
    }
    ```

## <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면

1. 솔루션을 빌드한 다음 Workflow1.xaml을 엽니다.

2. 끌어서를 **SimpleCodeActivity** 디자이너 캔버스로 도구 상자에서.

3. 클릭 합니다 **SimpleCodeActivity** 연 다음 속성 표의 슬라이더 컨트롤에 있는 파일과 컨트롤을 선택 합니다.

> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 이 디렉터리가 없으면로 이동 [Windows Communication Foundation (WCF) 및.NET Framework 4 용 Windows WF (Workflow Foundation) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 모든 Windows Communication Foundation (WCF)를 다운로드 하 고 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플. 이 샘플은 다음 디렉터리에 있습니다.
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Designer\PropertyGridExtensibility`
