---
title: '방법: 양식의 가장자리에 컨트롤 맞춤'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Dock property [Windows Forms], aligning controls (using code)
- forms [Windows Forms], aligning controls
- controls [Windows Forms], aligning on forms
- custom controls [Windows Forms], docking using code
ms.assetid: 5994cb59-242b-4e75-bd0e-62879c34d702
ms.openlocfilehash: 5d662489b7e31f391bbd508409e69c091a25592c
ms.sourcegitcommit: 121ab70c1ebedba41d276e436dd2b1502748a49f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2019
ms.locfileid: "70015938"
---
# <a name="how-to-align-a-control-to-the-edges-of-forms"></a>방법: 양식의 가장자리에 컨트롤 맞춤

<xref:System.Windows.Forms.Control.Dock%2A> 속성을 설정하여 양식 가장자리에 맞춰서 컨트롤을 정렬할 수 있습니다. 이 속성은 양식에서 컨트롤의 위치를 지정합니다. <xref:System.Windows.Forms.Control.Dock%2A> 속성은 다음 값으로 설정할 수 있습니다.

|설정|컨트롤에 대한 영향|
|-------------|----------------------------|
|<xref:System.Windows.Forms.DockStyle.Bottom>|양식의 아래쪽에 도킹합니다.|
|<xref:System.Windows.Forms.DockStyle.Fill>|양식의 나머지 공간을 모두 채웁니다.|
|<xref:System.Windows.Forms.DockStyle.Left>|양식의 왼쪽에 도킹합니다.|
|<xref:System.Windows.Forms.DockStyle.None>|도킹하지 않고 <xref:System.Windows.Forms.Control.Location%2A> 속성으로 지정된 위치에 표시합니다.|
|<xref:System.Windows.Forms.DockStyle.Right>|컨트롤을 양식의 오른쪽에 도킹합니다.|
|<xref:System.Windows.Forms.DockStyle.Top>|양식의 위쪽에 도킹합니다.|

Visual Studio에서는 디자인 타임에 이 기능을 지원합니다.

## <a name="set-the-dock-property-for-your-control-at-run-time"></a>런타임에 컨트롤의 Dock 속성 설정

코드에서 <xref:System.Windows.Forms.Control.Dock%2A> 속성을 적절한 값으로 설정합니다.

```vb
' To set the Dock property internally.
Me.Dock = DockStyle.Top
' To set the Dock property from another object.
UserControl1.Dock = DockStyle.Top
```

```csharp
// To set the Dock property internally.
this.Dock = DockStyle.Top;
// To set the Dock property from another object.
UserControl1.Dock = DockStyle.Top;
```

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.Control.Dock%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.Control.Anchor%2A?displayProperty=nameWithType>
- [.NET Framework에서 사용자 지정 Windows Forms 컨트롤 개발](developing-custom-windows-forms-controls.md)
- [방법: FlowLayoutPanel 컨트롤에서 자식 컨트롤 고정 및 도킹](how-to-anchor-and-dock-child-controls-in-a-flowlayoutpanel-control.md)
- [방법: TableLayoutPanel 컨트롤에서 자식 컨트롤 고정 및 도킹](how-to-anchor-and-dock-child-controls-in-a-tablelayoutpanel-control.md)
- [AutoSize 속성 개요](autosize-property-overview.md)
