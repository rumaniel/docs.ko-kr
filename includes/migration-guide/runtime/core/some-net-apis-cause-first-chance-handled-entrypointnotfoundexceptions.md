---
ms.openlocfilehash: b23f06ec5b27fbd7976a4b62ba6105c607eaee39
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59236699"
---
### <a name="some-net-apis-cause-first-chance-handled-entrypointnotfoundexceptions"></a>일부 .NET API는 첫 번째 기회(처리) EntryPointNotFoundExceptions의 원인

|   |   |
|---|---|
|설명|.NET Framework 4.5에서 소수의 .NET 메서드가 첫 번째 기회 <xref:System.EntryPointNotFoundException?displayProperty=name>을 throw하기 시작했습니다. 이러한 예외는 .NET Framework 내에서 처리되지만 첫 번째 예외를 예상하지 않은 테스트 자동화를 중단시킬 수 있습니다. 이러한 동일 API는 HighVersionLie를 사용하는 경우 일부 ApiVerifier 시나리오를 중단시킵니다.|
|제안 해결 방법|.NET Framework 4.5.1로 업그레이드하여 이 버그를 방지할 수 있습니다. 또는 첫 번째 기회 <xref:System.EntryPointNotFoundException?displayProperty=name>에서 문제가 발생하지 않도록 테스트 자동화를 업데이트할 수 있습니다.|
|범위|Microsoft Edge|
|버전|4.5|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Diagnostics.Debug.Assert(System.Boolean)?displayProperty=nameWithType></li><li><xref:System.Diagnostics.Debug.Assert(System.Boolean,System.String)?displayProperty=nameWithType></li><li><xref:System.Diagnostics.Debug.Assert(System.Boolean,System.String,System.String)?displayProperty=nameWithType></li><li><xref:System.Diagnostics.Debug.Assert(System.Boolean,System.String,System.String,System.Object[])?displayProperty=nameWithType></li><li><xref:System.Xml.Serialization.XmlSerializer.%23ctor(System.Type)?displayProperty=nameWithType></li></ul>|
