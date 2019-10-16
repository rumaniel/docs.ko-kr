---
title: Entity SQL 언어
ms.date: 03/30/2017
ms.assetid: 9e7d8837-28c5-429d-a824-7bafb59724cf
ms.openlocfilehash: a2e4b7245dbfccf7864481b52a0e868a85efbca6
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70251010"
---
# <a name="entity-sql-language"></a>Entity SQL 언어
Entity SQL은 SQL과 유사한 스토리지 독립적 쿼리 언어입니다. Entity SQL을 사용하면 엔터티 데이터를 개체 또는 테이블 형식으로 쿼리할 수 있습니다. Entity SQL은 다음의 경우에 사용해야 합니다.  
  
- 쿼리를 동적으로 런타임에 생성해야 하는 경우. 이 경우에는 런타임에 Entity SQL 쿼리 문자열을 생성하는 대신 <xref:System.Data.Objects.ObjectQuery%601>의 쿼리 작성기 메서드를 사용해야 합니다.  
  
- 쿼리를 모델 정의의 일부로 정의할 경우. Entity SQL만 데이터 모델에서 지원됩니다. 자세한 내용은 [QueryView 요소 (MSL)](/ef/ef6/modeling/designer/advanced/edmx/msl-spec#queryview-element-msl) 를 참조 하세요.  
  
- EntityClient에서 <xref:System.Data.EntityClient.EntityDataReader>를 사용하여 읽기 전용 엔터티 데이터를 행 집합으로 반환할 경우. 자세한 내용은 [Entity Framework에 대 한 EntityClient 공급자](../entityclient-provider-for-the-entity-framework.md)를 참조 하세요.  
  
- SQL 기반 쿼리 언어의 전문가에게는 Entity SQL이 가장 편할 수 있습니다.  
  
## <a name="using-entity-sql-with-the-entityclient-provider"></a>EntityClient 공급자와 함께 Entity SQL 사용  
 EntityClient 공급자와 함께 Entity SQL을 사용하려는 경우 자세한 내용은 다음 항목을 참조하세요.  
  
 [Entity Framework용 EntityClient 공급자](../entityclient-provider-for-the-entity-framework.md)  
  
 [방법: EntityConnection 연결 문자열 작성](../how-to-build-an-entityconnection-connection-string.md)  
  
 [방법: PrimitiveType 결과를 반환 하는 쿼리 실행](../how-to-execute-a-query-that-returns-primitivetype-results.md)  
  
 [방법: StructuralType 결과를 반환 하는 쿼리 실행](../how-to-execute-a-query-that-returns-structuraltype-results.md)  
  
 [방법: RefType 결과를 반환 하는 쿼리 실행](../how-to-execute-a-query-that-returns-reftype-results.md)  
  
 [방법: 복합 형식을 반환 하는 쿼리 실행](../how-to-execute-a-query-that-returns-complex-types.md)  
  
 [방법: 중첩 컬렉션을 반환 하는 쿼리 실행](../how-to-execute-a-query-that-returns-nested-collections.md)  
  
 [방법: EntityCommand를 사용 하 여 매개 변수가 있는 Entity SQL 쿼리 실행](../how-to-execute-a-parameterized-entity-sql-query-using-entitycommand.md)  
  
 [방법: EntityCommand를 사용 하 여 매개 변수가 있는 저장 프로시저 실행](../how-to-execute-a-parameterized-stored-procedure-using-entitycommand.md)  
  
 [방법: 다형 쿼리 실행](../how-to-execute-a-polymorphic-query.md)  
  
 [방법: Navigate 연산자를 사용 하 여 관계 탐색](../how-to-navigate-relationships-with-the-navigate-operator.md)  
  
## <a name="using-entity-sql-with-object-queries"></a>개체 쿼리와 함께 Entity SQL 사용  
 개체 쿼리와 함께 Entity SQL을 사용하려는 경우 자세한 내용은 다음 항목을 참조하세요.  
  
 [방법: 엔터티 형식 개체를 반환 하는 쿼리 실행](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738694(v=vs.100))  
  
 [방법: 매개 변수가 있는 쿼리 실행](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738521(v=vs.100))  
  
 [방법: 탐색 속성을 사용 하 여 관계 탐색](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896321(v=vs.100))  
  
 [방법: 사용자 정의 함수 호출](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dd490951(v=vs.100))  
  
 [방법: 데이터 필터링](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/cc716755(v=vs.100))  
  
 [방법: 데이터 정렬](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/cc716784(v=vs.100))  
  
 [방법: 데이터 그룹화](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896341(v=vs.100))  
  
 [방법: 데이터 집계](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/cc716738(v=vs.100))  
  
 [방법: 익명 형식 개체를 반환 하는 쿼리 실행](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738512(v=vs.100))  
  
 [방법: 기본 형식의 컬렉션을 반환 하는 쿼리 실행](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738451(v=vs.100))  
  
 [방법: EntityCollection에서 관련 개체 쿼리](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/cc716708(v=vs.100))  
  
 [방법: 두 쿼리의 합집합 순서](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896299(v=vs.100))  
  
 [방법: 쿼리 결과를 통한 페이지](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738702(v=vs.100))  
  
## <a name="in-this-section"></a>섹션 내용  
 [Entity SQL 개요](entity-sql-overview.md)  
  
 [엔터티 SQL 참조](entity-sql-reference.md)  
  
## <a name="see-also"></a>참고자료

- [ADO.NET Entity Framework](../index.md)
- [언어 참조](index.md)
