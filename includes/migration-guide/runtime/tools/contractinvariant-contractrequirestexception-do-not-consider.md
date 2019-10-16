---
ms.openlocfilehash: 204fe32ec8b7fbaab89e37d7e761469212091728
ms.sourcegitcommit: 4d8efe00f2e5ab42e598aff298d13b8c052d9593
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68237915"
---
### <a name="contractinvariant-or-contractrequirestexception-do-not-consider-stringisnullorempty-to-be-pure"></a>Contract.Invariant 또는 Contract.Requires\<TException>는 String.IsNullOrEmpty를 순수형으로 간주하지 않습니다

|   |   |
|---|---|
|세부 정보|.NET Framework 4.6.1을 대상으로 하는 앱의 경우 <xref:System.Diagnostics.Contracts.Contract.Invariant%2A?displayProperty=nameWithType>의 고정 계약 또는 <xref:System.Diagnostics.Contracts.Contract.Requires%2A?displayProperty=nameWithType)>의 사전 조건 계약이 <xref:System.String.IsNullOrEmpty%2A?displayProperty=nameWithType> 메서드를 호출하는 경우 재작성기에서 CC1036 컴파일러 경고: &quot;메서드에서 [순수형] 없이 'System.String.IsNullOrWhteSpace(System.String)' 메서드에 대한 호출이 감지되었습니다.&quot;를 내보냅니다. 이는 컴파일러 오류가 아닌 컴파일러 경고입니다.|
|제안 해결 방법|이 동작에서는 [GitHub 문제 #339](https://github.com/Microsoft/CodeContracts/issues/339)가 해결되었습니다. 이 경고를 제거하려면 [GitHub](https://github.com/Microsoft/CodeContracts/blob/master/README.md)에서 코드 계약 도구에 대한 소스 코드를 다운로드 및 컴파일할 수 있습니다. 다운로드 정보는 페이지 하단에서 찾을 수 있습니다.|
|범위|부|
|버전|4.6.1|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Diagnostics.Contracts.Contract.Invariant(System.Boolean)?displayProperty=nameWithType></li><li><xref:System.Diagnostics.Contracts.Contract.Requires(System.Boolean)?displayProperty=nameWithType></li></ul>|
