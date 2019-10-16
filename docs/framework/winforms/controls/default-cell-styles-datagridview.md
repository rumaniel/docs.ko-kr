---
title: '방법: 디자이너를 사용하여 Windows Forms DataGridView 컨트롤에 대한 기본 셀 스타일 및 데이터 형식 설정'
ms.date: 03/30/2017
helpviewer_keywords:
- DataGridView control [Windows Forms], cell styles
- cells [Windows Forms], setting styles
- data formats
- data [Windows Forms], setting formats
ms.assetid: fc6da49f-8942-41da-b49f-b2afc38cc656
ms.openlocfilehash: 6d7d867b7c9e83b68589e046565bfb0199692f5f
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69658508"
---
# <a name="how-to-set-default-cell-styles-and-data-formats-for-the-windows-forms-datagridview-control-using-the-designer"></a>방법: 디자이너를 사용하여 Windows Forms DataGridView 컨트롤에 대한 기본 셀 스타일 및 데이터 형식 설정

<xref:System.Windows.Forms.DataGridView> 컨트롤을 사용 하면 특정 열, 행 및 열 머리글에 대 한 기본 셀 스타일 및 셀 데이터 형식을 지정 하 고, 교대로 반복 되는 행에 대해 원장 효과를 만들 수 있습니다. 전체 컨트롤에 대해 설정 된 기본 스타일은 열 및 교대로 반복 되는 행에 대해 설정 된 기본 스타일에 의해 재정의 됩니다. 또한 개별 행 및 셀에 대해 코드에서 설정한 스타일이 기본 스타일을 재정의 합니다.

셀 스타일에 대 한 자세한 내용은 참조 하세요. [Windows Forms DataGridView 컨트롤의 셀 스타일](cell-styles-in-the-windows-forms-datagridview-control.md)합니다. 교대로 반복 되 [는 행에 대 한 스타일을 설정 하려면 방법: 디자이너](set-alternating-row-styles-for-the-datagrid-using-the-designer.md)를 사용 하 여 Windows Forms DataGridView 컨트롤에 대해 교대로 반복 되는 행 스타일을 설정 합니다.

또한 <xref:System.Windows.Forms.DataGridView.RowTemplate%2A> 속성을 사용 하 여 컨트롤에 추가 되는 모든 행에 영향을 주는 스타일을 설정할 수 있습니다. 행 템플릿에 [대 한 자세한 내용은 방법: Windows Forms DataGridView 컨트롤](use-the-row-template-to-customize-rows-in-the-datagrid.md)의 행을 사용자 지정 하려면 행 템플릿을 사용 합니다.

다음 절차에는 <xref:System.Windows.Forms.DataGridView> 컨트롤을 포함 하는 폼을 포함 하는 **Windows 응용 프로그램** 프로젝트가 필요 합니다. 이러한 프로젝트 [를 설정 하는 방법에 대 한 자세한 내용은 방법: Windows Forms 응용 프로그램 프로젝트](/visualstudio/ide/step-1-create-a-windows-forms-application-project) [를 만들고 방법: Windows Forms](how-to-add-controls-to-windows-forms.md)에 컨트롤을 추가 합니다.

### <a name="to-set-default-styles-for-all-cells-in-the-control"></a>컨트롤의 모든 셀에 대 한 기본 스타일을 설정 하려면

1. 디자이너에서 <xref:System.Windows.Forms.DataGridView> 컨트롤을 선택 합니다.

2. **속성** ![창에서 <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A>,](./media/visual-studio-ellipsis-button.png) 또는<xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle%2A>속성 옆에 있는 줄임표 단추 (Visual Studio 속성 창의 줄임표 단추 (...)를 클릭 합니다. <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle%2A> **CellStyle 작성기** 대화 상자가 나타납니다.

3. **미리 보기** 창을 사용 하 여 선택 내용을 확인 하 고 속성을 설정 하 여 스타일을 정의 합니다.

> [!NOTE]
> 비주얼 스타일을 사용 하는 경우를 제외 <xref:System.Windows.Forms.DataGridView.TopLeftHeaderCell%2A>하 고 행 및 열 머리글은 현재 테마에 따라 자동으로 스타일이 지정 되며 <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle%2A> 및 <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle%2A> 속성 값이 재정의 됩니다.
>
> 디자이너를 사용 하 여 선택한 <xref:System.Windows.Forms.DataGridView> 여러 컨트롤의 셀 스타일을 설정할 수 있습니다. 단, 수정할 셀 스타일 속성에 대해 동일한 값이 있는 경우에만 필요 합니다. 해당 속성에 대 한 셀 스타일이 다른 경우에는 **CellStyle 작성기** 대화 상자의 **속성** 창이 비어 있게 됩니다.

### <a name="to-set-default-styles-for-cells-in-individual-columns"></a>개별 열의 셀에 대 한 기본 스타일을 설정 하려면

1. 디자이너에서 컨트롤을 <xref:System.Windows.Forms.DataGridView> 마우스 오른쪽 단추로 클릭 하 고 **열 편집**을 선택 합니다.

2. **선택한 열** 목록에서 열을 선택 합니다.

3. **열 속성** 표에서![ 속성<xref:System.Windows.Forms.DataGridViewColumn.DefaultCellStyle%2A> 옆의 줄임표 단추 (Visual Studio](./media/visual-studio-ellipsis-button.png)의 속성 창에 있는 줄임표 단추 (...))를 클릭 합니다. **CellStyle 작성기** 대화 상자가 나타납니다.

4. **미리 보기** 창을 사용 하 여 선택 내용을 확인 하 고 속성을 설정 하 여 스타일을 정의 합니다.

### <a name="to-format-data-in-cells"></a>셀의 데이터에 서식을 지정 하려면

1. 위의 절차 중 하나를 사용 하 여 기본 셀 스타일 속성과 관련 된 **CellStyle 작성기** 대화 상자를 표시 합니다.

2. **CellStyle 작성기** 대화 상자에서![ <xref:System.Windows.Forms.DataGridViewCellStyle.Format%2A> 속성 옆에 있는 줄임표 단추 (Visual Studio](./media/visual-studio-ellipsis-button.png)속성 창의 줄임표 단추 (...)를 클릭 합니다. **형식 문자열** 대화 상자가 나타납니다.

3. 서식 유형을 선택한 다음 **샘플** 상자를 사용 하 여 선택 항목을 확인 하는 유형의 세부 정보 (예: 표시할 소수 자릿수)를 수정 합니다.

4. Null 값이 포함 될 <xref:System.Windows.Forms.DataGridView> 수 있는 데이터 소스에 컨트롤을 바인딩하는 경우 **null 값** 텍스트 상자에 입력 합니다. 이 값은 셀 값이 null 참조 (`Nothing` Visual Basic) 또는 <xref:System.DBNull.Value?displayProperty=nameWithType>와 같은 경우에 표시 됩니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridViewCellStyle>
- <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewColumn.DefaultCellStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewCellStyle.Format%2A?displayProperty=nameWithType>
- [Windows Forms DataGridView 컨트롤의 셀 스타일](cell-styles-in-the-windows-forms-datagridview-control.md)
- [방법: 디자이너를 사용 하 여 Windows Forms DataGridView 컨트롤에 대해 교대로 반복 되는 행 스타일 설정](set-alternating-row-styles-for-the-datagrid-using-the-designer.md)
- [방법: Windows Forms 애플리케이션 프로젝트 만들기](/visualstudio/ide/step-1-create-a-windows-forms-application-project)
- [방법: Windows Forms에 컨트롤 추가](how-to-add-controls-to-windows-forms.md)
