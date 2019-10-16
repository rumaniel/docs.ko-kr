---
title: '연습: 바인딩되지 않은 Windows Forms DataGridView 컨트롤 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data [Windows Forms], displaying without binding to data source
- DataGridView control [Windows Forms], unbound data
- DataGridView control [Windows Forms], displaying data without binding to a data source
- data [Windows Forms], unbound
- walkthroughs [Windows Forms], DataGridView control
ms.assetid: 5a8d6afa-1b4b-4b24-8db8-501086ffdebe
ms.openlocfilehash: ba821b461434cb7a5247d2962a161a1c171bbd14
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64651468"
---
# <a name="walkthrough-creating-an-unbound-windows-forms-datagridview-control"></a>연습: 바인딩되지 않은 Windows Forms DataGridView 컨트롤 만들기
데이터베이스에서 발생 하지 않는 테이블 형식 데이터를 표시 하려면 자주 좋습니다. 예를 들어 다음 문자열의 2 차원 배열의 내용을 표시 하는 것이 좋습니다. <xref:System.Windows.Forms.DataGridView> 클래스는 데이터 원본에 바인딩하지 않고 데이터를 표시 하는 쉽고 고도로 사용자 지정 가능한 방법을 제공 합니다. 이 연습을 채우는 방법을 보여는 <xref:System.Windows.Forms.DataGridView> 제어 하 고 추가 및 삭제 "바인딩되지 않은" 모드의 행을 관리 합니다. 기본적으로 사용자는 새 행을 추가할 수 있습니다. 행 추가 방지 하려면 설정 합니다 <xref:System.Windows.Forms.DataGridView.AllowUserToAddRows%2A> 속성은 `false`합니다.  
  
 이 항목의 코드를 단일 목록으로 복사하려면 [방법: 바인딩되지 않은 Windows Forms DataGridView 컨트롤 만들기](how-to-create-an-unbound-windows-forms-datagridview-control.md)합니다.  
  
## <a name="creating-the-form"></a>폼 만들기  
  
#### <a name="to-use-an-unbound-datagridview-control"></a>바인딩되지 않은 DataGridView 컨트롤을 사용 하려면  
  
1. 파생 되는 클래스를 만듭니다 <xref:System.Windows.Forms.Form> 하 고 다음 변수 선언을 포함 하 고 `Main` 메서드.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSimpleUnbound#01](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/CS/simpleunbound.cs#01)]
     [!code-vb[System.Windows.Forms.DataGridViewSimpleUnbound#01](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/VB/simpleunbound.vb#01)]  
    [!code-csharp[System.Windows.Forms.DataGridViewSimpleUnbound#02](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/CS/simpleunbound.cs#02)]
    [!code-vb[System.Windows.Forms.DataGridViewSimpleUnbound#02](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/VB/simpleunbound.vb#02)]  
  
2. 구현 된 `SetupLayout` 폼의 레이아웃을 설정 하려면 폼의 클래스 정의에 메서드.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSimpleUnbound#20](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/CS/simpleunbound.cs#20)]
     [!code-vb[System.Windows.Forms.DataGridViewSimpleUnbound#20](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/VB/simpleunbound.vb#20)]  
  
3. 만들기를 `SetupDataGridView` 메서드를 설정 하는 <xref:System.Windows.Forms.DataGridView> 열과 속성.  
  
     이 메서드는 먼저 추가 합니다 <xref:System.Windows.Forms.DataGridView> 컨트롤을 폼의 <xref:System.Windows.Forms.Control.Controls%2A> 컬렉션입니다. 그런 다음 표시할 열의 수를 사용 하 여 설정 됩니다는 <xref:System.Windows.Forms.DataGridView.ColumnCount%2A> 속성입니다. 열 머리글에 대 한 기본 스타일을 설정 하 여 설정 됩니다는 <xref:System.Windows.Forms.DataGridViewCellStyle.BackColor%2A>, <xref:System.Windows.Forms.DataGridViewCellStyle.ForeColor%2A>, 및 <xref:System.Windows.Forms.DataGridViewCellStyle.Font%2A> 의 속성을 <xref:System.Windows.Forms.DataGridViewCellStyle> 반환한는 <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle%2A> 속성입니다.  
  
     레이아웃 및 모양 속성을 설정 하 고 열 이름이 할당 됩니다. 이 메서드가 종료 되는 경우는 <xref:System.Windows.Forms.DataGridView> 컨트롤은을 채울 수 있습니다.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSimpleUnbound#30](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/CS/simpleunbound.cs#30)]
     [!code-vb[System.Windows.Forms.DataGridViewSimpleUnbound#30](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/VB/simpleunbound.vb#30)]  
  
4. 만들기는 `PopulateDataGridView` 에 행을 추가 하는 방법의 <xref:System.Windows.Forms.DataGridView> 제어 합니다.  
  
     각 행 노래 및 관련된 정보를 나타냅니다.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSimpleUnbound#40](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/CS/simpleunbound.cs#40)]
     [!code-vb[System.Windows.Forms.DataGridViewSimpleUnbound#40](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/VB/simpleunbound.vb#40)]  
  
5. 현재 위치에서 유틸리티 메서드를 사용 하 여 이벤트 처리기를 연결할 수 있습니다.  
  
     처리 하는 합니다 **추가** 및 **삭제** 단추의 <xref:System.Windows.Forms.Control.Click> 이벤트, 양식의 <xref:System.Windows.Forms.Form.Load> 이벤트 및 <xref:System.Windows.Forms.DataGridView> 컨트롤의 <xref:System.Windows.Forms.DataGridView.CellFormatting> 이벤트입니다.  
  
     경우는 **추가** 단추의 <xref:System.Windows.Forms.Control.Click> 이벤트가 발생 하면 새로 만든 빈 행에 추가 됩니다는 <xref:System.Windows.Forms.DataGridView>합니다.  
  
     경우는 **삭제** 단추의 <xref:System.Windows.Forms.Control.Click> 선택한 행을 삭제 하면, 사용자는 새 레코드에 대 한 행은 새 행을 추가 하지 않은 이벤트가 발생 합니다. 이 행의 마지막 행은 항상를 <xref:System.Windows.Forms.DataGridView> 제어 합니다.  
  
     경우 양식의 <xref:System.Windows.Forms.Form.Load> 이벤트가 발생 합니다 `SetupLayout`, `SetupDataGridView`, 및 `PopulateDataGridView` 유틸리티 메서드를 호출 합니다.  
  
     경우는 <xref:System.Windows.Forms.DataGridView.CellFormatting> 이벤트가 발생의 각 셀을 `Date` 열 형식은 long date 셀의 값을 구문 분석할 수 없는 경우가 아니면 합니다.  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSimpleUnbound#10](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/CS/simpleunbound.cs#10)]
     [!code-vb[System.Windows.Forms.DataGridViewSimpleUnbound#10](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSimpleUnbound/VB/simpleunbound.vb#10)]  
  
## <a name="testing-the-application"></a>애플리케이션 테스트  
 이제 예상 대로 작동 되도록 폼을 테스트할 수 있습니다.  
  
#### <a name="to-test-the-form"></a>폼을 테스트 하려면  
  
- F5 키를 눌러 애플리케이션을 실행합니다.  
  
     표시 됩니다는 <xref:System.Windows.Forms.DataGridView> 에 나열 된 노래를 표시 하는 컨트롤 `PopulateDataGridView`합니다. 포함 된 새 행을 추가할 수 있습니다 합니다 **행 추가** 단추를 사용 하 여 선택한 행을 삭제할 수는 **행 삭제** 단추입니다. 바인딩되지 않은 <xref:System.Windows.Forms.DataGridView> 컨트롤은 데이터 저장소 및 데이터에 같은 외부 소스에 관계 없이 <xref:System.Data.DataSet> 또는 배열입니다.  
  
## <a name="next-steps"></a>다음 단계  
 이 응용 프로그램의 기본적인 이해를 제공 합니다 <xref:System.Windows.Forms.DataGridView> 컨트롤의 기능입니다. 동작과 모양을 사용자 지정할 수 있습니다는 <xref:System.Windows.Forms.DataGridView> 여러 가지 방법으로 제어 합니다.  
  
- 헤더 및 테두리 스타일을 변경 합니다. 자세한 내용은 [방법: 변경 된 테두리 및 모눈선 스타일에는 Windows Forms DataGridView 컨트롤](change-the-border-and-gridline-styles-in-the-datagrid.md)합니다.  
  
- 사용 하도록 설정 하거나 사용자 입력을 제한 합니다 <xref:System.Windows.Forms.DataGridView> 제어 합니다. 자세한 내용은 [방법: 행 추가 방지 하 고 삭제는 Windows Forms DataGridView 컨트롤](prevent-row-addition-and-deletion-datagridview.md), 및 [방법: 에서 열을 설정 읽기 전용으로 Windows Forms DataGridView 컨트롤](how-to-make-columns-read-only-in-the-windows-forms-datagridview-control.md)합니다.  
  
- 데이터베이스 관련 오류에 대 한 사용자 입력을 확인 합니다. 자세한 내용은 [연습: Forms DataGridView 컨트롤의 Windows에서 데이터 입력 중에 발생 하는 오류 처리](handling-errors-that-occur-during-data-entry-in-the-datagrid.md)합니다.  
  
- 가상 모드를 사용 하 여 매우 큰 데이터 집합을 처리 합니다. 자세한 내용은 [연습: Forms DataGridView 컨트롤의 Windows에서 가상 모드 구현](implementing-virtual-mode-wf-datagridview-control.md)합니다.  
  
- 셀의 모양을 사용자 지정 합니다. 자세한 내용은 [방법: Windows Forms DataGridView 컨트롤에서 셀 모양 사용자 지정](customize-the-appearance-of-cells-in-the-datagrid.md) 고 [방법: Windows Forms DataGridView 컨트롤에 기본 셀 스타일 설정](how-to-set-default-cell-styles-for-the-windows-forms-datagridview-control.md)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- [Windows Forms DataGridView 컨트롤에서 데이터 표시](displaying-data-in-the-windows-forms-datagridview-control.md)
- [방법: 바인딩되지 않은 Windows Forms DataGridView 컨트롤 만들기](how-to-create-an-unbound-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤의 데이터 디스플레이 모드](data-display-modes-in-the-windows-forms-datagridview-control.md)
