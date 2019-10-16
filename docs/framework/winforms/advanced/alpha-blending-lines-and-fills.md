---
title: 선 및 채우기 알파 혼합
ms.date: 03/30/2017
helpviewer_keywords:
- lines [Windows Forms], adding transparency
- examples [Windows Forms], alpha blending
- alpha blending [Windows Forms], using with lines
- alpha blending
- lines [Windows Forms], alpha blending
- fills [Windows Forms], alpha blending
- alpha blending [Windows Forms], using with fills
- shapes [Windows Forms], adding transparency
ms.assetid: 5440f48c-3ac9-44c3-b170-c1c110bdbab8
ms.openlocfilehash: 66061341ee6539e2172c537a0b2a6ec9ff87565c
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67506112"
---
# <a name="alpha-blending-lines-and-fills"></a>선 및 채우기 알파 혼합
GDI +에서 색을 사용 하 여 알파, 빨강, 녹색 및 파랑으로 각각 8 비트가 32 비트 값입니다. 알파 값을 나타내는 색의 투명도-범위를 색이 배경 색과 혼합 됩니다. 알파 값 범위는 0에서 255까지, 0은 완전히 투명 한 색을 나타내는 255에서 완전히 불투명 한 색을 나타냅니다.  
  
 알파 혼합 원본과 배경 색 데이터의 픽셀 단위로 혼합 됩니다. 각 세 가지 구성 요소 (빨강, 녹색, 파랑)는 지정 된 소스 색의 배경색을 다음 수식에 따라 해당 구성 요소와 혼합 됩니다.  
  
 displayColor sourceColor × 알파 = 255 / + backgroundColor × (255 – 알파) / 255  
  
 예를 들어, 소스 색의 빨강 구성 요소는 150 및 배경 색의 빨강 구성 요소는 100입니다. 알파 값 200 인 경우 결과 색의 빨강 구성 요소는 다음과 같이 계산 됩니다.  
  
 150 × 200 / 255 + 100 × (255 – 200) / 255 = 139  
  
## <a name="in-this-section"></a>섹션 내용  
 [방법: 불투명 및 반투명 선 그리기](how-to-draw-opaque-and-semitransparent-lines.md)  
 알파 혼합 선을 그리는 방법을 보여 줍니다.  
  
 [방법: 불투명 및 반투명 브러시를 사용 하 여 그리기](how-to-draw-with-opaque-and-semitransparent-brushes.md)  
 브러시를 사용 하 여 알파 혼합 하는 방법을 설명 합니다.  
  
 [방법: 알파 혼합 조절 하려면 혼합 모드를 사용 합니다.](how-to-use-compositing-mode-to-control-alpha-blending.md)  
 사용 하 여 알파 혼합을 제어 하는 방법에 설명 <xref:System.Drawing.Drawing2D.CompositingMode>합니다.  
  
 [방법: 색 매트릭스를 사용 하 여 이미지에 알파 값 설정](how-to-use-a-color-matrix-to-set-alpha-values-in-images.md)  
 사용 하는 방법에 설명 된 <xref:System.Drawing.Imaging.ColorMatrix> 알파 혼합을 제어 하는 개체입니다.
