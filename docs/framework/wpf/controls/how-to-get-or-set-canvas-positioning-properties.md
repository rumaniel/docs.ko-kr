---
title: '방법: 캔버스 위치 지정 속성 가져오기 또는 설정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Canvas control [WPF], setting positioning properties
ms.assetid: 1636b950-2b5a-4507-8a10-c5034cc58b1c
ms.openlocfilehash: 06508e1198736ccb1cbda41641dff4bc634ef82b
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61910483"
---
# <a name="how-to-get-or-set-canvas-positioning-properties"></a>방법: 캔버스 위치 지정 속성 가져오기 또는 설정
위치 지정 메서드를 사용 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Controls.Canvas> 요소 자식 콘텐츠의 위치입니다. 콘텐츠를 사용 하 여이 예제는 <xref:System.Windows.Controls.ListBoxItem> 나타내는 위치 값 및 값의 인스턴스로 변환 <xref:System.Double>, 위치 지정에 대 한 필수 인수는 합니다. 값 다음 문자열로 다시 변환 되어에 텍스트로 표시 되는 <xref:System.Windows.Controls.TextBlock> 를 사용 하 여 요소를 <xref:System.Windows.Controls.Canvas.GetLeft%2A> 메서드.  
  
## <a name="example"></a>예제  
 다음 예제는 <xref:System.Windows.Controls.ListBox> 요소를 선택할 수 있는 11 <xref:System.Windows.Controls.ListBoxItem> 요소입니다. 합니다 <xref:System.Windows.Controls.Primitives.Selector.SelectionChanged> 이벤트 트리거는 `ChangeLeft` 후속 코드 블록이 정의 하는 사용자 지정 메서드.  
  
 각 <xref:System.Windows.Controls.ListBoxItem> 나타냅니다는 <xref:System.Double> 값인 인수 중 하나는 <xref:System.Windows.Controls.Canvas.SetLeft%2A> 메서드의 <xref:System.Windows.Controls.Canvas> 허용 합니다. 사용 하기 위해를 <xref:System.Windows.Controls.ListBoxItem> 의 인스턴스를 나타내는 <xref:System.Double>를 먼저 변환 해야 합니다 <xref:System.Windows.Controls.ListBoxItem> 올바른 데이터 형식으로.  
  
 [!code-xaml[CanvasPositioningProperties#1](~/samples/snippets/csharp/VS_Snippets_Wpf/CanvasPositioningProperties/CSharp/Window1.xaml#1)]  
  
 사용자가 변경 될 때 합니다 <xref:System.Windows.Controls.ListBox> 호출 선택은 `ChangeLeft` 사용자 지정 메서드. 이 메서드는 전달를 <xref:System.Windows.Controls.ListBoxItem> 에 <xref:System.Windows.LengthConverter> 변환 하는 개체를 <xref:System.Windows.Controls.ContentControl.Content%2A> 의 <xref:System.Windows.Controls.ListBoxItem> 인스턴스에 <xref:System.Double> (이 값으로 변환 된 이미는 <xref:System.String> 를 사용 하 여를 <xref:System.Windows.Controls.Control.ToString%2A> 메서드)입니다. 이 값은 다음에 다시 전달 합니다 <xref:System.Windows.Controls.Canvas.SetLeft%2A> 및 <xref:System.Windows.Controls.Canvas.GetLeft%2A> 의 메서드 <xref:System.Windows.Controls.Canvas> 의 위치를 변경 하려면를 `text1` 개체입니다.  
  
 [!code-csharp[CanvasPositioningProperties#2](~/samples/snippets/csharp/VS_Snippets_Wpf/CanvasPositioningProperties/CSharp/Window1.xaml.cs#2)]
 [!code-vb[CanvasPositioningProperties#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CanvasPositioningProperties/VisualBasic/Window1.xaml.vb#2)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.Canvas>
- <xref:System.Windows.Controls.ListBoxItem>
- <xref:System.Windows.LengthConverter>
- [패널 개요](panels-overview.md)
