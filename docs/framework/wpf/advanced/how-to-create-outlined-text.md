---
title: '방법: 윤곽선이 있는 텍스트 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- typography [WPF], linear gradient brush
- outlined text [WPF]
- gradient brush [WPF]
- linear gradient brush [WPF]
- typography [WPF], outline effects
ms.assetid: 4aa3cf6e-1953-4f26-8230-7c1409e5f28d
ms.openlocfilehash: 237bdc097cd2a3fbfff6dd79bce401c2d091e211
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61776772"
---
# <a name="how-to-create-outlined-text"></a>방법: 윤곽선이 있는 텍스트 만들기
대부분의 경우, 장식의 텍스트 문자열에 추가 하는 경우에 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 불연속 문자 또는 문자 모양을 컬렉션과 관련 된 텍스트를 사용 하는 응용 프로그램입니다. 예를 들어 선형 그라데이션 브러시를 만들고 적용 하는 <xref:System.Windows.Controls.Control.Foreground%2A> 의 속성을 <xref:System.Windows.Controls.TextBox> 개체입니다. 을 표시 하거나 텍스트 상자를 편집할 때 선형 그라데이션 브러시 현재 텍스트 문자열에서 문자 집합에 자동으로 적용 됩니다.  
  
 ![선형 그라데이션 브러시로 표시된 텍스트](./media/how-to-create-outlined-text/text-linear-gradient.jpg)    
  
 그러나 변환할 수도 있습니다 텍스트를 <xref:System.Windows.Media.Geometry> 개체를 다른 유형의 시각적 서식 있는 텍스트를 만들 수 있습니다. 예를 들어, 만들 수 있습니다는 <xref:System.Windows.Media.Geometry> 텍스트 문자열의 윤곽선을 기준으로 하는 개체입니다.  
  
 ![선형 그라데이션 브러시를 사용하여 표시한 텍스트 윤곽선](./media/how-to-create-outlined-text/text-outline-linear-gradient.jpg)  
  
 텍스트 변환 되 면을 <xref:System.Windows.Media.Geometry> 개체를 더 이상 문자 컬렉션이-텍스트 문자열의에서 문자를 수정할 수 없습니다. 그러나 스트로크와 채우기 속성을 수정하여 변환된 텍스트의 모양에 영향을 줄 수 있습니다. 스트로크는 변환된 텍스트의 윤곽선을 나타내고, 채우기는 변환된 텍스트의 윤곽선 내부에 있는 영역을 나타냅니다.  
  
 다음 예제에서는 스트로크 및 채우기 변환 된 텍스트를 수정 하 여 시각 효과 만드는 여러 가지 방법을 보여 줍니다.  
  
 ![채우기와 스트로크에 다른 색을 사용하는 텍스트](./media/how-to-create-outlined-text/fill-stroke-text-effect.jpg)  
  
 ![스트로크에 이미지 브러시가 적용된 텍스트](./media/how-to-create-outlined-text/image-brush-application.jpg)
  
 경계 상자 사각형 또는 변환된 된 텍스트의 강조 표시를 수정 하는 것도 가능 합니다. 다음 예제에서는 스트로크 및 변환 된 텍스트의 강조 표시를 수정 하 여 시각 효과를 만드는 방법을 보여 줍니다.  
  
 ![스트로크를 강조 표시에 이미지 브러시가 적용 된 텍스트](./media/how-to-create-outlined-text/image-brush-text-application.jpg)

## <a name="example"></a>예제  
 텍스트를 변환 하는 <xref:System.Windows.Media.Geometry> 개체가 사용 하는 <xref:System.Windows.Media.FormattedText> 개체입니다. 이 개체를 만든 후 사용할 수 있습니다는 <xref:System.Windows.Media.FormattedText.BuildGeometry%2A> 하 고 <xref:System.Windows.Media.FormattedText.BuildHighlightGeometry%2A> 텍스트를 변환 하는 메서드가 <xref:System.Windows.Media.Geometry> 개체입니다. 첫 번째 메서드가 반환 된 형식이 지정 된 텍스트의 기 하 도형 두 번째 메서드는 기 하 도형 서식 있는 텍스트의 경계 상자를 반환 합니다. 다음 코드 예제에는 만드는 방법을 보여 줍니다는 <xref:System.Windows.Media.FormattedText> 개체 및 서식 있는 텍스트 및 해당 경계 상자 기 하 도형 검색 합니다.  
  
 [!code-csharp[OutlineTextControlViewer#CreateText](~/samples/snippets/csharp/VS_Snippets_Wpf/OutlineTextControlViewer/CSharp/OutlineTextControl.cs#createtext)]
 [!code-vb[OutlineTextControlViewer#CreateText](~/samples/snippets/visualbasic/VS_Snippets_Wpf/OutlineTextControlViewer/visualbasic/outlinetextcontrol.vb#createtext)]  
  
 검색을 표시 하기 위해 합니다 <xref:System.Windows.Media.Geometry> 개체에 액세스 해야 합니다 <xref:System.Windows.Media.DrawingContext> 변환된 된 텍스트를 표시 하는 개체의 합니다. 이 코드 예제에서이 사용자 정의 렌더링을 지 원하는 클래스에서 파생 되는 사용자 지정 컨트롤 개체를 만들어서 이루어집니다.  
  
 표시할 <xref:System.Windows.Media.Geometry> 에 대 한 재정의 제공 하는 사용자 지정 컨트롤에서 개체를 <xref:System.Windows.UIElement.OnRender%2A> 메서드. 재정의 된 메서드를 사용 해야 합니다 <xref:System.Windows.Media.DrawingContext.DrawGeometry%2A> 그릴 메서드는 <xref:System.Windows.Media.Geometry> 개체입니다.  
  
 [!code-csharp[OutlineTextControlViewer#OnRender](~/samples/snippets/csharp/VS_Snippets_Wpf/OutlineTextControlViewer/CSharp/OutlineTextControl.cs#onrender)]
 [!code-vb[OutlineTextControlViewer#OnRender](~/samples/snippets/visualbasic/VS_Snippets_Wpf/OutlineTextControlViewer/visualbasic/outlinetextcontrol.vb#onrender)]  
  
  예제 사용자 지정 사용자 컨트롤 개체의 원본에 대 한 참조 [OutlineTextControl.cs에 대 한 C# ](https://github.com/dotnet/samples/blob/master/snippets/csharp/VS_Snippets_Wpf/OutlineTextControlViewer/CSharp/OutlineTextControl.cs) 하 고 [Visual basic OutlineTextControl.vb](https://github.com/dotnet/samples/blob/master/snippets/visualbasic/VS_Snippets_Wpf/OutlineTextControlViewer/visualbasic/outlinetextcontrol.vb). 
  
## <a name="see-also"></a>참고자료

- [서식 있는 텍스트 그리기](drawing-formatted-text.md)
