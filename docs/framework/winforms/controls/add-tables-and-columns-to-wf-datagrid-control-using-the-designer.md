---
title: '방법: 디자이너를 사용하여 Windows Forms DataGrid 컨트롤에 테이블 및 열 추가'
ms.date: 03/30/2017
helpviewer_keywords:
- columns [Windows Forms], adding to DataGrid control
- tables [Windows Forms], adding to DataGrid control
- DataGrid control [Windows Forms], adding tables and columns
ms.assetid: 4a6d1b34-b696-476b-bf8a-57c6230aa9e1
ms.openlocfilehash: d11c4f7e4cdfb597477bb99f38612ed648849f20
ms.sourcegitcommit: cf9515122fce716bcfb6618ba366e39b5a2eb81e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69040047"
---
# <a name="how-to-add-tables-and-columns-to-the-windows-forms-datagrid-control-using-the-designer"></a>방법: 디자이너를 사용하여 Windows Forms DataGrid 컨트롤에 테이블 및 열 추가

> [!NOTE]
> <xref:System.Windows.Forms.DataGridView> 컨트롤은 <xref:System.Windows.Forms.DataGrid> 컨트롤을 대체하고 여기에 다른 기능을 추가하여 새로 도입된 컨트롤이지만 이전 버전과의 호환성 및 이후 사용 가능성을 고려하여 <xref:System.Windows.Forms.DataGrid> 컨트롤을 계속 유지하도록 선택할 수 있습니다. 자세한 내용은 [Windows Forms DataGridView 및 DataGrid 컨트롤의 차이점](differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)을 참조하십시오.

<xref:System.Windows.Forms.DataGrid> 개체를 만들고 <xref:System.Windows.Forms.DataGrid> <xref:System.Windows.Forms.GridTableStylesCollection> 컨트롤의<xref:System.Windows.Forms.DataGrid.TableStyles%2A> 속성을 통해 액세스 되는 개체에 개체를 추가 하 여 테이블 및 열에 Windows Forms 컨트롤의 데이터를 표시할 수 있습니다. <xref:System.Windows.Forms.DataGridTableStyle> 각 테이블 스타일은 <xref:System.Windows.Forms.DataGridTableStyle.MappingName%2A> <xref:System.Windows.Forms.DataGridTableStyle>의 속성에 지정 된 모든 데이터 테이블의 내용을 표시 합니다. 기본적으로 열 스타일이 지정 되지 않은 테이블 스타일은 해당 데이터 테이블 내의 모든 열을 표시 합니다. 개체 <xref:System.Windows.Forms.DataGridColumnStyle> <xref:System.Windows.Forms.DataGridTableStyle.GridColumnStyles%2A> 를에<xref:System.Windows.Forms.DataGridTableStyle>추가 하 여 나타나는 테이블의 열 을제한할수있습니다.이열은각의속성을통해액세스됩니다.<xref:System.Windows.Forms.GridColumnStylesCollection>

다음 절차를 수행 하려면 <xref:System.Windows.Forms.DataGrid> 컨트롤이 포함 된 폼을 포함 하는 **Windows 응용 프로그램** 프로젝트가 필요 합니다. 이러한 프로젝트 [를 설정 하는 방법에 대 한 자세한 내용은 방법: Windows Forms 응용 프로그램 프로젝트](/visualstudio/ide/step-1-create-a-windows-forms-application-project) [를 만들고 방법: Windows Forms](how-to-add-controls-to-windows-forms.md)에 컨트롤을 추가 합니다. Visual Studio 2005 <xref:System.Windows.Forms.DataGrid> 에서는 기본적으로 컨트롤이 **도구 상자**에 없습니다. 이를 추가 하 [는 방법에 대 한 자세한 내용은 방법: 도구 상자](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/ms165355(v=vs.100))에 항목을 추가 합니다.

### <a name="to-add-a-table-to-the-datagrid-control-in-the-designer"></a>디자이너에서 DataGrid 컨트롤에 테이블을 추가 하려면

1. 테이블에 데이터를 표시 하려면 먼저 <xref:System.Windows.Forms.DataGrid> 컨트롤을 데이터 집합에 바인딩해야 합니다. 자세한 내용은 [방법: 디자이너](bind-wf-datagrid-control-to-a-data-source-using-the-designer.md)를 사용 하 여 Windows Forms DataGrid 컨트롤을 데이터 소스에 바인딩합니다.

2. 속성 창에서 <xref:System.Windows.Forms.DataGrid.TableStyles%2A> ![컨트롤의 속성을 선택한 다음 줄임표 단추 (Visual Studio 속성 창의 줄임표 단추 (...)를 클릭 하 여 속성 옆에 있는 줄임표 단추 (...)를 클릭 하 여 다음을 표시 합니다.](./media/visual-studio-ellipsis-button.png) <xref:System.Windows.Forms.DataGrid> **DataGridTableStyle 컬렉션 편집기**입니다.

3. 컬렉션 편집기에서 **추가** 를 클릭 하 여 테이블 스타일을 삽입 합니다.

4. **확인** 을 클릭 하 여 컬렉션 편집기를 닫은 다음 <xref:System.Windows.Forms.DataGrid.TableStyles%2A> 속성 옆에 있는 줄임표 단추를 클릭 하 여 다시 엽니다.

     컬렉션 편집기를 다시 열면 컨트롤에 바인딩된 모든 데이터 테이블이 테이블 스타일의 <xref:System.Windows.Forms.DataGridTableStyle.MappingName%2A> 속성에 대 한 드롭다운 목록에 표시 됩니다.

5. 컬렉션 편집기의 **멤버** 상자에서 테이블 스타일을 클릭 합니다.

6. 컬렉션 편집기의 **속성** 상자에서 표시 하려는 테이블에 대 <xref:System.Windows.Forms.DataGridTableStyle.MappingName%2A> 한 값을 선택 합니다.

### <a name="to-add-a-column-to-the-datagrid-control-in-the-designer"></a>디자이너에서 DataGrid 컨트롤에 열을 추가 하려면

1. **DataGridTableStyle 컬렉션 편집기**의 **멤버** 상자에서 적절 한 테이블 스타일을 선택 합니다. 컬렉션 편집기의 **속성** 상자에서 <xref:System.Windows.Forms.DataGridTableStyle.GridColumnStyles%2A> 컬렉션을 선택 하 고 속성 옆에 있는 줄임표 단추 (![Visual Studio 속성 창의 줄임표 단추 (...)를 클릭 합니다.](./media/visual-studio-ellipsis-button.png) **System.windows.forms.datagridcolumnstyle> 컬렉션 편집기**를 표시 합니다.

2. 컬렉션 편집기에서 **추가** 를 클릭 하 여 열 스타일을 삽입 하거나 **추가** 옆에 있는 아래쪽 화살표를 클릭 하 여 열 유형을 지정 합니다.

     드롭다운 상자에서 <xref:System.Windows.Forms.DataGridTextBoxColumn> 또는 <xref:System.Windows.Forms.DataGridBoolColumn> 형식 중 하나를 선택할 수 있습니다.

3. 확인을 클릭 하 여 **system.windows.forms.datagridcolumnstyle> 컬렉션 편집기**를 닫은 다음 <xref:System.Windows.Forms.DataGridTableStyle.GridColumnStyles%2A> 속성 옆에 있는 줄임표 단추를 클릭 하 여 다시 엽니다.

     컬렉션 편집기를 다시 열면 바인딩된 데이터 테이블의 모든 데이터 열이 열 스타일의 <xref:System.Windows.Forms.DataGridColumnStyle.MappingName%2A> 속성에 대 한 드롭다운 목록에 표시 됩니다.

4. 컬렉션 편집기의 **멤버** 상자에서 열 스타일을 클릭 합니다.

5. 컬렉션 편집기의 **속성** 상자에서 표시 하려는 열에 대 <xref:System.Windows.Forms.DataGridColumnStyle.MappingName%2A> 한 값을 선택 합니다.

## <a name="see-also"></a>참고자료

- [DataGrid 컨트롤](datagrid-control-windows-forms.md)
- [방법: Windows Forms DataGrid 컨트롤에서 열 삭제 또는 숨기기](how-to-delete-or-hide-columns-in-the-windows-forms-datagrid-control.md)
