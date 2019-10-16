---
title: RadioButton 컨트롤 개요(Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- RadioButton
helpviewer_keywords:
- RadioButton control [Windows Forms], about RadioButton control
- RadioButton control [Windows Forms], determining state
- radio buttons [Windows Forms], determining state
- radio buttons [Windows Forms], about radio buttons
ms.assetid: cd11f0c2-d098-4022-adf9-1455bc166a13
ms.openlocfilehash: 1210658226d9bcacbf4904fdc90a9908c34f5b73
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61755950"
---
# <a name="radiobutton-control-overview-windows-forms"></a>RadioButton 컨트롤 개요(Windows Forms)
Windows Forms <xref:System.Windows.Forms.RadioButton> 컨트롤 사용자에 게 둘 이상의 상호 배타적인 옵션 집합을 제공 합니다. 중요 한 차이점이 있기 라디오 단추 및 확인란 마찬가지로 함수에 나타날 수 있습니다 하는 동안: 동일한 그룹의 다른 라디오 단추가 사용자가 라디오 단추를 선택 하면도 선택할 수 없습니다. 반면에 임의 개수의 확인란을 선택할 수 있습니다. 라디오 단추 그룹을 사용자 지정, "Here is 집합을 하나만 선택할 수 있습니다."  
  
## <a name="using-the-control"></a>컨트롤 사용  
 경우는 <xref:System.Windows.Forms.RadioButton> 컨트롤을 클릭할 해당 <xref:System.Windows.Forms.RadioButton.Checked%2A> 속성이 `true` 및 <xref:System.Windows.Forms.Control.Click> 이벤트 처리기가 호출 됩니다. <xref:System.Windows.Forms.RadioButton.CheckedChanged> 이벤트는 때의 값을 <xref:System.Windows.Forms.RadioButton.Checked%2A> 속성 변경. 경우는 <xref:System.Windows.Forms.RadioButton.AutoCheck%2A> 속성이 `true` (기본값) 라디오 단추를 선택한 경우 그룹의 다른 모든 자동으로 지워집니다. 이 속성은 대개로 `false` 되도록 라디오 단추를 선택 하 여 유효성 검사 코드를 사용 하는 경우 허용 되는 옵션입니다. 으로 설정 된 컨트롤에 표시 되는 텍스트는 <xref:System.Windows.Forms.Control.Text%2A> 속성에 대 한 액세스를 바로 가기 키를 포함할 수 있습니다. 액세스 키를 통해 컨트롤을 액세스 키를 사용 하 여 ALT 키를 눌러 "클릭" 할 수 있습니다. 자세한 내용은 [방법: Windows Forms 컨트롤에 대 한 액세스 키를 만듭니다](how-to-create-access-keys-for-windows-forms-controls.md) 고 [방법: 설정 하 여 표시 되는 텍스트는 Windows Forms 컨트롤](how-to-set-the-text-displayed-by-a-windows-forms-control.md)합니다.  
  
 <xref:System.Windows.Forms.RadioButton> 제어 경우 눌러진을 선택 된 것으로 표시 되는 명령 단추 처럼 나타날 수 있습니다 합니다 <xref:System.Windows.Forms.RadioButton.Appearance%2A> 속성이 <xref:System.Windows.Forms.Appearance.Button>합니다. 라디오 단추를 사용 하 여 이미지를 표시할 수도 있습니다는 <xref:System.Windows.Forms.ButtonBase.Image%2A> 고 <xref:System.Windows.Forms.ButtonBase.ImageList%2A> 속성입니다. 자세한 내용은 [방법: 설정 하 여 표시 되는 이미지를 Windows Forms 컨트롤](how-to-set-the-image-displayed-by-a-windows-forms-control.md)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.RadioButton>
- [Panel 컨트롤 개요](panel-control-overview-windows-forms.md)
- [GroupBox 컨트롤 개요](groupbox-control-overview-windows-forms.md)
- [CheckBox 컨트롤 개요](checkbox-control-overview-windows-forms.md)
- [방법: Windows Forms 컨트롤에 대 한 액세스 키 만들기](how-to-create-access-keys-for-windows-forms-controls.md)
- [방법: 설정 하 여 표시 되는 텍스트는 Windows Forms 컨트롤](how-to-set-the-text-displayed-by-a-windows-forms-control.md)
- [방법: 함수 집합으로 그룹 Windows Forms RadioButton 컨트롤](how-to-group-windows-forms-radiobutton-controls-to-function-as-a-set.md)
- [RadioButton 컨트롤](radiobutton-control-windows-forms.md)
