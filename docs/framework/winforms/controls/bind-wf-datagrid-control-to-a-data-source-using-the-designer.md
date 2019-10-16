---
title: '방법: 디자이너를 사용하여 데이터 원본에 Windows Forms DataGrid 컨트롤 바인딩'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- datasets [Windows Forms], binding to DataGrid control
- data binding [Windows Forms], DataGrid control
- DataGrid control [Windows Forms], data binding
- Windows Forms controls, data binding
- bound controls [Windows Forms]
ms.assetid: 4e96e3d0-b1cc-4de1-8774-bc9970ec4554
ms.openlocfilehash: 665a1af990aaf615c763c1c2eae508024d9de5c7
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69917823"
---
# <a name="how-to-bind-the-windows-forms-datagrid-control-to-a-data-source-using-the-designer"></a>방법: 디자이너를 사용하여 데이터 원본에 Windows Forms DataGrid 컨트롤 바인딩

> [!NOTE]
> <xref:System.Windows.Forms.DataGridView> 컨트롤은 <xref:System.Windows.Forms.DataGrid> 컨트롤을 대체하고 여기에 다른 기능을 추가하여 새로 도입된 컨트롤이지만 이전 버전과의 호환성 및 이후 사용 가능성을 고려하여 <xref:System.Windows.Forms.DataGrid> 컨트롤을 계속 유지하도록 선택할 수 있습니다. 자세한 내용은 [Windows Forms DataGridView 및 DataGrid 컨트롤의 차이점](differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)을 참조하십시오.

 Windows Forms <xref:System.Windows.Forms.DataGrid> 컨트롤은 데이터 원본의 정보를 표시 하도록 특별히 설계 되었습니다. 디자인 타임에 <xref:System.Windows.Forms.DataGrid.DataSource%2A> 및 <xref:System.Windows.Forms.DataGrid.DataMember%2A> 속성을 설정 하거나 <xref:System.Windows.Forms.DataGrid.SetDataBinding%2A> 메서드를 호출 하 여 런타임에 컨트롤을 바인딩합니다. 다양 한 데이터 원본의 데이터를 표시할 수 있지만 가장 일반적인 원본은 데이터 집합 및 데이터 뷰입니다.

 디자인 타임에 데이터 원본을 사용할 수 있는 경우 (예: 폼에 데이터 집합 또는 데이터 뷰의 인스턴스가 포함 된 경우) 디자인 타임에 표를 데이터 원본에 바인딩할 수 있습니다. 그러면 표에서 데이터가 표시 되는 모양을 미리 볼 수 있습니다.

 런타임에 프로그래밍 방식으로 그리드를 바인딩할 수도 있습니다. 이는 런타임에 가져오는 정보를 기반으로 데이터 소스를 설정 하려는 경우에 유용 합니다. 예를 들어 응용 프로그램에서 사용자가 보려는 테이블의 이름을 지정할 수 있습니다. 디자인 타임에 데이터 원본이 없는 경우에도 필요 합니다. 여기에는 배열, 컬렉션, 형식화 되지 않은 데이터 집합 및 데이터 판독기와 같은 데이터 소스가 포함 됩니다.

 다음 절차에는 <xref:System.Windows.Forms.DataGrid> 컨트롤을 포함 하는 폼을 포함 하는 **Windows 응용 프로그램** 프로젝트가 필요 합니다. 이러한 프로젝트 [를 설정 하는 방법에 대 한 자세한 내용은 방법: Windows Forms 응용 프로그램 프로젝트](/visualstudio/ide/step-1-create-a-windows-forms-application-project) [를 만들고 방법: Windows Forms](how-to-add-controls-to-windows-forms.md)에 컨트롤을 추가 합니다. Visual Studio 2005 <xref:System.Windows.Forms.DataGrid> 에서 컨트롤은 기본적으로 **도구 상자** 에 있지 않습니다. 이를 추가 하 [는 방법에 대 한 자세한 내용은 방법: 도구 상자](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/ms165355(v=vs.100))에 항목을 추가 합니다. 또한 Visual Studio 2005에서는 디자인 타임 데이터 바인딩에 대해 **데이터 소스** 창을 사용할 수 있습니다. 자세한 내용은 [Visual Studio에서 데이터에 컨트롤 바인딩을](/visualstudio/data-tools/bind-controls-to-data-in-visual-studio)참조 하세요.

## <a name="to-data-bind-the-datagrid-control-to-a-single-table-in-the-designer"></a>디자이너에서 DataGrid 컨트롤을 단일 테이블에 데이터 바인딩하려면

1. 컨트롤의 <xref:System.Windows.Forms.DataGrid.DataSource%2A> 속성을 바인딩할 데이터 항목을 포함 하는 개체로 설정 합니다.

2. 데이터 소스가 데이터 집합인 경우 <xref:System.Windows.Forms.DataGrid.DataMember%2A> 속성을 바인딩할 테이블의 이름으로 설정 합니다.

3. 데이터 원본이 데이터 집합 또는 데이터 집합 테이블을 기반으로 하는 데이터 뷰 이면 폼에 코드를 추가 하 여 데이터 집합을 채웁니다.

     사용 하는 정확한 코드는 데이터 집합이 데이터를 가져오는 위치에 따라 달라 집니다. 데이터 집합을 데이터베이스에서 직접 채우는 경우 일반적으로 다음 코드 예제와 같이 `Fill` 데이터 어댑터의 메서드를 호출 합니다 .이 데이터 집합은 라는 `DsCategories1`데이터 집합을 채웁니다.

    ```vb
    sqlDataAdapter1.Fill(DsCategories1)
    ```

    ```csharp
    sqlDataAdapter1.Fill(DsCategories1);
    ```

    ```cpp
    sqlDataAdapter1->Fill(dsCategories1);
    ```

4. 필드 적절 한 테이블 스타일과 열 스타일을 표에 추가 합니다.

     테이블 스타일이 없으면 테이블은 표시 되지만 최소 서식 지정 및 모든 열이 표시 됩니다.

## <a name="to-data-bind-the-datagrid-control-to-multiple-tables-in-a-dataset-in-the-designer"></a>디자이너에서 데이터 집합의 여러 테이블에 DataGrid 컨트롤을 데이터 바인딩하려면

1. 컨트롤의 <xref:System.Windows.Forms.DataGrid.DataSource%2A> 속성을 바인딩할 데이터 항목을 포함 하는 개체로 설정 합니다.

2. 데이터 집합에 관련 테이블이 포함 된 경우 (즉, 관계 개체가 포함 된 경우) <xref:System.Windows.Forms.DataGrid.DataMember%2A> 속성을 부모 테이블의 이름으로 설정 합니다.

3. 데이터 집합을 채우는 코드를 작성 합니다.

## <a name="see-also"></a>참고자료

- [DataGrid 컨트롤 개요](datagrid-control-overview-windows-forms.md)
- [방법: Windows Forms DataGrid 컨트롤에 테이블 및 열 추가](how-to-add-tables-and-columns-to-the-windows-forms-datagrid-control.md)
- [DataGrid 컨트롤](datagrid-control-windows-forms.md)
- [Windows Forms 데이터 바인딩](../windows-forms-data-binding.md)
- [Visual Studio에서 데이터 액세스](/visualstudio/data-tools/accessing-data-in-visual-studio)
