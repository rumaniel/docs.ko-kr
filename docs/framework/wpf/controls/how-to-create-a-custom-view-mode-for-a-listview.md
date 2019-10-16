---
title: '방법: ListView에 대한 사용자 지정 보기 모드 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ListView controls [WPF], creating custom View mode
ms.assetid: 71077349-eeb9-4344-ab29-b5df96df3314
ms.openlocfilehash: de11250a2e7529fba3b262e42b6714262738fa90
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61910912"
---
# <a name="how-to-create-a-custom-view-mode-for-a-listview"></a>방법: ListView에 대한 사용자 지정 보기 모드 만들기
이 예제에는 사용자 지정을 만드는 방법을 보여 줍니다 <xref:System.Windows.Controls.ListView.View%2A> 에 대 한 모드는 <xref:System.Windows.Controls.ListView> 제어 합니다.  
  
## <a name="example"></a>예제  
 사용 해야 합니다는 <xref:System.Windows.Controls.ViewBase> 에 대 한 사용자 지정 보기를 만들 때 클래스는 <xref:System.Windows.Controls.ListView> 제어 합니다. 다음 예제에서는 호출 되는 뷰 모드를 `PlainView`에서 파생 되는 <xref:System.Windows.Controls.ViewBase> 클래스입니다.  
  
 [!code-csharp[ListViewCustomView#PlainView](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewCustomView/CSharp/PlainView.cs#plainview)]
 [!code-vb[ListViewCustomView#PlainView](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ListViewCustomView/visualbasic/plainview.vb#plainview)]  
  
 사용자 지정 보기에 스타일을 적용 하려면 사용 된 <xref:System.Windows.Style> 클래스입니다. 다음 예제에서는 정의 <xref:System.Windows.Style> 에 대 한는 `PlainView` 보기 모드입니다. 이전 예제에서는이 스타일의 값으로 설정 합니다 <xref:System.Windows.Controls.ViewBase.DefaultStyleKey%2A> 속성에 대해 정의 된 `PlainView`합니다.  
  
 [!code-xaml[ListViewCustomView#PlainViewStyle](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewCustomView/CSharp/Themes/Generic.xaml#plainviewstyle)]  
  
 사용자 지정 보기 모드에서 데이터의 레이아웃을 정의 하려면 정의 <xref:System.Windows.DataTemplate> 개체입니다. 다음 예제에서는 정의 <xref:System.Windows.DataTemplate> 데이터를 표시 하려면 사용할 수 있는 여 `PlainView` 보기 모드입니다.  
  
 [!code-xaml[ListViewCustomView#PlainViewDataTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewCustomView/CSharp/Window1.xaml#plainviewdatatemplate)]  
  
 다음 예제에서는 정의 하는 방법을 보여 줍니다는 <xref:System.Windows.ResourceKey> 에 대 한는 `PlainView` 보기 모드를 사용 하는 <xref:System.Windows.DataTemplate> 앞의 예제에 정의 된 합니다.  
  
 [!code-xaml[ListViewCustomView#PlainViewtileView](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewCustomView/CSharp/Window1.xaml#plainviewtileview)]  
  
 <xref:System.Windows.Controls.ListView> 설정 하는 경우 컨트롤 사용자 지정 보기를 사용할 수는 <xref:System.Windows.Controls.ListView.View%2A> 속성이 리소스 키입니다. 다음 예제에서는 지정 하는 방법을 보여 줍니다 `PlainView` 에 대 한 보기 모드를 <xref:System.Windows.Controls.ListView>입니다.  
  
 [!code-csharp[ListViewCustomView#ListViewtileViewmode](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewCustomView/CSharp/Window1.xaml.cs#listviewtileviewmode)]
 [!code-vb[ListViewCustomView#ListViewtileViewmode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ListViewCustomView/visualbasic/window1.xaml.vb#listviewtileviewmode)]  
  
 전체 샘플을 참조 하세요 [여러 뷰가 포함 된 ListView (C#)](https://github.com/dotnet/samples/tree/master/snippets/csharp/VS_Snippets_Wpf/ListViewCustomView/CSharp) 하거나 [여러 Views(Visual Basic)를 사용 하 여 ListView](https://github.com/dotnet/samples/tree/master/snippets/visualbasic/VS_Snippets_Wpf/ListViewCustomView/visualbasic)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.ListView>
- <xref:System.Windows.Controls.GridView>
- [방법 항목](listview-how-to-topics.md)
- [ListView 개요](listview-overview.md)
- [GridView 개요](gridview-overview.md)
