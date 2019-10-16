---
title: ListBox 컨트롤 개요(Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- ListBox
helpviewer_keywords:
- list boxes [Windows Forms], about list boxes
- ListBox control [Windows Forms], about ListBox control
ms.assetid: 37ea226b-6fc8-4c70-936a-c6af4e0cad4c
ms.openlocfilehash: f70246d4a4d158815ee9662036eca8edeb891d85
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62012895"
---
# <a name="listbox-control-overview-windows-forms"></a>ListBox 컨트롤 개요(Windows Forms)
Windows Forms <xref:System.Windows.Forms.ListBox> 컨트롤 사용자 하나 이상의 항목을 선택할 수 있는 목록이 표시 됩니다. 스크롤 막대를 자동으로 추가 됩니다 총 항목 수가 표시 될 수 있는 수를 초과 하면는 <xref:System.Windows.Forms.ListBox> 제어 합니다. 경우는 <xref:System.Windows.Forms.ListBox.MultiColumn%2A> 속성이 `true`, 여러 열에 있는 항목을 표시 하는 목록 상자 및 가로 스크롤 막대를 표시 합니다. 경우는 <xref:System.Windows.Forms.ListBox.MultiColumn%2A> 속성이 `false`, 단일 열에 있는 항목을 표시 하는 목록 상자 및 세로 스크롤 막대가 표시 됩니다. 때 <xref:System.Windows.Forms.ListBox.ScrollAlwaysVisible%2A> 로 설정 된 `true`, 스크롤 막대 항목 개수에 관계 없이 표시 됩니다. <xref:System.Windows.Forms.ListBox.SelectionMode%2A> 속성 결정 한 번에 목록 항목의 개수를 선택할 수 있습니다.  
  
## <a name="ways-to-change-the-listbox-control"></a>ListBox 컨트롤을 변경 하는 방법  
 <xref:System.Windows.Forms.ListBox.SelectedIndex%2A> 속성 목록 상자에서 선택한 첫 번째 항목에 해당 하는 정수 값을 반환 합니다. 선택한 항목을 변경 하 여 프로그래밍 방식으로 변경할 수 있습니다는 <xref:System.Windows.Forms.ListBox.SelectedIndex%2A> 코드 값; 목록에서 해당 항목을 Windows Form에 강조 표시 됩니다. 선택 된 항목이 있는 경우는 <xref:System.Windows.Forms.ListBox.SelectedIndex%2A> 값이-1입니다. 목록의 첫 번째 항목을 선택 하는 경우는 <xref:System.Windows.Forms.ListBox.SelectedIndex%2A> 값은 0입니다. 여러 항목을 선택 하는 경우는 <xref:System.Windows.Forms.ListBox.SelectedIndex%2A> 값 목록에서 처음 표시 되는 선택한 항목을 반영 합니다. <xref:System.Windows.Forms.ListBox.SelectedItem%2A> 속성은 비슷하지만 <xref:System.Windows.Forms.ListBox.SelectedIndex%2A>, 일반적으로 문자열을 항목 자체를 반환 합니다. 합니다 <xref:System.Windows.Forms.ListBox.ObjectCollection.Count%2A> 속성은 목록에서 항목 수와 값을 반영 합니다 <xref:System.Windows.Forms.ListBox.ObjectCollection.Count%2A> 속성은 항상 하나 이상 가장 큰 가능한 <xref:System.Windows.Forms.ListBox.SelectedIndex%2A> 때문에 값 <xref:System.Windows.Forms.ListBox.SelectedIndex%2A> 는 0부터 시작 합니다.  
  
 항목을 추가 하거나 삭제할를 <xref:System.Windows.Forms.ListBox> 컨트롤을 사용 합니다 <xref:System.Windows.Forms.ListBox.ObjectCollection.Add%2A>, <xref:System.Windows.Forms.ListBox.ObjectCollection.Insert%2A>, <xref:System.Windows.Forms.ListBox.ObjectCollection.Clear%2A> 또는 <xref:System.Windows.Forms.ListBox.ObjectCollection.Remove%2A> 메서드. 사용 하 여 목록에 항목을 추가할 수는 또는 <xref:System.Windows.Forms.ListBox.Items%2A> 디자인 타임 속성입니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ListBox>
- [방법: 추가 및 제거할 항목을 Windows Forms ComboBox, ListBox 또는 CheckedListBox 컨트롤](add-and-remove-items-from-a-wf-combobox.md)
- [방법: Windows의 내용을 정렬할 Forms ComboBox, ListBox 또는 CheckedListBox 컨트롤](sort-the-contents-of-a-wf-combobox-listbox-or-checkedlistbox-control.md)
- [방법: 데이터에 Windows Forms ComboBox 또는 ListBox 컨트롤 바인딩](how-to-bind-a-windows-forms-combobox-or-listbox-control-to-data.md)
- [ComboBox 컨트롤 개요](combobox-control-overview-windows-forms.md)
- [CheckedListBox 컨트롤 개요](checkedlistbox-control-overview-windows-forms.md)
- [옵션 목록 표시에 사용된 Windows Forms 컨트롤](windows-forms-controls-used-to-list-options.md)
- [방법: Windows Forms ComboBox, ListBox 또는 CheckedListBox 컨트롤에 대 한 조회 테이블 만들기](create-a-lookup-table-for-a-wf-combobox-listbox.md)
