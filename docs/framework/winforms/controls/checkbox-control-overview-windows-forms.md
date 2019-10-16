---
title: CheckBox 컨트롤 개요(Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- CheckBox
helpviewer_keywords:
- CheckBox control [Windows Forms], about CheckBox control
- data binding [Windows Forms], checkbox controls
- check boxes [Windows Forms], about check boxes
ms.assetid: 085a4e0b-9046-473f-b141-d0edddfb2ebb
ms.openlocfilehash: 2a18327d9836d1dbbcd5d5d6e73f217637736d20
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61938972"
---
# <a name="checkbox-control-overview-windows-forms"></a>CheckBox 컨트롤 개요(Windows Forms)
Windows Forms <xref:System.Windows.Forms.CheckBox> 컨트롤은 특정 조건이 설정 또는 해제되었는지를 나타냅니다. 일반적으로 예/아니요 또는 True/False 선택을 사용자에게 제공하는 데 사용됩니다. 확인란 컨트롤을 그룹으로 사용하여 사용자가 하나 이상 선택할 수 있는 여러 선택 항목을 표시할 수 있습니다.  
  
 확인란 컨트롤에는 사용자가 구성 된 선택 영역을 나타내는 데 사용 되는 각 라디오 단추 컨트롤와 비슷합니다. 한 번에 하나의 라디오 단추 그룹을 선택할 수 있습니다는 다릅니다. 확인란 컨트롤에 임의 개수의 확인란을 선택할 수 있습니다.  
  
 확인란을 단순 데이터 바인딩을 사용 하 여 데이터베이스의 요소에 연결할 수 있습니다. 사용 하 여 여러 확인란을 그룹화 할 수 있습니다는 <xref:System.Windows.Forms.GroupBox> 제어 합니다. 이 시각적 모양에 대 한 및 사용자 인터페이스 디자인에 대 한 그룹화 된 컨트롤 이동할 수 있습니다 함께 폼 디자이너에 있습니다. 자세한 내용은 [Windows Forms 데이터 바인딩](../windows-forms-data-binding.md) 하 고 [GroupBox 컨트롤](groupbox-control-windows-forms.md)합니다.  
  
 합니다 <xref:System.Windows.Forms.CheckBox> 컨트롤에 두 개의 중요 한 속성인 <xref:System.Windows.Forms.CheckBox.Checked%2A> 및 <xref:System.Windows.Forms.CheckBox.CheckState%2A>합니다. 합니다 <xref:System.Windows.Forms.CheckBox.Checked%2A> 속성 중 하나를 반환 합니다. `true` 또는 `false`합니다. <xref:System.Windows.Forms.CheckBox.CheckState%2A> 속성 중 하나를 반환 합니다. <xref:System.Windows.Forms.CheckState.Checked> 또는 <xref:System.Windows.Forms.CheckState.Unchecked>; 또는 합니다 <xref:System.Windows.Forms.CheckBox.ThreeState%2A> 속성이로 설정 되어 `true`, <xref:System.Windows.Forms.CheckBox.CheckState%2A> 반환할 수도 있습니다. <xref:System.Windows.Forms.CheckState.Indeterminate>합니다. 비활성화 된 상태의 상자를 나타내는 옵션을 사용할 수 없는 흐리게 모양으로 표시 됩니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.CheckBox>
- [방법: Windows Forms CheckBox 컨트롤을 사용 하 여 옵션 설정](how-to-set-options-with-windows-forms-checkbox-controls.md)
- [방법: Windows Forms CheckBox 클릭에 응답](how-to-respond-to-windows-forms-checkbox-clicks.md)
- [CheckBox 컨트롤](checkbox-control-windows-forms.md)
