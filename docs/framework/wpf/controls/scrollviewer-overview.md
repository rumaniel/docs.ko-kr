---
title: ScrollViewer 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- controls [WPF], ScrollViewer
- ScrollViewer control [WPF], about ScrollViewer control
ms.assetid: 94a13b94-cfdf-4b12-a1aa-90cb50c6e9b9
ms.openlocfilehash: a3302d9c360b0918a1fce956af3e3aa14f29361b
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62024029"
---
# <a name="scrollviewer-overview"></a>ScrollViewer 개요
사용자 인터페이스 내의 콘텐츠는 대개 컴퓨터 화면의 표시 영역보다 더 큽니다. 합니다 <xref:System.Windows.Controls.ScrollViewer> 컨트롤의 콘텐츠 스크롤을 사용 하는 편리한 방법을 제공 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 응용 프로그램입니다. 이 항목에서는 소개 된 <xref:System.Windows.Controls.ScrollViewer> 요소 몇 가지 사용 예제를 제공 합니다.  
  
<a name="what_is_a_scrollviewer_element"></a>   
## <a name="the-scrollviewer-control"></a>ScrollViewer 컨트롤  
 스크롤을 사용 하는 두 개의 미리 정의 된 요소가 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 응용 프로그램: <xref:System.Windows.Controls.Primitives.ScrollBar> 고 <xref:System.Windows.Controls.ScrollViewer>입니다. 합니다 <xref:System.Windows.Controls.ScrollViewer> 컨트롤을 가로 및 세로 캡슐화 <xref:System.Windows.Controls.Primitives.ScrollBar> 요소와 콘텐츠 컨테이너 (같은 <xref:System.Windows.Controls.Panel> 요소) 스크롤 가능한 영역에 표시 가능한 다른 요소를 표시 하기 위해. 사용 하려면 사용자 지정 개체를 빌드해야 합니다 <xref:System.Windows.Controls.Primitives.ScrollBar> 콘텐츠 스크롤에 대 한 요소입니다. 사용할 수 있습니다 합니다 <xref:System.Windows.Controls.ScrollViewer> 자체로 요소는 복합 컨트롤 이므로 캡슐화 <xref:System.Windows.Controls.Primitives.ScrollBar> 기능입니다.  
  
 <xref:System.Windows.Controls.ScrollViewer> 컨트롤 마우스와 키보드 명령에 응답 하 고 미리 결정 된 증분만큼 콘텐츠를 스크롤할 수 있는 다양 한 메서드를 정의 합니다. 사용할 수는 <xref:System.Windows.Controls.ScrollViewer.ScrollChanged> 에서 변경을 감지 하는 이벤트를 <xref:System.Windows.Controls.ScrollViewer> 상태입니다.  
  
 A <xref:System.Windows.Controls.ScrollViewer> 일반적으로 하나의 자식을 하나만 사용할 수는 <xref:System.Windows.Controls.Panel> 호스트할 수 있는 요소를 <xref:System.Windows.Controls.Panel.Children%2A> 요소의 컬렉션입니다. 합니다 <xref:System.Windows.Controls.ContentPresenter.Content%2A> 속성의 유일한 자식을 정의 <xref:System.Windows.Controls.ScrollViewer>합니다.  
  
<a name="scrollviewer_physical_vs_logical"></a>   
## <a name="physical-vs-logical-scrolling"></a>실제 및 논리적 스크롤  
 실제 스크롤은 미리 결정된 실제 증분만큼(일반적으로 픽셀 단위로 선언된 값만큼) 콘텐츠를 스크롤하는 데 사용됩니다. 논리적 스크롤은 논리 트리에서 다음 항목으로 스크롤하는 데 사용됩니다. 실제 스크롤은 대부분에 대 한 기본 스크롤 동작 <xref:System.Windows.Controls.Panel> 요소입니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]는 두 가지 스크롤 형식을 모두 지원합니다.  
  
#### <a name="the-iscrollinfo-interface"></a>IScrollInfo 인터페이스  
 합니다 <xref:System.Windows.Controls.Primitives.IScrollInfo> 인터페이스 내의 주요 스크롤 영역을 나타내는 <xref:System.Windows.Controls.ScrollViewer> 또는 파생 컨트롤입니다. 스크롤 속성 및으로 구현할 수 있는 메서드를 정의 하는 인터페이스 <xref:System.Windows.Controls.Panel> 는 실제 증분이 아닌 논리적 단위로 스크롤 필요로 하는 요소입니다. 인스턴스로 캐스팅 <xref:System.Windows.Controls.Primitives.IScrollInfo> 파생 하려면 <xref:System.Windows.Controls.Panel> 픽셀 증분만큼이 아닌 자식 컬렉션에 있는 다음 논리 단위를 스크롤 하는 유용한 방법을 제공 하 고 스크롤 메서드를 사용 하 여 다음입니다. 기본적으로 <xref:System.Windows.Controls.ScrollViewer> 컨트롤이 실제 단위로 스크롤을 지원 합니다.  
  
 <xref:System.Windows.Controls.StackPanel> 및 <xref:System.Windows.Controls.VirtualizingStackPanel> 둘 다 구현 <xref:System.Windows.Controls.Primitives.IScrollInfo> 기본적으로 논리적 스크롤을 지원 합니다. 레이아웃 컨트롤을 고유 하 게 지원 논리적 스크롤을 얻을 수 있습니다 호스트를 래핑하여 실제 스크롤 <xref:System.Windows.Controls.Panel> 요소에는 <xref:System.Windows.Controls.ScrollViewer> 설정 하는 <xref:System.Windows.Controls.ScrollViewer.CanContentScroll%2A> 속성을 `false`입니다.  
  
 다음 코드 예제에서는의 인스턴스로 캐스팅 하는 방법을 보여 줍니다 <xref:System.Windows.Controls.Primitives.IScrollInfo> 에 <xref:System.Windows.Controls.StackPanel> 콘텐츠 스크롤 메서드 사용 하 여 (<xref:System.Windows.Controls.Primitives.IScrollInfo.LineUp%2A> 및 <xref:System.Windows.Controls.Primitives.IScrollInfo.LineDown%2A>) 인터페이스에 의해 정의 합니다.  
  
 [!code-csharp[IScrollInfoMethods#3](~/samples/snippets/csharp/VS_Snippets_Wpf/IScrollInfoMethods/CSharp/Window1.xaml.cs#3)]
 [!code-vb[IScrollInfoMethods#3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/IScrollInfoMethods/VisualBasic/Window1.xaml.vb#3)]  
  
<a name="scrollviewer_markup_syntax_and_sample"></a>   
## <a name="defining-and-using-a-scrollviewer-element"></a>ScrollViewer 요소 정의 및 사용  
 다음 예제에서는 한 <xref:System.Windows.Controls.ScrollViewer> 일부 텍스트와 사각형이 포함 된 창에서. <xref:System.Windows.Controls.Primitives.ScrollBar> 요소가 표시 된 경우에 필요 합니다. 창의 크기를 조정할 때 합니다 <xref:System.Windows.Controls.Primitives.ScrollBar> 요소가 나타났다 사라집니다, 값이 업데이트 되어 합니다 <xref:System.Windows.Controls.ScrollViewer.ComputedHorizontalScrollBarVisibility%2A> 및 <xref:System.Windows.Controls.ScrollViewer.ComputedVerticalScrollBarVisibility%2A> 속성입니다.  
  
 [!code-cpp[ScrollViewer#1](~/samples/snippets/cpp/VS_Snippets_Wpf/ScrollViewer/CPP/ScrollViewer_wcp.cpp#1)]
 [!code-csharp[ScrollViewer#1](~/samples/snippets/csharp/VS_Snippets_Wpf/ScrollViewer/CSharp/ScrollViewer_wcp.cs#1)]
 [!code-vb[ScrollViewer#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ScrollViewer/VisualBasic/ScrollViewer.vb#1)]
 [!code-xaml[ScrollViewer#1](~/samples/snippets/xaml/VS_Snippets_Wpf/ScrollViewer/XAML/Pane1.xaml#1)]  
  
<a name="scrollviewer_styling_scrollviewer"></a>   
## <a name="styling-a-scrollviewer"></a>ScrollViewer 스타일 지정  
 Windows Presentation Foundation의 모든 컨트롤과 같이 <xref:System.Windows.Controls.ScrollViewer> 컨트롤의 기본 렌더링 동작을 변경 하기 위해 스타일을 지정할 수 있습니다. 컨트롤 스타일 지정에 대한 자세한 내용은 [스타일 지정 및 템플릿](styling-and-templating.md)을 참조하세요.  
  
<a name="scrollviewer_scroll_vs_paginate"></a>   
## <a name="paginating-documents"></a>문서 페이지 매김  
 문서 콘텐츠의 경우 스크롤 대신 페이지 매김을 지원하는 문서 컨테이너를 선택할 수 있습니다. <xref:System.Windows.Documents.FlowDocument> 와 같은 보기 컨트롤 내에서 호스팅 되도록 디자인 된 문서에는 <xref:System.Windows.Controls.FlowDocumentPageViewer>를 스크롤할 필요성을 방지 하는 여러 페이지에 걸쳐 분할 콘텐츠를 지 원하는 합니다. <xref:System.Windows.Controls.DocumentViewer> 보기에 대 한 솔루션을 제공 <xref:System.Windows.Documents.FixedDocument> 콘텐츠 표시 영역의 외부에 콘텐츠를 표시 하려면 기존 스크롤을 사용 하는 합니다.  
  
 문서 서식 및 프레젠테이션 옵션에 대한 자세한 내용은 [WPF의 문서](../advanced/documents-in-wpf.md)를 참조하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.ScrollViewer>
- <xref:System.Windows.Controls.Primitives.ScrollBar>
- <xref:System.Windows.Controls.Primitives.IScrollInfo>
- [방법: 스크롤 뷰어 만들기](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms752352(v=vs.90))
- [WPF의 문서](../advanced/documents-in-wpf.md)
- [ScrollBar 스타일 및 템플릿](scrollbar-styles-and-templates.md)
- [컨트롤](../advanced/optimizing-performance-controls.md)
