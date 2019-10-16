---
ms.openlocfilehash: fa09831ac47a59535ff73c8c8680c2642c3248c9
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59235522"
---
### <a name="sqlbulkcopy-uses-destination-column-encoding-for-strings"></a>SqlBulkCopy는 문자열에 대상 열 인코딩을 사용함

|   |   |
|---|---|
|세부 정보|열에 데이터를 삽입할 때 <xref:System.Data.SqlClient.SqlBulkCopy?displayProperty=name>에서는 <code>VARCHAR</code> 및 <code>CHAR</code> 형식에 대한 기본 인코딩 대신 대상 열의 인코딩을 사용합니다. 이러한 변경을 통해 대상 열에서 기본 인코딩을 사용하지 않는 경우 기본 인코딩을 사용하여 발생하는 데이터 손상의 가능성을 제거합니다. 드문 경우이지만 인코딩에서의 이 변경으로 인해 대상 열에 맞추기에는 너무 큰 데이터가 생성되는 경우, 기존 애플리케이션에서 SqlException 예외를 throw할 수 있습니다.|
|제안 해결 방법|인코딩 차이로 인해 <xref:System.Data.SqlClient.SqlBulkCopy?displayProperty=name>이 더 이상 데이터를 손상시키지 않을 것입니다. 대상 열의 크기 제한 근처 문자열을 복사하는 경우 데이터를 미리 인코딩(데이터가 대상 열에 맞는지 확인하기 위해 복사)하거나 <xref:System.Data.SqlClient.SqlException?displayProperty=name>을 catch해야 합니다.|
|범위|Microsoft Edge|
|버전|4.5|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Data.SqlClient.SqlBulkCopy?displayProperty=nameWithType></li><li><xref:System.Data.SqlClient.SqlBulkCopy.%23ctor(System.Data.SqlClient.SqlConnection)?displayProperty=nameWithType></li></ul>|
