---
title: '방법: 디자인 타임에 ElementHost 컨트롤 복사 및 붙여넣기'
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Forms, content copying and pasting
- interoperability [WPF]
- ElementHost control [Windows Forms], copying and pasting at design time
- WPF user control [Windows Forms], hosting in Windows Forms
ms.assetid: e570375d-2a68-44ba-b4f7-c781af2d20e8
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: dfe5244e0c5b61fdf6d940dd16d8c280f013b12c
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69666175"
---
# <a name="how-to-copy-and-paste-an-elementhost-control"></a>방법: ElementHost 컨트롤 복사 및 붙여넣기

이 절차에서는 Visual Studio에서 Windows Form에 Windows Presentation Foundation (WPF) 컨트롤을 복사 하는 방법을 보여 줍니다.

1. Visual Studio에서 Windows Forms 프로젝트에 새 WPF <xref:System.Windows.Controls.UserControl> 를 추가 합니다. 컨트롤 형식의 기본 이름인 `UserControl1.xaml`을 사용합니다. 자세한 내용은 [연습: 디자인 타임](walkthrough-creating-new-wpf-content-on-windows-forms-at-design-time.md)에 WINDOWS FORMS에서 새 WPF 콘텐츠 만들기

2. **속성** 창 <xref:System.Windows.FrameworkElement.Width%2A> 에서의 <xref:System.Windows.FrameworkElement.Height%2A> 및`UserControl1` 속성 값을 **200**로 설정 합니다.

3. <xref:System.Windows.Controls.Control.Background%2A> 속성의 값을 **Blue**로 설정 합니다.

4. 프로젝트를 빌드합니다.

5. Windows Forms 디자이너에서 `Form1`을 엽니다.

6. **도구 상자**에서의 `UserControl1` 인스턴스를 폼으로 끌어 옵니다.

   `UserControl1` 인스턴스가 `elementHost1`이라는 새 <xref:System.Windows.Forms.Integration.ElementHost> 컨트롤에서 호스트됩니다.

7. 선택 `elementHost1` 된 상태에서 **Ctrl**+**C** 를 눌러 클립보드로 복사 합니다.

8. **Ctrl**+**V** 를 눌러 복사 된 컨트롤을 폼에 붙여넣습니다.

   <xref:System.Windows.Forms.Integration.ElementHost> 이라는`elementHost2` 새 컨트롤이 폼에 만들어집니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [마이그레이션 및 상호 운용성](../../wpf/advanced/migration-and-interoperability.md)
- [WPF 컨트롤 사용](using-wpf-controls.md)
- [Visual Studio에서 XAML 디자인](/visualstudio/designers/designing-xaml-in-visual-studio)
