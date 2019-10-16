---
ms.openlocfilehash: 2413e1997b6e729b9d5889677e25254aaa24afea
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67859269"
---
### <a name="incorrect-implementation-of-memberdescriptorequals"></a>MemberDescriptor.Equals의 잘못된 구현

|   |   |
|---|---|
|세부 정보|<xref:System.ComponentModel.MemberDescriptor.Equals%2A?displayProperty=nameWithType> 메서드의 원래 구현은 비교되는 개체의 두 가지 문자열 속성을 비교합니다. 즉, 범주 이름과 설명 문자열입니다. 수정은 첫 번째 개체의 <xref:System.ComponentModel.MemberDescriptor.Category>를 두 번째의 <xref:System.ComponentModel.MemberDescriptor.Category>와 비교하고, 첫 번째의 <xref:System.ComponentModel.MemberDescriptor.Description>을 두 번째의 <xref:System.ComponentModel.MemberDescriptor.Description>과 비교하는 것입니다.|
|제안|애플리케이션이 <xref:System.ComponentModel.MemberDescriptor.Equals%2A?displayProperty=nameWithType>에 종속되어 있고 설명자가 동일할 때 <code>false</code>를 반환하는 경우 및 .NET Framework 4.6.2 이상 버전을 대상으로 하는 경우에 몇 가지 옵션이 있습니다.<ol><li><xref:System.ComponentModel.MemberDescriptor.Equals%2A?displayProperty=nameWithType> 메서드를 호출하는 것 외에도 <xref:System.ComponentModel.MemberDescriptor.Category> 및 <xref:System.ComponentModel.MemberDescriptor.Description> 필드를 수동으로 비교하도록 코드를 변경합니다.</li><li>app.config 파일에 다음 값을 추가하여 이러한 변경 내용을 옵트아웃합니다.</li></ol><pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.MemberDescriptorEqualsReturnsFalseIfEquivalent=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>애플리케이션이 .NET Framework 4.6.1 이하를 대상으로 하고 .NET Framework 4.6.2 이상에서 실행되는 경우 이 변경 내용을 활성화하려면 app.config 파일에 다음 값을 추가하여 호환성 스위치를 <code>false</code>로 설정하면 됩니다.<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.MemberDescriptorEqualsReturnsFalseIfEquivalent=false&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>|
|범위|Microsoft Edge|
|버전|4.6.2|
|형식|대상 변경|
|영향을 받는 API|<ul><li><xref:System.ComponentModel.MemberDescriptor.Equals(System.Object)?displayProperty=nameWithType></li></ul>|

