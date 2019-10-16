---
title: '연습: Windows Forms DataGridView 컨트롤에서 데이터 입력 중에 발생하는 오류 처리'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- error handling [Windows Forms], dataGridView control
- data grids [Windows Forms], error handling
- DataGridView control [Windows Forms], error handling
- data entry [Windows Forms], error handling
- error handling [Windows Forms], data entry
- walkthroughs [Windows Forms], DataGridView control
ms.assetid: 30a68b85-d3af-4946-83c1-1e2d010d0511
ms.openlocfilehash: cee6fe3b049378fa7bbe2585a3607049eaf231bc
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70046086"
---
# <a name="walkthrough-handling-errors-that-occur-during-data-entry-in-the-windows-forms-datagridview-control"></a>연습: Windows Forms DataGridView 컨트롤에서 데이터 입력 중에 발생하는 오류 처리

데이터 입력 응용 프로그램의 경우 기본 데이터 저장소에서 발생 하는 오류를 처리 하는 기능이 필요 합니다. Windows Forms <xref:System.Windows.Forms.DataGridView> 컨트롤은 데이터 저장소에서 제약 조건 위반 <xref:System.Windows.Forms.DataGridView.DataError> 또는 손상 된 비즈니스 규칙을 검색할 때 발생 하는 이벤트를 노출 하 여 쉽게 만듭니다.

이 연습에서는 Northwind 샘플 데이터베이스의 `Customers` 테이블에서 행을 검색 하 여 <xref:System.Windows.Forms.DataGridView> 컨트롤에 표시 합니다. 새 행 또는 `CustomerID` 편집 된 기존 행 <xref:System.Windows.Forms.DataGridView.DataError> 에서 중복 값이 검색 되 면이 이벤트가 발생 합니다 .이 이벤트는 예외를 설명 하는을 <xref:System.Windows.Forms.MessageBox> 표시 하 여 처리 됩니다.

이 항목의 코드를 단일 목록으로 복사하려면 [방법: Windows Forms DataGridView 컨트롤](handle-errors-that-occur-during-data-entry-in-the-datagrid.md)에서 데이터 입력 중에 발생 하는 오류를 처리 합니다.

## <a name="prerequisites"></a>필수 구성 요소

이 연습을 완료하려면 다음 사항이 필요합니다.

- Northwind SQL Server 예제 데이터베이스가 있는 서버에 액세스 합니다.

## <a name="creating-the-form"></a>폼 만들기

#### <a name="to-handle-data-entry-errors-in-the-datagridview-control"></a>DataGridView 컨트롤에서 데이터 입력 오류를 처리 하려면

1. 에서 <xref:System.Windows.Forms.Form> 파생 되 고 컨트롤과 <xref:System.Windows.Forms.BindingSource> 구성 요소를 <xref:System.Windows.Forms.DataGridView> 포함 하는 클래스를 만듭니다.

    다음 코드 예제에서는 기본 초기화를 제공 하며 메서드 `Main` 를 포함 합니다.

    [!code-csharp[System.Windows.Forms.DataGridView.DataError#01](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/CS/errorhandling.cs#01)]
    [!code-vb[System.Windows.Forms.DataGridView.DataError#01](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/VB/errorhandling.vb#01)]
    [!code-csharp[System.Windows.Forms.DataGridView.DataError#02](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/CS/errorhandling.cs#02)]
    [!code-vb[System.Windows.Forms.DataGridView.DataError#02](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/VB/errorhandling.vb#02)]

2. 데이터베이스 연결에 대 한 세부 정보를 처리 하기 위해 폼의 클래스 정의에 메서드를 구현 합니다.

    이 코드 예제에서는 채워진 `GetData` <xref:System.Data.DataTable> 개체를 반환 하는 메서드를 사용 합니다. `connectionString` 변수를 데이터베이스에 적합 한 값으로 설정 해야 합니다.

    > [!IMPORTANT]
    > 암호와 같은 중요한 정보를 연결 문자열 내에 저장하면 애플리케이션 보안 문제가 발생할 수 있습니다. 데이터베이스 액세스를 제어할 경우에는 통합 보안이라고도 하는 Windows 인증을 사용하는 방법이 더 안전합니다. 자세한 내용은 [연결 정보 보호](../../data/adonet/protecting-connection-information.md)를 참조하세요.

    [!code-csharp[System.Windows.Forms.DataGridView.DataError#30](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/CS/errorhandling.cs#30)]
    [!code-vb[System.Windows.Forms.DataGridView.DataError#30](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/VB/errorhandling.vb#30)]

3. 및<xref:System.Windows.Forms.DataGridView> <xref:System.Windows.Forms.Form.Load> 를초기화하고데이터바인딩을설정하는폼의이벤트에대한처리기<xref:System.Windows.Forms.BindingSource> 를 구현 합니다.

    [!code-csharp[System.Windows.Forms.DataGridView.DataError#10](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/CS/errorhandling.cs#10)]
    [!code-vb[System.Windows.Forms.DataGridView.DataError#10](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/VB/errorhandling.vb#10)]

4. 에서 이벤트 <xref:System.Windows.Forms.DataGridView.DataError> 를 처리 합니다.<xref:System.Windows.Forms.DataGridView>

    오류에 대 한 컨텍스트가 커밋 작업 인 경우에 <xref:System.Windows.Forms.MessageBox>오류를 표시 합니다.

    [!code-csharp[System.Windows.Forms.DataGridView.DataError#20](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/CS/errorhandling.cs#20)]
    [!code-vb[System.Windows.Forms.DataGridView.DataError#20](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/VB/errorhandling.vb#20)]

## <a name="testing-the-application"></a>애플리케이션 테스트

이제 폼을 테스트 하 여 예상 대로 동작 하는지 확인할 수 있습니다.

#### <a name="to-test-the-form"></a>폼을 테스트 하려면

- F5 키를 눌러 애플리케이션을 실행합니다.

  Customers 테이블의 데이터로 <xref:System.Windows.Forms.DataGridView> 채워진 컨트롤이 표시 됩니다. 에 대해 `CustomerID` 중복 값을 입력 하 고 편집 내용을 커밋하면 셀 값이 자동으로 되돌아가고 데이터 입력 오류를 표시 <xref:System.Windows.Forms.MessageBox> 하는이 표시 됩니다.

## <a name="next-steps"></a>다음 단계

이 응용 프로그램은 <xref:System.Windows.Forms.DataGridView> 컨트롤의 기능에 대 한 기본적인 이해를 제공 합니다. 여러 가지 방법으로 <xref:System.Windows.Forms.DataGridView> 컨트롤의 모양과 동작을 사용자 지정할 수 있습니다.

- 테두리 및 머리글 스타일을 변경 합니다. 자세한 내용은 [방법: Windows Forms DataGridView 컨트롤](change-the-border-and-gridline-styles-in-the-datagrid.md)의 테두리 및 모눈선 스타일을 변경 합니다.

- 사용자 입력을 <xref:System.Windows.Forms.DataGridView> 컨트롤에 사용 하거나 제한 합니다. 자세한 내용은 [방법: Windows Forms DataGridView 컨트롤](prevent-row-addition-and-deletion-datagridview.md)에서 행 추가 및 삭제를 방지 하 고 [다음을 수행 합니다. Windows Forms DataGridView 컨트롤](how-to-make-columns-read-only-in-the-windows-forms-datagridview-control.md)에서 열을 읽기 전용으로 설정 합니다.

- <xref:System.Windows.Forms.DataGridView> 컨트롤에 대 한 사용자 입력의 유효성을 검사 합니다. 자세한 내용은 [연습: DataGridView 컨트롤](walkthrough-validating-data-in-the-windows-forms-datagridview-control.md)Windows Forms에서 데이터의 유효성을 검사 합니다.

- 가상 모드를 사용 하 여 매우 큰 데이터 집합을 처리 합니다. 자세한 내용은 [연습: Windows Forms DataGridView 컨트롤](implementing-virtual-mode-wf-datagridview-control.md)에서 가상 모드 구현.

- 셀의 모양을 사용자 지정 합니다. 자세한 내용은 [방법: DataGridView 컨트롤](customize-the-appearance-of-cells-in-the-datagrid.md) Windows Forms에서 셀의 모양을 사용자 지정 하 고 [다음을 수행 합니다. Windows Forms DataGridView 컨트롤](how-to-set-default-cell-styles-for-the-windows-forms-datagridview-control.md)의 기본 셀 스타일을 설정 합니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.BindingSource>
- [Windows Forms DataGridView 컨트롤의 데이터 입력](data-entry-in-the-windows-forms-datagridview-control.md)
- [방법: Windows Forms DataGridView 컨트롤에서 데이터 입력 중에 발생 하는 오류를 처리 합니다.](handle-errors-that-occur-during-data-entry-in-the-datagrid.md)
- [연습: Windows Forms DataGridView 컨트롤의 데이터 유효성 검사](walkthrough-validating-data-in-the-windows-forms-datagridview-control.md)
- [연결 정보 보호](../../data/adonet/protecting-connection-information.md)
