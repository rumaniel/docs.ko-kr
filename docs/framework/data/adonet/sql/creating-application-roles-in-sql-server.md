---
title: SQL Server에서 애플리케이션 역할 만들기
ms.date: 03/30/2017
ms.assetid: 27442435-dfb2-4062-8c59-e2960833a638
ms.openlocfilehash: 212bda6f64829792e965dd6714428a05b30c995b
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70794281"
---
# <a name="creating-application-roles-in-sql-server"></a>SQL Server에서 애플리케이션 역할 만들기
애플리케이션 역할을 사용하면 데이터베이스 역할이나 사용자 대신 애플리케이션에 권한을 할당할 수 있습니다. 사용자는 데이터베이스에 연결한 후 애플리케이션 역할을 활성화하여 애플리케이션에 부여된 권한을 사용할 수 있습니다. 애플리케이션 역할에 부여된 권한은 연결되어 있는 동안 유효합니다.  
  
> [!IMPORTANT]
> 애플리케이션 역할은 클라이언트 애플리케이션에서 연결 문자열에 애플리케이션 역할 이름과 암호를 제공하면 활성화됩니다. 암호는 클라이언트 컴퓨터에 저장되므로 2계층 애플리케이션의 경우 애플리케이션 역할로 인해 보안상 취약한 부분이 발생할 수 있습니다. 3계층 애플리케이션에서는 애플리케이션 사용자가 액세스할 수 없는 방식으로 암호를 저장할 수 있습니다.  
  
## <a name="application-role-features"></a>애플리케이션 역할의 특징  
 애플리케이션 역할에는 다음과 같은 특징이 있습니다.  
  
- 데이터베이스 역할과 달리 애플리케이션 역할은 멤버를 포함하지 않습니다.  
  
- 애플리케이션 역할은 애플리케이션에서 `sp_setapprole` 시스템 저장 프로시저에 애플리케이션 역할 이름과 암호를 제공하면 활성화됩니다.  
  
- 암호는 클라이언트 컴퓨터에 저장되어 런타임에 제공되어야 하므로 SQL Server 내에서는 애플리케이션 역할을 활성화할 수 없습니다.  
  
- 암호가 암호화되지 않습니다. 매개 변수 암호는 단방향 해시로 저장됩니다.  
  
- 애플리케이션 역할이 활성화된 후 애플리케이션 역할을 통해 얻은 권한은 연결 기간 동안 유효합니다.  
  
- 애플리케이션 역할은 `public` 역할에 부여된 권한을 상속합니다.  
  
- `sysadmin` 고정 서버 역할의 멤버가 애플리케이션 역할을 활성화하는 경우, 연결 기간 동안 보안 컨텍스트가 해당 애플리케이션 역할의 보안 컨텍스트로 전환됩니다.  
  
- 애플리케이션 역할이 있는 데이터베이스에 `guest` 계정을 만들면 해당 애플리케이션 역할 또는 역할을 호출하는 어떤 로그인에 대해서도 데이터베이스 사용자 계정을 만들 필요가 없습니다. 애플리케이션 역할은 다른 데이터베이스에 `guest` 계정이 있는 경우에만 해당 데이터베이스에 직접 액세스할 수 있습니다.  
  
- SYSTEM_USER와 같은 로그인 이름을 반환하는 기본 제공 함수가 애플리케이션 역할을 호출한 로그인의 이름을 반환합니다. 데이터베이스 사용자 이름을 반환하는 기본 제공 함수는 애플리케이션 역할의 이름을 반환합니다.  
  
### <a name="the-principle-of-least-privilege"></a>최소 권한의 원칙  
 암호가 손상될 경우에 대비하여 애플리케이션 역할에는 반드시 필요한 권한만 부여해야 합니다. `public` 역할에 부여된 권한은 애플리케이션 역할을 사용하는 모든 데이터베이스에서 해지해야 합니다. 애플리케이션 역할 호출자가 액세스할 수 없도록 하려는 모든 데이터베이스에서 `guest` 계정을 비활성화하세요.  
  
### <a name="application-role-enhancements"></a>애플리케이션 역할의 향상된 기능  
 애플리케이션 역할을 활성화한 후 실행 컨텍스트를 원래 호출자로 되돌릴 수 있으므로 연결 풀링을 비활성화할 필요가 없습니다. 호출자 관련 컨텍스트 정보가 포함된 쿠키를 만드는 새로운 옵션이 `sp_setapprole` 프로시저에 추가되었습니다. `sp_unsetapprole` 프로시저를 호출하고 이 프로시저에 쿠키를 전달하면 세션을 되돌릴 수 있습니다.  
  
## <a name="application-role-alternatives"></a>응용 프로그램 역할의 대안  
 애플리케이션 역할은 암호로 보호되는데 이로 인해 보안상 취약한 부분이 발생할 수 있습니다. 암호가 애플리케이션 코드에 포함되거나 디스크에 저장되어 노출될 수 있습니다.  
  
 다음과 같은 대안을 고려해 보세요.  
  
- NO REVERT 및 WITH COOKIE 절과 함께 EXECUTE AS 문을 사용하여 컨텍스트를 전환합니다. 로그인에 매핑되지 않는 사용자 계정을 데이터베이스에 만든 다음 이 계정에 권한을 할당합니다. 이렇게 로그인에 매핑되지 않은 사용자로 EXECUTE AS를 사용하면 암호가 아니라 권한을 기반으로 하므로 더 안전합니다. 자세한 내용은 [SQL Server에서 가장으로 권한 사용자 지정](customizing-permissions-with-impersonation-in-sql-server.md)을 참조 하세요.  
  
- 저장 프로시저를 인증서로 서명하여 프로시저 실행에 꼭 필요한 권한만 부여합니다. 자세한 내용은 [SQL Server에서 저장 프로시저에 서명](signing-stored-procedures-in-sql-server.md)을 참조 하세요.  
  
## <a name="external-resources"></a>외부 리소스  
 자세한 내용은 다음 리소스를 참조하세요.  
  
|리소스|Description|  
|--------------|-----------------|  
|[응용 프로그램 역할](/sql/relational-databases/security/authentication-access/application-roles)|SQL Server 2008에서 애플리케이션 역할을 만들고 사용하는 방법에 대해 설명합니다.|  
  
## <a name="see-also"></a>참고자료

- [ADO.NET 응용 프로그램 보안](../securing-ado-net-applications.md)
- [SQL Server 보안 개요](overview-of-sql-server-security.md)
- [SQL Server의 응용 프로그램 보안 시나리오](application-security-scenarios-in-sql-server.md)
- [ADO.NET 개요](../ado-net-overview.md)
