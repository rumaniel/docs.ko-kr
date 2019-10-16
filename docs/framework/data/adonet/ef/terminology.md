---
title: Entity Framework 용어
ms.date: 03/30/2017
ms.assetid: fa2a1bd1-6118-487b-8673-eebc66b92945
ms.openlocfilehash: c48361fd51ecb320416e76e599e36da12faf76fb
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854281"
---
# <a name="entity-framework-terminology"></a>Entity Framework 용어
이 항목에서는 Entity Framework 설명서에서 자주 참조 되는 용어를 정의 합니다. 추가 정보를 볼 수 있는 관련 항목에 대한 링크가 제공됩니다.  
  
|용어|정의|  
|----------|----------------|  
|연결(association)|엔터티 형식 간의 관계 정의입니다.<br /><br /> 자세한 내용은 [Association 요소 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#association-element-csdl) 및 [연결 형식](../association-type.md)을 참조 하세요.|  
|연결 집합(association set)|같은 형식의 연결 인스턴스를 위한 논리 컨테이너입니다.<br /><br /> 자세한 내용은 [AssociationSet 요소 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#associationset-element-csdl) 및 [연결 집합](../association-set.md)을 참조 하세요.|  
|Code First|Entity Framework 4.1부터는 Code First 개발을 통해 모델을 프로그램 방식으로 만들 수 있습니다. Code First 개발에는 두 가지 다른 시나리오가 있습니다. 두 경우 모두 개발자는 .NET Framewor 클래스 정의를 코딩하여 모델을 정의한 후 데이터 주석 또는 fluent API를 사용하여 추가 매핑 또는 구성을 선택적으로 지정합니다.<br /><br /> Code First 개발은 [Entity Framework 5.0](https://go.microsoft.com/fwlink/?LinkId=234900)의 일부입니다. Entity Framework 5.0은 .NET Framework의 일부가 아니지만 .NET Framework 4.5에 빌드되어 있습니다. Entity Framework 5.0은 [' Entity Framework '](https://go.microsoft.com/fwlink/?LinkID=215714)[NuGet](https://go.microsoft.com/fwlink/?LinkId=232488) 패키지로 사용할 수 있습니다. 자세한 내용은 [Entity Framework 릴리스 및 버전 관리](https://go.microsoft.com/fwlink/?LinkId=234899)를 참조 하세요.|  
|명령 트리|하나 이상의 식으로 구성 된 모든 Entity Framework 쿼리의 일반적인 프로그래밍 방식 표현입니다.<br /><br /> 자세한 내용은 [Entity Framework 개요](overview.md)를 참조 하세요.|  
|복합 형식|개념적 모델에서 정의된 복합 속성을 나타내는 .NET Framework 클래스입니다. 복합 형식을 사용하면 엔터티 내에 스칼라 속성을 구성할 수 있습니다. 복합 개체는 복합 형식의 인스턴스입니다. 자세한 내용은 [ComplexType 요소 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#complextype-element-csdl) 및 [복합 형식](../complex-type.md)을 참조 하세요.|  
|ComplexType|키 속성이 없는, 엔터티 형식의 스칼라가 아닌 속성을 나타내는 데이터 형식의 지정입니다.<br /><br /> 자세한 내용은 [ComplexType 요소 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#complextype-element-csdl) 및 [복합 형식](../complex-type.md)을 참조 하세요.|  
|개념 모델(conceptual model)|Entity Framework의 응용 프로그램 도메인에 있는 엔터티 형식, 복합 형식, 연결, 엔터티 컨테이너, 엔터티 집합 및 연결 집합에 대 한 추상 사양입니다. 개념적 모델은 .csdl 파일에 CSDL로 정의됩니다.<br /><br /> 자세한 내용은 [모델링 및 매핑](modeling-and-mapping.md)을 참조 하세요.|  
|.csdl 파일|CSDL로 표현된 개념적 모델이 포함된 XML 파일입니다.|  
|CSDL(개념 스키마 정의 언어)|개념 모델의 엔터티 형식, 연결, 엔터티 컨테이너, 엔터티 집합 및 연결 집합을 정의하는 데 사용되는 XML 기반 언어입니다.<br /><br /> 자세한 내용은 [CSDL Specification](./language-reference/csdl-specification.md)을 참조하십시오.|  
|컨테이너(container)|엔터티 및 연결 집합의 논리적 그룹입니다.<br /><br /> 자세한 내용은 [EntityContainer 요소 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#entitycontainer-element-csdl) 및 [엔터티 컨테이너](../entity-container.md)를 참조 하세요.|  
|동시성|여러 사용자들이 공유 데이터를 동시에 액세스 및 변경할 수 있도록 하는 프로세스입니다. 기본적으로 Entity Framework는 낙관적 동시성 모델을 구현 합니다.|  
|방향|일부 연결의 비대칭 특성을 나타냅니다. 방향은 스키마에 있는 `FromRole` 또는 `ToRole` 요소의 `NavigationProperty` 및 `ReferentialConstraint` 특성으로 지정됩니다.<br /><br /> 자세한 내용은 [NavigationProperty 요소 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#navigationproperty-element-csdl) 및 [탐색 속성](../navigation-property.md)을 참조 하세요.|  
|즉시 로드(eager loading)|쿼리에서 명시적으로 요청된 개체와 함께 특정한 관련 개체 집합을 로드하는 프로세스입니다.|  
|.edmx 파일|CSDL로 표현된 개념적 모델, SSDL로 표현된 스토리지 모델, MSL로 표현된 두 모델 간의 매핑이 포함된 XML 파일입니다. .Edmx 파일은 엔터티 데이터 모델 도구를 통해 생성 됩니다. 자세한 내용은 [.Edmx 파일 개요](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/cc982042(v=vs.100))를 참조 하세요.|  
|end|연결에 참여하는 엔터티입니다.<br /><br /> 자세한 내용은 [End 요소 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#end-element-csdl) 및 [연결 끝](../association-end.md)을 참조 하세요.|  
|엔터티(entity)|데이터 형식을 정의하는 데 사용되는 애플리케이션 도메인의 개념입니다.<br /><br /> 자세한 내용은 [EntityType 요소 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#entitytype-element-csdl) 및 [엔터티 형식](../entity-type.md)을 참조 하세요.|  
|EntityClient|, `EntityConnection` `EntityCommand`및 와같은클래스를포함하는저장소독립적인ADO.NET데이터공급자입니다.`EntityDataReader` 는와 [!INCLUDE[esql](../../../../../includes/esql-md.md)] 함께 작동 하며,와 `SqlClient`같은 저장소 관련 ADO.NET 데이터 공급자에 연결 합니다.<br /><br /> 자세한 내용은 [Entity Framework에 대 한 EntityClient 공급자](entityclient-provider-for-the-entity-framework.md)를 참조 하세요.|  
|엔터티 컨테이너(entity container)|지정한 네임스페이스에서 구현될 엔터티 집합과 연결 집합을 지정합니다.<br /><br /> 자세한 내용은 [EntityContainer 요소 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#entitycontainer-element-csdl) 및 [엔터티 컨테이너](../entity-container.md)를 참조 하세요.|  
|EDM(엔터티 데이터 모델)|저장된 폼에 관계없이 데이터 구조를 엔터티와 관계로 설명하는 개념 집합입니다.<br /><br /> 자세한 내용은 [엔터티 데이터 모델](../entity-data-model.md)를 참조 하세요.|  
|Entity Framework|개발자가 데이터 소스의 논리 스키마에 매핑된 개념적 모델을 사용할 수 있도록 하여 데이터 지향 소프트웨어 애플리케이션의 개발을 지원하는 기술 집합입니다.<br /><br /> 자세한 내용은 [Entity Framework 개요](overview.md)를 참조 하세요.|  
|엔터티 집합|지정된 형식 및 해당 하위 형식의 엔터티를 위한 논리적 컨테이너입니다. 엔터티 집합은 데이터베이스 테이블에 매핑됩니다.<br /><br /> 자세한 내용은 [EntitySet 요소 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#entityset-element-csdl) 및 [엔터티 집합](../entity-set.md)을 참조 하세요.|  
|Entity SQL|개념적 엔터티 스키마를 직접 사용하며 상속 및 관계와 같은 개념적 모델 개념을 지원하는, 스토리지에 독립적인 SQL 언어입니다.<br /><br /> 자세한 내용은 [Entity SQL Language](./language-reference/entity-sql-language.md)를 참조 하세요.|  
|엔터티 형식(entity type)|개념적 모델에 정의 된 엔터티를 나타내는 .NET Framework 클래스입니다. 엔터티 형식은 스칼라, 복합 및 탐색 속성을 가질 수 있습니다. 개체는 엔터티 형식의 인스턴스입니다. 자세한 내용은 [개체 작업](working-with-objects.md)을 참조 하세요.|  
|EntityType|키와 명명된 속성 집합을 포함하고 개념적 모델 또는 스토리지 모델의 최상위 항목을 나타내는 데이터 형식의 지정입니다.<br /><br /> 자세한 내용은 [EntityType 요소 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#entitytype-element-csdl) 및 [엔터티 형식](../entity-type.md)을 참조 하세요.|  
|명시적 로드(explicit loading)|개체가 쿼리에서 반환될 때 관련 개체가 동시에 로드되지 않습니다. 기본적으로 탐색 속성의 `Load` 메서드를 사용하여 명시적으로 요청할 때까지 관련 개체는 로드되지 않습니다.|  
|외래 키 연결(foreign key association)|외래 키 속성을 통해 관리되는 엔터티 간의 연결입니다.|  
|식별 관계(identifying relationship)|주 엔터티의 기본 키가 종속 엔터티의 기본 키에 속하는 관계입니다. 이러한 종류의 관계에서는 종속 엔터티가 주 엔터티 없이 존재할 수 없습니다.|  
|독립 연결(independent association)|독립 개체가 나타내고 추적하는 엔터티 간의 연결입니다.|  
|Key|엔터티 형식의 고유한 인스턴스를 식별하는 데 사용되는 속성 또는 속성 집합을 지정하는 엔터티 형식의 특성입니다. <xref:System.Data.EntityKey> 클래스에 의해 개체 계층에서 표현됩니다.<br /><br /> 자세한 내용은 [Key 요소 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#key-element-csdl) 및 [엔터티 키](../entity-key.md)를 참조 하세요.|  
|지연 로드(lazy loading)|개체가 쿼리에서 반환될 때 관련 개체가 동시에 로드되지 않습니다. 대신 탐색 속성에 액세스하면 관련 개체가 자동으로 로드됩니다.|  
|LINQ to Entities|탐색, 필터링 및 프로젝션 작업을 비주얼 C# 및 Visual Basic에서 직접 선언적 방식으로 표현할 수 있도록 하는 쿼리 연산자 집합을 정의 하는 쿼리 구문입니다.<br /><br /> 자세한 내용은 [LINQ to Entities](./language-reference/linq-to-entities.md)합니다.|  
|매핑|개념적 모델에 있는 항목과 스토리지 모델에 있는 항목 간의 대응 지정입니다.<br /><br /> 자세한 내용은 [MSL 사양](./language-reference/msl-specification.md)을 참조 하세요.|  
|.msl 파일|MSL로 표현된, 개념적 모델과 스토리지 모델 간의 매핑이 포함된 XML 파일입니다.|  
|MSL(매핑 사양 언어)|개념 모델에서 정의한 항목을 스토리지 모델의 항목에 매핑하는 데 사용되는 XML 기반 언어입니다.<br /><br /> 자세한 내용은 [MSL 사양](./language-reference/msl-specification.md)을 참조 하세요.|  
|수정 함수|데이터 소스에 있는 데이터를 삽입, 업데이트 및 삭제하는 데 사용되는 저장 프로시저입니다. 이러한 함수는 Entity Framework 생성 된 명령 대신 사용 됩니다. 수정 함수는 스토리지 모델의 `Function` 요소에 의해 정의됩니다. [ModificationFunctionMapping](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/cc716778(v=vs.100)) 요소는 이러한 수정 함수를 개념적 모델에 정의 된 엔터티에 대 한 삽입, 업데이트 및 삭제 작업에 매핑합니다.|  
|복합성|연결에서 정의된 대로 관계의 양쪽에 존재할 수 있는 엔터티 수입니다. 카디널리티라고도 합니다.<br /><br /> 자세한 내용은 [End 요소 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#end-element-csdl) 및 [연결 끝](../association-end.md)을 참조 하세요.|  
|형식별 다중 엔터티 집합|둘 이상의 엔터티 집합에서 같은 엔터티 형식을 정의할 수 있는 기능입니다.<br /><br /> 자세한 내용은 [EntitySet 요소 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#entityset-element-csdl) 및 [방법: 유형별](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738537(v=vs.100))다중 엔터티 집합을 사용 하 여 모델을 정의 합니다.|  
|탐색 속성(navigation property)|연결에서 정의된 대로 다른 엔터티 형식에 대한 관계를 나타내는 엔터티 형식의 속성입니다. 탐색 속성은 연결에서 반대쪽 End의 복합성에 따라 관련 개체를 <xref:System.Data.Objects.DataClasses.EntityCollection%601> 또는 <xref:System.Data.Objects.DataClasses.EntityReference%601>로 반환하는 데 사용됩니다.<br /><br /> 자세한 내용은 [NavigationProperty 요소 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#navigationproperty-element-csdl) 및 [탐색 속성](../navigation-property.md)을 참조 하세요.|  
|쿼리 경로|개체 쿼리가 실행될 때 반환할 관련 개체를 지정하는 경로의 문자열 표현입니다. 쿼리 경로는 <xref:System.Data.Objects.ObjectQuery%601.Include%2A>의 <xref:System.Data.Objects.ObjectQuery%601> 메서드를 호출하여 정의됩니다.<br /><br /> 자세한 내용은 [관련 개체 로드](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896272(v=vs.100))합니다.|  
|개체 컨텍스트|개념적 모델에서 정의된 엔터티 컨테이너를 나타냅니다. 기본 데이터 소스에 대한 연결을 포함하며, 변경 내용 추적 및 ID 확인과 같은 서비스를 제공합니다. 개체 컨텍스트는 <xref:System.Data.Objects.ObjectContext> 또는 `DbContext` 클래스 인스턴스로 표현됩니다.<br /><br /> `DbContext`는 [Entity Framework 5.0](https://go.microsoft.com/fwlink/?LinkId=234900)의 일부입니다. Entity Framework 5.0은 .NET Framework의 일부가 아니지만 .NET Framework 4.5에 빌드되어 있습니다. Entity Framework 5.0은 [' Entity Framework '](https://go.microsoft.com/fwlink/?LinkID=215714)[NuGet](https://go.microsoft.com/fwlink/?LinkId=232488) 패키지로 사용할 수 있습니다. 자세한 내용은 [Entity Framework 릴리스 및 버전 관리](https://go.microsoft.com/fwlink/?LinkId=234899)를 참조 하세요.|  
|개체 계층|Entity Framework에서 사용되는 엔터티 형식 및 개체 컨텍스트 정의입니다.|  
|개체 쿼리|개체 컨텍스트 내에서 개념적 모델에 대해 실행되어 데이터를 개체로 반환하는 쿼리입니다.<br /><br /> 자세한 내용은 [개체 쿼리](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896241(v=vs.100))합니다.|  
|개체-관계형 매핑|관계형 데이터베이스의 데이터를 개체 지향 소프트웨어 애플리케이션에서 사용할 수 있는 데이터 형식으로 변형하기 위한 기술입니다.<br /><br /> Entity Framework는 저장소 모델에 정의 된 관계형 데이터를 개념적 모델에 정의 된 데이터 형식에 매핑하여 개체 관계형 매핑 서비스를 제공 합니다.<br /><br /> 자세한 내용은 [모델링 및 매핑](modeling-and-mapping.md)을 참조 하세요.|  
|개체 서비스(Object Services)|Entity Framework에서 제공 하는 서비스로, 응용 프로그램 코드가 .NET Framework 개체와 같은 엔터티에 대해 작동할 수 있도록 합니다.|  
|지속성 무시 개체|데이터 스토리지와 관련된 논리가 포함되지 않은 개체입니다. POCO 엔터티라고도 합니다.|  
|POCO|Plain Old CLR Object입니다. 다른 클래스에서 상속하거나 인터페이스를 구현하지 않는 개체입니다.|  
|POCO 엔터티|<xref:System.Data.Objects.DataClasses.EntityObject> 또는<xref:System.Data.Objects.DataClasses.ComplexObject> 에서 상속 하지 않고 Entity Framework 인터페이스를 구현 하지 않는 Entity Framework의 엔터티입니다. POCO 엔터티는 Entity Framework 응용 프로그램에서 사용 하는 기존 도메인 개체입니다. 이러한 엔터티는 지속성 무시를 지원합니다. 자세한 내용은 [POCO 엔터티 작업](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dd456853(v=vs.100))을 참조 하세요.|  
|프록시 개체|POCO 클래스에서 파생 되 고 변경 내용 추적과 지연 로드를 지원 하기 위해 Entity Framework에 의해 생성 되는 개체입니다. 자세한 내용은 [POCO 프록시를 만들기 위한 요구 사항](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dd468057(v=vs.100))을 참조 하세요.|  
|참조 제약 조건(referential constraint)|엔터티와 다른 엔터티 간에 종속 관계가 있음을 나타내는, 개념적 모델에서 정의된 제약 조건입니다. 이 제약 조건은 해당하는 주 엔터티 인스턴스가 없을 경우 종속 엔터티 인스턴스가 존재할 수 없음을 의미합니다.<br /><br /> 자세한 내용은 참조 무결성 제약 조건 [요소 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#referentialconstraint-element-csdl) 및 [참조 무결성 제약 조건](../referential-integrity-constraint.md)을 참조 하세요.|  
|관계(relationship)|엔터티 간의 논리적 연결입니다.|  
|역할(role)|연결의 각 `End`에 지정되어 관계의 의미 체계를 설명하는 이름입니다.<br /><br /> 자세한 내용은 [End 요소 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#end-element-csdl) 및 [연결 끝](../association-end.md)을 참조 하세요.|  
|스칼라 속성|스토리지 모델의 단일 필드에 매핑되는 엔터티의 속성입니다.|  
|자체 추적 엔터티(self-tracking entity)|변경 내용을 스칼라 속성, 복합 속성 및 탐색 속성에 기록하는 기능이 있는 T4(Text Template Transformation Toolkit)에서 만들어진 엔터티입니다.|  
|단순 형식|개념적 모델에서 속성을 정의하는 데 사용되는 기본 형식입니다.<br /><br /> 자세한 내용은 [개념적 모델 형식 (CSDL)](/ef/ef6/modeling/designer/advanced/edmx/csdl-spec#conceptual-model-types-csdl) 및 [엔터티 데이터 모델을 참조 하세요. 기본 데이터 형식](../entity-data-model-primitive-data-types.md)입니다.|  
|분할 엔터티|스토리지 모델에 있는 두 개의 별도 형식에 매핑되는 엔터티 형식입니다.<br /><br /> 자세한 내용은 [방법: 두 테이블](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896233(v=vs.100))에 매핑된 단일 엔터티를 사용 하 여 모델을 정의 합니다.|  
|스토리지 모델|관계형 데이터베이스와 같은 지원되는 데이터 소스에 있는 데이터의 논리적 모델에 대한 정의입니다. 스토리지 모델은 스토리지 .ssdl 파일에서 SSDL로 정의됩니다.<br /><br /> 자세한 내용은 [모델링 및 매핑](modeling-and-mapping.md) 및 [SSDL 사양](./language-reference/ssdl-specification.md)을 참조 하세요.|  
|.ssdl 파일|SSDL로 표현된 스토리지 모델이 포함된 XML 파일입니다.|  
|SSDL(저장소 스키마 정의 언어)|흔히 데이터베이스 스키마에 해당하는 스토리지 모델의 엔터티 형식, 연결, 엔터티 컨테이너, 엔터티 집합 및 연결 집합을 정의하는 데 사용되는 XML 기반 언어입니다.<br /><br /> 자세한 내용은 [SSDL 사양](./language-reference/ssdl-specification.md)을 참조 하세요.|  
|계층당 하나의 테이블|형식 계층 구조를 모델링하는 방법 중 하나로, 계층 구조에 있는 모든 형식의 특성이 하나의 테이블에 포함됩니다.|  
|형식당 하나의 테이블|데이터베이스의 형식 계층 구조를 모델링하는 방법 중 하나로, 일대일 관계의 여러 테이블을 사용하여 다양한 형식을 모델링합니다.|  
  
## <a name="see-also"></a>참고자료

- [ADO.NET Entity Framework](index.md)
- [Entity Framework 개요](overview.md)
- [시작](getting-started.md)
- [Entity Framework 리소스](resources.md)
