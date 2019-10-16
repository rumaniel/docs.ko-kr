---
title: '방법: TreeView 성능 향상'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- TreeView control [WPF], improving the performance
ms.assetid: b792c740-cf2b-4da8-8ba8-3d2e5a821874
ms.openlocfilehash: de1b46da2a7c6c3db0c0c19cdbb654fcf2fbbd6c
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61771009"
---
# <a name="how-to-improve-the-performance-of-a-treeview"></a>방법: TreeView 성능 향상
경우는 <xref:System.Windows.Controls.TreeView> 많은 항목이 로드 하는 데 걸리는 시간 사용자 인터페이스에서 상당한 지연이 발생할 수 있습니다. 설정 하 여 로드 하는 시간을 향상 시킬 수 있습니다 합니다 `VirtualizingStackPanel.IsVirtualizing` 연결 속성을 `true`입니다.  UI를 사용자가 스크롤할 때 대응할 느린 수도 있습니다는 <xref:System.Windows.Controls.TreeView> 스크롤 막대의 엄지 단추를 끌거나 마우스 휠을 사용 하 여 합니다. 성능을 향상 시킬 수 있습니다 합니다 <xref:System.Windows.Controls.TreeView> 설정 하 여 사용자가 스크롤할 때 합니다 `VirtualizingStackPanel.VirtualizationMode` 연결 된 속성을 <xref:System.Windows.Controls.VirtualizationMode.Recycling?displayProperty=nameWithType>입니다.  
  
## <a name="example"></a>예제  
  
## <a name="description"></a>설명  
다음 예제에서는 <xref:System.Windows.Controls.TreeView> 로 설정 하는 `VirtualizingStackPanel.IsVirtualizing` 연결 된 속성을 true로 및 `VirtualizingStackPanel.VirtualizationMode` 연결 된 속성을 <xref:System.Windows.Controls.VirtualizationMode.Recycling?displayProperty=nameWithType> 해당 성능을 최적화 하기 위해.  
  
## <a name="code"></a>코드  
 [!code-xaml[RecycleItemContainerShippets#VirtualizingTreeView](~/samples/snippets/csharp/VS_Snippets_Wpf/RecycleItemContainerShippets/CSharp/Window1.xaml#virtualizingtreeview)]  
  
 다음 예제에서는 이전 예제에 사용 데이터를 보여 줍니다.  
  
 [!code-csharp[RecycleItemContainerShippets#TreeViewData](~/samples/snippets/csharp/VS_Snippets_Wpf/RecycleItemContainerShippets/CSharp/Window1.xaml.cs#treeviewdata)]
 [!code-vb[RecycleItemContainerShippets#TreeViewData](~/samples/snippets/visualbasic/VS_Snippets_Wpf/RecycleItemContainerShippets/visualbasic/window1.xaml.vb#treeviewdata)]  
  
## <a name="see-also"></a>참고자료

- [컨트롤](../advanced/optimizing-performance-controls.md)
