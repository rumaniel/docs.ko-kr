---
title: SQL Server CLR 통합 소개
ms.date: 03/30/2017
ms.assetid: 551d2290-ed80-49be-b377-44b32444da1c
ms.openlocfilehash: 76c6fb4cb37807f286f1f1f2aeedbdea6c74fe38
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72002136"
---
# <a name="introduction-to-sql-server-clr-integration"></a>SQL Server CLR 통합 소개
CLR(공용 언어 런타임)은 Microsoft .NET Framework의 핵심으로, 모든 .NET Framework 코드에 실행 환경을 제공합니다. CLR 내에서 실행되는 코드를 관리 코드라고 합니다. CLR에서는 JIT(Just-In-Time) 컴파일, 메모리 할당 및 관리, 형식 안전성 적용, 예외 처리, 스레드 관리 및 보안 같은 프로그램 실행을 위한 다양한 기능과 서비스를 제공합니다.  
  
 CLR이 Microsoft SQL Server에서 호스트되는 경우(CLR 통합이라고 함) 관리 코드에 저장 프로시저, 트리거, 사용자 정의 함수, 사용자 정의 형식 및 사용자 정의 집계를 작성할 수 있습니다. 관리 코드는 실행되기 전에 네이티브 코드로 컴파일되기 때문에 일부 시나리오에서는 성능이 크게 향상될 수 있습니다.  
  
 관리 코드에서는 CAS(코드 액세스 보안), 코드 링크 및 애플리케이션 도메인을 사용하여 어셈블리에서 특정 작업을 수행하지 못하도록 합니다. SQL Server에서는 CAS를 사용하여 관리 코드의 보안을 손쉽게 유지하고 운영 체제나 데이터베이스 서버의 성능이 떨어지지 않도록 합니다.  
  
 이 단원은 SQL Server CLR 통합으로 프로그래밍을 시작하는 데 필요한 정보만 제공하며 모든 정보를 포괄적으로 다루지는 않습니다. 자세한 내용을 보려면 현재 사용하고 있는 SQL Server 버전에 해당하는 SQL Server 온라인 설명서 버전을 참조하세요.  
  
 **SQL Server 온라인 설명서**  
  
- [CLR (공용 언어 런타임) 통합 개요](https://go.microsoft.com/fwlink/?LinkId=115242)  
  
## <a name="enabling-clr-integration"></a>CLR 통합 사용  
 Microsoft SQL Server에서 CLR(공용 언어 런타임) 통합 기능은 기본적으로 사용하지 않도록 설정되어 있으며 CLR 통합을 사용하여 구현되는 개체를 사용하려면 이를 활성화해야 합니다. Transact-SQL을 사용하여 CLR 통합을 활성화하려면 다음과 같이 `clr enabled` 저장 프로시저의 `sp_configure` 옵션을 사용합니다.  
  
```sql  
sp_configure 'clr enabled', 1  
GO  
RECONFIGURE  
GO  
```  
  
 `clr enabled` 옵션을 0으로 설정하면 CLR 통합이 비활성화됩니다. CLR 통합을 비활성화하면 SQL Server에서는 모든 CLR 루틴의 실행을 중지하고 모든 애플리케이션 도메인을 언로드합니다.  
  
 자세한 내용을 보려면 현재 사용하고 있는 SQL Server 버전에 해당하는 SQL Server 온라인 설명서 버전을 참조하세요.  
  
 **SQL Server 온라인 설명서**  
  
- [CLR 통합 사용](https://go.microsoft.com/fwlink/?LinkId=115230)  
  
## <a name="deploying-a-clr-assembly"></a>CLR 어셈블리 배포  
 테스트 서버에서 테스트되고 확인된 CLR 메서드는 배포 스크립트를 사용하여 프로덕션 서버에 배포할 수 있습니다. 배포 스크립트는 수동으로 생성하거나 SQL Server Management Studio를 사용하여 생성할 수 있습니다. 자세한 내용을 보려면 현재 사용하고 있는 SQL Server 버전에 해당하는 SQL Server 온라인 설명서 버전을 참조하세요.  
  
 **SQL Server 온라인 설명서**  
  
1. [CLR 데이터베이스 개체 배포](https://go.microsoft.com/fwlink/?LinkId=115232)  
  
## <a name="clr-integration-security"></a>CLR 통합 보안  
 Microsoft .NET Framework CLR(공용 언어 런타임)과 통합된 Microsoft SQL Server 보안 모델은 SQL Server 내에서 실행되는 다양한 유형의 CLR 및 비 CLR 개체 간에 액세스를 관리 및 보호합니다. 이러한 개체는 서버에서 실행되는 Transact-SQL 문이나 다른 CLR 개체에서 호출할 수 있습니다.  
  
 자세한 내용을 보려면 현재 사용하고 있는 SQL Server 버전에 해당하는 SQL Server 온라인 설명서 버전을 참조하세요.  
  
 **SQL Server 온라인 설명서**  
  
- [CLR 통합 보안](https://go.microsoft.com/fwlink/?LinkId=115234)  
  
## <a name="debugging-a-clr-assembly"></a>CLR 어셈블리 디버깅  
 Microsoft SQL Server는 데이터베이스에서의 Transact-SQL 및 CLR(공용 언어 런타임) 개체 디버깅을 지원합니다. 디버깅은 여러 언어에서 수행되므로 사용자는 Transact-SQL에서 CLR 개체로 또는 CLR 개체에서 Transact-SQL로 매끄럽게 단계를 수행할 수 있습니다.  
  
 자세한 내용을 보려면 현재 사용하고 있는 SQL Server 버전에 해당하는 SQL Server 온라인 설명서 버전을 참조하세요.  
  
 **SQL Server 온라인 설명서**  
  
- [CLR 데이터베이스 개체 디버깅](https://go.microsoft.com/fwlink/?LinkId=115236)  
  
## <a name="see-also"></a>참조

- [코드 액세스 보안 및 ADO.NET](../code-access-security.md)
- [ADO.NET 개요](../ado-net-overview.md)
