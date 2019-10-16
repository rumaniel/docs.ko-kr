---
title: Graphics 개체의 상태 관리
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- graphics [Windows Forms], managing state
- graphics [Windows Forms], clipping
ms.assetid: 6207cad1-7a34-4bd6-bfc1-db823ca7a73e
ms.openlocfilehash: ce645133af35271fe1de969621907c53183d9a54
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67505599"
---
# <a name="managing-the-state-of-a-graphics-object"></a>Graphics 개체의 상태 관리
<xref:System.Drawing.Graphics> GDI +의 핵심 클래스입니다. 가져올 항목을 그리려면를 <xref:System.Drawing.Graphics> 개체 속성을 설정 하 고 해당 메서드를 호출할 <xref:System.Drawing.Graphics.DrawLine%2A>, <xref:System.Drawing.Graphics.DrawImage%2A>, <xref:System.Drawing.Graphics.DrawString%2A>, 등).  
  
 다음 예제에서는 합니다 <xref:System.Drawing.Graphics.DrawRectangle%2A> 메서드는 <xref:System.Drawing.Graphics> 개체입니다. 전달 된 첫 번째 인수는 <xref:System.Drawing.Graphics.DrawRectangle%2A> 메서드는을 <xref:System.Drawing.Pen> 개체입니다.  
  
```vb  
Dim graphics As Graphics = e.Graphics  
Dim pen As New Pen(Color.Blue) ' Opaque blue  
graphics.DrawRectangle(pen, 10, 10, 200, 100)  
```  
  
```csharp  
Graphics graphics = e.Graphics;  
Pen pen = new Pen(Color.Blue);  // Opaque blue  
graphics.DrawRectangle(pen, 10, 10, 200, 100);  
```  
  
## <a name="graphics-state"></a>그래픽 상태  
 A <xref:System.Drawing.Graphics> 개체는 그리기 메서드를 같은 제공 둘 <xref:System.Drawing.Graphics.DrawLine%2A> 고 <xref:System.Drawing.Graphics.DrawRectangle%2A>합니다. <xref:System.Drawing.Graphics> 개체는 다음 범주로 나누어진 그래픽 상태를 유지 합니다.  
  
- 품질 설정  
  
- 변형  
  
- 클리핑 영역  
  
### <a name="quality-settings"></a>품질 설정  
 <xref:System.Drawing.Graphics> 개체에 그려지는 항목의 품질에 영향을 주는 몇 가지 속성이 있습니다. 예를 들어, 설정할 수 있습니다는 <xref:System.Drawing.Graphics.TextRenderingHint%2A> 적용 된 텍스트 앤티앨리어싱 (있는 경우)의 형식을 지정 하는 속성입니다. 품질에 영향을 주는 다른 속성은 <xref:System.Drawing.Graphics.SmoothingMode%2A>, <xref:System.Drawing.Graphics.CompositingMode%2A>를 <xref:System.Drawing.Graphics.CompositingQuality%2A>, 및 <xref:System.Drawing.Graphics.InterpolationMode%2A>합니다.  
  
 다음 예제에서는 다듬기 모드를 사용 하 여 하나 두 타원을 그립니다 <xref:System.Drawing.Drawing2D.SmoothingMode.AntiAlias> 로 다듬기 모드를 사용 하 여 개와 <xref:System.Drawing.Drawing2D.SmoothingMode.HighSpeed>:  
  
```vb  
Dim graphics As Graphics = e.Graphics  
Dim pen As New Pen(Color.Blue)  
  
graphics.SmoothingMode = SmoothingMode.AntiAlias  
graphics.DrawEllipse(pen, 0, 0, 200, 100)  
graphics.SmoothingMode = SmoothingMode.HighSpeed  
graphics.DrawEllipse(pen, 0, 150, 200, 100)  
```  
  
```csharp  
Graphics graphics = e.Graphics;  
Pen pen = new Pen(Color.Blue);  
  
graphics.SmoothingMode = SmoothingMode.AntiAlias;  
graphics.DrawEllipse(pen, 0, 0, 200, 100);  
graphics.SmoothingMode = SmoothingMode.HighSpeed;  
graphics.DrawEllipse(pen, 0, 150, 200, 100);  
```  
  
### <a name="transformations"></a>변형  
 A <xref:System.Drawing.Graphics> 개체를 유지 관리 하 여 그리는 모든 항목에 적용 되는 두 개의 변환 (월드 및 페이지) <xref:System.Drawing.Graphics> 개체입니다. 모든 3x3 유사 변형 월드에 저장할 수 있습니다. 관계 변형 크기 조정, 회전, 반사, 기울이기 및 번역을 포함 합니다. 크기를 조정 하 고 단위 (예를 들어 인치로 픽셀)를 변경 하는 것에 대 한 페이지 변환은 사용할 수 있습니다. 자세한 내용은 [좌표계 및 변형](coordinate-systems-and-transformations.md)합니다.  
  
 다음 예제에서는 설정의 월드 및 페이지 변형을 <xref:System.Drawing.Graphics> 개체입니다. 월드 30도 회전을로 설정 됩니다. 페이지 변환은 두 번째 좌표 전달 되도록 설정 되어 <xref:System.Drawing.Graphics.DrawEllipse%2A> 픽셀 대신 (밀리미터 단위)로 간주 됩니다. 코드에서는 두 개의 동일한 호출을 <xref:System.Drawing.Graphics.DrawEllipse%2A> 메서드. 첫 번째 적용할 월드 <xref:System.Drawing.Graphics.DrawEllipse%2A> 두 번째 호출 및 (월드 및 페이지) 둘 다 적용 됩니다 <xref:System.Drawing.Graphics.DrawEllipse%2A> 호출 합니다.  
  
```vb  
Dim graphics As Graphics = e.Graphics  
Dim pen As New Pen(Color.Red)  
  
graphics.ResetTransform()  
graphics.RotateTransform(30) ' world transformation  
graphics.DrawEllipse(pen, 0, 0, 100, 50)  
graphics.PageUnit = GraphicsUnit.Millimeter ' page transformation  
graphics.DrawEllipse(pen, 0, 0, 100, 50)  
```  
  
```csharp  
Graphics graphics = e.Graphics;  
Pen pen = new Pen(Color.Red);   
  
graphics.ResetTransform();  
graphics.RotateTransform(30);                    // world transformation  
graphics.DrawEllipse(pen, 0, 0, 100, 50);  
graphics.PageUnit = GraphicsUnit.Millimeter;     // page transformation  
graphics.DrawEllipse(pen, 0, 0, 100, 50);  
```  
  
 다음 그림에서는 두 타원을 보여 줍니다. 30도 회전 (클라이언트 영역의 왼쪽 위 모퉁이) 좌표계의 원점을, 타원의 중앙에 대 한 하지는 note 합니다. 두 번째 타원에 대 한 1의 펜 너비 첫 번째 타원은 및 1 밀리미터 1 픽셀씩 의미는 note도 합니다.  
  
 ![타원 두를 보여 주는 그림: 회전 및 펜 너비입니다.](./media/managing-the-state-of-a-graphics-object/set-rotation-pen-width-drawellipse-method.png)  
  
### <a name="clipping-region"></a>클리핑 영역  
 A <xref:System.Drawing.Graphics> 개체를 유지 관리 하 여 그리는 모든 항목에 적용 되는 클리핑 영역 <xref:System.Drawing.Graphics> 개체입니다. 호출 하 여 클리핑 영역을 설정할 수 있습니다는 <xref:System.Drawing.Graphics.SetClip%2A> 메서드.  
  
 다음 예제에서는 두 개의 사각형의 결합 하 여 더하기 모양의 영역을 만듭니다. 해당 지역의 클립 영역으로 지정 되는 <xref:System.Drawing.Graphics> 개체입니다. 그런 다음 코드는 클리핑 영역 내부에 제한 된 두 줄을 그립니다.  
  
```vb  
Dim graphics As Graphics = e.Graphics  
  
' Opaque red, width 5  
Dim pen As New Pen(Color.Red, 5)  
  
' Opaque aqua  
Dim brush As New SolidBrush(Color.FromArgb(255, 180, 255, 255))  
  
' Create a plus-shaped region by forming the union of two rectangles.  
Dim [region] As New [Region](New Rectangle(50, 0, 50, 150))  
[region].Union(New Rectangle(0, 50, 150, 50))  
graphics.FillRegion(brush, [region])  
  
' Set the clipping region.  
graphics.SetClip([region], CombineMode.Replace)  
  
' Draw two clipped lines.  
graphics.DrawLine(pen, 0, 30, 150, 160)  
graphics.DrawLine(pen, 40, 20, 190, 150)  
```  
  
```csharp  
Graphics graphics = e.Graphics;  
  
// Opaque red, width 5  
Pen pen = new Pen(Color.Red, 5);    
  
// Opaque aqua  
SolidBrush brush = new SolidBrush(Color.FromArgb(255, 180, 255, 255));    
  
// Create a plus-shaped region by forming the union of two rectangles.  
Region region = new Region(new Rectangle(50, 0, 50, 150));  
region.Union(new Rectangle(0, 50, 150, 50));  
graphics.FillRegion(brush, region);  
  
// Set the clipping region.  
graphics.SetClip(region, CombineMode.Replace);  
  
// Draw two clipped lines.  
graphics.DrawLine(pen, 0, 30, 150, 160);  
graphics.DrawLine(pen, 40, 20, 190, 150);  
```  
  
 다음 그림에서는 잘린된 줄을 보여 줍니다.  
  
 ![제한 된 클립 영역을 보여 주는 다이어그램입니다.](./media/managing-the-state-of-a-graphics-object/set-clipping-region-setclip-method.png)  
  
## <a name="see-also"></a>참고자료

- [Windows Forms의 그래픽 및 그리기](graphics-and-drawing-in-windows-forms.md)
- [중첩된 Graphics 컨테이너 사용](using-nested-graphics-containers.md)
