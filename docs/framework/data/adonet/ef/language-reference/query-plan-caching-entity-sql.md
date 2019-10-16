---
title: 쿼리 계획 캐싱(Entity SQL)
ms.date: 03/30/2017
ms.assetid: 90b0c685-5ef2-461b-98b4-c3c0a2b253c7
ms.openlocfilehash: ca95f3aed5c092247a97bbfe5b0237a45b95ae16
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70249293"
---
# <a name="query-plan-caching-entity-sql"></a>쿼리 계획 캐싱(Entity SQL)
쿼리 실행 시도가 있으면 쿼리 파이프라인에서는 항상 해당 쿼리가 이미 컴파일되어 사용 가능한지 알아보기 위해 쿼리 계획 캐시를 확인합니다. 사용 가능한 쿼리가 있으면 새 쿼리를 작성하지 않고 캐시된 계획을 재사용합니다. 쿼리 계획 캐시에 일치 항목이 없을 경우에는 쿼리를 컴파일하고 캐시합니다. 쿼리는 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 텍스트 및 매개 변수 컬렉션(이름과 형식)으로 식별됩니다. 모든 텍스트 비교에서는 대/소문자가 구별됩니다.  
  
## <a name="configuration"></a>Configuration  
 쿼리 계획 캐싱은 <xref:System.Data.EntityClient.EntityCommand>를 통해 구성할 수 있습니다.  
  
 <xref:System.Data.EntityClient.EntityCommand.EnablePlanCaching%2A?displayProperty=nameWithType>을 통해 쿼리 계획 캐싱을 사용하려면 이 속성을 `true`로, 사용하지 않으려면 `false`로 설정합니다. 두 번 이상 사용할 가능성이 적은 개별 동적 쿼리에 대해 계획 캐싱을 사용하지 않도록 설정하면 성능이 향상됩니다.  
  
 <xref:System.Data.Objects.ObjectQuery.EnablePlanCaching%2A>을 통해 쿼리 계획 캐싱을 사용하도록 설정할 수 있습니다.  
  
## <a name="recommended-practice"></a>권장 방법  
 일반적으로 동적 쿼리는 사용하지 않아야 합니다. 다음 동적 쿼리 예제는 유효성 검사 없이 사용자의 직접적인 입력을 사용하므로 SQL 삽입 공격에 취약합니다.  
  
 `"SELECT sp.SalesYTD FROM AdventureWorksEntities.SalesPerson as sp WHERE sp.EmployeeID = " + employeeTextBox.Text;`  
  
 동적으로 생성된 쿼리를 사용하는 경우 다시 사용할 가능성이 적은 캐시 항목의 불필요한 메모리 사용을 방지하기 위해 쿼리 계획 캐싱을 사용하지 않도록 설정하는 것이 좋습니다.  
  
 정적 쿼리 및 매개 변수화된 쿼리에 대해 쿼리 계획 캐싱을 이용하면 성능이 향상될 수 있습니다. 다음은 정적 쿼리의 예제입니다.  
  
```  
"SELECT sp.SalesYTD FROM AdventureWorksEntities.SalesPerson as sp";  
```  
  
 쿼리가 쿼리 계획 캐시와 제대로 일치하려면 다음 요구 사항을 준수해야 합니다.  
  
- 쿼리 텍스트가 상수 패턴이어야 하며, 가능한 한 상수 문자열 또는 리소스여야 합니다.  
  
- 사용자가 제공한 값을 전달해야 하는 경우 항상 <xref:System.Data.EntityClient.EntityParameter> 또는 <xref:System.Data.Objects.ObjectParameter>를 사용해야 합니다.  
  
 쿼리 계획 캐시에서 불필요하게 슬롯을 사용하는 다음 쿼리 패턴을 피해야 합니다.  
  
- 텍스트의 대/소문자 변경  
  
- 공백으로 변경  
  
- 리터럴 값으로 변경  
  
- 주석 내부의 텍스트 변경  
  
## <a name="see-also"></a>참고자료

- [Entity SQL 개요](entity-sql-overview.md)
