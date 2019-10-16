---
title: DateTimePicker 컨트롤 개요(Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- DateTimePicker
helpviewer_keywords:
- DateTimePicker control [Windows Forms], about
- date and time picker controls
ms.assetid: 501af106-e9fc-4efc-b9b3-c9d8dcaf8c5c
ms.openlocfilehash: 451172b51427e4932470c53737c7bc276920271c
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61909170"
---
# <a name="datetimepicker-control-overview-windows-forms"></a>DateTimePicker 컨트롤 개요(Windows Forms)
Windows Forms <xref:System.Windows.Forms.DateTimePicker> 컨트롤 날짜 또는 시간 목록에서 단일 항목을 선택할 수 있습니다. 날짜를 나타내는 데, 두 부분으로 표시: 텍스트와 목록 옆의 아래쪽 화살표를 클릭할 때 표시 되는 모눈에 표시 된 날짜를 사용 하 여 드롭다운 목록입니다. 표에서 같습니다는 <xref:System.Windows.Forms.MonthCalendar> 여러 날짜를 선택할 때 사용할 수 있는 컨트롤입니다. 에 대 한 자세한 합니다 <xref:System.Windows.Forms.MonthCalendar> 제어를 참조 하십시오 [MonthCalendar 컨트롤 개요](monthcalendar-control-overview-windows-forms.md)합니다.  
  
## <a name="key-properties"></a>키 속성  
 하려는 경우는 <xref:System.Windows.Forms.DateTimePicker> 을 선택 하거나 시간 날짜 대신 편집에 대 한 컨트롤로 표시할 설정 합니다 <xref:System.Windows.Forms.DateTimePicker.ShowUpDown%2A> 속성을 `true` 및 <xref:System.Windows.Forms.DateTimePicker.Format%2A> 속성을 <xref:System.Windows.Forms.DateTimePickerFormat.Time>입니다. 자세한 내용은 [방법: DateTimePicker 컨트롤을 사용 하 여 시간 표시](how-to-display-time-with-the-datetimepicker-control.md)합니다.  
  
 경우는 <xref:System.Windows.Forms.DateTimePicker.ShowCheckBox%2A> 속성이 `true`, 확인란 컨트롤에서 선택한 날짜 옆에 표시 됩니다. 확인란을 선택 하면 선택한 날짜 및 시간 값을 업데이트할 수 있습니다. 확인란을 선택 하지 않으면 값을 사용할 수 없게 표시 됩니다.  
  
 컨트롤의 <xref:System.Windows.Forms.DateTimePicker.MaxDate%2A> 고 <xref:System.Windows.Forms.DateTimePicker.MinDate%2A> 속성의 날짜 및 시간 범위를 결정 합니다. <xref:System.Windows.Forms.DateTimePicker.Value%2A> 현재 날짜 및 시간에 설정 되어 속성에 포함 되어 있습니다. 자세한 내용은 [방법: 설정 및 Forms DateTimePicker 컨트롤을 Windows 사용 하 여 날짜를 반환](how-to-set-and-return-dates-with-the-windows-forms-datetimepicker-control.md)합니다. 값으로 설정 되는 네 가지 형식으로 표시할 수 있습니다 합니다 <xref:System.Windows.Forms.DateTimePicker.Format%2A> 속성: <xref:System.Windows.Forms.DateTimePickerFormat.Long>를 <xref:System.Windows.Forms.DateTimePickerFormat.Short>를 <xref:System.Windows.Forms.DateTimePickerFormat.Time>, 또는 <xref:System.Windows.Forms.DateTimePickerFormat.Custom>합니다. 사용자 지정 형식의 선택 하는 경우 설정 해야 합니다 <xref:System.Windows.Forms.DateTimePicker.CustomFormat%2A> 속성을 적절 한 문자열입니다. 자세한 내용은 [방법: Windows Forms DateTimePicker 컨트롤을 사용 하는 사용자 지정 형식에 날짜 표시](display-a-date-in-a-custom-format-with-wf-datetimepicker-control.md)합니다.  
  
## <a name="see-also"></a>참고자료

- [방법: Windows Forms DateTimePicker 컨트롤을 사용 하는 사용자 지정 형식에서 날짜를 표시 합니다.](display-a-date-in-a-custom-format-with-wf-datetimepicker-control.md)
- [방법: Windows Forms DateTimePicker 컨트롤을 포함 하는 설정 및 반환 날짜](how-to-set-and-return-dates-with-the-windows-forms-datetimepicker-control.md)
