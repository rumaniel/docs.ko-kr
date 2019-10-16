---
ms.openlocfilehash: d6c658f306dd4792e3cb5dbdc9471043ca95a071
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67859110"
---
### <a name="httpruntimeappdomainapppath-throws-a-nullreferenceexception"></a>HttpRuntime.AppDomainAppPath가 NullReferenceException을 Throw함

|   |   |
|---|---|
|세부 정보|.NET Framework 4.6.2에서 런타임은 null 문자를 포함하는 <code>P:System.Web.HttpRuntime.AppDomainAppPath</code> 값을 검색할 때 <code>T:System.NullReferenceException</code>를 throw합니다. .NET Framework 4.6.1 이전 버전에서 런타임은 <code>T:System.ArgumentNullException</code>를 throw합니다.|
|제안|이러한 변경에 대처하기 위해 다음 중 하나를 수행할 수 있습니다.<ul><li>애플리케이션이 .NET Framework 4.6.2에서 실행 중인 경우 <code>T:System.NullReferenceException</code>를 처리합니다.</li><li>.NET Framework 4.7로 업그레이드하면 이전 동작이 복원되고 <code>T:System.ArgumentNullException</code>가 throw됩니다.</li></ul>|
|범위|Microsoft Edge|
|버전|4.6.2|
|형식|대상 변경|
|영향을 받는 API|<ul><li><xref:System.Web.HttpRuntime.AppDomainAppPath?displayProperty=nameWithType></li></ul>|

