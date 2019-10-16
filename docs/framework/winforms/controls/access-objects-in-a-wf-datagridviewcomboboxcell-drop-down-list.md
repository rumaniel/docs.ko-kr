---
title: '방법: Windows Forms DataGridViewComboBoxCell 드롭다운 목록에서 개체 액세스'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataGridView control [Windows Forms], accessing objects in combo box cells
- combo boxes [Windows Forms], in DataGridView control
- combo boxes [Windows Forms], accessing objects in DataGridViewComboBoxCell drop-down lists
ms.assetid: bcbe794a-d1fa-47f8-b5a3-5f085b32097d
ms.openlocfilehash: 8df9ef1c30704c8b0d0dc7bbec48e53252cf9ae6
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64665877"
---
# <a name="how-to-access-objects-in-a-windows-forms-datagridviewcomboboxcell-drop-down-list"></a>방법: Windows Forms DataGridViewComboBoxCell 드롭다운 목록에서 개체 액세스
같은 합니다 <xref:System.Windows.Forms.ComboBox> 컨트롤을 <xref:System.Windows.Forms.DataGridViewComboBoxColumn> 및 <xref:System.Windows.Forms.DataGridViewComboBoxCell> 형식을 사용 하면 임의의 개체 드롭다운 목록에 추가할 수입니다. 이 기능을 사용 하 여 별도 컬렉션에서 해당 개체를 저장 하지 않고 드롭다운 목록에서 복잡 한 상태를 나타낼 수 있습니다.  
  
 달리를 <xref:System.Windows.Forms.ComboBox> 컨트롤을 <xref:System.Windows.Forms.DataGridView> 형식은 하지는 <xref:System.Windows.Forms.ComboBox.SelectedItem%2A> 현재 선택한 개체를 검색 하는 속성. 대신 설정 해야 합니다 <xref:System.Windows.Forms.DataGridViewComboBoxColumn.ValueMember%2A?displayProperty=nameWithType> 또는 <xref:System.Windows.Forms.DataGridViewComboBoxCell.ValueMember%2A?displayProperty=nameWithType> 속성을 비즈니스 개체의 속성 이름입니다. 셀 비즈니스 개체의 표시 속성을 설정 하는 사용자를 선택 하면 <xref:System.Windows.Forms.DataGridViewCell.Value%2A> 속성입니다.  
  
 셀 값을 통해 비즈니스 개체를 검색 하 여 `ValueMember` 속성 자체 비즈니스 개체에 대 한 참조를 반환 하는 속성을 지정 해야 합니다. 따라서 비즈니스 개체의 형식에 대 한 제어 없는 경우 이러한 속성 상속을 통해 형식을 확장 하 여 추가 해야 합니다.  
  
 다음 절차에는 비즈니스 개체를 사용 하 여 드롭다운 목록을 채울 셀을 통해 개체를 검색 하는 방법을 보여 줍니다 <xref:System.Windows.Forms.DataGridViewCell.Value%2A> 속성입니다.  
  
### <a name="to-add-business-objects-to-the-drop-down-list"></a>드롭다운 목록에 비즈니스 개체를 추가 하려면  
  
1. 새 <xref:System.Windows.Forms.DataGridViewComboBoxColumn> 우 해당 <xref:System.Windows.Forms.DataGridViewComboBoxColumn.Items%2A> 컬렉션입니다. 열을 설정할 수 또는 <xref:System.Windows.Forms.DataGridViewComboBoxColumn.DataSource%2A> 비즈니스 개체의 컬렉션에는 속성입니다. 그러나이 경우 추가할 수 없습니다 "할당 되지 않은" 드롭 다운 목록 컬렉션에서 해당 비즈니스 개체를 만들지 않고 합니다.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewComboBoxObjectBinding#110](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/CS/form1.cs#110)]
     [!code-vb[System.Windows.Forms.DataGridViewComboBoxObjectBinding#110](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/vb/form1.vb#110)]  
  
2. <xref:System.Windows.Forms.DataGridViewComboBoxColumn.DisplayMember%2A> 및 <xref:System.Windows.Forms.DataGridViewComboBoxColumn.ValueMember%2A> 속성을 설정합니다. <xref:System.Windows.Forms.DataGridViewComboBoxColumn.DisplayMember%2A> 드롭다운 목록에서 표시할 비즈니스 개체의 속성을 나타냅니다. <xref:System.Windows.Forms.DataGridViewComboBoxColumn.ValueMember%2A> 비즈니스 개체에 대 한 참조를 반환 하는 속성을 나타냅니다.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewComboBoxObjectBinding#115](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/CS/form1.cs#115)]
     [!code-vb[System.Windows.Forms.DataGridViewComboBoxObjectBinding#115](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/vb/form1.vb#115)]  
  
3. 비즈니스 개체 형식 현재 인스턴스에 대 한 참조를 반환 하는 속성이 포함 되어 있는지 확인 합니다. 이 속성에 할당 된 값을 사용 하 여 이름은 <xref:System.Windows.Forms.DataGridViewComboBoxColumn.ValueMember%2A> 이전 단계에서 합니다.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewComboBoxObjectBinding#310](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/CS/form1.cs#310)]
     [!code-vb[System.Windows.Forms.DataGridViewComboBoxObjectBinding#310](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/vb/form1.vb#310)]  
  
### <a name="to-retrieve-the-currently-selected-business-object"></a>현재 선택 된 비즈니스 개체를 검색 하려면  
  
- 셀을 가져옵니다 <xref:System.Windows.Forms.DataGridViewCell.Value%2A> 속성 및 비즈니스 개체 형식으로 캐스팅 합니다.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewComboBoxObjectBinding#120](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/CS/form1.cs#120)]
     [!code-vb[System.Windows.Forms.DataGridViewComboBoxObjectBinding#120](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/vb/form1.vb#120)]  
  
## <a name="example"></a>예제  
 전체 예제는 드롭다운 목록에서 비즈니스 개체의 사용을 보여 줍니다. 예에서를 <xref:System.Windows.Forms.DataGridView> 컨트롤의 컬렉션에 바인딩된 `Task` 개체입니다. 각 `Task` 개체에는 `AssignedTo` 나타내는 속성을 `Employee` 현재 해당 작업에 할당 하는 개체입니다. 합니다 `Assigned To` 열에 표시 됩니다는 `Name` 직원 또는 "할당 되지 않은" 경우 각각에 대 한 속성 값 할당 합니다 `Task.AssignedTo` 속성 값이 `null`합니다.  
  
 이 예제에서는의 동작을 보려면 다음 단계를 수행 합니다.  
  
1. 할당을 변경 합니다 `Assigned To` 드롭 다운 목록에서 다른 값을 선택 하거나 CTRL + 0 콤보 상자 셀의 열입니다.  
  
2. 클릭 `Generate Report` 에 현재 할당을 표시 합니다. 함을이 변경 된 `Assigned To` 열을 자동으로 업데이트는 `tasks` 컬렉션입니다.  
  
3. 클릭을 `Request Status` 를 호출 하려면 단추를 `RequestStatus` 현재 메서드의 `Employee` 해당 행에 대 한 개체입니다. 이 선택된 된 개체 성공적으로 검색 된 방법을 보여 줍니다.  
  
 [!code-csharp[System.Windows.Forms.DataGridViewComboBoxObjectBinding#000](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/CS/form1.cs#000)]
 [!code-vb[System.Windows.Forms.DataGridViewComboBoxObjectBinding#000](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/vb/form1.vb#000)]  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- System 및 System.Windows.Forms 어셈블리에 대한 참조  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridViewComboBoxColumn>
- <xref:System.Windows.Forms.DataGridViewComboBoxColumn.Items%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewComboBoxColumn.DataSource%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewComboBoxColumn.ValueMember%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewComboBoxCell>
- <xref:System.Windows.Forms.DataGridViewComboBoxCell.Items%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewComboBoxCell.DataSource%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewComboBoxCell.ValueMember%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewCell.Value%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.ComboBox>
- [Windows Forms DataGridView 컨트롤에서 데이터 표시](displaying-data-in-the-windows-forms-datagridview-control.md)
