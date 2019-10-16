---
title: 사용자 지정 컨트롤 그리기 및 렌더링
ms.date: 03/30/2017
helpviewer_keywords:
- custom controls [Windows Forms], rendering
- custom controls [Windows Forms], painting
- user controls [Windows Forms], painting
ms.assetid: a09dbf76-0966-4cbf-a66a-2083ba98e068
ms.openlocfilehash: 14abac5678bfffa3cdb61307fd3cb54681c82a99
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67506091"
---
# <a name="custom-control-painting-and-rendering"></a>사용자 지정 컨트롤 그리기 및 렌더링
컨트롤 그리기 사용자 지정.NET Framework로 쉽게 수행할 수 있는 여러 복잡 한 작업 중 하나입니다. 사용자 지정 컨트롤을 작성할 때 컨트롤의 그래픽 모양에 대 한 여러 옵션이 있습니다. 상속 되는 컨트롤을 작성 하는 경우는 `Control`, 컨트롤의 그래픽 표현을 렌더링할 수 있도록 코드를 제공 해야 합니다. 상속 하 여 사용자 정의 컨트롤을 만드는 경우는 `UserControl`, 상속 되는지 또는 Windows Forms 컨트롤 중 하나에서 표준 그래픽 표시를 재정의 하 고 수 있습니다 그래픽 코드를 제공 합니다. 구성 요소 컨트롤에 대 한 사용자 지정 렌더링을 제공 하려는 경우는 `UserControl` 을 제작 하는, 옵션은 더욱 제한 되지만 광범위 한 컨트롤 및 응용 프로그램에 대 한 그래픽 기능을 계속 사용할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [Windows Forms 컨트롤 렌더링](rendering-a-windows-forms-control.md)  
 컨트롤을 표시 하는 논리를 프로그래밍 하는 방법을 보여 줍니다.  
  
 [사용자가 그린 컨트롤](user-drawn-controls.md)  
 작성 하 고 컨트롤에 대 한 렌더링 코드를 재정의 하는 단계에 간략하게 설명 합니다.  
  
 [구성 요소 컨트롤](constituent-controls.md)  
 사용자 컨트롤 및 폼에에서 구성 요소 컨트롤에 대 한 사용자 지정 렌더링 코드를 구현 하는 방법을 설명 합니다.  
  
 [방법: 런타임에 컨트롤 숨기기](how-to-make-your-control-invisible-at-run-time.md)  
 사용 하는 방법을 보여 줍니다는 <xref:System.Windows.Forms.Control.Visible%2A> 속성을 숨기 거 나 컨트롤을 표시 합니다.  
  
 [방법: 컨트롤에 투명 한 배경을 제공합니다](how-to-give-your-control-a-transparent-background.md)  
 사용 하는 방법을 보여 줍니다는 <xref:System.Windows.Forms.Control.SetStyle%2A> 불투명, 투명 하 게 또는 부분적으로 투명 한 배경색을 만드는 방법.  
  
 [비주얼 스타일을 사용하여 컨트롤 렌더링](rendering-controls-with-visual-styles.md)  
 지 원하는 운영 체제에서 비주얼 스타일을 사용 하 여 컨트롤을 렌더링 하는 방법을 보여 줍니다.  
  
## <a name="reference"></a>참조  
 <xref:System.Windows.Forms.Control>  
 이 클래스를 설명하고 모든 해당 멤버의 링크를 포함합니다.  
  
 <xref:System.Windows.Forms.UserControl>  
 이 클래스를 설명하고 모든 해당 멤버의 링크를 포함합니다.  
  
 <xref:System.Windows.Forms.Control.OnPaint%2A>  
 이 메서드를 설명합니다.  
  
## <a name="related-sections"></a>관련 단원  
 [방법: 그리는 데 필요한 그래픽 개체 만들기](../advanced/how-to-create-graphics-objects-for-drawing.md)  
 Visual Studio의 관점에서 GDI + 그래픽 기능을 소개 하 고 자세한 정보에 대 한 링크를 제공 합니다.  
  
 [사용자 지정 컨트롤의 종류](varieties-of-custom-controls.md)  
 작성할 수 있습니다 하는 사용자 지정 컨트롤의 종류를 설명 합니다.
