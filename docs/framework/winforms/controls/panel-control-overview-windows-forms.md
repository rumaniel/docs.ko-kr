---
title: Panel 컨트롤 개요(Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- Panel
helpviewer_keywords:
- grouping controls [Windows Forms], Panel control
- Panel control [Windows Forms], about Panel control
ms.assetid: b6b83636-2c39-4dad-89d6-f0fa41049a74
ms.openlocfilehash: d4976b3725d04162ac10242c486f57c4d2598769
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62012687"
---
# <a name="panel-control-overview-windows-forms"></a>Panel 컨트롤 개요(Windows Forms)
Windows Forms <xref:System.Windows.Forms.Panel> 컨트롤은 다른 컨트롤에 대 한 식별 가능한 그룹화를 제공 하는 데 사용 됩니다. 일반적으로 폼 함수로 세분화 하기 패널을 사용 합니다. 예를 들어, 어떤 야간 운송 같은 메일 옵션을 지정 하는 주문 양식과 할 수 있습니다. 그룹화는 패널에서 모든 옵션 논리 시각적 표시를 제공 합니다. 디자인 타임에 컨트롤을 쉽게 이동할 수 있습니다. 모든-이동 하는 경우는 <xref:System.Windows.Forms.Panel> 모든 포함 된 컨트롤이, 너무 제어 합니다. 패널에 그룹화 된 컨트롤을 통해 액세스할 수 있습니다 해당 <xref:System.Windows.Forms.Control.Controls%2A> 속성입니다. 이 속성의 컬렉션을 반환 <xref:System.Windows.Forms.Control> 되므로 일반적으로 컨트롤을 캐스팅 해야 경우 해당 특정 형식에 이러한 방식으로 검색 합니다.  
  
## <a name="panel-versus-groupbox"></a>GroupBox 및 패널  
 그러나 <xref:System.Windows.Forms.Panel> 제어는 비슷합니다는 <xref:System.Windows.Forms.GroupBox> 컨트롤만 합니다 <xref:System.Windows.Forms.Panel> 컨트롤에서 스크롤 막대를 가질 수 있습니다만 <xref:System.Windows.Forms.GroupBox> 컨트롤 캡션을 표시 합니다.  
  
## <a name="key-properties"></a>키 속성  
 스크롤 막대를 표시 하려면 설정 합니다 <xref:System.Windows.Forms.ScrollableControl.AutoScroll%2A> 속성을 `true`입니다. 설정 하 여 패널의 모양을 사용자 지정할 수도 있습니다는 <xref:System.Windows.Forms.Control.BackColor%2A>, <xref:System.Windows.Forms.Control.BackgroundImage%2A>, 및 <xref:System.Windows.Forms.Panel.BorderStyle%2A> 속성입니다. 에 대 한 자세한 합니다 <xref:System.Windows.Forms.Control.BackColor%2A> 하 고 <xref:System.Windows.Forms.Control.BackgroundImage%2A> 속성을 참조 하세요 [방법: 패널의 배경 설정](how-to-set-the-background-of-a-windows-forms-panel.md)합니다. 합니다 <xref:System.Windows.Forms.Panel.BorderStyle%2A> 속성 패널에 테두리가 표시 되지를 사용 하 여 설명 된 경우를 결정 (<xref:System.Windows.Forms.BorderStyle.None>), 일반 줄 (<xref:System.Windows.Forms.BorderStyle.FixedSingle>), 또는 숨겨진된 줄 (<xref:System.Windows.Forms.BorderStyle.Fixed3D>).  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.Panel>
- [GroupBox 컨트롤](groupbox-control-windows-forms.md)
- [방법: 디자이너를 사용 하 여 Windows Forms 패널 컨트롤을 사용 하 여 그룹 컨트롤](group-controls-with-wf-panel-control-using-the-designer.md)
- [방법: 디자이너를 사용 하 여 Windows Forms 패널의 배경 설정](how-to-set-the-background-of-a-windows-forms-panel-using-the-designer.md)
