---
title: Entity Framework용 SqlClient에서 알려진 문제
ms.date: 03/30/2017
ms.assetid: 48fe4912-4d0f-46b6-be96-3a42c54780f6
ms.openlocfilehash: 18e3ad59af4014086bd475815011b6008bcb5052
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854556"
---
# <a name="known-issues-in-sqlclient-for-entity-framework"></a>Entity Framework용 SqlClient에서 알려진 문제
이 단원에서는 .NET Framework Data Provider for SQL Server(SqlClient)와 관련된 알려진 문제에 대해 설명합니다.  
  
## <a name="trailing-spaces-in-string-functions"></a>문자열 함수의 후행 공백  
 SQL Server는 문자열 값에서 후행 공백을 무시 합니다. 따라서 문자열에 후행 공백을 전달 하면 오류가 발생할 때까지 예측할 수 없는 결과가 발생할 수 있습니다.  
  
 문자열에 후행 공백이 있어야 하는 경우에는 SQL Server에서 문자열을 자르지 않도록 끝에 공백 문자를 추가 하는 것을 고려해 야 합니다. 후행 공백이 필요하지 않은 경우 쿼리 파이프라인을 통해 전달하기 전에 트리밍해야 합니다.  
  
## <a name="right-function"></a>RIGHT 함수  
 `null`이 아닌 값을 첫 번째 인수, 0을 두 번째 인수로 `RIGHT(nvarchar(max)`, 0`)` 또는 `RIGHT(varchar(max)`, 0`)`에 전달하면 `NULL` 문자열 대신 `empty` 값이 반환됩니다.  
  
## <a name="cross-and-outer-apply-operators"></a>CROSS 및 OUTER APPLY 연산자  
 CROSS 및 OUTER APPLY 연산자는 SQL Server 2005에서 도입 되었습니다. 경우에 따라 쿼리 파이프라인은 CROSS APPLY 및/또는 OUTER APPLY 연산자가 포함 된 Transact-sql 문을 생성할 수 있습니다. SQL Server 2005 이전 SQL Server 버전을 비롯 한 일부 백엔드 공급자는 이러한 연산자를 지원 하지 않으므로 이러한 백 엔드 공급자에서는 이러한 쿼리를 실행할 수 없습니다.  
  
 다음은 출력 쿼리에 CROSS APPLY 및/또는 OUTER APPLY 연산자가 포함될 수 있는 일반적인 시나리오입니다.  
  
- 페이징이 있는 상호 관련된 하위 쿼리  
  
- 상호 관련된 하위 쿼리 또는 탐색으로 생성된 컬렉션에 대한 `AnyElement`  
  
- 요소 선택기를 허용하는 그룹화 메서드를 사용하는 LINQ 쿼리  
  
- CROSS APPLY 또는 OUTER APPLY가 명시적으로 지정된 쿼리  
  
- REF 구문보다 DEREF 구문을 우선 적용하는 쿼리  
  
## <a name="skip-operator"></a>SKIP 연산자  
 SQL Server 2000를 사용 하는 경우 키가 아닌 열에 ORDER BY와 함께 SKIP을 사용 하면 잘못 된 결과가 반환 될 수 있습니다. 키가 아닌 열에 중복 데이터가 있는 경우, 지정된 개수 이상의 행을 건너뛸 수 있습니다. 이는 SQL Server 2000에 대해 SKIP이 변환 되기 때문입니다. 예를 들어 다음 쿼리에서 `E.NonKeyColumn`에 중복 값이 있으면 5개가 넘는 행을 건너뛸 수 있습니다.  
  
```  
SELECT [E] FROM Container.EntitySet AS [E] ORDER BY [E].[NonKeyColumn] DESC SKIP 5L  
```  
  
## <a name="targeting-the-correct-sql-server-version"></a>올바른 SQL Server 버전을 대상으로 지정  
 Entity Framework는 저장소 모델 파일 (ssdl)에 있는 Schema 요소의 `ProviderManifestToken` 특성에 지정 된 SQL Server 버전에 따라 transact-sql 쿼리를 대상으로 합니다. 이 버전은 연결된 실제 SQL Server의 버전과 다를 수 있습니다. 예를 들어 SQL Server 2005를 사용 하지만 `ProviderManifestToken` 특성이 2008로 설정 된 경우 생성 된 transact-sql 쿼리가 서버에서 실행 되지 않을 수 있습니다. 예를 들어 SQL Server 2008에 도입 된 새 날짜 시간 형식을 사용 하는 쿼리는 이전 버전의 SQL Server에서 실행 되지 않습니다. SQL Server 2005를 사용 하지만 `ProviderManifestToken` 특성이 2000로 설정 되어 있으면 생성 된 transact-sql 쿼리가 더 이상 최적화 되지 않을 수 있습니다. 그렇지 않으면 쿼리가 지원 되지 않는다는 예외가 발생할 수 있습니다. 자세한 내용은이 항목의 앞부분에 나오는 CROSS 및 OUTER APPLY 연산자 섹션을 참조 하세요.  
  
 특정 데이터베이스 동작은 데이터베이스로 설정된 호환성 수준에 따라 달라집니다. `ProviderManifestToken` 특성을 2005로 설정 하 고 SQL Server 버전이 2005 이지만 데이터베이스의 호환성 수준이 "80" (SQL Server 2000)로 설정 된 경우 생성 된 transact-sql은 SQL Server 2005를 대상으로 지정 하지만 호환성 수준 설정입니다. 예를 들어, ORDER BY 목록의 열 이름이 선택기의 열 이름과 일치하는 경우 정렬 정보가 손실될 수 있습니다.  
  
## <a name="nested-queries-in-projection"></a>프로젝션의 중첩 쿼리  
 프로젝션 절의 중첩 쿼리는 서버의 Cartesian 제품 쿼리로 변환될 수 있습니다. SLQ Server를 비롯 한 일부 백 엔드 서버에서는 TempDB 테이블이 매우 커질 수 있습니다. 서버 성능이 저하될 수 있습니다.  
  
 다음은 프로젝션 절의 중첩 쿼리 예제입니다.  
  
```  
SELECT c, (SELECT c, (SELECT c FROM AdventureWorksModel.Vendor AS c  ) As Inner2 FROM AdventureWorksModel.JobCandidate AS c  ) As Inner1 FROM AdventureWorksModel.EmployeeDepartmentHistory AS c  
```  
  
## <a name="server-generated-guid-identity-values"></a>서버에서 생성된 GUID ID 값  
 Entity Framework는 서버에서 생성 된 GUID 형식 id 값을 지원 하지만, 공급자는 행이 삽입 된 후 서버에서 생성 된 id 값의 반환을 지원 해야 합니다. SQL Server 2005부터 [OUTPUT 절](https://go.microsoft.com/fwlink/?LinkId=169400) 을 통해 SQL Server 데이터베이스에서 서버에서 생성 된 GUID 형식을 반환할 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- [Entity Framework용 SqlClient](sqlclient-for-the-entity-framework.md)
- [LINQ to Entities에서 알려진 문제 및 고려 사항](./language-reference/known-issues-and-considerations-in-linq-to-entities.md)
