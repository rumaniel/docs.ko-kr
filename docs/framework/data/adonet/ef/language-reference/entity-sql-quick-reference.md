---
title: Entity SQL 빠른 참조
ms.date: 03/30/2017
ms.assetid: e53dad9e-5e83-426e-abb4-be3e78e3d6dc
ms.openlocfilehash: 9ccfc461d394af8804c960ebf460e7fbfb025b64
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71833870"
---
# <a name="entity-sql-quick-reference"></a>Entity SQL 빠른 참조
이 항목에서는 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] 쿼리에 대한 빠른 참조를 제공합니다. 이 항목의 쿼리는 AdventureWorks Sales 모델을 기반으로 합니다.  
  
## <a name="literals"></a>리터럴  
  
### <a name="string"></a>문자열  
 유니코드 문자열 리터럴과 유니코드가 아닌 문자열 리터럴이 있습니다. 유니코드 문자열 앞에 N이 붙습니다. 예를 들어 `N'hello'`입니다.  
  
 다음은 비유니코드 문자열 리터럴의 예제입니다.  
  
```sql  
'hello'  
--same as  
"hello"  
```  
  
 출력:  
  
|값|  
|-----------|  
|hello|  
  
### <a name="datetime"></a>DateTime  
 DateTime 리터럴에서는 날짜와 시간 부분 모두 필수 요소입니다. 기본값은 없습니다.  
  
 예:  
  
```sql  
DATETIME '2006-12-25 01:01:00.000'   
--same as  
DATETIME '2006-12-25 01:01'  
```  
  
 출력:  
  
|값|  
|-----------|  
|12/25/2006 1:01:00 AM|  
  
### <a name="integer"></a>Integer  
 Integer 리터럴은 Int32(123), UInt32(123U), Int64(123L) 및 UInt64(123UL) 형식일 수 있습니다.  
  
 예:  
  
```sql  
--a collection of integers  
{1, 2, 3}  
```  
  
 출력:  
  
|값|  
|-----------|  
|1|  
|2|  
|3|  
  
### <a name="other"></a>기타  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서 지원되는 기타 리터럴은 Guid, Binary, Float/Double, Decimal, `null` 등입니다. [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서 Null 리터럴은 개념적 모델의 다른 모든 형식과 호환 가능한 것으로 간주됩니다.  
  
## <a name="type-constructors"></a>형식 생성자  
  
### <a name="row"></a>ROW  
 [ROW](row-entity-sql.md) 는 다음과 같이 구조적으로 형식화 된 익명 (레코드) 값을 생성 `ROW(1 AS myNumber, ‘Name’ AS myName).`입니다.  
  
 예:  
  
```sql  
SELECT VALUE row (product.ProductID AS ProductID, product.Name
    AS ProductName) FROM AdventureWorksEntities.Product AS product
```  
  
 출력:  
  
|ProductID|이름|  
|---------------|----------|  
|1|Adjustable Race|  
|879|All-Purpose Bike Stand|  
|712|AWC Logo Cap|  
|...|...|  
  
### <a name="multiset"></a>MULTISET  
 [MULTISET](multiset-entity-sql.md) 는 다음과 같은 컬렉션을 생성 합니다.  
  
 `MULTISET(1,2,2,3)` `--same as`-`{1,2,2,3}.`  
  
 예:  
  
```sql  
SELECT VALUE product FROM AdventureWorksEntities.Product AS product WHERE product.ListPrice IN MultiSet (125, 300)  
```  
  
 출력:  
  
|ProductID|이름|ProductNumber|…|  
|---------------|----------|-------------------|-------|  
|842|Touring-Panniers, Large|PA-T100|…|  
  
### <a name="object"></a>Object  
 [명명 된 형식 생성자](named-type-constructor-entity-sql.md) `person("abc", 12)`과 같은 사용자 정의 개체를 생성 합니다.  
  
 예:  
  
```sql  
SELECT VALUE AdventureWorksModel.SalesOrderDetail (o.SalesOrderDetailID, o.CarrierTrackingNumber, o.OrderQty,   
o.ProductID, o.SpecialOfferID, o.UnitPrice, o.UnitPriceDiscount,   
o.rowguid, o.ModifiedDate) FROM AdventureWorksEntities.SalesOrderDetail   
AS o  
```  
  
 출력:  
  
|SalesOrderDetailID|CarrierTrackingNumber|OrderQty|ProductID|...|  
|------------------------|---------------------------|--------------|---------------|---------|  
|1|4911-403C-98|1|776|...|  
|2|4911-403C-98|3|777|...|  
|...|...|...|...|...|  
  
## <a name="references"></a>참조  
  
### <a name="ref"></a>REF  
 [REF](ref-entity-sql.md) 는 엔터티 형식 인스턴스에 대 한 참조를 만듭니다. 예를 들어, 다음 쿼리는 주문 엔터티 집합의 개별 주문 엔터티에 대한 참조를 반환합니다.  
  
```sql  
SELECT REF(o) AS OrderID FROM Orders AS o  
```  
  
 출력:  
  
|값|  
|-----------|  
|1|  
|2|  
|3|  
|...|  
  
 다음 예제에서는 속성 추출 연산자(.)를 사용하여 엔터티의 속성에 액세스합니다. 속성 추출 연산자가 사용되면 해당 참조가 자동으로 역참조됩니다.  
  
 예:  
  
```sql  
SELECT VALUE REF(p).Name FROM   
    AdventureWorksEntities.Product AS p
```  
  
 출력:  
  
|값|  
|-----------|  
|Adjustable Race|  
|All-Purpose Bike Stand|  
|AWC Logo Cap|  
|...|  
  
### <a name="deref"></a>DEREF  
 [DEREF](deref-entity-sql.md) 는 참조 값을 역참조 하 고이 역참조의 결과를 생성 합니다. 예를 들어, `SELECT DEREF(o2.r) FROM (SELECT REF(o) AS r FROM LOB.Orders AS o) AS o2` 쿼리는 Orders 엔터티 집합의 개별 Order별로 Order 엔터티를 생성합니다.  
  
 예:  
  
```sql  
SELECT VALUE DEREF(REF(p)).Name FROM   
    AdventureWorksEntities.Product AS p
```  
  
 출력:  
  
|값|  
|-----------|  
|Adjustable Race|  
|All-Purpose Bike Stand|  
|AWC Logo Cap|  
|...|  
  
### <a name="createref-and-key"></a>CREATEREF 및 KEY  
 [CREATEREF](createref-entity-sql.md) 키를 전달 하는 참조를 만듭니다. [Key](key-entity-sql.md) 는 형식 참조가 있는 식의 키 부분을 추출 합니다.  
  
 예:  
  
```sql  
SELECT VALUE Key(CreateRef(AdventureWorksEntities.Product, row(p.ProductID)))   
    FROM AdventureWorksEntities.Product AS p
```  
  
 출력:  
  
|ProductID|  
|---------------|  
|980|  
|365|  
|771|  
|...|  
  
## <a name="functions"></a>함수  
  
### <a name="canonical"></a>정식  
 [정식 함수](canonical-functions.md) 에 대 한 네임 스페이스는 `Edm.Length("string")`과 같이 Edm입니다. 정식 함수와 이름이 같은 함수가 포함된 다른 네임스페이스를 가져오지 않는 한, 네임스페이스를 지정할 필요가 없습니다. 두 네임스페이스의 함수가 동일한 경우 사용자는 전체 이름을 지정해야 합니다.  
  
 예:  
  
```sql  
SELECT Length(c. FirstName) AS NameLen FROM
    AdventureWorksEntities.Contact AS c   
    WHERE c.ContactID BETWEEN 10 AND 12  
```  
  
 출력:  
  
|NameLen|  
|-------------|  
|6|  
|6|  
|5|  
  
### <a name="microsoft-provider-specific"></a>Microsoft 공급자 특정  
 [Microsoft 공급자별 함수](../sqlclient-for-ef-functions.md) 는 `SqlServer` 네임 스페이스에 있습니다.  
  
 예:  
  
```sql  
SELECT SqlServer.LEN(c.EmailAddress) AS EmailLen FROM
    AdventureWorksEntities.Contact AS c WHERE   
    c.ContactID BETWEEN 10 AND 12  
```  
  
 출력:  
  
|EmailLen|  
|--------------|  
|27|  
|27|  
|26|  
  
## <a name="namespaces"></a>네임스페이스  
 를 [사용 하 여](using-entity-sql.md) 쿼리 식에 사용 되는 네임 스페이스를 지정 합니다.  
  
 예:  
  
```sql  
using SqlServer; LOWER('AA');  
```  
  
 출력:  
  
|값|  
|-----------|  
|aa|  
  
## <a name="paging"></a>페이징  
 [SKIP](skip-entity-sql.md) 및 [LIMIT](limit-entity-sql.md) 하위 절을 [ORDER by](order-by-entity-sql.md) 절에 선언 하 여 페이징을 표현할 수 있습니다.  
  
 예:  
  
```sql  
SELECT c.ContactID as ID, c.LastName AS Name FROM
    AdventureWorks.Contact AS c ORDER BY c.ContactID SKIP 9 LIMIT 3;  
```  
  
 출력:  
  
|id|이름|  
|--------|----------|  
|10|Adina|  
|11|Agcaoili|  
|12|Aguilar|  
  
## <a name="grouping"></a>그룹화  
 [그룹화 방법](group-by-entity-sql.md) 쿼리 ([SELECT](select-entity-sql.md)) 식에서 반환 되는 개체가 배치 될 그룹을 지정 합니다.  
  
 예:  
  
```sql  
SELECT VALUE name FROM AdventureWorksEntities.Product AS P
    GROUP BY P.Name HAVING MAX(P.ListPrice) > 5  
```  
  
 출력:  
  
|name|  
|----------|  
|LL Mountain Seat Assembly|  
|ML Mountain Seat Assembly|  
|HL Mountain Seat Assembly|  
|...|  
  
## <a name="navigation"></a>탐색  
 관계 탐색 연산자를 사용하여 엔터티 간의(시작 End에서 끝 End) 관계를 탐색할 수 있습니다. [NAVIGATE](navigate-entity-sql.md) 는 \<namespace >으로 한정 된 관계 유형을 사용 합니다. \<relationship 유형 이름 >. Navigate는 to end의 카디널리티가 1 인 경우 Ref @ no__t-0T > 반환 합니다. 끝 end의 카디널리티가 n 인 경우 < Ref @ no__t-0T > > 컬렉션이 반환 됩니다.  
  
 예:  
  
```sql  
SELECT a.AddressID, (SELECT VALUE DEREF(v) FROM   
    NAVIGATE(a, AdventureWorksModel.FK_SalesOrderHeader_Address_BillToAddressID) AS v)   
    FROM AdventureWorksEntities.Address AS a  
```  
  
 출력:  
  
|AddressID|  
|---------------|  
|1|  
|2|  
|3|  
|...|  
  
## <a name="select-value-and-select"></a>SELECT VALUE 및 SELECT  
  
### <a name="select-value"></a>SELECT VALUE  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 암시적 행 생성을 건너뛰도록 SELECT VALUE 절을 제공합니다. SELECT VALUE 절에는 하나의 항목만 지정할 수 있습니다. 이러한 절을 사용 하면 SELECT 절의 항목 주위에 행 래퍼가 생성 되지 않고 원하는 모양의 컬렉션이 생성 될 수 있습니다. 예를 들어 `SELECT VALUE a`입니다.  
  
 예:  
  
```sql  
SELECT VALUE p.Name FROM AdventureWorksEntities.Product AS p
```  
  
 출력:  
  
|이름|  
|----------|  
|Adjustable Race|  
|All-Purpose Bike Stand|  
|AWC Logo Cap|  
|...|  
  
### <a name="select"></a>SELECT  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)]에서는 임의의 행을 만드는 행 생성자도 제공합니다. SELECT는 `SELECT a, b, c`와 같이 프로젝션의 요소를 하나 이상 사용하며 필드가 있는 데이터 레코드를 생성합니다.  
  
 예:  
  
 SELECT p.Name, p.ProductID FROM AdventureWorksEntities.Product as p 출력:  
  
|이름|ProductID|  
|----------|---------------|  
|Adjustable Race|1|  
|All-Purpose Bike Stand|879|  
|AWC Logo Cap|712|  
|...|...|  
  
## <a name="case-expression"></a>CASE 식  
 [Case 식은](case-entity-sql.md) 부울 식 집합을 계산 하 여 결과를 확인 합니다.  
  
 예:  
  
```sql  
CASE WHEN AVG({25,12,11}) < 100 THEN TRUE ELSE FALSE END  
```  
  
 출력:  
  
|값|  
|-----------|  
|true|  
  
## <a name="see-also"></a>참조

- [엔터티 SQL 참조](entity-sql-reference.md)
- [Entity SQL 개요](entity-sql-overview.md)
