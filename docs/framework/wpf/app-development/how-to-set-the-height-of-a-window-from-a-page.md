---
title: '방법: 페이지에서 창 높이 설정'
ms.date: 03/30/2017
helpviewer_keywords:
- windows [WPF], setting height from a page
- pages [WPF], setting window height from
- height of window [WPF], setting from a page
ms.assetid: 4e4488ff-ab5c-4ee9-81a4-e1addb55c5cc
ms.openlocfilehash: c1041af88241011b51c96d7b61423344a32b25ca
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69940796"
---
# <a name="how-to-set-the-height-of-a-window-from-a-page"></a>방법: 페이지에서 창 높이 설정
이 예제에서는에서 <xref:System.Windows.Controls.Page>창의 높이를 설정 하는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 는 <xref:System.Windows.Controls.Page> 를 설정 <xref:System.Windows.Controls.Page.WindowHeight%2A>하 여 호스트 창의 높이를 설정할 수 있습니다. 이 속성을 사용 <xref:System.Windows.Controls.Page> 하면에서 호스트 하는 창의 형식을 명시적으로 알지 못합니다.  
  
> [!NOTE]
> 을 사용 하 여 <xref:System.Windows.Controls.Page.WindowHeight%2A>창의 높이를 설정 하려면가 <xref:System.Windows.Controls.Page> 창의 자식 이어야 합니다.  
  
 [!code-xaml[HOWTONavigationSnippets#SetPageWindowHeightXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTONavigationSnippets/CSharp/SetWindowHeightPage.xaml#setpagewindowheightxaml)]
