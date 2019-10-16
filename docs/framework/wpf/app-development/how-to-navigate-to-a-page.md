---
title: '방법: 페이지 탐색'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- pages [WPF], navigating to
- navigation [WPF], to page
ms.assetid: 2a556fc0-748b-417f-a58a-0d05a7afb66f
ms.openlocfilehash: 38814268c9bb271ad3d88d549fb6ec4c6cbfed40
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69966036"
---
# <a name="how-to-navigate-to-a-page"></a>방법: 페이지 탐색
이 예제에서는에서 <xref:System.Windows.Navigation.NavigationWindow>페이지를 탐색할 수 있는 여러 가지 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 에서 <xref:System.Windows.Navigation.NavigationWindow> 다음 중 하나를 사용 하 여 페이지로 이동할 수 있습니다.  
  
- <xref:System.Windows.Navigation.NavigationWindow.Source%2A> 속성  
  
- <xref:System.Windows.Navigation.NavigationWindow.Navigate%2A> 메서드  
  
 [!code-csharp[HOWTONavigationSnippets#NavigateToPageCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTONavigationSnippets/CSharp/MainWindow.xaml.cs#navigatetopagecode)]
 [!code-vb[HOWTONavigationSnippets#NavigateToPageCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTONavigationSnippets/visualbasic/mainwindow.xaml.vb#navigatetopagecode)]  
  
> [!NOTE]
> [!INCLUDE[TLA#tla_uri#initcap#plural](../../../../includes/tlasharptla-urisharpinitcapsharpplural-md.md)] 상대 또는 절대 수 있습니다. 자세한 내용은 [WPF의 Pack URI](pack-uris-in-wpf.md)를 참조하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.Frame>
- <xref:System.Windows.Controls.Page>
- <xref:System.Windows.Navigation.NavigationService>
