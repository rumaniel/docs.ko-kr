---
title: StatusStrip 컨트롤 개요
ms.date: 03/30/2017
f1_keywords:
- StatusStrip
helpviewer_keywords:
- StatusStrip control [Windows Forms], about StatusStrip control
- status bars [Windows Forms], about status bars
ms.assetid: c0d9bcbb-f8b8-46ef-bae2-4146b8c8ce99
ms.openlocfilehash: f6f2d4b19b7ec91c964c72e3aca85e0253c7cc22
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62009645"
---
# <a name="statusstrip-control-overview"></a>StatusStrip 컨트롤 개요
<xref:System.Windows.Forms.StatusStrip> 컨트롤은 <xref:System.Windows.Forms.Form>에 표시되는 개체, 개체의 구성 요소 또는 응용 프로그램 내에서 해당 개체의 작업과 관련된 컨텍스트 정보에 대한 정보를 표시합니다. 일반적으로 <xref:System.Windows.Forms.StatusStrip> 컨트롤은 각각 텍스트, 아이콘 또는 둘 다를 표시하는 <xref:System.Windows.Forms.ToolStripStatusLabel> 개체로 구성됩니다. <xref:System.Windows.Forms.StatusStrip>에 <xref:System.Windows.Forms.ToolStripDropDownButton>, <xref:System.Windows.Forms.ToolStripSplitButton> 및 <xref:System.Windows.Forms.ToolStripProgressBar> 컨트롤이 포함될 수도 있습니다.  
  
 기본 <xref:System.Windows.Forms.StatusStrip>에는 패널이 없습니다. <xref:System.Windows.Forms.StatusStrip>에 패널을 추가하려면 <xref:System.Windows.Forms.ToolStripItemCollection.AddRange%2A?displayProperty=nameWithType> 메서드를 사용합니다.  
  
 Visual Studio에서는 <xref:System.Windows.Forms.StatusStrip> 항목 및 일반적인 명령 처리가 광범위하게 지원됩니다.  
  
 도 참조 하세요 [StatusStrip 항목 컬렉션 편집기](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/ms233631(v=vs.100)) 하 고 [StatusStrip 작업 대화 상자](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/ms233642(v=vs.100))합니다.  
  
 <xref:System.Windows.Forms.StatusStrip>은 이전 버전의 <xref:System.Windows.Forms.StatusBar> 컨트롤을 대체하고 확장하지만 이전 버전과의 호환성 및 앞으로의 사용 가능성을 고려하여 <xref:System.Windows.Forms.StatusBar>를 유지하도록 선택할 수 있습니다.  
  
### <a name="important-statusstrip-members"></a>중요한 StatusStrip 멤버  
  
|이름|설명|  
|----------|-----------------|  
|<xref:System.Windows.Forms.StatusStrip.CanOverflow%2A>|<xref:System.Windows.Forms.StatusStrip>에서 오버플로 기능을 지원하는지를 나타내는 값을 가져오거나 설정합니다.|  
|<xref:System.Windows.Forms.StatusStrip.Stretch%2A>|<xref:System.Windows.Forms.StatusStrip>이 <xref:System.Windows.Forms.ToolStripContainer>의 끝에서 끝까지 확장되는지를 나타내는 값을 가져오거나 설정합니다.|  
  
### <a name="important-statusstrip-companion-classes"></a>중요한 StatusStrip 도우미 클래스  
  
|이름|설명|  
|----------|-----------------|  
|<xref:System.Windows.Forms.ToolStripStatusLabel>|<xref:System.Windows.Forms.StatusStrip> 컨트롤의 패널을 나타냅니다.|  
|<xref:System.Windows.Forms.ToolStripDropDownButton>|사용자가 단일 항목을 선택할 수 있는 연결된 <xref:System.Windows.Forms.ToolStripDropDown>을 표시합니다.|  
|<xref:System.Windows.Forms.ToolStripSplitButton>|표준 단추와 드롭다운 메뉴인 두 부분으로 구성된 컨트롤을 나타냅니다.|  
|<xref:System.Windows.Forms.ToolStripProgressBar>|프로세스의 완료 상태를 표시합니다.|  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.StatusStrip>
- <xref:System.Windows.Forms.ToolStripStatusLabel>
- <xref:System.Windows.Forms.ToolStripStatusLabel.Spring%2A>
