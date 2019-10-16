---
title: 형식 생성(Entity SQL)
ms.date: 03/30/2017
ms.assetid: 41fa7bde-8d20-4a3f-a3d2-fb791e128010
ms.openlocfilehash: 7113aaf1c2caa982a8ab4751928856c1271570cb
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70251119"
---
# <a name="constructing-types-entity-sql"></a>형식 생성(Entity SQL)
[!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 행 생성자, 명명 된 형식 생성자 및 컬렉션 생성자 라는 세 가지 종류의 생성자를 제공 합니다.  
  
## <a name="row-constructors"></a>행 생성자  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]의 행 생성자를 사용하여 값 하나 이상을 기반으로 구조적으로 형식화된 익명 레코드를 생성합니다. 행 생성자의 결과 형식은 필드 형식이 행 생성에 사용된 값의 형식과 동일한 행 형식입니다. 예를 들어 다음 식은 `Record(a int, b string, c int)` 형식의 값을 생성합니다.  
  
 `ROW(1 AS a, "abc" AS b, a + 34 AS c)`  
  
 행 생성자에서 식의 별칭을 제공하지 않으면 Entity Framework에서 별칭을 생성합니다. 자세한 내용은 [식별자](identifiers-entity-sql.md)의 "별칭 규칙" 섹션을 참조 하세요.  
  
 행 생성자에서 식에 별칭을 지정하는 데 다음 규칙이 적용됩니다.  
  
- 행 생성자의 식은 동일한 생성자 내의 다른 별칭을 참조할 수 없습니다.  
  
- 동일한 행 생성자 내의 서로 다른 두 식은 별칭이 같을 수 없습니다.  
  
 행 생성자에 대 한 자세한 내용은 [row](row-entity-sql.md)를 참조 하십시오.  
  
## <a name="collection-constructors"></a>컬렉션 생성자  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]의 컬렉션 생성자를 사용하여 값 목록에서 multiset 인스턴스를 만듭니다. 생성자의 모든 값은 상호 호환되는 `T` 형식이어야 하며, 생성자는 `Multiset<T>` 형식의 컬렉션을 생성합니다. 예를 들어, 다음 식은 정수 컬렉션을 만듭니다.  
  
 `Multiset(1, 2, 3)`  
  
 `{1, 2, 3}`  
  
 빈 multiset 생성자는 요소 형식을 확인할 수 없으므로 사용할 수 없습니다. 다음은 유효하지 않습니다.  
  
 `multiset() {}`  
  
 자세한 내용은 [MULTISET](multiset-entity-sql.md)를 참조 하세요.  
  
## <a name="named-type-constructors-namedtype-initializers"></a>명명된 형식 생성자(NamedType 이니셜라이저)  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서 형식 생성자(이니셜라이저)는 명명된 복합 형식과 엔터티 형식 인스턴스를 만들 수 있습니다. 예를 들어, 다음 식은 `Person` 형식의 인스턴스를 만듭니다.  
  
 `Person("abc", 12)`  
  
 다음 식은 복합 형식의 인스턴스를 만듭니다.  
  
 `MyModel.ZipCode(‘98118’, ‘4567’)`  
  
 다음 식은 중첩된 복합 형식의 인스턴스를 만듭니다.  
  
 `MyModel.AddressInfo('My street address', 'Seattle', 'WA', MyModel.ZipCode('98118', '4567'))`  
  
 다음 식은 중첩된 복합 형식을 가진 엔터티의 인스턴스를 만듭니다.  
  
 `MyModel.Person("Bill", MyModel.AddressInfo('My street address', 'Seattle', 'WA', MyModel.ZipCode('98118', '4567')))`  
  
 다음 예제에서는 복합 형식의 속성을 null로 초기화하는 방법을 보여 줍니다. `MyModel.ZipCode(‘98118’, null)`  
  
 생성자의 인수는 형식의 특성 선언과 동일한 순서인 것으로 가정됩니다.  
  
 자세한 내용은 [명명 된 형식 생성자](named-type-constructor-entity-sql.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [엔터티 SQL 참조](entity-sql-reference.md)
- [Entity SQL 개요](entity-sql-overview.md)
- [형식 시스템](type-system-entity-sql.md)
