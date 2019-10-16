---
title: 데이터 세트 스키마 유추 프로세스 요약
ms.date: 03/30/2017
ms.assetid: fd0891c8-d068-4e30-a76f-7c375f078bf7
ms.openlocfilehash: 35e9b67d2d0a47aa69eabdb4b7e94f95b0b9589f
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71833973"
---
# <a name="summary-of-the-dataset-schema-inference-process"></a>데이터 세트 스키마 유추 프로세스 요약
유추 과정에서는 우선 XML 문서에서 테이블로 유추될 요소를 결정합니다. 그런 다음 남아 있는 XML에서 해당 테이블의 열을 결정합니다. 중첩된 테이블인 경우에는 유추 과정에서 중첩된 <xref:System.Data.DataRelation> 및 <xref:System.Data.ForeignKeyConstraint> 개체를 생성합니다.  
  
 다음은 유추 규칙에 대 한 간략 한 요약입니다.  
  
- 특성이 있는 요소는 테이블로 유추됩니다.  
  
- 자식 요소가 있는 요소는 테이블로 유추됩니다.  
  
- 반복되는 요소는 하나의 테이블로 유추됩니다.  
  
- 문서 요소에 열로 유추되는 특성이나 자식 요소가 없으면 문서 요소 또는 루트 요소는 <xref:System.Data.DataSet>으로 유추됩니다. 그렇지 않으면 문서 요소는 테이블로 유추됩니다.  
  
- 특성은 열로 유추됩니다.  
  
- 특성이나 자식 요소가 없거나 반복되지 않는 요소는 열로 유추됩니다.  
  
- 테이블로 유추 되는 다른 요소 내에서 중첩 테이블로 유추 되는 요소의 경우 두 테이블 간에 중첩 된 **DataRelation** 이 생성 됩니다. **TableName_Id** 라는 새 기본 키 열이 두 테이블에 모두 추가 되 고 **DataRelation**에서 사용 됩니다. **TableName_Id** 열을 사용 하 여 두 테이블 간에 **ForeignKeyConstraint** 생성 됩니다.  
  
- 테이블로 유추 되 고 텍스트가 포함 되지만 자식 요소가 없는 요소의 경우 각 요소의 텍스트에 대해 **TableName_Text** 라는 새 열이 만들어집니다. 테이블로 유추되는 요소에 텍스트와 자식 요소가 모두 있으면 해당 텍스트는 무시됩니다.  
  
## <a name="see-also"></a>참조

- [XML에서 데이터 세트 관계형 구조 유추](inferring-dataset-relational-structure-from-xml.md)
- [XML에서 데이터 세트 로드](loading-a-dataset-from-xml.md)
- [XML에서 데이터 세트 스키마 정보 로드](loading-dataset-schema-information-from-xml.md)
- [데이터 세트에서 XML 사용](using-xml-in-a-dataset.md)
- [DataSets, DataTables 및 DataViews](index.md)
- [ADO.NET 개요](../ado-net-overview.md)
