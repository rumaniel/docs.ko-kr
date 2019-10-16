---
title: GDI+의 카디널 스플라인
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- splines [Windows Forms], cardinal
- GDI+, cardinal splines
- cardinal splines
ms.assetid: 09b3797a-6294-422d-9adf-a5a0a7695c0c
ms.openlocfilehash: 4588f6f606f0f479aeae1d143f23175ec4be32a5
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61779134"
---
# <a name="cardinal-splines-in-gdi"></a>GDI+의 카디널 스플라인
카디널 스플라인에 더 큰 곡선을 형성 하는 개별 곡선 시퀀스입니다. 스플라인은 포인트와 장력 매개 변수 배열에 의해 지정 됩니다. 카디널 스플라인; 배열의 각 요소를 통해 원활 하 게 전달 날카로운 모퉁이가 없고 및 곡선의 다듬기에 갑작스러운 변경 하지 않고 있습니다. 다음 그림에서는 지점 및 카디널 스플라인을 집합의 각 요소를 통과 하는 집합을 보여 줍니다.  
  
 ![카디널 스플라인](./media/aboutgdip02-art09.gif "Aboutgdip02_art09")  
  
## <a name="physical-and-mathematical-splines"></a>물리적 및 수학 스플라인  
 실제 스플라인은 씬 wood 또는 기타 유연한 자료. 수학 스플라인이 도입 되기 전에 디자이너 실제 스플라인 곡선을 그리는 데 있습니다. 디자이너는 스플라인을 종이에 배치 지정된 된 집합이 지점에 주석을 고정 합니다. 디자이너를 만들 수는 곡선 스플라인 따라 그리는 방식으로 펜 또는 연필을 사용 하 여. 지정 된 일련의 점으로 다양 한 물리적 스플라인의 속성에 따라 곡선 만들어냈습니다. 예를 들어, 구부러진에 높은 저항을 사용 하 여 스플라인을 극도로 스플라인 보다 다른 곡선을 생성 합니다.  
  
 수학 스플라인에 대 한 수식은 기반으로 유연한 막대의 속성 수학 스플라인 곡선에서 생성 되는 곡선 스플라인 물리적으로 만들어 졌 던 곡선 비슷합니다 되므로 합니다. 실제 스플라인 장력이 다른 요소의 지정 된 집합을 통해 다른 곡선을 생산 하 고, 처럼 수학 스플라인 장력 매개 변수에 대 한 값이 서로 다른 요소의 지정 된 집합을 통해 다른 곡선 생성 됩니다. 다음 그림에서는 동일한 점 집합을 통해 전달 하는 네 가지 카디널 스플라인 보여 줍니다. 각 스플라인 장력 표시 됩니다. 0의 장력을 무한 이면 물리적 장력이 점 간 최단 방식 (직선) 되려면 곡선에 해당 합니다. 1의 장력 이상 총 벤드 경로 스플라인을 없는 실제 장력을에 해당 합니다. 1 보다 큰 압력 값을 사용 하 여 곡선 경로가 더 길어질 푸시 압축된 스프링 처럼 동작 합니다.  
  
 ![카디널 스플라인](./media/aboutgdip02-art10.gif "Aboutgdip02_art10")  
  
 앞의 그림에서 네 개의 스플라인 시작 지점에 동일한 접선을 공유합니다. 탄젠트 값은 곡선을 따라 다음 지점으로 시작 점에서 그린 선입니다. 마찬가지로, 끝점의 공유 탄젠트를 이전 시점 곡선의 끝점에서 가져온 선입니다.  
  
 카디널 스플라인 그리기를 하려면 인스턴스의 <xref:System.Drawing.Graphics> 클래스를 <xref:System.Drawing.Pen>, 및 배열을 <xref:System.Drawing.Point> 인스턴스의 개체를 <xref:System.Drawing.Graphics> 클래스를 제공 합니다 <xref:System.Drawing.Graphics.DrawCurve%2A> 스플라인을 그립니다, 메서드를 및 <xref:System.Drawing.Pen> 선 두께 색 같은 스플라인 특성을 저장합니다. 배열을 <xref:System.Drawing.Point> 개체에 곡선을 통과 하는 점을 저장 합니다. 다음 코드 예제에서 요소를 통해 전달 되는 카디널 스플라인 그리기 하는 방법을 보여 줍니다 `myPointArray`합니다. 세 번째 장력입니다.  
  
 [!code-csharp[LinesCurvesAndShapes#31](~/samples/snippets/csharp/VS_Snippets_Winforms/LinesCurvesAndShapes/CS/Class1.cs#31)]
 [!code-vb[LinesCurvesAndShapes#31](~/samples/snippets/visualbasic/VS_Snippets_Winforms/LinesCurvesAndShapes/VB/Class1.vb#31)]  
  
## <a name="see-also"></a>참고자료

- [선, 곡선 및 도형](lines-curves-and-shapes.md)
- [곡선 구성 및 그리기](constructing-and-drawing-curves.md)
