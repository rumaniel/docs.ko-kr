---
title: ADO.NET 기술 옵션 및 지침
ms.date: 03/30/2017
ms.assetid: c8577281-38e6-4ce5-b036-572039a4c3d8
ms.openlocfilehash: d0f363d5eb102edf965c9c6068873fce0721d288
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70785778"
---
# <a name="adonet-technology-options-and-guidelines"></a>ADO.NET 기술 옵션 및 지침
ADO.NET 데이터 플랫폼은 여러 릴리스에 걸쳐 만들어진 전략으로, 개발자가 개념적 엔터티 데이터 모델을 기반으로 프로그래밍할 수 있도록 하여 필요한 코딩 및 유지 관리 작업을 줄일 수 있도록 합니다. 이 플랫폼에는 ADO.NET Entity Framework와 관련 기술이 포함됩니다.  
  
## <a name="entity-framework"></a>Entity Framework  
 ADO.NET Entity Framework는 개발자가 관계형 저장소 스키마에 대해 직접 프로그래밍하는 대신 개념적 응용 프로그램 모델에 대해 프로그래밍하는 방법으로 데이터 액세스 응용 프로그램을 만들 수 있도록 설계되었습니다. 이 프레임워크의 목표는 데이터 지향 응용 프로그램에 필요한 코드와 유지 관리 작업의 양을 줄이는 것입니다. 자세한 내용은 [ADO.NET Entity Framework](./ef/index.md)를 참조 하세요.  
  
### <a name="entity-data-model-edm"></a>EDM(엔터티 데이터 모델)  
 EDM(엔터티 데이터 모델)은 애플리케이션 데이터를 엔터티 집합 및 관계로 정의하는 디자인 사양입니다. 이 모델의 데이터는 애플리케이션 경계 간의 데이터 프로그래밍 기능 및 개체 관계형 매핑을 지원합니다.  
  
### <a name="object-services"></a>개체 서비스(Object Services)  
 개체 서비스를 사용하면 프로그래머가 CLR(공용 언어 런타임) 클래스 집합을 통해 개념적 모델과 상호 작용할 수 있습니다. 이러한 클래스는 개념적 모델에서 자동으로 생성되거나, 개념적 모델의 구조를 반영하도록 독립적으로 개발될 수 있습니다. 또한 개체 서비스는 상태 관리, 변경 내용 추적, ID 확인, 관계 로드 및 탐색, 데이터베이스 수정 내용에 개체 변경 내용 전파, Entity SQL 쿼리 작성 지원 등의 서비스를 포함하여 Entity Framework를 지원하는 인프라도 제공합니다. 자세한 내용은 [개체 서비스 개요(Entity Framework)](https://docs.microsoft.com/previous-versions/bb386871(v=vs.100))를 참조하세요.  
  
### <a name="linq-to-entities"></a>LINQ to Entities  
 LINQ to Entities는 개발자가 LINQ 식과 LINQ 표준 쿼리 연산자를 사용하여 Entity Framework 개체 컨텍스트에 대한 강력한 형식의 쿼리를 만들 수 있도록 구현된 LINQ(Language-Integrated Query)입니다. LINQ to Entities를 사용하면 개발자가 Microsoft SQL Server 및 타사 데이터베이스 간의 매우 유연한 개체 관계형 매핑을 사용하여 개념적 모델로 작업할 수 있습니다. 자세한 내용은 [LINQ to Entities](./ef/language-reference/linq-to-entities.md)합니다.  
  
### <a name="entity-sql"></a>Entity SQL  
 Entity SQL은 엔터티 데이터 모델과 상호 작용하도록 디자인된 텍스트 기반의 쿼리 언어입니다. Entity SQL은 상속, 복합 형식 및 명시적 관계와 같은 높은 수준의 모델링 개념 측면에서 쿼리할 수 있는 생성자가 포함된 SQL 언어입니다. 개발자가 개체 서비스와 함께 Entity SQL을 직접 사용할 수도 있습니다. 자세한 내용은 [Entity SQL Language](./ef/language-reference/entity-sql-language.md)를 참조 하세요.  
  
### <a name="entityclient"></a>EntityClient  
 EntityClient는 엔터티 데이터 모델과 상호 작용하는 데 사용할 수 있는 새 .NET Framework 데이터 공급자입니다. EntityClient는 .NET Framework 데이터 공급자의 패턴에 따라 <xref:System.Data.EntityClient.EntityConnection>를 반환하는 <xref:System.Data.EntityClient.EntityCommand> 및 <xref:System.Data.EntityClient.EntityDataReader> 개체를 노출합니다. EntityClient는 Entity SQL 언어와 함께 사용되어 스토리지별 데이터 공급자에 대한 유연한 매핑을 제공합니다. 자세한 내용은 [Entity Framework에 대 한 EntityClient 공급자](./ef/entityclient-provider-for-the-entity-framework.md)를 참조 하세요.  
  
### <a name="entity-data-model-tools"></a>엔터티 데이터 모델 도구  
 Entity Framework는 EDM 애플리케이션을 쉽게 작성할 수 있도록 명령줄 도구, 마법사 및 디자이너를 제공합니다. EntityDataSource 컨트롤은 EDM에 기반한 데이터 바인딩 시나리오를 지원합니다. EntityDataSource 컨트롤의 프로그래밍 화면은 Visual Studio에 포함된 다른 데이터 소스 컨트롤과 유사합니다. 자세한 내용은 [ADO.NET 엔터티 데이터 모델 Tools](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb399249(v=vs.100))를 참조 하세요.  
  
## <a name="linq-to-sql"></a>LINQ to SQL  
 LINQ to SQL은 .NET Framework 클래스를 사용하여 SQL Server 데이터베이스를 모델링할 수 있도록 하는 OR/M(개체 관계형 매핑) 구현입니다. LINQ to SQL을 사용하면 LINQ를 사용하여 데이터베이스를 쿼리할 수 있으며 데이터베이스에서 데이터를 업데이트, 삽입 및 삭제할 수 있습니다. LINQ to SQL은 트랜잭션, 뷰, 저장 프로시저 등을 지원하며 데이터 유효성 검사 및 비즈니스 논리 규칙을 데이터 모델에 통합할 수 있는 간단한 방법을 제공합니다. O/R 디자이너(개체 관계형 디자이너)를 사용하면 데이터베이스의 개체를 기반으로 하는 엔터티 클래스 및 연결을 모델링할 수 있습니다. 자세한 내용은 [Visual Studio의 LINQ to SQL 도구](/visualstudio/data-tools/linq-to-sql-tools-in-visual-studio2)를 참조하세요.  
  
## <a name="wcf-data-services"></a>WCF Data Services  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]는 웹 또는 인트라넷에 데이터 서비스를 배포합니다. 데이터는 엔터티 데이터 모델의 사양에 따라 엔터티와 관계로 구조화됩니다. 이 모델에 배포되는 데이터는 표준 HTTP 프로토콜로 주소를 지정할 수 있습니다. 자세한 내용은 [WCF Data Services 4.5](../wcf/index.md)를 참조하세요.  
  
## <a name="see-also"></a>참고자료

- [ADO.NET 개요](ado-net-overview.md)
- [ADO.NET의 새로운 기능](whats-new.md)
