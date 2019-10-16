---
title: SQL Server에서 가장으로 권한 사용자 지정
ms.date: 03/30/2017
ms.assetid: dc733d09-1d6d-4af0-9c4b-8d24504860f1
ms.openlocfilehash: b5dcef80afffa7bb3722a09020c5445dbc47f16a
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70782476"
---
# <a name="customizing-permissions-with-impersonation-in-sql-server"></a>SQL Server에서 가장으로 권한 사용자 지정
많은 수의 애플리케이션에서 저장 프로시저를 사용하여 데이터에 액세스하며, 이 경우 소유권 체인을 사용하여 액세스를 기본 테이블로 제한합니다. 저장 프로시저에 EXECUTE 권한을 부여하고 기본 테이블에 대한 권한을 취소하거나 거부할 수 있습니다. SQL Server에서는 저장 프로시저 및 테이블의 소유자가 동일한 경우 호출자의 권한을 확인하지 않습니다. 그러나 개체의 소유자가 다른 경우 또는 동적 SQL의 경우에는 소유권 체인이 작동하지 않습니다.  
  
 참조되는 데이터베이스 개체에 대한 권한이 호출자에게 없을 때 저장 프로시저에 EXECUTE AS 절을 사용할 수 있습니다. EXECUTE AS 절의 효과는 실행 컨텍스트가 프록시 사용자로 전환된다는 것입니다. 중첩된 저장 프로시저나 트리거에 대한 모든 호출 및 모든 코드는 프록시 사용자의 보안 컨텍스트에서 실행됩니다. 실행 컨텍스트는 프로시저 실행 후 또는 REVERT 문이 실행될 때만 원래 호출자로 되돌아갑니다.  
  
## <a name="context-switching-with-the-execute-as-statement"></a>EXECUTE AS 문을 사용하여 컨텍스트 전환  
 Transact-SQL의 EXECUTE AS 문을 사용하면 다른 로그인 또는 데이터베이스 사용자를 가장하여 문의 실행 컨텍스트를 전환할 수 있습니다. 이 방법은 쿼리와 프로시저를 다른 사용자로 테스트할 때 유용합니다.  
  
```  
EXECUTE AS LOGIN = 'loginName';  
EXECUTE AS USER = 'userName';  
```  
  
 현재 가장하고 있는 로그인 또는 사용자에 대해 IMPERSONATE 권한이 있어야 합니다. 이 권한은 모든 데이터베이스에 대해 `sysadmin` 권한이 있고 소유한 데이터베이스에서 `db_owner` 역할 멤버인 것을 의미합니다.  
  
## <a name="granting-permissions-with-the-execute-as-clause"></a>EXECUTE AS 절을 사용하여 권한 부여  
 저장 프로시저, 트리거 또는 사용자 정의 함수(인라인 테이블 반환 함수 제외)의 정의 헤더에 EXECUTE AS 절을 사용할 수 있습니다. 이렇게 하면 사용자 이름 또는 EXECUTE AS 절에 지정된 키워드의 컨텍스트에서 프로시저를 실행할 수 있습니다. 로그인에 매핑되지 않은 데이터베이스에 프록시 사용자를 만들고 프로시저가 액세스하는 개체에 대해 필요한 권한만 부여할 수 있습니다. EXECUTE AS 절에 지정된 프록시 사용자에게만 모듈에서 액세스하는 모든 개체에 대한 권한이 부여되어야 합니다.  
  
> [!NOTE]
> TRUNCATE TABLE과 같은 일부 작업에는 부여할 수 있는 권한이 없습니다. 문을 프로시저 내에 포함하고 ALTER TABLE 권한이 있는 사용자를 지정하면 테이블을 자르는 권한을 프로시저에 대해 EXECUTE 권한만 가진 호출자로 확장할 수 있습니다.  
  
 EXECUTE AS 절에 지정된 컨텍스트는 중첩된 프로시저 및 트리거를 포함하여 프로시저의 실행 기간 동안 유효합니다. 실행이 완료되거나 REVERT 문이 실행되면 컨텍스트가 호출자에게 되돌아갑니다.  
  
 프로시저에서 EXECUTE AS 절을 사용할 때는 다음 세 단계를 수행합니다.  
  
1. 로그인에 매핑되지 않는 데이터베이스에 프록시 사용자를 만듭니다. 이 단계는 필수 사항은 아니지만 권한 관리에 도움이 됩니다.  
  
```  
CREATE USER proxyUser WITHOUT LOGIN  
```  
  
1. 프록시 사용자에게 필요한 권한을 부여합니다.  
  
2. 저장 프로시저 또는 사용자 정의 함수에 EXECUTE AS 절을 추가합니다.  
  
```  
CREATE PROCEDURE [procName] WITH EXECUTE AS 'proxyUser' AS ...  
```  
  
> [!NOTE]
> 호출자의 원래 보안 컨텍스트가 유지되지 않기 때문에 감사가 필요한 애플리케이션은 중단될 수 있습니다. SESSION_USER, USER 또는 USER_NAME과 같이 현재 사용자의 ID를 반환하는 기본 제공 함수는 원래 호출자가 아니라 EXECUTE AS 절과 연관된 사용자를 반환합니다.  
  
### <a name="using-execute-as-with-revert"></a>REVERT와 함께 EXECUTE AS 사용  
 Transact-SQL REVERT 문을 사용하여 원래 실행 컨텍스트로 되돌아갈 수 있습니다.  
  
 선택적 절 (NO REVERT COOKIE = @variableName)을 사용 하면 @variableName 변수에 올바른 값이 포함 된 경우 실행 컨텍스트를 다시 호출자로 전환할 수 있습니다. 이를 통해 연결 풀링이 사용되는 환경에서 실행 컨텍스트를 다시 호출자로 전환할 수 있습니다. 의 @variableName 값은 EXECUTE AS 문의 호출자 에게만 알려져 있으므로 호출자는 응용 프로그램을 호출 하는 최종 사용자가 실행 컨텍스트를 변경할 수 없도록 보장할 수 있습니다. 연결이 닫히면 연결은 풀로 반환됩니다. ADO.NET의 연결 풀링에 대 한 자세한 내용은 [연결 풀링 (ADO.NET) SQL Server](../sql-server-connection-pooling.md)을 참조 하세요.  
  
### <a name="specifying-the-execution-context"></a>실행 컨텍스트 지정  
 사용자 지정 외에도 EXECUTE AS는 다음 키워드와 함께 사용할 수 있습니다.  
  
- CALLER. 기본적으로 CALLER로 실행됩니다. 다른 옵션을 지정하지 않으면 프로시저는 호출자의 보안 컨텍스트에서 실행됩니다.  
  
- OWNER. OWNER로 실행할 경우 프로시저는 프로시저 소유자의 컨텍스트에서 실행됩니다. `dbo` 또는 데이터베이스 소유자가 소유한 스키마에서 만들어진 프로시저는 무제한 권한으로 실행됩니다.  
  
- SELF. SELF로 실행할 경우 저장 프로시저 작성자의 보안 컨텍스트에서 실행됩니다. 지정된 사용자로 실행하는 것과 같으며, 여기서 지정된 사용자는 프로시저를 만들거나 변경하는 사용자입니다.  
  
## <a name="see-also"></a>참고자료

- [ADO.NET 응용 프로그램 보안](../securing-ado-net-applications.md)
- [SQL Server 보안 개요](overview-of-sql-server-security.md)
- [SQL Server의 응용 프로그램 보안 시나리오](application-security-scenarios-in-sql-server.md)
- [SQL Server에서 저장 프로시저를 사용하여 권한 관리](managing-permissions-with-stored-procedures-in-sql-server.md)
- [SQL Server에서 동적 보안 SQL 작성](writing-secure-dynamic-sql-in-sql-server.md)
- [SQL Server에서 저장 프로시저에 서명](signing-stored-procedures-in-sql-server.md)
- [저장 프로시저로 데이터 수정](../modifying-data-with-stored-procedures.md)
- [ADO.NET 개요](../ado-net-overview.md)
