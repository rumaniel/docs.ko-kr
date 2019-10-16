---
title: SQL Server의 서버 및 데이터베이스 역할
ms.date: 03/30/2017
ms.assetid: 5482dfdb-e498-4614-8652-b174829eed13
ms.openlocfilehash: f3e31aa67bfbaa541d8d1eb5b8b61dfd28182c72
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70791782"
---
# <a name="server-and-database-roles-in-sql-server"></a>SQL Server의 서버 및 데이터베이스 역할
모든 버전의 SQL Server에서는 역할 기반 보안을 사용하므로 개별 사용자 대신 역할이나 사용자 그룹에 권한을 할당할 수 있습니다. 고정 서버 역할과 고정 데이터베이스 역할에는 고정 권한 집합이 할당되어 있습니다.  
  
## <a name="fixed-server-roles"></a>고정 서버 역할  
 고정 서버 역할에는 서버 범위의 고정 권한 집합이 할당되어 있습니다. 고정 서버 역할은 SQL Server를 관리하는 데 사용되며 이 역할에 할당된 권한은 변경할 수 없습니다. 데이터베이스에 사용자 계정을 만들지 않고도 고정 서버 역할에 로그인을 할당할 수 있습니다.  
  
> [!IMPORTANT]
> `sysadmin` 고정 서버 역할은 다른 모든 역할을 포함하며 범위에 제한이 없습니다. 완전히 신뢰할 수 있는 보안 주체만 이 역할에 추가하세요. `sysadmin` 역할 멤버는 모든 서버 데이터베이스 및 리소스에 대해 취소할 수 없는 관리 권한을 갖습니다.  
  
 고정 서버 역할에 사용자를 추가할 때는 주의를 기울여야 합니다. 예를 들어 `bulkadmin` 역할에 속한 사용자는 로컬 파일의 내용을 테이블에 삽입할 수 있으므로 이로 인해 데이터 무결성이 손상될 수 있습니다. 고정 서버 역할 및 권한의 전체 목록은 SQL Server 온라인 설명서를 참조 하세요.  
  
## <a name="fixed-database-roles"></a>고정 데이터베이스 역할  
 고정 데이터베이스 역할에는 권한 그룹을 간편하게 관리할 수 있도록 미리 정의된 권한 집합이 할당되어 있습니다. `db_owner` 역할의 멤버는 데이터베이스에 대한 모든 구성 및 관리 작업을 수행할 수 있습니다.  
  
 SQL Server의 미리 정의된 역할에 대한 자세한 내용은 다음 리소스를 참조하세요.  
  
|리소스|Description|  
|--------------|-----------------|  
|[서버 수준 역할](/sql/relational-databases/security/authentication-access/server-level-roles)|SQL Server에서 고정 서버 역할 및 이와 관련 된 사용 권한을 설명 합니다.|  
|[데이터베이스 수준 역할](/sql/relational-databases/security/authentication-access/database-level-roles)|고정 데이터베이스 역할 및 역할에 연결된 권한에 대해 설명합니다.|  
  
## <a name="database-roles-and-users"></a>데이터베이스 역할 및 사용자  
 데이터베이스 개체를 사용하려면 로그인을 데이터베이스 사용자 계정에 매핑해야 합니다. 그러면 데이터베이스 사용자를 데이터베이스 역할에 추가하여 해당 역할에 연결된 모든 권한을 상속할 수 있습니다. 모든 권한을 부여할 수 있습니다.  
  
 애플리케이션 보안을 디자인할 때 `public` 역할, `dbo` 사용자 계정 및 `guest` 계정에 대해 신중하게 검토해야 합니다.  
  
### <a name="the-public-role"></a>public 역할  
 `public` 역할은 시스템 데이터베이스를 비롯한 모든 데이터베이스에 포함됩니다. 이 역할은 삭제할 수 없으며 이 역할에서 사용자를 추가 또는 제거할 수 없습니다. 모든 사용자 및 역할은 기본적으로 `public` 역할에 속하므로 `public` 역할에 부여된 권한을 상속합니다. 따라서 모든 사용자에게 허용하려는 권한만 `public` 역할에 부여해야 합니다.  
  
### <a name="the-dbo-user-account"></a>dbo 사용자 계정  
 `dbo` 또는 데이터베이스 소유자는 데이터베이스에서 모든 작업을 수행할 수 있는 권한을 암시적으로 가지고 있는 사용자 계정입니다. `sysadmin` 고정 서버 역할의 멤버는 자동으로 `dbo`에 매핑됩니다.  
  
> [!NOTE]
> `dbo`는 [SQL Server의 소유권 및 사용자 스키마 분리](ownership-and-user-schema-separation-in-sql-server.md)에 설명 된 스키마의 이름 이기도 합니다.  
  
 `dbo` 사용자 계정을 `db_owner` 고정 데이터베이스 역할과 혼동하는 경우가 많습니다. `db_owner`의 범위는 데이터베이스이고 `sysadmin`의 범위는 전체 서버입니다. `db_owner` 역할의 멤버 자격은 `dbo` 사용자 권한을 부여하지 않습니다.  
  
### <a name="the-guest-user-account"></a>guest 사용자 계정  
 사용자가 인증되어 SQL Server 인스턴스에 로그인할 수 있게 된 경우 해당 사용자가 액세스하는 각 데이터베이스에는 별도의 사용자 계정이 있어야 합니다. 각 데이터베이스에 사용자 계정이 있어야 하므로 사용자가 SQL Server의 한 인스턴스에 연결한 후 서버의 모든 데이터베이스에 액세스하는 것을 방지할 수 있습니다. 데이터베이스에 `guest` 사용자 계정이 있으므로 로그인한 계정은 데이터베이스 사용자 계정이 없어도 데이터베이스에 액세스함으로써 이러한 요구 사항을 피할 수 있습니다.  
  
 `guest` 계정은 모든 버전의 SQL Server에 포함된 기본 제공 계정입니다. 새 데이터베이스에서는 이 계정이 기본적으로 비활성화되어 있습니다. 이 계정이 활성화되어 있는 경우 Transact-SQL의 REVOKE CONNECT FROM GUEST 문을 실행하여 계정의 CONNECT 권한을 취소함으로써 이 계정을 비활성화할 수 있습니다.  
  
> [!IMPORTANT]
> 고유 데이터베이스 권한이 없는 모든 로그인은 이 계정에 부여된 데이터베이스 권한을 가지게 되므로 `guest` 계정은 사용하지 않는 것이 좋습니다. 불가피하게 `guest` 계정을 사용해야 하는 경우에는 계정에 최소 권한만 부여하세요.  
  
 SQL Server 로그인, 사용자 및 역할에 대한 자세한 내용은 다음 리소스를 참조하세요.  
  
|리소스|Description|  
|--------------|-----------------|  
|[데이터베이스 엔진 권한 시작](/sql/relational-databases/security/authentication-access/getting-started-with-database-engine-permissions)|보안 주체, 역할, 자격 증명, 보안 개체 및 권한에 대해 설명하는 항목의 링크를 제공합니다.|  
|[주체로](/sql/relational-databases/security/authentication-access/principals-database-engine)|보안 주체에 대해 설명하며 서버 및 데이터베이스 역할에 대해 설명하는 항목의 링크를 제공합니다.|  
  
## <a name="see-also"></a>참고자료

- [ADO.NET 응용 프로그램 보안](../securing-ado-net-applications.md)
- [SQL Server의 응용 프로그램 보안 시나리오](application-security-scenarios-in-sql-server.md)
- [SQL Server에서 인증](authentication-in-sql-server.md)
- [SQL Server에서 소유권 및 사용자 스키마 분리](ownership-and-user-schema-separation-in-sql-server.md)
- [SQL Server에서 권한 부여 및 권한](authorization-and-permissions-in-sql-server.md)
- [ADO.NET 개요](../ado-net-overview.md)
