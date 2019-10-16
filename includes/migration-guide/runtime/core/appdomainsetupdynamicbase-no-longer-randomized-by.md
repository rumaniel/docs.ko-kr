---
ms.openlocfilehash: ab7731d34aad5b6b6481f13ba11b778393e2cac2
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67858620"
---
### <a name="appdomainsetupdynamicbase-is-no-longer-randomized-by-userandomizedstringhashalgorithm"></a>AppDomainSetup.DynamicBase는 더 이상 UseRandomizedStringHashAlgorithm에 의해 무작위화되지 않음

|   |   |
|---|---|
|세부 정보|.NET Framework 4.6 이전에는, UseRandomizedStringHashAlgorithm이 앱의 구성 파일에서 활성화된 경우 애플리케이션 도메인 간 또는 프로세스 간에 <xref:System.AppDomainSetup.DynamicBase> 값이 무작위화되었습니다. .NET Framework 4.6부터 <xref:System.AppDomainSetup.DynamicBase>가 실행 중인 앱의 여러 인스턴스와 다른 앱 도메인 간에 안정적인 결과를 반환합니다. 동적 기반은 여전히 앱에 따라 다릅니다. 이 변경은 동일한 앱의 다른 인스턴스에 대한 임의의 이름 지정 요소만 제거합니다.|
|제안|<code>UseRandomizedStringHashAlgorithm</code>을 사용하도록 설정해도 <xref:System.AppDomainSetup.DynamicBase>가 무작위화되지 않습니다. 임의 기반이 필요한 경우 이 API를 통하지 않고 앱의 코드에서 생성해야 합니다.|
|범위|Microsoft Edge|
|버전|4.6|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.AppDomainSetup.DynamicBase?displayProperty=nameWithType></li></ul>|

