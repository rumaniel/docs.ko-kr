---
title: '방법: Windows Forms DateTimePicker 컨트롤을 사용하여 날짜를 사용자 지정 형식으로 표시'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- DateTimePicker control [Windows Forms], display styles
- examples [Windows Forms], DateTimePicker control
- dates [Windows Forms], displaying in DateTimePicker control
ms.assetid: 39767691-2d2b-46b6-a663-b7901e581a6e
ms.openlocfilehash: 08d5a505229cd434dbf82e8ae4624bb418efd379
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61972169"
---
# <a name="how-to-display-a-date-in-a-custom-format-with-the-windows-forms-datetimepicker-control"></a>방법: Windows Forms DateTimePicker 컨트롤을 사용하여 날짜를 사용자 지정 형식으로 표시
Windows Forms <xref:System.Windows.Forms.DateTimePicker> 컨트롤의 컨트롤에서 날짜와 시간 표시를 서식 지정에 유연성을 제공 합니다. 합니다 <xref:System.Windows.Forms.DateTimePicker.Format%2A> 속성에 나열 된 미리 정의 된 형식에서 선택할 수는 <xref:System.Windows.Forms.DateTimePickerFormat>합니다. 이러한 용도 맞게 적절 한 인 경우에 나열 된 형식 문자를 사용 하 여 사용자 고유의 형식 스타일을 만들 수 있습니다 <xref:System.Windows.Forms.DateTimePicker.CustomFormat%2A>합니다.  
  
### <a name="to-display-a-custom-format"></a>사용자 지정 형식을 표시 하려면  
  
1. <xref:System.Windows.Forms.DateTimePicker.Format%2A> 속성을 `DateTimePickerFormat.Custom`으로 설정합니다.  
  
2. 설정 된 <xref:System.Windows.Forms.DateTimePicker.CustomFormat%2A> 는 형식 문자열 속성입니다.  
  
    ```vb  
    DateTimePicker1.Format = DateTimePickerFormat.Custom  
    ' Display the date as "Mon 27 Feb 2012".  
    DateTimePicker1.CustomFormat = "ddd dd MMM yyyy"  
    ```  
  
    ```csharp  
    dateTimePicker1.Format = DateTimePickerFormat.Custom;  
    // Display the date as "Mon 27 Feb 2012".  
    dateTimePicker1.CustomFormat = "ddd dd MMM yyyy";  
    ```  
  
    ```cpp  
    dateTimePicker1->Format = DateTimePickerFormat::Custom;  
    // Display the date as "Mon 27 Feb 2012".  
    dateTimePicker1->CustomFormat = "ddd dd MMM yyyy";  
    ```  
  
### <a name="to-add-text-to-the-formatted-value"></a>서식이 지정 된 값으로 텍스트를 추가 하려면  
  
1. 작은따옴표를 사용 하 여 "M"와 같은 문자 형식 또는 같은 구분 되지 않는 모든 문자를 묶습니다 ":". 아래의 형식 문자열은 형식으로 현재 날짜를 표시 하는 예를 들어, "임: 05시 30분: 31 년 3 월 금요일 02, 2012"영어 (미국) 문화권의 합니다.  
  
    ```vb  
    DateTimePicker1.CustomFormat = "'Today is:' hh:mm:ss dddd MMMM dd, yyyy"  
    ```  
  
    ```csharp  
    dateTimePicker1.CustomFormat = "'Today is:' hh:mm:ss dddd MMMM dd, yyyy";  
    ```  
  
    ```cpp  
    dateTimePicker1->CustomFormat =  
       "'Today is:' hh:mm:ss dddd MMMM dd, yyyy";  
    ```  
  
     문화권 설정에 따라 단일 따옴표로 묶이지 않은 문자를 변경할 수 있습니다. 위의 형식 문자열은 형식으로 현재 날짜를 표시 하는 예를 들어, "임: 05시 30분: 31 년 3 월 금요일 02, 2012"영어 (미국) 문화권의 합니다. 참고 "ss" 이므로 구분 문자가 되도록 것이 아니므로 첫 번째 콜론을 하나의 따옴표로 묶입니다. 다른 문화권의 형식으로 나타날 수 있습니다 "임: 05.30.31 금요일 년 3 월 02 2012"입니다.  
  
## <a name="see-also"></a>참고자료

- [DateTimePicker 컨트롤](datetimepicker-control-windows-forms.md)
- [방법: Windows Forms DateTimePicker 컨트롤을 포함 하는 설정 및 반환 날짜](how-to-set-and-return-dates-with-the-windows-forms-datetimepicker-control.md)
