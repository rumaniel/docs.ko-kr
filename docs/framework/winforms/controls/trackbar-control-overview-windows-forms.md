---
title: TrackBar 컨트롤 개요(Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- TrackBar
helpviewer_keywords:
- sliders [Windows Forms], about sliders
- TrackBar control [Windows Forms], about TrackBar control
- slider controls [Windows Forms], about slider controls
ms.assetid: 95910ecb-8a4c-4776-89fa-206c89ed6973
ms.openlocfilehash: 1606db73485944f3dfa8b9c084bffda817520c7c
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62009268"
---
# <a name="trackbar-control-overview-windows-forms"></a>TrackBar 컨트롤 개요(Windows Forms)
Windows Forms <xref:System.Windows.Forms.TrackBar> 시각적으로 조정 된 숫자 설정을 하거나 많은 양의 정보를 탐색 하기 위한 컨트롤 (라고도 "slider" 컨트롤)는 데 사용 합니다. <xref:System.Windows.Forms.TrackBar> 컨트롤에 두 부분으로 구성 합니다:는 엄지 단추 라고도 슬라이더의 눈금 표시 합니다. Thumb는 조정할 수 있는 부분입니다. 해당 위치에 해당 하는 <xref:System.Windows.Forms.TrackBar.Value%2A> 속성입니다. 눈금 표시 되는 정기적으로 배치 되는 시각적 표시기입니다. 트랙 표시줄을 가로 또는 세로로 정렬할 수 있습니다 지정 하는 단위로 이동 합니다. 예를 들어 시스템에 대 한 커서 깜박임 속도 또는 마우스 속도 제어 하려면 트랙 표시줄을 사용할 수 있습니다.  
  
## <a name="key-properties"></a>키 속성  
 키 속성을 <xref:System.Windows.Forms.TrackBar> 컨트롤은 <xref:System.Windows.Forms.TrackBar.Value%2A>, <xref:System.Windows.Forms.TrackBar.TickFrequency%2A>, <xref:System.Windows.Forms.TrackBar.Minimum%2A>, 및 <xref:System.Windows.Forms.TrackBar.Maximum%2A>합니다. <xref:System.Windows.Forms.TrackBar.TickFrequency%2A> 눈금 사이의 간격이입니다. <xref:System.Windows.Forms.TrackBar.Minimum%2A> 및 <xref:System.Windows.Forms.TrackBar.Maximum%2A> 트랙 표시줄 위에 나타낼 수 있는 최소 및 최대 값입니다.  
  
 다른 두 가지 중요 한 속성은 <xref:System.Windows.Forms.TrackBar.SmallChange%2A> 고 <xref:System.Windows.Forms.TrackBar.LargeChange%2A>입니다. 값을 <xref:System.Windows.Forms.TrackBar.SmallChange%2A> 속성 thumb은 왼쪽 또는 오른쪽 화살표 키를 누르면에 대 한 응답에서 이동 하는 위치입니다. 값을 <xref:System.Windows.Forms.TrackBar.LargeChange%2A> 속성이 위치 엄지 단추는 PAGE UP 또는 PAGE DOWN 키를 누른 상태에 대 한 응답으로 이동 하거나 thumb의 어느 쪽에 트랙 표시줄 마우스에 대 한 응답에서 클릭할 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.TrackBar>
- [TrackBar 컨트롤](trackbar-control-windows-forms.md)
