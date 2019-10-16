---
title: SplitContainer 컨트롤 개요(Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- SplitContainer
helpviewer_keywords:
- SplitContainer control [Windows Forms], about SplitContainer control
ms.assetid: 6de5a5f7-97a5-402d-be6d-7e2785483db5
ms.openlocfilehash: 76299d9bbd2b3eac4e765dfacf579c9979721fff
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69963215"
---
# <a name="splitcontainer-control-overview-windows-forms"></a>SplitContainer 컨트롤 개요(Windows Forms)
Windows Forms <xref:System.Windows.Forms.SplitContainer> 컨트롤은 복합으로 간주될 수 있습니다. 이동 가능한 막대로 구분된 두 개의 패널입니다. 마우스 포인터가 막대 위에 있으면 포인터 모양이 변경되어 막대를 이동할 수 있음을 표시합니다.  
  
> [!IMPORTANT]
> **도구 상자** <xref:System.Windows.Forms.SplitContainer> 에서 컨트롤은 <xref:System.Windows.Forms.Splitter> 이전 버전의 Visual Studio에 있던 컨트롤을 대체 합니다. <xref:System.Windows.Forms.SplitContainer> 컨트롤이 <xref:System.Windows.Forms.Splitter> 컨트롤보다 훨씬 선호됩니다. 기존 애플리케이션과의 호환성을 위해 <xref:System.Windows.Forms.Splitter> 클래스도 .NET Framework에 여전히 포함되어 있지만 새 프로젝트에는 <xref:System.Windows.Forms.SplitContainer> 컨트롤을 사용하는 것이 좋습니다.  
  
 <xref:System.Windows.Forms.SplitContainer> 컨트롤을 사용 하면 복잡 한 사용자 인터페이스를 만들 수 있습니다. 대개 한 패널에서 선택 하 여 다른 패널에 표시 되는 개체를 결정할 수 있습니다. 이 정렬은 정보를 표시하고 찾는 데 매우 효율적입니다. 두 개의 패널을 사용 하면 영역의 정보를 집계할 수 있으며, 막대 또는 "분할자"를 사용 하면 사용자가 패널 크기를 쉽게 조정할 수 있습니다.  
  
 두 개 <xref:System.Windows.Forms.SplitContainer> 이상의 컨트롤을중첩하여두번째컨트롤을가로방향으로만들어위쪽및아래쪽패널을<xref:System.Windows.Forms.SplitContainer> 만들 수도 있습니다.  
  
 컨트롤은 <xref:System.Windows.Forms.SplitContainer> 기본적으로 키보드에 액세스할 수 있습니다. <xref:System.Windows.Forms.SplitContainer.IsSplitterFixed%2A> 속성이로 `false`설정 된 경우 사용자는 화살표 키를 눌러 분할자를 이동할 수 있습니다.  
  
 컨트롤의 속성은 <xref:System.Windows.Forms.SplitContainer.Orientation%2A> 컨트롤이 아니라 분할자의 방향을 결정 합니다. <xref:System.Windows.Forms.SplitContainer> 따라서이 속성이로 <xref:System.Windows.Forms.Orientation.Vertical>설정 되 면 분할자는 위쪽에서 아래쪽으로 실행 되어 왼쪽 및 오른쪽 패널을 만듭니다.  
  
 또한 속성의 값은 <xref:System.Windows.Forms.SplitContainer.Orientation%2A> 속성의 값에 따라 달라 집니다. <xref:System.Windows.Forms.SplitContainer.SplitterRectangle%2A> 자세한 내용은 속성을 참조 <xref:System.Windows.Forms.SplitContainer.SplitterRectangle%2A> 하세요.  
  
 <xref:System.Windows.Forms.SplitContainer> 컨트롤의 크기와 움직임을 제한할 수도 있습니다. 속성은 컨트롤의 <xref:System.Windows.Forms.SplitContainer> 크기를 <xref:System.Windows.Forms.SplitContainer.IsSplitterFixed%2A> 조정 하 고 나 서 분할자를 키보드 또는 마우스로 이동할 수 있는지 여부를 결정 하는 패널을 결정 합니다. <xref:System.Windows.Forms.SplitContainer.FixedPanel%2A>  
  
> [!NOTE]
> <xref:System.Windows.Forms.SplitContainer.IsSplitterFixed%2A> 속성이 <xref:System.Windows.Forms.SplitContainer.SplitterDistance%2A> 로 `true`설정 된 경우에도 분할자는 속성을 사용 하는 등의 방법으로 프로그래밍 방식으로 계속 이동할 수 있습니다.  
  
 마지막으로, <xref:System.Windows.Forms.SplitContainer> 컨트롤의 각 패널에는 개별 크기를 결정 하는 속성이 있습니다.  
  
## <a name="commonly-used-properties-methods-and-events"></a>일반적으로 사용되는 속성, 메서드 및 이벤트  
  
|이름|Description|  
|----------|-----------------|  
|<xref:System.Windows.Forms.SplitContainer.FixedPanel%2A> 속성|컨트롤의 크기를 조정 하 고 <xref:System.Windows.Forms.SplitContainer> 나 서 동일한 크기를 유지할 패널을 결정 합니다.|  
|<xref:System.Windows.Forms.SplitContainer.IsSplitterFixed%2A> 속성|분할자를 키보드 또는 마우스로 이동할 수 있는지 여부를 결정 합니다.|  
|<xref:System.Windows.Forms.SplitContainer.Orientation%2A> 속성|분할자를 가로 또는 세로로 정렬할지 여부를 결정 합니다.|  
|<xref:System.Windows.Forms.SplitContainer.SplitterDistance%2A> 속성|왼쪽 또는 위쪽 가장자리에서 이동할 수 있는 분할자 막대 까지의 거리 (픽셀 단위)를 결정 합니다.|  
|<xref:System.Windows.Forms.SplitContainer.SplitterIncrement%2A> 속성|사용자가 분할자를 이동할 수 있는 최소 거리 (픽셀)를 결정 합니다.|  
|<xref:System.Windows.Forms.SplitContainer.SplitterWidth%2A> 속성|분할자의 두께 (픽셀 단위)를 결정 합니다.|  
|<xref:System.Windows.Forms.SplitContainer.SplitterMoving> 이벤트|분할자를 이동할 때 발생 합니다.|  
|<xref:System.Windows.Forms.SplitContainer.SplitterMoved> 이벤트|분할자를 이동할 때 발생 합니다.|  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.SplitContainer>
- [SplitContainer 컨트롤](splitcontainer-control-windows-forms.md)
- [SplitContainer 컨트롤 샘플](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/0ffz7d1b(v=vs.90))
