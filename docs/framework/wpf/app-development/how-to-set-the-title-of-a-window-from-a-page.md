---
title: '방법: 페이지에서 창 제목 설정'
ms.date: 03/30/2017
helpviewer_keywords:
- windows [WPF], setting title from a page
- title of window [WPF], setting from a page
- pages [WPF], setting window title from
ms.assetid: fecf0d19-3eb6-4f8c-a44f-ff1b6f2b34b3
ms.openlocfilehash: 0f618af89965822b0df96a264997dabd9cae7608
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69940782"
---
# <a name="how-to-set-the-title-of-a-window-from-a-page"></a>방법: 페이지에서 창 제목 설정
이 예제에서는이 호스팅되는 창의 <xref:System.Windows.Controls.Page> 제목을 설정 하는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 페이지는 다음과 같이 <xref:System.Windows.Controls.Page.WindowTitle%2A> 속성을 설정 하 여 호스트 하는 창의 제목을 변경할 수 있습니다.  
  
 [!code-xaml[HOWTONavigationSnippets#SetPageWindowTitleXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTONavigationSnippets/CSharp/SetWindowTitlePage.xaml#setpagewindowtitlexaml)]  
  
> [!NOTE]
> 페이지의 <xref:System.Windows.Controls.Page.Title%2A> 속성을 설정 해도 창 제목 값은 변경 되지 않습니다. 대신, <xref:System.Windows.Controls.Page.Title%2A> 탐색 기록에서 페이지 항목의 이름을 지정 합니다.
