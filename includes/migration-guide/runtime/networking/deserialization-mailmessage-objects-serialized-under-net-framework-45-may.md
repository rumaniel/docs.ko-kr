---
ms.openlocfilehash: a6f93bbdf39a1b525e2daeb12afc3a6392a66e30
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59235752"
---
### <a name="deserialization-of-mailmessage-objects-serialized-under-the-net-framework-45-may-fail"></a>.NET Framework 4.5에서 직렬화된 MailMessage 개체의 역직렬화가 실패할 수 있음

|   |   |
|---|---|
|세부 정보|.NET Framework 4.5부터는 <xref:System.Web.Mail.MailMessage> 개체에 비 ASCII 문자가 포함될 수 있습니다. .NET Framework 4에서는 ASCII 문자만 지원됩니다. ASCII가 아닌 문자를 포함하고 .NET Framework 4.5 이상에서 직렬화되는 <xref:System.Web.Mail.MailMessage> 개체는 .NET Framework 4에서 역직렬화될 수 없습니다.|
|제안 해결 방법|<xref:System.Web.Mail.MailMessage> 개체를 역직렬화할 때 코드가 예외 처리를 제공하는지 확인합니다.|
|범위|부|
|버전|4.5|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Web.Mail.MailMessage?displayProperty=nameWithType></li></ul>|
