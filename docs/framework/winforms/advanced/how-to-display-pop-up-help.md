---
title: '방법: 팝업 도움말 표시'
ms.date: 03/30/2017
helpviewer_keywords:
- pop-up Help
- Help [Windows Forms], pop-up Help
- Windows Forms, displaying Help
- forms [Windows Forms], displaying Help
- modal dialog boxes [Windows Forms], pop-up Help
- F1 Help [Windows Forms], in dialog boxes
- HelpProvider component [Windows Forms]
- Help [Windows Forms], adding to dialog boxes
ms.assetid: 218aa81e-e87e-4d67-af05-11627bbdce3b
ms.openlocfilehash: bf3bcbff0cd6f3bbf71e96e748cb170d5ce68dfc
ms.sourcegitcommit: 0d0a6e96737dfe24d3257b7c94f25d9500f383ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65211409"
---
# <a name="how-to-display-pop-up-help"></a>방법: 팝업 도움말 표시

통해 Windows Forms에 도움말을 표시 하는 한 가지 방법은는 **도움말** 단추를 통해 액세스할 수 있는 제목 표시줄의 오른쪽에 있는 <xref:System.Windows.Forms.Form.HelpButton%2A> 속성입니다. 이 도움말 표시 유형은 대화 상자에서 사용하기에 적합합니다. 모달 대화 상자를 먼저 닫아야 다른 창으로 포커스를 이동할 수 있으므로 모달 형식으로 표시되는 대화 상자(<xref:System.Windows.Forms.Form.ShowDialog%2A> 메서드 사용)에서 외부 도움말 시스템을 가져오려면 문제가 발생합니다. 또한 사용 하 여는 **도움말** 단추는 필요 없습니다 **최소화** 단추 또는 **최대화** 단추가 제목 표시줄에 표시 합니다. 이 표준 대화 상자 규칙, 일반적으로 폼에는 있지만 **최소화** 하 고 **최대화** 단추입니다.

사용할 수도 있습니다는 <xref:System.Windows.Forms.HelpProvider> 팝업 도움말을 구현한 경우에 파일에 컨트롤을 도움말 시스템에서 연결 하려면 구성 요소입니다. 자세한 내용은 [는 Windows 응용 프로그램에서 도움말 제공](how-to-provide-help-in-a-windows-application.md)합니다.

## <a name="display-pop-up-help"></a>팝업 도움말 표시

1. Visual Studio에서 끌어를 [HelpProvider](../controls/helpprovider-component-windows-forms.md) 폼에 도구 상자에서 구성 요소입니다.

   Windows Forms 디자이너 아래쪽의 트레이에 배치됩니다.

2. 속성 창에서 <xref:System.Windows.Forms.Form.HelpButton%2A> 속성을 `true`로 설정합니다. 그러면 폼의 제목 표시줄 오른쪽에 물음표가 있는 단추가 표시됩니다.

3. <xref:System.Windows.Forms.Form.HelpButton%2A>이 표시되려면 폼의 <xref:System.Windows.Forms.Form.MinimizeBox%2A> 및 <xref:System.Windows.Forms.Form.MaximizeBox%2A> 속성을 `false`로 설정하고 <xref:System.Windows.Forms.Form.ControlBox%2A> 속성을 `true`로 설정하고 <xref:System.Windows.Forms.Form.FormBorderStyle%2A> 속성을 <xref:System.Windows.Forms.FormBorderStyle.FixedSingle>, <xref:System.Windows.Forms.FormBorderStyle.Fixed3D>, <xref:System.Windows.Forms.FormBorderStyle.FixedDialog> 또는 <xref:System.Windows.Forms.FormBorderStyle.Sizable> 값 중 하나로 설정해야 합니다.

4. 폼에서 도움말을 표시할 컨트롤을 선택하고 속성 창에서 도움말 문자열을 설정합니다. 비슷하게 창에 표시 되는 텍스트 문자열이 며이 [ToolTip](../controls/tooltip-component-windows-forms.md)합니다.

5. **F5**키를 누릅니다.

6. 키를 눌러 합니다 **도움말** 제목 표시줄에 단추 및 도움말 문자열을 설정 하는 컨트롤을 클릭 합니다.

## <a name="see-also"></a>참고자료

- [ToolTip을 사용한 컨트롤 도움말](control-help-using-tooltips.md)
- [Windows Forms에 사용자 도움말 통합](integrating-user-help-in-windows-forms.md)
- [Windows Forms](../index.md)
