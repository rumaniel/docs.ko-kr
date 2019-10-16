---
title: '방법: Windows Forms ListView 컨트롤에서 항목 그룹화'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ListView control [Windows Forms], grouping items
- lists [Windows Forms], grouping items
- grouping
- list views [Windows Forms], grouping items
- groups
- groups [Windows Forms], in Windows Forms controls
ms.assetid: 610416a1-8da4-436c-af19-5f19e654769b
ms.openlocfilehash: b4cd2b9ed23f377912270d33b1415ad39c9e80c0
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69966625"
---
# <a name="how-to-group-items-in-a-windows-forms-listview-control"></a>방법: Windows Forms ListView 컨트롤에서 항목 그룹화
<xref:System.Windows.Forms.ListView> 컨트롤의 그룹화 기능을 사용 하면 관련 항목 집합을 그룹으로 표시할 수 있습니다. 이러한 그룹은 그룹 제목이 포함 된 가로 그룹 헤더로 화면에 구분 됩니다. 그룹을 사용 <xref:System.Windows.Forms.ListView> 하 여 항목을 사전순으로, 날짜별로 또는 다른 논리적 그룹화로 그룹화 하 여 많은 목록을 보다 쉽게 탐색할 수 있습니다. 다음 그림은 몇 가지 그룹화 된 항목을 보여 줍니다.  
  
 ![홀수 및 심지어 ListView 그룹의 스크린샷](./media/how-to-group-items-in-a-windows-forms-listview-control-using-the-designer/odd-even-list-view-groups.gif)  
   
 그룹화를 사용 하려면 먼저 디자이너에서 또는 프로그래밍 방식으로 하나 이상의 그룹을 만들어야 합니다. 그룹이 정의 된 후에는 항목을 그룹에 <xref:System.Windows.Forms.ListView> 할당할 수 있습니다. 한 그룹에서 다른 그룹으로 항목을 프로그래밍 방식으로 이동할 수도 있습니다.  
  
> [!NOTE]
> <xref:System.Windows.Forms.ListView>응용 프로그램에서 메서드를 [!INCLUDE[WinXpFamily](../../../../includes/winxpfamily-md.md)] <xref:System.Windows.Forms.Application.EnableVisualStyles%2A?displayProperty=nameWithType> 호출 하는 경우에만 그룹을 사용할 수 있습니다. 이전 버전의 운영 체제 그룹 관련 모든 코드가 미치지 않으며 그룹 표시 되지 않습니다. 자세한 내용은 <xref:System.Windows.Forms.ListView.Groups%2A?displayProperty=nameWithType>을 참조하세요.  
  
### <a name="to-add-groups"></a>그룹을 추가 하려면  
  
1. <xref:System.Windows.Forms.ListViewGroupCollection.Add%2A> 컬렉션의 <xref:System.Windows.Forms.ListView.Groups%2A> 메서드를 사용합니다.  
  
     [!code-csharp[System.Windows.Forms.ListViewLegacyTopics#21](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/CS/Class1.cs#21)]
     [!code-vb[System.Windows.Forms.ListViewLegacyTopics#21](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/VB/Class1.vb#21)]  
  
### <a name="to-remove-groups"></a>그룹을 제거 하려면  
  
1. 컬렉션의 <xref:System.Windows.Forms.ListViewGroupCollection.Clear%2A> <xref:System.Windows.Forms.ListViewGroupCollection.RemoveAt%2A> 또는메서드를사용합니다<xref:System.Windows.Forms.ListView.Groups%2A> .  
  
     메서드 <xref:System.Windows.Forms.ListViewGroupCollection.RemoveAt%2A> 는 단일 그룹을 제거 합니다. <xref:System.Windows.Forms.ListViewGroupCollection.Clear%2A> 메서드는 목록에서 모든 그룹을 제거 합니다.  
  
    > [!NOTE]
    > 그룹을 제거 해도 해당 그룹 내의 항목은 제거 되지 않습니다.  
  
     [!code-csharp[System.Windows.Forms.ListViewLegacyTopics#22](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/CS/Class1.cs#22)]
     [!code-vb[System.Windows.Forms.ListViewLegacyTopics#22](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/VB/Class1.vb#22)]  
  
### <a name="to-assign-items-to-groups-or-move-items-between-groups"></a>그룹에 항목을 할당 하거나 그룹 간에 항목을 이동 하려면  
  
1. 개별 항목 <xref:System.Windows.Forms.ListViewItem.Group%2A?displayProperty=nameWithType> 의 속성을 설정 합니다.  
  
     [!code-csharp[System.Windows.Forms.ListViewLegacyTopics#23](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/CS/Class1.cs#23)]
     [!code-vb[System.Windows.Forms.ListViewLegacyTopics#23](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/VB/Class1.vb#23)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ListView>
- <xref:System.Windows.Forms.ListView.Groups%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.ListViewGroup>
- [ListView 컨트롤](listview-control-windows-forms.md)
- [ListView 컨트롤 개요](listview-control-overview-windows-forms.md)
- [방법: Windows Forms ListView 컨트롤을 사용 하 여 항목 추가 및 제거](how-to-add-and-remove-items-with-the-windows-forms-listview-control.md)
