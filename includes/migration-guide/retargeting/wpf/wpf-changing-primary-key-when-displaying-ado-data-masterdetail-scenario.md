---
ms.openlocfilehash: 2cd107dc92fd0fae89717c38840ce7ea44f3ac9a
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59774083"
---
### <a name="wpf-changing-a-primary-key-when-displaying-ado-data-in-a-masterdetail-scenario"></a>마스터/세부 정보 시나리오에서 ADO 데이터를 표시할 때 기본 키를 변경하는 WPF

|   |   |
|---|---|
|세부 정보|<code>Order</code> 형식 항목의 ADO 컬렉션이 있고 기본 키 &quot;OrderID&quot;를 통해 ADO 컬렉션을 <code>Detail</code> 형식 항목의 컬렉션에 연결하는 &quot;OrderDetails&quot;라는 관계가 있다고 가정합니다. WPF 앱에서 목록 컨트롤을 지정된 순서에 대한 세부 정보에 바인딩할 수 있습니다.<pre><code class="lang-xml">&lt;ListBox ItemsSource=&quot;{Binding Path=OrderDetails}&quot; &gt;&#13;&#10;</code></pre>DataContext가 <code>Order</code>인 경우. WPF는 <code>OrderDetails</code> 속성의 값(<code>OrderID</code>가 마스터 항목의 <code>OrderID</code>와 일치하는 모든 <code>Detail</code> 항목의 컬렉션 D)을 가져옵니다. 마스터 항목의 기본 키 <code>OrderID</code>를 변경하면 동작이 변경됩니다. ADO는 세부 정보 컬렉션에 있는 영향을 받는 각 레코드(컬렉션 D로 복사된 레코드)의 <code>OrderID</code>를 자동으로 변경합니다.  하지만 D는 어떻게 처리될까요?<ul><li>이전 동작:   컬렉션 D가 지워집니다.   마스터 항목이 <code>OrderDetails</code> 속성에 대한 변경 알림을 표시하지 <em>않습니다</em>.  ListBox가 현재 비어 있는 컬렉션 D를 계속 사용합니다.</li><li>새 동작:  컬렉션 D가 변경되지 않습니다.   각 항목이 <code>OrderID</code> 속성에 대한 변경 알림을 표시합니다.  ListBox가 컬렉션 D를 계속 사용하고 새 <code>OrderID</code>와 함께 세부 정보를 표시합니다.</li></ul>WPF는 <code>followParent</code> 인수를 <code>true</code>로 설정하고 ADO 메서드 <xref:System.Data.DataRowView.CreateChildView(System.Data.DataRelation,System.Boolean)?displayProperty=nameWithType>를 호출하는 다른 방법으로 컬렉션 D를 만들어 새 동작을 구현합니다.|
|제안 해결 방법|앱은 다음 AppContext 스위치를 사용하여 새 동작을 가져옵니다.<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.Data.DoNotUseFollowParentWhenBindingToADODataRelation=false&quot;/&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;&#13;&#10;</code></pre>스위치는 기본적으로 .NET 4.7.1 이하를 대상으로 하는 앱의 경우 <code>true</code>(이전 동작)로 설정되고, .NET 4.7.2 이상을 대상으로 하는 앱의 경우 <code>false</code>(새 동작)로 설정됩니다.|
|범위|부|
|버전|4.7.2|
|형식|대상 변경|
