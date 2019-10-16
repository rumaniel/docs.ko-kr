---
title: 속성 변경 이벤트
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- custom controls [Windows Forms], property changes (using code)
- properties [Windows Forms], changes
ms.assetid: 268039ec-5aaa-4d76-b902-acccb036c850
ms.openlocfilehash: cabfd9e799288a332a0b2f96140f5f1cc328508b
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61755430"
---
# <a name="property-changed-events"></a>속성 변경 이벤트
명명 된 속성 알림을 보내도록 컨트롤 원하면 *PropertyName* 명명 된 이벤트를 정의 하는 변경 내용을 *PropertyName* `Changed` 라는 이름의 메서드 `On` *PropertyName* `Changed` 는 이벤트를 발생 시킵니다. Windows Forms의 명명 정책을 단어를 추가 하는 것 *Changed* 속성의 이름입니다. 속성 변경 이벤트의 관련된 이벤트 대리자 형식이 <xref:System.EventHandler>, 이벤트 데이터 형식이 <xref:System.EventArgs>합니다. 기본 클래스 <xref:System.Windows.Forms.Control> 와 같은 대부분의 속성 변경 이벤트를 정의 <xref:System.Windows.Forms.Control.BackColorChanged>를 <xref:System.Windows.Forms.Control.BackgroundImageChanged>를 <xref:System.Windows.Forms.Control.FontChanged>, <xref:System.Windows.Forms.Control.LocationChanged>, 등입니다. 이벤트에 대 한 배경 정보를 참조 하세요 [이벤트](../../../standard/events/index.md) 하 고 [Windows Forms 컨트롤의 이벤트](events-in-windows-forms-controls.md)합니다.  
  
 속성 변경 이벤트 소비자 컨트롤의 변경에 응답 하는 이벤트 처리기를 연결할 수 있도록 하므로 유용 합니다. 컨트롤을 발생 시킨 속성 변경 이벤트에 응답 하는 경우 해당 재정의 `On` *PropertyName* `Changed` 이벤트에 대리자를 연결 하는 대신 메서드. 일반적으로 컨트롤을 다른 속성을 업데이트 하거나 일부 또는 모든 그리기 화면을 그려서 속성 변경 이벤트에 응답 합니다.  
  
 다음 예제와 방법을 `FlashTrackBar` 사용자 지정 컨트롤에서 상속 하는 속성 변경 이벤트의 일부에 대 한 응답 <xref:System.Windows.Forms.Control>합니다. 전체 샘플을 참조 하세요. [방법: 진행률을 보여 주는 Windows Forms 컨트롤 만들기](how-to-create-a-windows-forms-control-that-shows-progress.md)합니다.  
  
 [!code-csharp[System.Windows.Forms.FlashTrackBar#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/CS/FlashTrackBar.cs#2)]
 [!code-vb[System.Windows.Forms.FlashTrackBar#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FlashTrackBar/VB/FlashTrackBar.vb#2)]  
  
## <a name="see-also"></a>참고자료

- [이벤트](../../../standard/events/index.md)
- [Windows Forms 컨트롤의 이벤트](events-in-windows-forms-controls.md)
- [Windows Forms 컨트롤의 속성](properties-in-windows-forms-controls.md)
