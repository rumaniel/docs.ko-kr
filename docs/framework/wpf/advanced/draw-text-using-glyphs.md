---
title: 문자 모양을 사용하여 텍스트 그리기
ms.date: 03/30/2017
helpviewer_keywords:
- text [WPF], drawing with Glyphs objects
- Glyphs objects [WPF], drawing text
- typography [WPF], Glyphs objects
ms.assetid: 587ab17e-a419-4ad5-b6da-8933a8e83d97
ms.openlocfilehash: 55bbc50de519d6607a843fcd633f2c07db53109f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62010373"
---
# <a name="draw-text-using-glyphs"></a>문자 모양을 사용하여 텍스트 그리기
이 항목에서는 하위 수준 사용 하는 방법에 설명 <xref:System.Windows.Documents.Glyphs> 에서 텍스트를 표시 하는 개체 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 속성을 정의 하는 방법을 보여는 <xref:System.Windows.Documents.Glyphs> 개체의 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]합니다. 합니다 <xref:System.Windows.Documents.Glyphs> 개체의 출력을 나타냅니다는 <xref:System.Windows.Media.GlyphRun> 에서 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]합니다. 이 예에서는 로컬 컴퓨터의 C:\WINDOWS\Fonts 폴더에 Arial, Courier New 및 Times New Roman 글꼴이 설치되어 있다고 가정합니다.  
  
 [!code-xaml[GlyphsOvwSample1#1](~/samples/snippets/csharp/VS_Snippets_Wpf/GlyphsOvwSample1/CS/default.xaml#1)]  
  
 이 예의 다른 속성을 정의 하는 방법을 보여 줍니다 <xref:System.Windows.Documents.Glyphs> 개체 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]합니다.  
  
 [!code-xaml[GlyphsOvwSamp2#1](~/samples/snippets/csharp/VS_Snippets_Wpf/GlyphsOvwSamp2/CS/default.xaml#1)]  
  
## <a name="see-also"></a>참고자료

- [WPF의 입력 체계](typography-in-wpf.md)
