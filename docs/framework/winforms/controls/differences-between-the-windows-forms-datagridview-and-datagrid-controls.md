---
title: Windows Forms DataGridView 및 DataGrid 컨트롤 간의 차이점
ms.date: 03/30/2017
helpviewer_keywords:
- data grids [Windows Forms
- DataGrid control [Windows Forms], DataGridView control compared
- DataGridView control [Windows Forms], DataGrid control compared
ms.assetid: d412c786-140e-4210-8a56-a68467530a55
ms.openlocfilehash: 6802ef375d8d15826725e68f5065317192523178
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61972213"
---
# <a name="differences-between-the-windows-forms-datagridview-and-datagrid-controls"></a>Windows Forms DataGridView 및 DataGrid 컨트롤 간의 차이점
합니다 <xref:System.Windows.Forms.DataGridView> 컨트롤은 대체 하는 새 컨트롤을 <xref:System.Windows.Forms.DataGrid> 컨트롤입니다. 합니다 <xref:System.Windows.Forms.DataGridView> 컨트롤에서 누락 된 다양 한 기본 및 고급 기능을 제공 합니다 <xref:System.Windows.Forms.DataGrid> 제어 합니다. 또한 아키텍처는 <xref:System.Windows.Forms.DataGridView> 컨트롤을 사용 하면 훨씬 쉽게 확장 및 보다 사용자 지정할 수는 <xref:System.Windows.Forms.DataGrid> 제어 합니다.  
  
 다음 표에에서 제공 되는 기본 기능 중 몇 가지는 <xref:System.Windows.Forms.DataGridView> 컨트롤에서 누락 된는 <xref:System.Windows.Forms.DataGrid> 컨트롤입니다.  
  
|DataGridView 컨트롤의 기능|설명|  
|----------------------------------|-----------------|  
|여러 열 형식|합니다 <xref:System.Windows.Forms.DataGridView> 컨트롤은 보다 더 많은 기본 제공 열 형식을 제공 합니다 <xref:System.Windows.Forms.DataGrid> 제어 합니다. 이러한 열 유형에 가장 일반적인 시나리오의 요구 사항을 충족 하지만 훨씬 용이 하 게 확장 하거나 대체의 열 형식 보다는 <xref:System.Windows.Forms.DataGrid> 제어 합니다. 자세한 내용은 [Windows Forms DataGridView 컨트롤의 열 형식](column-types-in-the-windows-forms-datagridview-control.md)합니다.|  
|여러 가지 방법으로 데이터를 표시 하려면|<xref:System.Windows.Forms.DataGrid> 컨트롤은 외부 데이터 원본에서 데이터 표시를 제한 합니다. 하지만 <xref:System.Windows.Forms.DataGridView> 제어 데이터를 표시할 수 바인딩되지 않은 컨트롤, 바인딩된 데이터 원본에서 데이터 또는 바인딩 및 바인딩 해제 된 데이터에 함께 저장 합니다. 가상 모드를 구현할 수도 있습니다는 <xref:System.Windows.Forms.DataGridView> 컨트롤 사용자 지정 데이터 관리를 제공 합니다. 자세한 내용은 [Windows Forms DataGridView 컨트롤의 데이터 디스플레이 모드](data-display-modes-in-the-windows-forms-datagridview-control.md)합니다.|  
|데이터 표시를 사용자 지정 하는 여러 방법|<xref:System.Windows.Forms.DataGridView> 컨트롤은 많은 속성 및 데이터 형식 및 표시 방법을 지정할 수 있도록 이벤트를 제공 합니다. 예를 들어, 셀, 행 및 열에 포함 된 데이터에 따라 모양을 변경할 수 있습니다 하거나 다른 형식의 해당 하는 데이터를 사용 하 여 특정 데이터 형식의 데이터를 바꿀 수 있습니다. 자세한 내용은 [Windows Forms DataGridView 컨트롤에서 데이터 형식](data-formatting-in-the-windows-forms-datagridview-control.md)합니다.|  
|셀, 행, 열 및 머리글 모양 및 동작을 변경 하기 위한 여러 옵션|<xref:System.Windows.Forms.DataGridView> 컨트롤을 사용 하면 다양 한 방법으로 개별 grid 구성 요소를 사용 하 여 사용할 수 있습니다. 예를 들어, 행 및 스크롤; 않도록 열을 고정할 수 있습니다. 행, 열 및 머리글 숨기기 행, 열 및 헤더 크기를 조정 하는;으로 변경 사용자가 선택을;으로 변경 및 개별 셀, 행 및 열에 대 한 도구 설명 및 바로 가기 메뉴를 제공 합니다.|  
  
 <xref:System.Windows.Forms.DataGrid> 특별 한 요구 사항 및 이전 버전과 호환성에 대 한 제어 유지 됩니다. 거의 모든 용도로 사용 해야는 <xref:System.Windows.Forms.DataGridView> 제어 합니다. 사용할 수 있는 기능만 합니다 <xref:System.Windows.Forms.DataGrid> 컨트롤에서 사용할 수 없는 <xref:System.Windows.Forms.DataGridView> 컨트롤은 단일 컨트롤에 두 개의 관련된 테이블에서 정보 계층 구조로 표시 합니다. 두 개를 사용 해야 <xref:System.Windows.Forms.DataGridView> 마스터/세부 관계에 있는 두 테이블의에서 정보를 표시 하는 컨트롤입니다.  
  
## <a name="upgrading-to-the-datagridview-control"></a>DataGridView 컨트롤에서로 업그레이드  
 기존 응용 프로그램을 사용 하는 경우는 <xref:System.Windows.Forms.DataGrid> 컨트롤에서 사용자 지정 하지 않고 간단한 데이터 바인딩 시나리오를 대체할 수 있습니다 단순히 이전 컨트롤 새 컨트롤을 사용 하 여 합니다. 두 컨트롤 모두에 표준 Windows Forms 데이터 바인딩 아키텍처를 사용 하므로 <xref:System.Windows.Forms.DataGridView> 컨트롤 추가 구성이 필요 없는 사용 하 여 바인딩된 데이터 표시 됩니다. 그러나 데이터를 바인딩하여 데이터 바인딩 기능 향상,을 활용 하는 것이 좋습니다. 하려는 <xref:System.Windows.Forms.BindingSource> 에 바인딩할 수 있습니다 하는 구성 요소는 <xref:System.Windows.Forms.DataGridView> 제어 합니다. 자세한 내용은 [BindingSource 구성 요소](bindingsource-component.md)합니다.  
  
 때문에 <xref:System.Windows.Forms.DataGridView> 컨트롤에 완전히 새로운 아키텍처를 사용할 수 있도록 간단 하 게 변환 경로가 없는 <xref:System.Windows.Forms.DataGrid> 사용 하 여 사용자 지정을 <xref:System.Windows.Forms.DataGridView> 제어 합니다. 그러나 많은 <xref:System.Windows.Forms.DataGrid> 사용자 지정이 필요 하지는 <xref:System.Windows.Forms.DataGridView> 새 컨트롤에서 사용할 수 있는 기본 제공 기능으로 인해 제어 합니다. 에 대 한 사용자 지정 열 형식을 만든 경우는 <xref:System.Windows.Forms.DataGrid> 컨트롤을 사용 하는 <xref:System.Windows.Forms.DataGridView> 새로운 아키텍처를 사용 하 여 다시 구현 해야 제어 합니다. 자세한 내용은 [Windows Forms DataGridView 컨트롤 사용자 지정](customizing-the-windows-forms-datagridview-control.md)합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGrid>
- <xref:System.Windows.Forms.BindingSource>
- [DataGridView 컨트롤](datagridview-control-windows-forms.md)
- [DataGrid 컨트롤](datagrid-control-windows-forms.md)
- [BindingSource 구성 요소](bindingsource-component.md)
- [Windows Forms DataGridView 컨트롤의 열 형식](column-types-in-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤의 셀 스타일](cell-styles-in-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤의 데이터 디스플레이 모드](data-display-modes-in-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤의 데이터 형식 지정](data-formatting-in-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤의 크기 조정 옵션](sizing-options-in-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤의 열 정렬 모드](column-sort-modes-in-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤의 선택 모드](selection-modes-in-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤 사용자 지정](customizing-the-windows-forms-datagridview-control.md)
