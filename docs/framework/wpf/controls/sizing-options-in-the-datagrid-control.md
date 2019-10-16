---
title: DataGrid 컨트롤의 크기 조정 옵션
ms.date: 03/30/2017
helpviewer_keywords:
- DataGrid control [WPF], sizing
- size [WPF], DataGrid
- automatically size DataGrid [WPF]
ms.assetid: 96a0e47e-b010-4302-98ef-2daac446d8db
ms.openlocfilehash: 6d100fb17b1ee3e652985a637d333d9f65e20d36
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61970991"
---
# <a name="sizing-options-in-the-datagrid-control"></a>DataGrid 컨트롤의 크기 조정 옵션
다양 한 옵션을 제어할 수 있는 방법을 <xref:System.Windows.Controls.DataGrid> 크기가 자동으로 조정 합니다. 합니다 <xref:System.Windows.Controls.DataGrid>, 및 개별 행과 열에는 <xref:System.Windows.Controls.DataGrid>, 해당 콘텐츠를 자동으로 크기를 설정할 수 있습니다 또는 특정 값으로 설정할 수 있습니다. 기본적으로 <xref:System.Windows.Controls.DataGrid> 증가 및 해당 내용의 크기에 맞게 축소 됩니다.  
  
## <a name="sizing-the-datagrid"></a>DataGrid 크기 조정  
  
### <a name="cautions-when-using-automatic-sizing"></a>자동 크기 조정 사용 시 주의 사항  
 기본적으로 <xref:System.Windows.FrameworkElement.Height%2A> 및 <xref:System.Windows.FrameworkElement.Width%2A> 의 속성을 <xref:System.Windows.Controls.DataGrid> 으로 설정 됩니다 <xref:System.Double.NaN?displayProperty=nameWithType> ("`Auto`" XAML에서), 및 <xref:System.Windows.Controls.DataGrid> 해당 내용의 크기에 따라 조정 됩니다.  
  
 와 같은 해당 자식의 크기를 제한 하지 않는 컨테이너 안에 배치 되는 경우는 <xref:System.Windows.Controls.Canvas> 나 <xref:System.Windows.Controls.StackPanel>, <xref:System.Windows.Controls.DataGrid> 컨테이너의 표시 경계를 넘어서 연장 됩니다 및 스크롤 막대가 표시 되지 것입니다. 이 조건에 모두 유용성 및 성능 영향을 줍니다.  
  
 경우 데이터 집합에 바인딩된 경우 합니다 <xref:System.Windows.FrameworkElement.Height%2A> 의 <xref:System.Windows.Controls.DataGrid> 가 바인딩된 데이터 집합의 각 데이터 항목에 대 한 행을 추가 하려면 계속 제한 되지 않습니다. 이 인해 발생할 수 있습니다는 <xref:System.Windows.Controls.DataGrid> 행 추가 됨에 따라 응용 프로그램의 표시 경계를 벗어나 성장할 수 있습니다. 합니다 <xref:System.Windows.Controls.DataGrid> 는 스크롤 막대 여기서 때문에 표시 하지 해당 <xref:System.Windows.FrameworkElement.Height%2A> 새 행을 수용 하기 위해 확장을 계속 합니다.  
  
 개체의 각 행에 대해 만들어집니다는 <xref:System.Windows.Controls.DataGrid>합니다. 큰 데이터 집합을 사용 하는 경우 및 허용 하는 <xref:System.Windows.Controls.DataGrid> 자동으로 크기를 자동으로, 많은 수의 개체 생성 응용 프로그램의 성능이 저하 될 수 있습니다.  
  
 큰 데이터 집합을 사용 하 여 작업할 때 이러한 문제를 방지, 것이 좋습니다 구체적으로 설정 하는 합니다 <xref:System.Windows.FrameworkElement.Height%2A> 의 <xref:System.Windows.Controls.DataGrid> 제한 하는 컨테이너에 배치 또는 해당 <xref:System.Windows.FrameworkElement.Height%2A>와 같은 <xref:System.Windows.Controls.Grid>합니다. 경우는 <xref:System.Windows.FrameworkElement.Height%2A> 액세스가 제한 합니다 <xref:System.Windows.Controls.DataGrid> 맞춰 지정 된 행만 만들어집니다 <xref:System.Windows.FrameworkElement.Height%2A>, 새 데이터를 표시 하는 데 필요한 대로 행을 재활용 합니다.  
  
### <a name="setting-the-datagrid-size"></a>DataGrid 크기 설정  
 합니다 <xref:System.Windows.Controls.DataGrid> 자동으로 크기를 지정 된 경계 내에서 설정할 수 있습니다 또는 <xref:System.Windows.Controls.DataGrid> 특정 크기를 설정할 수 있습니다. 다음 표에서 컨트롤을 설정할 수 있는 속성은 <xref:System.Windows.Controls.DataGrid> 크기입니다.  
  
|속성|설명|  
|--------------|-----------------|  
|<xref:System.Windows.FrameworkElement.Height%2A>|에 대 한 특정 높이 설정 합니다 <xref:System.Windows.Controls.DataGrid>합니다.|  
|<xref:System.Windows.FrameworkElement.MaxHeight%2A>|높이 대 한 상한을 설정 합니다 <xref:System.Windows.Controls.DataGrid>합니다. <xref:System.Windows.Controls.DataGrid> 이 높이 도달할 때까지 세로로 확장 됩니다.|  
|<xref:System.Windows.FrameworkElement.MinHeight%2A>|높이 대 한 하한값을 설정 합니다 <xref:System.Windows.Controls.DataGrid>합니다. <xref:System.Windows.Controls.DataGrid> 이 높이 도달할 때까지 세로로 축소 됩니다.|  
|<xref:System.Windows.FrameworkElement.Width%2A>|에 대 한 특정 너비로 설정 된 <xref:System.Windows.Controls.DataGrid>합니다.|  
|<xref:System.Windows.FrameworkElement.MaxWidth%2A>|너비에 대 한 상한을 설정 합니다 <xref:System.Windows.Controls.DataGrid>합니다. <xref:System.Windows.Controls.DataGrid> 이 너비에 도달할 때까지 가로로 늘어납니다.|  
|<xref:System.Windows.FrameworkElement.MinWidth%2A>|너비에 대 한 하한값을 설정 합니다 <xref:System.Windows.Controls.DataGrid>합니다. <xref:System.Windows.Controls.DataGrid> 이 너비에 도달할 때까지 가로로 줄어듭니다.|  
  
## <a name="sizing-rows-and-row-headers"></a>행 및 행 머리글 크기 조정  
  
### <a name="datagrid-rows"></a>DataGrid 행  
 기본적으로 <xref:System.Windows.Controls.DataGrid> 행의 <xref:System.Windows.FrameworkElement.Height%2A> 속성이로 설정 되어 <xref:System.Double.NaN?displayProperty=nameWithType> ("`Auto`" XAML에서), 행 높이가 해당 내용의 크기를 확장 합니다. 모든 행의 높이 <xref:System.Windows.Controls.DataGrid> 설정 하 여 지정할 수는 <xref:System.Windows.Controls.DataGrid.RowHeight%2A?displayProperty=nameWithType> 속성입니다. 사용자는 행 머리글 구분선을 끌어 행 높이 변경할 수 있습니다.  
  
### <a name="datagrid-row-headers"></a>DataGrid 행 머리글  
 행 머리글을 표시 하는 <xref:System.Windows.Controls.DataGrid.HeadersVisibility%2A> 속성으로 설정 되어 있어야 <xref:System.Windows.Controls.DataGridHeadersVisibility.Row?displayProperty=nameWithType> 또는 <xref:System.Windows.Controls.DataGridHeadersVisibility.All?displayProperty=nameWithType>합니다. 기본적으로 행 머리글이 표시 되 고 자동으로 해당 콘텐츠에 맞게 크기입니다. 행 머리글을 설정 하 여 특정 너비를 지정할 수 있습니다는 <xref:System.Windows.Controls.DataGrid.RowHeaderWidth%2A?displayProperty=nameWithType> 속성입니다.  
  
## <a name="sizing-columns-and-column-headers"></a>열 및 열 머리글을 크기 조정  
  
### <a name="datagrid-columns"></a>DataGrid 열  
 합니다 <xref:System.Windows.Controls.DataGrid> 값을 사용 합니다 <xref:System.Windows.Controls.DataGridLength> 및 <xref:System.Windows.Controls.DataGridLengthUnitType> 절대 또는 자동 크기 조정 모드를 지정 하는 구조입니다.  
  
 다음 표에서에서 제공 하는 값은 <xref:System.Windows.Controls.DataGridLengthUnitType> 구조입니다.  
  
|이름|설명|  
|----------|-----------------|  
|<xref:System.Windows.Controls.DataGridLengthUnitType.Auto>|기본 모드 크기 조정 자동 <xref:System.Windows.Controls.DataGrid> 열 셀 및 열 머리글의 내용에 기반 합니다.|  
|<xref:System.Windows.Controls.DataGridLengthUnitType.SizeToCells>|셀 기반 자동 크기 모드를 크기 조정 <xref:System.Windows.Controls.DataGrid> 열 머리글을 포함 하지 않고 열에서 셀의 내용에 기반 합니다.|  
|<xref:System.Windows.Controls.DataGridLengthUnitType.SizeToHeader>|머리글 기반 자동 크기 모드를 크기 조정 <xref:System.Windows.Controls.DataGrid> 열만 열 머리글의 내용에 기반 합니다.|  
|<xref:System.Windows.Controls.DataGridLengthUnitType.Pixel>|픽셀 기반 모드 크기 조정 <xref:System.Windows.Controls.DataGrid> 제공 된 숫자 값을 기준으로 하는 열입니다.|  
|<xref:System.Windows.Controls.DataGridLengthUnitType.Star>|별 크기 조정 모드를 가중치에 따라 사용 가능한 공간을 배포에 사용 됩니다.<br /><br /> XAML을 별표 값은 n * 여기서 n 나타냅니다 숫자 값으로 표현 됩니다. 1\* 같습니다 \*합니다. 예를 들어, 두 경우의 열을 <xref:System.Windows.Controls.DataGrid> 너비가 \* 2 및\*, 첫 번째 열을 수신할 사용 가능한 공간에의 한 부분 및 두 번째 열에는 두 개의 부분 사용 가능한 공간을 받게 됩니다.|  
  
 합니다 <xref:System.Windows.Controls.DataGridLengthConverter> 클래스를 사용 하 여 숫자 또는 문자열 값 사이 데이터를 변환할 수 있습니다 및 <xref:System.Windows.Controls.DataGridLength> 값입니다.  
  
 기본적으로 <xref:System.Windows.Controls.DataGrid.ColumnWidth%2A?displayProperty=nameWithType> 속성이 <xref:System.Windows.Controls.DataGridLength.SizeToHeader%2A>, 및 <xref:System.Windows.Controls.DataGridColumn.Width%2A?displayProperty=nameWithType> 속성이 <xref:System.Windows.Controls.DataGridLength.Auto%2A>합니다. 크기 조정 모드를로 설정 되 면 <xref:System.Windows.Controls.DataGridLength.Auto%2A> 또는 <xref:System.Windows.Controls.DataGridLength.SizeToCells%2A>, 광범위 한 표시 콘텐츠 너비 열 커집니다. 스크롤할 때 이러한 크기 조정 모드 하면 콘텐츠 인 경우 확장할 열을 뷰로 스크롤 된 현재 열 크기 보다 큽니다. 콘텐츠 보기에서 스크롤 된 후에 열 축소 되지 않습니다.  
  
 열에는 <xref:System.Windows.Controls.DataGrid> 지정 된 경계 내 에서만 자동으로 크기를 설정할 수도 있습니다 또는 특정 크기에 열을 설정할 수 있습니다. 다음 표에서 열 크기를 제어를 설정할 수 있는 속성을 보여줍니다.  
  
|속성|설명|  
|--------------|-----------------|  
|<xref:System.Windows.Controls.DataGrid.MaxColumnWidth%2A?displayProperty=nameWithType>|모든 열에 대 한 상한을 설정 합니다 <xref:System.Windows.Controls.DataGrid>합니다.|  
|<xref:System.Windows.Controls.DataGridColumn.MaxWidth%2A?displayProperty=nameWithType>|개별 열에 대 한 상한을 설정 합니다. <xref:System.Windows.Controls.DataGrid.MaxColumnWidth%2A?displayProperty=nameWithType>를 재정의합니다.|  
|<xref:System.Windows.Controls.DataGrid.MinColumnWidth%2A?displayProperty=nameWithType>|설정의 모든 열에 대 한 하한값을 <xref:System.Windows.Controls.DataGrid>입니다.|  
|<xref:System.Windows.Controls.DataGridColumn.MinWidth%2A?displayProperty=nameWithType>|개별 열에 대 한 하한값을 설정합니다. <xref:System.Windows.Controls.DataGrid.MinColumnWidth%2A?displayProperty=nameWithType>를 재정의합니다.|  
|<xref:System.Windows.Controls.DataGrid.ColumnWidth%2A?displayProperty=nameWithType>|모든 열에 대 한 특정 너비로 설정 된 <xref:System.Windows.Controls.DataGrid>합니다.|  
|<xref:System.Windows.Controls.DataGridColumn.Width%2A?displayProperty=nameWithType>|개별 열에 대 한 특정 너비를 설정 합니다. <xref:System.Windows.Controls.DataGrid.ColumnWidth%2A?displayProperty=nameWithType>를 재정의합니다.|  
  
### <a name="datagrid-column-headers"></a>DataGrid 열 머리글  
 기본적으로 <xref:System.Windows.Controls.DataGrid> 열 머리글이 표시 됩니다. 열 머리글을 숨기려면 합니다 <xref:System.Windows.Controls.DataGrid.HeadersVisibility%2A> 속성으로 설정 되어 있어야 <xref:System.Windows.Controls.DataGridHeadersVisibility.Row?displayProperty=nameWithType> 또는 <xref:System.Windows.Controls.DataGridHeadersVisibility.None?displayProperty=nameWithType>합니다. 기본적으로 열 머리글에 표시 되는 경우 자동으로 크기가 해당 내용에 맞게 합니다. 열 머리글을 설정 하 여 특정 높이 지정할 수 있습니다는 <xref:System.Windows.Controls.DataGrid.ColumnHeaderHeight%2A?displayProperty=nameWithType> 속성입니다.  
  
### <a name="resizing-with-the-mouse"></a>마우스를 사용 하 여 크기 조정  
 사용자가 크기를 조정할 수 <xref:System.Windows.Controls.DataGrid> 행과 행 또는 열 머리글 구분선을 끌어서 열입니다. <xref:System.Windows.Controls.DataGrid> 행 또는 열 머리글 구분선을 두 번 클릭 하 여 행 및 열 자동 크기 조정도 지원 합니다. 사용자 특정 열의 크기를 조정 하지 못하도록 설정 합니다 <xref:System.Windows.Controls.DataGridColumn.CanUserResize%2A?displayProperty=nameWithType> 속성을 `false` 개별 열에 대 한 합니다. 사용자가 모든 열의 크기를 조정 하지 못하도록 설정 합니다 <xref:System.Windows.Controls.DataGrid.CanUserResizeColumns%2A?displayProperty=nameWithType> 속성을 `false`입니다. 사용자가 모든 행의 크기를 조정 하지 못하도록 설정 합니다 <xref:System.Windows.Controls.DataGrid.CanUserResizeRows%2A?displayProperty=nameWithType> 속성을 `false`입니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Controls.DataGrid>
- <xref:System.Windows.Controls.DataGridColumn>
- <xref:System.Windows.Controls.DataGridLength>
- <xref:System.Windows.Controls.DataGridLengthConverter>
