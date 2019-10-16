---
title: SQL Server에서 저장 프로시저를 사용하여 권한 관리
ms.date: 03/30/2017
ms.assetid: 08fa34e8-2ffa-470d-ba62-e511a5f8558e
ms.openlocfilehash: 412d2a0a292e2ac83e6c42cf721c83e63633408c
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70780958"
---
# <a name="managing-permissions-with-stored-procedures-in-sql-server"></a>SQL Server에서 저장 프로시저를 사용하여 권한 관리
데이터베이스 주변을 방어하는 여러 줄을 작성하는 한 가지 방법은 저장 프로시저 또는 사용자 정의 함수를 사용하여 모든 데이터 액세스를 구현하는 것입니다. 테이블과 같은 원본 개체에 대한 모든 권한을 취소하거나 거부하고 저장 프로시저에 EXECUTE 권한을 부여합니다. 그러면 효율적으로 데이터 및 데이터베이스 개체 주변에 보안 경계를 만듭니다.  
  
## <a name="stored-procedure-benefits"></a>저장 프로시저의 장점  
 저장 프로시저에는 다음과 같은 장점이 있습니다.  
  
- 데이터 논리 및 비즈니스 규칙을 캡슐화하여 개발자 및 데이터베이스 관리자가 의도하는 방식으로만 사용자가 데이터 및 개체에 액세스할 수 있습니다.  
  
- 모든 사용자 입력의 유효성을 확인하는 매개 변수화된 저장 프로시저를 사용하여 SQL 삽입 공격을 막을 수 있습니다. 동적 SQL을 사용하는 경우 명령을 매개 변수화하고 매개 변수 값을 쿼리 문자열에 직접 넣지 마세요.  
  
- 임시 쿼리 및 데이터 수정은 허용되지 않습니다. 실수로 또는 악의적으로 데이터를 파괴하거나 서버 또는 네트워크의 성능을 약화시키는 쿼리를 실행하지 못하도록 합니다.  
  
- 오류를 클라이언트 애플리케이션으로 직접 전달하지 않고 프로시저 코드에서 처리할 수 있습니다. 그러면 검색 공격을 도울 수 있는 오류 메시지가 반환되지 못합니다. 오류를 기록하고 서버에서 처리합니다.  
  
- 저장 프로시저는 한 번만 작성되어 여러 애플리케이션에서 액세스될 수 있습니다.  
  
- 클라이언트 애플리케이션에서는 내부 데이터 구조에 대해서는 몰라도 됩니다. 변경 내용이 매개 변수 목록 또는 반환된 데이터 형식에 영향을 미치지 않는 경우 클라이언트 애플리케이션에서 변경할 필요 없이 저장 프로시저 코드를 변경할 수 있습니다.  
  
- 여러 작업을 하나의 프로시저 호출로 결합하므로 저장 프로시저는 네트워크 트래픽을 줄여 줍니다.  
  
## <a name="stored-procedure-execution"></a>저장 프로시저 실행  
 저장 프로시저는 소유권 체인의 장점을 활용하여 데이터에 대한 액세스를 제공하므로 사용자는 데이터베이스 개체에 액세스하기 위해 명시적 권한을 가질 필요가 없습니다. 소유권 체인은 순차적으로 서로 액세스하는 개체가 동일한 사용자에 의해 소유될 때 발생합니다. 예를 들어 저장 프로시저가 다른 저장 프로시저를 호출할 수 있으며 여러 테이블에 액세스할 수 있습니다. 실행 체인에 있는 모든 개체의 소유자가 동일한 경우 SQL Server는 호출자의 다른 개체에 대한 권한이 아닌 호출자에 대한 EXECUTE 권한만 확인합니다. 따라서 저장 프로시저에 EXECUTE 권한만 부여해야 하며 원본 테이블에 대한 모든 권한을 취소하거나 거부할 수 있습니다.  
  
## <a name="best-practices"></a>최선의 구현 방법  
 저장 프로시저를 작성하는 것만으로 애플리케이션이 충분히 보호되는 것은 아닙니다. 다음과 같은 잠재적인 보안 허점을 고려해야 합니다.  
  
- 저장 프로시저에서 데이터에 액세스하려는 데이터베이스 역할에 대해 EXECUTE 권한을 부여합니다.  
  
- `public` 역할을 포함하여 데이터베이스의 모든 역할과 사용자에 대해 원본 테이블에 대한 모든 권한을 취소하거나 거부합니다. 모든 사용자는 public에서 권한을 상속합니다. 따라서 `public`에 대한 권한을 거부하면 소유자 및 `sysadmin` 멤버만 액세스할 수 있으며 다른 모든 사용자는 다른 역할의 멤버에서 권한을 상속할 수 없게 됩니다.  
  
- `sysadmin` 또는 `db_owner` 역할에 사용자 또는 역할을 추가하지 마세요. 시스템 관리자 및 데이터베이스 소유자가 모든 데이터베이스 개체에 액세스할 수 있습니다.  
  
- `guest` 계정을 비활성화합니다. 그러면 익명 사용자가 데이터베이스에 연결하지 못합니다. 새 데이터베이스에서 guest 계정은 기본적으로 비활성화됩니다.  
  
- 오류 처리를 구현하고 오류를 기록합니다.  
  
- 모든 사용자 입력의 유효성을 확인하는 매개 변수화된 저장 프로시저를 만듭니다. 모든 사용자 입력을 신뢰되지 않은 것으로 처리합니다.  
  
- 동적 SQL은 반드시 필요한 경우에만 사용하세요. 입력 문자열에서 문자열 값을 구분하고 구분 기호가 생기지 않도록 Transact-SQL QUOTENAME() 함수를 사용합니다.  
  
## <a name="external-resources"></a>외부 리소스  
 자세한 내용은 다음 리소스를 참조하세요.  
  
|리소스|설명|  
|--------------|-----------------|  
|[저장 프로시저](/sql/relational-databases/stored-procedures/stored-procedures-database-engine) 및 [SQL 삽입](https://go.microsoft.com/fwlink/?LinkId=98234)(SQL Server 온라인 설명서)|저장 프로시저를 만드는 방법과 SQL 삽입이 작동하는 방식을 설명하는 항목입니다.|  
  
## <a name="see-also"></a>참고자료

- [ADO.NET 응용 프로그램 보안](../securing-ado-net-applications.md)
- [SQL Server 보안 개요](overview-of-sql-server-security.md)
- [SQL Server의 응용 프로그램 보안 시나리오](application-security-scenarios-in-sql-server.md)
- [SQL Server에서 동적 보안 SQL 작성](writing-secure-dynamic-sql-in-sql-server.md)
- [SQL Server에서 저장 프로시저에 서명](signing-stored-procedures-in-sql-server.md)
- [SQL Server에서 가장으로 권한 사용자 지정](customizing-permissions-with-impersonation-in-sql-server.md)
- [저장 프로시저로 데이터 수정](../modifying-data-with-stored-procedures.md)
- [ADO.NET 개요](../ado-net-overview.md)
