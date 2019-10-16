---
title: SQL Server에서 동적 보안 SQL 작성
ms.date: 03/30/2017
ms.assetid: df5512b0-c249-40d2-82f9-f9a2ce6665bc
ms.openlocfilehash: c02455ba8798df1de1d52f6b4db3426d41b95daf
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70791414"
---
# <a name="writing-secure-dynamic-sql-in-sql-server"></a>SQL Server에서 동적 보안 SQL 작성
SQL 삽입은 악의적 사용자가 유효한 입력 대신 Transact-SQL 문을 입력하는 데 사용하는 프로세스입니다. 이러한 공격으로 인해 입력이 유효성 검사를 거치지 않고 서버로 직접 전달되고 애플리케이션이 삽입된 코드를 실행하면 데이터가 손상되거나 제거될 수 있습니다.  
  
 SQL Server는 구문상 유효한 쿼리가 수신되면 모두 실행하기 때문에 SQL 문을 생성하는 모든 프로시저에 삽입 취약성이 있는지 검토해야 합니다. 매개 변수화된 데이터인 경우에도 숙련된 공격자에 의해 조작될 가능성이 있습니다. 동적 SQL을 사용하는 경우 쿼리 문자열에는 매개 변수 값을 직접 포함하지 않도록 하고 명령은 매개 변수화해야 합니다.  
  
## <a name="anatomy-of-a-sql-injection-attack"></a>SQL 삽입 공격 분석  
 삽입 프로세스는 텍스트 문자열을 중간에 종료하고 새 명령을 추가하는 방식으로 작동합니다. 삽입된 명령에는 실행되기 전에 추가된 문자열이 있을 수 있으므로 공격자는 주석 표시("--")를 사용하여 삽입된 문자열을 종료합니다. 이후 텍스트는 실행 시 무시됩니다. 세미콜론(;) 구분 기호를 사용하여 여러 명령을 삽입할 수 있습니다.  
  
 삽입된 SQL 코드가 구문상 올바른 경우 프로그래밍 방식으로는 훼손 여부를 찾아낼 수 없습니다. 따라서 모든 사용자 입력의 유효성을 검사하고 생성된 SQL 명령을 현재 사용 중인 서버에서 실행하는 코드를 신중하게 검토해야 합니다. 유효성을 검사하지 않은 사용자 입력은 연결하지 마세요. 문자열 연결은 스크립트 삽입 공격의 기본적인 대상이 됩니다.  
  
 다음은 몇 가지 유용한 지침입니다.  
  
- Transact-SQL 문을 사용자 입력에서 직접 빌드하지 않고 저장 프로시저를 사용하여 사용자 입력의 유효성을 검사합니다.  
  
- 유형, 길이, 형식 및 범위를 테스트하여 사용자 입력의 유효성을 검사합니다. Transact-SQL QUOTENAME() 함수를 사용하여 시스템 이름을 이스케이프하거나 REPLACE() 함수를 사용하여 문자열의 모든 문자를 이스케이프합니다.  
  
- 애플리케이션의 각 계층에서 여러 단계의 유효성 검사를 구현합니다.  
  
- 입력의 크기와 데이터 형식을 테스트하고 적절한 제한을 적용합니다. 이렇게 하면 의도적인 버퍼 오버런을 방지할 수 있습니다.  
  
- 문자열 변수의 내용을 테스트하고 예상된 값만 허용합니다. 이진 데이터, 이스케이프 시퀀스 및 주석 문자가 있는 항목은 거부합니다.  
  
- XML 문서를 사용할 때는 입력되는 모든 데이터를 스키마와 비교하여 유효성을 검사합니다.  
  
- 다중 계층 환경에서는 신뢰할 수 있는 영역으로 들어가는 모든 데이터의 유효성을 검사해야 합니다.  
  
- 파일 이름을 생성 하는 데 사용할 수 있는 필드에는 다음 문자열을 허용 하지 않습니다. AUX, CLOCK $, COM1 ~ COM8, CON, CONFIG $, LPT1 ~ LPT8, NUL, PRN.  
  
- <xref:System.Data.SqlClient.SqlParameter> 개체를 저장 프로시저 및 명령과 함께 사용하여 형식 검사와 길이 유효성 검사를 제공합니다.  
  
- 클라이언트 코드에 <xref:System.Text.RegularExpressions.Regex> 식을 사용하여 유효하지 않은 문자를 필터링합니다.  
  
## <a name="dynamic-sql-strategies"></a>동적 SQL 전략  
 동적으로 생성된 SQL 문을 절차적 코드에서 실행하면 소유권 체인이 끊어져서 SQL Server는 동적 SQL에서 액세스하는 개체에 대해 호출자의 권한을 확인합니다.  
  
 SQL Server에서는 동적 SQL을 실행하는 사용자 정의 함수 및 저장 프로시저를 사용하여 사용자에게 데이터에 대한 액세스 권한을 부여하는 방법이 도입되었습니다.  
  
- [SQL Server에서 가장으로 권한 사용자 지정](customizing-permissions-with-impersonation-in-sql-server.md)에 설명된 대로 Transact-SQL EXECUTE AS 절과 함께 가장을 사용합니다.  
  
- [SQL Server에서 저장 프로시저에 서명](signing-stored-procedures-in-sql-server.md)에 설명된 대로 인증서로 저장 프로시저를 서명합니다.  
  
### <a name="execute-as"></a>EXECUTE AS  
 EXECUTE AS 절은 호출자의 권한을 EXECUTE AS 절에 지정된 사용자의 권한으로 바꿉니다. 중첩된 저장 프로시저 또는 트리거는 프록시 사용자의 보안 컨텍스트에서 실행됩니다. 이로 인해 행 수준 보안을 사용하거나 감사가 필요한 애플리케이션이 중단될 수 있습니다. 사용자의 ID를 반환하는 일부 함수는 원래 호출자가 아니라 EXECUTE AS 절에 지정된 사용자를 반환합니다. 실행 컨텍스트는 프로시저 실행 후 또는 REVERT 문이 실행될 때만 원래 호출자로 되돌아갑니다.  
  
### <a name="certificate-signing"></a>인증서 서명  
 인증서로 서명된 저장 프로시저가 실행될 때는 인증서 사용자에게 부여된 권한이 호출자의 권한과 병합됩니다. 실행 컨텍스트는 동일하게 유지되고 인증서 사용자는 호출자를 가장하지 않습니다. 저장 프로시저에 서명하려면 몇 가지 단계를 구현해야 합니다. 프로시저가 수정될 때마다 다시 서명해야 합니다.  
  
### <a name="cross-database-access"></a>데이터베이스 간 액세스  
 동적으로 생성된 SQL 문이 실행되는 경우에는 데이터베이스 간 소유권 체인이 작동하지 않습니다. SQL Server에서는 다른 데이터베이스의 데이터에 액세스하는 저장 프로시저를 만들고 두 데이터베이스 모두에 존재하는 인증서로 프로시저에 서명하여 이 문제를 피할 수 있습니다. 이렇게 하면 사용자에게 데이터베이스 액세스 또는 권한을 부여하지 않고 프로시저에서 사용되는 데이터베이스 리소스에 사용자가 액세스하도록 할 수 있습니다.  
  
## <a name="external-resources"></a>외부 리소스  
 자세한 내용은 다음 리소스를 참조하세요.  
  
|리소스|Description|  
|--------------|-----------------|  
|[저장 프로시저](/sql/relational-databases/stored-procedures/stored-procedures-database-engine) 및 [SQL 삽입](/sql/relational-databases/security/sql-injection)(SQL Server 온라인 설명서)|저장 프로시저를 만드는 방법과 SQL 삽입이 작동하는 방식을 설명하는 항목입니다.|  
  
## <a name="see-also"></a>참고자료

- [ADO.NET 응용 프로그램 보안](../securing-ado-net-applications.md)
- [SQL Server 보안 개요](overview-of-sql-server-security.md)
- [SQL Server의 응용 프로그램 보안 시나리오](application-security-scenarios-in-sql-server.md)
- [SQL Server에서 저장 프로시저를 사용하여 권한 관리](managing-permissions-with-stored-procedures-in-sql-server.md)
- [SQL Server에서 저장 프로시저에 서명](signing-stored-procedures-in-sql-server.md)
- [SQL Server에서 가장으로 권한 사용자 지정](customizing-permissions-with-impersonation-in-sql-server.md)
- [ADO.NET 개요](../ado-net-overview.md)
