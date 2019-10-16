---
title: 질문과 대답
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 252ed666-0679-4eea-b71b-2f14117ef443
ms.openlocfilehash: ed9149eb5b88d648c02863e0fb0101e5503e1c73
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70782148"
---
# <a name="frequently-asked-questions"></a>질문과 대답

다음 단원에서는 [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)]를 구현할 때 발생할 수 있는 일반적인 문제에 대한 해결 방법을 제시합니다.

[문제 해결](troubleshooting.md)에서는 추가 문제를 해결 합니다.

## <a name="cannot-connect"></a>연결할 수 없음

질문. 데이터베이스에 연결할 수 없습니다.

1\. 연결 문자열이 올바르고 SQL Server 인스턴스가 실행 되 고 있는지 확인 합니다. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]을 사용하려면 명명된 파이프 프로토콜도 사용하도록 설정해야 합니다. 자세한 내용은 [연습 별 학습](learning-by-walkthroughs.md)을 참조 하세요.

## <a name="changes-to-database-lost"></a>데이터베이스 변경 내용 손실

질문. 데이터베이스의 데이터를 변경했는데 애플리케이션을 다시 실행했더니 변경 내용이 없어졌습니다.

1\. <xref:System.Data.Linq.DataContext.SubmitChanges%2A>를 호출하여 결과를 데이터베이스에 저장해야 합니다.

## <a name="database-connection-open-how-long"></a>데이터베이스 연결: 기간을 엽니다.

질문. 데이터베이스는 얼마 동안 연결된 상태로 유지됩니까?

1\. 일반적으로 연결은 쿼리 결과를 사용할 때까지 유지됩니다. 모든 결과를 처리하는 데 시간이 많이 걸릴 것으로 예상되고 결과를 캐시해도 상관 없다면 쿼리에 <xref:System.Linq.Enumerable.ToList%2A> ¦ Àû ëÇÏ Ê Ã À. 각 개체를 한 번만 처리하는 일반적인 시나리오에서는 `DataReader` 및 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 모두에서 스트리밍 모델을 사용하는 것이 더 효과적입니다.

세부적인 연결 사용은 다음에 따라 달라집니다.

- 연결 개체를 사용하여 <xref:System.Data.Linq.DataContext>를 만든 경우의 연결 상태

- 연결 문자열 설정(예: MARS(Multiple Active Result Sets) 사용). 자세한 내용은 [MARS(여러 활성 결과 집합)](../multiple-active-result-sets-mars.md)를 참조하세요.

## <a name="updating-without-querying"></a>쿼리하지 않고 업데이트

질문. 데이터베이스를 먼저 쿼리하지 않고 테이블 데이터를 업데이트할 수 있습니까?

1\. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에는 설정 기반의 업데이트 명령이 없지만 다음 기술 중 하나를 사용하여 쿼리 없이 업데이트할 수 있습니다.

- <xref:System.Data.Linq.DataContext.ExecuteCommand%2A>를 사용하여 SQL 코드를 보냅니다.

- 개체의 새 인스턴스를 만든 후 업데이트에 영향을 주는 현재 값(필드)을 모두 초기화합니다. 그런 다음 <xref:System.Data.Linq.DataContext>를 사용하여 개체를 <xref:System.Data.Linq.Table%601.Attach%2A>에 연결하고 변경할 필드를 수정합니다.

## <a name="unexpected-query-results"></a>예기치 않은 쿼리 결과

질문. 쿼리가 예기치 않은 결과를 반환합니다. 무슨 문제가 있는지 어떻게 확인합니까?

1\. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에는 생성된 SQL 코드를 검사할 수 있는 도구가 여러 가지 있습니다. 그 중에서도 <xref:System.Data.Linq.DataContext.Log%2A>가 가장 중요합니다. 자세한 내용은 [디버깅 지원](debugging-support.md)을 참조 하세요.

## <a name="unexpected-stored-procedure-results"></a>예기치 않은 저장 프로시저 결과

질문. `MAX()`를 사용하여 반환 값을 계산하는 저장 프로시저를 사용하고 있습니다. 저장 프로시저를 O/R 디자이너 화면으로 끌면 반환 값이 올바르지 않습니다.

1\. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 다음과 같은 두 가지 방법으로 데이터베이스에서 생성된 값을 저장 프로시저를 통해 반환합니다.

- 출력 결과에 이름을 지정하는 방법

- 출력 매개 변수를 명시적으로 지정하는 방법

다음은 잘못된 출력의 예제입니다. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]은 결과를 매핑할 수 없기 때문에 항상 0을 반환합니다.

```sql
create procedure proc2

as

begin

select max(i) from t where name like 'hello'

end
```

다음은 출력 매개 변수를 사용하여 얻은 올바른 출력의 예제입니다.

```sql
create procedure proc2

@result int OUTPUT

as

select @result = MAX(i) from t where name like 'hello'

go
```

다음은 출력 결과에 이름을 지정하여 얻은 올바른 출력의 예제입니다.

```sql
create procedure proc2

as

begin

select nax(i) AS MaxResult from t where name like 'hello'

end
```

자세한 내용은 [저장 프로시저를 사용 하 여 작업 사용자 지정](customizing-operations-by-using-stored-procedures.md)을 참조 하세요.

## <a name="serialization-errors"></a>Serialization 오류

질문. Serialize 하려고 하면 다음과 같은 오류가 발생 합니다. "Type ' ChangeTracker + StandardChangeTracker ' ... serializable로 표시 되어 있지 않습니다. "

1\. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 코드 생성은 <xref:System.Runtime.Serialization.DataContractSerializer> serialization을 지원하지만 <xref:System.Xml.Serialization.XmlSerializer> 또는 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>는 지원하지 않습니다. 자세한 내용은 [Serialization](serialization.md)을 참조하세요.

## <a name="multiple-dbml-files"></a>여러 DBML 파일

질문. 여러 DBML 파일에서 일부 테이블을 공유할 경우 컴파일 오류가 발생합니다.

1\. 개체 관계형 디자이너의 **컨텍스트 네임 스페이스** 및 **엔터티 네임 스페이스** 속성을 각 DBML 파일에 대 한 고유 값으로 설정 합니다. 이렇게 하면 이름/네임스페이스 충돌이 해결됩니다.

## <a name="avoiding-explicit-setting-of-database-generated-values-on-insert-or-update"></a>삽입 또는 업데이트 시 데이터베이스에서 생성된 값을 명시적으로 설정해야 하는 문제 방지

질문. 데이터베이스 테이블에 SQL `DateCreated`를 기본값으로 사용하는 `Getdate()` 열이 있습니다. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]을 사용하여 새 레코드를 삽입하려고 하면 값이 `NULL`로 설정됩니다. 데이터베이스의 기본값이 설정되어야 하지 않나요?

1\. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]은 ID(자동 증분)와 rowguidcol(데이터베이스에서 생성된 GUID) 및 타임스탬프 열에 대해서만 이와 같이 기본값을 적용합니다. <xref:System.Data.Linq.Mapping.ColumnAttribute.IsDbGenerated%2A> 및 속성을<xref:System.Data.Linq.Mapping.AutoSync.OnUpdate> 수동으로 설정 = `true` 해야 하는 경우도 있습니다. <xref:System.Data.Linq.Mapping.ColumnAttribute.AutoSync%2A> = <xref:System.Data.Linq.Mapping.AutoSync.Always> / <xref:System.Data.Linq.Mapping.AutoSync.OnInsert> /

## <a name="multiple-dataloadoptions"></a>여러 DataLoadOptions

질문. 첫 번째 로드 옵션을 덮어쓰지 않고 다른 로드 옵션을 지정할 수 있습니까?

1\. 예. 다음 예제에서처럼 첫 번째 로드 옵션을 덮어쓰지 않습니다.

```vb
Dim dlo As New DataLoadOptions()
dlo.LoadWith(Of Order)(Function(o As Order) o.Customer)
dlo.LoadWith(Of Order)(Function(o As Order) o.OrderDetails)
```

```csharp
DataLoadOptions dlo = new DataLoadOptions();
dlo.LoadWith<Order>(o => o.Customer);
dlo.LoadWith<Order>(o => o.OrderDetails);
```

## <a name="errors-using-sql-compact-35"></a>SQL Compact 3.5 사용 오류

질문. SQL Server Compact 3.5 데이터베이스에서 테이블을 끌어올 때 오류가 발생 합니다.

1\. 개체 관계형 디자이너는 SQL Server Compact 3.5를 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 지원 하지 않습니다. 이 경우에는 고유 엔터티 클래스를 만들어 적절한 특성을 추가해야 합니다.

## <a name="errors-in-inheritance-relationships"></a>상속 관계 오류

질문. 개체 관계형 디자이너에서 도구 상자 상속 셰이프를 사용 하 여 두 엔터티를 연결 했지만 오류가 발생 했습니다.

1\. 관계를 만드는 것만으로는 부족합니다. 판별자 열, 기본 클래스 판별자 값 및 파생 클래스 판별자 값 등의 정보를 제공해야 합니다.

## <a name="provider-model"></a>공급자 모델

질문. 사용할 수 있는 공용 공급자 모델이 있습니까?

1\. 아니요, 사용할 수 있는 공용 공급자 모델은 없습니다. 지금은 SQL Server 및 SQL Server Compact 3.5만 지원합니다.[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]

## <a name="sql-injection-attacks"></a>SQL 삽입 공격

질문. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]은 SQL 삽입 공격으로부터 어떻게 보호됩니까?

1\. 사용자 입력을 연결하여 만든 기존 SQL 쿼리의 경우에는 SQL 삽입 공격이 상당히 큰 위협 요소였습니다. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 쿼리에 <xref:System.Data.SqlClient.SqlParameter>를 사용하여 이러한 삽입 공격을 방지합니다. 즉, 사용자 입력은 매개 변수 값으로 변환됩니다. 이 방법을 사용하면 사용자 입력을 통해 악의적인 명령이 사용되는 문제를 방지할 수 있습니다.

## <a name="changing-read-only-flag-in-dbml-files"></a>DBML 파일에서 읽기 전용 플래그 변경

질문. DBML 파일에서 개체 모델을 만들 때 일부 속성의 setter를 어떻게 제거합니까?

1\. 이와 같은 고급 시나리오에서는 다음과 같은 단계를 수행하세요.

1. .dbml 파일에서 <xref:System.Data.Linq.ITable.IsReadOnly%2A> 플래그를 `True`로 변경하여 속성을 수정합니다.

2. 부분 클래스를 추가합니다. 읽기 전용 멤버에 대해 매개 변수가 있는 생성자를 만듭니다.

3. 기본 <xref:System.Data.Linq.Mapping.UpdateCheck> 값(<xref:System.Data.Linq.Mapping.UpdateCheck.Never>)을 검토하여 애플리케이션에 사용할 수 있는 올바른 값인지 확인합니다.

    > [!CAUTION]
    > Visual Studio에서 개체 관계형 디자이너를 사용 하는 경우 변경 내용을 덮어쓸 수 있습니다.

## <a name="aptca"></a>APTCA

질문. 부분적으로 신뢰할 수 있는 코드에서 System.Data.Linq를 사용할 수 있습니까?

1\. 예, system.string 어셈블리는 <xref:System.Security.AllowPartiallyTrustedCallersAttribute> 특성으로 표시 된 .NET Framework 어셈블리 사이에 있습니다. 이 표시가 없으면 .NET Framework의 어셈블리는 완전히 신뢰할 수 있는 코드 에서만 사용할 수 있습니다.

에서 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 부분적으로 신뢰할 수 있는 호출자를 허용 하는 주요 시나리오 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 는 웹 응용 프로그램에서 어셈블리에 액세스할 수 있도록 설정 하는 것입니다. 여기서 *트러스트* 구성은 Medium입니다.

## <a name="mapping-data-from-multiple-tables"></a>여러 테이블의 데이터 매핑

질문. 사용하는 엔터티의 데이터를 여러 테이블에서 가져오는데 이러한 데이터를 어떻게 매핑합니까?

1\. 데이터베이스에 뷰를 만들어 엔터티를 해당 뷰에 매핑할 수 있습니다. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 테이블과 마찬가지로 뷰에 대해서도 동일한 SQL을 생성합니다.

> [!NOTE]
> 그러나 이 시나리오에서는 뷰 사용이 제한됩니다. 이 방법은 기본 뷰에서 <xref:System.Data.Linq.Table%601>에 대해 수행되는 작업을 지원하는 경우에 가장 안전하게 사용할 수 있습니다. 수행하려는 작업은 사용자 자신만이 알고 있습니다. 예를 들어 대부분의 응용 프로그램은 읽기 전용 이며 다른 큰 숫자는 `Create` 뷰에 대해 저장 프로시저만 사용 하 여 작업을 수행 / / `Update` `Delete` 합니다.

## <a name="connection-pooling"></a>연결 풀링

질문. <xref:System.Data.Linq.DataContext> 풀링에 도움이 되는 생성자가 있습니까?

1\. <xref:System.Data.Linq.DataContext>의 인스턴스는 다시 사용하지 마세요. 각 <xref:System.Data.Linq.DataContext>는 하나의 특정 편집/쿼리 세션에 대한 상태(ID 캐시 포함)를 유지합니다. 데이터베이스의 현재 상태를 기반으로 새 인스턴스를 사용하려면 새 <xref:System.Data.Linq.DataContext>를 사용하세요.

여전히 기본 ADO.NET 연결 풀링을 사용할 수 있습니다. 자세한 내용은 [SQL Server 연결 풀링(ADO.NET)](../../sql-server-connection-pooling.md)을 참조하세요.

## <a name="second-datacontext-is-not-updated"></a>두 번째 DataContext가 업데이트되지 않음

질문. <xref:System.Data.Linq.DataContext>의 인스턴스 하나를 사용하여 데이터베이스에 값을 저장했습니다. 그런데 동일한 데이터베이스에 대한 두 번째 <xref:System.Data.Linq.DataContext>에 업데이트된 값이 반영되지 않습니다. 두 번째 <xref:System.Data.Linq.DataContext> 인스턴스가 캐시된 값을 반환하는 것 같습니다.

1\. 이 동작은 설계 시 의도된 것입니다. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]은 첫 번째 인스턴스와 동일한 인스턴스/값을 계속해서 반환합니다. 데이터를 업데이트할 경우에는 낙관적 동시성을 사용합니다. 이 경우 현재 데이터베이스 상태를 원래 데이터와 비교하여 데이터가 변경되지 않았는지 확인합니다. 데이터가 변경된 경우 충돌이 발생하고 애플리케이션에서는 이 문제를 해결해야 합니다. 애플리케이션에서는 한 가지 옵션으로 원래 상태를 현재 데이터베이스 상태로 다시 설정한 후 업데이트를 다시 시도합니다. 자세한 내용은 [방법: 변경 충돌](how-to-manage-change-conflicts.md)을 관리 합니다.

<xref:System.Data.Linq.DataContext.ObjectTrackingEnabled%2A>를 false로 설정하여 캐싱 및 변경 추적을 해제할 수도 있습니다. 이렇게 하면 쿼리할 때마다 최신 값을 검색할 수 있습니다.

## <a name="cannot-call-submitchanges-in-read-only-mode"></a>읽기 전용 모드에서 SubmitChanges를 호출할 수 없음

질문. 읽기 전용 모드에서 <xref:System.Data.Linq.DataContext.SubmitChanges%2A>를 호출하려고 하면 오류가 발생합니다.

1\. 읽기 전용 모드에서는 컨텍스트에서 변경 내용을 추적하지 않습니다.

## <a name="see-also"></a>참고자료

- [참조](reference.md)
- [문제 해결](troubleshooting.md)
- [LINQ to SQL의 보안](security-in-linq-to-sql.md)
