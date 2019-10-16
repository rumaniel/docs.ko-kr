---
title: '방법: 라우트된 이벤트 처리'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- routed events [WPF], handling
- bubbling events [WPF]
ms.assetid: 157787b4-f469-4047-8777-5b034145f32e
ms.openlocfilehash: edb3d6724af89b7e85986c50b579084e3c4e5070
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62001509"
---
# <a name="how-to-handle-a-routed-event"></a>방법: 라우트된 이벤트 처리
이 예제에서는 버블링 이벤트가 작동하는 방법과 라우트된 이벤트 데이터를 처리할 수 있는 처리기를 작성하는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]에서 요소는 요소 트리 구조로 정렬됩니다. 부모 요소는 초기에 요소 트리의 자식 요소에 의해 발생된 이벤트 처리에 참여할 수 있습니다. 이는 이벤트 라우팅으로 인해 가능합니다.  
  
 라우트된 이벤트는 일반적으로 두 가지 라우팅 전략(버블링 또는 터널링) 중 하나를 따릅니다. 이 예제에서는 버블링 이벤트에 중점을 두고 사용 하 여 <xref:System.Windows.Controls.Primitives.ButtonBase.Click?displayProperty=nameWithType> 라우팅 작동 방법을 보여 주는 이벤트를 합니다.  
  
 다음 예제에서는 두 개의 <xref:System.Windows.Controls.Button> 제어 하 고 사용 하 여 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 특성은이 예제는 공통 부모 요소에 이벤트 처리기를 연결 하는 구문을 <xref:System.Windows.Controls.StackPanel>합니다. 각 개별 이벤트 처리기를 연결 하는 대신 <xref:System.Windows.Controls.Button> 자식 요소를이 예제에서는 특성 구문을 사용 하 여 이벤트 처리기를 연결 합니다 <xref:System.Windows.Controls.StackPanel> 부모 요소입니다. 이 이벤트 처리 패턴은 처리기가 연결되어 있는 요소의 수를 줄이는 기술로서 이벤트 라우팅을 사용하는 방법을 보여 줍니다. 각각에 대 한 모든 버블링 이벤트 <xref:System.Windows.Controls.Button> 부모 요소를 통해 경로입니다.  
  
 부모에 유의 <xref:System.Windows.Controls.StackPanel> 요소를 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 특성을 부분적으로 정규화 하는 이름으로 지정 하는 이벤트 이름을 <xref:System.Windows.Controls.Button> 클래스입니다. 합니다 <xref:System.Windows.Controls.Button> 클래스는를 <xref:System.Windows.Controls.Primitives.ButtonBase> 파생 된 클래스는 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 해당 멤버 목록에 이벤트입니다. 처리중인 이벤트가 라우트된 이벤트 처리기가 연결된 요소의 멤버 목록에 있지 않은 경우 이벤트 처리기 연결을 위해 이러한 부분 한정 기술이 필요합니다.  
  
 [!code-xaml[RoutedEventHandle#XAML](~/samples/snippets/csharp/VS_Snippets_Wpf/RoutedEventHandle/CSharp/default.xaml#xaml)]  
  
 다음 예제에서는 처리 된 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 이벤트입니다.  이 예제에서는 이벤트를 처리하는 요소와 이벤트를 발생시키는 요소를 보여 줍니다. 이벤트 처리기는 두 버튼 중 하나를 클릭할 때 실행됩니다.  
  
 [!code-csharp[RoutedEventHandle#Handler](~/samples/snippets/csharp/VS_Snippets_Wpf/RoutedEventHandle/CSharp/default.xaml.cs#handler)]
 [!code-vb[RoutedEventHandle#Handler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/RoutedEventHandle/VisualBasic/MainWindow.xaml.vb#handler)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.RoutedEvent>
- [입력 개요](input-overview.md)
- [라우트된 이벤트 개요](routed-events-overview.md)
- [방법 항목](events-how-to-topics.md)
- [XAML 구문 정보](xaml-syntax-in-detail.md)
