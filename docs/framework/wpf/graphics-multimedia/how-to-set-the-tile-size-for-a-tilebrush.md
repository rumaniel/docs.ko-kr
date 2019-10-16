---
title: '방법: TileBrush의 타일 크기 설정'
ms.date: 03/30/2017
helpviewer_keywords:
- TileBrush [WPF], size of tile properties
- Viewport property of TileBrush [WPF]
ms.assetid: 04f41090-1b46-4e36-832f-d27d28708b8c
ms.openlocfilehash: 80b5dfc668464df829db593668bea8a9a4ec09e4
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61804210"
---
# <a name="how-to-set-the-tile-size-for-a-tilebrush"></a>방법: TileBrush의 타일 크기 설정

에 대 한 타일 크기를 설정 하는 방법을 보여주는이 예제는 <xref:System.Windows.Media.TileBrush>합니다. 기본적으로 <xref:System.Windows.Media.TileBrush> 는 사용자가 칠하고 있는 영역을 완전히 채우는 단일 타일을 생성 합니다. 설정 하 여이 동작을 재정의할 수는 <xref:System.Windows.Media.TileBrush.Viewport%2A> 고 <xref:System.Windows.Media.TileBrush.ViewportUnits%2A> 속성입니다.

합니다 <xref:System.Windows.Media.TileBrush.Viewport%2A> 속성에 대 한 타일 크기를 지정 된 <xref:System.Windows.Media.TileBrush>합니다. 기본적으로 값을 <xref:System.Windows.Media.TileBrush.Viewport%2A> 속성은 그리는 영역의 크기를 기준으로 합니다. 수 있도록 합니다 <xref:System.Windows.Media.TileBrush.Viewport%2A> 속성이 절대 타일 크기를 지정 설정 합니다 <xref:System.Windows.Media.TileBrush.ViewportUnits%2A> 속성을 <xref:System.Windows.Media.BrushMappingMode.Absolute>입니다.

## <a name="example"></a>예제

다음 예제에서는 <xref:System.Windows.Media.ImageBrush>, 형식의 <xref:System.Windows.Media.TileBrush>, 타일을 사용 하 여 사각형을 그립니다. 예제는 각 타일 출력 영역 (사각형)의 50%에서 50%로 설정합니다. 결과적으로 이미지 프로젝션 4개를 사용한 사각형이 그려집니다.

다음 그림에서는 예제의 출력을 보여 줍니다.

![바둑판식 이미지 브러시를 사용 하 여 보여 주는 네 개의 체리를 사용 하 여 사각형입니다.](./media/how-to-set-the-tile-size-for-a-tilebrush/rectangle-tile-image-brush.png)

[!code-csharp[UsingImageBrush_snip#RelativeTileSizeExample](~/samples/snippets/csharp/VS_Snippets_Wpf/UsingImageBrush_snip/CSharp/TileSizeExample.cs#relativetilesizeexample)]

다음 예제에서는 <xref:System.Windows.Media.ImageBrush>, 설정 해당 <xref:System.Windows.Media.TileBrush.Viewport%2A> 를 `0,0,25,25` 고 <xref:System.Windows.Media.TileBrush.ViewportUnits%2A> 에 <xref:System.Windows.Media.BrushMappingMode.Absolute>, 하는 다른 사각형을 그리는 데 사용 합니다. 결과적으로 이 브러시는 너비 및 높이가 각각 25픽셀인 타일을 생성합니다.

다음 그림에서는 예제의 출력을 보여 줍니다.

![뷰포트를 사용 하 여 바둑판식으로 배열 된 TileBrush를 보여 주는 40 8 체리를 사용 하 여 사각형입니다.](./media/how-to-set-the-tile-size-for-a-tilebrush/25-x-25-viewport-tilebrush.png)

[!code-csharp[UsingImageBrush_snip#AbsoluteTileSizeExample](~/samples/snippets/csharp/VS_Snippets_Wpf/UsingImageBrush_snip/CSharp/TileSizeExample.cs#absolutetilesizeexample)]

앞의 예제는 큰 샘플의 일부입니다. 전체 샘플을 참조 하세요 [ImageBrush 샘플](https://go.microsoft.com/fwlink/?LinkID=160005)합니다.

이 예제에서는 합니다 <xref:System.Windows.Media.ImageBrush> 클래스를 <xref:System.Windows.Media.TileBrush.Viewport%2A> 및 <xref:System.Windows.Media.TileBrush.ViewportUnits%2A> 속성을 다른 동일 하 게 작동 <xref:System.Windows.Media.TileBrush> 개체, 즉,에 대 한 <xref:System.Windows.Media.DrawingBrush> 및 <xref:System.Windows.Media.VisualBrush>. 에 대 한 자세한 내용은 <xref:System.Windows.Media.ImageBrush> 집합과 <xref:System.Windows.Media.TileBrush> 개체를 참조 하세요 [이미지, 그림 및 시각적 표시로 그리기](painting-with-images-drawings-and-visuals.md)합니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Media.TileBrush>
- [이미지, 그림 및 시각적 표시로 그리기](painting-with-images-drawings-and-visuals.md)
- [TileBrush로 다른 바둑판식 배열 패턴 만들기](how-to-create-different-tile-patterns-with-a-tilebrush.md)
