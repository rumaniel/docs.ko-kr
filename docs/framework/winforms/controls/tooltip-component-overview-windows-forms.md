---
title: ToolTip 구성 요소 개요(Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- ToolTip
helpviewer_keywords:
- tooltips [Windows Forms], about tooltips
- ToolTip component [Windows Forms], about ToolTip component
ms.assetid: 3fbc6f08-c882-4acd-a960-a08efe3c7e6e
ms.openlocfilehash: 3fbe883501d1ce36ca25ea07631f98042f451e07
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62009337"
---
# <a name="tooltip-component-overview-windows-forms"></a>ToolTip 구성 요소 개요(Windows Forms)
Windows Forms <xref:System.Windows.Forms.ToolTip> 구성 요소는 사용자가 컨트롤을 가리킬 때 텍스트를 표시합니다. 도구 설명은 모든 컨트롤에 연결될 수 있습니다. 이 구성 요소의 사용 예: 폼에 공간을 절약 하기 단추에 작은 아이콘을 표시 하 도구 설명을 사용 하 여 단추의 기능을 설명 합니다.  
  
## <a name="working-with-the-tooltip-component"></a>ToolTip 구성 요소를 사용 하 여 작업  
 A <xref:System.Windows.Forms.ToolTip> 구성 요소를 제공는 `ToolTip` Windows 폼 또는 다른 컨테이너에 여러 컨트롤에 속성입니다. 예를 들어, 하나를 배치 하는 경우 <xref:System.Windows.Forms.ToolTip> 양식의 구성 요소에 대 한 "여기에 이름을 입력"을 표시할 수 있습니다를 <xref:System.Windows.Forms.TextBox> 제어 하 고 "여기를 클릭 변경 내용을 저장 하려면"을 <xref:System.Windows.Forms.Button> 컨트롤입니다.  
  
 주요 메서드는 <xref:System.Windows.Forms.ToolTip> 구성 요소는 <xref:System.Windows.Forms.ToolTip.SetToolTip%2A> 고 <xref:System.Windows.Forms.ToolTip.GetToolTip%2A>입니다. 사용할 수는 <xref:System.Windows.Forms.ToolTip.SetToolTip%2A> 컨트롤에 대해 표시할 도구 설명을 설정 하는 방법입니다. 자세한 내용은 [방법: 디자인 타임에 Windows Form의 컨트롤에 도구 설명 설정](how-to-set-tooltips-for-controls-on-a-windows-form-at-design-time.md)합니다. 키 속성은 <xref:System.Windows.Forms.ToolTip.Active%2A>로 설정 되어야 합니다 `true` 도구 설명에 표시 및 <xref:System.Windows.Forms.ToolTip.AutomaticDelay%2A>도구 설명 문자열 표시 되는 시간의 길이 설정 하는, 사용자 표시 도구 설명 컨트롤에 얼마나 오래 가리켜야 하는 방법과 시간 다음 도구 설명 창이 표시 됩니다. 자세한 내용은 [방법: Windows Forms ToolTip 구성 요소의 지연 변경](how-to-change-the-delay-of-the-windows-forms-tooltip-component.md)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ToolTip>
- [방법: 디자인 타임에 Windows Form의 컨트롤에 도구 설명 설정](how-to-set-tooltips-for-controls-on-a-windows-form-at-design-time.md)
- [방법: Windows Forms ToolTip 구성 요소의 지연 변경](how-to-change-the-delay-of-the-windows-forms-tooltip-component.md)
