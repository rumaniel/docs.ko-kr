---
ms.openlocfilehash: 1721d32f8cdc9b6ea4b4732e38afa56a8a532600
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59234817"
---
### <a name="dbparameterprecision-and-dbparameterscale-are-now-public-virtual-members"></a>DbParameter.Precision 및 DbParameter.Scale는 이제 공용 가상 멤버임

|   |   |
|---|---|
|세부 정보|<xref:System.Data.Common.DbParameter.Precision>과 <xref:System.Data.Common.DbParameter.Scale>은 공용 가상 속성으로 구현됩니다. 이들은 명시적 인터페이스 구현에 해당하는 <xref:System.Data.Common.DbParameter.System%23Data%23IDbDataParameter%23Precision>과 <xref:System.Data.Common.DbParameter.System%23Data%23IDbDataParameter%23Scale>로 대체됩니다.|
|제안 해결 방법|ADO.NET 데이터베이스 공급자를 다시 작성할 때 이러한 차이는 전체 자릿수 및 소수 자릿수 속성에 적용될 'override' 키워드가 필요합니다. 이것은 구성 요소를 다시 빌드할 때만 필요하며 기존의 이진 파일은 계속 작동합니다.|
|범위|부|
|버전|4.5.1|
|형식|대상 변경|
|영향을 받는 API|<ul><li><xref:System.Data.Common.DbParameter.Precision?displayProperty=nameWithType></li><li><xref:System.Data.Common.DbParameter.Scale?displayProperty=nameWithType></li></ul>|
