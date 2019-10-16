---
title: DataGridView 컨트롤 기술 요약(Windows Forms)
ms.date: 03/30/2017
helpviewer_keywords:
- DataGridView control [Windows Forms], about DataGridView control
- data grids [Windows Forms], about data grids
ms.assetid: 094498c3-a126-4a3f-83fe-f69e96c7717b
ms.openlocfilehash: f8898f76971b6088fa8ca831961ea7f12e1ab4e6
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65588843"
---
# <a name="datagridview-control-technology-summary-windows-forms"></a>DataGridView 컨트롤 기술 요약(Windows Forms)
이 항목에서는 `DataGridView` 제어 및 이를 사용하도록 지원하는 클래스에 대한 정보를 요약하여 설명합니다.  
  
 테이블 형식으로 데이터를 표시 해야 하는 자주 수행 될 가능성이 있는 경우 `DataGridView` 컨트롤은 그리드에서 데이터를 제공 하기 위한 완벽 한 솔루션을 되도록 설계 되었습니다.  
  
## <a name="keywords"></a>키워드  
 DataGridView, BindingSource, 테이블, 셀, 데이터 바인딩, 가상 모드  
  
## <a name="namespaces"></a>네임스페이스  
 <xref:System.Windows.Forms?displayProperty=nameWithType>  
  
 <xref:System.Data?displayProperty=nameWithType>  
  
## <a name="related-technologies"></a>관련 기술  
 `BindingSource`  
  
## <a name="background"></a>배경  
 사용자 인터페이스 (UI) 디자이너 자주 해야 할 사용자에 게 테이블 형식 데이터를 표시 합니다. .NET Framework에는 테이블 또는 그리드에서 데이터를 표시 하는 여러 방법을 제공 합니다. `DataGridView` 컨트롤은 Windows Forms 응용 프로그램에 대 한이 기술의 최신 진화를 나타냅니다.  
  
 `DataGridView` 컨트롤에서 행의 데이터 저장소에서 데이터를 표시할 수 있습니다. 다양 한 유형의 데이터 저장소 지원 됩니다. 데이터 저장소는 1 차원 배열과 같이 간단 하 고 형식화 되지 않은 데이터를 포함할 수 있거나 같은 형식화 된 데이터를 저장할 수는 <xref:System.Data.DataSet>합니다. 자세한 내용은 [방법: 바인딩 데이터는 Windows Forms DataGridView 컨트롤](how-to-bind-data-to-the-windows-forms-datagridview-control.md)합니다.  
  
 `DataGridView` 컨트롤에서는 데이터를 표 형식으로 표시하는 강력하고 유연한 방법을 제공합니다. 매우 큰 작은 데이터 집합의 읽기 전용 또는 편집할 수 있는 뷰를 표시할 컨트롤을 사용할 수 있습니다.  
  
 확장할 수 있습니다는 `DataGridView` 응용 프로그램에 사용자 지정 동작을 빌드하는 데 여러 가지 방법으로 제어 합니다. 예를 들어 프로그래밍 방식으로 고유한 정렬 알고리즘을 지정하고 고유한 셀 형식을 만들 수도 있습니다. 여러 속성 중에서 선택하여 `DataGridView` 컨트롤의 모양을 쉽게 사용자 지정할 수 있습니다. 다양 한 유형의 데이터 저장소를 데이터 원본으로 사용할 수 있습니다 또는 `DataGridView` 컨트롤에 바인딩된 데이터 소스 없이 작동할 수 있습니다.  
  
## <a name="implementing-datagridview-classes"></a>DataGridView 클래스 구현  
 여러 가지 방법으로 활용 하는 `DataGridView` 컨트롤의 확장 기능입니다. 이벤트와 속성을 통해 컨트롤의 다양 한 측면을 사용자 지정할 수 있지만 일부 사용자 지정을 사용 하면 기존 계획에서 파생 된 새 클래스를 만들려면 해야 `DataGridView` 클래스입니다.  
  
 가장 일반적으로 사용 되는 기본 클래스는 `DataGridViewCell` 고 `DataGridViewColumn`입니다. 고유한 셀 클래스를 파생 시킬 수 있습니다 `DataGridViewCell` 또는 해당 하위 클래스입니다. 모든 셀 형식 열에 추가할 수 있지만 일반적으로 클래스를 파생 도우미 열에서 `DataGridViewColumn` 기본적으로 사용자 지정 셀 형식의 셀을 호스팅하는 합니다.  
  
 구현할 수는 `IDataGridViewEditingCell` 편집 기능을 갖지만 편집 모드에서 컨트롤을 호스팅하지 않는 셀 형식을 만들 파생된 셀 클래스의 인터페이스입니다. 편집 모드의 셀에서 호스트할 수 있는 컨트롤을 만들려면 구현할 수 있습니다 합니다 `IDataGridViewEditingControl` 에서 파생 된 클래스에 인터페이스 <xref:System.Windows.Forms.Control>합니다.  
  
 자세한 내용은 [방법: 셀과 사용자 지정 동작 및 모양을 확장 하 여 열에는 Windows Forms DataGridView 컨트롤](customize-cells-and-columns-in-the-datagrid-by-extending-behavior.md) 고 [방법: DataGridView 셀에서 Windows Forms 컨트롤 호스팅](how-to-host-controls-in-windows-forms-datagridview-cells.md)합니다.  
  
## <a name="datagridview-classes-at-a-glance"></a>한 눈에 DataGridView 클래스  
 <xref:System.Windows.Forms>  
  
|기술 영역|클래스/인터페이스/구성 요소|  
|---------------------|-------------------------------------------------|  
|데이터 바인딩|<xref:System.Windows.Forms.BindingSource>|  
|데이터 표시|<xref:System.Windows.Forms.DataGridView><br /><br /> <xref:System.Windows.Forms.DataGridViewCell> 클래스와 파생된 클래스<br /><br /> <xref:System.Windows.Forms.DataGridViewRow> 클래스와 파생된 클래스<br /><br /> <xref:System.Windows.Forms.DataGridViewColumn> 클래스와 파생된 클래스<br /><br /> <xref:System.Windows.Forms.DataGridViewCellStyle>|  
|<xref:System.Windows.Forms.DataGridView> 확장성|<xref:System.Windows.Forms.DataGridViewCell> 클래스와 파생된 클래스<br /><br /> <xref:System.Windows.Forms.DataGridViewColumn> 클래스와 파생된 클래스<br /><br /> <xref:System.Windows.Forms.IDataGridViewEditingCell><br /><br /> <xref:System.Windows.Forms.IDataGridViewEditingControl>|  
  
## <a name="whats-new"></a>새로운 기능  
 <xref:System.Windows.Forms.DataGridView> 컨트롤은 Windows Forms를 사용 하 여 테이블 형식 데이터를 표시 하기 위한 완벽 한 솔루션을 되도록 설계 되었습니다. 사용을 고려해 야 합니다 <xref:System.Windows.Forms.DataGridView> 와 같은 다른 솔루션과 전에 제어 <xref:System.Windows.Forms.DataGrid>새 응용 프로그램을 제작 하는 경우. 자세한 내용은 [Windows Forms DataGridView 및 DataGrid 컨트롤의 차이점](differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)을 참조하십시오.  
  
 합니다 <xref:System.Windows.Forms.DataGridView> 제어와 함께에서 작업할 수는 <xref:System.Windows.Forms.BindingSource> 구성 요소입니다. 이 구성 요소는 폼의 기본 데이터 원본으로 설계 되었습니다. 간의 상호 작용을 관리할 수는 <xref:System.Windows.Forms.DataGridView> 제어 및 데이터에 관계 없이 해당 데이터 원본에 대 한 원본 유형입니다.  
  
## <a name="see-also"></a>참고자료

- [DataGridView 컨트롤 개요](datagridview-control-overview-windows-forms.md)
- [DataGridView 컨트롤 아키텍처](datagridview-control-architecture-windows-forms.md)
- [연결 정보 보호](../../data/adonet/protecting-connection-information.md)
