---
title: '연습: 두 Windows Forms DataGridView 컨트롤을 사용 하 여 마스터-세부 폼 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataGridView control [Windows Forms], master/detail form
- parent-child tables [Windows Forms], displaying on Windows Forms
- master-details lists [Windows Forms], displaying on Windows Forms
- walkthroughs [Windows Forms], DataGridView control
ms.assetid: c5fa29e8-47f7-4691-829b-0e697a691f36
ms.openlocfilehash: 4212c7223aca6a5e7de3189d5f6b2757453cc438
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70046091"
---
# <a name="walkthrough-creating-a-masterdetail-form-using-two-windows-forms-datagridview-controls"></a>연습: 두 개의 Windows Forms DataGridView 컨트롤을 사용하여 마스터/세부 양식 만들기

<xref:System.Windows.Forms.DataGridView> 컨트롤 사용에 대 한 가장 일반적인 시나리오 중 하나는 두 데이터베이스 테이블 간의 부모/자식 관계가 표시 되는 *마스터/세부* 폼입니다. 마스터 테이블에서 행을 선택 하면 세부 정보 테이블이 해당 자식 데이터로 업데이트 됩니다.

<xref:System.Windows.Forms.DataGridView> 컨트롤과<xref:System.Windows.Forms.BindingSource> 구성 요소 간의 상호 작용을 사용 하 여 마스터/세부 폼을 쉽게 구현할 수 있습니다. 이 연습에서는 두 <xref:System.Windows.Forms.DataGridView> 개의 컨트롤과 두 개의 <xref:System.Windows.Forms.BindingSource> 구성 요소를 사용 하 여 폼을 빌드합니다. 이 폼에는 Northwind SQL Server 예제 데이터베이스에와 `Customers` `Orders`라는 두 개의 관련 테이블이 표시 됩니다. 작업이 완료 되 면 마스터 <xref:System.Windows.Forms.DataGridView> 의 데이터베이스에 있는 모든 고객을 표시 하는 폼과 선택한 고객에 대 한 모든 주문이 세부 정보 <xref:System.Windows.Forms.DataGridView>로 표시 됩니다.

이 항목의 코드를 단일 목록으로 복사하려면 [방법: 두 Windows Forms DataGridView 컨트롤](create-a-master-detail-form-using-two-datagridviews.md)을 사용 하 여 마스터/세부 폼을 만듭니다.

## <a name="prerequisites"></a>전제 조건

이 연습을 완료하려면 다음 사항이 필요합니다.

- Northwind SQL Server 예제 데이터베이스가 있는 서버에 액세스 합니다.

## <a name="creating-the-form"></a>폼 만들기

#### <a name="to-create-a-masterdetail-form"></a>마스터/세부 폼을 만들려면

1. 에서 <xref:System.Windows.Forms.Form> 파생 되 고 두 개의 <xref:System.Windows.Forms.DataGridView> 컨트롤과 두 개의 <xref:System.Windows.Forms.BindingSource> 구성 요소를 포함 하는 클래스를 만듭니다. 다음 코드는 기본 폼 초기화를 제공 하 고 `Main` 메서드를 포함 합니다. Visual Studio 디자이너를 사용 하 여 폼을 만드는 경우이 코드 대신 디자이너에서 생성 한 코드를 사용할 수 있지만 여기에 변수 선언에 표시 된 이름을 사용 해야 합니다.

    [!code-csharp[System.Windows.Forms.DataGridViewMasterDetails#01](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMasterDetails/CS/masterdetails.cs#01)]
    [!code-vb[System.Windows.Forms.DataGridViewMasterDetails#01](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMasterDetails/VB/masterdetails.vb#01)]
    [!code-csharp[System.Windows.Forms.DataGridViewMasterDetails#02](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMasterDetails/CS/masterdetails.cs#02)]
    [!code-vb[System.Windows.Forms.DataGridViewMasterDetails#02](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMasterDetails/VB/masterdetails.vb#02)]

2. 데이터베이스에 연결 하는 세부 정보를 처리 하기 위해 폼의 클래스 정의에 메서드를 구현 합니다. 이 예제에서는 <xref:System.Data.DataSet> 개체 `GetData` 를 채우고, 데이터 집합 <xref:System.Windows.Forms.BindingSource> 에 <xref:System.Data.DataRelation> 개체를 추가 하 고, 구성 요소를 바인딩하는 메서드를 사용 합니다. `connectionString` 변수를 사용자의 데이터베이스에 적합한 값으로 설정해야 합니다.

    > [!IMPORTANT]
    > 암호와 같은 중요한 정보를 연결 문자열 내에 저장하면 애플리케이션 보안 문제가 발생할 수 있습니다. 데이터베이스 액세스를 제어할 경우에는 통합 보안이라고도 하는 Windows 인증을 사용하는 방법이 더 안전합니다. 자세한 내용은 [연결 정보 보호](../../data/adonet/protecting-connection-information.md)를 참조하세요.

    [!code-csharp[System.Windows.Forms.DataGridViewMasterDetails#20](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMasterDetails/CS/masterdetails.cs#20)]
    [!code-vb[System.Windows.Forms.DataGridViewMasterDetails#20](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMasterDetails/VB/masterdetails.vb#20)]

3. 컨트롤을 <xref:System.Windows.Forms.Form.Load> <xref:System.Windows.Forms.BindingSource> 구성 요소에 `GetData` 바인딩한 다음 메서드를 호출 하는 폼의 이벤트에 대 한 처리기를 구현 합니다. <xref:System.Windows.Forms.DataGridView> 다음 예제에는 표시 된 데이터 <xref:System.Windows.Forms.DataGridView> 에 맞게 열의 크기를 조정 하는 코드가 포함 되어 있습니다.

    [!code-csharp[System.Windows.Forms.DataGridViewMasterDetails#10](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMasterDetails/CS/masterdetails.cs#10)]
    [!code-vb[System.Windows.Forms.DataGridViewMasterDetails#10](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMasterDetails/VB/masterdetails.vb#10)]

## <a name="testing-the-application"></a>애플리케이션 테스트

이제 폼을 테스트 하 여 예상 대로 동작 하는지 확인할 수 있습니다.

#### <a name="to-test-the-form"></a>폼을 테스트 하려면

- 애플리케이션을 컴파일하고 실행합니다.

  서로 다른 두 개의 <xref:System.Windows.Forms.DataGridView> 컨트롤이 표시 됩니다. 위쪽은 Northwind `Customers` 테이블의 고객이 고 하단 `Orders` 은 선택 된 고객에 해당 하는입니다. 위쪽 <xref:System.Windows.Forms.DataGridView>에 있는 다른 행을 선택 하면 그에 따라 아래쪽 <xref:System.Windows.Forms.DataGridView> 의 내용이 변경 됩니다.

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
- [Windows Forms DataGridView 컨트롤에서 데이터 표시](displaying-data-in-the-windows-forms-datagridview-control.md)
- [방법: 두 Windows Forms DataGridView 컨트롤을 사용 하 여 마스터/세부 폼 만들기](create-a-master-detail-form-using-two-datagridviews.md)
- [연결 정보 보호](../../data/adonet/protecting-connection-information.md)
