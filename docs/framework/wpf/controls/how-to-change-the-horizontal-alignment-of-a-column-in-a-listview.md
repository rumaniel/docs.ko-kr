---
title: '방법: ListView에서 열의 가로 맞춤 변경'
ms.date: 03/30/2017
helpviewer_keywords:
- ListView controls [WPF], horizontal alignment [WPF]
ms.assetid: b9573e44-9dad-4d14-939c-7859ca372758
ms.openlocfilehash: 528a711c1cf7992bb32c0aa4d6e81d71744c9f80
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61911068"
---
# <a name="how-to-change-the-horizontal-alignment-of-a-column-in-a-listview"></a>방법: ListView에서 열의 가로 맞춤 변경
기본적으로 각 열에 콘텐츠를 <xref:System.Windows.Controls.ListViewItem> 왼쪽에 맞춰집니다. 제공 하 여 각 열의 맞춤을 변경할 수 있습니다는 <xref:System.Windows.DataTemplate> 설정 합니다 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 내 요소의 속성에는 <xref:System.Windows.DataTemplate>. 이 항목에서는 어떻게를 <xref:System.Windows.Controls.ListView> 의 한 열에 맞춤을 변경 하는 방법 및 기본적으로 해당 내용을 맞춥니다.는 <xref:System.Windows.Controls.ListView>합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는의 데이터에에서는 `Title` 및 `ISBN` 열 왼쪽에 맞춰집니다.  
  
 [!code-xaml[ListViewHowTos#1](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewHowTos/CSharp/Window1.xaml#1)]  
[!code-xaml[ListViewHowTos#2](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewHowTos/CSharp/Window1.xaml#2)]  
  
 맞춤을 변경 하는 `ISBN` 열을 지정 해야 하는 합니다 <xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A> 각 속성 <xref:System.Windows.Controls.ListViewItem> 는 <xref:System.Windows.HorizontalAlignment.Stretch>되도록 각 요소 <xref:System.Windows.Controls.ListViewItem> 에 걸쳐 있을 수 또는 각 열의 너비를 전체 놓일. 때문에 <xref:System.Windows.Controls.ListView> 바인딩된 데이터 원본에 설정 하는 스타일을 생성 해야 합니다 <xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A>합니다. 사용 해야 하는 다음에 <xref:System.Windows.DataTemplate> 사용 하는 대신 내용을 표시 하는 <xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A> 속성입니다. 표시할 합니다 `ISBN` 각 템플릿의 합니다 <xref:System.Windows.DataTemplate> 만 포함할 수 있습니다를 <xref:System.Windows.Controls.TextBlock> 있는 해당 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 속성이로 설정 <xref:System.Windows.HorizontalAlignment.Right>.  
  
 스타일을 정의 하는 다음 예제에서는 및 <xref:System.Windows.DataTemplate> 하는 데 필요한를 `ISBN` 오른쪽 맞춤, 열 및 변경 합니다 <xref:System.Windows.Controls.GridViewColumn> 참조는 <xref:System.Windows.DataTemplate>.  
  
 [!code-xaml[ListViewHowTos#3](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewHowTos/CSharp/Window1.xaml#3)]  
[!code-xaml[ListViewHowTos#4](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewHowTos/CSharp/Window1.xaml#4)]  
  
## <a name="see-also"></a>참고자료

- [데이터 바인딩 개요](../data/data-binding-overview.md)
- [데이터 템플릿 개요](../data/data-templating-overview.md)
- [XMLDataProvider 및 XPath 쿼리를 사용하여 XML 데이터에 바인딩](../data/how-to-bind-to-xml-data-using-an-xmldataprovider-and-xpath-queries.md)
- [ListView 개요](listview-overview.md)
