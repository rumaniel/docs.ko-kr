---
title: '방법: 요소에 표시기(Adorner) 바인딩'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- UIElements [WPF], binding adorners to
- adorners [WPF], binding to specified UIElements
ms.assetid: b2101611-a0ee-4137-bdb8-9b3673d2e6b9
ms.openlocfilehash: e8c7eb929042bfe1455bfc9bf459fc466de5c397
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69923489"
---
# <a name="how-to-bind-an-adorner-to-an-element"></a>방법: 요소에 표시기(Adorner) 바인딩
이 예제에서는 지정 <xref:System.Windows.UIElement>된에 표시기를 프로그래밍 방식으로 바인딩하는 방법을 보여 줍니다.  
  
## <a name="example"></a>예제  
 표시기를 특정 <xref:System.Windows.UIElement>에 바인딩하려면 다음 단계를 수행 합니다.  
  
1. 표시 될 `static` 에 <xref:System.Windows.Documents.AdornerLayer.GetAdornerLayer%2A> 대 한 <xref:System.Windows.Documents.AdornerLayer> <xref:System.Windows.UIElement> 개체를 가져오려면 메서드를 호출 합니다. <xref:System.Windows.Documents.AdornerLayer.GetAdornerLayer%2A>지정 된 **UIElement**에서 시작 하 여 시각적 트리를 탐색 하 고 찾은 첫 번째 표시기 계층을 반환 합니다. (표시기 계층이 없으면 메서드가 null을 반환합니다.)  
  
2. 메서드를 <xref:System.Windows.Documents.AdornerLayer.Add%2A> 호출 하 여 표시기를 대상 **UIElement**에 바인딩합니다.  
  
 다음 예제에서는 SimpleCircleAdorner (위에 표시 됨) <xref:System.Windows.Controls.TextBox> 를 *mytextbox*라는에 바인딩합니다.  
  
 [!code-csharp[Adorners_SimpleCircleAdorner#_AdornSingleElement](~/samples/snippets/csharp/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/CSharp/Window1.xaml.cs#_adornsingleelement)]
 [!code-vb[Adorners_SimpleCircleAdorner#_AdornSingleElement](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/VisualBasic/Window1.xaml.vb#_adornsingleelement)]  
  
> [!NOTE]
> [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]를 사용하여 표시기를 다른 요소에 바인딩하는 것은 현재 지원되지 않습니다.  
  
## <a name="see-also"></a>참고자료

- [표시기 개요](adorners-overview.md)
