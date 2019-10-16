---
title: '방법: 탐색 기록을 뒤로 탐색'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- history [WPF], navigating back
- navigation [WPF], through navigation history (back)
ms.assetid: 9343234b-d864-441d-b8a7-d895cba80a87
ms.openlocfilehash: 53b32e145390d7052262042c7a793699c163b373
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69969347"
---
# <a name="how-to-navigate-back-through-navigation-history"></a>방법: 탐색 기록을 뒤로 탐색
이 예제에서는 후방 탐색 기록에서 항목으로 이동 하는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 에서 호스트 <xref:System.Windows.Navigation.NavigationWindow> <xref:System.Windows.Controls.Frame> 되는 콘텐츠 (또는 Internet Explorer)에서 실행 되는 코드는 탐색 기록을 통해 다시 탐색할 수 있으며 한 번에 하나의 항목만 탐색할 수 있습니다. <xref:System.Windows.Navigation.NavigationService>  
  
 한 항목을 뒤로 이동 하려면 먼저 **CanGoBack** 속성을 검사 하 여 후방 탐색 기록에 항목이 있는지 확인 하 고, **GoBack** 메서드를 호출 하 여 한 항목 뒤로 이동 합니다. 이는 다음 예제에 설명 되어 있습니다.  
  
 [!code-csharp[HOWTONavigationSnippets#NavigateBackCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTONavigationSnippets/CSharp/HomePage.xaml.cs#navigatebackcode)]
 [!code-vb[HOWTONavigationSnippets#NavigateBackCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTONavigationSnippets/visualbasic/homepage.xaml.vb#navigatebackcode)]  
  
 **CanGoBack** 및 **GoBack** 은, <xref:System.Windows.Controls.Frame>및 <xref:System.Windows.Navigation.NavigationWindow> <xref:System.Windows.Navigation.NavigationService>에서 구현 됩니다.  
  
> [!NOTE]
> **GoBack**을 호출 하 고 후방 탐색 기록 <xref:System.InvalidOperationException> 에 항목이 없는 경우이 발생 합니다.
