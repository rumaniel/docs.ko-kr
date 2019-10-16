---
title: '방법: 프로그래밍 방식으로 TextWrapping 속성 변경'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- documents [WPF], changing TextWrapping property programmatically
- TextWrapping property [WPF], changing programmatically
ms.assetid: 30d25554-4c82-4df9-a8d6-35683a4a13bb
ms.openlocfilehash: 21ca31d24121492fe6927cd533d5b3c0785b5a28
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61776664"
---
# <a name="how-to-change-the-textwrapping-property-programmatically"></a>방법: 프로그래밍 방식으로 TextWrapping 속성 변경
## <a name="example"></a>예제  
 다음 코드 예제에서는 값을 변경 하는 방법을 보여 줍니다는 <xref:System.Windows.Controls.TextBlock.TextWrapping%2A> 속성 프로그래밍 방식으로 합니다.  
  
 세 <xref:System.Windows.Controls.Button> 요소 안에 배치 되는 <xref:System.Windows.Controls.StackPanel> 요소에 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]. 각 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 에 대 한 이벤트를 <xref:System.Windows.Controls.Button> 코드에서 이벤트 처리기에 해당 합니다. 이벤트 처리기와 같은 이름을 사용 합니다 <xref:System.Windows.Controls.TextBlock.TextWrapping%2A> 값에 적용 됩니다 `txt2` 단추를 클릭할 때입니다. 에 텍스트 뿐만 `txt1` (을 <xref:System.Windows.Controls.TextBlock> 에 표시 되지 않습니다는 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]) 속성에 변경 내용을 반영 하도록 업데이트 됩니다.  
  
 [!code-xaml[TextWrapProperty#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextWrapProperty/VisualBasic/Pane1.xaml#1)]  
  
 [!code-csharp[TextWrapProperty#2](~/samples/snippets/csharp/VS_Snippets_Wpf/TextWrapProperty/CSharp/Window1.xaml.cs#2)]
 [!code-vb[TextWrapProperty#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextWrapProperty/VisualBasic/Pane1.xaml.vb#2)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.TextBlock.TextWrapping%2A>
- <xref:System.Windows.TextWrapping>
