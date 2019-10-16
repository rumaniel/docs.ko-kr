---
title: '방법: Windows Forms MonthCalendar 컨트롤에서 여러 달 표시'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- calendars [Windows Forms], formatting display
- examples [Windows Forms], calendar controls
- calendars [Windows Forms], multiple months
- MonthCalendar control [Windows Forms], formatting display
ms.assetid: d197caa2-38a5-4cb4-acc3-562130c2ace3
ms.openlocfilehash: c2252ccf1c8fec0dcaba634e6da093ab976ce1f6
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64614758"
---
# <a name="how-to-display-more-than-one-month-in-the-windows-forms-monthcalendar-control"></a>방법: Windows Forms MonthCalendar 컨트롤에서 여러 달 표시
Windows Forms <xref:System.Windows.Forms.MonthCalendar> 컨트롤 한 번에 최대 12 개월을 표시할 수 있습니다. 기본적으로 컨트롤은 한 달만 표시 되지만 몇 달이 표시 되 고 컨트롤 내에서 정렬 되는 방식을 지정할 수 있습니다. 컨트롤의 크기 조정 달력의 크기를 변경한 경우, 하므로 새 차원에 대 한 폼에 공간이 충분 해야 합니다.  
  
### <a name="to-display-multiple-months"></a>여러 달 표시  
  
- 설정 된 <xref:System.Windows.Forms.MonthCalendar.CalendarDimensions%2A> 속성 가로 및 세로로 표시할 월의 수입니다.  
  
    ```vb  
    MonthCalendar1.CalendarDimensions = New System.Drawing.Size (3,2)  
    ```  
  
    ```csharp  
    monthCalendar1.CalendarDimensions = new System.Drawing.Size (3,2);  
    ```  
  
    ```cpp  
    monthCalendar1->CalendarDimensions = System::Drawing::Size (3,2);  
    ```  
  
## <a name="see-also"></a>참고자료

- [MonthCalendar 컨트롤](monthcalendar-control-windows-forms.md)
- [방법: Windows Forms MonthCalendar 컨트롤에서 날짜 범위 선택](how-to-select-a-range-of-dates-in-the-windows-forms-monthcalendar-control.md)
- [방법: Windows Forms MonthCalendar 컨트롤의 모양 변경](how-to-change-monthcalendar-control-appearance.md)
