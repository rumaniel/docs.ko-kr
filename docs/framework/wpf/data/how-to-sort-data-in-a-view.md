---
title: '방법: 보기에서 데이터 정렬'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data binding [WPF], sorting data in views
- data binding [WPF], grouping data in views
- grouping data in views [WPF]
- views [WPF], sorting data
- views [WPF], grouping data
- sorting data in views [WPF]
ms.assetid: f4c43578-01b7-4774-a953-acb95a13b94a
ms.openlocfilehash: 32f73d3c3ba213778654f0d1ee7bbae16b9d845b
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62020727"
---
# <a name="how-to-sort-data-in-a-view"></a>방법: 보기에서 데이터 정렬
이 예제에는 뷰에서 데이터를 정렬 하는 방법을 설명 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 간단한 <xref:System.Windows.Controls.ListBox> 및 <xref:System.Windows.Controls.Button>:  
  
 [!code-xaml[ListBoxSort_snip#HowTo](~/samples/snippets/csharp/VS_Snippets_Wpf/ListBoxSort_snip/CSharp/Window1.xaml#howto)]  
  
 합니다 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 단추의 이벤트 처리기의 항목을 정렬 하기 위한 논리가 포함 된 <xref:System.Windows.Controls.ListBox> 내림차순에서입니다. 에 항목을 추가 하기 때문에이 수행할 수 있습니다는 <xref:System.Windows.Controls.ListBox> 이러한 방식으로 추가 합니다는 <xref:System.Windows.Controls.ItemCollection> 의 합니다 <xref:System.Windows.Controls.ListBox>, 및 <xref:System.Windows.Controls.ItemCollection> 에서 파생 되는 <xref:System.Windows.Data.CollectionView> 클래스. 바인딩하는 경우에 <xref:System.Windows.Controls.ListBox> 사용 하 여 컬렉션을 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 속성을 정렬 하려면 동일한 기법을 사용할 수 있습니다.  
  
 [!code-csharp[ListBoxSort_snip#HowToCode](~/samples/snippets/csharp/VS_Snippets_Wpf/ListBoxSort_snip/CSharp/Window1.xaml.cs#howtocode)]
 [!code-vb[ListBoxSort_snip#HowToCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ListBoxSort_snip/visualbasic/window1.xaml.vb#howtocode)]  
  
 뷰 개체에 대 한 참조를 만든으로 다른 컬렉션 보기의 콘텐츠를 정렬 하려면 동일한 기법을 사용할 수 있습니다. 보고 하는 방법의 예제를 참조 하세요 [데이터 컬렉션의 기본 뷰 가져오기](how-to-get-the-default-view-of-a-data-collection.md)합니다. 다른 예제를 보려면 [는 GridView 열은 머리글을 클릭 하면 정렬](../controls/how-to-sort-a-gridview-column-when-a-header-is-clicked.md)합니다. 보기에 대 한 자세한 내용은 참조 컬렉션에 바인딩 [데이터 바인딩 개요](data-binding-overview.md)합니다.  
  
 정렬 논리를 적용 하는 방법의 예 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]를 참조 하세요 [정렬 및 그룹 데이터를 XAML에서 뷰를 사용 하 여](how-to-sort-and-group-data-using-a-view-in-xaml.md)입니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Data.ListCollectionView.CustomSort%2A>
- [헤더를 클릭하면 GridView 열 정렬](../controls/how-to-sort-a-gridview-column-when-a-header-is-clicked.md)
- [데이터 바인딩 개요](data-binding-overview.md)
- [뷰에서 데이터 필터링](how-to-filter-data-in-a-view.md)
- [방법 항목](data-binding-how-to-topics.md)
