---
title: 함수(Entity SQL)
ms.date: 03/30/2017
ms.assetid: 52b3d776-5acc-4f69-b614-5a43ce56ef9f
ms.openlocfilehash: ec94a0f16fb3b836297f6675cc938a711816555b
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70250911"
---
# <a name="functions-entity-sql"></a>함수(Entity SQL)
Entity SQL에서는 사용자 정의 함수, 정식 함수 및 공급자 특정 함수를 지원합니다. 사용자 정의 함수는 개념적 모델에 지정되거나 쿼리에 인라인으로 지정됩니다. 자세한 내용은 [사용자 정의 함수](user-defined-functions-entity-sql.md)를 참조 하세요.  
  
 정식 함수는 Entity Framework에 미리 정의되어 있으며 데이터 공급자의 지원이 필요합니다. 공급자가 지원하지 않는 함수를 사용자가 호출하는 경우 Entity SQL 명령은 실패합니다. 따라서, 일반적으로 정식 함수는 공급자 특정 네임스페이스에 들어 있는 저장소 특정 함수의 경우에 권장됩니다. 자세한 내용은 [정식 함수](canonical-functions.md)를 참조 하세요.  
  
 Microsoft SQL 클라이언트 관리 공급자에서는 공급자 특정 함수 집합이 제공됩니다. 자세한 내용은 [Entity Framework 함수에 대 한 SqlClient](../sqlclient-for-ef-functions.md)를 참조 하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
 [사용자 정의 함수](user-defined-functions-entity-sql.md)  
  
 [함수 오버로드 확인](function-overload-resolution-entity-sql.md)  
  
 [집계 함수](../aggregate-functions-sqlclient-for-entity-framework.md)  
  
## <a name="see-also"></a>참고자료

- [Entity SQL 개요](entity-sql-overview.md)
