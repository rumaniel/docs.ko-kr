---
title: ComboBox 컨트롤 개요(Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- ComboBox
helpviewer_keywords:
- drop-down lists [Windows Forms], Windows Forms
- ComboBox control [Windows Forms], about ComboBox control
- drop-down lists [Windows Forms], ComboBox control
- combo boxes [Windows Forms], about combo boxes
ms.assetid: a58b393f-a614-45d1-8961-857a024b5acd
ms.openlocfilehash: 80056771744c9b97828a024adf32638e545a839e
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61956171"
---
# <a name="combobox-control-overview-windows-forms"></a>ComboBox 컨트롤 개요(Windows Forms)
Windows Forms <xref:System.Windows.Forms.ComboBox> 드롭다운 콤보 상자에서 데이터를 표시할 컨트롤을 사용 합니다. 기본적으로 <xref:System.Windows.Forms.ComboBox> 컨트롤이 두 부분으로 표시 됩니다:, 상위 부분은 텍스트 상자에 사용자는 목록 항목을 입력할 수 있도록 합니다. 두 번째 부분에 있는 사용자 수 하나를 선택 하는 항목의 목록을 표시 하는 목록 상자입니다. 콤보 상자의 다른 스타일의 자세한 내용은 참조 [Windows Forms ComboBox Instead of ListBox를 사용 하는 경우](when-to-use-a-windows-forms-combobox-instead-of-a-listbox.md)합니다.  
  
 <xref:System.Windows.Forms.ComboBox.SelectedIndex%2A> 속성 선택한 목록 항목에 해당 하는 정수 값을 반환 합니다. 선택한 항목을 변경 하 여 프로그래밍 방식으로 변경할 수 있습니다는 <xref:System.Windows.Forms.ComboBox.SelectedIndex%2A> 코드 값; 목록에서 해당 항목 콤보 상자의 텍스트 상자 부분에 표시 됩니다. 선택 된 항목이 있는 경우는 <xref:System.Windows.Forms.ComboBox.SelectedIndex%2A> 값이-1입니다. 목록의 첫 번째 항목을 선택 하면 해당 <xref:System.Windows.Forms.ComboBox.SelectedIndex%2A> 값은 0입니다. <xref:System.Windows.Forms.ComboBox.SelectedItem%2A> 속성은 비슷하지만 <xref:System.Windows.Forms.ComboBox.SelectedIndex%2A> , 일반적으로 문자열을 항목 자체를 반환 합니다. 합니다 <xref:System.Windows.Forms.ComboBox.ObjectCollection.Count%2A> 속성은 목록에서 항목 수와 값을 반영 합니다 <xref:System.Windows.Forms.ComboBox.ObjectCollection.Count%2A> 속성은 항상 하나 이상 가장 큰 가능한 <xref:System.Windows.Forms.ComboBox.SelectedIndex%2A> 때문에 값 <xref:System.Windows.Forms.ComboBox.SelectedIndex%2A> 는 0부터 시작 합니다.  
  
 항목을 추가 하거나 삭제할를 <xref:System.Windows.Forms.ComboBox> 컨트롤을 사용 합니다 <xref:System.Windows.Forms.ComboBox.ObjectCollection.Add%2A>, <xref:System.Windows.Forms.ComboBox.ObjectCollection.Insert%2A>, <xref:System.Windows.Forms.ComboBox.ObjectCollection.Clear%2A> 또는 <xref:System.Windows.Forms.ComboBox.ObjectCollection.Remove%2A> 메서드. 사용 하 여 목록에 항목을 추가할 수는 또는 <xref:System.Windows.Forms.ComboBox.Items%2A> 디자이너의 속성입니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ComboBox>
- [ListBox 컨트롤 개요](listbox-control-overview-windows-forms.md)
- [ListBox 대신 Windows Forms ComboBox를 사용해야 하는 경우](when-to-use-a-windows-forms-combobox-instead-of-a-listbox.md)
- [방법: 추가 및 제거할 항목을 Windows Forms ComboBox, ListBox 또는 CheckedListBox 컨트롤](add-and-remove-items-from-a-wf-combobox.md)
- [방법: Windows의 내용을 정렬할 Forms ComboBox, ListBox 또는 CheckedListBox 컨트롤](sort-the-contents-of-a-wf-combobox-listbox-or-checkedlistbox-control.md)
- [방법: 액세스 관련 항목에는 Windows Forms ComboBox, ListBox 또는 CheckedListBox 컨트롤](access-specific-items-in-a-wf-combobox-listbox-or-checkedlistbox.md)
- [방법: 데이터에 Windows Forms ComboBox 또는 ListBox 컨트롤 바인딩](how-to-bind-a-windows-forms-combobox-or-listbox-control-to-data.md)
- [옵션 목록 표시에 사용된 Windows Forms 컨트롤](windows-forms-controls-used-to-list-options.md)
- [방법: Windows Forms ComboBox, ListBox 또는 CheckedListBox 컨트롤에 대 한 조회 테이블 만들기](create-a-lookup-table-for-a-wf-combobox-listbox.md)
