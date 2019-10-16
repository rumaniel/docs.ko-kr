---
title: 사용자 정의 함수(Entity SQL)
ms.date: 03/30/2017
ms.assetid: 3f9e6bbd-8e5a-43e1-809f-f8a61338e522
ms.openlocfilehash: 9ddafb18a10ff2313fd27eab453907054a35218a
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70248766"
---
# <a name="user-defined-functions-entity-sql"></a>사용자 정의 함수(Entity SQL)
Entity SQL에서는 쿼리에서 사용자 정의 함수를 호출할 수 있습니다. 쿼리를 사용 하 여 이러한 함수를 인라인으로 정의할 수 [있습니다 (방법: 사용자 정의 함수](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dd490951(v=vs.100))를 호출 하거나 개념적 모델의 일부로 호출 합니다 [(방법: 개념적 모델](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dd456812(v=vs.100))에서 사용자 지정 함수를 정의 합니다. 개념적 모델 함수는 개념적 모델에 있는 [Function](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#function-element-csdl) 요소의 [DefiningExpression](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#definingexpression-element-csdl) 요소에서 Entity SQL 명령으로 정의 됩니다.  
  
 Entity SQL을 통해 쿼리 명령 자체에서 함수를 정의할 수 있습니다. [함수](function-entity-sql.md) 연산자는 인라인 함수를 정의 합니다. 함수 시그니처가 고유하면 단일 명령에서 여러 함수를 정의할 수 있으며, 이러한 함수는 이름이 같을 수 있습니다. 자세한 내용은 [Function Overload Resolution](function-overload-resolution-entity-sql.md)을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- [함수](functions-entity-sql.md)
