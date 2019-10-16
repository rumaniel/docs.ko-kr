---
title: '방법: 리플렉션 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- creating reflections [WPF]
- brushes [WPF], creating reflections
- reflections [WPF], creating
ms.assetid: 4f017e16-ab80-43c7-98df-03b6bddbb203
ms.openlocfilehash: 61b597cd36fcf0d60f215d9b5403f3b42b21dec4
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61904226"
---
# <a name="how-to-create-a-reflection"></a>방법: 리플렉션 만들기
사용 하는 방법을 보여 주는이 예제는 <xref:System.Windows.Media.VisualBrush> 반사를 만들려고 합니다. 때문에 <xref:System.Windows.Media.VisualBrush> 기존 시각적 개체를 표시할 수 있습니다, 리플렉션 및 확대와 같은 흥미로운 시각적 효과 생성 하기 위해이 기능을 사용할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 <xref:System.Windows.Media.VisualBrush> 의 반사 만들기에 <xref:System.Windows.Controls.Border> 여러 요소를 포함 하는 합니다. 다음 그림에서는 이 예제가 생성하는 출력을 보여 줍니다.  
  
 ![시각적 개체를 반영](./media/graphicsmm-visualbrush-reflection-small.jpg "graphicsmm_visualbrush_reflection_small")  
반사된 표시 개체  
  
 [!code-csharp[visualbrush_markup_snip#GraphicsMMVisualBrushReflectionExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/visualbrush_markup_snip/CSharp/ReflectionExample.cs#graphicsmmvisualbrushreflectionexamplewholepage)]
 [!code-vb[visualbrush_markup_snip#GraphicsMMVisualBrushReflectionExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/visualbrush_markup_snip/visualbasic/reflectionexample.vb#graphicsmmvisualbrushreflectionexamplewholepage)]
 [!code-xaml[visualbrush_markup_snip#GraphicsMMVisualBrushReflectionExampleWholePage](~/samples/snippets/xaml/VS_Snippets_Wpf/visualbrush_markup_snip/XAML/ReflectionExample.xaml#graphicsmmvisualbrushreflectionexamplewholepage)]  
  
 화면의 일부를 확대 하는 방법 및 반사를 만드는 방법을 보여 주는 예제를 포함 하는 전체 샘플을 참조 하세요 [VisualBrush 샘플](https://go.microsoft.com/fwlink/?LinkID=160049)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.VisualBrush>
- [이미지, 그림 및 시각적 표시로 그리기](painting-with-images-drawings-and-visuals.md)
