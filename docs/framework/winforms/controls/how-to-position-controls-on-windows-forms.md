---
title: '방법: Windows Forms에서 컨트롤 배치'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
f1_keywords:
- Location
- Location.Y
- Location.X
helpviewer_keywords:
- controls [Windows Forms]
- controls [Windows Forms], moving
- snaplines
- controls [Windows Forms], positioning
ms.assetid: 4693977e-34a4-4f19-8221-68c3120c2b2b
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 1cc2cb4c749b7290a6edf914a8e6a697006ef43c
ms.sourcegitcommit: 37616676fde89153f563a485fc6159fc57326fc2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2019
ms.locfileid: "69987078"
---
# <a name="how-to-position-controls-on-windows-forms"></a>방법: Windows Forms에 컨트롤 배치

컨트롤의 위치를 지정 하려면 Visual Studio에서 Windows Forms 디자이너를 사용 하거나 <xref:System.Windows.Forms.Control.Location%2A> 속성을 지정 합니다.

## <a name="position-a-control-on-the-design-surface-of-the-windows-forms-designer"></a>Windows Forms 디자이너의 디자인 화면에 컨트롤 배치

Visual Studio에서 마우스를 사용 하 여 컨트롤을 적절 한 위치로 끕니다.

> [!NOTE]
> 컨트롤을 선택 하 고 화살표 키로 이동 하 여 더 정확 하 게 배치 합니다. 또한 *맞춤선* 은 폼에 컨트롤을 정확 하 게 배치할 수 있도록 지원 합니다. 자세한 내용은 [연습: 맞춤선](walkthrough-arranging-controls-on-windows-forms-using-snaplines.md)을 사용 하 여 Windows Forms에 컨트롤 정렬

## <a name="position-a-control-using-the-properties-window"></a>속성 창를 사용 하 여 컨트롤 배치

1. Visual Studio에서 배치 하려는 컨트롤을 선택 합니다.

2. **속성** 창에서 <xref:System.Windows.Forms.Control.Location%2A> 속성에 대 한 값을 쉼표로 구분 하 여 입력 하 여 해당 컨테이너 내에 컨트롤을 배치 합니다.

   첫 번째 숫자 (X)는 컨테이너의 왼쪽 테두리에서의 거리입니다. 두 번째 숫자 (Y)는 컨테이너 영역의 위쪽 테두리에서 픽셀 단위로 측정 된 거리입니다.

   > [!NOTE]
   > <xref:System.Windows.Forms.Control.Location%2A> 속성을 확장 하 여 **X** 및 **Y** 값을 개별적으로 입력할 수 있습니다.

## <a name="position-a-control-programmatically"></a>프로그래밍 방식으로 컨트롤 배치

1. 컨트롤의 <xref:System.Drawing.Point>속성을로 설정 합니다. <xref:System.Windows.Forms.Control.Location%2A>

    ```vb
    Button1.Location = New Point(100, 100)
    ```

    ```csharp
    button1.Location = new Point(100, 100);
    ```

    ```cpp
    button1->Location = Point(100, 100);
    ```

2. 하위 속성을 <xref:System.Windows.Forms.Control.Left%2A> 사용 하 여 컨트롤 위치의 X 좌표를 변경 합니다.

    ```vb
    Button1.Left = 300
    ```

    ```csharp
    button1.Left = 300;
    ```

    ```cpp
    button1->Left = 300;
    ```

## <a name="increment-a-controls-location-programmatically"></a>컨트롤의 위치를 프로그래밍 방식으로 증가

<xref:System.Windows.Forms.Control.Left%2A> 하위 속성을 설정 하 여 컨트롤의 X 좌표를 늘립니다.

```vb
Button1.Left += 200
```

```csharp
button1.Left += 200;
```

```cpp
button1->Left += 200;
```

> [!NOTE]
> 컨트롤의 X 및 Y 위치를 동시에 설정 하려면 속성을사용합니다.<xref:System.Windows.Forms.Control.Location%2A> 위치를 개별적으로 설정 하려면 컨트롤 <xref:System.Windows.Forms.Control.Left%2A> 의 (**X**) 또는 <xref:System.Windows.Forms.Control.Top%2A> (**Y**) 하위 속성을 사용 합니다. 이 구조체는 단추의 좌표 복사본을 포함 하므로 단추의 위치를 나타내는 <xref:System.Drawing.Point> 구조체의 X 및 Y 좌표를 암시적으로 설정 하지 마십시오.

## <a name="see-also"></a>참고자료

- [Windows Forms 컨트롤](index.md)
- [연습: 맞춤선을 사용 하 여 Windows Forms에서 컨트롤 정렬](walkthrough-arranging-controls-on-windows-forms-using-snaplines.md)
- [연습: TableLayoutPanel를 사용 하 여 Windows Forms에서 컨트롤 정렬](walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)
- [연습: FlowLayoutPanel를 사용 하 여 Windows Forms에서 컨트롤 정렬](walkthrough-arranging-controls-on-windows-forms-using-a-flowlayoutpanel.md)
- [개별 Windows Forms 컨트롤 레이블 지정 및 바로 가기 제공](labeling-individual-windows-forms-controls-and-providing-shortcuts-to-them.md)
- [Windows Forms에 사용할 수 있는 컨트롤](controls-to-use-on-windows-forms.md)
- [기능별 Windows Forms 컨트롤](windows-forms-controls-by-function.md)
- [방법: Windows Forms의 화면 위치를 설정 합니다.](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/52aha046(v=vs.100))
