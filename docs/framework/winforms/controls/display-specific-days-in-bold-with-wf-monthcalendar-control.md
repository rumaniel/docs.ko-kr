---
title: '방법: Windows Forms MonthCalendar 컨트롤을 사용하여 특정 날짜를 굵게 표시'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- calendars [Windows Forms], displaying dates in bold
- examples [Windows Forms], calendar controls
- GetDayBold event
- MonthCalendar control [Windows Forms], dates displayed in bold
ms.assetid: 8b20db5b-8118-4825-90e8-2c45c186ac7d
ms.openlocfilehash: 27b19e47d108b9af43a6d8882264d62c726ffe56
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61972083"
---
# <a name="how-to-display-specific-days-in-bold-with-the-windows-forms-monthcalendar-control"></a>방법: Windows Forms MonthCalendar 컨트롤을 사용하여 특정 날짜를 굵게 표시
Windows Forms <xref:System.Windows.Forms.MonthCalendar> 반복적으로 또는 단일 날짜로 컨트롤 굵은 글꼴로 일 표시할 수 있습니다. 주말과 휴일 등의 특정 날짜에 주목 하도록이 수행할 수 있습니다.  
  
 이 기능을 제어 하는 세 가지 속성입니다. <xref:System.Windows.Forms.MonthCalendar.BoldedDates%2A> 속성 단일 날짜를 포함 합니다. <xref:System.Windows.Forms.MonthCalendar.AnnuallyBoldedDates%2A> 속성 매년 굵게 표시 되는 날짜가 포함 되어 있습니다. <xref:System.Windows.Forms.MonthCalendar.MonthlyBoldedDates%2A> 속성 매월 굵게 표시 되는 날짜가 포함 되어 있습니다. 이러한 각 속성의 배열을 포함 <xref:System.DateTime> 개체입니다. 추가 하거나, 이러한 목록 중 하나에서 날짜를 제거 하려면 추가 하거나 제거 해야 합니다는 <xref:System.DateTime> 개체입니다.  
  
### <a name="to-make-a-date-appear-in-bold-type"></a>날짜를 굵게 표시 하려면  
  
1. 만들기는 <xref:System.DateTime> 개체입니다.  
  
    ```vb  
    Dim myVacation1 As Date = New DateTime(2001, 6, 10)  
    Dim myVacation2 As Date = New DateTime(2001, 6, 17)  
    ```  
  
    ```csharp  
    DateTime myVacation1 = new DateTime(2001, 6, 10);  
    DateTime myVacation2 = new DateTime(2001, 6, 17);  
    ```  
  
    ```cpp  
    DateTime myVacation1 = DateTime(2001, 6, 10);  
    DateTime myVacation2 = DateTime(2001, 6, 17);  
    ```  
  
2. 호출 하 여 하나의 날짜를 굵게 합니다 <xref:System.Windows.Forms.MonthCalendar.AddBoldedDate%2A>, <xref:System.Windows.Forms.MonthCalendar.AddAnnuallyBoldedDate%2A>, 또는 <xref:System.Windows.Forms.MonthCalendar.AddMonthlyBoldedDate%2A> 메서드의 <xref:System.Windows.Forms.MonthCalendar> 제어 합니다.  
  
    ```vb  
    MonthCalendar1.AddBoldedDate(myVacation1)  
    MonthCalendar1.AddBoldedDate(myVacation2)  
    ```  
  
    ```csharp  
    monthCalendar1.AddBoldedDate(myVacation1);  
    monthCalendar1.AddBoldedDate(myVacation2);  
    ```  
  
    ```cpp  
    monthCalendar1->AddBoldedDate(myVacation1);  
    monthCalendar1->AddBoldedDate(myVacation2);  
    ```  
  
     – 또는 –  
  
     굵게 표시 된 날짜 집합이 한 번에 모두의 배열을 만들어 <xref:System.DateTime> 개체 및 속성 중 하나에 할당 합니다.  
  
    ```vb  
    Dim VacationDates As DateTime() = {myVacation1, myVacation2}  
    MonthCalendar1.BoldedDates = VacationDates  
    ```  
  
    ```csharp  
    DateTime[] VacationDates = {myVacation1, myVacation2};  
    monthCalendar1.BoldedDates = VacationDates;  
    ```  
  
    ```cpp  
    Array<DateTime>^ VacationDates = {myVacation1, myVacation2};  
    monthCalendar1->BoldedDates = VacationDates;  
    ```  
  
### <a name="to-make-a-date-appear-in-the-regular-font"></a>일반 글꼴로 표시할 날짜를 확인 합니다.  
  
1. 호출 하 여 일반 글꼴로 표시 단일 굵게 표시 된 날짜를 확인 합니다 <xref:System.Windows.Forms.MonthCalendar.RemoveBoldedDate%2A>, <xref:System.Windows.Forms.MonthCalendar.RemoveAnnuallyBoldedDate%2A>, 또는 <xref:System.Windows.Forms.MonthCalendar.RemoveMonthlyBoldedDate%2A> 메서드.  
  
    ```vb  
    MonthCalendar1.RemoveBoldedDate(myVacation1)  
    MonthCalendar1.RemoveBoldedDate(myVacation2)  
    ```  
  
    ```csharp  
    monthCalendar1.RemoveBoldedDate(myVacation1);  
    monthCalendar1.RemoveBoldedDate(myVacation2);  
    ```  
  
    ```cpp  
    monthCalendar1->RemoveBoldedDate(myVacation1);  
    monthCalendar1->RemoveBoldedDate(myVacation2);  
    ```  
  
     – 또는 –  
  
     호출 하 여 세 개의 목록 중 하나에서 굵게 표시 되는 모든 날짜를 제거 합니다 <xref:System.Windows.Forms.MonthCalendar.RemoveAllBoldedDates%2A>, <xref:System.Windows.Forms.MonthCalendar.RemoveAllAnnuallyBoldedDates%2A>, 또는 <xref:System.Windows.Forms.MonthCalendar.RemoveAllMonthlyBoldedDates%2A> 메서드.  
  
    ```vb  
    MonthCalendar1.RemoveAllBoldedDates()  
    ```  
  
    ```csharp  
    monthCalendar1.RemoveAllBoldedDates();  
    ```  
  
    ```cpp  
    monthCalendar1->RemoveAllBoldedDates();  
    ```  
  
2. 호출 하 여 글꼴의 모양을 업데이트는 <xref:System.Windows.Forms.MonthCalendar.UpdateBoldedDates%2A> 메서드.  
  
    ```vb  
    MonthCalendar1.UpdateBoldedDates()  
    ```  
  
    ```csharp  
    monthCalendar1.UpdateBoldedDates();  
    ```  
  
    ```cpp  
    monthCalendar1->UpdateBoldedDates();  
    ```  
  
## <a name="see-also"></a>참고자료

- [MonthCalendar 컨트롤](monthcalendar-control-windows-forms.md)
- [방법: Windows Forms MonthCalendar 컨트롤에서 날짜 범위 선택](how-to-select-a-range-of-dates-in-the-windows-forms-monthcalendar-control.md)
- [방법: Windows Forms MonthCalendar 컨트롤의 모양 변경](how-to-change-monthcalendar-control-appearance.md)
- [방법: Windows Forms MonthCalendar 컨트롤에서 여러 달 표시](display-more-than-one-month-wf-monthcalendar-control.md)
