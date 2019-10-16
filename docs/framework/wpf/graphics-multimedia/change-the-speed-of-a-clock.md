---
title: '방법: Timeline 속도를 변경하지 않고 시계 속도 변경'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- speed of Clock [WPF], changing
- clocks [WPF], changing speed of
ms.assetid: 72f36dd0-f085-445d-8589-19a83fe74f5e
ms.openlocfilehash: 19e6874b9b472cb4a5f716677f99af03f2b73b10
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62010191"
---
# <a name="how-to-change-the-speed-of-a-clock-without-changing-the-speed-of-its-timeline"></a>방법: Timeline 속도를 변경하지 않고 시계 속도 변경
A <xref:System.Windows.Media.Animation.ClockController> 개체의 <xref:System.Windows.Media.Animation.ClockController.SpeedRatio%2A> 속성의 속도 변경할 수 있습니다를 <xref:System.Windows.Media.Animation.Clock> 변경 하지 않고 합니다 <xref:System.Windows.Media.Animation.Timeline.SpeedRatio%2A> 클록의의 <xref:System.Windows.Media.Animation.Timeline>합니다. 다음 예제에서는 <xref:System.Windows.Media.Animation.ClockController> 대화형으로 수정 하는 데 사용 되는 <xref:System.Windows.Media.Animation.ClockController.SpeedRatio%2A> 클록의 합니다. 합니다 <xref:System.Windows.Media.Animation.Clock.CurrentGlobalSpeedInvalidated> 이벤트 및 클록의 <xref:System.Windows.Media.Animation.Clock.CurrentGlobalSpeed%2A> 속성은 클록의 현재 전역 속도 표시 하는 데 사용 됩니다 될 때마다 해당 대화형 <xref:System.Windows.Media.Animation.ClockController.SpeedRatio%2A> 변경 됩니다.  
  
## <a name="example"></a>예제  
 [!code-csharp[timingbehaviors_procedural_snip#GraphicsMMClockControllerSpeedRatioExample](~/samples/snippets/csharp/VS_Snippets_Wpf/timingbehaviors_procedural_snip/CSharp/ClockControllerSpeedRatioExample.cs#graphicsmmclockcontrollerspeedratioexample)]
 [!code-vb[timingbehaviors_procedural_snip#GraphicsMMClockControllerSpeedRatioExample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/timingbehaviors_procedural_snip/visualbasic/clockcontrollerspeedratioexample.vb#graphicsmmclockcontrollerspeedratioexample)]
