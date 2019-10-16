---
title: SQL Server의 애플리케이션 보안 시나리오
ms.date: 03/30/2017
ms.assetid: 0164f3a4-406e-4693-bec3-03c8e18b46d7
ms.openlocfilehash: bf844f35a3504af52cdb6bf745862ad5098dfc5f
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70782698"
---
# <a name="application-security-scenarios-in-sql-server"></a>SQL Server의 애플리케이션 보안 시나리오
안전한 SQL Server 클라이언트 애플리케이션을 만드는 방법이 정확하게 한 가지만 존재하지는 않습니다. 모든 애플리케이션은 요구 사항, 배포 환경 및 사용자 집단에 따라 고유합니다. 초기에 배포했을 때에는 비교적 안전했던 애플리케이션도 시간이 지남에 따라 안전하지 못할 수 있습니다. 앞으로 생길 수 있는 위협을 정확히 예측하는 것은 불가능합니다.  
  
 SQL Server 제품은 개발자가 안전한 데이터베이스 애플리케이션을 만들 수 있도록 최신의 보안 기능을 통합한 여러 버전으로 발전하고 있습니다. 그러나 보안을 한 번에 해결할 수는 없으며 계속적으로 모니터링하고 업데이트해야 합니다.  
  
## <a name="common-threats"></a>일반적인 위협  
 개발자는 보안 위협, 이에 직면하기 위해 제공하는 도구 및 자초한 보안 허점을 피하는 방법을 이해해야 합니다. 한 연결 부분이 손상되면 전체 강도에 영향을 미친다는 점에서 보안은 체인에 비유할 수 있습니다. 다음 표에는 일반적인 보안 위협이 들어 있으며 이 단원의 항목에서 보다 상세히 설명됩니다.  
  
### <a name="sql-injection"></a>SQL 삽입  
 SQL 삽입은 악의적 사용자가 유효한 입력 대신 Transact-SQL 문을 입력하는 데 사용하는 프로세스입니다. 입력이 유효성 검사를 거치지 않고 서버로 직접 전달되고 우연히 애플리케이션에서 삽입된 코드를 실행하면 공격으로 인해 데이터가 손상되거나 제거될 수 있습니다. 저장 프로시저와 매개 변수화된 명령을 사용하면 동적 SQL을 방지하고 모든 사용자에 대한 권한을 제한하므로 SQL Server 삽입 공격을 막을 수 있습니다.  
  
### <a name="elevation-of-privilege"></a>권한 높이기  
 권한 높이기 공격은 사용자가 소유자 또는 관리자와 같이 신뢰할 수 있는 계정 권한이 있는 것처럼 가정할 때 발생합니다. 항상 최소 권한 사용자 계정에서 실행해야 하고 반드시 필요한 권한만 할당하세요. 실행 코드에 대해서는 관리자 또는 소유자 계정을 사용하지 마세요. 그러면 공격이 성공하더라도 발생할 수 있는 손상 정도가 제한됩니다. 추가 권한이 필요한 작업을 수행하는 경우 작업 기간 동안에만 프로시저 서명 또는 가장을 사용하세요. 인증서를 사용하여 저장 프로시저에 서명하거나 가장을 사용하여 임시로 권한을 할당할 수 있습니다.  
  
### <a name="probing-and-intelligent-observation"></a>검색 및 지능형 관찰  
 검색 공격에서는 보안 취약성을 찾기 위해 애플리케이션에서 생성되는 오류 메시지를 사용할 수 있습니다. SQL Server 오류 정보가 최종 사용자에게 반환되지 않도록 하기 위해 모든 절차의 코드에서 오류 처리를 구현합니다.  
  
### <a name="authentication"></a>인증  
 SQL Server 로그인을 사용할 때 사용자 입력 기반의 연결 문자열이 런타임에 생성되는 경우 연결 문자열 삽입 공격이 발생할 수 있습니다. 유효한 키워드 쌍에 대해 연결 문자열을 확인하지 않는 경우 공격자는 추가 문자를 삽입하여 서버의 중요 데이터 또는 기타 리소스에 액세스할 수도 있습니다. 가능한 경우 Windows 인증을 사용합니다. SQL Server 로그인을 사용해야 하는 경우 <xref:System.Data.SqlClient.SqlConnectionStringBuilder>를 사용하여 런타임에 연결 문자열을 만들고 유효성을 확인합니다.  
  
### <a name="passwords"></a>암호  
 공격자는 권한 있는 사용자의 암호를 가져오거나 추측할 수 있으므로 많은 공격에서 성공합니다. 암호는 공격자에 대한 첫 번째 방어선이므로 강력한 암호 설정은 시스템 보안의 필수적인 조건입니다. 혼합 모드 인증에 대한 암호 정책을 만들고 적용하세요.  
  
 Windows 인증을 사용하는 경우에도 항상 `sa` 계정에 대해 강력한 암호를 할당하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
 [SQL Server에서 저장 프로시저를 사용하여 권한 관리](managing-permissions-with-stored-procedures-in-sql-server.md)  
 저장 프로시저를 사용하여 권한을 관리하고 데이터 액세스를 제어하는 방법에 대해 설명합니다. 저장 프로시저 사용은 여러 보안 위협에 대응하는 효율적인 방법입니다.  
  
 [SQL Server에서 동적 보안 SQL 작성](writing-secure-dynamic-sql-in-sql-server.md)  
 저장 프로시저를 사용하여 안전한 동적 SQL을 작성하는 기술에 대해 설명합니다.  
  
 [SQL Server에서 저장 프로시저에 서명](signing-stored-procedures-in-sql-server.md)  
 사용자가 직접 액세스할 수 없는 데이터를 사용할 수 있도록 인증서를 사용하여 저장 프로시저에 서명하는 방법에 대해 설명합니다. 호출자가 직접 수행할 권한이 없는 작업을 저장 프로시저에서 수행할 수 있습니다.  
  
 [SQL Server에서 가장으로 권한 사용자 지정](customizing-permissions-with-impersonation-in-sql-server.md)  
 EXECUTE AS 절을 사용하여 다른 사용자를 가장하는 방법에 대해 설명합니다. 가장은 실행 컨텍스트를 호출자에서 지정된 사용자로 전환합니다.  
  
 [SQL Server에서 행 수준 권한 부여](granting-row-level-permissions-in-sql-server.md)  
 데이터 액세스를 제한하는 낮은 수준의 권한을 구현하는 방법에 대해 설명합니다.  
  
 [SQL Server에서 애플리케이션 역할 만들기](creating-application-roles-in-sql-server.md)  
 애플리케이션 역할의 특성과 기능에 대해 설명합니다.  
  
 [SQL Server에서 데이터베이스 간 액세스 활성화](enabling-cross-database-access-in-sql-server.md)  
 보안을 위협하지 않고 데이터베이스 간 액세스를 허용하는 방법에 대해 설명합니다.  
  
## <a name="see-also"></a>참고자료

- [SQL Server 보안](sql-server-security.md)
- [SQL Server 보안 개요](overview-of-sql-server-security.md)
- [ADO.NET 응용 프로그램 보안](../securing-ado-net-applications.md)
- [ADO.NET 개요](../ado-net-overview.md)
