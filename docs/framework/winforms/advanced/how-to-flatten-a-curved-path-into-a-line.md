---
title: '방법: 구부러진 경로를 선으로 펴기'
ms.date: 03/30/2017
helpviewer_keywords:
- graphics [Windows Forms], flattening curves into lines
- curves [Windows Forms], flattening
- GraphicsPath object
- paths [Windows Forms], flattening
- drawing [Windows Forms], flattening curves
ms.assetid: e654b8de-25f4-4735-9208-42e4514a589c
ms.openlocfilehash: d59a802618ddd5080c651e822ed4c09641f7f170
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64645362"
---
# <a name="how-to-flatten-a-curved-path-into-a-line"></a>방법: 구부러진 경로를 선으로 펴기
<xref:System.Drawing.Drawing2D.GraphicsPath> 선 및 3 차원 곡선 스플라인의 시퀀스를 저장 하는 개체입니다. 여러 종류의 곡선 (줄임표, 원호를 카디 날 곡선 스플라인) 경로 추가할 수 있지만 경로에 저장 되기 전에 각 곡선을 베 지 어 스플라인을 변환할 합니다. 경로 평면화 하는 작업은 경로 있는 각 베 지 어 스플라인을 직선 시퀀스로 변환 하는 구성 됩니다. 다음 그림에서는 전후의 경로 보여 줍니다.  
  
 ![직선 및 곡선](./media/aboutgdip02-art32a.gif "AboutGdip02_Art32A")  
  
### <a name="to-flatten-a-path"></a>경로 평면화 하려면  
  
- 호출 된 <xref:System.Drawing.Drawing2D.GraphicsPath.Flatten%2A> 메서드는 <xref:System.Drawing.Drawing2D.GraphicsPath> 개체입니다. <xref:System.Drawing.Drawing2D.GraphicsPath.Flatten%2A> 메서드는 결합 된 경로 원래 경로 간의 최대 거리를 지정 하는 직선 화 정도 인수를 받습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Drawing.Drawing2D.GraphicsPath?displayProperty=nameWithType>
- [선, 곡선 및 도형](lines-curves-and-shapes.md)
- [경로 구성 및 그리기](constructing-and-drawing-paths.md)
