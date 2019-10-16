---
ms.openlocfilehash: 891c29b731214fb0028e960256b79cfc267d86b9
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59804535"
---
### <a name="deserialization-of-objects-across-appdomains-can-fail"></a>앱 도메인 간의 개체 역직렬화가 실패할 수 있습니다.

|   |   |
|---|---|
|세부 정보|경우에 따라, 애플리케이션 기반이 다른 둘 이상의 앱 도메인이 앱에서 사용되는 경우 앱 도메인 간에 논리 호출 컨텍스트의 개체를 deserialize하려고 하면 예외가 throw됩니다.|
|제안 해결 방법|[완화: 앱 도메인 간 개체의 deserialization](~/docs/framework/migration-guide/mitigation-deserialization-of-objects-across-app-domains.md)을 참조하세요.|
|범위|Microsoft Edge|
|버전|4.5.1|
|형식|런타임|
