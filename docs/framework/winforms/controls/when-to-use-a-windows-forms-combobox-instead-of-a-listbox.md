---
title: ListBox 대신 Windows Forms ComboBox를 사용해야 하는 경우
ms.date: 03/30/2017
helpviewer_keywords:
- ListBox control [Windows Forms], adding and removing items
- ListBox control [Windows Forms], vs. ComboBox
- bound controls [Windows Forms], combo boxes
- Windows Forms controls, data binding
- ComboBox control [Windows Forms], compared to ListBox
- combo boxes [Windows Forms], compared to list boxes
- ListBox control [Windows Forms], accessing items
- ListCount property
ms.assetid: 7bcaea58-1cfa-46db-9baf-b75a69d8f9ec
ms.openlocfilehash: 8a2429049acf1a22edde8d132ece17da4e91f1db
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61759832"
---
# <a name="when-to-use-a-windows-forms-combobox-instead-of-a-listbox"></a>ListBox 대신 Windows Forms ComboBox를 사용해야 하는 경우
<xref:System.Windows.Forms.ComboBox> 하며 <xref:System.Windows.Forms.ListBox> 컨트롤 유사 하 게 동작에 있으며 일부 경우 않을 서로 바꿔 사용할 수 있습니다. 그러나 하나 또는 다른 작업에 더 적절 한 경우 경우가 있습니다.  
  
 일반적으로 제안 된 선택 목록이 하 고 목록 상자는 목록에 새로운 기능에 대 한 입력을 제한 하려는 경우 적절 한 경우 콤보 상자 적합 합니다. 콤보 상자의 목록에 없는 항목에 입력할 수 있도록 텍스트 상자 필드를 포함 합니다. 경우는 예외를 <xref:System.Windows.Forms.ComboBox.DropDownStyle%2A> 속성이 <xref:System.Windows.Forms.ComboBoxStyle.DropDownList>합니다. 이 경우 컨트롤의 첫 번째 문자를 입력 하는 경우 항목을 선택 됩니다.  
  
 또한 콤보 상자 폼에서 공간을 절약 합니다. 아래쪽 화살표를 클릭할 때까지 전체 목록은 표시 되지 않으므로, 콤보 상자 목록 상자에 적합 하지는 작은 공간에 쉽게 맞출 수 있습니다. 경우는 예외입니다 합니다 <xref:System.Windows.Forms.ComboBox.DropDownStyle%2A> 속성이 <xref:System.Windows.Forms.ComboBoxStyle.Simple>: 전체 목록이 표시 되 고 콤보 상자의 목록 상자 보다 더 많은 공간을 차지 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.ComboBox>
- <xref:System.Windows.Forms.ListBox>
- [방법: 추가 및 제거할 항목을 Windows Forms ComboBox, ListBox 또는 CheckedListBox 컨트롤](add-and-remove-items-from-a-wf-combobox.md)
- [방법: Windows의 내용을 정렬할 Forms ComboBox, ListBox 또는 CheckedListBox 컨트롤](sort-the-contents-of-a-wf-combobox-listbox-or-checkedlistbox-control.md)
- [옵션 목록 표시에 사용된 Windows Forms 컨트롤](windows-forms-controls-used-to-list-options.md)
