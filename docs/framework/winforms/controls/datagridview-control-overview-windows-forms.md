---
title: DataGridView 컨트롤 개요(Windows Forms)
ms.date: 03/30/2017
f1_keywords:
- DataGridView
helpviewer_keywords:
- DataGridView control [Windows Forms], about DataGridView control
- grid controls [Windows Forms]
- tables [Windows Forms], displaying in DataGridView control
- tables [Windows Forms], binding to DataGridView control
- columns [Windows Forms], DataGridView control
- bound controls [Windows Forms], dataGridView control
- datasets [Windows Forms], binding to DataGridView control
- data grids [Windows Forms], about data grids
- data [Windows Forms], resorting
- data [Windows Forms], navigating
- grids [Windows Forms]
- data binding [Windows Forms], DataGridView control
- data sources [Windows Forms], binding to DataGridView control
- DataGridView control [Windows Forms], data binding
ms.assetid: 0a45c661-89dc-4390-9cc6-c47eee501488
ms.openlocfilehash: 992bf57642c955a87cd7675e0bbe7c52131e8039
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69969144"
---
# <a name="datagridview-control-overview-windows-forms"></a>DataGridView 컨트롤 개요(Windows Forms)
> [!NOTE]
> <xref:System.Windows.Forms.DataGridView> 컨트롤은 <xref:System.Windows.Forms.DataGrid> 컨트롤을 대체하고 여기에 다른 기능을 추가하여 새로 도입된 컨트롤이지만 이전 버전과의 호환성 및 이후 사용 가능성을 고려하여 <xref:System.Windows.Forms.DataGrid> 컨트롤을 계속 유지하도록 선택할 수 있습니다. 자세한 내용은 [Windows Forms DataGridView 및 DataGrid 컨트롤의 차이점](differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)을 참조하십시오.  
  
 <xref:System.Windows.Forms.DataGridView> 컨트롤을 사용 하면 여러 종류의 데이터 원본에서 테이블 형식 데이터를 표시 하 고 편집할 수 있습니다.  
  
 데이터를 <xref:System.Windows.Forms.DataGridView> 컨트롤에 바인딩하는 것은 간단 하 고 직관적 이며 대부분의 경우 <xref:System.Windows.Forms.DataGridView.DataSource%2A> 속성을 설정 하는 것 만큼 간단 합니다. 여러 목록이 나 테이블을 포함 하는 데이터 원본에 바인딩하는 경우 바인딩할 목록 <xref:System.Windows.Forms.DataGridView.DataMember%2A> 또는 테이블을 지정 하는 문자열로 속성을 설정 합니다.  
  
 컨트롤 <xref:System.Windows.Forms.DataGridView> 은 표준 Windows Forms 데이터 바인딩 모델을 지원 하므로 다음 목록에서 설명 하는 클래스의 인스턴스에 바인딩합니다.  
  
- 1 차원 배열을 포함 하 <xref:System.Collections.IList> 여 인터페이스를 구현 하는 모든 클래스입니다.  
  
- <xref:System.ComponentModel.IListSource> 인터페이스를 구현 하는 클래스 (예: <xref:System.Data.DataTable> 및 <xref:System.Data.DataSet> 클래스)  
  
- 클래스와 같은 <xref:System.ComponentModel.IBindingList> 인터페이스를 구현 하는 클래스입니다. <xref:System.ComponentModel.BindingList%601>  
  
- 클래스와 같은 <xref:System.ComponentModel.IBindingListView> 인터페이스를 구현 하는 클래스입니다. <xref:System.Windows.Forms.BindingSource>  
  
 컨트롤 <xref:System.Windows.Forms.DataGridView> 은 반환 된 개체에서 구현 되는 경우 이러한 인터페이스 또는 <xref:System.ComponentModel.ICustomTypeDescriptor> 인터페이스에서 반환 된 속성 컬렉션에 의해 반환 되는 개체의 공용 속성에 대 한 데이터 바인딩을 지원 합니다.  
  
 일반적으로 바인딩할를 <xref:System.Windows.Forms.BindingSource> 구성 요소 및 바인딩은 <xref:System.Windows.Forms.BindingSource> 구성 요소를 다른 데이터 원본 또는 비즈니스 개체를 입력 합니다. <xref:System.Windows.Forms.BindingSource> 다양 한 데이터 원본에 바인딩할 수 있습니다 하 고 많은 데이터 바인딩 문제를 자동으로 해결할 수 있기 때문에 구성 요소는 기본 데이터 원본입니다. 자세한 내용은 [BindingSource 구성 요소](bindingsource-component.md)를 참조 하세요.  
  
 기본 데이터 저장소가 없는 *바인딩되지* 않은 모드 에서도 컨트롤을사용할수있습니다.<xref:System.Windows.Forms.DataGridView> 바인딩되지 <xref:System.Windows.Forms.DataGridView> 않은 컨트롤을 사용 하는 코드 예제를 보려면 [연습: 바인딩되지 않은 Windows Forms DataGridView 컨트롤](walkthrough-creating-an-unbound-windows-forms-datagridview-control.md)을 만듭니다.  
  
 컨트롤 <xref:System.Windows.Forms.DataGridView> 은 매우 구성 가능 하 고 확장 가능 하며 여러 속성, 메서드 및 이벤트를 제공 하 여 모양과 동작을 사용자 지정 합니다. Windows Forms 응용 프로그램에서 표 형식 데이터를 표시 하려면 다른 컨트롤 앞에 <xref:System.Windows.Forms.DataGridView> 컨트롤을 사용 하는 것이 <xref:System.Windows.Forms.DataGrid>좋습니다 (예:). 읽기 전용 값의 작은 그리드를 표시 하거나 사용자가 수백만 개의 레코드를 사용 하 여 테이블을 편집할 수 있도록 설정 하는 경우 컨트롤은 <xref:System.Windows.Forms.DataGridView> 쉽게 프로그래밍 가능 하 고 메모리를 효율적으로 사용할 수 있는 솔루션을 제공 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [DataGridView 컨트롤 기술 요약](datagridview-control-technology-summary-windows-forms.md)  
 컨트롤 <xref:System.Windows.Forms.DataGridView> 개념과 관련 클래스 사용을 요약 합니다.  
  
 [DataGridView 컨트롤 아키텍처](datagridview-control-architecture-windows-forms.md)  
 해당 형식 계층 구조 및 <xref:System.Windows.Forms.DataGridView> 상속 구조를 설명 하는 컨트롤의 아키텍처에 대해 설명 합니다.  
  
 [DataGridView 컨트롤 시나리오](datagridview-control-scenarios-windows-forms.md)  
 <xref:System.Windows.Forms.DataGridView> 컨트롤이 사용 되는 가장 일반적인 시나리오에 대해 설명 합니다.  
  
 [DataGridView 컨트롤 코드 디렉터리](datagridview-control-code-directory-windows-forms.md)  
 다양 <xref:System.Windows.Forms.DataGridView> 한 작업에 대 한 설명서의 코드 예제에 대 한 링크를 제공 합니다. 이러한 예제는 작업 형식별로 분류되어 제공됩니다.  
  
## <a name="related-sections"></a>관련 단원  
 [Windows Forms DataGridView 컨트롤의 열 형식](column-types-in-the-windows-forms-datagridview-control.md)  
 정보를 표시 하 고 사용자가 <xref:System.Windows.Forms.DataGridView> 정보를 수정 또는 추가할 수 있도록 하는 Windows Forms 컨트롤의 열 유형에 대해 설명 합니다.  
  
 [Windows Forms DataGridView 컨트롤에서 데이터 표시](displaying-data-in-the-windows-forms-datagridview-control.md)  
 수동으로 또는 외부 데이터 소스에서 컨트롤을 데이터로 채우는 방법을 설명하는 항목을 제공합니다.  
  
 [Windows Forms DataGridView 컨트롤 사용자 지정](customizing-the-windows-forms-datagridview-control.md)  
 <xref:System.Windows.Forms.DataGridView> 셀 및 행의 사용자 지정 그리기를 수행하고 파생된 셀, 열 및 행 형식을 설명하는 항목을 제공합니다.  
  
 [Windows Forms DataGridView 컨트롤의 성능 조정](performance-tuning-in-the-windows-forms-datagridview-control.md)  
 컨트롤을 효율적으로 사용하여 대용량 데이터를 사용할 때 성능 문제를 방지하는 방법을 설명하는 항목을 제공합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.BindingSource>
- [DataGridView 컨트롤](datagridview-control-windows-forms.md)
- [Windows Forms DataGridView 컨트롤의 기본 기능](default-functionality-in-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤에서의 기본 키보드 및 마우스 처리](default-keyboard-and-mouse-handling-in-the-windows-forms-datagridview-control.md)
