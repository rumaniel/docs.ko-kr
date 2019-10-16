---
title: Windows Forms MenuStrip 컨트롤의 메뉴 항목 병합
ms.date: 03/30/2017
helpviewer_keywords:
- MenuStrip [Windows Forms], merging
- merging [Windows Forms], general concepts
ms.assetid: 95e113ba-f362-4dda-8a76-6d95ddc45cee
ms.openlocfilehash: 9a1f59a065faaa3a08a9d8a68973adb1faa5ed09
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64582928"
---
# <a name="merging-menu-items-in-the-windows-forms-menustrip-control"></a>Windows Forms MenuStrip 컨트롤의 메뉴 항목 병합
응용 프로그램을 다중 문서 인터페이스 (MDI)에 있는 경우 부모 폼의 메뉴에 메뉴 항목이 나 자식 폼의 전체 메뉴를 병합할 수 있습니다.  
  
 이 항목에서는 MDI 응용 프로그램에서 메뉴 항목 병합에 연결 된 기본 개념을 설명 합니다.  
  
## <a name="general-concepts"></a>일반 개념  
 병합 프로시저에는 대상 및 소스 컨트롤을 모두 포함 됩니다.  
  
- 대상이 <xref:System.Windows.Forms.MenuStrip> 메뉴 항목을 병합 되는 주 또는 MDI 부모 폼에서 제어 합니다.  
  
- 원본이 <xref:System.Windows.Forms.MenuStrip> 병합할 대상 메뉴에 메뉴 항목이 들어 있는 MDI 자식 폼의 컨트롤입니다.  
  
 <xref:System.Windows.Forms.MenuStrip.MdiWindowListItem%2A> 현재 MDI의 제목을 채워집니다 드롭다운 목록이 있는 부모 폼의 MDI 자식 메뉴 항목을 식별 하는 속성입니다. 예를 들어, 일반적으로 나열할 수에서 현재 열려 있는 MDI 자식 폼의 **창** 메뉴.  
  
 <xref:System.Windows.Forms.ToolStripMenuItem.IsMdiWindowListEntry%2A> 에서 가져온 메뉴 항목을 식별 하는 속성을 <xref:System.Windows.Forms.MenuStrip> MDI 자식 폼에서.  
  
 수동 또는 자동으로 메뉴 항목을 병합할 수 있습니다. 두 방법 모두 동일한 방식으로 메뉴 항목 병합 하지만 병합이이 항목 뒷부분의 "수동 병합" 및 "자동 병합" 섹션에서 설명 했 듯이 다르게 활성화 됩니다. 각 병합 동작을 수동 및 자동 병합을 다음 병합 작업을 영향을 줍니다.  
  
 <xref:System.Windows.Forms.MenuStrip> 메뉴 항목 간에 이동 병합 <xref:System.Windows.Forms.ToolStrip> 간 사용 하는 경우 처럼 복제 하는 대신 <xref:System.Windows.Forms.MainMenu>합니다.  
  
## <a name="mergeaction-values"></a>MergeAction 값  
 원본에서 메뉴 항목에 병합 작업을 설정할 <xref:System.Windows.Forms.MenuStrip> 를 사용 하 여는 <xref:System.Windows.Forms.MergeAction> 속성입니다.  
  
 다음 표에서 사용할 수 있는 병합 작업의 의미와 일반적인 사용 방법을 설명 합니다.  
  
|MergeAction 값|설명|일반적인 용도|  
|-----------------------|-----------------|-----------------|  
|<xref:System.Windows.Forms.MergeAction.Append>|(기본값) 대상 항목의 컬렉션의 끝에 소스 항목을 추가합니다.|프로그램의 일부를 활성화할 때 메뉴 항목 메뉴의 끝에 추가 합니다.|  
|<xref:System.Windows.Forms.MergeAction.Insert>|소스 항목에서 지정 된 위치에서 대상 항목의 컬렉션에 추가 된 <xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A> 소스 항목에서 속성을 설정 합니다.|중간 또는 프로그램의 일부를 활성화할 때 메뉴의 시작 부분에 메뉴 항목을 추가 합니다.<br /><br /> 경우 변수의 <xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A> 동일 메뉴 항목 모두에 대해 추가 된 역순입니다. 설정 <xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A> 적절 하 게 원래 순서를 유지 합니다.|  
|<xref:System.Windows.Forms.MergeAction.Replace>|텍스트 일치 항목을 찾거나 사용 하는 <xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A> 값 텍스트 일치 하는 항목이 발견 되 고 원본 메뉴 항목과 일치 하는 대상 메뉴 항목을 다음으로 바꿉니다.|대상 메뉴 항목을 다르게 수행 하는 동일한 이름의 원본 메뉴 항목을 바꿉니다.|  
|<xref:System.Windows.Forms.MergeAction.MatchOnly>|텍스트 일치 항목을 찾거나 사용 된 <xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A> 텍스트 일치 하는 항목이 발견 되 면 대상에 원본의 드롭다운 목록 항목을 모두 추가한 경우 값입니다.|메뉴 구조 구축 삽입을 하위 메뉴에 메뉴 항목을 추가 또는 하위 메뉴에서 메뉴 항목을 제거 합니다. 기본에서 MDI 자식 메뉴 항목을를 추가할 수는 예를 들어 <xref:System.Windows.Forms.MenuStrip> **다른 이름으로 저장** 메뉴.<br /><br /> <xref:System.Windows.Forms.MergeAction.MatchOnly> 이 기능을 사용 하면 어떤 동작도 수행 하지 않고 메뉴 구조를 탐색할 수 있습니다. 후속 항목을 확인 하는 방법을 제공 합니다.|  
|<xref:System.Windows.Forms.MergeAction.Remove>|텍스트 일치 항목을 찾거나 사용 하는 <xref:System.Windows.Forms.ToolStripItem.MergeIndex%2A> 값 텍스트 일치 하는 항목이 발견 되 고 대상에서 항목을 제거 합니다.|대상에서 메뉴 항목을 제거 <xref:System.Windows.Forms.MenuStrip>합니다.|  
  
## <a name="manual-merging"></a>수동 병합  
 만 <xref:System.Windows.Forms.MenuStrip> 컨트롤이 자동 병합에 참여 합니다. 와 같은 다른 컨트롤의 항목을 결합 하 <xref:System.Windows.Forms.ToolStrip> 하 고 <xref:System.Windows.Forms.StatusStrip> 컨트롤을 병합 해야 해당 수동으로 호출 하 여 합니다 <xref:System.Windows.Forms.ToolStripManager.Merge%2A> 및 <xref:System.Windows.Forms.ToolStripManager.RevertMerge%2A> 필요에 따라 코드에서 메서드.  
  
## <a name="automatic-merging"></a>자동 병합  
 소스 폼을 활성화 하 여 MDI 응용 프로그램에 대 한 자동 병합을 사용할 수 있습니다. 사용 하는 <xref:System.Windows.Forms.MenuStrip> MDI 응용 프로그램에서 설정 합니다 <xref:System.Windows.Forms.Form.MainMenuStrip%2A> 속성을 대상 <xref:System.Windows.Forms.MenuStrip> 병합 작업이 원본에서 수행 되도록 <xref:System.Windows.Forms.MenuStrip> 대상에 반영 됩니다 <xref:System.Windows.Forms.MenuStrip>합니다.  
  
 활성화 하 여 자동 병합을 트리거할 수 있습니다는 <xref:System.Windows.Forms.MenuStrip> MDI 원본입니다. 활성화 되 면 원본 <xref:System.Windows.Forms.MenuStrip> MDI 대상에 병합 됩니다. 새 폼을 활성화 하는 경우 마지막 폼의 병합 되돌아가고 새 폼에서 트리거됩니다. 설정 하 여이 동작을 제어할 수 있습니다는 <xref:System.Windows.Forms.ToolStripItem.MergeAction%2A> 각각에 필요한 속성을 <xref:System.Windows.Forms.ToolStripItem>를 설정 하 고는 <xref:System.Windows.Forms.ToolStrip.AllowMerge%2A> 각 속성 <xref:System.Windows.Forms.MenuStrip>합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ToolStripManager>
- <xref:System.Windows.Forms.MenuStrip>
- [MenuStrip 컨트롤](menustrip-control-windows-forms.md)
- [방법: MenuStrip이 포함 된 MDI 창 목록 만들기](how-to-create-an-mdi-window-list-with-menustrip-windows-forms.md)
- [방법: MDI 응용 프로그램의 자동 메뉴 병합 설정](how-to-set-up-automatic-menu-merging-for-mdi-applications.md)
