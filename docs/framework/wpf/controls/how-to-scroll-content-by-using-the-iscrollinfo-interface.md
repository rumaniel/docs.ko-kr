---
title: '방법: IScrollInfo 인터페이스를 사용하여 콘텐츠 스크롤'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ScrollViewer control [WPF], scrolling content
- scrolling content [WPF]
- IScrollInfo interface [WPF]
ms.assetid: d8700bef-a3f8-4c12-9de2-fc3b79f32cd3
ms.openlocfilehash: 6ebd8268e1358b45709885c07e6b096d5f806ebb
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62051249"
---
# <a name="how-to-scroll-content-by-using-the-iscrollinfo-interface"></a>방법: IScrollInfo 인터페이스를 사용하여 콘텐츠 스크롤
사용 하 여 콘텐츠 스크롤 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Controls.Primitives.IScrollInfo> 인터페이스입니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 기능의 <xref:System.Windows.Controls.Primitives.IScrollInfo> 인터페이스입니다. 이 예에서는 만듭니다는 <xref:System.Windows.Controls.StackPanel> 요소에 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 부모에 중첩 된 <xref:System.Windows.Controls.ScrollViewer>합니다. 자식 요소를 <xref:System.Windows.Controls.StackPanel> 정의한 메서드를 사용 하 여 논리적으로 스크롤할 수 합니다 <xref:System.Windows.Controls.Primitives.IScrollInfo> 인터페이스와의 인스턴스로 캐스트 <xref:System.Windows.Controls.StackPanel> (`sp1`) 코드에서.  
  
 [!code-xaml[IScrollInfoMethods#2](~/samples/snippets/csharp/VS_Snippets_Wpf/IScrollInfoMethods/CSharp/Window1.xaml#2)]  
  
 각 <xref:System.Windows.Controls.Button> 에 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 파일에서 스크롤 동작을 제어 하는 연결 된 사용자 지정 메서드를 트리거합니다 <xref:System.Windows.Controls.StackPanel>합니다. 다음 예제에서는 사용 하는 방법을 보여 줍니다는 <xref:System.Windows.Controls.Primitives.IScrollInfo.LineUp%2A> 및 <xref:System.Windows.Controls.Primitives.IScrollInfo.LineDown%2A> ; 메서드 또한 일반적으로 모든 위치 지정 메서드를 사용 하는 방법을 보여 줍니다는 <xref:System.Windows.Controls.Primitives.IScrollInfo> 클래스를 정의 합니다.  
  
 [!code-csharp[IScrollInfoMethods#3](~/samples/snippets/csharp/VS_Snippets_Wpf/IScrollInfoMethods/CSharp/Window1.xaml.cs#3)]
 [!code-vb[IScrollInfoMethods#3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/IScrollInfoMethods/VisualBasic/Window1.xaml.vb#3)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.ScrollViewer>
- <xref:System.Windows.Controls.Primitives.IScrollInfo>
- <xref:System.Windows.Controls.StackPanel>
- [ScrollViewer 개요](scrollviewer-overview.md)
- [방법 항목](scrollviewer-how-to-topics.md)
- [패널 개요](panels-overview.md)
