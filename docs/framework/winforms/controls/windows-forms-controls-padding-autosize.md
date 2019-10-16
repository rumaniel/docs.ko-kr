---
title: '연습: Padding, Margin 및 AutoSize 속성을 사용하여 Windows Forms 컨트롤 레이아웃'
ms.date: 03/30/2017
f1_keywords:
- Margin.Bottom
- Margin.Left
- Margin.Top
- Margin.All
- Margin.Right
helpviewer_keywords:
- Margin property [Windows Forms], walkthroughs
- walkthroughs [Windows Forms], layout
- AutoSize property [Windows Forms], walkthroughs
- Padding property [Windows Forms], walkthroughs
- layout [Windows Forms], margins and padding
- Windows Forms, layout
ms.assetid: f8ae2a6b-db13-4630-8e25-d104091205c7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: daf0c6495b89033e75c27a1ff0cbceaff9d85f34
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69987162"
---
# <a name="walkthrough-lay-out-controls-with-padding-margins-and-the-autosize-property"></a>연습: 안쪽 여백, 여백 및 AutoSize 속성을 사용 하 여 컨트롤 레이아웃

폼의 정확한 컨트롤 배치는 많은 애플리케이션에서 우선 순위가 높습니다. Visual Studio의 **Windows Forms 디자이너** 는이를 위해 다양 한 레이아웃 도구를 제공 합니다. 가장 중요 한 <xref:System.Windows.Forms.Control.Margin%2A>세 가지는 모든 Windows Forms 컨트롤에 <xref:System.Windows.Forms.Control.AutoSize%2A> 나타나는, <xref:System.Windows.Forms.Control.Padding%2A>및 속성입니다.

<xref:System.Windows.Forms.Control.Margin%2A> 속성은 다른 컨트롤을 컨트롤의 테두리에서 지정된 거리에 유지하는 컨트롤 주위의 공간을 정의합니다.

<xref:System.Windows.Forms.Control.Padding%2A> 속성은 컨트롤의 내용(예: <xref:System.Windows.Forms.Control.Text%2A> 속성의 값)을 컨트롤의 테두리에서 지정된 거리에 유지하는 컨트롤 내부의 공간을 정의합니다.

다음 그림에서는 컨트롤의 <xref:System.Windows.Forms.Control.Padding%2A> 및 <xref:System.Windows.Forms.Control.Margin%2A> 속성을 보여 줍니다.

![Windows Forms 컨트롤의 여백 및 안쪽 여백](./media/vs-winformpadmargin.gif)

속성 <xref:System.Windows.Forms.Control.AutoSize%2A> 은 컨트롤이 내용에 맞게 자동으로 크기를 조정 하도록 지시 합니다. 원래 <xref:System.Windows.Forms.Control.Size%2A> 속성의 값 보다 작게 크기를 조정 하지 않으며 해당 <xref:System.Windows.Forms.Control.Padding%2A> 속성의 값을 고려 합니다.

## <a name="prerequisites"></a>필수 구성 요소

이 연습을 완료 하려면 Visual Studio가 필요 합니다.

## <a name="create-the-project"></a>프로젝트를 만듭니다.

1. Visual Studio에서 라는 `LayoutExample` **Windows 응용 프로그램** 프로젝트를 만듭니다.

2. **Windows Forms 디자이너**에서 양식을 선택 합니다.

## <a name="set-margins-for-controls"></a>컨트롤의 여백 설정

속성을 <xref:System.Windows.Forms.Control.Margin%2A> 사용 하 여 컨트롤 간의 기본 거리를 설정할 수 있습니다. 컨트롤을 다른 컨트롤에 가까이 이동할 때 두 컨트롤의 여백을 보여 주는 맞춤선이 표시 됩니다. 이동 하는 컨트롤은 여백으로 정의 된 거리에도 맞춰집니다.

### <a name="arrange-controls-on-your-form-using-the-margin-property"></a>Margin 속성을 사용 하 여 폼에 컨트롤을 정렬 합니다.

1. <xref:System.Windows.Forms.Button> **도구 상자** 에서 두 컨트롤을 폼으로 끌어 옵니다.

2. <xref:System.Windows.Forms.Button> 컨트롤 중 하나를 선택 하 고 거의 닿을 때까지 다른 컨트롤에 가깝게 이동 합니다.

   두 항목 사이에 나타나는 맞춤선을 관찰 합니다. 이 거리는 두 컨트롤 <xref:System.Windows.Forms.Control.Margin%2A> 값의 합계입니다. 이동 하는 컨트롤이이 거리에 맞춰집니다. 자세한 [내용은 연습: 맞춤선](walkthrough-arranging-controls-on-windows-forms-using-snaplines.md)을 사용 하 여 Windows Forms에 컨트롤 정렬

3. **속성 창** 에서 <xref:System.Windows.Forms.Control.Margin%2A> 항목을 확장 하 고 <xref:System.Windows.Forms.Padding.All%2A> 속성을 **20**으로 설정 하 여 컨트롤 중 하나의 속성을변경합니다.<xref:System.Windows.Forms.Control.Margin%2A>

4. <xref:System.Windows.Forms.Button> 컨트롤 중 하나를 선택 하 고 다른 컨트롤에 가깝게 이동 합니다.

   여백 값의 합을 정의 하는 맞춤선이 더 길고 컨트롤이 다른 컨트롤에서 더 큰 거리에 맞춰집니다.

5. **속성** 창 <xref:System.Windows.Forms.Control.Margin%2A> 에서 <xref:System.Windows.Forms.Control.Margin%2A> 항목을 확장 하 고 <xref:System.Windows.Forms.Padding.Top%2A> 속성을 **5**로 설정 하 여 선택한 컨트롤의 속성을 변경 합니다.

6. 선택한 컨트롤을 다른 컨트롤 아래로 이동 하 여 맞춤선이 더 짧아 지는 지 확인 합니다. 선택한 컨트롤을 다른 컨트롤의 왼쪽으로 이동 하 고 4 단계에서 관찰 된 값이 맞춤선에 유지 되는지 확인 합니다.

7. <xref:System.Windows.Forms.Control.Margin%2A> 속성<xref:System.Windows.Forms.Padding.Right%2A> 의각<xref:System.Windows.Forms.Padding.All%2A> 특성,,,, 를다른값으로설정하거나속성을사용하여모두동일한값으로설정할수있습니다.<xref:System.Windows.Forms.Padding.Bottom%2A> <xref:System.Windows.Forms.Padding.Left%2A> <xref:System.Windows.Forms.Padding.Top%2A>

## <a name="set-padding-for-controls"></a>컨트롤의 안쪽 여백 설정

응용 프로그램에 필요한 정확한 레이아웃을 얻기 위해 컨트롤에는 종종 자식 컨트롤이 포함 됩니다. 자식 컨트롤의 테두리를 부모 컨트롤의 테두리에 근접 하 게 지정 하려는 경우 부모 <xref:System.Windows.Forms.Control.Padding%2A> 컨트롤의 속성을 자식 <xref:System.Windows.Forms.Control.Margin%2A> 컨트롤의 속성과 함께 사용 합니다. 속성은 컨트롤의 콘텐츠 (예: <xref:System.Windows.Forms.Button> 컨트롤의 <xref:System.Windows.Forms.Control.Text%2A> 속성)가 해당 테두리에 근접 하는 것을 제어 하는 데도 사용 됩니다. <xref:System.Windows.Forms.Control.Padding%2A>

### <a name="arrange-controls-on-your-form-using-padding"></a>안쪽 여백을 사용 하 여 폼에 컨트롤 정렬

1. <xref:System.Windows.Forms.Button> 도구 상자 **에서** 컨트롤을 폼으로 끌어다 놓습니다.

2. 컨트롤의 속성 값 **을 true**로 변경 합니다. <xref:System.Windows.Forms.Control.AutoSize%2A> <xref:System.Windows.Forms.Button>

3. 속성 창 <xref:System.Windows.Forms.Control.Padding%2A> 에서 <xref:System.Windows.Forms.Control.Padding%2A> 항목을 확장 하 고 <xref:System.Windows.Forms.Padding.All%2A> 속성을 **5**로 설정 하 여 속성을 변경 합니다.

   컨트롤이 확장 되어 새 안쪽 여백을 위한 공간을 제공 합니다.

4. <xref:System.Windows.Forms.GroupBox> 도구 상자 **에서** 컨트롤을 폼으로 끌어다 놓습니다. **도구 상자** <xref:System.Windows.Forms.Button> 에서컨트롤로컨트롤을끌어옵니다.<xref:System.Windows.Forms.GroupBox> 컨트롤의 오른쪽 아래 모퉁이에 맞도록 컨트롤의위치를조정합니다.<xref:System.Windows.Forms.Button> <xref:System.Windows.Forms.GroupBox>

   컨트롤이 <xref:System.Windows.Forms.Button> 컨트롤<xref:System.Windows.Forms.GroupBox> 의 아래쪽 및 오른쪽 테두리에 가까워지면 표시 되는 맞춤선을 관찰 합니다. 이러한 맞춤선은 <xref:System.Windows.Forms.Control.Margin%2A> <xref:System.Windows.Forms.Button>의 속성에 해당 합니다.

5. **속성** 창 <xref:System.Windows.Forms.GroupBox> 에서 <xref:System.Windows.Forms.Control.Padding%2A> 항목을<xref:System.Windows.Forms.Control.Padding%2A> 확장 하 고속성을 20으로 설정 하 여 컨트롤의 속성을 변경 합니다 <xref:System.Windows.Forms.Padding.All%2A> .

6. 컨트롤 내에서 컨트롤을 <xref:System.Windows.Forms.Button> 선택 하 고의 <xref:System.Windows.Forms.GroupBox>가운데로 이동 합니다. <xref:System.Windows.Forms.GroupBox>

   맞춤선이 <xref:System.Windows.Forms.GroupBox> 컨트롤의 테두리에서 더 큰 거리에 표시 됩니다. 이 <xref:System.Windows.Forms.Button> 거리는 <xref:System.Windows.Forms.Control.Margin%2A> 컨트롤의 속성 및 <xref:System.Windows.Forms.GroupBox> 컨트롤의 <xref:System.Windows.Forms.Control.Padding%2A> 속성에 대 한 합계입니다.

## <a name="size-controls-automatically"></a>컨트롤 자동 크기 조정

일부 응용 프로그램에서는 컨트롤의 크기가 디자인 타임에와 동일 하 게 실행 되지 않습니다. 예를 들어, <xref:System.Windows.Forms.Button> 컨트롤의 텍스트는 데이터베이스에서 가져올 수 있으며 해당 길이는 미리 알 수 없습니다.

<xref:System.Windows.Forms.Control.AutoSize%2A> 속성이 로`true`설정 되 면 컨트롤은 해당 내용에 맞게 크기가 조정 됩니다. 자세한 내용은 [AutoSize 속성 개요](autosize-property-overview.md)를 참조 하세요.

### <a name="arrange-controls-on-your-form-using-the-autosize-property"></a>AutoSize 속성을 사용 하 여 폼에 컨트롤 정렬

1. <xref:System.Windows.Forms.Button> 도구 상자 **에서** 컨트롤을 폼으로 끌어다 놓습니다.

2. 컨트롤의 속성 값 **을 true**로 변경 합니다. <xref:System.Windows.Forms.Control.AutoSize%2A> <xref:System.Windows.Forms.Button>

3. 컨트롤의 <xref:System.Windows.Forms.Control.Text%2A> 속성을 **이 단추에 대 한 텍스트 속성의 긴 문자열로**변경 합니다. <xref:System.Windows.Forms.Button>

   변경 내용을 커밋하면 컨트롤의 <xref:System.Windows.Forms.Button> 크기가 새 텍스트에 맞게 조정 됩니다.

4. <xref:System.Windows.Forms.Button> **도구 상자** 에서 다른 컨트롤을 폼으로 끌어 놓습니다.

5. 컨트롤의 <xref:System.Windows.Forms.Control.Text%2A> 속성을 "**이 단추에는 텍스트 속성에 대 한 긴 문자열이 있습니다."로 변경 합니다.** <xref:System.Windows.Forms.Button>

   변경을 커밋할 때 컨트롤은 <xref:System.Windows.Forms.Button> 자체적으로 크기를 조정 하지 않으며 컨트롤의 오른쪽 가장자리에 의해 텍스트가 잘립니다.

6. 속성 창 <xref:System.Windows.Forms.Control.Padding%2A> 에서 <xref:System.Windows.Forms.Control.Padding%2A> 항목을 확장 하 고 <xref:System.Windows.Forms.Padding.All%2A> 속성을 **5**로 설정 하 여 속성을 변경 합니다.

   컨트롤의 내부에 있는 텍스트는 네 면 모두 잘립니다.

7. 컨트롤의 <xref:System.Windows.Forms.Button> <xref:System.Windows.Forms.Control.AutoSize%2A> 속성을 **true**로 변경 합니다.

   컨트롤 <xref:System.Windows.Forms.Button> 은 전체 문자열을 포함 하도록 크기를 조정 합니다. 또한 텍스트 <xref:System.Windows.Forms.Button> 주위에 안쪽 여백이 추가 되어 컨트롤이 네 방향으로 모두 확장 됩니다.

8. <xref:System.Windows.Forms.Button> 도구 상자 **에서** 컨트롤을 폼으로 끌어다 놓습니다. 폼의 오른쪽 아래 모퉁이 근처에 배치 합니다.

9. 컨트롤의 속성 값 **을 true**로 변경 합니다. <xref:System.Windows.Forms.Control.AutoSize%2A> <xref:System.Windows.Forms.Button>

10. 컨트롤의 <xref:System.Windows.Forms.Control.Anchor%2A> 속성<xref:System.Windows.Forms.AnchorStyles.Right>을 ,<xref:System.Windows.Forms.AnchorStyles.Bottom>로설정합니다. <xref:System.Windows.Forms.Button>

11. 컨트롤의 <xref:System.Windows.Forms.Control.Text%2A> 속성을 "**이 단추에는 텍스트 속성에 대 한 긴 문자열이 있습니다."로 변경 합니다.** <xref:System.Windows.Forms.Button>

   변경 내용을 커밋하면 <xref:System.Windows.Forms.Button> 컨트롤이 왼쪽 방향으로 조정 됩니다. 일반적으로 자동 크기 조정은 <xref:System.Windows.Forms.Control.Anchor%2A> 속성 설정 반대쪽의 방향으로 컨트롤의 크기를 증가 시킵니다.

## <a name="autosize-and-autosizemode-properties"></a>AutoSize 및 AutoSizeMode 속성

 일부 컨트롤은 `AutoSizeMode` 컨트롤의 자동 크기 조정 동작에 대 한 보다 세분화 된 제어를 제공 하는 속성을 지원 합니다.

### <a name="use-the-autosizemode-property"></a>AutoSizeMode 속성 사용

1. <xref:System.Windows.Forms.Panel> 도구 상자 **에서** 컨트롤을 폼으로 끌어다 놓습니다.

2. 컨트롤의 속성 값 **을 true**로 설정 합니다. <xref:System.Windows.Forms.Control.AutoSize%2A> <xref:System.Windows.Forms.Panel>

3. **도구 상자** <xref:System.Windows.Forms.Button> 에서컨트롤로컨트롤을끌어옵니다.<xref:System.Windows.Forms.Panel>

4. <xref:System.Windows.Forms.Button> 컨트롤<xref:System.Windows.Forms.Panel> 의 오른쪽 아래 모퉁이 근처에 컨트롤을 놓습니다.

5. 컨트롤을 <xref:System.Windows.Forms.Panel> 선택 하 고 오른쪽 아래 크기 조정 핸들을 가져옵니다. 컨트롤의 <xref:System.Windows.Forms.Panel> 크기를 더 크거나 작게 조정 합니다.

   > [!NOTE]
   > <xref:System.Windows.Forms.Panel> 컨트롤의 크기를 자유롭게 조정할 수 있지만 <xref:System.Windows.Forms.Button> 컨트롤의 오른쪽 아래 모퉁이의 위치 보다 작게 크기를 조정할 수 없습니다. 이 동작은 `AutoSizeMode` 속성의 기본값 ( <xref:System.Windows.Forms.AutoSizeMode.GrowOnly>)으로 지정 됩니다.

6. <xref:System.Windows.Forms.Panel> <xref:System.Windows.Forms.AutoSizeMode.GrowAndShrink>컨트롤의 속성값을로설정합니다.`AutoSizeMode`

   컨트롤의 크기를 조정 하 여 <xref:System.Windows.Forms.Button> 컨트롤을 둘러쌉니다. <xref:System.Windows.Forms.Panel> 컨트롤의 <xref:System.Windows.Forms.Panel> 크기를 조정할 수 없습니다.

7. 컨트롤을 <xref:System.Windows.Forms.Panel> 컨트롤의 왼쪽 위 모퉁이 쪽으로 끌어 옵니다. <xref:System.Windows.Forms.Button>

   컨트롤의 크기 <xref:System.Windows.Forms.Button> 를 컨트롤의 새 위치로 조정 합니다. <xref:System.Windows.Forms.Panel>

## <a name="next-steps"></a>다음 단계

Windows Forms 응용 프로그램에서 컨트롤을 정렬 하는 다양 한 레이아웃 기능이 있습니다. 다음은 시도해 볼 수 있는 몇 가지 조합입니다.

- 컨트롤을 <xref:System.Windows.Forms.TableLayoutPanel> 사용 하 여 폼을 빌드합니다. 자세한 [내용은 연습: TableLayoutPanel](walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)를 사용 하 여 Windows Forms에 컨트롤 정렬 컨트롤의 속성 값과 해당 자식 컨트롤의 속성을변경해봅니다.<xref:System.Windows.Forms.Control.Margin%2A> <xref:System.Windows.Forms.Control.Padding%2A> <xref:System.Windows.Forms.TableLayoutPanel>

- 컨트롤을 <xref:System.Windows.Forms.FlowLayoutPanel> 사용 하 여 동일한 실험을 시도 합니다. 자세한 [내용은 연습: FlowLayoutPanel](walkthrough-arranging-controls-on-windows-forms-using-a-flowlayoutpanel.md)를 사용 하 여 Windows Forms에 컨트롤 정렬

- <xref:System.Windows.Forms.Panel> 컨트롤의 도킹 자식 컨트롤을 사용 하 여 실험 합니다. 속성은 보다 일반적으로 <xref:System.Windows.Forms.ScrollableControl.DockPadding%2A> 속성을 인식 하며, 자식 컨트롤 <xref:System.Windows.Forms.Panel> 을 컨트롤에 배치 하 고 자식 컨트롤의 <xref:System.Windows.Forms.Control.Dock%2A> 속성을로 설정 하 여이에 대 한 것입니다. <xref:System.Windows.Forms.Control.Padding%2A> <xref:System.Windows.Forms.DockStyle.Fill>. <xref:System.Windows.Forms.Panel> 컨트롤 의<xref:System.Windows.Forms.Control.Padding%2A> 속성을 다양 한 값으로 설정 하 고 효과를 확인 합니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.Control.AutoSize%2A>
- <xref:System.Windows.Forms.ScrollableControl.DockPadding%2A>
- <xref:System.Windows.Forms.Control.Margin%2A>
- <xref:System.Windows.Forms.Control.Padding%2A>
- [AutoSize 속성 개요](autosize-property-overview.md)
- [연습: TableLayoutPanel를 사용 하 여 Windows Forms에서 컨트롤 정렬](walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)
- [연습: FlowLayoutPanel를 사용 하 여 Windows Forms에서 컨트롤 정렬](walkthrough-arranging-controls-on-windows-forms-using-a-flowlayoutpanel.md)
- [연습: 맞춤선을 사용 하 여 Windows Forms에서 컨트롤 정렬](walkthrough-arranging-controls-on-windows-forms-using-snaplines.md)
