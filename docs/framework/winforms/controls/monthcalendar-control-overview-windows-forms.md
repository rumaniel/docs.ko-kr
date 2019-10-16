---
title: MonthCalendar 컨트롤 개요(Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- MonthCalendar
helpviewer_keywords:
- calendars [Windows Forms], Windows Forms controls
- calendar controls [Windows Forms], Windows Forms
- MonthCalendar control [Windows Forms], setting the first day of the week
ms.assetid: 788c5325-b721-44ec-95bf-9b680ba0f6a2
ms.openlocfilehash: 8928a78735392920d893661c70554bd35eba2886
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61768487"
---
# <a name="monthcalendar-control-overview-windows-forms"></a>MonthCalendar 컨트롤 개요(Windows Forms)
Windows Forms <xref:System.Windows.Forms.MonthCalendar> 컨트롤 보기 및 날짜 정보를 설정 하는 사용자를 위한 직관적인 그래픽 인터페이스를 제공 합니다. 달력 컨트롤을 표시 합니다:는 요일, 날짜는 강조 표시의 선택한 범위를 사용 하 여 아래에 있는 열으로 정렬 하는 월의 번호가 매겨진된 날짜를 포함 하는 표입니다. 월 캡션의 어느 쪽에 있는 화살표 단추를 클릭 하 여 다른 월을 선택할 수 있습니다. 유사한 달리 <xref:System.Windows.Forms.DateTimePicker> 컨트롤을이 컨트롤을 사용 하 여 둘 이상의 날짜를 선택할 수 있습니다. 에 대 한 자세한 내용은 합니다 <xref:System.Windows.Forms.DateTimePicker> 제어를 참조 하십시오 [DateTimePicker 컨트롤](datetimepicker-control-windows-forms.md)합니다.  
  
## <a name="configuring-the-monthcalendar-control"></a>MonthCalendar 컨트롤 구성  
 <xref:System.Windows.Forms.MonthCalendar> 가능한 컨트롤의 모양이 표시 됩니다. 기본적으로 오늘 날짜는 원이 표시 됩니다와 그리드의 맨 아래에 설명 되어 있습니다. 설정 하 여이 기능을 변경할 수 있습니다 합니다 <xref:System.Windows.Forms.MonthCalendar.ShowToday%2A> 하 고 <xref:System.Windows.Forms.MonthCalendar.ShowTodayCircle%2A> 속성을 `false`입니다. 설정 하 여 일정에 주 번호를 추가할 수도 있습니다는 <xref:System.Windows.Forms.MonthCalendar.ShowWeekNumbers%2A> 속성을 `true`입니다. 설정 하 여는 <xref:System.Windows.Forms.MonthCalendar.CalendarDimensions%2A> 속성인 개월 가로 및 세로로 표시 하는 여러 개 있을 수 있습니다. 기본적으로 첫 번째 일 주를 기준으로 일요일은 표시 되지만 사용 하 여 임의의 날짜를 지정할 수 있습니다는 <xref:System.Windows.Forms.MonthCalendar.FirstDayOfWeek%2A> 속성입니다.  
  
 설정할 수도 있습니다에 표시할 특정 날짜를 한 번만, 매월 또는 매년 굵게 표시 된 추가 하 여 <xref:System.DateTime> 개체를 <xref:System.Windows.Forms.MonthCalendar.BoldedDates%2A>를 <xref:System.Windows.Forms.MonthCalendar.AnnuallyBoldedDates%2A>, 및 <xref:System.Windows.Forms.MonthCalendar.MonthlyBoldedDates%2A> 속성입니다. 자세한 내용은 [방법: Forms MonthCalendar 컨트롤의 Windows를 사용 하 여 특정 날짜를 굵게 표시](display-specific-days-in-bold-with-wf-monthcalendar-control.md)합니다.  
  
 키 속성을 <xref:System.Windows.Forms.MonthCalendar> 컨트롤은 <xref:System.Windows.Forms.MonthCalendar.SelectionRange%2A>, 컨트롤에서 선택한 날짜 범위입니다. 합니다 <xref:System.Windows.Forms.MonthCalendar.SelectionRange%2A> 값에서 설정 선택 될 수 있는 일의 최대 수를 초과할 수 없습니다는 <xref:System.Windows.Forms.MonthCalendar.MaxSelectionCount%2A> 속성입니다. 사용자가 선택할 수는 시작 및 종료 날짜에 따라 결정 됩니다 합니다 <xref:System.Windows.Forms.MonthCalendar.MaxDate%2A> 및 <xref:System.Windows.Forms.MonthCalendar.MinDate%2A> 속성입니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.MonthCalendar>
- [MonthCalendar 컨트롤](monthcalendar-control-windows-forms.md)
