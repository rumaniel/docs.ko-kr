---
title: '방법: 디자이너를 사용하여 Windows Forms DataGridView 컨트롤에 대한 대체 행 스타일 설정'
ms.date: 03/30/2017
helpviewer_keywords:
- ledger-like formats
- DataGridView control [Windows Forms], row style alternation
- Windows Forms, rows
- rows [Windows Forms], alternating
- data [Windows Forms], displaying
ms.assetid: 02373442-bf94-4470-9f8a-e44c4a9d5b88
ms.openlocfilehash: a24b4e6af98d2637ecae2352aaa881adcd1c1a45
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69666839"
---
# <a name="how-to-set-alternating-row-styles-for-the-windows-forms-datagridview-control-using-the-designer"></a>방법: 디자이너를 사용하여 Windows Forms DataGridView 컨트롤에 대한 대체 행 스타일 설정

표 형식 데이터는 교대로 반복 되는 행의 배경색이 서로 다른 원장 형식으로 표시 됩니다. 이 형식을 사용하면 특히 많은 열을 포함하는 넓은 테이블에서 사용자가 각 행에 있는 셀을 쉽게 구분할 수 있습니다.

<xref:System.Windows.Forms.DataGridView> 컨트롤을 사용하여 교대로 반복되는 행에 대한 전체 스타일 정보를 지정할 수 있습니다. 배경색 뿐만 아니라 전경 색 및 글꼴과 같은 스타일 특성을 사용 하 여 교대로 반복 되는 행을 구분할 수 있습니다. 자세한 내용은 [Windows Forms DataGridView 컨트롤의 셀 스타일](cell-styles-in-the-windows-forms-datagridview-control.md)합니다.

다음 절차에는 <xref:System.Windows.Forms.DataGridView> 컨트롤을 포함 하는 폼을 포함 하는 **Windows 응용 프로그램** 프로젝트가 필요 합니다. 이러한 프로젝트 [를 설정 하는 방법에 대 한 자세한 내용은 방법: Windows Forms 응용 프로그램 프로젝트](/visualstudio/ide/step-1-create-a-windows-forms-application-project) [를 만들고 방법: Windows Forms](how-to-add-controls-to-windows-forms.md)에 컨트롤을 추가 합니다.

### <a name="define-styles-for-alternating-rows"></a>교대로 반복 되는 행에 대 한 스타일 정의

1. 디자이너에서 <xref:System.Windows.Forms.DataGridView> 컨트롤을 선택 합니다.

2. 속성 창 ![](./media/visual-studio-ellipsis-button.png)에서 속성<xref:System.Windows.Forms.DataGridView.AlternatingRowsDefaultCellStyle%2A> 옆에 있는 줄임표 단추 (Visual Studio 속성 창의 줄임표 단추 (...)를 클릭 합니다.

3. **CellStyle 작성기** 대화 상자에서 속성을 설정 하 여 스타일을 정의 하 고 **미리 보기** 창을 사용 하 여 선택 내용을 확인 합니다. 지정 하는 스타일은 두 번째 항목부터 시작 하 여 컨트롤에 표시 되는 다른 모든 행에 사용 됩니다.

4. 나머지 행에 대 한 스타일을 정의 하려면 속성을 <xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A> 사용 하 여 2 단계와 3 단계를 반복 합니다.

    > [!NOTE]
    > 여러 속성에서 상속 된 스타일을 사용 하 여 셀이 표시 됩니다. 스타일 상속에 대 한 자세한 내용은 참조 하세요. [Windows Forms DataGridView 컨트롤의 셀 스타일](cell-styles-in-the-windows-forms-datagridview-control.md)합니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- [Windows Forms DataGridView 컨트롤의 셀 스타일](cell-styles-in-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤의 기본 형식 및 스타일 지정](basic-formatting-and-styling-in-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤에 디자이너 사용](using-the-designer-with-the-windows-forms-datagridview-control.md)
- [방법: Windows Forms 애플리케이션 프로젝트 만들기](/visualstudio/ide/step-1-create-a-windows-forms-application-project)
- [방법: Windows Forms에 컨트롤 추가](how-to-add-controls-to-windows-forms.md)
