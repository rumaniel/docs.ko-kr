---
title: 그래픽 인터페이스의 구조
ms.date: 03/30/2017
helpviewer_keywords:
- GDI+, using managed interface
- graphics [Windows Forms], class structure
ms.assetid: 010a1e46-656b-40a1-8d5d-87aa05ee1243
ms.openlocfilehash: d3b16249b6bae4a113661f5a3a47097046ba20f1
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67505274"
---
# <a name="structure-of-the-graphics-interface"></a>그래픽 인터페이스의 구조
GDI + 관리 되는 클래스 인터페이스는 약 60 개의 클래스, 50 개의 열거형 및 8 구조를 포함합니다. <xref:System.Drawing.Graphics> 클래스 GDI + 기능의 핵심은 실제로 선, 곡선, 도형, 이미지 및 텍스트를 그릴 수 있는 클래스입니다.  
  
## <a name="important-classes"></a>중요 한 클래스  
 대부분의 클래스와 함께 작동 합니다 <xref:System.Drawing.Graphics> 클래스입니다. 예를 들어 합니다 <xref:System.Drawing.Graphics.DrawLine%2A> 메서드는 수신를 <xref:System.Drawing.Pen> 그릴 선의 특성 (예: 색, 너비, 대시 스타일 및 like)을 보유 하는 개체입니다. <xref:System.Drawing.Graphics.FillRectangle%2A> 방법에 대 한 포인터를 받을 수는 <xref:System.Drawing.Drawing2D.LinearGradientBrush> 작동 하는 개체를 <xref:System.Drawing.Graphics> 효과 사용 하 여 사각형에 맞게 개체. <xref:System.Drawing.Font> 및 <xref:System.Drawing.StringFormat> 개체에는 방법에 영향을 <xref:System.Drawing.Graphics> 개체 텍스트를 그립니다. A <xref:System.Drawing.Drawing2D.Matrix> 개체 저장 및 조작의 월드 변형을 <xref:System.Drawing.Graphics> 개체를 회전, 크기 조정 및 이미지를 대칭 이동 하는 데 사용 됩니다.  
  
 GDI +-여러 구조를 제공 하는 중 (예를 들어 <xref:System.Drawing.Rectangle>, <xref:System.Drawing.Point>, 및 <xref:System.Drawing.Size>) 그래픽 데이터를 구성 합니다. 또한 특정 클래스 주로으로 구조화 된 데이터 형식을 제공 합니다. 예를 들어, 합니다 <xref:System.Drawing.Imaging.BitmapData> 클래스는 도우미에 대 한는 <xref:System.Drawing.Bitmap> 클래스 및 <xref:System.Drawing.Drawing2D.PathData> 클래스에 대 한 도우미는는 <xref:System.Drawing.Drawing2D.GraphicsPath> 클래스.  
  
 GDI + 관련 상수 컬렉션은 여러 열거형을 정의 합니다. 예를 들어 합니다 <xref:System.Drawing.Drawing2D.LineJoin> 요소를 포함 하는 열거형 <xref:System.Drawing.Drawing2D.LineJoin.Bevel>, <xref:System.Drawing.Drawing2D.LineJoin.Miter>, 및 <xref:System.Drawing.Drawing2D.LineJoin.Round>, 두 선을 조인할 때 사용할 수 있는 스타일을 지정 하는 합니다.  
  
## <a name="see-also"></a>참고자료

- [그래픽 개요](graphics-overview-windows-forms.md)
- [GDI + 관리 코드 정보](about-gdi-managed-code.md)
- [관리되는 그래픽 클래스 사용](using-managed-graphics-classes.md)
