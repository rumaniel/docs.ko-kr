---
title: DataGridView 컨트롤 아키텍처(Windows Forms)
ms.date: 03/30/2017
helpviewer_keywords:
- DataGridView control [Windows Forms], architecture
ms.assetid: 1c6cabf0-02ee-4bbc-9574-b54bb7f5b19e
ms.openlocfilehash: 15d10ed2ec0bc78acfe887fe583d4850425eeab9
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64648105"
---
# <a name="datagridview-control-architecture-windows-forms"></a>DataGridView 컨트롤 아키텍처(Windows Forms)
<xref:System.Windows.Forms.DataGridView> 컨트롤과 관련 된 클래스는 테이블 형식 데이터 표시 및 편집에 대 한 유연 하 고 확장 가능한 시스템을 하도록 설계 되었습니다. 이러한 클래스에 포함 된 모든는 <xref:System.Windows.Forms?displayProperty=nameWithType> 네임 스페이스 및 이러한 모든 "DataGridView" 접두사를 사용 하 여 이름이 됩니다.  
  
## <a name="architecture-elements"></a>아키텍처 요소  
 주 <xref:System.Windows.Forms.DataGridView> 도우미 클래스에서 파생 <xref:System.Windows.Forms.DataGridViewElement>합니다. 다음 개체 모델을 보여 줍니다는 <xref:System.Windows.Forms.DataGridViewElement> 상속 계층 구조입니다.  
  
 ![DataGridViewElement 개체 모델 계층 구조를 보여 주는 다이어그램입니다.](./media/datagridview-control-architecture-windows-forms/datagridviewelement-object-model.gif)  
  
 <xref:System.Windows.Forms.DataGridViewElement> 클래스는 부모에 대 한 참조를 제공 <xref:System.Windows.Forms.DataGridView> 제어 하 고이 <xref:System.Windows.Forms.DataGridViewElement.State%2A> 속성에서 값의 조합을 나타내는 값을 보유 하는 <xref:System.Windows.Forms.DataGridViewElementStates> 열거형.  
  
 다음 섹션에서는 <xref:System.Windows.Forms.DataGridView> 도우미 자세히 클래스입니다.  
  
### <a name="datagridviewelementstates"></a>DataGridViewElementStates  
 <xref:System.Windows.Forms.DataGridViewElementStates> 열거형 다음 값을 포함 합니다.  
  
- <xref:System.Windows.Forms.DataGridViewElementStates.None>  
  
- <xref:System.Windows.Forms.DataGridViewElementStates.Frozen>  
  
- <xref:System.Windows.Forms.DataGridViewElementStates.ReadOnly>  
  
- <xref:System.Windows.Forms.DataGridViewElementStates.Resizable>  
  
- <xref:System.Windows.Forms.DataGridViewElementStates.ResizableSet>  
  
- <xref:System.Windows.Forms.DataGridViewElementStates.Selected>  
  
- <xref:System.Windows.Forms.DataGridViewElementStates.Visible>  
  
 이 열거형의 값 비트 논리 연산자를 함께 사용할 수 있으므로 <xref:System.Windows.Forms.DataGridViewElement.State%2A> 속성은 둘 이상의 상태를 한 번에 표현할 수 있습니다. 예를 들어, 한 <xref:System.Windows.Forms.DataGridViewElement> 동시에 사용할 수 있습니다 <xref:System.Windows.Forms.DataGridViewElementStates.Frozen>, <xref:System.Windows.Forms.DataGridViewElementStates.Selected>, 및 <xref:System.Windows.Forms.DataGridViewElementStates.Visible>.  
  
### <a name="cells-and-bands"></a>셀 및 밴드  
 <xref:System.Windows.Forms.DataGridView> 컨트롤 구성 개체의 두 가지 기본적인 종류: 셀 및 밴드입니다. 모든 셀에서 파생 된 <xref:System.Windows.Forms.DataGridViewCell> 기본 클래스입니다. 두 종류의 밴드 <xref:System.Windows.Forms.DataGridViewColumn> 하 고 <xref:System.Windows.Forms.DataGridViewRow>에서 파생 되는 <xref:System.Windows.Forms.DataGridViewBand> 기본 클래스.  
  
 합니다 <xref:System.Windows.Forms.DataGridView> 여러 클래스와 상호 운용 제어 되지만 가장 일반적으로 발생 <xref:System.Windows.Forms.DataGridViewCell>를 <xref:System.Windows.Forms.DataGridViewColumn>, 및 <xref:System.Windows.Forms.DataGridViewRow>합니다.  
  
### <a name="datagridviewcell"></a>DataGridViewCell  
 셀이에 대 한 상호 작용의 기본 단위는 <xref:System.Windows.Forms.DataGridView>합니다. 표시는 셀을 중심으로 하 고 데이터 항목은 대개 셀을 통해 수행 됩니다. 사용 하 여 셀에 액세스할 수 있습니다는 <xref:System.Windows.Forms.DataGridViewRow.Cells%2A> 의 컬렉션을 <xref:System.Windows.Forms.DataGridViewRow> 클래스를 사용 하 여 선택한 셀에 액세스할 수는 <xref:System.Windows.Forms.DataGridView.SelectedCells%2A> 의 컬렉션은 <xref:System.Windows.Forms.DataGridView> 컨트롤입니다. 다음 개체 모델이이 사용법을 보여 줍니다 및 표시를 <xref:System.Windows.Forms.DataGridViewCell> 상속 계층 구조입니다.  
  
 ![DataGridViewCell 개체 모델 계층 구조를 보여 주는 다이어그램입니다.](./media/datagridview-control-architecture-windows-forms/datagridviewcell-object-model.gif)  
  
 <xref:System.Windows.Forms.DataGridViewCell> 유형 셀 형식도 파생 되는 추상 기본 클래스입니다. <xref:System.Windows.Forms.DataGridViewCell> 및 Windows Forms 컨트롤, 하지만 일부 호스트 Windows Forms 컨트롤 파생된 형식에 해당 되지 않습니다. 셀에서 지 원하는 모든 편집 기능은 호스트 된 컨트롤에서 일반적으로 처리 됩니다.  
  
 <xref:System.Windows.Forms.DataGridViewCell> 개체 제어 하지 않습니다 고유한 모양과 그리기 기능 동일한 방식으로 Windows Forms 컨트롤로. 대신 합니다 <xref:System.Windows.Forms.DataGridView> 모양의 담당 해당 <xref:System.Windows.Forms.DataGridViewCell> 개체입니다. 상호 작용 하 여 셀의 동작과 모양을 향상 시킬 수 있습니다는 <xref:System.Windows.Forms.DataGridView> 컨트롤의 속성 및 이벤트입니다. 사용자 지정 기능에 대 한 특별 한 요구 사항이 있는 경우는 <xref:System.Windows.Forms.DataGridView> 컨트롤에서 파생 되는 고유한 클래스를 구현할 수 있습니다 <xref:System.Windows.Forms.DataGridViewCell> 또는 해당 자식 클래스 중 하나입니다.  
  
 다음 목록에서 파생 된 클래스를 보여 줍니다. <xref:System.Windows.Forms.DataGridViewCell>:  
  
- <xref:System.Windows.Forms.DataGridViewTextBoxCell>  
  
- <xref:System.Windows.Forms.DataGridViewButtonCell>  
  
- <xref:System.Windows.Forms.DataGridViewLinkCell>  
  
- <xref:System.Windows.Forms.DataGridViewCheckBoxCell>  
  
- <xref:System.Windows.Forms.DataGridViewComboBoxCell>  
  
- <xref:System.Windows.Forms.DataGridViewImageCell>  
  
- <xref:System.Windows.Forms.DataGridViewHeaderCell>  
  
- <xref:System.Windows.Forms.DataGridViewRowHeaderCell>  
  
- <xref:System.Windows.Forms.DataGridViewColumnHeaderCell>  
  
- <xref:System.Windows.Forms.DataGridViewTopLeftHeaderCell>  
  
- 사용자 지정 셀 형식  
  
### <a name="datagridviewcolumn"></a>DataGridViewColumn  
 스키마를 <xref:System.Windows.Forms.DataGridView> 제어의 연결 된 데이터 저장소로 표현 됩니다는 <xref:System.Windows.Forms.DataGridView> 컨트롤의 열입니다. 액세스할 수 있습니다 합니다 <xref:System.Windows.Forms.DataGridView> 를 사용 하 여 컨트롤의 열을 <xref:System.Windows.Forms.DataGridView.Columns%2A> 컬렉션입니다. 사용 하 여 선택한 열에 액세스할 수 있습니다는 <xref:System.Windows.Forms.DataGridView.SelectedColumns%2A> 컬렉션입니다. 다음 개체 모델이이 사용법을 보여 줍니다 및 표시를 <xref:System.Windows.Forms.DataGridViewColumn> 상속 계층 구조입니다.  
  
 ![DataGridViewColumn 개체 모델 계층 구조를 보여 주는 다이어그램입니다.](./media/datagridview-control-architecture-windows-forms/datagridviewcolumn-object-model.gif)  
  
 키 셀 형식 중 일부에 해당 열 형식이 있습니다. 파생 된 이러한는 <xref:System.Windows.Forms.DataGridViewColumn> 기본 클래스입니다.  
  
 다음 목록에서 파생 된 클래스를 보여 줍니다. <xref:System.Windows.Forms.DataGridViewColumn>:  
  
- <xref:System.Windows.Forms.DataGridViewButtonColumn>  
  
- <xref:System.Windows.Forms.DataGridViewCheckBoxColumn>  
  
- <xref:System.Windows.Forms.DataGridViewComboBoxColumn>  
  
- <xref:System.Windows.Forms.DataGridViewImageColumn>  
  
- <xref:System.Windows.Forms.DataGridViewTextBoxColumn>  
  
- <xref:System.Windows.Forms.DataGridViewLinkColumn>  
  
- 사용자 지정 열 형식  
  
### <a name="datagridview-editing-controls"></a>DataGridView 편집 컨트롤  
 고급 편집 기능을 일반적으로 지원 되는 셀 Windows Forms 컨트롤에서 파생 되는 호스트 된 컨트롤을 사용 합니다. 이러한 컨트롤을 구현할 수도 <xref:System.Windows.Forms.IDataGridViewEditingControl> 인터페이스입니다. 다음 개체 모델에서는 이러한 컨트롤의 사용을 보여 줍니다.  
  
 ![DataGridView 편집 컨트롤 개체 모델 계층을 보여 주는 다이어그램입니다.](./media/datagridview-control-architecture-windows-forms/datagridviewediting-object-model.gif)  
  
 다음과 같은 편집 컨트롤을 함께 제공 되는 <xref:System.Windows.Forms.DataGridView> 제어 합니다.  
  
- <xref:System.Windows.Forms.DataGridViewComboBoxEditingControl>  
  
- <xref:System.Windows.Forms.DataGridViewTextBoxEditingControl>  
  
 고유한 편집 컨트롤을 만드는 방법에 대 한 자세한 내용은 [방법: DataGridView 셀에서 Windows Forms 컨트롤 호스팅](how-to-host-controls-in-windows-forms-datagridview-cells.md)합니다.  
  
 다음 표에서 셀 형식, 열 형식 및 편집 컨트롤 간의 관계를 보여 줍니다.  
  
|셀 형식|호스팅된 컨트롤|열 유형|  
|---------------|--------------------|-----------------|  
|<xref:System.Windows.Forms.DataGridViewButtonCell>|N/A|<xref:System.Windows.Forms.DataGridViewButtonColumn>|  
|<xref:System.Windows.Forms.DataGridViewCheckBoxCell>|N/A|<xref:System.Windows.Forms.DataGridViewCheckBoxColumn>|  
|<xref:System.Windows.Forms.DataGridViewComboBoxCell>|<xref:System.Windows.Forms.DataGridViewComboBoxEditingControl>|<xref:System.Windows.Forms.DataGridViewComboBoxColumn>|  
|<xref:System.Windows.Forms.DataGridViewImageCell>|N/A|<xref:System.Windows.Forms.DataGridViewImageColumn>|  
|<xref:System.Windows.Forms.DataGridViewLinkCell>|N/A|<xref:System.Windows.Forms.DataGridViewLinkColumn>|  
|<xref:System.Windows.Forms.DataGridViewTextBoxCell>|<xref:System.Windows.Forms.DataGridViewTextBoxEditingControl>|<xref:System.Windows.Forms.DataGridViewTextBoxColumn>|  
  
### <a name="datagridviewrow"></a>DataGridViewRow  
 <xref:System.Windows.Forms.DataGridViewRow> 저장소에 있는 데이터에서 레코드의 데이터 필드 클래스 표시는 <xref:System.Windows.Forms.DataGridView> 컨트롤이 연결 되어 있습니다. 액세스할 수 있습니다 합니다 <xref:System.Windows.Forms.DataGridView> 사용 하 여 컨트롤의 행을 <xref:System.Windows.Forms.DataGridView.Rows%2A> 컬렉션입니다. 사용 하 여 선택한 행에 액세스할 수 있습니다는 <xref:System.Windows.Forms.DataGridView.SelectedRows%2A> 컬렉션입니다. 다음 개체 모델이이 사용법을 보여 줍니다 및 표시를 <xref:System.Windows.Forms.DataGridViewRow> 상속 계층 구조입니다.  
  
 ![DataGridViewRow 개체 모델 계층 구조를 보여 주는 다이어그램입니다.](./media/datagridview-control-architecture-windows-forms/datagridviewrow-object-model.gif)
  
 사용자 고유의 형식을 파생 시킬 수 있습니다는 <xref:System.Windows.Forms.DataGridViewRow> 클래스를이 일반적으로 필요가 없습니다. 합니다 <xref:System.Windows.Forms.DataGridView> 컨트롤에 행 관련 이벤트 및 동작을 사용자 지정에 대 한 속성 몇 가지 해당 <xref:System.Windows.Forms.DataGridViewRow> 개체입니다.  
  
 사용 하는 경우는 <xref:System.Windows.Forms.DataGridView> 컨트롤의 <xref:System.Windows.Forms.DataGridView.AllowUserToAddRows%2A> 속성을 새 행을 추가 하기 위한 특별 한 행이 마지막 행으로 나타납니다. 이 행의 일부인는 <xref:System.Windows.Forms.DataGridView.Rows%2A> 컬렉션 하지만 주의가 필요할 수 있는 특별 한 기능이 있습니다. 자세한 내용은 [Windows Forms DataGridView 컨트롤에서 새 레코드에 대 한 행을 사용 하 여](using-the-row-for-new-records-in-the-windows-forms-datagridview-control.md)입니다.  
  
## <a name="see-also"></a>참고자료

- [DataGridView 컨트롤 개요](datagridview-control-overview-windows-forms.md)
- [Windows Forms DataGridView 컨트롤 사용자 지정](customizing-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤에서 새 레코드에 행 사용](using-the-row-for-new-records-in-the-windows-forms-datagridview-control.md)
