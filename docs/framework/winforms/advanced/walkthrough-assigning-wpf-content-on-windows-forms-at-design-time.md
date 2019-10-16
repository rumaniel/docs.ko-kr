---
title: '연습: 디자인 타임에 Windows Forms에서 WPF 콘텐츠 할당'
ms.date: 03/30/2017
helpviewer_keywords:
- WPF content [Windows Forms], assigning at design time
- ElementHost control [Windows Forms], assigning WPF content at design time
- interoperability [WPF]
- Windows Forms, content assignments
- WPF user control [Windows Forms], hosting in Windows Forms
ms.assetid: b3e9ef93-7e0f-4a2f-8f1e-3437609a1eb7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: bc5f5e2d8808c0a60df721bf2c0ed76b45ef49a0
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69666254"
---
# <a name="walkthrough-assign-wpf-content-on-windows-forms-at-design-time"></a>연습: 디자인 타임에 Windows Forms에 WPF 콘텐츠 할당

이 문서에서는 폼에 표시 하려는 Windows Presentation Foundation (WPF) 컨트롤 형식을 선택 하는 방법을 보여 줍니다. 프로젝트에 포함된 모든 WPF 컨트롤 형식을 선택할 수 있습니다.

## <a name="prerequisites"></a>필수 구성 요소

이 연습을 완료하려면 Visual Studio가 필요합니다.

## <a name="create-the-project"></a>프로젝트를 만듭니다.

Visual Studio를 열고 Visual Basic 또는 시각적 개체 C# `SelectingWpfContent`에 새 Windows Forms 응용 프로그램 프로젝트를 만듭니다.

> [!NOTE]
> WPF 콘텐츠를 호스트하는 경우 C# 및 Visual Basic 프로젝트만 지원됩니다.

## <a name="create-the-wpf-control-types"></a>WPF 컨트롤 형식 만들기

프로젝트에 WPF 컨트롤 형식을 추가한 후 다양한 <xref:System.Windows.Forms.Integration.ElementHost> 컨트롤에서 호스트할 수 있습니다.

1. 새 WPF <xref:System.Windows.Controls.UserControl> 프로젝트를 솔루션에 추가합니다. 컨트롤 형식의 기본 이름인 `UserControl1.xaml`을 사용합니다. 자세한 내용은 [연습: 디자인 타임](walkthrough-creating-new-wpf-content-on-windows-forms-at-design-time.md)에 WINDOWS FORMS에서 새 WPF 콘텐츠 만들기

2. 디자인 뷰에서 `UserControl1`이 선택되었는지 확인합니다.

3. **속성** 창에서 <xref:System.Windows.FrameworkElement.Width%2A> 및 <xref:System.Windows.FrameworkElement.Height%2A> 속성의 값을 **200**로 설정 합니다.

4. 에 컨트롤 <xref:System.Windows.Controls.TextBox?displayProperty=nameWithType> 을 추가 <xref:System.Windows.Controls.TextBox.Text%2A> 하 고속성값을HostedContent<xref:System.Windows.Controls.UserControl> 로 설정합니다.

5. 프로젝트에 두 번째 WPF <xref:System.Windows.Controls.UserControl>을 추가합니다. 컨트롤 형식의 기본 이름인 `UserControl2.xaml`을 사용합니다.

6. **속성** 창에서 <xref:System.Windows.FrameworkElement.Width%2A> 및 <xref:System.Windows.FrameworkElement.Height%2A> 속성의 값을 **200**로 설정 합니다.

7. 에 컨트롤 <xref:System.Windows.Controls.TextBox?displayProperty=nameWithType> 을 추가 <xref:System.Windows.Controls.TextBox.Text%2A> 하 고속성의값을HostedContent2<xref:System.Windows.Controls.UserControl> 로 설정 합니다.

   > [!NOTE]
   > 일반적으로 더 복잡한 WPF 콘텐츠를 호스트해야 합니다. <xref:System.Windows.Controls.TextBox?displayProperty=nameWithType> 컨트롤은 여기서 설명 목적으로만 사용됩니다.

8. 프로젝트를 빌드합니다.

## <a name="select-wpf-controls"></a>WPF 컨트롤 선택

이미 콘텐츠를 호스트하고 있는 <xref:System.Windows.Forms.Integration.ElementHost> 컨트롤에 다른 WPF 콘텐츠를 할당할 수 있습니다.

1. Windows Forms 디자이너에서 `Form1`을 엽니다.

2. **도구 상자**에서을 두 번 클릭 `UserControl1` 하 여 폼에서의 `UserControl1` 인스턴스를 만듭니다.

   `UserControl1` 인스턴스가 `elementHost1`이라는 새 <xref:System.Windows.Forms.Integration.ElementHost> 컨트롤에서 호스트됩니다.

3. 에 대 한 `elementHost1`스마트 태그 패널에서 호스트 된 **콘텐츠 선택** 드롭다운 목록을 엽니다.

4. 드롭다운 목록 상자에서 **UserControl2** 를 선택 합니다.

   이제 `elementHost1` 컨트롤이 `UserControl2` 형식의 인스턴스를 호스트합니다.

5. 속성 창 에서 <xref:System.Windows.Forms.Integration.ElementHost.Child%2A> 속성이 **UserControl2**로 설정 되어 있는지 확인 합니다.

6. **도구 상자**의 **WPF 상호 운용성** 그룹에서 <xref:System.Windows.Forms.Integration.ElementHost> 컨트롤을 폼으로 끌어옵니다.

   새 컨트롤의 기본 이름은 `elementHost2`입니다.

7. 에 대 한 `elementHost2`스마트 태그 패널에서 호스트 된 **콘텐츠 선택** 드롭다운 목록을 엽니다.

8. 드롭다운 목록에서 **UserControl1** 을 선택 합니다.

9. 이제 `elementHost2` 컨트롤이 `UserControl1` 형식의 인스턴스를 호스트합니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [마이그레이션 및 상호 운용성](../../wpf/advanced/migration-and-interoperability.md)
- [WPF 컨트롤 사용](using-wpf-controls.md)
- [Visual Studio에서 XAML 디자인](/visualstudio/designers/designing-xaml-in-visual-studio)
