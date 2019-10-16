---
title: '방법: 디자이너를 사용하여 Windows Forms DataGrid 컨트롤에 마스터-세부 목록 만들기'
ms.date: 03/30/2017
helpviewer_keywords:
- master-details lists
- DataGrid control [Windows Forms], master-details lists
- related tables [Windows Forms], displaying in DataGrid control
ms.assetid: 19438ba2-f687-4417-a2fb-ab1cd69d4ded
ms.openlocfilehash: 3962b671176ad158b338889140181834e05bbeee
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69929719"
---
# <a name="how-to-create-master-details-lists-with-the-windows-forms-datagrid-control-using-the-designer"></a>방법: 디자이너를 사용하여 Windows Forms DataGrid 컨트롤에 마스터-세부 목록 만들기

> [!NOTE]
> <xref:System.Windows.Forms.DataGridView> 컨트롤은 <xref:System.Windows.Forms.DataGrid> 컨트롤을 대체하고 여기에 다른 기능을 추가하여 새로 도입된 컨트롤이지만 이전 버전과의 호환성 및 이후 사용 가능성을 고려하여 <xref:System.Windows.Forms.DataGrid> 컨트롤을 계속 유지하도록 선택할 수 있습니다. 자세한 내용은 [Windows Forms DataGridView 및 DataGrid 컨트롤의 차이점](differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)을 참조하십시오.

 에 <xref:System.Data.DataSet> 일련의 관련 테이블이 포함 되어 있는 경우 두 개의 <xref:System.Windows.Forms.DataGrid> 컨트롤을 사용 하 여 데이터를 마스터-세부 형식으로 표시할 수 있습니다. 하나 <xref:System.Windows.Forms.DataGrid> 는 마스터 그리드로 지정 되 고 두 번째는 세부 정보 표로 지정 됩니다. 마스터 목록에서 항목을 선택 하면 관련 된 모든 자식 항목이 세부 정보 목록에 표시 됩니다. 예를 들어에 <xref:System.Data.DataSet> customers 테이블과 관련 Orders 테이블이 포함 되어 있는 경우에는 customers 테이블을 마스터 그리드로 지정 하 고 orders 테이블을 세부 정보 표로 지정 합니다. 마스터 표에서 고객이 선택 된 경우 Orders 테이블에서 해당 고객과 연결 된 모든 주문이 세부 정보 표에 표시 됩니다.

 다음 절차를 수행 하려면 **Windows 응용 프로그램** 프로젝트가 필요 합니다 (**파일** > **새로 만들기** > **프로젝트** > **Visual C#**  또는 **Visual Basic**  >   **클래식 데스크톱** > **Windows Forms 응용 프로그램**).

## <a name="to-create-a-master-details-list-in-the-designer"></a>디자이너에서 마스터-세부 목록을 만들려면

1. 폼에 <xref:System.Windows.Forms.DataGrid> 컨트롤 두 개를 추가 합니다. 자세한 내용은 [방법: Windows Forms](how-to-add-controls-to-windows-forms.md)에 컨트롤을 추가 합니다. Visual Studio 2005 <xref:System.Windows.Forms.DataGrid> 에서 컨트롤은 기본적으로 **도구 상자** 에 있지 않습니다. 자세한 내용은 [방법: 도구 상자](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/ms165355(v=vs.100))에 항목을 추가 합니다.

    > [!NOTE]
    > 다음 단계는 디자인 타임 데이터 바인딩에 대해 **데이터 소스** 창을 사용 하는 Visual Studio 2005에는 적용 되지 않습니다. 자세한 내용은 [Visual Studio에서 데이터에 컨트롤 바인딩](/visualstudio/data-tools/bind-controls-to-data-in-visual-studio) 및 [방법: Windows Forms 응용 프로그램](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/57tx3hhe(v=vs.120))에 관련 데이터를 표시 합니다.

2. **서버 탐색기** 에서 폼으로 두 개 이상의 테이블을 끌어 옵니다.

3. **데이터** 메뉴에서 데이터 **집합 생성**을 선택 합니다.

4. XML 디자이너를 사용 하 여 테이블 간의 관계를 설정 합니다. 자세한 내용은 다음을 참조 하세요. MSDN의 XML 스키마 및 데이터 집합에서 일 대 다 관계를 만듭니다.

5. **파일** 메뉴에서 **모두 저장** 을 선택 하 여 관계를 저장 합니다.

6. 다음과 같이 <xref:System.Windows.Forms.DataGrid> 마스터 그리드를 지정 하려는 컨트롤을 구성 합니다.

    1. 속성의 드롭다운 목록에서를 <xref:System.Data.DataSet> 선택 합니다. <xref:System.Windows.Forms.DataGrid.DataSource%2A>

    2. <xref:System.Windows.Forms.DataGrid.DataMember%2A> 속성의 드롭다운 목록에서 마스터 테이블 (예: "Customers")을 선택 합니다.

7. 다음과 같이 <xref:System.Windows.Forms.DataGrid> 세부 정보 표를 지정 하려는 컨트롤을 구성 합니다.

    1. 속성의 드롭다운 목록에서를 <xref:System.Data.DataSet> 선택 합니다. <xref:System.Windows.Forms.DataGrid.DataSource%2A>

    2. <xref:System.Windows.Forms.DataGrid.DataMember%2A> 속성의 드롭다운 목록에서 마스터 테이블과 세부 테이블 간의 관계 (예: "CustOrd")를 선택 합니다. 관계를 보려면 드롭다운 목록에서 마스터 테이블 옆에 있는 더하기 기호 ( **+** )를 클릭 하 여 노드를 확장 합니다.

## <a name="see-also"></a>참고자료

- [DataGrid 컨트롤](datagrid-control-windows-forms.md)
- [DataGrid 컨트롤 개요](datagrid-control-overview-windows-forms.md)
- [방법: Windows Forms DataGrid 컨트롤을 데이터 소스에 바인딩](how-to-bind-the-windows-forms-datagrid-control-to-a-data-source.md)
- [Visual Studio에서 데이터에 컨트롤 바인딩](/visualstudio/data-tools/bind-controls-to-data-in-visual-studio)
