---
title: 안정성
ms.date: 03/30/2017
helpviewer_keywords:
- SQL Server [.NET Framework]
- managed code, reliability
- reliability [.NET Framework]
- writing reliable code
- code, reliability
ms.assetid: 294aa306-0afe-4cbe-b397-86ba9f1860f8
author: mairaw
ms.author: mairaw
ms.openlocfilehash: acb84c6617cdffabfe276895f81e7df2b04bb8bb
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71046244"
---
# <a name="reliability"></a>안정성
SQL Server와 같은 서버 환경에서 실행되는 코드를 비동기 예외로부터 보호하는 것이 중요합니다. 여기에서 설명한 대로 안정성은 SQL Server에는 특별하지 않지만 .NET Framework 버전 2.0 환경에서 실행되는 모든 호스트용으로 신뢰할 수 있는 코드를 작성할 때는 중요합니다. 그러나 SQL Server는 버전 2.0의 새로운 안정성 기능을 광범위하게 이용하는 첫 번째 서비스이므로 예제로 사용됩니다.  
  
 SQL Server에서 실행되는 코드는 다른 서버 환경보다 더 엄격한 안정성 지침을 처리해야 합니다. 리소스 사용의 에지에서 SQL Server가 지속적으로 작동하기 때문입니다.  <xref:System.OutOfMemoryException> 및 <xref:System.Threading.ThreadAbortException> 예외는 SQL Server 환경에서 일반적으로 발생합니다. 이러한 지침은 일반적으로 안정성보다는 완전히 신뢰할 수 있는 관리 코드가 <xref:System.AppDomain> 수준 재활용 시 올바른 절차에 따라 실패할 수 있도록 하는 데 더 중점을 둡니다. 이것이 서버에서 일관성과 가용성을 유지하는 기본 방법입니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [SQL Server 프로그래밍 및 호스트 보호 특성](sql-server-programming-and-host-protection-attributes.md)  
 SQL Server에서 <xref:System.Security.Permissions.HostProtectionAttribute> 특성을 사용하여 관리 코드의 실행을 제한하는 방법을 설명합니다.  
  
 [안전성 모범 사례](reliability-best-practices.md)  
 안정성 요구 사항을 충족하는 코드를 작성하기 위한 지침을 제공합니다.  
  
 [제약이 있는 실행 영역](constrained-execution-regions.md)  
 제약이 있는 실행 영역(CER)의 동작과 함수에 대해 설명합니다.  
  
## <a name="reference"></a>참조  
 <xref:System.Security.Permissions.HostProtectionAttribute>  
  
 <xref:System.Security.Permissions.HostProtectionResource>
