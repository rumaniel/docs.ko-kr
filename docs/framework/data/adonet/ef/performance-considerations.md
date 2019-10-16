---
title: 성능 고려 사항(Entity Framework)
ms.date: 03/30/2017
ms.assetid: 61913f3b-4f42-4d9b-810f-2a13c2388a4a
ms.openlocfilehash: eb46b183ec1e930dfe5c4a1eea237024033c357d
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854608"
---
# <a name="performance-considerations-entity-framework"></a>성능 고려 사항(Entity Framework)
이 항목에서는 ADO.NET Entity Framework의 성능 특징에 대해 설명하고, Entity Framework 애플리케이션의 성능 개선을 위해 고려해야 할 몇 가지 사항을 알려 줍니다.  
  
## <a name="stages-of-query-execution"></a>쿼리 실행 단계  
 Entity Framework의 쿼리 성능을 보다 잘 이해하기 위해서는 쿼리가 개념적 모델에 대해 실행하고 데이터를 개체로 반환할 때 수행되는 작업을 알고 있는 것이 좋습니다. 다음 표에서는 이러한 일련의 작업에 대해 설명합니다.  
  
|연산|상대 비용|빈도|주석|  
|---------------|-------------------|---------------|--------------|  
|메타데이터 로드|보통|애플리케이션 도메인당 한 번|Entity Framework에서 사용되는 모델 및 매핑 메타데이터가 <xref:System.Data.Metadata.Edm.MetadataWorkspace>로 로드됩니다. 이 메타데이터는 전역으로 캐시되고 동일한 애플리케이션 도메인의 다른 <xref:System.Data.Objects.ObjectContext> 인스턴스에서 사용할 수 있습니다.|  
|데이터베이스 연결 열기|보통<sup>1</sup>|필요한 만큼|데이터베이스에 대 한 열린 연결은 중요 한 리소스를 사용 하기 때문에 Entity Framework는 필요한 경우에만 데이터베이스 연결을 열고 닫습니다. 또한 연결을 명시적으로 열 수 있습니다. 자세한 내용은 [트랜잭션과 연결 관리](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896325(v=vs.100))합니다.|  
|뷰 생성|높음|애플리케이션 도메인당 한 번 미리 생성할 수 있습니다.|Entity Framework에서 개념적 모델에 대해 쿼리를 실행하거나 데이터 소스에 변경 내용을 저장하려면 먼저 로컬 쿼리 뷰 집합을 생성하여 데이터베이스에 액세스해야 합니다. 이러한 뷰를 생성하는 데 비용이 많이 들기 때문에 디자인 타임에 뷰를 미리 생성한 후 프로젝트에 추가할 수 있습니다. 자세한 내용은 [방법: 뷰를 미리 생성 하 여 쿼리 성능을](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896240(v=vs.100))향상 시킵니다.|  
|쿼리 준비|보통<sup>2</sup>|고유 쿼리당 한 번|쿼리 명령을 작성하고, 모델 및 매핑 메타데이터를 기반으로 명령 트리를 생성하고, 반환된 데이터의 셰이프를 정의하는 비용을 포함합니다. Entity SQL 쿼리 명령과 LINQ 쿼리가 모두 캐시되므로 동일한 쿼리를 나중에 실행하는 경우 시간이 더 적게 걸립니다. 그러나, 여전히 컴파일된 LINQ 쿼리를 사용하여 나중에 실행할 때 이러한 비용을 줄일 수 있으며 컴파일된 쿼리는 자동으로 캐시되는 LINQ 쿼리에서보다 효율적으로 작동합니다. 자세한 내용은 [컴파일된 쿼리 (LINQ to Entities)](./language-reference/compiled-queries-linq-to-entities.md)를 참조 하세요. LINQ 쿼리 실행에 대 한 일반적인 내용은 [LINQ to Entities](./language-reference/linq-to-entities.md)를 참조 하세요. **참고:**  메모리 내 컬렉션에 `Enumerable.Contains` 연산자를 적용하는 LINQ to Entities 쿼리는 자동으로 캐시되지 않습니다. 또한 메모리 내 컬렉션은 컴파일된 LINQ 쿼리에서 매개 변수화할 수 없습니다.|  
|쿼리 실행|낮음<sup>2</sup>|쿼리당 한 번|ADO.NET 데이터 공급자를 사용하여 데이터 소스에 대해 명령을 실행하는 비용입니다. 대부분의 데이터 소스에서 쿼리 계획을 캐시하므로 동일한 쿼리를 나중에 실행하는 경우 시간이 더 적게 걸릴 수 있습니다.|  
|형식 로드 및 유효성 검사|낮음<sup>3</sup>|<xref:System.Data.Objects.ObjectContext> 인스턴스당 한 번|형식은 개념적 모델에서 정의하는 형식에 대해 로드되고 유효성이 검사됩니다.|  
|추적|낮음<sup>3</sup>|쿼리에서 반환하는 개체당 한 번 <sup>4</sup>|쿼리에서 <xref:System.Data.Objects.MergeOption.NoTracking> 병합 옵션을 사용하는 경우 이 단계는 성능에 영향을 주지 않습니다.<br /><br /> 쿼리에서 <xref:System.Data.Objects.MergeOption.AppendOnly>, <xref:System.Data.Objects.MergeOption.PreserveChanges> 또는 <xref:System.Data.Objects.MergeOption.OverwriteChanges> 병합 옵션을 사용하는 경우 <xref:System.Data.Objects.ObjectStateManager>에서 쿼리 결과를 추적합니다. 쿼리가 반환한 각 추적된 개체에 대해 <xref:System.Data.EntityKey>가 생성되고 이는 <xref:System.Data.Objects.ObjectStateEntry>에서 <xref:System.Data.Objects.ObjectStateManager>를 만드는 데 사용됩니다. <xref:System.Data.Objects.ObjectStateEntry>에 대한 기존 <xref:System.Data.EntityKey>를 찾을 수 있는 경우 기존 개체가 반환됩니다. <xref:System.Data.Objects.MergeOption.PreserveChanges> 또는 <xref:System.Data.Objects.MergeOption.OverwriteChanges> 옵션이 사용되는 경우 개체를 반환하기 전에 업데이트합니다.<br /><br /> 자세한 내용은 [Id 확인, 상태 관리 및 변경 내용 추적](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896269(v=vs.100))합니다.|  
|개체 구체화|보통<sup>3</sup>|쿼리에서 반환하는 개체당 한 번 <sup>4</sup>|반환된 <xref:System.Data.Common.DbDataReader> 개체를 읽고, <xref:System.Data.Common.DbDataRecord> 클래스의 각 인스턴스에 있는 값을 기준으로 개체를 만들고 속성 값을 설정하는 프로세스입니다. <xref:System.Data.Objects.ObjectContext>에 이미 개체가 있고 쿼리에서 <xref:System.Data.Objects.MergeOption.AppendOnly> 또는 <xref:System.Data.Objects.MergeOption.PreserveChanges> 병합 옵션을 사용하는 경우 이 단계는 성능에 영향을 주지 않습니다. 자세한 내용은 [Id 확인, 상태 관리 및 변경 내용 추적](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896269(v=vs.100))합니다.|  
  
 <sup>1</sup> 데이터 원본 공급자가 연결 풀링을 구현 하는 경우 연결을 여는 비용이 풀 전체에 분산 됩니다. .NET Provider for SQL Server에서는 연결 풀링을 지원합니다.  
  
 <sup>2</sup> 비용은 쿼리 복잡성이 증가 함에 따라 증가 합니다.  
  
 <sup>3</sup> 쿼리에서 반환 되는 개체 수에 비례하여 총 비용이 늘어납니다.  
  
 <sup>4</sup> entityclient 쿼리가 개체 대신를 <xref:System.Data.EntityClient.EntityDataReader> 반환 하므로 entityclient 쿼리에는이 오버 헤드가 필요 하지 않습니다. 자세한 내용은 [Entity Framework에 대 한 EntityClient 공급자](entityclient-provider-for-the-entity-framework.md)를 참조 하세요.  
  
## <a name="additional-considerations"></a>기타 고려 사항  
 다음은 Entity Framework 애플리케이션의 성능에 영향을 줄 수 있는 기타 고려 사항입니다.  
  
### <a name="query-execution"></a>쿼리 실행  
 쿼리는 리소스를 많이 사용할 수 있으므로 코드의 어느 시점에, 어느 컴퓨터에서 쿼리를 실행하는지 살펴보세요.  
  
#### <a name="deferred-versus-immediate-execution"></a>지연된 실행과 즉시 실행 비교  
 <xref:System.Data.Objects.ObjectQuery%601> 또는 LINQ 쿼리를 만들 때 쿼리가 즉시 실행되지 않을 수 있습니다. 쿼리 실행은 `foreach`(C#)나 `For Each`(Visual Basic) 열거 시 또는 <xref:System.Collections.Generic.List%601> 컬렉션을 채우도록 지정된 경우와 같이 결과가 필요할 때까지 지연됩니다. 쿼리 실행은 사용자가 <xref:System.Data.Objects.ObjectQuery%601.Execute%2A>에서 <xref:System.Data.Objects.ObjectQuery%601> 메서드를 호출하거나 <xref:System.Linq.Enumerable.First%2A> 또는 <xref:System.Linq.Enumerable.Any%2A>와 같은 단일 쿼리를 반환하는 LINQ 메서드를 호출할 때 즉시 시작됩니다. 자세한 내용은 [개체 쿼리](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896241(v=vs.100)) 및 [쿼리 실행 (LINQ to Entities)](./language-reference/query-execution.md)을 참조 하세요.  
  
#### <a name="client-side-execution-of-linq-queries"></a>LINQ 쿼리의 클라이언트 쪽 실행  
 LINQ 쿼리 실행은 데이터 소스를 호스트하는 컴퓨터에서 이루어지지만 일부 LINQ 쿼리는 클라이언트 컴퓨터에서 확인됩니다. 자세한 내용은 쿼리 실행의 저장소 실행 섹션 [(LINQ to Entities)](./language-reference/query-execution.md)을 참조 하세요.  
  
### <a name="query-and-mapping-complexity"></a>쿼리 및 매핑 복잡성  
 엔터티 모델의 매핑 및 개별 쿼리의 복잡성은 쿼리 성능에 상당한 영향을 줍니다.  
  
#### <a name="mapping-complexity"></a>매핑 복잡성  
 개념적 모델의 엔터티와 스토리지 모델의 테이블 간 단순 일대일 매핑보다 다소 복잡한 모델은 일대일 매핑의 모델보다 복잡한 명령을 생성합니다.  
  
#### <a name="query-complexity"></a>쿼리 복잡성  
 데이터 소스에 대해 실행되는 명령에 많은 수의 조인이 필요하거나 많은 양의 데이터를 반환하는 쿼리는 다음 방식으로 성능에 영향을 줄 수 있습니다.  
  
- 간단해 보이는 개념적 모델의 쿼리로 인해 데이터 소스에 대해 보다 복잡한 쿼리가 실행될 수 있습니다. 이는 Entity Framework에서 개념적 모델에 대한 쿼리를 데이터 소스에 대한 동등한 쿼리로 변환하기 때문에 발생합니다. 개념적 모델의 단일 엔터티 집합이 데이터 소스에 있는 둘 이상의 테이블에 매핑되거나 엔터티 간 관계가 조인 테이블에 매핑되면 데이터 소스 쿼리에 대해 실행되는 쿼리 명령에서 하나 이상의 조인을 필요로 할 수 있습니다.  
  
    > [!NOTE]
    > <xref:System.Data.Objects.ObjectQuery.ToTraceString%2A> 또는 <xref:System.Data.Objects.ObjectQuery%601> 클래스의 <xref:System.Data.EntityClient.EntityCommand> 메서드를 사용하여 제공된 쿼리의 데이터 소스에 대해 실행된 명령을 볼 수 있습니다. 자세한 내용은 [방법: 저장소 명령을](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896348(v=vs.100))확인 합니다.  
  
- 중첩 Entity SQL 쿼리는 서버에서 조인을 만들고 많은 수의 행을 반환할 수 있습니다.  
  
     다음은 프로젝션 절의 중첩 쿼리 예제입니다.  
  
    ```  
    SELECT c, (SELECT c, (SELECT c FROM AdventureWorksModel.Vendor AS c  ) As Inner2   
        FROM AdventureWorksModel.JobCandidate AS c  ) As Inner1   
        FROM AdventureWorksModel.EmployeeDepartmentHistory AS c  
    ```  
  
     또한 이러한 쿼리로 인해 쿼리 파이프라인이 중첩 쿼리에 대해 개체가 중복된 단일 쿼리를 생성할 수 있습니다. 이에 따라 단일 열이 여러 번 중복될 수 있습니다. SLQ Server를 비롯한 일부 데이터베이스에서는 이로 인해 TempDB 테이블 크기가 과도하게 커질 수 있으므로 서버 성능이 저하될 수 있습니다. 중첩 쿼리를 실행할 때는 주의를 기울여야 합니다.  
  
- 많은 양의 데이터를 반환하는 쿼리는 클라이언트가 결과 집합의 크기에 비례하여 리소스를 사용하는 작업을 수행할 경우 성능이 저하될 수 있습니다. 그러므로 쿼리에서 반환되는 데이터 양을 제한하는 것이 좋습니다. 자세한 내용은 [방법: 쿼리 결과](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738702(v=vs.100))를 통해 페이지를 이동 합니다.  
  
 Entity Framework에 의해 자동으로 생성된 명령은 데이터베이스 개발자가 명시적으로 작성한 유사 명령보다 복잡할 수 있습니다. 데이터 소스에 대해 실행된 명령에 명시적 제어가 필요한 경우 테이블 반환 함수 또는 저장 프로시저에 대한 매핑을 정의하는 것이 좋습니다.  
  
#### <a name="relationships"></a>관계  
 최적의 쿼리 성능을 위해 엔터티 간 관계를 엔터티 모델의 연결과 데이터 소스의 논리적 관계로 정의해야 합니다.  
  
### <a name="query-paths"></a>쿼리 경로  
 기본적으로 <xref:System.Data.Objects.ObjectQuery%601>를 실행할 때 자체적으로 관계를 나타내는 개체는 반환되지만 관련 개체는 반환되지 않습니다. 관련 개체는 다음 세 가지 방법 중 하나로 로드할 수 있습니다.  
  
1. <xref:System.Data.Objects.ObjectQuery%601>가 실행되기 전에 쿼리 경로를 설정합니다.  
  
2. 개체가 노출하는 탐색 속성에서 `Load` 메서드를 호출합니다.  
  
3. <xref:System.Data.Objects.ObjectContextOptions.LazyLoadingEnabled%2A>에서 <xref:System.Data.Objects.ObjectContext> 옵션을 `true`로 설정합니다. [엔터티 데이터 모델 Designer](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/cc716685(v=vs.100))를 사용 하 여 개체 계층 코드를 생성 하면이 작업이 자동으로 수행 됩니다. 자세한 내용은 [생성 된 코드 개요](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/cc982041(v=vs.100))를 참조 하세요.  
  
 사용할 옵션을 고려할 때는 데이터베이스에 대한 요청의 수와 단일 쿼리에 반환되는 데이터의 양이 서로 상쇄되는 관계임을 염두에 두어야 합니다. 자세한 내용은 [관련 개체 로드](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896272(v=vs.100))합니다.  
  
#### <a name="using-query-paths"></a>쿼리 경로 사용  
 쿼리 경로는 쿼리가 반환하는 개체의 그래프를 정의합니다. 쿼리 경로를 정의하면 데이터베이스에 대한 단일 요청만이 경로에 정의된 모든 개체를 반환하면 됩니다. 쿼리 경로를 사용하면 단순 개체 쿼리의 데이터 소스에 대해 복잡한 명령이 실행될 수 있습니다. 이는 관련 개체를 단일 쿼리에서 반환하려면 조인이 하나 이상 필요하기 때문에 발생합니다. 이러한 복잡성은 다대다 관계가 포함된 상속이나 경로를 가진 엔터티와 같은 복합 엔터티 모델에 대한 쿼리에서 더 커집니다.  
  
> [!NOTE]
> <xref:System.Data.Objects.ObjectQuery.ToTraceString%2A>에서 생성되는 명령을 보려면 <xref:System.Data.Objects.ObjectQuery%601> 메서드를 사용하세요. 자세한 내용은 [방법: 저장소 명령을](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896348(v=vs.100))확인 합니다.  
  
 쿼리 경로에 관련 개체가 너무 많거나 개체에 행 데이터가 너무 많은 경우 데이터 소스에서 쿼리를 완료하지 못할 수 있습니다. 쿼리에 필요한 중간 임시 스토리지가 데이터 소스의 용량을 초과하는 경우 이런 현상이 발생할 수 있습니다. 이 경우, 관련 개체를 명시적으로 로드하는 방법으로 데이터 원본 쿼리의 복잡성을 줄일 수 있습니다.  
  
#### <a name="explicitly-loading-related-objects"></a>명시적으로 관련 개체 로드  
 `Load` 또는 <xref:System.Data.Objects.DataClasses.EntityCollection%601>를 반환하는 탐색 속성에서 <xref:System.Data.Objects.DataClasses.EntityReference%601> 메서드를 호출하여 관련 개체를 명시적으로 로드할 수 있습니다. 명시적으로 개체를 로드하는 경우 `Load`가 호출될 때마다 데이터베이스에 대한 라운드트립이 필요합니다.  
  
> [!NOTE]
> `Load` 문(Visual Basic에서는 `foreach`)을 사용하는 경우와 같이 반환된 개체 컬렉션을 반복하면서 `For Each`를 호출하는 경우 데이터 소스 관련 공급자는 단일 연결에서 여러 활성 결과 집합을 지원해야 합니다. SQL Server 데이터베이스의 경우 공급자 연결 문자열에서 `MultipleActiveResultSets = true` 값을 지정해야 합니다.  
  
 엔터티에 <xref:System.Data.Objects.ObjectContext.LoadProperty%2A> 또는 <xref:System.Data.Objects.DataClasses.EntityCollection%601> 속성이 없는 경우에는 <xref:System.Data.Objects.DataClasses.EntityReference%601> 메서드를 사용할 수도 있습니다. 이 메서드는 POCO 엔터티를 사용하는 경우에 유용합니다.  
  
 관련 개체를 명시적으로 로드할 때 조인 수 및 중복 데이터 양이 줄어들지만 `Load`에서 데이터베이스에 대한 연결을 반복해야 합니다. 이러한 반복 작업은 많은 수의 개체를 명시적으로 로드하는 경우 비용이 많이 들 수 있습니다.  
  
### <a name="saving-changes"></a>변경 내용 저장  
 <xref:System.Data.Objects.ObjectContext.SaveChanges%2A>에서 <xref:System.Data.Objects.ObjectContext> 메서드를 호출할 때 컨텍스트에서 추가되거나, 업데이트되거나, 삭제된 각각의 개체에 대해 별도의 만들기, 업데이트 또는 삭제 명령이 생성됩니다. 이러한 명령은 데이터 소스에서 단일 트랜잭션으로 실행됩니다. 쿼리와 마찬가지로 만들기, 업데이트 및 삭제 작업의 성능은 개념적 모델에서의 매핑 복잡성에 따라 다릅니다.  
  
### <a name="distributed-transactions"></a>분산 트랜잭션  
 DTC(Distributed Transaction Coordinator)에 의해 관리되는 리소스가 필요한 명시적 트랜잭션에서의 작업은 DTC가 필요하지 않은 유사한 작업보다 비용이 훨씬 많이 듭니다. DTC로의 승격은 다음 상황에 발생할 수 있습니다.  
  
- 항상 명시적 트랜잭션을 DTC로 승격하는 SQL Server 2000 데이터베이스 또는 기타 데이터 소스에 대한 작업을 포함하는 명시적 트랜잭션  
  
- Entity Framework에서 연결을 관리 하는 경우 SQL Server 2005에 대 한 작업이 포함 된 명시적 트랜잭션입니다. 이는 Entity Framework의 기본 동작인 단일 트랜잭션 내에서 연결이 닫히고 다시 열릴 때마다 SQL Server 2005가 DTC로 승격 되기 때문에 발생 합니다. 이 DTC 승격은 SQL Server 2008 사용 시 발생하지 않습니다. SQL Server 2005를 사용할 때 이러한 승격이 발생하지 않도록 하려면 트랜잭션 내에서 연결을 명시적으로 열고 닫아야 합니다. 자세한 내용은 [트랜잭션과 연결 관리](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896325(v=vs.100))합니다.  
  
 <xref:System.Transactions> 트랜잭션 내에서 하나 이상의 작업이 실행될 때 명시적 트랜잭션이 사용됩니다. 자세한 내용은 [트랜잭션과 연결 관리](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896325(v=vs.100))합니다.  
  
## <a name="strategies-for-improving-performance"></a>성능 향상 전략  
 다음 전략을 사용하면 Entity Framework에서 쿼리의 전체 성능을 향상시킬 수 있습니다.  
  
#### <a name="pre-generate-views"></a>뷰 미리 생성  
 엔터티 모델을 기반으로 하는 뷰 생성 작업은 처음 애플리케이션에서 쿼리를 실행할 때 상당한 비용이 듭니다. EdmGen.exe 유틸리티를 사용하면 디자인 시 프로젝트에 추가할 수 있는 Visual Basic 또는 C# 코드 파일로 뷰를 미리 생성할 수 있습니다. T4(Text Template Transformation Toolkit)를 사용하여 미리 컴파일된 뷰를 생성할 수도 있습니다. 또한 런타임에 미리 생성된 뷰의 유효성을 검사하여 지정된 엔터티 모델의 현재 버전과 일치하는지 확인할 수 있습니다. 자세한 내용은 [방법: 뷰를 미리 생성 하 여 쿼리 성능을](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896240(v=vs.100))향상 시킵니다.
  
 매우 큰 모델로 작업하는 경우 고려할 사항은 다음과 같습니다.  
  
 .NET 메타데이터 형식은 지정된 이진 파일의 사용자 문자열 문자 수를 16,777,215(0xFFFFFF)로 제한합니다. 매우 큰 모델에 대 한 뷰를 생성 하는 경우 뷰 파일이이 크기 제한에 도달 하면 "남아 있는 논리 공간이 없으므로 사용자 문자열을 더 이상 만들 수 없습니다." 라는 메시지가 나타납니다. 컴파일 오류입니다. 이 크기 제한은 관리되는 모든 이진 파일에 적용됩니다. 자세한 내용은 크고 복잡 한 모델을 사용할 때 오류를 방지 하는 방법을 보여 주는 [블로그](https://go.microsoft.com/fwlink/?LinkId=201476) 를 참조 하세요.  
  
#### <a name="consider-using-the-notracking-merge-option-for-queries"></a>쿼리에 대한 NoTracking 병합 옵션 사용  
 개체 컨텍스트에서 반환된 개체를 추적하려면 비용이 필요합니다. 개체에 대한 변경 내용을 감지하고 동일한 논리 엔터티에 대한 여러 요청에서 동일한 개체 인스턴스를 반환하도록 할 경우 개체가 <xref:System.Data.Objects.ObjectContext> 인스턴스에 연결되어야 합니다. 개체를 업데이트 하거나 삭제할 계획이 없고 id 관리가 필요 하지 않은 경우 쿼리를 실행할 때 병합 옵션을 사용 하 <xref:System.Data.Objects.MergeOption.NoTracking> 는 것이 좋습니다.  
  
#### <a name="return-the-correct-amount-of-data"></a>적절한 양의 데이터 반환  
 일부 시나리오에서는 <xref:System.Data.Objects.ObjectQuery%601.Include%2A> 메서드를 사용하여 쿼리 경로를 지정하는 작업을 수행하면 데이터베이스에 대한 라운드트립 수가 줄어들어 훨씬 속도가 빨라집니다. 그러나 또 다른 시나리오에서는 조인 수가 더 적은 아주 간단한 쿼리로 인해 데이터가 덜 중복되어 관련 개체를 로드하는 데이터베이스에 대한 추가 라운드트립의 속도가 보다 더 빠를 수 있습니다. 이 때문에 관련 개체를 검색하는 여러 방법의 성능을 테스트하는 것이 좋습니다. 자세한 내용은 [관련 개체 로드](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896272(v=vs.100))합니다.  
  
 단일 쿼리에서 너무 많은 데이터가 반환되지 않도록 하려면 쿼리 결과를 보다 관리하기 쉬운 그룹으로 페이징하세요. 자세한 내용은 [방법: 쿼리 결과](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738702(v=vs.100))를 통해 페이지를 이동 합니다.  
  
#### <a name="limit-the-scope-of-the-objectcontext"></a>ObjectContext의 범위 제한  
 대부분의 경우 <xref:System.Data.Objects.ObjectContext> 문(Visual Basic에서는 `using`) 내에서 `Using…End Using` 인스턴스를 만들어야 합니다. 이렇게 하면 코드가 문 블록을 종료할 때 개체 컨텍스트와 연결된 리소스가 자동으로 삭제되도록 하여 성능을 향상시킬 수 있습니다. 그러나 컨트롤이 개체 컨텍스트에서 관리하는 개체로 바인딩된 경우 바인딩이 필요할 때까지 <xref:System.Data.Objects.ObjectContext> 인스턴스가 유지 관리되어야 하고, 그렇지 않은 경우 해당 인스턴스가 수동으로 삭제되어야 합니다. 자세한 내용은 [트랜잭션과 연결 관리](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896325(v=vs.100))합니다.  
  
#### <a name="consider-opening-the-database-connection-manually"></a>수동으로 데이터베이스 연결 열기  
 응용 프로그램에서 일련의 개체 쿼리를 실행 하거나 자주 호출 <xref:System.Data.Objects.ObjectContext.SaveChanges%2A> 하 여 데이터 원본에 대 한 만들기, 업데이트 및 삭제 작업을 유지 하는 경우 Entity Framework는 지속적으로 데이터 원본에 대 한 연결을 열고 닫아야 합니다. 이러한 경우 해당 작업 시작 시 연결을 수동으로 열고, 작업 완료 시 연결을 수동으로 닫거나 삭제하세요. 자세한 내용은 [트랜잭션과 연결 관리](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896325(v=vs.100))합니다.  
  
## <a name="performance-data"></a>성능 데이터  
 Entity Framework에 대 한 일부 성능 데이터는 [ADO.NET 팀 블로그의](https://go.microsoft.com/fwlink/?LinkId=91905)다음 게시물에 게시 됩니다.  
  
- [ADO.NET Entity Framework의 성능 살펴보기-1 부](https://go.microsoft.com/fwlink/?LinkId=123907)  
  
- [ADO.NET Entity Framework의 성능 살펴보기 – 2 부](https://go.microsoft.com/fwlink/?LinkId=123909)  
  
- [ADO.NET Entity Framework 성능 비교](https://go.microsoft.com/fwlink/?LinkID=123913)  
  
## <a name="see-also"></a>참고자료

- [개발 및 배포 고려 사항](development-and-deployment-considerations.md)
