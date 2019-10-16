---
title: '방법: 디자인 타임에 Windows Form의 컨트롤에 대한 도구 설명 설정'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- tooltips [Windows Forms], for controls
- examples [Windows Forms], tooltips
ms.assetid: c4b60637-4c0a-44c2-a103-f66dff887936
ms.openlocfilehash: 0d6725fc1a00826870e6400bffce63a1788e802c
ms.sourcegitcommit: 0d0a6e96737dfe24d3257b7c94f25d9500f383ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65211693"
---
# <a name="how-to-set-tooltips-for-controls-on-a-windows-form-at-design-time"></a>방법: 디자인 타임에 Windows Form의 컨트롤에 도구 설명 설정

설정할 수 있습니다는 <xref:System.Windows.Forms.ToolTip> Visual Studio에서 Windows Forms 디자이너 또는 코드에서 문자열입니다. 에 대 한 자세한 내용은 합니다 <xref:System.Windows.Forms.ToolTip> 구성 요소를 참조 하세요 [ToolTip 구성 요소 개요](tooltip-component-overview-windows-forms.md)합니다.

## <a name="set-a-tooltip-programmatically"></a>프로그래밍 방식으로 도구 설명 설정

1. 도구 설명이 표시 되는 컨트롤을 추가 합니다.

2. 사용 된 <xref:System.Windows.Forms.ToolTip.SetToolTip%2A> 메서드의 <xref:System.Windows.Forms.ToolTip> 구성 요소입니다.

    ```vb
    ' In this example, Button1 is the control to display the ToolTip.
    ToolTip1.SetToolTip(Button1, "Save changes")
    ```

    ```csharp
    // In this example, button1 is the control to display the ToolTip.
    toolTip1.SetToolTip(button1, "Save changes");
    ```

    ```cpp
    // In this example, button1 is the control to display the ToolTip.
    toolTip1->SetToolTip(button1, "Save changes");
    ```

## <a name="set-a-tooltip-in-the-designer"></a>디자이너에서 도구 설명 설정

1. Visual Studio에서 추가 <xref:System.Windows.Forms.ToolTip> 폼에 구성 요소입니다.

2. 도구 설명 표시 되거나 폼에 추가 하는 컨트롤을 선택 합니다.

3. 에 **속성** 창에서 **ToolTip1의 도구 설명** 텍스트 문자열을 적절 한 값입니다.

### <a name="to-remove-a-tooltip-programmatically"></a>도구 설명에 프로그래밍 방식으로 제거 하려면

1. 사용 된 <xref:System.Windows.Forms.ToolTip.SetToolTip%2A> 메서드의 <xref:System.Windows.Forms.ToolTip> 구성 요소입니다.

    ```vb
    ' In this example, Button1 is the control displaying the ToolTip.
    ToolTip1.SetToolTip(Button1, Nothing)
    ```

    ```csharp
    // In this example, button1 is the control displaying the ToolTip.
    toolTip1.SetToolTip(button1, null);
    ```

    ```cpp
    // In this example, button1 is the control displaying the ToolTip.
    toolTip1->SetToolTip(button1, NULL);
    ```

## <a name="remove-a-tooltip-in-the-designer"></a>디자이너에서 도구 설명을 제거합니다

1. Visual Studio에서 도구 설명에 표시 되는 컨트롤을 선택 합니다.

2. 에 **속성** 창에서 텍스트를 삭제 합니다 **ToolTip1의 도구 설명**합니다.

## <a name="see-also"></a>참고자료

- [ToolTip 구성 요소 개요](tooltip-component-overview-windows-forms.md)
- [방법: Windows Forms ToolTip 구성 요소의 지연 변경](how-to-change-the-delay-of-the-windows-forms-tooltip-component.md)
- [ToolTip 구성 요소](tooltip-component-windows-forms.md)
