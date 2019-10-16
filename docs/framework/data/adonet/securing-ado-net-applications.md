---
title: ADO.NET 애플리케이션 보안
ms.date: 03/30/2017
ms.assetid: 005a1d43-6ee5-471e-ad98-1d30a44d49d5
ms.openlocfilehash: 725ba568f3cd482991359237f4fc42b7da99bc0a
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795064"
---
# <a name="securing-adonet-applications"></a>ADO.NET 애플리케이션 보안
보안 ADO.NET 애플리케이션을 작성하려면 사용자 입력의 유효성을 확인하지 않는 것과 같은 일반적인 코딩 문제를 피하는 것 외에도 여러 부분을 고려해야 합니다. 데이터에 액세스하는 애플리케이션에는 공격자가 중요한 데이터를 검색, 조작 또는 제거하는 데 악용할 수 있는 여러 잠재적인 오류 지점이 있습니다. 따라서 애플리케이션 디자인 단계의 위협 모델링 과정에서부터 최종 배포와 진행 중인 유지 관리에 이르기까지 보안의 모든 측면을 이해해야 합니다.  
  
 .NET Framework에서는 데이터베이스 애플리케이션을 보호하고 관리할 수 있는 여러 유용한 클래스, 서비스 및 도구를 제공합니다. CLR(공용 언어 런타임)은 관리 코드의 권한을 더 제한하는 CAS(코드 액세스 보안)를 사용하여 실행될 코드에 형식 안전 환경을 제공합니다. 다음 보안 데이터 액세스 코딩 연습에서는 잠재적인 공격자에 의해 발생할 수 있는 손상을 제한합니다.  
  
 보안 코드를 작성하면 데이터베이스와 같은 관리되지 않는 리소스 작업을 할 때 자초한 보안 허점을 막지 못합니다. SQL Server와 같은 대부분의 서버 데이터베이스는 제대로 구현되는 경우 보안을 강화하는 자체 보안 시스템을 가집니다. 그러나 제대로 구성되지 않은 경우 강력한 보안 시스템으로 구성된 데이터 소스라 할지라도 공격에 취약할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [보안 개요](security-overview.md)  
 보안 ADO.NET 애플리케이션 디자인에 대한 권장 사항을 제공합니다.  
  
 [보안 데이터 액세스](secure-data-access.md)  
 안전한 데이터 소스의 데이터로 작업하는 방법에 대해 설명합니다.  
  
 [안전한 클라이언트 애플리케이션](secure-client-applications.md)  
 클라이언트 애플리케이션 보안을 위한 고려 사항에 대해 설명합니다.  
  
 [코드 액세스 보안 및 ADO.NET](code-access-security.md)  
 CAS를 사용하여 ADO.NET 코드를 보호하는 방법 및 부분 신뢰를 사용하는 방법에 대해 설명합니다.  
  
 [개인 정보 및 데이터 보안](privacy-and-data-security.md)  
 ADO.NET 애플리케이션의 암호화 옵션에 대해 설명합니다.  
  
## <a name="related-sections"></a>관련 단원  
 [SQL Server 보안](./sql/sql-server-security.md)  
 개발자 관점에서 SQL Server 보안 기능에 대해 설명합니다.  
  
 [보안 고려 사항](./ef/security-considerations.md)  
 Entity Framework 애플리케이션의 보안에 대해 설명합니다.  
  
 [보안](../../../standard/security/index.md)  
 .NET에서 보안의 여러 가지 측면에 대해 설명하는 항목의 링크가 들어 있습니다.  
  
 [보안 도구](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/7w3fd0wb(v=vs.90))  
 보안 정책을 보호하고 관리하는 .NET Framework 도구입니다.  
  
 [보안 애플리케이션을 만들기 위한 리소스](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/ms165101(v=vs.100))  
 보안 애플리케이션 만들기에 대한 항목의 링크를 제공합니다.  
  
 [보안 관련 참조 목록](/visualstudio/ide/security-bibliography)  
 온라인 및 인쇄 작업에서 사용 가능한 외부 리소스의 링크를 제공합니다.  
  
## <a name="see-also"></a>참고자료

- [ADO.NET](index.md)
- [ADO.NET 개요](ado-net-overview.md)
