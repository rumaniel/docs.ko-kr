---
title: SQL Server Express 보안
ms.date: 03/30/2017
ms.assetid: cf9cf6d9-4b05-43e9-ac7b-6cefbfcd6d4e
ms.openlocfilehash: 55f1d141e50ed7afd851d7330cfaf2e3b6380f18
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70791695"
---
# <a name="sql-server-express-security"></a>SQL Server Express 보안
Microsoft SQL Server Express Edition(SQL Server Express)은 Microsoft SQL Server를 기반으로 하며 대부분의 데이터베이스 엔진 기능을 지원합니다. 이 제품은 중요하지 않은 기능 및 네트워크 연결이 기본적으로 해제되어 있기 때문에 악의적인 사용자의 공격에 노출되는 영역이 적습니다.  
  
 일반적으로 SQL Server Express는 명명된 인스턴스로 설치되며 인스턴스의 기본 이름은 `SQLExpress`입니다. 명명된 인스턴스는 컴퓨터의 네트워크 이름과 설치 시 사용자가 지정하는 인스턴스 이름의 조합으로 식별됩니다.  
  
## <a name="network-access"></a>네트워크 액세스  
 보안상의 이유로 SQL Server Express에서는 네트워크 프로토콜이 기본적으로 비활성화되어 있습니다. 이를 통해 SQL Server Express의 인스턴스를 호스트하는 컴퓨터를 손상시킬 수 있는 외부 사용자의 공격을 차단할 수 있습니다. 다른 컴퓨터에서 SQL Server Express 인스턴스에 연결하려면 명시적으로 네트워크 연결을 사용하도록 설정하고 SQL Server Browser 서비스를 시작해야 합니다.  
  
 네트워크 연결을 활성화한 후에는 다른 SQL Server 버전과 동일한 보안 요구 사항이 SQL Server Express 인스턴스에 적용됩니다.  
  
## <a name="user-instances"></a>사용자 인스턴스  
 사용자 인스턴스는 SQL Server Express의 부모 인스턴스에서 생성된 별도의 SQL Server Express 데이터베이스 엔진 인스턴스입니다. 사용자 인스턴스의 기본적인 목적은 최소 권한 사용자 계정으로 Windows를 실행하는 사용자에게 해당 로컬 컴퓨터에서 실행되는 SQL Server Express 인스턴스에 대한 시스템 관리자 권한(`sysadmin`)을 제공하는 것입니다. 자신의 컴퓨터에 대해 시스템 관리자 권한을 가진 사용자는 사용자 인스턴스를 사용할 필요가 없습니다.  
  
 사용자 인스턴스는 사용자를 대신하여 SQL Server 또는 SQL Server Express의 기본 인스턴스에서 생성됩니다. 사용자 인스턴스는 서비스가 이니라 사용자의 Windows 보안 컨텍스트 내에서 사용자 프로세스로 실행됩니다. SQL Server 로그인은 허용되지 않고 Windows 로그인만 지원됩니다. 따라서 사용자 인스턴스에서 실행되는 소프트웨어에서는 해당 사용자가 권한을 가지고 있지 않은 시스템 차원의 변경을 수행할 수 없습니다. 사용자 인스턴스를 자식 또는 클라이언트 인스턴스라고도 하며, RANU(Run As Normal User)로 표현하기도 합니다.  
  
 각 사용자 인스턴스는 부모 인스턴스 및 동일한 컴퓨터에서 실행되는 다른 사용자 인스턴스로부터 격리됩니다. 사용자 인스턴스에 설치된 데이터베이스는 단일 사용자 모드에서만 열리기 때문에 여러 사용자가 해당 데이터베이스에 연결할 수 없습니다. 사용자 인스턴스에서는 복제, 분산 쿼리 및 원격 연결 기능을 사용할 수 없습니다. 사용자 인스턴스에 연결한 사용자는 부모 SQL Server Express 인스턴스에 대해 특별한 권한을 갖지 않습니다.  
  
## <a name="external-resources"></a>외부 리소스  
 SQL Server Express에 대한 자세한 내용은 다음 리소스를 참조하세요.  
  
|||  
|-|-|  
|[Microsoft SQL Server 2005 Express Edition Books Online](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/ms165706(v=sql.90))|SQL Server 2005 Express Edition의 전체 설명서가 있습니다.|  
|SQL Server 온라인 설명서에서 비관리자 [의 사용자 인스턴스](https://docs.microsoft.com/previous-versions/sql/sql-server-2008/ms143684(v=sql.100))|사용자 인스턴스를 만들고 배포하는 방법을 설명합니다.|  
|[SQL Server Express 사용자 인스턴스](sql-server-express-user-instances.md)|ADO.NET 애플리케이션에서 사용할 수 있는 사용자 인스턴스 기능에 대해 설명합니다. 사용자 인스턴스를 사용하는 방법, <xref:System.Data.SqlClient.SqlConnection>을 통해 사용자 인스턴스에 연결하는 방법, 사용자 인스턴스 수명 및 사용자 인스턴스 시나리오에 대해 설명합니다.|  
  
## <a name="see-also"></a>참고자료

- [SQL Server 보안](sql-server-security.md)
- [SQL Server Express 사용자 인스턴스](sql-server-express-user-instances.md)
- [ADO.NET 개요](../ado-net-overview.md)
