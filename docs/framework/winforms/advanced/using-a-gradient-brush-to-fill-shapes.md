---
title: 그라데이션 브러시를 사용하여 도형 채우기
ms.date: 03/30/2017
helpviewer_keywords:
- brushes [Windows Forms], gradient brushes
- gradient brushes
- examples [Windows Forms], gradient brushes
ms.assetid: 2c6037b9-05bd-44c0-a22a-19584b722524
ms.openlocfilehash: 7ff555ba4fd81e9123e5f9e9feed38a0ec9d0a08
ms.sourcegitcommit: ca2ca60e6f5ea327f164be7ce26d9599e0f85fe4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65063612"
---
# <a name="using-a-gradient-brush-to-fill-shapes"></a>그라데이션 브러시를 사용하여 도형 채우기
그라데이션 브러시 효과 사용 하 여 도형 채우기를 사용할 수 있습니다. 예를 들어, 오른쪽 가장자리에 모양의 왼쪽된 가장자리에서 이동 하면 점진적으로 변경 하는 색으로 모양을 채울 가로 그라데이션을 사용할 수 있습니다. 사각형 왼쪽된 가장자리는 검정을 사용 하 여 imagine (0, 0, 0 빨강, 녹색 및 파랑 구성 요소에 의해 표현 됨) 및 오른쪽 가장자리 빨강 (255, 0, 0)입니다. 256 픽셀 사각형의 면이 지정 된 픽셀의 빨강 구성 요소는 왼쪽에 있는 픽셀의 빨강 구성 요소 보다 큰 하나가 됩니다. 행에서 가장 왼쪽 픽셀의 색 구성 요소 (0, 0, 0), 두 번째 픽셀 (1, 0, 0)에 세 번째 픽셀 (2, 0, 0)에 등에 오른쪽에 있는 픽셀의 색 구성 요소 (255, 0, 0)에 도달할 때까지 합니다. 이러한 방식된으로 색 값 색 그라데이션을 구성 합니다.  
  
 가로, 세로 이동 하거나 지정된 된 기울어진된 줄으로 병렬 선형 그라데이션 색을 변경 합니다. 내부 및 경로 경계에 대 한 이동 경로 그라데이션 색을 변경 합니다. 경로 그라데이션 다양 한 효과 달성 하기 위해 사용자 지정할 수 있습니다.  
  
 다음 그림에서는 선형 그라데이션 브러시를 사용 하 여 채워진 사각형 및 타원 경로 그라데이션 브러시를 사용 하 여 입력을 보여 줍니다.  
  
 ![타원 사용 하는 그라데이션 브러시가 채워진 사각형입니다.](./media/using-a-gradient-brush-to-fill-shapes/rectangle-ellipse-gradient-brush.png)  
  
## <a name="in-this-section"></a>섹션 내용  
 [방법: 선형 그라데이션 만들기](how-to-create-a-linear-gradient.md)  
 선형 그라데이션을 만드는 방법을 보여 줍니다는 <xref:System.Drawing.Drawing2D.LinearGradientBrush> 클래스입니다.  
  
 [방법: 경로 그라데이션 만들기](how-to-create-a-path-gradient.md)  
 사용 하 여 경로 그라데이션 하는 방법에 설명 합니다 <xref:System.Drawing.Drawing2D.PathGradientBrush> 클래스입니다.  
  
 [방법: 그라데이션에 감마 보정 적용](how-to-apply-gamma-correction-to-a-gradient.md)  
 그라데이션 브러시를 사용 하 여 감마 보정을 사용 하는 방법에 설명 합니다.  
  
## <a name="reference"></a>참조  
 <xref:System.Drawing.Drawing2D.LinearGradientBrush?displayProperty=nameWithType>  
 이 클래스에 대 한 설명을 포함 하 고 모든 해당 멤버의 링크를 포함 합니다.  
  
 <xref:System.Drawing.Drawing2D.PathGradientBrush?displayProperty=nameWithType>  
 이 클래스에 대 한 설명을 포함 하 고 모든 해당 멤버의 링크를 포함 합니다.
