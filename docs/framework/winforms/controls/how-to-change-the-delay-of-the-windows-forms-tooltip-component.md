---
title: '방법: Windows Forms ToolTip 구성 요소의 지연 변경'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- ToolTip component [Windows Forms], delay values
- tooltips [Windows Forms], delay values
- examples [Windows Forms], tooltips
ms.assetid: 08979ba7-dd84-477b-ab17-8d06e759be99
ms.openlocfilehash: cf257cccd272c16c3d7c3d403456265444fc8ac8
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61781240"
---
# <a name="how-to-change-the-delay-of-the-windows-forms-tooltip-component"></a>방법: Windows Forms ToolTip 구성 요소의 지연 변경
Windows Forms에 대해 설정할 수 있는 지연 값이 여러 개 <xref:System.Windows.Forms.ToolTip> 구성 요소입니다. 이러한 모든 속성에 대 한 측정 단위 시간 (밀리초)입니다. <xref:System.Windows.Forms.ToolTip.InitialDelay%2A> 속성 표시할 도구 설명 문자열에 대 한 연결된 된 컨트롤에서 사용자를 가리켜야 기간을 결정 합니다. <xref:System.Windows.Forms.ToolTip.ReshowDelay%2A> 속성 간 한 도구 설명이 연결 된 컨트롤에서 마우스를 움직일 때 표시할 도구 설명 문자열의 후속 걸리는 시간 (밀리초)의 수를 설정 합니다. <xref:System.Windows.Forms.ToolTip.AutoPopDelay%2A> 속성 도구 설명 문자열이 표시 되는 시간의 길이 결정 합니다. 개별적으로 또는 값을 설정 하 여 이러한 값을 설정할 수는 <xref:System.Windows.Forms.ToolTip.AutomaticDelay%2A> 속성, 속성에 할당 된 값에 따라 설정 되는 다른 지연은 <xref:System.Windows.Forms.ToolTip.AutomaticDelay%2A> 속성입니다. 예를 들어, <xref:System.Windows.Forms.ToolTip.AutomaticDelay%2A> N 값으로 설정 됩니다 <xref:System.Windows.Forms.ToolTip.InitialDelay%2A> N으로 설정 됩니다 <xref:System.Windows.Forms.ToolTip.ReshowDelay%2A> 의 값으로 설정 됩니다 <xref:System.Windows.Forms.ToolTip.AutomaticDelay%2A> 5로 나눈 (또는 N/5) 및 <xref:System.Windows.Forms.ToolTip.AutoPopDelay%2A> 5 번의 값에 해당 값으로 설정 됩니다는 <xref:System.Windows.Forms.ToolTip.AutomaticDelay%2A> 속성 (또는 5N).  
  
### <a name="to-set-the-delay"></a>지연 시간을 설정 하려면  
  
1. 이 예제에 표시 된 대로 다음 속성을 설정 합니다.  
  
    ```vb  
    ToolTip1.InitialDelay = 500  
    ToolTip1.ReshowDelay = 100  
    ToolTip1.AutoPopDelay = 5000  
    ```  
  
    ```csharp  
    ToolTip1.InitialDelay = 500;  
    ToolTip1.ReshowDelay = 100;  
    ToolTip1.AutoPopDelay = 5000;  
    ```  
  
    ```cpp  
    toolTip1->InitialDelay = 500;  
    toolTip1->ReshowDelay = 100;  
    toolTip1->AutoPopDelay = 5000;  
    ```  
  
## <a name="see-also"></a>참고자료

- [ToolTip 구성 요소 개요](tooltip-component-overview-windows-forms.md)
- [방법: 디자인 타임에 Windows Form의 컨트롤에 도구 설명 설정](how-to-set-tooltips-for-controls-on-a-windows-form-at-design-time.md)
- [ToolTip 구성 요소](tooltip-component-windows-forms.md)
