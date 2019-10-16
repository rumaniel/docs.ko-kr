---
title: '방법: 코드를 사용하여 이벤트 처리기 추가'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- event handlers [WPF], adding
- XAML [WPF], adding event handlers
ms.assetid: 269c61e0-6bd9-4291-9bed-1c5ee66da486
ms.openlocfilehash: 017b32dc07f62cc4553a84f7b91687fb34a53c65
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69937468"
---
# <a name="how-to-add-an-event-handler-using-code"></a>방법: 코드를 사용하여 이벤트 처리기 추가
이 예제에서는 코드를 사용 하 여 요소에 이벤트 처리기를 추가 하는 방법을 보여 줍니다.  
  
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 요소에 이벤트 처리기를 추가 하 고 요소를 포함 하는 태그 페이지가 이미 로드 된 경우 코드를 사용 하 여 처리기를 추가 해야 합니다. 또는를 사용 하 여 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]요소를 선언 하지 않고 코드를 사용 하 여 응용 프로그램에 대 한 요소 트리를 완전히 빌드하는 경우 특정 메서드를 호출 하 여 생성 된 요소 트리에 이벤트 처리기를 추가할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예에서는에서 <xref:System.Windows.Controls.Button> [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]초기에 정의 된 기존 페이지에 새를 추가 합니다. 코드 숨겨진 파일은 이벤트 처리기 메서드를 구현 하 고 해당 메서드를의 새 이벤트 처리기 <xref:System.Windows.Controls.Button>로 추가 합니다.  
  
 이 C# 예제에서는 `+=` 연산자를 사용 하 여 이벤트에 처리기를 할당 합니다. 이 연산자는 CLR (공용 언어 런타임) 이벤트 처리 모델에서 처리기를 할당 하는 데 사용 되는 연산자와 동일 합니다. Microsoft Visual Basic는 이벤트 처리기를 추가 하는 수단으로이 연산자를 지원 하지 않습니다. 대신, 다음 두 가지 방법 중 하나가 필요 합니다.  
  
- 메서드를 `AddressOf` 연산자와 함께 사용 하 여 이벤트 처리기 구현을 참조 합니다. <xref:System.Windows.UIElement.AddHandler%2A>  
  
- 키워드를 `Handles` 이벤트 처리기 정의의 일부로 사용 합니다. 이 기법은 여기에 표시 되지 않습니다. [Visual Basic 및 WPF 이벤트 처리를](visual-basic-and-wpf-event-handling.md)참조 하세요.  
  
 [!code-xaml[RoutedEventAddRemoveHandler#XAML](~/samples/snippets/csharp/VS_Snippets_Wpf/RoutedEventAddRemoveHandler/CSharp/default.xaml#xaml)]  
  
 [!code-csharp[RoutedEventAddRemoveHandler#Handler](~/samples/snippets/csharp/VS_Snippets_Wpf/RoutedEventAddRemoveHandler/CSharp/default.xaml.cs#handler)]
 [!code-vb[RoutedEventAddRemoveHandler#Handler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/RoutedEventAddRemoveHandler/VisualBasic/default.xaml.vb#handler)]  
  
> [!NOTE]
> 처음에 구문 분석 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 된 페이지에서 이벤트 처리기를 추가 하는 것이 훨씬 더 간단 합니다. 이벤트 처리기를 추가 하려는 개체 요소 내에서 처리할 이벤트의 이름과 일치 하는 특성을 추가 합니다. 그런 다음 해당 특성의 값을 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 페이지의 코드 파일에 정의 된 이벤트 처리기 메서드의 이름으로 지정 합니다. 자세한 내용은 [XAML 개요 (WPF)](xaml-overview-wpf.md) 또는 [라우트된 이벤트 개요](routed-events-overview.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [라우트된 이벤트 개요](routed-events-overview.md)
- [방법 항목](events-how-to-topics.md)
