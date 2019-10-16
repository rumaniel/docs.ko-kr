---
ms.openlocfilehash: 1f06a185939c40274adad1ceac6990719069167a
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59804553"
---
### <a name="change-in-behavior-in-data-definition-language-ddl-apis"></a>DDL(데이터 정의 언어) API에서 동작 변경

|   |   |
|---|---|
|세부 정보|AttachDBFilename이 지정되면 DDL API의 동작은 다음과 같이 변경됩니다.<ul><li>연결 문자열에 초기 카탈로그 값을 지정할 필요는 없습니다. 이전에는 AttachDBFilename 및 초기 카탈로그가 모두 필요했습니다.</li><li>AttachDBFilename 및 초기 카탈로그가 모두 지정되고 제공된 MDF 파일이 있는 경우 <xref:System.Data.Objects.ObjectContext.DatabaseExists%2A> 메서드는 <code>true</code>를 반환합니다. 이전에는 <code>false</code>를 반환했습니다.</li><li>AttachDBFilename 및 초기 카탈로그가 모두 지정되고 제공된 MDF 파일이 있는 경우 <xref:System.Data.Objects.ObjectContext.DeleteDatabase%2A> 메서드 호출은 파일을 삭제합니다.</li><li>존재하지 않는 MDF 및 존재하지 않는 Initial Catalog로 연결 문자열이 AttachDBFilename 값을 지정할 때 <xref:System.Data.Objects.ObjectContext.DeleteDatabase%2A>가 호출되면, 이 메서드는 <xref:System.InvalidOperationException> 예외를 throw합니다. 이전에는 <xref:System.Data.SqlClient.SqlException> 예외를 throw했습니다.</li></ul>|
|제안 해결 방법|이러한 변경으로 인해 DDL API를 사용하는 도구와 애플리케이션을 보다 쉽게 빌드할 수 있습니다. 이러한 변경 사항은 다음 시나리오에서 애플리케이션 호환성에 영향을 줄 수 있습니다.<ul><li><code>DROP DATABASE</code>가 <xref:System.Data.Objects.ObjectContext.DeleteDatabase%2A>를 반환할 경우 <xref:System.Data.Objects.ObjectContext.DatabaseExists%2A>를 호출하는 대신 사용자는 <code>true</code> 명령을 직접 실행하는 코드를 작성합니다. 이는 데이터베이스가 연결되지 않았지만 MDF 파일이 있는 경우 기존 코드를 중단시킵니다.</li><li>사용자는 <xref:System.Data.Objects.ObjectContext.DeleteDatabase%2A> 메서드에서 Initial Catalog 및 MDF 파일이 없을 때 <xref:System.InvalidOperationException>이 아닌 <xref:System.Data.SqlClient.SqlException>을 throw하도록 기대되는 코드를 작성합니다.</li></ul>|
|범위|부|
|버전|4.5|
|형식|런타임|
