---
title: '방법: 깊이를 확인할 수 없는 데이터에 TreeView 바인딩'
ms.date: 03/30/2017
helpviewer_keywords:
- TreeView control [WPF], binding to data of indeterminate depth
ms.assetid: daddcd74-1b0f-4ffd-baeb-ec934c5e0f53
ms.openlocfilehash: 7da0a121cdb854c787c105c92cec70b7c4b3244e
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61911081"
---
# <a name="how-to-bind-a-treeview-to-data-that-has-an-indeterminable-depth"></a>방법: 깊이를 확인할 수 없는 데이터에 TreeView 바인딩
바인딩할 하는 상황이 있을 수 있습니다는 <xref:System.Windows.Controls.TreeView> 깊이가 알려지지 않은 데이터 원본에 있습니다.  이 데이터를 기본적으로 폴더가 포함 폴더, 파일 시스템 등 회사의 조직 구조는 재귀 직원의 직속 부하로 다른 직원 있는 경우 발생할 수 있습니다.  
  
 데이터 원본에는 계층적 개체 모델이 있어야 합니다. 예를 들어는 `Employee` 클래스 직원의 직속 부하 직원 개체의 컬렉션을 포함할 수 있습니다. 계층적이 지는 방식으로 데이터를 표시 하는 경우에 데이터의 계층적 표현이 빌드해야 합니다.  
  
 설정 하는 경우는 <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A?displayProperty=nameWithType> 속성 경우에 <xref:System.Windows.Controls.ItemsControl> 생성는 <xref:System.Windows.Controls.ItemsControl> 각 자식 항목 다음 자식에 대 한 <xref:System.Windows.Controls.ItemsControl> 에서는 동일한 <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> 부모로 합니다. 예를 들어, 설정 하는 경우는 <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> 데이터 바인딩된 속성 <xref:System.Windows.Controls.TreeView>각각 <xref:System.Windows.Controls.TreeViewItem> 생성된 되는 <xref:System.Windows.DataTemplate> 에 할당 된를 <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> 속성은 <xref:System.Windows.Controls.TreeView>합니다.  
  
 <xref:System.Windows.HierarchicalDataTemplate> 지정할 수 있습니다 합니다 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 에 대 한를 <xref:System.Windows.Controls.TreeViewItem>, 또는 <xref:System.Windows.Controls.HeaderedItemsControl>, 데이터 서식 파일에서. 설정한 경우 합니다 <xref:System.Windows.HierarchicalDataTemplate.ItemsSource%2A?displayProperty=nameWithType> 속성 값을 때 사용 되는 <xref:System.Windows.HierarchicalDataTemplate> 적용 됩니다. 사용 하 여를 <xref:System.Windows.HierarchicalDataTemplate>, 재귀적으로 설정할 수 있습니다 합니다 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 각각에 대 한 <xref:System.Windows.Controls.TreeViewItem> 에 <xref:System.Windows.Controls.TreeView>.  
  
## <a name="example"></a>예제  
 다음 예제에서는 바인딩하는 방법을 보여는 <xref:System.Windows.Controls.TreeView> 계층적 데이터를 사용 하 여는 <xref:System.Windows.HierarchicalDataTemplate> 지정 하는 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 각각에 대 한 <xref:System.Windows.Controls.TreeViewItem>합니다.  <xref:System.Windows.Controls.TreeView> 회사의 직원을 나타내는 XML 데이터에 바인딩합니다.  각 `Employee` 다른 요소가 포함 될 수 있습니다 `Employee` 부하 직원을 나타내는 요소입니다. 데이터를 재귀적 이므로 <xref:System.Windows.HierarchicalDataTemplate> 각 수준에 적용할 수 있습니다.  
  
 [!code-xaml[TreeViewWithUnknownDepth#1](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeViewWithUnknownDepth/CS/Window1.xaml#1)]  
  
## <a name="see-also"></a>참고자료

- [데이터 바인딩 개요](../data/data-binding-overview.md)
- [데이터 템플릿 개요](../data/data-templating-overview.md)
