---
title: '연습: 디자인 타임에 Windows Forms에서 WPF 콘텐츠 정렬'
ms.date: 03/30/2017
helpviewer_keywords:
- WPF user control [Windows Forms], hosting in a layout panel
- WPF content [Windows Forms], arranging at design time
- Windows Forms, arranging WPF content at design time
- WPF content [Windows Forms], hosting in Windows Forms
- Windows Forms, anchoring and docking WPF content
- interoperability [WPF]
ms.assetid: 5efb1c53-1484-43d6-aa8a-f4861b99bb8a
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 7858ffd708c78d6397d533f613ccc2ea78d6cbed
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69658520"
---
# <a name="walkthrough-arrange-wpf-content-on-windows-forms-at-design-time"></a>연습: 디자인 타임에 Windows Forms에서 WPF 콘텐츠 정렬

이 문서에서는 고정 및 맞춤선과 같은 Windows Forms 레이아웃 기능을 사용 하 여 Windows Presentation Foundation (WPF) 컨트롤을 정렬 하는 방법을 보여 줍니다.

## <a name="prerequisites"></a>필수 구성 요소

이 연습을 완료하려면 Visual Studio가 필요합니다.

## <a name="create-the-project"></a>프로젝트를 만듭니다.

Visual Studio를 열고 Visual Basic 또는 시각적 개체 C# `ArrangeElementHost`에 새 Windows Forms 응용 프로그램 프로젝트를 만듭니다.

> [!NOTE]
> WPF 콘텐츠를 호스트하는 경우 C# 및 Visual Basic 프로젝트만 지원됩니다.

## <a name="create-the-wpf-control"></a>WPF 컨트롤 만들기

프로젝트에 WPF 컨트롤을 추가한 후 폼에 정렬할 수 있습니다.

1. 프로젝트에 새 WPF <xref:System.Windows.Controls.UserControl>을 추가합니다. 컨트롤 형식의 기본 이름인 `UserControl1.xaml`을 사용합니다. 자세한 내용은 [연습: 디자인 타임](walkthrough-creating-new-wpf-content-on-windows-forms-at-design-time.md)에 WINDOWS FORMS에서 새 WPF 콘텐츠 만들기

2. 디자인 뷰에서 `UserControl1`이 선택되었는지 확인합니다.

3. **속성** 창에서 <xref:System.Windows.FrameworkElement.Width%2A> 및 <xref:System.Windows.FrameworkElement.Height%2A> 속성의 값을 **200**로 설정 합니다.

4. <xref:System.Windows.Controls.Control.Background%2A> 속성의 값을 **Blue**로 설정 합니다.

5. 프로젝트를 빌드합니다.

## <a name="host-wpf-controls-in-a-layout-panel"></a>레이아웃 패널에서 WPF 컨트롤 호스트

다른 Windows Forms 컨트롤을 사용하는 것과 동일한 방식으로 레이아웃 패널에서 WPF 컨트롤을 사용할 수 있습니다.

1. Windows Forms 디자이너에서 `Form1`을 엽니다.

2. **도구 상자**에서 컨트롤을 <xref:System.Windows.Forms.TableLayoutPanel> 폼으로 끌어옵니다.

3. 컨트롤의 스마트 태그 패널에서 **마지막 행 제거**를 선택 합니다. <xref:System.Windows.Forms.TableLayoutPanel>

4. <xref:System.Windows.Forms.TableLayoutPanel> 컨트롤을 더 큰 너비와 높이로 조정합니다.

5. **도구 상자**에서을 두 번 클릭 `UserControl1` 하 여 <xref:System.Windows.Forms.TableLayoutPanel> 컨트롤의 첫 `UserControl1` 번째 셀에의 인스턴스를 만듭니다.

   `UserControl1` 인스턴스가 `elementHost1`이라는 새 <xref:System.Windows.Forms.Integration.ElementHost> 컨트롤에서 호스트됩니다.

6. **도구 상자**에서 두 번 클릭 `UserControl1` 하 여 <xref:System.Windows.Forms.TableLayoutPanel> 컨트롤의 두 번째 셀에 다른 인스턴스를 만듭니다.

7. **문서 개요** 창에서을 선택 `tableLayoutPanel1`합니다.

8. **속성** 창에서 <xref:System.Windows.Forms.Control.Padding%2A> 속성의 값을 **10, 10, 10, 10**으로 설정 합니다.

   두 <xref:System.Windows.Forms.Integration.ElementHost> 컨트롤 모두 새 레이아웃에 맞게 크기가 조정됩니다.

## <a name="use-snaplines-to-align-wpf-controls"></a>맞춤선을 사용 하 여 WPF 컨트롤 맞춤

맞춤선을 사용하여 폼에서 컨트롤을 쉽게 맞출 수 있습니다. 맞춤선을 사용하여 WPF 컨트롤도 맞출 수 있습니다. 자세한 내용은 [연습: 맞춤선](../controls/walkthrough-arranging-controls-on-windows-forms-using-snaplines.md)을 사용 하 여 Windows Forms에 컨트롤 정렬

1. **도구 상자**에서의 `UserControl1` 인스턴스를 폼으로 끌고 <xref:System.Windows.Forms.TableLayoutPanel> 컨트롤 아래의 공간에 놓습니다.

   `UserControl1` 인스턴스가 `elementHost3`이라는 새 <xref:System.Windows.Forms.Integration.ElementHost> 컨트롤에서 호스트됩니다.

2. 맞춤선을 사용하여 `elementHost3`의 왼쪽 가장자리를 <xref:System.Windows.Forms.TableLayoutPanel> 컨트롤의 왼쪽 가장자리에 맞춥니다.

3. 맞춤선을 사용하여 `elementHost3`의 크기를 <xref:System.Windows.Forms.TableLayoutPanel> 컨트롤과 동일한 너비로 조정합니다.

4. 가운데 맞춤선이 컨트롤 사이에 나타날 때까지 `elementHost3`을 <xref:System.Windows.Forms.TableLayoutPanel> 컨트롤 쪽으로 이동합니다.

5. **속성** 창에서 Margin 속성의 값을 **20, 20, 20, 20**으로 설정 합니다.

6. 가운데 맞춤선이 다시 나타날 때까지 `elementHost3`을 <xref:System.Windows.Forms.TableLayoutPanel> 컨트롤에서 멀리 이동합니다. 이제 가운데 맞춤선이 여백 20을 나타냅니다.

7. 왼쪽 `elementHost3` 가장자리가의 `elementHost1`왼쪽 가장자리에 맞춰질 때까지 오른쪽으로 이동 합니다.

8. 오른쪽 가장자리가 `elementHost2`의 오른쪽 가장자리와 맞춰질 때까지 `elementHost3`의 너비를 변경합니다.

## <a name="anchor-and-dock-wpf-controls"></a>WPF 컨트롤 고정 및 도킹

폼에 호스트된 WPF 컨트롤은 다른 Windows Forms 컨트롤과 동일한 고정 및 도킹 동작을 갖습니다.

1. `elementHost1`을(를) 선택합니다.

2. **속성** 창에서 <xref:System.Windows.Forms.Control.Anchor%2A> 속성을 **Top, Bottom, Left, Right**로 설정 합니다.

3. <xref:System.Windows.Forms.TableLayoutPanel> 컨트롤을 더 큰 크기로 조정합니다.

   `elementHost1` 컨트롤의 크기가 조정되어 셀을 채웁니다.

4. `elementHost2`을(를) 선택합니다.

5. **속성** 창에서 <xref:System.Windows.Forms.Control.Dock%2A> 속성의 값을로 <xref:System.Windows.Forms.DockStyle.Fill>설정 합니다.

   `elementHost2` 컨트롤의 크기가 조정되어 셀을 채웁니다.

6. <xref:System.Windows.Forms.TableLayoutPanel> 컨트롤을 선택합니다.

7. <xref:System.Windows.Forms.Control.Dock%2A> 속성의 값을 <xref:System.Windows.Forms.DockStyle.Top>로 설정합니다.

8. `elementHost3`을(를) 선택합니다.

9. <xref:System.Windows.Forms.Control.Dock%2A> 속성의 값을 <xref:System.Windows.Forms.DockStyle.Fill>로 설정합니다.

   `elementHost3` 컨트롤의 크기가 조정되어 폼의 나머지 공간을 채웁니다.

10. 폼의 크기를 조정합니다.

    <xref:System.Windows.Forms.Integration.ElementHost> 컨트롤 3개의 크기가 모두 적절하게 조정됩니다.

    자세한 내용은 [방법: TableLayoutPanel 컨트롤](../controls/how-to-anchor-and-dock-child-controls-in-a-tablelayoutpanel-control.md)의 자식 컨트롤을 고정 및 도킹 합니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [방법: TableLayoutPanel 컨트롤에서 자식 컨트롤 고정 및 도킹](../controls/how-to-anchor-and-dock-child-controls-in-a-tablelayoutpanel-control.md)
- [방법: 디자인 타임에 컨트롤을 폼의 가장자리에 맞춤](../controls/how-to-align-a-control-to-the-edges-of-forms-at-design-time.md)
- [연습: 맞춤선을 사용 하 여 Windows Forms에서 컨트롤 정렬](../controls/walkthrough-arranging-controls-on-windows-forms-using-snaplines.md)
- [마이그레이션 및 상호 운용성](../../wpf/advanced/migration-and-interoperability.md)
- [WPF 컨트롤 사용](using-wpf-controls.md)
- [Visual Studio에서 XAML 디자인](/visualstudio/designers/designing-xaml-in-visual-studio)
