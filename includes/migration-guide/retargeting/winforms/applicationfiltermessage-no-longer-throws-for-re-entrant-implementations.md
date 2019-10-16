---
ms.openlocfilehash: 8e37007318a55188d44607fd5e4c4f3950c105df
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67804327"
---
### <a name="applicationfiltermessage-no-longer-throws-for-re-entrant-implementations-of-imessagefilterprefiltermessage"></a>Application.FilterMessage는 IMessageFilter.PreFilterMessage의 재진입 구현에 대해 더 이상 throw하지 않음

|   |   |
|---|---|
|세부 정보|.NET Framework 4.6.1에 앞서 <xref:System.Windows.Forms.Application.AddMessageFilter(System.Windows.Forms.IMessageFilter)?displayProperty=name> 또는 <xref:System.Windows.Forms.Application.RemoveMessageFilter(System.Windows.Forms.IMessageFilter)?displayProperty=name>라고 하는 <xref:System.Windows.Forms.IMessageFilter.PreFilterMessage(System.Windows.Forms.Message@)>를 사용하여 <xref:System.Windows.Forms.Application.FilterMessage(System.Windows.Forms.Message@)>을 호출하면(<xref:System.Windows.Forms.Application.DoEvents>도 호출하면서) <xref:System.IndexOutOfRangeException?displayProperty=name>을 발생시킵니다.<p/>4\.6.1.NET Framework를 대상으로 하는 애플리케이션부터 이 예외는 더 이상 throw되지 않으며 위에서 설명한 것처럼 재진입 필터가 사용될 수 있습니다.|
|제안|위에서 설명한 재진입 <xref:System.Windows.Forms.IMessageFilter.PreFilterMessage(System.Windows.Forms.Message@)> 동작 때문에 <xref:System.Windows.Forms.Application.FilterMessage(System.Windows.Forms.Message@)>가 더 이상 throw되지 않습니다. 이는 .NET Framework 4.6.1을 대상으로 하는 애플리케이션에만 영향을 줍니다. .NET Framework 4.6.1을 대상으로 하는 애플리케이션은 [DontSupportReentrantFilterMessage](~/docs/framework/migration-guide/mitigation-custom-imessagefilter-prefiltermessage-implementations.md#mitigation) 호환성 스위치를 사용하여 이 변경을 옵트아웃(또는 이전 프레임워크를 대상으로 하는 애플리케이션은 옵트인)할 수 있습니다.|
|범위|Microsoft Edge|
|버전|4.6.1|
|형식|대상 변경|
|영향을 받는 API|<ul><li><xref:System.Windows.Forms.Application.FilterMessage(System.Windows.Forms.Message@)?displayProperty=nameWithType></li></ul>|

