---
title: 선과 곡선의 앤티 앨리어싱
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- antialiasing
- antialiasing [Windows Forms], smoothing modes
- GDI+, antialiasing
ms.assetid: 810da1a4-c136-4abf-88df-68e49efdd8d4
ms.openlocfilehash: 871c5cb3cd9356f677633acb04fe82021a9787c5
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67506143"
---
# <a name="antialiasing-with-lines-and-curves"></a>선과 곡선의 앤티 앨리어싱
선을 그릴 GDI +를 사용 하면 시작 지점 및 끝 줄의 지점 제공 하지만 줄에 각 픽셀에 대 한 정보를 제공할 필요가 없습니다. GDI + 특정 디스플레이 장치에 선을 표시 하려면 어떤 픽셀이 켜 집니다 결정할 디스플레이 드라이버 소프트웨어와 함께 작동 합니다.  
  
## <a name="aliasing"></a>별칭 지정  
 바로 빨간색 선이 (4, 2) 지점에서 점 (16, 10)으로 이동 하는 것이 좋습니다. 좌표 시스템의 왼쪽 위 모퉁이에 원점 및 측정 단위는 픽셀을 가정 합니다. 또한 해당 x 축 지점 y 축 지점과 오른쪽 아래로 가정 합니다. 다음 그림에서는 컬러 배경에 그려진 빨간색 선은의 확대 된 뷰를 보여 줍니다.  
  
 ![선, 앤티 앨리어싱](./media/aboutgdip02-art33.gif "AboutGdip02_Art33")  
  
 선을 렌더링 하는 데 빨간색 픽셀은 불투명 합니다. 줄에서 부분적으로 투명 한 픽셀이 없습니다. 이 유형의 선 렌더링을 사용 하면 선이 가변된 모양 및 약간 계단 처럼 보입니다. 이 기술은 계단식으로 선을 나타내는 별칭; 라고 합니다. 계단은 이론적인 선의 대 한 별칭입니다.  
  
## <a name="antialiasing"></a>앤티 앨리어싱  
 줄을 렌더링 하기 위한 보다 복잡 한 기술에서는 부분적으로 투명 한 픽셀 불투명 한 픽셀와 함께 사용 합니다. 픽셀 순수 빨강으로 설정 됩니다 또는 레드 팀 및 배경색을 혼합 하려면 정도 따라 줄으로 합니다. 이러한 유형의 렌더링 앤티 앨리어싱 라고 및 사람의 눈에 게 더 부드러운 줄에서 발생 합니다. 다음 그림에서는 특정 픽셀 앤티 앨리어싱 선을 위해 배경색과 혼합 되는 방법을 보여 줍니다.  
  
 ![선 앤티 앨리어싱](./media/aboutgdip02-art34.gif "AboutGdip02_Art34")  
  
 앤티 앨리어싱, 다듬기, 라고도 곡선에도 적용할 수 있습니다. 다음 그림에서는 평활된 타원의 확대 된 뷰를 보여 줍니다.  
  
 ![곡선 앤티 앨리어싱](./media/aboutgdip02-art35.gif "AboutGdip02_Art35")  
  
 다음 그림에서는 실제 크기에 한 번 앤티 앨리어싱 앤티 앨리어싱 없이 한 번에 동일한 타원을 보여 줍니다.  
  
 ![앤티 앨리어싱 예](./media/aboutgdip02-art36.gif "AboutGdip02_Art36")  
  
 앤티 앨리어싱을 사용 하는 선과 곡선을 그릴의 인스턴스를 만듭니다는 <xref:System.Drawing.Graphics> 클래스 설정 및 해당 <xref:System.Drawing.Graphics.SmoothingMode%2A> 속성을 <xref:System.Drawing.Drawing2D.SmoothingMode.AntiAlias> 또는 <xref:System.Drawing.Drawing2D.SmoothingMode.HighQuality>합니다. 다음 중 하나를 호출 하는 그리기 메서드 같은 <xref:System.Drawing.Graphics> 클래스입니다.  
  
 [!code-csharp[LinesCurvesAndShapes#81](~/samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#81)]
 [!code-vb[LinesCurvesAndShapes#81](~/samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#81)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Drawing.Drawing2D.SmoothingMode?displayProperty=nameWithType>
- [선, 곡선 및 도형](lines-curves-and-shapes.md)
- [방법: 텍스트에 앤티 앨리어싱 사용](how-to-use-antialiasing-with-text.md)
