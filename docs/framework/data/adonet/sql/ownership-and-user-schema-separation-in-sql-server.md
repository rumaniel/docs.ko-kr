---
title: SQL Server에서 소유권 및 사용자와 스키마 분리
ms.date: 03/30/2017
ms.assetid: 242830c1-31b5-4427-828c-cc22ff339f30
ms.openlocfilehash: 5ad3d927bcf3534e134db2c98b79842b0e6148f3
ms.sourcegitcommit: 5ae5a1a9520b8b8b6164ad728d396717f30edafc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/11/2019
ms.locfileid: "70894430"
---
# <a name="ownership-and-user-schema-separation-in-sql-server"></a>SQL Server에서 소유권 및 사용자와 스키마 분리
SQL Server 보안의 주요 개념은 개체 소유자에게 취소할 수 없는 개체 관리 권한이 있다는 것입니다. 개체 소유자의 권한을 제거할 수 없으며 사용자가 데이터베이스의 개체를 소유하는 경우 데이터베이스에서 사용자를 삭제할 수 없습니다.  
  
## <a name="user-schema-separation"></a>사용자 스키마 분리  
 사용자 스키마 분리를 통해 데이터베이스 개체 권한을 더욱 유연하게 관리할 수 있습니다. *스키마* 는 개체를 별도의 네임 스페이스로 그룹화 할 수 있도록 하는 데이터베이스 개체에 대 한 명명 된 컨테이너입니다. 예를 들어, AdventureWorks 샘플 데이터베이스에는 Production, Sales 및 HumanResources에 대한 스키마가 들어 있습니다.  
  
 개체를 참조하는 4부분으로 구성된 명명 구문은 스키마 이름을 지정합니다.  
  
```text
Server.Database.DatabaseSchema.DatabaseObject  
```  
  
### <a name="schema-owners-and-permissions"></a>스키마 소유자 및 권한  
 스키마는 데이터베이스 주체에서 소유하며 단일 주체가 여러 스키마를 소유할 수 있습니다. 스키마의 모든 개체에서 상속된 보안 규칙을 스키마에 적용할 수 있습니다. 스키마에 대한 액세스 권한을 설정했으면 새 개체가 스키마에 추가되었으므로 이러한 권한이 자동으로 적용됩니다. 사용자는 기본 스키마에 할당되며 여러 데이터베이스 사용자가 동일한 스키마를 공유할 수 있습니다.  
  
 개발자가 스키마에서 개체를 만들 때 기본적으로 개발자가 아닌 스키마를 소유하는 보안 주체가 개체를 소유합니다. 개체 소유권은 ALTER AUTHORIZATION Transact-SQL 문을 사용하여 전송할 수 있습니다. 스키마는 다른 사용자가 소유하고 스키마에 할당된 권한보다 세부적인 권한을 가지는 개체도 포함할 수 있지만 권한 관리가 복잡해지므로 이 방법은 권장하지 않습니다. 스키마 사이에 개체를 제거할 수 있으며 보안 주체 사이에 스키마 소유권을 전송할 수 있습니다. 스키마에 영향을 주지 않고 데이터베이스 사용자를 삭제할 수 있습니다.  
  
### <a name="built-in-schemas"></a>기본 제공 스키마  
 SQL Server는 기본 제공 데이터베이스 사용자 및 역할과 같은 이름을 가진 10개의 미리 정의된 스키마와 함께 제공됩니다. 이 기능은 이전 버전과의 호환성을 위해 존재합니다. 스키마가 필요하지 않은 경우 고정된 데이터베이스 역할과 이름이 같은 스키마를 삭제할 수 있습니다. 다음 스키마는 삭제할 수 없습니다.  
  
- `dbo`  
  
- `guest`  
  
- `sys`  
  
- `INFORMATION_SCHEMA`  
  
 모델 데이터베이스에서 스키마를 삭제하면 해당 스키마가 새 데이터베이스에 나타나지 않습니다.  
  
> [!NOTE]
> `sys` 및 `INFORMATION_SCHEMA` 스키마는 시스템 개체용으로 예약되어 있습니다. 이러한 스키마의 개체는 만들거나 삭제할 수 없습니다.  
  
#### <a name="the-dbo-schema"></a>dbo 스키마  
 `dbo` 스키마는 새로 만든 데이터베이스의 기본 스키마입니다. `dbo` 스키마는 `dbo` 사용자 계정에서 소유합니다. CREATE USER Transact-SQL 명령을 사용하여 만들어진 사용자는 기본적으로 `dbo`를 기본 스키마로 가집니다.  
  
 `dbo` 스키마에 할당된 사용자에게는 `dbo` 사용자 계정의 권한이 상속되지 않습니다. 사용자에게는 스키마의 권한이 상속되지 않고 스키마에 포함된 데이터베이스 개체의 스키마 권한이 상속됩니다.  
  
> [!NOTE]
> 한 부분으로 구성된 이름을 사용하여 데이터베이스 개체를 참조할 때 SQL Server에서는 먼저 사용자의 기본 스키마를 찾습니다. 개체를 기본 스키마에서 찾을 수 없으면 SQL Server는 `dbo` 스키마에서 찾습니다. 개체가 `dbo` 스키마에 없는 경우 오류가 반환됩니다.  
  
## <a name="external-resources"></a>외부 리소스  
 개체 소유권 및 스키마에 대한 자세한 내용은 다음 리소스를 참조하세요.  
  
|리소스|Description|  
|--------------|-----------------|  
|[사용자 스키마 분리](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms190387(v=sql.105))|사용자 스키마 분리에서 도입된 변경 내용을 설명합니다. 새 동작, 소유권에 대한 영향, 카탈로그 뷰 및 권한이 포함되어 있습니다.|  
  
## <a name="see-also"></a>참고자료

- [ADO.NET 응용 프로그램 보안](../securing-ado-net-applications.md)
- [SQL Server의 응용 프로그램 보안 시나리오](application-security-scenarios-in-sql-server.md)
- [SQL Server에서 인증](authentication-in-sql-server.md)
- [SQL Server의 서버 및 데이터베이스 역할](server-and-database-roles-in-sql-server.md)
- [SQL Server에서 권한 부여 및 권한](authorization-and-permissions-in-sql-server.md)
- [ADO.NET 개요](../ado-net-overview.md)
