---
title: '방법: 이벤트 처리기에서 원본 요소 찾기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- source element in event handlers [WPF]
- event handlers [WPF], finding source element in
ms.assetid: 85f71c5a-b714-4c65-9711-7d905c2bbe98
ms.openlocfilehash: 9a49878c9ad8313903df4506796998fd43e2e749
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61757510"
---
# <a name="how-to-find-the-source-element-in-an-event-handler"></a>방법: 이벤트 처리기에서 원본 요소 찾기
이 예제에서는 이벤트 처리기에서 소스 요소를 찾는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 다음 예제는 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 코드 숨김 파일에 선언 된 이벤트 처리기입니다. 사용자가 처리기에 연결 된 단추를 클릭 하면 처리기 속성 값을 변경 합니다. 처리기 코드를 사용 하는 <xref:System.Windows.RoutedEventArgs.Source%2A> 속성 변경 이벤트 인수에서 보고 되는 라우트된 이벤트 데이터의는 <xref:System.Windows.FrameworkElement.Width%2A> 속성 값에는 <xref:System.Windows.RoutedEventArgs.Source%2A> 요소.  
  
 [!code-xaml[RoutedEventSource#XAMLHandler](~/samples/snippets/csharp/VS_Snippets_Wpf/RoutedEventSource/CSharp/default.xaml#xamlhandler)]  
  
 [!code-csharp[RoutedEventSource#Handler](~/samples/snippets/csharp/VS_Snippets_Wpf/RoutedEventSource/CSharp/default.xaml.cs#handler)]
 [!code-vb[RoutedEventSource#Handler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/RoutedEventSource/VisualBasic/default.xaml.vb#handler)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.RoutedEventArgs>
- [라우트된 이벤트 개요](routed-events-overview.md)
- [방법 항목](events-how-to-topics.md)
