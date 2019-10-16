---
title: Windows Forms DataGridView 컨트롤의 셀 스타일
ms.date: 03/30/2017
helpviewer_keywords:
- DataGridView control [Windows Forms], cell styles
- cells [Windows Forms], styles
- data grids [Windows Forms], cell styles
ms.assetid: dbb75ed6-8804-4232-8382-f9920c2e380c
ms.openlocfilehash: be4c47db5c56685a84153a9ae4a9a2fe14c6adad
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69917762"
---
# <a name="cell-styles-in-the-windows-forms-datagridview-control"></a>Windows Forms DataGridView 컨트롤의 셀 스타일
<xref:System.Windows.Forms.DataGridView> 컨트롤에 있는 각 셀에는 텍스트 서식, 배경색, 전경색 및 글꼴과 같은 고유한 스타일을 사용할 수 있습니다. 그러나 일반적으로 여러 셀은 특정 스타일 특성을 공유 합니다.  
  
 스타일을 공유 하는 셀 그룹에는 특정 행 또는 열에 있는 모든 셀, 특정 값이 포함 된 모든 셀 또는 컨트롤의 모든 셀이 포함 될 수 있습니다. 이러한 그룹은 겹치기 때문에 각 셀의 스타일 정보를 둘 이상의 위치로 가져올 수 있습니다. 예를 들어, <xref:System.Windows.Forms.DataGridView> 컨트롤의 모든 셀이 동일한 글꼴을 사용 하 고 통화 열의 셀만 통화 형식을 사용 하 고 음수를 사용 하는 통화 셀만 빨강 전경색을 사용 하도록 할 수 있습니다.  
  
## <a name="the-datagridviewcellstyle-class"></a>DataGridViewCellStyle 클래스  
 <xref:System.Windows.Forms.DataGridViewCellStyle> 클래스에는 비주얼 스타일과 관련 된 다음 속성이 포함 되어 있습니다.  
  
- <xref:System.Windows.Forms.DataGridViewCellStyle.BackColor%2A> 및 <xref:System.Windows.Forms.DataGridViewCellStyle.ForeColor%2A>  
  
- <xref:System.Windows.Forms.DataGridViewCellStyle.SelectionBackColor%2A> 및 <xref:System.Windows.Forms.DataGridViewCellStyle.SelectionForeColor%2A>  
  
- <xref:System.Windows.Forms.DataGridViewCellStyle.Font%2A>  
  
 또한이 클래스에는 서식 지정과 관련 된 다음 속성이 포함 됩니다.  
  
- <xref:System.Windows.Forms.DataGridViewCellStyle.Format%2A> 및 <xref:System.Windows.Forms.DataGridViewCellStyle.FormatProvider%2A>  
  
- <xref:System.Windows.Forms.DataGridViewCellStyle.NullValue%2A> 및 <xref:System.Windows.Forms.DataGridViewCellStyle.DataSourceNullValue%2A>  
  
- <xref:System.Windows.Forms.DataGridViewCellStyle.WrapMode%2A>  
  
- <xref:System.Windows.Forms.DataGridViewCellStyle.Alignment%2A>  
  
- <xref:System.Windows.Forms.DataGridViewCellStyle.Padding%2A>  
  
 이러한 속성 및 다른 셀 스타일 속성에 대 한 자세한 내용은 아래의 참고 항목 <xref:System.Windows.Forms.DataGridViewCellStyle> 섹션에 나열 된 참조 설명서 및 항목을 참조 하십시오.  
  
## <a name="using-datagridviewcellstyle-objects"></a>DataGridViewCellStyle 개체 사용  
 <xref:System.Windows.Forms.DataGridView>, <xref:System.Windows.Forms.DataGridViewCellStyle> ,<xref:System.Windows.Forms.DataGridViewColumn>및클래스 의다양한속성및해당파생클래스에서개체를검색할수있습니다.<xref:System.Windows.Forms.DataGridViewCell> <xref:System.Windows.Forms.DataGridViewRow> 이러한 속성 중 하나를 아직 설정 하지 않은 경우 해당 값을 검색 하면 새 <xref:System.Windows.Forms.DataGridViewCellStyle> 개체가 만들어집니다. 또한 사용자 고유의 <xref:System.Windows.Forms.DataGridViewCellStyle> 개체를 인스턴스화하고 이러한 속성에 할당할 수 있습니다.  
  
 <xref:System.Windows.Forms.DataGridViewCellStyle> 여러<xref:System.Windows.Forms.DataGridView> 요소 간에 개체를 공유 하 여 스타일 정보가 불필요 하 게 중복 되는 것을 방지할 수 있습니다. 컨트롤, 열 및 행 수준에서 설정 된 스타일은 각 수준을 셀 수준까지 필터링 하기 때문에 위의 수준과 다른 각 수준의 스타일 속성만 설정 하 여 스타일 중복을 방지할 수도 있습니다. 이에 대해서는 다음에 나오는 스타일 상속 섹션에서 자세히 설명 합니다.  
  
 다음 표에서는 개체를 가져오거나 설정 <xref:System.Windows.Forms.DataGridViewCellStyle> 하는 기본 속성을 보여 줍니다.  
  
|속성|클래스|Description|  
|--------------|-------------|-----------------|  
|`DefaultCellStyle`|<xref:System.Windows.Forms.DataGridView>, <xref:System.Windows.Forms.DataGridViewColumn>,및파생클래스 <xref:System.Windows.Forms.DataGridViewRow>|머리글 셀을 포함 하 여 전체 컨트롤의 모든 셀, 열 또는 행에 사용 되는 기본 스타일을 가져오거나 설정 합니다.|  
|<xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A>|<xref:System.Windows.Forms.DataGridView>|컨트롤의 모든 행에 사용 되는 기본 셀 스타일을 가져오거나 설정 합니다. 머리글 셀은 포함 되지 않습니다.|  
|<xref:System.Windows.Forms.DataGridView.AlternatingRowsDefaultCellStyle%2A>|<xref:System.Windows.Forms.DataGridView>|컨트롤의 교대로 반복 되는 행에 사용 되는 기본 셀 스타일을 가져오거나 설정 합니다. 원장과 비슷한 효과를 만드는 데 사용 됩니다.|  
|<xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle%2A>|<xref:System.Windows.Forms.DataGridView>|컨트롤의 행 머리글에 사용 되는 기본 셀 스타일을 가져오거나 설정 합니다. 비주얼 스타일을 사용 하는 경우 현재 테마에 의해 재정의 됩니다.|  
|<xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle%2A>|<xref:System.Windows.Forms.DataGridView>|컨트롤의 열 머리글에 사용 되는 기본 셀 스타일을 가져오거나 설정 합니다. 비주얼 스타일을 사용 하는 경우 현재 테마에 의해 재정의 됩니다.|  
|<xref:System.Windows.Forms.DataGridViewCell.Style%2A>|<xref:System.Windows.Forms.DataGridViewCell>및 파생 클래스|셀 수준에서 지정 된 스타일을 가져오거나 설정 합니다. 이러한 스타일은 상위 수준에서 상속 된 스타일을 재정의 합니다.|  
|`InheritedStyle`|<xref:System.Windows.Forms.DataGridViewCell>, <xref:System.Windows.Forms.DataGridViewRow>,및파생클래스 <xref:System.Windows.Forms.DataGridViewColumn>|상위 수준에서 상속 된 스타일을 포함 하 여 셀, 행 또는 열에 현재 적용 된 스타일을 모두 가져옵니다.|  
  
 위에서 설명한 것 처럼 속성이 이전에 설정 되지 않은 경우 스타일 속성의 값 <xref:System.Windows.Forms.DataGridViewCellStyle> 을 가져오면 자동으로 새 개체가 인스턴스화됩니다. 이러한 개체를 불필요 하 게 만드는 것을 방지 하기 위해 행 및 <xref:System.Windows.Forms.DataGridViewBand.HasDefaultCellStyle%2A> 열 클래스에는 <xref:System.Windows.Forms.DataGridViewBand.DefaultCellStyle%2A> 속성이 설정 되었는지 여부를 확인 하는 데 사용할 수 있는 속성이 있습니다. 마찬가지로, 셀 클래스 <xref:System.Windows.Forms.DataGridViewCell.HasStyle%2A> 에는 <xref:System.Windows.Forms.DataGridViewCell.Style%2A> 속성이 설정 되었는지 여부를 나타내는 속성이 있습니다.  
  
 각 스타일 속성은 <xref:System.Windows.Forms.DataGridView> 컨트롤에 해당 하는 *PropertyName* `Changed` 이벤트를 포함 합니다. 행, 열 및 셀 속성의 경우`Row`이벤트의 이름은 "", "`Column`" 또는 "`Cell`"로 시작 됩니다 (예: <xref:System.Windows.Forms.DataGridView.RowDefaultCellStyleChanged>). 이러한 각 이벤트는 해당 스타일 속성이 다른 <xref:System.Windows.Forms.DataGridViewCellStyle> 개체로 설정 된 경우 발생 합니다. 이러한 이벤트는 스타일 속성에서 개체를 <xref:System.Windows.Forms.DataGridViewCellStyle> 검색 하 고 해당 속성 값을 수정할 때 발생 하지 않습니다. 셀 스타일 개체 자체의 변경 내용에 응답 하려면 <xref:System.Windows.Forms.DataGridView.CellStyleContentChanged> 이벤트를 처리 합니다.  
  
## <a name="style-inheritance"></a>스타일 상속  
 각 <xref:System.Windows.Forms.DataGridViewCell> 은 해당 <xref:System.Windows.Forms.DataGridViewCell.InheritedStyle%2A> 속성에서 모양을 가져옵니다. 이 <xref:System.Windows.Forms.DataGridViewCellStyle> 속성에서 반환 되는 개체는 형식의 <xref:System.Windows.Forms.DataGridViewCellStyle>속성 계층에서 해당 값을 상속 합니다. 이러한 속성은 머리글이 아닌 셀 <xref:System.Windows.Forms.DataGridViewCell.InheritedStyle%2A> 의가 해당 값을 가져오는 순서 대로 아래에 나열 되어 있습니다.  
  
1. <xref:System.Windows.Forms.DataGridViewCell.Style%2A?displayProperty=nameWithType>  
  
2. <xref:System.Windows.Forms.DataGridViewRow.DefaultCellStyle%2A?displayProperty=nameWithType>  
  
3. <xref:System.Windows.Forms.DataGridView.AlternatingRowsDefaultCellStyle%2A?displayProperty=nameWithType>(홀수 인덱스 번호가 있는 행의 셀에만 해당)  
  
4. <xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A?displayProperty=nameWithType>  
  
5. <xref:System.Windows.Forms.DataGridViewColumn.DefaultCellStyle%2A?displayProperty=nameWithType>  
  
6. <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=nameWithType>  
  
 행 및 열 머리글 셀의 경우 속성 <xref:System.Windows.Forms.DataGridViewCell.InheritedStyle%2A> 은 다음 원본 속성 목록에서 지정 된 순서로 값으로 채워집니다.  
  
1. <xref:System.Windows.Forms.DataGridViewCell.Style%2A?displayProperty=nameWithType>  
  
2. <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle%2A?displayProperty=nameWithType> 또는 <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle%2A?displayProperty=nameWithType>  
  
3. <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=nameWithType>  
  
 다음 다이어그램은이 프로세스를 보여 줍니다.  
  
 ![DataGridViewCellStyle 형식의 속성](./media/cell-styles-in-the-windows-forms-datagridview-control/datagridviewcells-inheritance-diagram.gif "DataGridViewCells 상속 다이어그램")  
  
 특정 행과 열에 의해 상속 되는 스타일에도 액세스할 수 있습니다. 열 <xref:System.Windows.Forms.DataGridViewColumn.InheritedStyle%2A> 속성은 다음 속성의 값을 상속 합니다.  
  
1. <xref:System.Windows.Forms.DataGridViewColumn.DefaultCellStyle%2A?displayProperty=nameWithType>  
  
2. <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=nameWithType>  
  
 Row <xref:System.Windows.Forms.DataGridViewRow.InheritedStyle%2A> 속성은 다음 속성에서 해당 값을 상속 합니다.  
  
1. <xref:System.Windows.Forms.DataGridViewRow.DefaultCellStyle%2A?displayProperty=nameWithType>  
  
2. <xref:System.Windows.Forms.DataGridView.AlternatingRowsDefaultCellStyle%2A?displayProperty=nameWithType>(홀수 인덱스 번호가 있는 행의 셀에만 해당)  
  
3. <xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A?displayProperty=nameWithType>  
  
4. <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=nameWithType>  
  
 속성에서 반환 `InheritedStyle` 하는 <xref:System.Windows.Forms.DataGridViewCellStyle> 개체의 각 속성에 대해 해당 속성이 <xref:System.Windows.Forms.DataGridViewCellStyle> 클래스 기본값 이외의 값으로 설정 된 적절 한 목록의 첫 번째 셀 스타일에서 속성 값을 가져옵니다.  
  
 다음 표에서는 예제 셀의 <xref:System.Windows.Forms.DataGridViewCellStyle.ForeColor%2A> 속성 값이 포함 하는 열에서 상속 되는 방법을 보여 줍니다.  
  
|형식의 속성`DataGridViewCellStyle`|검색 `ForeColor` 한 개체의 예제 값|  
|----------------------------------------------|----------------------------------------------------|  
|<xref:System.Windows.Forms.DataGridViewCell.Style%2A?displayProperty=nameWithType>|<xref:System.Drawing.Color.Empty?displayProperty=nameWithType>|  
|<xref:System.Windows.Forms.DataGridViewRow.DefaultCellStyle%2A?displayProperty=nameWithType>|<xref:System.Drawing.Color.Red%2A?displayProperty=nameWithType>|  
|<xref:System.Windows.Forms.DataGridView.AlternatingRowsDefaultCellStyle%2A?displayProperty=nameWithType>|<xref:System.Drawing.Color.Empty?displayProperty=nameWithType>|  
|<xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A?displayProperty=nameWithType>|<xref:System.Drawing.Color.Empty?displayProperty=nameWithType>|  
|<xref:System.Windows.Forms.DataGridViewColumn.DefaultCellStyle%2A?displayProperty=nameWithType>|<xref:System.Drawing.Color.DarkBlue%2A?displayProperty=nameWithType>|  
|<xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=nameWithType>|<xref:System.Drawing.Color.Black%2A?displayProperty=nameWithType>|  
  
 이 경우 <xref:System.Drawing.Color.Red%2A?displayProperty=nameWithType> 셀의 행에 있는 값은 목록의 첫 번째 값입니다. 이 값은 <xref:System.Windows.Forms.DataGridViewCellStyle.ForeColor%2A> <xref:System.Windows.Forms.DataGridViewCell.InheritedStyle%2A>셀의 속성 값이 됩니다.  
  
 다음 다이어그램에서는 다양 <xref:System.Windows.Forms.DataGridViewCellStyle> 한 속성이 다른 위치에서 해당 값을 상속 하는 방법을 보여 줍니다.  
  
 ![DataGridView 속성&#45;값 상속](./media/cell-styles-in-the-windows-forms-datagridview-control/datagridviewcells-value-inheritance-diagram.gif "DataGridViewCells 값 상속 다이어그램")  
  
 스타일 상속을 활용 하 여 여러 위치에서 동일한 정보를 지정 하지 않고도 전체 컨트롤에 대 한 적절 한 스타일을 제공할 수 있습니다.  
  
 설명 된 대로 머리글 셀이 스타일 상속에 참여 하지만 <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle%2A> <xref:System.Windows.Forms.DataGridView> 컨트롤의 및 <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle%2A> 속성에서 반환 되는 개체에는에서 반환 된 개체의 속성 값을 재정의 하는 초기 속성 값이 있습니다. <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A> 속성입니다. <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A> 속성에서 반환 하는 개체에 대해 속성을 설정 하 여 행 및 열 머리글에 적용 하려면 <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle%2A> 및 <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle%2A> 속성이 반환 하는 개체의 해당 속성을 표시 된 기본값으로 설정 해야 합니다. <xref:System.Windows.Forms.DataGridViewCellStyle> 클래스에 대 한입니다.  
  
> [!NOTE]
> 비주얼 스타일을 사용 하는 경우를 제외 <xref:System.Windows.Forms.DataGridView.TopLeftHeaderCell%2A>하 고 행 및 열 머리글은 현재 테마에 따라 자동으로 스타일이 지정 되어 이러한 속성으로 지정 된 스타일을 재정의 합니다.  
  
 , 및 형식은 열 속성<xref:System.Windows.Forms.DataGridViewColumn.DefaultCellStyle%2A> 에 의해 반환 되는 개체의 일부 값도 초기화 합니다. <xref:System.Windows.Forms.DataGridViewCheckBoxColumn> <xref:System.Windows.Forms.DataGridViewButtonColumn> <xref:System.Windows.Forms.DataGridViewImageColumn> 자세한 내용은 해당 형식에 대 한 참조 설명서를 참조 하세요.  
  
## <a name="setting-styles-dynamically"></a>동적으로 스타일 설정  
 특정 값을 사용 하 여 셀 스타일을 사용자 지정 하려면 <xref:System.Windows.Forms.DataGridView.CellFormatting?displayProperty=nameWithType> 이벤트에 대 한 처리기를 구현 합니다. 이 이벤트에 대 한 처리기는 <xref:System.Windows.Forms.DataGridViewCellFormattingEventArgs> 형식의 인수를 받습니다. 이 개체에는 <xref:System.Windows.Forms.DataGridView> 컨트롤의 해당 위치와 함께 형식이 지정 되는 셀의 값을 확인할 수 있는 속성이 포함 되어 있습니다. 또한이 개체는 형식이 <xref:System.Windows.Forms.DataGridViewCellFormattingEventArgs.CellStyle%2A> 지정 되는 셀의 <xref:System.Windows.Forms.DataGridViewCell.InheritedStyle%2A> 속성 값으로 초기화 되는 속성을 포함 합니다. 셀 스타일 속성을 수정 하 여 셀 값 및 위치에 적합 한 스타일 정보를 지정할 수 있습니다.  
  
> [!NOTE]
> 또한 <xref:System.Windows.Forms.DataGridView.RowPrePaint> 및 <xref:System.Windows.Forms.DataGridView.RowPostPaint> 이벤트는 이벤트 데이터 <xref:System.Windows.Forms.DataGridViewCellStyle> 에서 개체를 수신 하지만, 해당 하는 경우 읽기 전용 용도의 행 <xref:System.Windows.Forms.DataGridViewRow.InheritedStyle%2A> 속성의 복사본 이며, 컨트롤에 영향을 주지 않습니다.  
  
 <xref:System.Windows.Forms.DataGridView.CellMouseEnter?displayProperty=nameWithType> 및 이벤트와 같은 이벤트에 대 한 <xref:System.Windows.Forms.DataGridView.CellMouseLeave> 응답으로 개별 셀의 스타일을 동적으로 수정할 수도 있습니다. 예를 들어 <xref:System.Windows.Forms.DataGridView.CellMouseEnter> 이벤트 처리기에서 셀의 <xref:System.Windows.Forms.DataGridViewCell.Style%2A> 속성을 통해 검색 되는 셀 배경색의 현재 값을 저장 한 다음 마우스로 가리킬 때 셀을 강조 표시 하는 새 색으로 설정할 수 있습니다. <xref:System.Windows.Forms.DataGridView.CellMouseLeave> 이벤트에 대 한 처리기에서 배경색을 원래 값으로 복원할 수 있습니다.  
  
> [!NOTE]
> 특정 스타일 값의 설정 여부에 관계 <xref:System.Windows.Forms.DataGridViewCell.Style%2A> 없이 셀의 속성에 저장 된 값을 캐시 하는 것이 중요 합니다. 스타일 설정을 일시적으로 바꾸면 원래 "설정 안 함" 상태로 복원 하면 셀이 상위 수준에서 스타일 설정을 상속 하는 것으로 돌아갑니다. 스타일이 상속 되었는지 여부에 관계 없이 셀에 적용 되는 실제 스타일을 결정 해야 하는 경우 셀의 <xref:System.Windows.Forms.DataGridViewCell.InheritedStyle%2A> 속성을 사용 합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridViewCellStyle>
- <xref:System.Windows.Forms.DataGridView.AlternatingRowsDefaultCellStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewBand.InheritedStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewRow.InheritedStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewColumn.InheritedStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewBand.DefaultCellStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewCell.InheritedStyle%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewCell.Style%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.CellFormatting?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.CellStyleContentChanged?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.RowPrePaint?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.RowPostPaint?displayProperty=nameWithType>
- [Windows Forms DataGridView 컨트롤의 기본 형식 및 스타일 지정](basic-formatting-and-styling-in-the-windows-forms-datagridview-control.md)
- [방법: Windows Forms DataGridView 컨트롤에 기본 셀 스타일 설정](how-to-set-default-cell-styles-for-the-windows-forms-datagridview-control.md)
- [Windows Forms DataGridView 컨트롤의 데이터 형식 지정](data-formatting-in-the-windows-forms-datagridview-control.md)
