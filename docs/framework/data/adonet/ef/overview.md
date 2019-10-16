---
title: Entity Framework 개요
ms.date: 09/17/2018
ms.assetid: a2166b3d-d8ba-4a0a-8552-6ba1e3eaaee0
ms.openlocfilehash: 92aa7b9c1f163c0496a821cca375c8b7e1b21a5f
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854349"
---
# <a name="entity-framework-overview"></a>Entity Framework 개요

Entity Framework은 데이터 지향 소프트웨어 응용 프로그램의 개발을 지 원하는 ADO.NET의 기술 집합입니다. 데이터 지향 애플리케이션의 설계자와 개발자는 두 가지 다른 목적을 달성하기 위해 노력해 왔습니다. 해결 중인 비즈니스 문제의 엔터티, 관계 및 논리를 모델링해야 하며, 데이터를 저장 및 검색하는 데 사용되는 데이터 엔진도 사용해야 합니다. 데이터는 각각 해당 프로토콜을 가진 여러 개의 스토리지 시스템에 걸쳐 있을 수 있습니다. 단일 스토리지 시스템에서 작동하는 애플리케이션도 스토리지 시스템의 요구 사항 및 효율적이고 유지 가능한 애플리케이션 코드를 작성하기 위한 요구 사항의 균형을 조정해야 합니다.

Entity Framework를 사용 하면 개발자가 기본 데이터베이스 테이블 및 열에 대해 걱정 하지 않고도 도메인 특정 개체 및 속성 (예: 고객 및 고객 주소)의 형태로 데이터를 작업할 수 있습니다. 저장. Entity Framework를 사용하면 개발자가 데이터를 처리할 때 보다 높은 추상 수준에서 작업할 수 있으며, 기존의 응용 프로그램에서보다 적은 코드로 데이터 지향 응용 프로그램을 만들고 유지 관리할 수 있습니다. Entity Framework은 .NET Framework의 구성 요소 이기 때문에 Entity Framework 응용 프로그램은 .NET Framework 버전 3.5 s p 1부터 시작 하는 모든 컴퓨터에서 실행할 수 있습니다.

## <a name="give-life-to-models"></a>모델에 수명 제공
 애플리케이션 또는 서비스를 만들 때의 오랫동안 지속된 일반적인 디자인 방법은 애플리케이션 또는 서비스를 도메인 모델, 논리 모델 및 실제 모델의 세 부분으로 나누는 것입니다. 도메인 모델은 모델링되는 시스템의 엔터티 및 관계를 정의합니다. 관계형 데이터베이스에 대한 논리 모델은 FOREIGN KEY 제약 조건이 있는 테이블로 엔터티와 관계를 정규화합니다. 실제 모델은 분할 및 인덱싱과 같은 스토리지 세부 정보를 지정하여 특정 데이터 엔진의 기능을 다룹니다.

 데이터베이스 관리자는 성능 향상을 위해 실제 모델을 미세 조정하지만, 애플리케이션 코드를 작성하는 프로그래머는 주로 SQL 쿼리를 작성하고 저장 프로시저를 호출하여 논리 모델에서 작업합니다. 도메인 모델은 일반적으로 애플리케이션 요구 사항을 파악하고 전달하기 위한 도구로 사용되며, 프로젝트의 초기 단계에서 확인하고 토론한 다음 버려지는 단순한 다이어그램으로 사용되는 경우가 많습니다. 대부분의 개발 팀에서는 개념적 모델을 만드는 단계를 생략하고 관계형 데이터베이스의 테이블, 열 및 키를 지정하는 단계에서 작업을 시작합니다.

 Entity Framework는 개발자가 도메인 모델의 엔터티 및 관계 (Entity Framework의 *개념적* 모델 이라고 함)를 쿼리할 수 있도록 하 고 해당 작업을 데이터 원본으로 변환 하는 Entity Framework에 의존 하 여 모델에 대 한 수명 주기를 제공 합니다. – 특정 명령입니다. 이렇게 하면 애플리케이션이 하드 코딩 방식으로 특정 데이터 소스에 종속되지 않습니다.

 Code First를 사용하여 작업할 때 개념적 모델이 스토리지 모델에 코드로 매핑됩니다. Entity Framework는 정의 하는 추가 구성 및 개체 형식에 따라 개념적 모델을 유추할 수 있습니다. 매핑 메타데이터는 사용자가 코드로 제공한 추가 구성 정보와 도메인 형식을 정의하는 방법을 기반으로 런타임 중 생성됩니다. Entity Framework는 메타 데이터에 따라 필요에 따라 데이터베이스를 생성 합니다. 자세한 내용은 [개념적 모델 만들기 및 매핑](https://go.microsoft.com/fwlink/?LinkID=235382)을 참조 하세요.

 엔터티 데이터 모델 도구를 사용하여 작업할 때 개념적 모델, 스토리지 모델 및 이 두 모델 간의 매핑은 XML 기반 스키마로 표현되고 해당 확장명의 파일에 정의됩니다.

- CSDL(개념 스키마 정의 언어)은 개념적 모델을 정의합니다. CSDL은 Entity Framework [엔터티 데이터 모델](../entity-data-model.md)의 구현입니다. 파일 확장명은 .csdl입니다.

- SSDL(스토리지 스키마 정의 언어)은 논리 모델이라고도 하는 스토리지 모델을 정의합니다. 파일 확장명은 .ssdl입니다.

- MSL(매핑 사양 언어)은 스토리지 모델과 개념적 모델 간의 매핑을 정의합니다. 파일 확장명은 .msl입니다.

스토리지 모델과 매핑은 개념적 모델, 데이터 클래스 또는 애플리케이션 코드를 변경하지 않고도 필요에 따라 변경할 수 있습니다. 스토리지 모델은 공급자와 관련이 있으므로 다양한 데이터 소스에서 일관성 있는 개념적 모델을 사용할 수 있습니다.

Entity Framework는 이러한 모델 및 매핑 파일을 사용 하 여 개념적 모델의 엔터티 및 관계에 대 한 만들기, 읽기, 업데이트 및 삭제 작업을 데이터 소스의 동등한 작업으로 사용 합니다. Entity Framework은 개념적 모델의 엔터티를 데이터 원본의 저장 프로시저에 매핑하는 것도 지원 합니다. 자세한 내용은 [CSDL, SSDL 및 MSL 사양](./language-reference/csdl-ssdl-and-msl-specifications.md)합니다.

## <a name="map-objects-to-data"></a>데이터에 개체 매핑
 개체 지향 프로그래밍을 사용하는 경우 데이터 스토리지 시스템과 상호 작용해야 합니다. 클래스의 구성은 관계형 데이터베이스 테이블의 구성을 미러링하는 경우가 많지만 완전히 일치하지는 않습니다. 여러 개의 정규화된 테이블이 하나의 클래스에 해당하는 경우가 많으며 클래스 간의 관계가 테이블 간의 관계와 다르게 표현되기도 합니다. 예를 들어 판매 주문의 고객을 나타내기 위해 `Order` 클래스는 `Customer` 클래스 인스턴스에 대한 참조가 포함된 속성을 사용할 수 있지만, 데이터베이스의 `Order` 테이블 행에는 `Customer` 테이블의 기본 키 값에 해당하는 값을 가진 외래 키 열(또는 열 집합)이 포함됩니다. `Customer` 클래스는 `Orders` 클래스 인스턴스의 컬렉션이 포함된 `Order` 속성을 가질 수 있는 반면, 데이터베이스의 `Customer` 테이블에는 해당하는 열이 없습니다. Entity Framework를 사용 하면 개발자는 이러한 방식으로 관계를 나타내거나 데이터베이스에 표시 되는 관계를 보다 긴밀 하 게 모델링할 수 있습니다.

 기존 솔루션은 개체 지향 클래스와 속성을 관계형 테이블과 열에 매핑만 하여 흔히 "임피던스 불일치"라고 하는 이 간격을 연결하려고 했습니다. 이 일반적인 방법을 사용 하는 대신 Entity Framework는 논리적 모델의 관계형 테이블, 열 및 외래 키 제약 조건을 개념적 모델의 엔터티 및 관계에 매핑합니다. 이렇게 하면 보다 유연성 있게 개체를 정의하고 논리 모델을 최적화할 수 있습니다. 엔터티 데이터 모델 도구는 개념적 모델을 기반으로 확장 가능한 데이터 클래스를 생성 합니다. 이러한 클래스는 개발자가 추가하는 멤버로 확장할 수 있는 부분 클래스입니다. 기본적으로, 특정 개념적 모델에 대해 생성되는 클래스는 엔터티를 개체로 구체화하고 변경 내용을 추적 및 저장하기 위한 서비스를 제공하는 기본 클래스에서 파생됩니다. 개발자는 이러한 클래스를 통해 엔터티 및 관계를 연결에 의해 관련된 개체로 사용할 수 있습니다. 또한 개발자는 개념적 모델에 대해 생성된 클래스를 사용자 지정할 수도 있습니다. 자세한 내용은 [개체 작업](working-with-objects.md)을 참조 하세요.

## <a name="access-and-change-entity-data"></a>엔터티 데이터 액세스 및 변경

단순한 개체-관계형 매핑 솔루션 이상의 의미가 있는 Entity Framework는 근본적으로 응용 프로그램이 개념적 모델의 엔터티 및 관계로 표현된 데이터에 액세스하여 변경할 수 있도록 합니다. Entity Framework는 모델 및 매핑 파일의 정보를 사용 하 여 개념적 모델에 표시 된 엔터티 형식에 대 한 개체 쿼리를 데이터 소스 관련 쿼리로 변환 합니다. 쿼리 결과는 Entity Framework에서 관리 하는 개체로 구체화 됩니다. Entity Framework은 개념적 모델을 쿼리하고 개체를 반환 하는 다음과 같은 방법을 제공 합니다.

- LINQ to Entities. 개념적 모델에 정의된 엔터티 형식을 쿼리하기 위한 LINQ(Language-Integrated Query) 지원을 제공합니다. 자세한 내용은 [LINQ to Entities](./language-reference/linq-to-entities.md)합니다.

- [!INCLUDE[esql](../../../../../includes/esql-md.md)]. 개념적 모델의 엔터티와 직접 작동 하며 엔터티 데이터 모델 개념을 지 원하는, 저장소에 독립적인 SQL 언어입니다. [!INCLUDE[esql](../../../../../includes/esql-md.md)]는 EntityClient 공급자를 사용 하 여 실행 되는 개체 쿼리 및 쿼리와 함께 사용 됩니다. 자세한 내용은 [Entity SQL 개요](./language-reference/entity-sql-overview.md)를 참조 하세요.

Entity Framework는 EntityClient 데이터 공급자를 포함 합니다. 이 공급자는 연결을 관리 하 고, 엔터티 쿼리를 데이터 소스 관련 쿼리로 변환 하 고, Entity Framework에서 엔터티 데이터를 개체로 구체화 하는 데 사용 하는 데이터 판독기를 반환 합니다. 개체 구체화가 필요하지 않은 경우 응용 프로그램에서 [!INCLUDE[esql](../../../../../includes/esql-md.md)] 쿼리를 실행하고 반환된 읽기 전용 데이터 판독기를 사용할 수 있도록 하여 EntityClient 공급자를 표준 ADO.NET 데이터 공급자처럼 사용할 수도 있습니다. 자세한 내용은 [Entity Framework에 대 한 EntityClient 공급자](entityclient-provider-for-the-entity-framework.md)를 참조 하세요.

다음 다이어그램은 데이터 액세스를 위한 Entity Framework 아키텍처를 보여 줍니다.

![Entity Framework 아키텍처 다이어그램](./media/wd-efarchdiagram.gif "wd_EFArchDiagram")

엔터티 데이터 모델 도구는 개념적 모델의 엔터티 컨테이너를 `System.Data.Objects.ObjectContext` 나타내는 `System.Data.Entity.DbContext` 또는에서 파생 된 클래스를 생성할 수 있습니다. 이 개체 컨텍스트는 변경 내용을 추적하고 ID, 동시성 및 관계를 관리하기 위한 기능을 제공합니다. 또한 이 클래스는 데이터 소스에 삽입, 업데이트 및 삭제를 쓰는 `SaveChanges` 메서드를 노출합니다. 쿼리와 마찬가지로, 이러한 변경 작업은 시스템에서 자동으로 생성된 명령이나 개발자가 지정한 저장 프로시저로 수행됩니다.

## <a name="data-providers"></a>데이터 공급자

공급자 `EntityClient` 는 개념적 엔터티 및 관계를 기준으로 데이터에 액세스 하 여 ADO.NET 공급자 모델을 확장 합니다. [!INCLUDE[esql](../../../../../includes/esql-md.md)]을 사용하는 쿼리를 실행합니다. [!INCLUDE[esql](../../../../../includes/esql-md.md)]에서는 `EntityClient`가 데이터베이스와 통신할 수 있도록 기본 쿼리 언어를 제공합니다. 자세한 내용은 [Entity Framework에 대 한 EntityClient 공급자](entityclient-provider-for-the-entity-framework.md)를 참조 하세요.

Entity Framework에는 정식 명령 트리를 지 원하는 업데이트 된 SqlClient Data Provider 포함 되어 있습니다. 자세한 내용은 [Entity Framework SqlClient](sqlclient-for-the-entity-framework.md)(영문)를 참조 하세요.

## <a name="entity-data-model-tools"></a>엔터티 데이터 모델 도구

Visual Studio는 Entity Framework 런타임과 함께 매핑 및 모델링 도구를 포함 합니다. 자세한 내용은 [모델링 및 매핑](modeling-and-mapping.md)을 참조 하세요.

## <a name="learn-more"></a>자세한 정보

Entity Framework에 대 한 자세한 내용은 다음을 참조 하세요.

[시작](getting-started.md) -간단한 Entity Framework 응용 프로그램을 만드는 방법을 보여 주는 [빠른](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb399182(v=vs.100))시작을 사용 하 여 빠르게 시작 하 고 실행 하는 방법에 대 한 정보를 제공 합니다.

[Entity Framework 용어](terminology.md) -엔터티 데이터 모델 및 Entity Framework에 의해 도입 된 여러 용어와 Entity Framework 설명서에서 사용 되는 용어를 정의 합니다.

[Entity Framework 리소스](resources.md) -개념 항목에 대 한 링크와 Entity Framework 응용 프로그램 빌드를 위한 외부 항목 및 리소스에 대 한 링크를 제공 합니다.

## <a name="see-also"></a>참고자료

- [ADO.NET Entity Framework](index.md)
