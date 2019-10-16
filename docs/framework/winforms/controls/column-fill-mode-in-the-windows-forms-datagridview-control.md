---
title: Windows Forms DataGridView 컨트롤의 열 채우기 모드
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data grids [Windows Forms], automatically resizing columns
- DataGridView control [Windows Forms], column fill mode
- data grids [Windows Forms], column fill mode
ms.assetid: b4ef7411-ebf4-4e26-bb33-aecec90de80c
ms.openlocfilehash: f9eb45e9b96ccb97938c7396d177ccedbea329e6
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65590372"
---
# <a name="column-fill-mode-in-the-windows-forms-datagridview-control"></a>Windows Forms DataGridView 컨트롤의 열 채우기 모드
열 채우기 모드에는 <xref:System.Windows.Forms.DataGridView> 컨트롤이 사용 가능한 표시 영역의 너비를 채우도록 열 크기를 자동으로 조정합니다. 각 열의 너비를 해당 <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A> 속성 값과 같거나 더 크게 유지해야 하는 경우 컨트롤이 가로 스크롤 막대를 표시하지 않습니다.  
  
 각 열의 크기 조정 동작은 해당 <xref:System.Windows.Forms.DataGridViewColumn.InheritedAutoSizeMode%2A> 속성에 따라 달라집니다. 이 속성의 값은 컨트롤의 <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A> 속성 또는 열 값이 <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode.NotSet>(기본값)인 경우 컨트롤의 <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A> 속성에서 상속됩니다.  
  
 각 열에서 서로 다른 크기 모드를 사용할 수 있지만 크기 모드가 <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode.Fill>인 열은 다른 열에서 사용되지 않는 표시 영역 너비를 공유합니다. 이 너비는 <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> 속성 값에 비례하여 채우기 모드 열 간에 나눠집니다. 예를 들어 두 열의 <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> 값이 각각 100과 200인 경우 첫 번째 열은 두 번째 열 너비의 절반입니다.  
  
## <a name="user-resizing-in-fill-mode"></a>채우기 모드에서 사용자 크기 조정  
 셀 내용에 따라 크기를 조정하는 크기 조정 모드와 달리, 채우기 모드에서는 <xref:System.Windows.Forms.DataGridViewColumn.Resizable%2A> 속성 값이 `true`인 열의 크기를 사용자가 조정할 수 있습니다. 사용자가 채우기 모드 열의 크기를 조정하는 경우 크기가 조정된 열 뒤의 모든 채우기 모드 열(<xref:System.Windows.Forms.Control.RightToLeft%2A>가 `false`이면 오른쪽에 있는 열, 그러지 않으면 왼쪽에 있는 열)도 사용 가능한 너비 변경을 보정하기 위해 크기가 조정됩니다. 크기가 조정된 열 뒤에 채우기 모드 열이 없는 경우 보정을 위해 컨트롤의 다른 모든 채우기 모드 열의 크기가 조정됩니다. 컨트롤에 다른 채우기 모드 열이 없는 경우 크기 조정이 무시됩니다. 채우기 모드가 아닌 열의 크기를 조정하는 경우 보정을 위해 컨트롤의 모든 채우기 모드 열의 크기가 변경됩니다.  
  
 채우기 모드 열의 크기를 조정한 후 변경된 모든 열의 <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> 값이 비례해서 조정됩니다. 예를 들어 채우기 모드 열 4개의 <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> 값이 100인 경우 두 번째 열의 크기를 원래 너비의 절반으로 조정하면 <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> 값은 100, 50, 125, 125가 됩니다. 채우기 모드가 아닌 열의 크기를 조정하는 경우 채우기 모드 열이 동일한 비율을 유지하면서 크기가 조정되어 보정하기 때문에 <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> 값이 변경되지 않습니다.  
  
## <a name="content-based-fillweight-adjustment"></a>콘텐츠 기반 FillWeight 조정  
 <xref:System.Windows.Forms.DataGridView.AutoResizeColumns%2A> 메서드와 같은 <xref:System.Windows.Forms.DataGridView> 자동 크기 조정 메서드를 사용하여 채우기 모드 열에 대한 <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> 값을 초기화할 수 있습니다. 이 메서드는 먼저 열에서 콘텐츠를 표시하는 데 필요한 너비를 계산합니다. 그런 다음 비율이 계산된 너비의 비율과 일치하도록 컨트롤이 모든 채우기 모드 열의 <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> 값을 조정합니다. 끝으로, 컨트롤의 모든 열이 사용 가능한 가로 공간을 채우도록 컨트롤이 새로운 <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> 비율을 사용하여 채우기 모드 열의 크기를 조정합니다.  
  
## <a name="example"></a>예제  
  
### <a name="description"></a>설명  
 <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A>, <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A>, <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> 및 <xref:System.Windows.Forms.DataGridViewColumn.Resizable%2A> 속성에 적합한 값을 사용하여 다양한 시나리오에 대한 열 크기 조정 동작을 사용자 지정할 수 있습니다.  
  
 다음 데모 코드를 통해 다양한 열의 <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A>, <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> 및 <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A> 속성에 대해 다른 값을 실험할 수 있습니다. 이 예제에서 <xref:System.Windows.Forms.DataGridView> 컨트롤은 고유한 <xref:System.Windows.Forms.DataGridView.Columns%2A> 컬렉션에 바인딩되고 <xref:System.Windows.Forms.DataGridViewColumn.HeaderText%2A>, <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A>, <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A>, <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A> 및 <xref:System.Windows.Forms.DataGridViewColumn.Width%2A> 속성에 각각 하나의 열이 바인딩됩니다. 또한 각 열은 컨트롤에서 하나의 행으로 표시되고, 행의 값을 변경하면 해당 열의 속성이 업데이트되므로 값이 상호 작용하는 방식을 확인할 수 있습니다.  
  
### <a name="code"></a>코드  
 [!code-csharp[System.Windows.Forms.DataGridViewFillColumnsDemo#00](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewFillColumnsDemo/CS/fillcolumns.cs#00)]
 [!code-vb[System.Windows.Forms.DataGridViewFillColumnsDemo#00](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewFillColumnsDemo/vb/fillcolumns.vb#00)]  
  
### <a name="comments"></a>설명  
 이 데모 애플리케이션을 사용하려면 다음을 수행합니다.  
  
- 폼 크기를 변경합니다. <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> 속성 값으로 지정된 비율을 유지하면서 열의 너비가 어떻게 변경되는지 관찰합니다.  
  
- 마우스로 열 구분선을 끌어서 열 크기를 변경합니다. <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> 값이 어떻게 변경되는지 관찰합니다.  
  
- 한 열의 <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A> 값을 변경한 다음 폼을 끌어서 크기를 조정합니다. 폼을 충분히 작게 만들 때 <xref:System.Windows.Forms.DataGridViewColumn.Width%2A> 값이 어떻게 <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A> 값 아래로 내려가지 않는지 관찰합니다.  
  
- 더한 값이 컨트롤의 너비를 초과하도록 모든 열의 <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A> 값을 큰 숫자로 변경합니다. 가로 스크롤 막대가 어떻게 나타나는지 관찰합니다.  
  
- 일부 열의 <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A> 값을 변경합니다. 열이나 폼의 크기를 조정할 때의 효과를 관찰합니다.  
  
## <a name="compiling-the-code"></a>코드 컴파일  
 이 예제에는 다음 사항이 필요합니다.  
  
- System, System.Drawing 및 System.Windows.Forms 어셈블리에 대한 참조  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridView.AutoResizeColumns%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewAutoSizeColumnsMode>
- <xref:System.Windows.Forms.DataGridViewColumn>
- <xref:System.Windows.Forms.DataGridViewColumn.InheritedAutoSizeMode%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode>
- <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewColumn.Width%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DataGridViewColumn.Resizable%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.Control.RightToLeft%2A?displayProperty=nameWithType>
- [Windows Forms DataGridView 컨트롤의 열 및 행 크기 조정](resizing-columns-and-rows-in-the-windows-forms-datagridview-control.md)
