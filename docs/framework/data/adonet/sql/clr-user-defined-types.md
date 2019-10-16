---
title: CLR 사용자 정의 형식
ms.date: 03/30/2017
ms.assetid: 9f70e0b0-3a0d-4eb1-b914-07a5d0c167c2
ms.openlocfilehash: e3b087124773db592b349e07cd022b0f642bdbe3
ms.sourcegitcommit: e08b319358a8025cc6aa38737854f7bdb87183d6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/29/2019
ms.locfileid: "64910726"
---
# <a name="clr-user-defined-types"></a>CLR 사용자 정의 형식
Microsoft SQL Server에서는 Microsoft .NET Framework CLR(공용 언어 런타임)로 구현된 UDT(사용자 정의 형식)를 지원합니다. CLR은 SQL Server에 통합되어 있으며 이 메커니즘을 통해 데이터베이스의 형식 시스템을 확장할 수 있습니다. UDT는 SQL Server 데이터 형식 시스템에 대한 사용자 확장성 및 구조적 복합 형식을 정의할 수 있는 기능을 제공합니다.  
  
 UDT는 애플리케이션 아키텍처 측면에서 다음과 같은 두 가지 이점을 제공합니다.  
  
- 클라이언트와 서버에서 내부 상태 및 외부 동작 간의 강력한 캡슐화  
  
- 다른 관련 서버 기능과의 밀접한 통합. 고유한 UDT를 정의하고 나면 열 정의를 포함한 SQL Server에 시스템 형식을 사용할 수 있는 경우 모든 컨텍스트에 사용할 수 있으며 변수, 매개 변수, 함수 결과, 커서, 트리거 및 복제로도 사용할 수 있습니다.  
  
 자세한 내용은 참조는 [SQL Server 설명서](/sql) 사용 중인 SQL Server의 버전에 대 한 합니다.
  
 **SQL Server 설명서**
  
1. [CLR 사용자 정의 형식](/sql/relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types)  
  
## <a name="see-also"></a>참고자료

- [ADO.NET 개요](../ado-net-overview.md)
