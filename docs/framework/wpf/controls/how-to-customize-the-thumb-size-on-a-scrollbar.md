---
title: '방법: ScrollBar의 Thumb 크기 사용자 지정'
ms.date: 03/30/2017
helpviewer_keywords:
- ScrollBar control [WPF]
- customizing thumb size [WPF]
- thumb size [WPF]
ms.assetid: fa32b866-5ca1-4e73-85e7-2ac64b80d194
ms.openlocfilehash: 60ae7c4e95801036c5deb0c485645297509b830c
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61911055"
---
# <a name="how-to-customize-the-thumb-size-on-a-scrollbar"></a>방법: ScrollBar의 Thumb 크기 사용자 지정
이 항목에서는 설정 하는 방법에 설명 합니다 <xref:System.Windows.Controls.Primitives.Thumb> 의 <xref:System.Windows.Controls.Primitives.ScrollBar> 고정 된 크기 및 최소 크기를 지정 하는 방법에는 <xref:System.Windows.Controls.Primitives.Thumb> 의 <xref:System.Windows.Controls.Primitives.ScrollBar>.  
  
## <a name="example"></a>예제  
  
## <a name="description"></a>설명  
 다음 예에서는 <xref:System.Windows.Controls.Primitives.ScrollBar> 있는 <xref:System.Windows.Controls.Primitives.Thumb> 고정 크기입니다. 예제에서는 <xref:System.Windows.Controls.Primitives.Track.ViewportSize%2A> 의 속성을 <xref:System.Windows.Controls.Primitives.Thumb> 에 <xref:System.Double.NaN> 의 높이 가져오거나 설정는 <xref:System.Windows.Controls.Primitives.Thumb>.  가로 만들려면 <xref:System.Windows.Controls.Primitives.ScrollBar> 사용 하 여는 <xref:System.Windows.Controls.Primitives.Thumb> 는 고정된 폭, 너비를 설정 합니다 <xref:System.Windows.Controls.Primitives.Thumb>.  
  
## <a name="code"></a>코드  
 [!code-xaml[ScrollBarCustomThumbSize#1](~/samples/snippets/csharp/VS_Snippets_Wpf/ScrollBarCustomThumbSize/CS/Window1.xaml#1)]  
  
## <a name="description"></a>설명  
 다음 예에서는 <xref:System.Windows.Controls.Primitives.ScrollBar> 있는 <xref:System.Windows.Controls.Primitives.Thumb> 최소 크기입니다. 값을 설정 하는 예제 <xref:System.Windows.SystemParameters.VerticalScrollBarButtonHeightKey%2A>합니다. 가로 만들려면 <xref:System.Windows.Controls.Primitives.ScrollBar> 사용 하 여는 <xref:System.Windows.Controls.Primitives.Thumb> 는 최소 너비에 설정 합니다 <xref:System.Windows.SystemParameters.HorizontalScrollBarButtonWidthKey%2A>합니다.  
  
## <a name="code"></a>코드  
 [!code-xaml[ScrollBarCustomThumbSize#2](~/samples/snippets/csharp/VS_Snippets_Wpf/ScrollBarCustomThumbSize/CS/Window1.xaml#2)]  
  
## <a name="see-also"></a>참고자료

- [ScrollBar 스타일 및 템플릿](scrollbar-styles-and-templates.md)
