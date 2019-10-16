---
title: SQL 생성
ms.date: 03/30/2017
ms.assetid: 0e16aa02-d458-4418-a765-58b42aad9315
ms.openlocfilehash: 9c5301d3f4d5bc2e0db4a138c6d8ceb06d3a7845
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854362"
---
# <a name="sql-generation"></a>SQL 생성
Entity Framework에 대 한 공급자를 작성 하는 경우 Entity Framework 명령 트리를 특정 데이터베이스가 이해할 수 있는 SQL로 변환 해야 합니다. 예를 들어 Transact-sql은 SQL Server 또는 PL/SQL for Oracle입니다. 이 섹션에서는 Entity Framework 공급자에 대해 SQL 생성 구성 요소 (SELECT 쿼리에 대 한)를 개발 하는 방법에 대해 설명 합니다. Insert, update 및 delete 쿼리에 대 한 자세한 내용은 [수정 SQL 생성](modification-sql-generation.md)을 참조 하십시오.  
  
 이 섹션을 이해 하려면 Entity Framework 및 ADO.NET 공급자 모델에 대해 잘 알고 있어야 합니다. 또한 명령 트리와 <xref:System.Data.Common.CommandTrees.DbExpression>도 이해해야 합니다.  
  
## <a name="the-role-of-the-sql-generation-module"></a>SQL 생성 모듈의 역할  
 Entity Framework 공급자의 SQL 생성 모듈은 지정 된 쿼리 명령 트리를 SQL: 1999 규격 데이터베이스를 대상으로 하는 단일 SQL SELECT 문으로 변환 합니다. 생성된 SQL에는 중첩 쿼리가 가능한 한 적게 포함되어야 합니다. SQL 생성 모듈은 출력 쿼리 명령 트리를 단순화하지 않아야 합니다. 예를 들어 조인을 제거 하 고 연속 필터 노드를 축소 하 여이 작업을 수행 합니다. Entity Framework  
  
 <xref:System.Data.Common.DbProviderServices> 클래스는 <xref:System.Data.Common.DbCommand>로 명령 트리를 변환하기 위해 SQL 생성 계층에 액세스할 수 있는 시작점입니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [명령 트리의 모양](the-shape-of-the-command-trees.md)  
  
 [명령 트리에서 SQL 생성 - 최선의 방법](generating-sql-from-command-trees-best-practices.md)  
  
 [샘플 공급자의 SQL 생성](sql-generation-in-the-sample-provider.md)  
  
## <a name="see-also"></a>참고자료

- [Entity Framework 데이터 공급자 작성](writing-an-ef-data-provider.md)
