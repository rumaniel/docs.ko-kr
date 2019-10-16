---
title: '방법: Windows Forms에서 단일 이벤트 처리기에 여러 이벤트 연결'
ms.date: 03/30/2017
dev_langs:
- vb
helpviewer_keywords:
- events [Windows Forms], connecting multiple to single event handler
- event handlers [Windows Forms], connecting events to
- menus [Windows Forms], event-handling methods for multiple menu items
- Windows Forms controls, events
- menu items [Windows Forms], multicasting event-handling methods
ms.assetid: 5a20749a-41b5-4acc-8eb1-9e5040b0a2c4
ms.openlocfilehash: eec6a754b885cd169e5542221caefb3233c4c8af
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61967024"
---
# <a name="how-to-connect-multiple-events-to-a-single-event-handler-in-windows-forms"></a>방법: Windows Forms에서 단일 이벤트 처리기에 여러 이벤트 연결
응용 프로그램 디자인에서 있습니다 경우가 동일한 절차를 수행 하는 여러 이벤트 또는 단일 이벤트 처리기를 사용 하 여 여러 이벤트에 대 한 합니다. 예를 들어, 동일한 기능을 노출 하는 경우 폼에서 단추와 마찬가지로 동일한 이벤트를 발생 시킬 수 있는 메뉴 명령이에 강력한 시간 보호기가 경우가 많습니다. 속성 창의 이벤트 보기를 사용 하 여이 수행할 수 있습니다 C# 를 사용 하 여 또는 합니다 `Handles` 키워드 및 **클래스 이름** 및 **메서드 이름** 드롭다운 목록 상자는 Visual Basic 코드 편집기에서.  
  
### <a name="to-connect-multiple-events-to-a-single-event-handler-in-visual-basic"></a>Visual Basic에서 단일 이벤트 처리기에 여러 이벤트 연결  
  
1. 폼을 마우스 오른쪽 단추로 클릭 하 고 선택 **코드 보기**합니다.  
  
2. **클래스 이름** 드롭다운 목록 상자에서 처리할 이벤트 처리기로 원하는 컨트롤 중 하나를 선택 합니다.  
  
3. **메서드 이름** 드롭다운 목록 상자에서 이벤트를 처리할 이벤트 처리기를 중 하나를 선택 합니다.  
  
4. 코드 편집기는 적절 한 이벤트 처리기를 삽입 하 고 메서드 내에서 커서를 놓습니다. 에서는 아래 예제는 <xref:System.Windows.Forms.Control.Click> 에 대 한 이벤트를 <xref:System.Windows.Forms.Button> 컨트롤입니다.  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click  
    ' Add event-handler code here.  
    End Sub  
    ```  
  
5. 다른 이벤트를 처리를 추가 합니다 `Handles` 절.  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click, Button2.Click  
    ' Add event-handler code here.  
    End Sub  
    ```  
  
6. 이벤트 처리기에 적절 한 코드를 추가 합니다.  
  
### <a name="to-connect-multiple-events-to-a-single-event-handler-in-c"></a>C에서 단일 이벤트 처리기에 여러 이벤트 연결\#
  
1. 이벤트 처리기를 연결 하려는 컨트롤을 선택 합니다.  
  
2. 속성 창에서 클릭 합니다 **이벤트** 단추 (![이벤트 단추](./media/vxeventsbutton-propertieswindow.png "vxEventsButton_PropertiesWindow")).  
  
3. 처리 하려는 이벤트의 이름을 클릭 합니다.  
  
4. 이벤트 이름 옆에 있는 값 섹션에서 처리 하려는 이벤트의 메서드 시그니처와 일치 하는 기존 이벤트 처리기의 목록을 표시 하려면 드롭다운 단추를 클릭 합니다.  
  
5. 목록에서 적절 한 이벤트 처리기를 선택 합니다.  
  
     코드는 이벤트에서 기존 이벤트 처리기를 바인딩할 폼에 추가 됩니다.  
  
## <a name="see-also"></a>참고자료

- [Windows Forms에서 이벤트 처리기 만들기](creating-event-handlers-in-windows-forms.md)
- [이벤트 처리기 개요](event-handlers-overview-windows-forms.md)
