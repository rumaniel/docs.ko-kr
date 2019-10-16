---
title: '방법: 페이지가 브라우저에 호스트되는지 여부 확인'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- hosted pages in browser [WPF]
- pages [WPF], hosted in browser
ms.assetid: 737e0f26-8371-49b4-9579-70879e51e1aa
ms.openlocfilehash: d154de2f885101d1bd0c4613dfb1604be8acbe6a
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61947812"
---
# <a name="how-to-determine-if-a-page-is-browser-hosted"></a>방법: 페이지가 브라우저에 호스트되는지 여부 확인
확인 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Controls.Page> 브라우저에서 호스팅됩니다.  
  
## <a name="example"></a>예제  
 <xref:System.Windows.Controls.Page> 알 수 없는 호스트 수 및 결과적으로 호스트를 비롯 한 여러 가지 형식으로 로드할 수는 <xref:System.Windows.Controls.Frame>, <xref:System.Windows.Navigation.NavigationWindow>, 또는 브라우저. 라이브러리 어셈블리를 하나 이상의 페이지를 포함 하 고는 참조 되는 여러 독립 실행형으로 탐색할 수 있는 경우 발생할 수 있습니다 ([!INCLUDE[TLA#tla_xbap](../../../../includes/tlasharptla-xbap-md.md)]) 응용 프로그램을 호스트 합니다.  
  
 다음 예제에 사용 하는 방법을 보여 줍니다. <xref:System.Windows.Interop.BrowserInteropHelper.IsBrowserHosted%2A?displayProperty=nameWithType> 여부를 확인 하는 <xref:System.Windows.Controls.Page> 브라우저에서 호스팅됩니다.  
  
 [!code-csharp[HOWTOBrowserInteropHelperSnippets#IsBrowserHostedCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTOBrowserInteropHelperSnippets/CSharp/Page1.xaml.cs#isbrowserhostedcode)]
 [!code-vb[HOWTOBrowserInteropHelperSnippets#IsBrowserHostedCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTOBrowserInteropHelperSnippets/visualbasic/page1.xaml.vb#isbrowserhostedcode)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.Frame>
- <xref:System.Windows.Controls.Page>
