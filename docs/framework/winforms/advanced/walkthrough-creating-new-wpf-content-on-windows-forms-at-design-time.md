---
title: '연습: 디자인 타임에 Windows Forms에서 새 WPF 콘텐츠 만들기'
ms.date: 08/18/2018
helpviewer_keywords:
- interoperability [Windows Forms], WPF and Windows Forms
- WPF content [Windows Forms], hosting in Windows Forms
- hosting WPF content in Windows Forms
- ElementHost control
- WPF user control [Windows Forms], hosting in Windows Forms
ms.assetid: 2e92d8e8-f0e4-4df7-9f07-2acf35cd798c
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 5e5112aa0b025648ce68a93f0f3da026ec99fe89
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69987142"
---
# <a name="walkthrough-create-new-wpf-content-on-windows-forms-at-design-time"></a>연습: 디자인 타임에 Windows Forms에서 새 WPF 콘텐츠 만들기

이 문서에서는 Windows Forms 기반 응용 프로그램에서 사용할 WPF (Windows Presentation Foundation) 컨트롤을 만드는 방법을 보여 줍니다.

## <a name="prerequisites"></a>전제 조건

이 연습을 완료하려면 Visual Studio가 필요합니다.

## <a name="create-the-project"></a>프로젝트를 만듭니다.

Visual Studio를 열고 Visual Basic 또는 시각적 개체 C# `HostingWpf`에 새 **Windows Forms 앱 (.NET Framework)** 프로젝트를 만듭니다.

> [!NOTE]
> WPF 콘텐츠를 호스트하는 경우 C# 및 Visual Basic 프로젝트만 지원됩니다.

## <a name="create-a-new-wpf-control"></a>새 WPF 컨트롤 만들기

새 WPF 컨트롤을 만들고 프로젝트에 추가하는 작업은 다른 항목을 프로젝트에 추가하는 것만큼 쉽습니다. Windows Forms 디자이너은 *복합 컨트롤*또는 *사용자 정의*컨트롤 이라는 특정 종류의 컨트롤에서 작동 합니다. WPF 사용자 정의 컨트롤에 대한 자세한 내용은 <xref:System.Windows.Controls.UserControl>을 참조하세요.

> [!NOTE]
> WPF용 <xref:System.Windows.Controls.UserControl?displayProperty=nameWithType> 형식은 Windows Forms에서 제공하는 <xref:System.Windows.Forms.UserControl?displayProperty=nameWithType>이라는 사용자 정의 컨트롤 형식과 별개입니다.

새 WPF 컨트롤을 만들려면 다음을 수행 합니다.

1. **솔루션 탐색기**에서 새 **WPF 사용자 정의 컨트롤 라이브러리 (.NET Framework)** 프로젝트를 솔루션에 추가 합니다. 컨트롤 라이브러리의 기본 이름인 `WpfControlLibrary1`을 사용합니다. 기본 컨트롤 이름은 `UserControl1.xaml`입니다.

   새 컨트롤을 추가 하면 다음과 같은 결과가 나타납니다.

   - UserControl1.xaml 파일이 추가됩니다.

   - UserControl1.xaml.cs (또는 UserControl1) 파일이 추가 됩니다. 이 파일에는 이벤트 처리기 및 기타 구현에 대한 코드 숨김이 포함됩니다.

   - WPF 어셈블리에 대한 참조가 추가됩니다.

   - 파일 UserControl1은 Visual Studio 용 WPF 디자이너에서 열립니다.

2. 디자인 뷰에서 `UserControl1`이 선택되었는지 확인합니다.

3. **속성** 창에서 <xref:System.Windows.FrameworkElement.Width%2A> 및 <xref:System.Windows.FrameworkElement.Height%2A> 속성의 값을 **200**로 설정 합니다.

4. **도구 상자**에서 컨트롤을 <xref:System.Windows.Controls.TextBox?displayProperty=nameWithType> 디자인 화면으로 끌어 옵니다.

5. **속성** 창에서 <xref:System.Windows.Controls.TextBox.Text%2A> 속성의 값을 **Hosted Content**로 설정 합니다.

   > [!NOTE]
   > 일반적으로 더 복잡한 WPF 콘텐츠를 호스트해야 합니다. <xref:System.Windows.Controls.TextBox?displayProperty=nameWithType> 컨트롤은 여기서 설명 목적으로만 사용됩니다.

6. 프로젝트를 빌드합니다.

## <a name="add-a-wpf-control-to-a-windows-form"></a>Windows Form에 WPF 컨트롤 추가

폼에서 새 WPF 컨트롤을 사용할 준비가 되었습니다. Windows Forms는 <xref:System.Windows.Forms.Integration.ElementHost> 컨트롤을 사용 하 여 WPF 콘텐츠를 호스팅합니다.

Windows Form에 WPF 컨트롤을 추가 하려면 다음을 수행 합니다.

1. Windows Forms 디자이너에서 `Form1`을 엽니다.

2. **도구 상자**에서 **WPFUserControlLibrary WPF User Controls**이라는 레이블이 지정 된 탭을 찾습니다.

3. `UserControl1` 인스턴스를 폼으로 끕니다.

    - WPF 컨트롤을 호스트할 폼에 <xref:System.Windows.Forms.Integration.ElementHost> 컨트롤이 자동으로 만들어집니다.

    - 컨트롤 <xref:System.Windows.Forms.Integration.ElementHost> `elementHost1` 의 이름이이 고 **속성** 창에서 해당 <xref:System.Windows.Forms.Integration.ElementHost.Child%2A> 속성이 **UserControl1**로 설정 된 것을 볼 수 있습니다.

    - WPF 어셈블리에 대한 참조가 프로젝트에 추가됩니다.

    - `elementHost1` 컨트롤에는 사용 가능한 호스팅 옵션을 표시하는 스마트 태그 패널이 있습니다.

4. **ElementHost Tasks** 스마트 태그 패널에서 **부모 컨테이너에서 도킹**을 선택 합니다.

5. **F5** 키를 눌러 응용 프로그램을 빌드하고 실행합니다.

## <a name="next-steps"></a>다음 단계

Windows Forms와 WPF는 서로 다른 기술이지만 긴밀하게 상호 운용하도록 설계되었습니다. 응용 프로그램에서 다양 한 모양과 동작을 제공 하려면 다음을 시도 합니다.

- WPF 페이지에서 Windows Forms 컨트롤을 호스트합니다. 자세한 내용은 [연습: WPF](../../wpf/advanced/walkthrough-hosting-a-windows-forms-control-in-wpf.md)에서 Windows Forms 컨트롤 호스팅.

- WPF 콘텐츠에 Windows Forms 시각적 스타일을 적용합니다. 자세한 내용은 [방법: 하이브리드 응용 프로그램](../../wpf/advanced/how-to-enable-visual-styles-in-a-hybrid-application.md)에서 비주얼 스타일을 사용 하도록 설정 합니다.

- WPF 콘텐츠의 스타일을 변경합니다. 자세한 내용은 [연습: WPF 콘텐츠](walkthrough-styling-wpf-content.md)스타일 지정

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [마이그레이션 및 상호 운용성](../../wpf/advanced/migration-and-interoperability.md)
- [WPF 컨트롤 사용](using-wpf-controls.md)
- [Visual Studio에서 XAML 디자인](/visualstudio/designers/designing-xaml-in-visual-studio)
