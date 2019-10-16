---
title: '방법: 탐색 기록을 앞으로 또는 뒤로 탐색'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- history [WPF], navigating forward
- navigation [WPF], through navigation history (forward)
ms.assetid: 5939d574-5f53-469e-85f5-1f2b13607caa
ms.openlocfilehash: 76a78debdce14123cc465ac9abf4db906fe0a2df
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69961347"
---
# <a name="how-to-navigate-forward-or-back-through-navigation-history"></a>방법: 탐색 기록을 앞으로 또는 뒤로 탐색
이 예제에서는 탐색 기록에서 항목으로 앞으로 또는 뒤로 이동 하는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 다음 호스트의 콘텐츠에서 실행 되는 코드는 탐색 기록을 앞뒤로 탐색할 수 있으며 한 번에 한 항목만 탐색할 수 있습니다.  
  
- <xref:System.Windows.Navigation.NavigationWindow>사용 하 여<xref:System.Windows.Navigation.NavigationService>  
  
- <xref:System.Windows.Controls.Frame>사용 하 여<xref:System.Windows.Navigation.NavigationService>  
  
- Internet Explorer  
  
 한 항목 앞으로 이동 하려면 먼저 **CanGoForward** 속성을 검사 하 여 전방 탐색 기록에 항목이 있는지 확인 해야 합니다. 한 항목 앞으로 이동 하려면 **Goforward** 메서드를 호출 합니다. 이는 다음 예제에 설명 되어 있습니다.  
  
 [!code-csharp[HOWTONavigationSnippets#NavigateForwardCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTONavigationSnippets/CSharp/HomePage.xaml.cs#navigateforwardcode)]
 [!code-vb[HOWTONavigationSnippets#NavigateForwardCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTONavigationSnippets/visualbasic/homepage.xaml.vb#navigateforwardcode)]  
  
 한 항목 뒤로 이동 하려면 먼저 **CanGoBack** 속성을 검사 하 여 후방 탐색 기록에 항목이 있는지 확인 해야 합니다. 한 항목 뒤로 이동 하려면 **GoBack** 메서드를 호출 합니다. 이는 다음 예제에 설명 되어 있습니다.  
  
 [!code-csharp[HOWTONavigationSnippets#NavigateBackCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTONavigationSnippets/CSharp/HomePage.xaml.cs#navigatebackcode)]
 [!code-vb[HOWTONavigationSnippets#NavigateBackCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTONavigationSnippets/visualbasic/homepage.xaml.vb#navigatebackcode)]  
  
 **CanGoForward**, **goforward**, **CanGoBack**및 **GoBack** 은, <xref:System.Windows.Navigation.NavigationWindow> <xref:System.Windows.Controls.Frame>및 <xref:System.Windows.Navigation.NavigationService>에서 구현 됩니다.  
  
> [!NOTE]
> **Goforward**를 호출 하 고 전방 탐색 기록에 항목이 없거나, **GoBack**을 호출 하 고 후방 탐색 <xref:System.InvalidOperationException> 기록에 항목이 없는 경우이 throw 됩니다.
