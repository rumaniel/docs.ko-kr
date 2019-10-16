---
title: '방법: 페이지 새로 고침'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- pages [WPF], refreshing
- refreshing pages [WPF]
ms.assetid: 06dd1bbd-81c4-40ad-ac0d-7a5b326b1465
ms.openlocfilehash: 71a71c91384a8905413358d023531afec23f2d41
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61947670"
---
# <a name="how-to-refresh-a-page"></a>방법: 페이지 새로 고침
호출 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Navigation.NavigationWindow.Refresh%2A> 의 현재 콘텐츠를 새로 고칠 메서드는 <xref:System.Windows.Navigation.NavigationWindow>합니다.  
  
## <a name="example"></a>예제  
 <xref:System.Windows.Navigation.NavigationWindow.Refresh%2A> 현재 콘텐츠를 새로 고칩니다는 <xref:System.Windows.Navigation.NavigationWindow> 해당 원본에서 다시 로드 해야 합니다.  
  
 [!code-csharp[HOWTONavigationSnippets#NavigateRefreshCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTONavigationSnippets/CSharp/MainWindow.xaml.cs#navigaterefreshcode)]
 [!code-vb[HOWTONavigationSnippets#NavigateRefreshCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTONavigationSnippets/visualbasic/mainwindow.xaml.vb#navigaterefreshcode)]
