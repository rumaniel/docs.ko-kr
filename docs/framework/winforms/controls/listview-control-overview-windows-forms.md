---
title: ListView 컨트롤 개요(Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- ListView
helpviewer_keywords:
- lists
- ListView control [Windows Forms], about ListView control
- list views
ms.assetid: c9ef56c1-3bb1-4101-9f4e-e95e720f2756
ms.openlocfilehash: 7b7eac942a7e857ad731c0f77389e84aee287c08
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69952158"
---
# <a name="listview-control-overview-windows-forms"></a>ListView 컨트롤 개요(Windows Forms)
Windows Forms <xref:System.Windows.Forms.ListView> 컨트롤은 아이콘이 포함된 항목 목록을 표시합니다. 목록 뷰를 사용하여 Windows 탐색기의 오른쪽 창과 같은 사용자 인터페이스를 만들 수 있습니다. 컨트롤에는 다음과 같은 네 가지 보기 모드가 있습니다. LargeIcon, SmallIcon, List 및 Details가 있습니다.  
  
## <a name="what-you-can-do-with-the-listview-control"></a>ListView 컨트롤을 사용 하 여 수행할 수 있는 작업  
  
> [!NOTE]
> 추가 보기 모드인 타일은 Windows XP 및 Windows Server 2003 운영 체제 에서만 사용할 수 있습니다. 자세한 내용은 [방법: Windows Forms ListView 컨트롤](how-to-enable-tile-view-in-a-windows-forms-listview-control.md)에서 Tile 보기를 사용 하도록 설정 합니다.  
  
 LargeIcon 모드는 항목 텍스트 옆에 있는 긴 아이콘을 표시 합니다. 컨트롤이 충분히 크면 항목이 여러 열에 표시 됩니다. SmallIcon 모드는 작은 아이콘을 표시 한다는 점을 제외 하 고 동일 합니다. 목록 모드는 작은 아이콘을 표시 하지만 항상 단일 열에 있습니다. 세부 정보 모드는 여러 열에 항목을 표시 합니다. 자세한 내용은 [방법: Windows Forms ListView 컨트롤](how-to-add-columns-to-the-windows-forms-listview-control.md)에 열을 추가 합니다. 뷰 모드는 속성에 <xref:System.Windows.Forms.ListView.View%2A> 의해 결정 됩니다. 모든 보기 모드는 이미지 목록의 이미지를 표시할 수 있습니다. 자세한 내용은 [방법: Windows Forms ListView 컨트롤](how-to-display-icons-for-the-windows-forms-listview-control.md)의 아이콘을 표시 합니다.  
  
 다음 표에서는 일부 <xref:System.Windows.Forms.ListView> 멤버와 이러한 멤버가 유효한 뷰를 나열 합니다.  
  
|ListView 구성원|보기|  
|---------------------|----------|  
|<xref:System.Windows.Forms.ListView.Alignment%2A> 속성|<xref:System.Windows.Forms.View.SmallIcon> 또는 <xref:System.Windows.Forms.View.LargeIcon>|  
|<xref:System.Windows.Forms.ListView.AutoArrange%2A> 속성|<xref:System.Windows.Forms.View.SmallIcon> 또는 <xref:System.Windows.Forms.View.LargeIcon>|  
|<xref:System.Windows.Forms.ListView.AutoResizeColumn%2A> 메서드|<xref:System.Windows.Forms.View.Details>|  
|<xref:System.Windows.Forms.ListView.Columns%2A> 속성|<xref:System.Windows.Forms.View.Details> 또는 <xref:System.Windows.Forms.View.Tile>|  
|<xref:System.Windows.Forms.ListView.DrawSubItem> 이벤트|<xref:System.Windows.Forms.View.Details>|  
|<xref:System.Windows.Forms.ListView.FindItemWithText%2A> 메서드|<xref:System.Windows.Forms.View.Details>, <xref:System.Windows.Forms.View.List>또는 <xref:System.Windows.Forms.View.Tile>|  
|<xref:System.Windows.Forms.ListView.FindNearestItem%2A> 메서드|<xref:System.Windows.Forms.View.SmallIcon> 또는 <xref:System.Windows.Forms.View.LargeIcon>|  
|<xref:System.Windows.Forms.ListView.GetItemAt%2A> 메서드|<xref:System.Windows.Forms.View.Details> 또는 <xref:System.Windows.Forms.View.Tile>|  
|<xref:System.Windows.Forms.ListView.Groups%2A> 속성|제외한 모든 보기 <xref:System.Windows.Forms.View.List>|  
|<xref:System.Windows.Forms.ListView.HeaderStyle%2A> 속성|<xref:System.Windows.Forms.View.Details>.|  
|<xref:System.Windows.Forms.ListView.InsertionMark%2A> 속성|<xref:System.Windows.Forms.View.LargeIcon>, <xref:System.Windows.Forms.View.SmallIcon>또는 <xref:System.Windows.Forms.View.Tile>|  
  
 <xref:System.Windows.Forms.ListView> 컨트롤의 키 속성은 컨트롤에 <xref:System.Windows.Forms.ListView.Items%2A>의해 표시 되는 항목을 포함 하는입니다. 속성 <xref:System.Windows.Forms.ListView.SelectedItems%2A> 은 컨트롤에서 현재 선택 된 항목의 컬렉션을 포함 합니다. <xref:System.Windows.Forms.ListView.MultiSelect%2A> 속성이 로`true`설정 된 경우 사용자는 여러 항목을 선택 하 여 한 번에 여러 항목을 끌어서 놓을 수 있습니다. <xref:System.Windows.Forms.ListView.CheckBoxes%2A> 속성이 <xref:System.Windows.Forms.ListView> 로`true`설정 된 경우 컨트롤은 항목 옆에 있는 확인란을 표시할 수 있습니다.  
  
 속성 <xref:System.Windows.Forms.ListView.Activation%2A> 은 사용자가 목록에서 항목을 활성화 하기 위해 수행 해야 하는 동작의 유형을 결정 합니다. <xref:System.Windows.Forms.ItemActivation.Standard>옵션은 <xref:System.Windows.Forms.ItemActivation.OneClick>, 및 <xref:System.Windows.Forms.ItemActivation.TwoClick>입니다. <xref:System.Windows.Forms.ItemActivation.OneClick>활성화 하려면 한 번 클릭 하 여 항목을 활성화 해야 합니다. <xref:System.Windows.Forms.ItemActivation.TwoClick>활성화 하려면 사용자가 항목을 활성화 하려면 두 번 클릭 해야 합니다. 한 번 클릭으로 항목 텍스트의 색을 변경 합니다. <xref:System.Windows.Forms.ItemActivation.Standard>활성화 하려면 사용자가 항목을 활성화 하려면 두 번 클릭 해야 하지만 항목의 모양은 변경 되지 않습니다.  
  
 컨트롤 <xref:System.Windows.Forms.ListView> 은 그룹화, 타일 보기 및 삽입 표시를 포함 하 여 Windows XP 플랫폼에서 사용할 수 있는 비주얼 스타일 및 기타 기능도 지원 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ListView>
- [ListView 컨트롤](listview-control-windows-forms.md)
- [방법: Windows Forms ListView 컨트롤을 사용 하 여 항목 추가 및 제거](how-to-add-and-remove-items-with-the-windows-forms-listview-control.md)
- [방법: Windows Forms ListView 컨트롤에 열 추가](how-to-add-columns-to-the-windows-forms-listview-control.md)
- [방법: Windows Forms ListView 컨트롤의 아이콘 표시](how-to-display-icons-for-the-windows-forms-listview-control.md)
- [방법: Windows Forms ListView 컨트롤을 사용 하 여 열에 하위 항목 표시](how-to-display-subitems-in-columns-with-the-windows-forms-listview-control.md)
- [방법: Windows Forms ListView 컨트롤에서 항목 선택](how-to-select-an-item-in-the-windows-forms-listview-control.md)
- [방법: Windows Forms ListView 컨트롤에서 항목 그룹화](how-to-group-items-in-a-windows-forms-listview-control.md)
- [방법: Windows Forms ListView 컨트롤에 삽입 표시를 표시 합니다.](how-to-display-an-insertion-mark-in-a-windows-forms-listview-control.md)
- [방법: ListView 컨트롤에 검색 기능 추가](how-to-add-search-capabilities-to-a-listview-control.md)
- [방법: TreeView 또는 ListView 컨트롤에 사용자 지정 정보 추가 (Windows Forms)](add-custom-information-to-a-treeview-or-listview-control-wf.md)
- [방법: Windows Forms를 사용 하 여 다중 창 사용자 인터페이스 만들기](how-to-create-a-multipane-user-interface-with-windows-forms.md)
