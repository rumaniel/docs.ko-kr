---
title: '방법: 페이지 로드 중지'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- pages [WPF], stopping from loading
- methods [WPF], Stoploading
- events [WPF], NavigationStopped
- NavigationStopped properties [WPF]
- stopping pages from loading [WPF]
- loading [WPF], stopping
ms.assetid: e2b695b0-517e-462c-8ccf-90cc8d6ba864
ms.openlocfilehash: c5694bb2cb6c618cd84bad3dc893ae3855e44892
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62006683"
---
# <a name="how-to-stop-a-page-from-loading"></a>방법: 페이지 로드 중지
호출 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Navigation.NavigationWindow.StopLoading%2A> 다운로드 마치기 전에 콘텐츠 탐색을 중지 하는 방법입니다.  
  
## <a name="example"></a>예제  
 <xref:System.Windows.Navigation.NavigationWindow.StopLoading%2A> 요청 된 콘텐츠의 다운로드를 중지 하 고 하면는 <xref:System.Windows.Navigation.NavigationWindow.NavigationStopped> 이벤트가 발생 합니다.  
  
 [!code-csharp[HOWTONavigationSnippets#NavigateStopLoadingCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTONavigationSnippets/CSharp/MainWindow.xaml.cs#navigatestoploadingcode)]
 [!code-vb[HOWTONavigationSnippets#NavigateStopLoadingCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTONavigationSnippets/visualbasic/mainwindow.xaml.vb#navigatestoploadingcode)]
