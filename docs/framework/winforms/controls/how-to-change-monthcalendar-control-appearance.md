---
title: '방법: Windows Forms MonthCalendar 컨트롤의 모양 변경'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- examples [Windows Forms], calendar controls
- MonthCalendar control [Windows Forms], formatting display
ms.assetid: d09b95c9-e108-4608-9b31-b9100c0677bf
ms.openlocfilehash: 5582624d881b2d8039bcd5e8ac45e548c7b38f57
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69929044"
---
# <a name="how-to-change-the-windows-forms-monthcalendar-controls-appearance"></a>방법: Windows Forms MonthCalendar 컨트롤의 모양 변경
Windows Forms <xref:System.Windows.Forms.MonthCalendar> 컨트롤을 사용 하면 여러 가지 방법으로 달력의 모양을 사용자 지정할 수 있습니다. 예를 들어 색 구성표를 설정 하 고 주 번호와 현재 날짜를 표시 하거나 숨기도록 선택할 수 있습니다.  
  
### <a name="to-change-the-month-calendars-color-scheme"></a>월 달력의 색 구성표를 변경 하려면  
  
- <xref:System.Windows.Forms.MonthCalendar.TitleBackColor%2A>, <xref:System.Windows.Forms.MonthCalendar.TitleForeColor%2A> 및 와<xref:System.Windows.Forms.MonthCalendar.TrailingForeColor%2A>같은 속성을 설정 합니다. 속성 <xref:System.Windows.Forms.MonthCalendar.TitleBackColor%2A> 은 요일에 대 한 글꼴 색도 결정 합니다. 속성 <xref:System.Windows.Forms.MonthCalendar.TrailingForeColor%2A> 은 표시 된 월 또는 월 앞과 뒤의 날짜 색을 결정 합니다.  
  
    ```vb  
    MonthCalendar1.TitleBackColor = System.Drawing.Color.Blue  
    MonthCalendar1.TrailingForeColor = System.Drawing.Color.Red  
    MonthCalendar1.TitleForeColor = System.Drawing.Color.Yellow  
    ```  
  
    ```csharp  
    monthCalendar1.TitleBackColor = System.Drawing.Color.Blue;  
    monthCalendar1.TrailingForeColor = System.Drawing.Color.Red;  
    monthCalendar1.TitleForeColor = System.Drawing.Color.Yellow;  
    ```  
  
    ```cpp  
    monthCalendar1->TitleBackColor = System::Drawing::Color::Blue;  
    monthCalendar1->TrailingForeColor = System::Drawing::Color::Red;  
    monthCalendar1->TitleForeColor = System::Drawing::Color::Yellow;  
    ```  
  
    > [!NOTE]
    > Windows Vista부터 테마에 따라 일부 속성을 설정 하면 일정의 모양이 변경 되지 않을 수 있습니다. 예를 들어 Windows가 Aero 테마를 사용 하도록 설정 <xref:System.Windows.Forms.MonthCalendar.BackColor%2A>된 경우 <xref:System.Windows.Forms.MonthCalendar.TitleForeColor%2A>, <xref:System.Windows.Forms.MonthCalendar.TitleBackColor%2A>, 또는 <xref:System.Windows.Forms.MonthCalendar.TrailingForeColor%2A> 속성을 설정 해도 아무런 효과가 없습니다. 즉, 런타임에 현재 운영 체제 테마에서 파생 되는 모양을 사용 하 여 달력의 업데이트 된 렌더링 됩니다. 이러한 속성을 사용 하 고 이전 버전의 달력을 사용 하려면 응용 프로그램에 대 한 비주얼 스타일을 사용 하지 않도록 설정할 수 있습니다. 비주얼 스타일을 사용 하지 않도록 설정 하면 애플리케이션에서 다른 컨트롤의 동작과 모양을 달라질 수 있습니다. Visual Basic에서 비주얼 스타일을 사용 하지 않으려면 프로젝트 디자이너를 열고 선택 취소 합니다 **XP 비주얼 스타일 사용** 확인란 합니다. C#에서 비주얼 스타일을 사용 하지 않으려면 Program.cs를 열고 주석 `Application.EnableVisualStyles();`합니다. 비주얼 스타일에 대 한 자세한 내용은 [비주얼 스타일 사용](/windows/desktop/controls/cookbook-overview)을 참조 하세요.  
  
### <a name="to-display-the-current-date-at-the-bottom-of-the-control"></a>컨트롤의 맨 아래에 있는 현재 날짜를 표시 하려면  
  
- <xref:System.Windows.Forms.MonthCalendar.ShowToday%2A> 속성을 `true`으로 설정합니다. 아래 예제에서는 폼을 두 번 클릭 했을 때 오늘 날짜를 표시 하거나 생략할 때를 전환 합니다.  
  
    ```vb  
    Private Sub Form1_DoubleClick(ByVal sender As Object, _  
    ByVal e As System.EventArgs) Handles MyBase.DoubleClick  
       ' Toggle between True and False.  
       MonthCalendar1.ShowToday = Not MonthCalendar1.ShowToday  
    End Sub  
    ```  
  
    ```csharp  
    private void Form1_DoubleClick(object sender, System.EventArgs e)  
    {  
       // Toggle between True and False.  
       monthCalendar1.ShowToday = !monthCalendar1.ShowToday;  
    }  
    ```  
  
    ```cpp  
    private:  
       System::Void Form1_DoubleClick(System::Object ^  sender,  
          System::EventArgs ^  e)  
       {  
          // Toggle between True and False.  
          monthCalendar1->ShowToday = !monthCalendar1->ShowToday;  
       }  
    ```  
  
     (시각적 C#개체, C++시각적 개체) 폼의 생성자에 다음 코드를 추가 하 여 이벤트 처리기를 등록 합니다.  
  
    ```csharp  
    this.DoubleClick += new System.EventHandler(this.Form1_DoubleClick);  
    ```  
  
    ```cpp  
    this->DoubleClick += gcnew System::EventHandler(this,  
       &Form1::Form1_DoubleClick);  
    ```  
  
### <a name="to-display-week-numbers"></a>주 번호를 표시 하려면  
  
- <xref:System.Windows.Forms.MonthCalendar.ShowWeekNumbers%2A> 속성을 `true`으로 설정합니다. 코드 또는 속성 창에서이 속성을 설정할 수 있습니다.  
  
     주 번호는 첫 번째 요일의 왼쪽에 있는 별도의 열에 표시 됩니다.  
  
    ```vb  
    MonthCalendar1.ShowWeekNumbers = True  
    ```  
  
    ```csharp  
    monthCalendar1.ShowWeekNumbers = true;  
    ```  
  
    ```cpp  
    monthCalendar1->ShowWeekNumbers = true;  
    ```  
  
## <a name="see-also"></a>참고자료

- [MonthCalendar 컨트롤](monthcalendar-control-windows-forms.md)
- [방법: Windows Forms MonthCalendar 컨트롤에서 날짜 범위 선택](how-to-select-a-range-of-dates-in-the-windows-forms-monthcalendar-control.md)
- [방법: Windows Forms MonthCalendar 컨트롤을 사용 하 여 특정 날짜를 굵게 표시](display-specific-days-in-bold-with-wf-monthcalendar-control.md)
- [방법: Windows Forms MonthCalendar 컨트롤에서 한 달 이상 표시](display-more-than-one-month-wf-monthcalendar-control.md)
