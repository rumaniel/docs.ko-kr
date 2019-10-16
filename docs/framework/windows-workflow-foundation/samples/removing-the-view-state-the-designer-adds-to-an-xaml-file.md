---
title: WF는 XAML 파일에 추가 된 디자이너 뷰 상태 제거
ms.date: 03/30/2017
ms.assetid: a801ce22-8699-483c-a392-7bb3834aae4f
ms.openlocfilehash: af57f838ea12d7199268988bf01baa0b61447650
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65637852"
---
# <a name="removing-the-view-state-the-designer-adds-to-an-xaml-file"></a>XAML 파일에 추가 하는 디자이너 뷰 상태 제거

이 샘플에서는 <xref:System.Xaml.XamlWriter>에서 파생되며 XAML 파일에서 뷰 상태를 제거하는 클래스를 만드는 방법을 보여 줍니다. [!INCLUDE[wfd1](../../../../includes/wfd1-md.md)]에서는 뷰 상태라고 하는 정보를 XAML 문서에 기록합니다. 뷰 상태는 런타임에 필요하지 않으며 디자인 타임에 필요한 레이아웃 위치 등과 같은 정보를 가리킵니다. [!INCLUDE[wfd2](../../../../includes/wfd2-md.md)]에서는 XAML 문서를 편집할 때 이 정보를 해당 문서에 삽입합니다. [!INCLUDE[wfd2](../../../../includes/wfd2-md.md)]에서는 XAML 파일에 뷰 상태를 기록하는 데 `mc:Ignorable` 특성을 사용하므로 런타임에 XAML 파일을 로드할 때는 이 정보가 로드되지 않습니다. 이 샘플에서는 XAML 노드를 처리하는 동안 이와 같은 뷰 상태 정보를 제거하는 클래스를 만드는 방법을 보여 줍니다.

## <a name="discussion"></a>토론

이 샘플에서는 사용자 지정 작성기를 만드는 방법을 보여 줍니다.

사용자 지정 XAML 작성기를 빌드하려면 <xref:System.Xaml.XamlWriter>에서 상속되는 클래스를 만듭니다. XAML 작성기가 종종 중첩 되어 것을 "내부" XAML 작성기를 추적 하기 위해 일반적인 합니다. 이러한 "내부 ' 기록기에 작업을 다음 처리를 스택의 나머지 부분을 위임 하기 위해 여러 진입점이 있을 수 있습니다, XAML 작성기의 나머지 스택에 대 한 참조로 생각할 수 있습니다.

이 샘플에서는 특히 주목해야 할 항목이 몇 가지 있습니다. 그 중 하나는 기록할 항목이 디자이너 네임스페이스에 속한 것인지 여부를 확인하는 일입니다. 이렇게 하면 워크플로의 디자이너 네임스페이스에서 다른 형식을 사용하지 않도록 방지하는 효과도 있습니다.

```csharp
static Boolean IsDesignerAttachedProperty(XamlMember xamlMember)
{
    return xamlMember.IsAttachable &&
        xamlMember.PreferredXamlNamespace.Equals(c_sapNamespaceURI, StringComparison.OrdinalIgnoreCase);
}

const String c_sapNamespaceURI = "http://schemas.microsoft.com/netfx/2009/xaml/activities/presentation";

// The next item of interest is the constructor, where the utilization of the inner XAML writer is seen.
public ViewStateCleaningWriter(XamlWriter innerWriter)
{
    this.InnerWriter = innerWriter;
    this.MemberStack = new Stack<XamlMember>();
}

XamlWriter InnerWriter {get; set; }
Stack<XamlMember> MemberStack {get; set; }
```

또한 이렇게 하면 노드 스트림을 통과하는 동안 사용되는 XAML 멤버의 스택이 만들어집니다. 이 샘플의 나머지 부분은 주로 `WriteStartMember` 메서드에 포함됩니다.

```csharp
public override void WriteStartMember(XamlMember xamlMember)
{
    MemberStack.Push(xamlMember);

    if (IsDesignerAttachedProperty(xamlMember))
    {
        m_attachedPropertyDepth++;
    }

    if (m_attachedPropertyDepth > 0)
    {
        return;
    }

    InnerWriter.WriteStartMember(xamlMember);
}
```

이후의 메서드에서는 해당 메서드가 여전히 뷰 상태 컨테이너에 포함되어 있는지 여부를 확인하고, 메서드가 뷰 상태 컨테이너에 포함되어 있으면 노드를 작성기 스택에 전달하지 않고 되돌아갑니다.

```csharp
public override void WriteValue(Object value)
{
    if (m_attachedPropertyDepth > 0)
    {
        return;
    }

    InnerWriter.WriteValue(value);
}
```

사용자 지정 XAML 작성기를 사용하려면 이를 XAML 작성기 스택에 함께 연결해야 합니다. 다음 코드에서는 이를 사용하는 방법을 보여 줍니다.

```csharp
XmlWriterSettings writerSettings = new XmlWriterSettings {  Indent = true };
XmlWriter xmlWriter = XmlWriter.Create(File.OpenWrite(args[1]), writerSettings);
XamlXmlWriter xamlWriter = new XamlXmlWriter(xmlWriter, new XamlSchemaContext());
XamlServices.Save(new ViewStateCleaningWriter(ActivityXamlServices.CreateBuilderWriter(xamlWriter)), ab);
```

## <a name="to-use-this-sample"></a>이 샘플을 사용하려면

1. ViewStateCleaningWriter.sln 솔루션 파일을 열고 Visual Studio 2010을 사용 합니다.

2. 명령 프롬프트를 열고 ViewStageCleaningWriter.exe가 빌드된 디렉터리로 이동합니다.

3. Workflow1.xaml 파일에 대해 ViewStateCleaningWriter.exe를 실행합니다.

   실행 파일의 구문은 다음과 같습니다.

   ```console
   ViewStateCleaningWriter.exe [input file] [output file]
   ```

   XAML 파일을이 출력 \[outfile]에 있는 해당 뷰 상태 정보가 모두 제거 합니다.

> [!NOTE]
> <xref:System.Activities.Statements.Sequence> 워크플로의 경우 여러 개의 가상화 힌트도 제거됩니다. 따라서 다음 번 로드 시 디자이너를 통해 레이아웃이 다시 계산됩니다. <xref:System.Activities.Statements.Flowchart>에 대해 이 샘플을 사용하면 위치 및 선 라우팅 정보가 모두 제거되며, 이를 다음 번에 디자이너로 다시 로드하면 모든 활동이 화면 왼쪽에 쌓입니다.

## <a name="to-create-a-sample-xaml-file-for-use-with-this-sample"></a>이 샘플과 함께 사용할 샘플 XAML 파일을 만들려면

1. Visual Studio 2010을 엽니다.

2. 새 워크플로 콘솔 애플리케이션을 만듭니다.

3. 몇 가지 활동을 끌어 캔버스에 놓습니다.

4. 워크플로 XAML 파일을 저장합니다.

5. XAML 파일을 조사하여 속성에 연결된 뷰 상태가 있는지 확인합니다.

> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 이 디렉터리가 없으면로 이동 [Windows Communication Foundation (WCF) 및.NET Framework 4 용 Windows WF (Workflow Foundation) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 모든 Windows Communication Foundation (WCF)를 다운로드 하 고 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플. 이 샘플은 다음 디렉터리에 있습니다.
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Designer\ViewStateCleaningWriter`
