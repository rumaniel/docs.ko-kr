---
title: SQL Server에서 데이터베이스간 액세스 활성화
ms.date: 03/30/2017
ms.assetid: 10663fb6-434c-4c81-8178-ec894b9cf895
ms.openlocfilehash: f69a405a562bfae3bc283f2b3166812046be868e
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70794189"
---
# <a name="enabling-cross-database-access-in-sql-server"></a>SQL Server에서 데이터베이스간 액세스 활성화
데이터베이스 간 소유권 체인은 한 데이터베이스의 프로시저가 다른 데이터베이스의 개체에 종속되는 경우 발생합니다. 끊어지지 않은 소유권 체인에서는 모든 개체 소유자가 동일한 로그인 계정에 매핑되어야 한다는 점을 제외하고 데이터베이스 간 소유권 체인은 단일 데이터베이스 내의 소유권 체인과 같은 방식으로 작동합니다. 소스 데이터베이스의 소스 개체와 대상 데이터베이스의 대상 개체를 동일한 로그인 계정에서 소유하는 경우 SQL Server는 대상 개체의 권한을 확인하지 않습니다.  
  
## <a name="off-by-default"></a>기본적으로 활성화되지 않음  
 데이터베이스 간 소유권 체인은 기본적으로 해제되어 있습니다. Microsoft에서는 데이터베이스 간 소유권 체인이 다음과 같은 보안 위험에 노출되므로 데이터베이스 간 소유권 체인을 비활성화할 것을 권장합니다.  
  
- 데이터베이스 소유자 및 `db_ddladmin` 또는 `db_owners` 데이터베이스 역할의 멤버는 개체를 만들어 다른 사용자가 소유하도록 할 수 있습니다. 이러한 개체는 잠재적으로 다른 데이터베이스의 개체를 대상으로 합니다. 이것은 데이터베이스 간 소유권 체인을 활성화할 때 모든 데이터베이스의 데이터에 대해 이러한 사용자를 완전 신뢰한다는 의미입니다.  
  
- CREATE DATABASE 권한이 있는 사용자는 새 데이터베이스를 만들고 기존 데이터베이스에 연결할 수 있습니다. 데이터베이스 간 소유권 체인이 활성화되면 이러한 사용자는 새로 만들었거나 연결한 데이터베이스를 통해 권한이 없는 다른 데이터베이스의 개체에 액세스할 수 있습니다.  
  
## <a name="enabling-cross-database-ownership-chaining"></a>데이터베이스 간 소유권 체인 활성화  
 데이터베이스 간 소유권 체인은 권한이 높은 사용자를 완전 신뢰할 수 있는 환경에서만 활성화해야 합니다. 모든 데이터베이스에 대해 설정하는 동안 구성하거나 Transact-SQL 명령 `sp_configure` 및 `ALTER DATABASE`을 사용하는 특정 데이터베이스에 대해 선택적으로 구성할 수 있습니다.  
  
 데이터베이스 간 소유권 체인을 선택적으로 구성하려면 `sp_configure`를 사용하여 서버에 대해 이를 해제합니다. ALTER DATABASE 명령을 SET DB_CHAINING ON으로 사용하여 데이터베이스 간 소유권 체인을 해당 데이터베이스에 대해서만 구성합니다.  
  
 다음 샘플에서는 모든 데이터베이스에 대해 데이터베이스 간 소유권 체인을 설정합니다.  
  
```  
EXECUTE sp_configure 'show advanced', 1;  
RECONFIGURE;  
EXECUTE sp_configure 'cross db ownership chaining', 1;  
RECONFIGURE;  
```  
  
 다음 샘플에서는 특정 데이터베이스에 대해 데이터베이스 간 소유권 체인을 설정합니다.  
  
```  
ALTER DATABASE Database1 SET DB_CHAINING ON;  
ALTER DATABASE Database2 SET DB_CHAINING ON;  
```  
  
### <a name="dynamic-sql"></a>동적 SQL  
 데이터베이스 간 소유권 체인은 동일 사용자가 두 데이터베이스에 없는 경우 동적으로 생성된 SQL 문이 실행되는 환경에서는 동작하지 않습니다. SQL Server에서는 다른 데이터베이스의 데이터에 액세스하는 저장 프로시저를 만들고 두 데이터베이스 모두에 존재하는 인증서로 프로시저에 서명하여 이 문제를 피할 수 있습니다. 이렇게 하면 사용자에게 데이터베이스 액세스 또는 권한을 부여하지 않고 프로시저에서 사용되는 데이터베이스 리소스에 사용자가 액세스하도록 할 수 있습니다.  
  
## <a name="external-resources"></a>외부 리소스  
 자세한 내용은 다음 리소스를 참조하세요.  
  
|리소스|Description|  
|--------------|-----------------|  
|EXECUTE AS 및 [DB 간 소유권 체인 옵션](/sql/database-engine/configure-windows/cross-db-ownership-chaining-server-configuration-option)을 [사용 하 여 데이터베이스 가장을 확장](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms188304(v=sql.105)) 합니다.|문서에서는 SQL Server 인스턴스에 대 한 데이터베이스 간 소유권 체인을 구성 하는 방법을 설명 합니다.|  
  
## <a name="see-also"></a>참고자료

- [ADO.NET 응용 프로그램 보안](../securing-ado-net-applications.md)
- [SQL Server 보안 개요](overview-of-sql-server-security.md)
- [SQL Server에서 저장 프로시저를 사용하여 권한 관리](managing-permissions-with-stored-procedures-in-sql-server.md)
- [SQL Server에서 동적 보안 SQL 작성](writing-secure-dynamic-sql-in-sql-server.md)
- [SQL Server에서 저장 프로시저에 서명](signing-stored-procedures-in-sql-server.md)
- [ADO.NET 개요](../ado-net-overview.md)
