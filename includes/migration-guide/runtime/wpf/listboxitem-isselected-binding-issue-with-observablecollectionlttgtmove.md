---
ms.openlocfilehash: 44cb833fc93caaa79000147421e1c013f755b9cb
ms.sourcegitcommit: 4d8efe00f2e5ab42e598aff298d13b8c052d9593
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68238010"
---
### <a name="listboxitem-isselected-binding-issue-with-observablecollectionlttgtmove"></a>ObservableCollection&lt;T&gt;.Move의 ListBoxItem IsSelected 바인딩 문제

|   |   |
|---|---|
|세부 정보|선택한 항목을 사용하여 <xref:System.Windows.Controls.ListBox?displayProperty=name>에 바인딩된 컬렉션에서 <xref:System.Collections.ObjectModel.ObservableCollection%601.Move(System.Int32,System.Int32)> 또는 <xref:System.Collections.ObjectModel.ObservableCollection%601.MoveItem(System.Int32,System.Int32)>을 호출하면 이후에 <xref:System.Windows.Controls.ListBox?displayProperty=name> 항목을 선택하거나 선택 취소할 때 비정상적인 동작이 발생할 수 있습니다.|
|제안 해결 방법|<xref:System.Collections.ObjectModel.ObservableCollection%601.Move(System.Int32,System.Int32)> 대신 <xref:System.Collections.ObjectModel.Collection%601.Remove(%600)?displayProperty=name> 및 <xref:System.Collections.ObjectModel.Collection%601.Insert(System.Int32,%600)?displayProperty=name>을 호출하면 이 문제가 해결됩니다. 또는 .NET Framework 4.6에서 이 문제가 수정되어 해당 버전의 .NET Framework로 업그레이드하여 해결할 수 있습니다.|
|범위|부|
|버전|4.5|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Collections.ObjectModel.ObservableCollection%601.Move(System.Int32,System.Int32)?displayProperty=nameWithType></li><li><xref:System.Collections.ObjectModel.ObservableCollection%601.MoveItem(System.Int32,System.Int32)?displayProperty=nameWithType></li></ul>|
