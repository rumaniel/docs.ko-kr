---
title: StatusBar 컨트롤 개요(Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- StatusBar
helpviewer_keywords:
- StatusBar control [Windows Forms], about StatusBar control
- status bars
ms.assetid: b7b9852c-633d-4416-bb2e-94852b989c6c
ms.openlocfilehash: bd58d4c70e3a3c88e57fe242957f669d1944fd71
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69964432"
---
# <a name="statusbar-control-overview-windows-forms"></a>StatusBar 컨트롤 개요(Windows Forms)
> [!IMPORTANT]
> 및 <xref:System.Windows.Forms.StatusStrip> <xref:System.Windows.Forms.StatusBar> <xref:System.Windows.Forms.StatusBarPanel> <xref:System.Windows.Forms.StatusBar> 컨트롤은를 대체 하 고 및 <xref:System.Windows.Forms.StatusBarPanel> 컨트롤에 기능을 추가 합니다. 그러나 및 컨트롤은 이전 버전과의 호환성 및 향후 사용을 위해 유지 됩니다. <xref:System.Windows.Forms.ToolStripStatusLabel> 선택.  
  
 Windows Forms [StatusBar 컨트롤](statusbar-control-windows-forms.md) 은 폼에서 주로 창의 맨 아래에 표시 되는 영역으로 사용 됩니다 .이 영역에서 응용 프로그램은 다양 한 종류의 상태 정보를 표시할 수 있습니다. <xref:System.Windows.Forms.StatusBar>컨트롤에는 상태를 나타내는 텍스트 또는 아이콘을 표시 하는 상태 표시줄 패널 또는 프로세스가 작동 하는 애니메이션의 일련의 아이콘이 있을 수 있습니다. 예를 들어 Microsoft Word에서 문서를 저장 하 고 있음을 나타냅니다.  
  
## <a name="using-the-statusbar-control"></a>StatusBar 컨트롤 사용  
 Internet Explorer는 마우스를 하이퍼링크 위로 가져갈 때 상태 표시줄을 사용 하 여 페이지의 URL을 표시 합니다. Microsoft Word는 페이지 위치, 섹션 위치 및 겹쳐쓰기 및 수정 내용 추적과 같은 편집 모드에 대 한 정보를 제공 합니다. 및 Visual Studio는 상태 표시줄을 사용 하 여 도킹 된 창을 도킹 또는 부동으로 조작 하는 방법을 설명 하는 등 상황에 맞는 정보를 제공 합니다.  
  
 <xref:System.Windows.Forms.StatusBar.ShowPanels%2A> 속성을 `false` (<xref:System.Windows.Forms.StatusBar.Text%2A> 기본값)으로 설정 하 고 상태 표시줄의 속성을 상태 표시줄에 표시할 텍스트로 설정 하 여 상태 표시줄에 단일 메시지를 표시할 수 있습니다. <xref:System.Windows.Forms.StatusBar.ShowPanels%2A> 속성을로 `true` 설정 하 고의 <xref:System.Windows.Forms.StatusBar.StatusBarPanelCollection.Add%2A> <xref:System.Windows.Forms.StatusBar.StatusBarPanelCollection>메서드를 사용 하 여 여러 유형의 정보를 표시 하도록 상태 표시줄을 패널로 나눌 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.StatusBar>
- <xref:System.Windows.Forms.ToolStripStatusLabel>
- [방법: Windows Forms StatusBar 컨트롤에서 클릭 한 패널 확인](determine-which-panel-wf-statusbar-control-was-clicked.md)
