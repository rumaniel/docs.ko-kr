---
ms.openlocfilehash: 4e81087431091dfa4d5432d5ea5e2b665be2b130
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59774403"
---
### <a name="listtforeach-can-throw-exception-when-modifying-list-item"></a>List\<T>.ForEach는 목록 항목을 수정할 때 예외를 throw할 수 있음

|   |   |
|---|---|
|세부 정보|.NET Framework 4.5부터는 호출 컬렉션의 요소가 수정되면 <xref:System.Collections.Generic.List%601.ForEach(System.Action{%600})> 열거자가 <xref:System.InvalidOperationException?displayProperty=name> 예외를 throw합니다. 이전에는 예외를 throw하지 않고 경합 상태가 발생할 수 있었습니다.|
|제안 해결 방법|이상적으로, 안전한 작업을 위해 요소를 열거하는 동안 목록을 수정하지 않도록 코드를 수정해야 합니다. 그러나 이전 동작으로 되돌리려면 응용 프로그램이 .NET Framework 4.0을 대상으로 할 수 있습니다.|
|범위|Microsoft Edge|
|버전|4.5|
|형식|대상 변경|
|영향을 받는 API|<ul><li><xref:System.Collections.Generic.List%601.ForEach(System.Action{%600})?displayProperty=nameWithType></li></ul>|
