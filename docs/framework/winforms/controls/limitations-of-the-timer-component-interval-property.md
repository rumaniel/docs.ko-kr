---
title: Windows Forms Timer 구성 요소의 Interval 속성에 대한 제한 사항
ms.date: 03/30/2017
helpviewer_keywords:
- timers [Windows Forms], event intervals
- Interval property [Windows Forms], limitations
- timers [Windows Forms], Windows-based
- Timer component [Windows Forms], limitations of Interval property
ms.assetid: 7e5fb513-77e7-4046-a8e8-aab94e61ca0f
ms.openlocfilehash: a9c4fda179e45ad2cf2ee2183e5881e97b763cdc
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64644935"
---
# <a name="limitations-of-the-windows-forms-timer-components-interval-property"></a>Windows Forms Timer 구성 요소의 Interval 속성에 대한 제한 사항
Windows Forms <xref:System.Windows.Forms.Timer> 구성 요소에는 <xref:System.Windows.Forms.Timer.Interval%2A> 타이머 이벤트 및 다음 간에 전달 하는 시간을 밀리초 단위로 지정 하는 속성입니다. 구성 요소를 사용 하지 않도록 설정 하지 않으면 타이머를 계속 수신 하는 <xref:System.Windows.Forms.Timer.Tick> 거의 같은 시간 간격으로 이벤트입니다.  
  
 이 구성 요소는 Windows Forms 환경에 맞게 설계되었습니다. 서버 환경에 적합한 타이머가 필요한 경우 [서버 기반 타이머 소개](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/tb9yt5e6(v=vs.90))를 참조하세요.  
  
## <a name="the-interval-property"></a>간격 속성  
 합니다 <xref:System.Windows.Forms.Timer.Interval%2A> 속성이 프로그래밍할 때 고려해 야 할 몇 가지 제한이 <xref:System.Windows.Forms.Timer> 구성 요소:  
  
- 응용 프로그램 또는 다른 응용 프로그램은 시스템에 큰 부담을 주므로 할 경우-긴 루프, 과도 한 계산 또는 드라이브, 네트워크 또는 포트 액세스 같은-응용 프로그램으로 타이머 이벤트를 자주를 얻지 못할 수는 <xref:System.Windows.Forms.Timer.Interval%2A> 속성을 지정 합니다.  
  
- 간격이 경과 시간에 정확 하 게 보장 되지 않습니다. 정확성을 위해 타이머 필요에 따라 시스템 시간을 확인 대신 해야 계속 누적된 시간을 내부적으로 추적 하려고 합니다.  
  
- 전체 자릿수는 <xref:System.Windows.Forms.Timer.Interval%2A> 속성이 밀리초에서입니다. 일부 컴퓨터에는 시간 (밀리초) 보다 더 높은 해상도 고해상도 카운터를 제공 합니다. 이러한 카운터 컴퓨터의 프로세서 하드웨어에 따라 달라 집니다.
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.Timer>
- [Timer 구성 요소](timer-component-windows-forms.md)
- [Timer 구성 요소 개요](timer-component-overview-windows-forms.md)
