---
title: '방법: 시각적 개체의 그리기 콘텐츠 열거'
ms.date: 03/30/2017
helpviewer_keywords:
- retrieving the DrawingGroup value of a Visual [WPF]
- enumerating the contents of a Visual [WPF]
ms.assetid: 2974ddb3-2997-4713-8fd2-e93d549c58a8
ms.openlocfilehash: 25aa0c3706005c1e16cedd7e06914db764545ebb
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69930078"
---
# <a name="how-to-enumerate-drawing-content-of-a-visual"></a>방법: 시각적 개체의 그리기 콘텐츠 열거
개체 <xref:System.Windows.Media.Drawing> 는<xref:System.Windows.Media.Visual>의 콘텐츠를 열거 하기 위한 개체 모델을 제공 합니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 <xref:System.Windows.Media.VisualTreeHelper.GetDrawing%2A> 메서드를 사용 하 여의 <xref:System.Windows.Media.DrawingGroup> <xref:System.Windows.Media.Visual> 값을 검색 하 고이를 열거 합니다.  
  
> [!NOTE]
> 시각적 개체의 콘텐츠를 열거 하는 경우 개체를 검색 <xref:System.Windows.Media.Drawing> 하 고 렌더링 데이터의 기본 표현이 벡터 그래픽 명령 목록으로 표시 되지 않습니다. 자세한 내용은 [WPF 그래픽 렌더링 개요](wpf-graphics-rendering-overview.md)를 참조하세요.  
  
 [!code-csharp[DrawingMiscSnippets_snip#GraphicsMMRetrieveDrawings](~/samples/snippets/csharp/VS_Snippets_Wpf/DrawingMiscSnippets_snip/CSharp/EnumerateDrawingsExample.xaml.cs#graphicsmmretrievedrawings)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.Drawing>
- <xref:System.Windows.Media.DrawingGroup>
- <xref:System.Windows.Media.VisualTreeHelper>
- [Drawing 개체 개요](drawing-objects-overview.md)
- [WPF 그래픽 렌더링 개요](wpf-graphics-rendering-overview.md)
