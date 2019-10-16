---
title: ProgressBar 컨트롤 개요(Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- ProgressBar
helpviewer_keywords:
- ProgressBar control [Windows Forms], about ProgressBar control
- progress controls [Windows Forms], about progress controls
ms.assetid: a05d9cba-3a6a-4f8f-94b8-8ec12799fb80
ms.openlocfilehash: 7dd434492cd688527ddbce5aaffa442a0b40a9e4
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69968314"
---
# <a name="progressbar-control-overview-windows-forms"></a>ProgressBar 컨트롤 개요(Windows Forms)
> [!IMPORTANT]
> <xref:System.Windows.Forms.ToolStripProgressBar> 컨트롤은 <xref:System.Windows.Forms.ProgressBar> 컨트롤을 대체하고 여기에 다른 기능을 추가하여 새로 도입된 컨트롤이지만 이전 버전과의 호환성 및 이후 사용 가능성을 고려하여 <xref:System.Windows.Forms.ProgressBar> 컨트롤을 계속 유지하도록 선택할 수 있습니다.  
  
 Windows Forms <xref:System.Windows.Forms.ProgressBar> 컨트롤은 가로 막대에 정렬 된 적절 한 수의 사각형을 표시 하 여 프로세스의 진행 상황을 나타냅니다. 프로세스가 완료 되 면 막대가 채워집니다. 진행률 표시줄은 일반적으로 사용자에 게 프로세스가 완료 될 때까지 대기 하는 시간을 파악 하는 데 사용 됩니다. 예를 들어, 많은 파일이 로드 되는 경우입니다.  
  
> [!NOTE]
> 컨트롤 <xref:System.Windows.Forms.ProgressBar> 은 폼의 가로 방향 으로만 지정할 수 있습니다.  
  
## <a name="key-properties-and-methods"></a>키 속성 및 메서드  
 <xref:System.Windows.Forms.ProgressBar> <xref:System.Windows.Forms.ProgressBar.Minimum%2A> <xref:System.Windows.Forms.ProgressBar.Maximum%2A>컨트롤의 키 속성은, 및입니다. <xref:System.Windows.Forms.ProgressBar.Value%2A> <xref:System.Windows.Forms.ProgressBar.Minimum%2A> 및<xref:System.Windows.Forms.ProgressBar.Maximum%2A> 속성은 진행률 표시줄에 표시할 수 있는 최대값 및 최소값을 설정 합니다. 속성 <xref:System.Windows.Forms.ProgressBar.Value%2A> 은 작업 완료에 대 한 진행률을 나타냅니다. 컨트롤에 표시 되는 막대가 블록으로 구성 되기 때문에 <xref:System.Windows.Forms.ProgressBar> 컨트롤에 표시 되는 값은 속성의 현재 값을 <xref:System.Windows.Forms.ProgressBar.Value%2A> 대략적 으로만 계산 합니다. <xref:System.Windows.Forms.ProgressBar> 컨트롤의 크기에 따라 속성은 <xref:System.Windows.Forms.ProgressBar.Value%2A> 다음 블록을 표시할 시기를 결정 합니다.  
  
 현재 진행 값을 업데이트 하는 가장 일반적인 방법은 <xref:System.Windows.Forms.ProgressBar.Value%2A> 속성을 설정 하는 코드를 작성 하는 것입니다. 큰 파일을 로드 하는 예제에서는 최대 파일 크기 (kb)를 설정할 수 있습니다. 예를 들어 <xref:System.Windows.Forms.ProgressBar.Maximum%2A> 속성이 100 <xref:System.Windows.Forms.ProgressBar.Minimum%2A> 로 설정 된 경우 속성은 10으로 설정 되 고, <xref:System.Windows.Forms.ProgressBar.Value%2A> 속성은 50로 설정 되 고, 5 개의 사각형이 표시 됩니다. 표시할 수 있는 숫자의 절반입니다.  
  
 그러나 <xref:System.Windows.Forms.ProgressBar> <xref:System.Windows.Forms.ProgressBar.Value%2A> 속성을 직접 설정 하는 것 외에도 컨트롤에 표시 된 값을 수정 하는 다른 방법이 있습니다. 속성을 사용 하 여 <xref:System.Windows.Forms.ProgressBar.Value%2A> 속성을 증가 시킬 값을 지정할 수 있습니다. <xref:System.Windows.Forms.ProgressBar.Step%2A> 그런 다음 <xref:System.Windows.Forms.ProgressBar.PerformStep%2A> 메서드를 호출 하면 값이 증가 합니다. 증가값 다를 사용할 수 있습니다는 <xref:System.Windows.Forms.ProgressBar.Increment%2A> 메서드는 증가 하는 데 사용할 값을 지정 합니다 <xref:System.Windows.Forms.ProgressBar.Value%2A> 속성입니다.  
  
 사용자에 게 현재 동작 <xref:System.Windows.Forms.StatusBar> 에 대 한 정보를 그래픽으로 알리는 또 다른 컨트롤은 컨트롤입니다.  
  
> [!IMPORTANT]
> 및 <xref:System.Windows.Forms.StatusStrip> <xref:System.Windows.Forms.StatusBar> <xref:System.Windows.Forms.StatusBarPanel> <xref:System.Windows.Forms.StatusBar> 컨트롤은를 대체 하 고 및 <xref:System.Windows.Forms.StatusBarPanel> 컨트롤에 기능을 추가 합니다. 그러나 및 컨트롤은 이전 버전과의 호환성 및 향후 사용을 위해 유지 됩니다. <xref:System.Windows.Forms.ToolStripStatusLabel> 선택.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ProgressBar>
- [ProgressBar 컨트롤](progressbar-control-windows-forms.md)
