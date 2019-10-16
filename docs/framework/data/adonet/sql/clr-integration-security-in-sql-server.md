---
title: SQL Server의 CLR 통합 보안
ms.date: 03/30/2017
ms.assetid: 489fe096-fd1d-42de-8438-bf7aed46aea2
ms.openlocfilehash: 4756d13ff52a4c55b48c3ea56d26111029c8a7e4
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70794566"
---
# <a name="clr-integration-security-in-sql-server"></a>SQL Server의 CLR 통합 보안
Microsoft SQL Server에는 .NET Framework의 CLR(공용 언어 런타임) 구성 요소가 통합되어 있습니다. 따라서 이제는 Microsoft Visual Basic .NET 또는 Microsoft Visual C#을 비롯한 모든 .NET Framework 언어를 사용하여 저장 프로시저, 트리거, 사용자 정의 형식, 사용자 정의 함수, 사용자 정의 집계 및 스트리밍 테이블 반환 함수를 작성할 수 있습니다.  
  
 CLR은 관리 코드에 대해 CAS(코드 액세스 보안)라는 보안 모델을 지원합니다. 이 모델에서는 코드를 통해 메타데이터로 제공되는 증명 정보를 기준으로 어셈블리에 권한을 부여합니다. SQL Server에서는 SQL Server의 사용자 기반 보안 모델을 CLR의 코드 액세스 기반 보안 모델과 통합합니다.  
  
## <a name="external-resources"></a>외부 리소스  
 CLR과 SQL Server 통합에 대한 자세한 내용은 다음 리소스를 참조하세요.  
  
|리소스|Description|  
|--------------|-----------------|  
|[코드 액세스 보안](../../../misc/code-access-security.md)|.NET Framework의 CAS에 대해 설명하는 항목을 제공합니다.|  
|[CLR 통합 보안](/sql/relational-databases/clr-integration/security/clr-integration-security)|SQL Server 내에서 실행되는 관리 코드를 위한 보안 모델에 대해 설명합니다.|  
  
## <a name="see-also"></a>참고자료

- [ADO.NET 응용 프로그램 보안](../securing-ado-net-applications.md)
- [SQL Server의 응용 프로그램 보안 시나리오](application-security-scenarios-in-sql-server.md)
- [SQL Server 공용 언어 런타임 통합](sql-server-common-language-runtime-integration.md)
- [ADO.NET 개요](../ado-net-overview.md)
