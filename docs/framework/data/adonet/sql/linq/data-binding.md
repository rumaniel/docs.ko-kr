---
title: 데이터 바인딩
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: cbec8b02-a1e8-4ae8-a83b-bb5190413ac5
ms.openlocfilehash: 79a14e787b4fe1aa1b16ad661b11a43b12bdd718
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70247375"
---
# <a name="data-binding"></a>데이터 바인딩

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]grid 컨트롤과 같은 공용 컨트롤에 대 한 바인딩을 지원 합니다. 특히 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 데이터 표에 바인딩과 마스터-세부 사항 바인딩 처리를 위한 기본 패턴을 표시 및 업데이트 측면 모두에서 정의합니다.

## <a name="underlying-principle"></a>기본 원칙

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)] 쿼리를 데이터베이스에서 실행하기 위해 SQL로 변환합니다. 그 결과 강력한 형식의 `IEnumerable`이 생성됩니다. 이러한 개체는 일반 CLR (공용 언어 런타임) 개체 이므로 일반적인 개체 데이터 바인딩을 사용 하 여 결과를 표시할 수 있습니다. 반면 변경 작업(삽입, 업데이트 및 삭제)에는 추가 단계가 필요합니다.

## <a name="operation"></a>작업

Windows Forms 컨트롤에 명시적으로 바인딩하려면 <xref:System.ComponentModel.IListSource>를 구현합니다. 데이터 소스 제네릭 <xref:System.Data.Linq.Table%601> (`Table<T>` `DataQuery` <xref:System.ComponentModel.IListSource>또는 VisualBasic`Table(Of T)` ) 및 제네릭는를 구현 C# 하도록 업데이트 되었습니다. UI(사용자 인터페이스) 데이터 바인딩 엔진(Windows Forms 및 Windows Presentation Foundation)에서는 모두 해당 데이터 소스에서 <xref:System.ComponentModel.IListSource>를 구현하는지 여부를 테스트합니다. 따라서 다음 예제와 같이 쿼리의 직접 영향을 컨트롤의 데이터 소스에 쓰면 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 컬렉션 생성이 암시적으로 호출됩니다.

[!code-csharp[DLinqDataBinding#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqDataBinding/cs/Program.cs#1)]
[!code-vb[DLinqDataBinding#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqDataBinding/vb/Module1.vb#1)]

Windows Presentation Foundation에서도 동일한 동작이 발생합니다.

[!code-csharp[DLinqDataBinding#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqDataBinding/cs/Program.cs#2)]
[!code-vb[DLinqDataBinding#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqDataBinding/vb/Module1.vb#2)]

컬렉션 생성은 <xref:System.Data.Linq.Table%601>에서 제네릭 `DataQuery` 및 제네릭 <xref:System.ComponentModel.IListSource.GetList%2A>에 의해 구현됩니다.

## <a name="ilistsource-implementation"></a>IListSource 구현

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 다음과 같은 두 위치에서 <xref:System.ComponentModel.IListSource>를 구현합니다.

- 데이터 소스가 <xref:System.Data.Linq.Table%601>인 경우 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 테이블을 탐색하여 테이블의 참조를 보관하는 `DataBindingList` 컬렉션을 채웁니다.

- 데이터 소스가 <xref:System.Linq.IQueryable%601>인 경우 다음과 같은 두 가지 시나리오가 있습니다.

  - [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]가 <xref:System.Data.Linq.Table%601>에서 기본 <xref:System.Linq.IQueryable%601>을 찾는 경우 소스를 편집할 수 있으며 첫 번째 글머리 기호의 경우와 상황이 같아집니다.

  - 에서 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 기본 <xref:System.Data.Linq.Table%601>을 찾을 수 없는 경우 소스에서 `groupby`버전을 허용 하지 않습니다 (예:). [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]지정 된 속성의 T 엔터티에 대 `SortableBindingList`한 정렬 기능을 구현 <xref:System.ComponentModel.BindingList%601> 하는 단순 인 제네릭를 채우도록 쿼리를 탐색 합니다.

## <a name="specialized-collections"></a>특수 컬렉션

이 문서의 앞부분에서 설명한 많은 기능에서 <xref:System.ComponentModel.BindingList%601>는 몇 가지 다른 클래스용으로 설계된 특수 클래스입니다. 이러한 클래스는 제네릭 `SortableBindingList` 및 제네릭 `DataBindingList` 클래스입니다. 둘 다 정수로 선언됩니다.

### <a name="generic-sortablebindinglist"></a>제네릭 SortableBindingList

이 클래스는 <xref:System.ComponentModel.BindingList%601>에서 상속되며 <xref:System.ComponentModel.BindingList%601>의 정렬 가능한 버전입니다. 정렬은 메모리 내 솔루션이며 데이터베이스 자체와는 연결하지 않습니다. <xref:System.ComponentModel.BindingList%601>는 <xref:System.ComponentModel.IBindingList>를 구현하지만 기본적으로 정렬을 지원하지 않습니다. 그러나는 <xref:System.ComponentModel.BindingList%601> 가상 <xref:System.ComponentModel.IBindingList> *핵심* 메서드를 사용 하 여를 구현 합니다. 이러한 메서드는 쉽게 재정의할 수 있습니다. 제네릭 `SortableBindingList`는 <xref:System.ComponentModel.BindingList%601.SupportsSortingCore%2A>, <xref:System.ComponentModel.BindingList%601.SortPropertyCore%2A>, <xref:System.ComponentModel.BindingList%601.SortDirectionCore%2A> 및 <xref:System.ComponentModel.BindingList%601.ApplySortCore%2A>를 재정의합니다. `ApplySortCore`는 <xref:System.ComponentModel.IBindingList.ApplySort%2A>에서 호출되며 지정한 속성의 T 항목 목록을 정렬합니다.

속성이 T에 속하지 않으면 예외가 발생합니다.

정렬을 수행하기 위해 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 제네릭 `SortableBindingList.PropertyComparer`에서 상속되는 제네릭 <xref:System.Collections.Generic.Comparer%601.System%23Collections%23IComparer%23Compare%2A> 클래스를 만들고 지정된 형식 T에 대한 기본 비교자인 `PropertyDescriptor`와 방향을 구현합니다. 이 클래스는 T가 `Comparer`의 `PropertyType`인 경우 T의 `PropertyDescriptor`를 동적으로 만듭니다. 그런 다음 정적 제네릭 `Comparer`에서 기본 비교자를 검색합니다. 기본 인스턴스는 리플렉션을 사용하여 가져옵니다.

제네릭 `SortableBindingList`도 `DataBindingList`의 기본 클래스입니다. 제네릭 `SortableBindingList`에서는 항목 추가/제거 추적을 일시 중단 또는 다시 시작하기 위한 두 개의 가상 메서드를 제공합니다. 이러한 두 메서드는 정렬과 같은 기본 기능에 사용할 수 있지만 실제로 제네릭 `DataBindingList`와 같은 상위 클래스에서 구현됩니다.

### <a name="generic-databindinglist"></a>제네릭 DataBindingList

이 클래스는 제네릭 `SortableBindingLIst`에서 상속됩니다. 제네릭 `DataBindingList`는 컬렉션의 초기 채우기에 사용되는 제네릭 `Table`에 대한 기본 제네릭 `IQueryable`의 참조를 보관합니다. 제네릭 `DatabindingList`는 `InsertItem`() 및 `RemoveItem`()를 재정의하여 항목 추가/제거에 대한 추적을 컬렉션에 추가합니다. 또한 추적 기능의 추상 일시 중단/다시 시작을 구현하여 추적을 조건부로 만듭니다. 이 기능을 사용하면 제네릭 `DataBindingList`에서 부모 클래스의 추적 기능에 대한 모든 다형적 사용을 활용할 수 있습니다.

## <a name="binding-to-entitysets"></a>EntitySet에 바인딩

`EntitySet`은 이미 `EntitySet`를 구현하는 컬렉션이므로 <xref:System.ComponentModel.IBindingList>에 바인딩하는 것은 특수한 경우입니다. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 정렬 및 취소(<xref:System.ComponentModel.ICancelAddNew>) 지원을 추가합니다. `EntitySet` 클래스는 내부 목록을 사용하여 엔터티를 저장합니다. 이 목록은 제네릭 배열을 기반으로 하는 하위 수준 컬렉션인 제네릭 `ItemList` 클래스입니다.

### <a name="adding-a-sorting-feature"></a>정렬 기능 추가

배열에서는 T의 `Array.Sort()`와 함께 사용할 수 있는 정렬 메서드(`Comparer`)를 제공합니다. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 이 항목의 앞부분에서 설명한 제네릭 `SortableBindingList.PropertyComparer` 클래스를 사용하여 이 `Comparer`에서 정렬할 속성과 방향을 가져옵니다. `ApplySort` 메서드를 제네릭 `ItemList`에 추가하면 이 기능이 호출됩니다.

이제 다음과 같이 `EntitySet`측에서 정렬 지원을 선언해야 합니다.

- <xref:System.ComponentModel.IBindingList.SupportsSorting%2A>가 `true`를 반환하는 경우

- <xref:System.ComponentModel.IBindingList.ApplySort%2A>에서 `entities.ApplySort()`와 `OnListChanged()`를 차례로 호출합니다.

- <xref:System.ComponentModel.IBindingList.SortDirection%2A> 및 <xref:System.ComponentModel.IBindingList.SortProperty%2A> 속성은 로컬 멤버에 저장된 현재 정렬 정의를 노출합니다.

System.object를 사용 하 여 > entityset\<를 사용 하는 경우에는 entityset를 사용 하는 경우 > entityset\<를 호출 해야 합니다. GetNewBindingList를 업데이트 합니다.

System.object를 사용 하 고 bindingsource. datamember 속성을 설정 하 고 bindingsource. DataSource를이 속성을 사용 하는 클래스에 설정 하는 경우에는 EntitySet\<를 > 합니다. EntitySet\<>를 호출할 필요가 없습니다. GetNewBindingList를 업데이트 하면 정렬 기능이 손실 됩니다.

## <a name="caching"></a>캐싱

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 쿼리에서는 <xref:System.ComponentModel.IListSource.GetList%2A>를 구현합니다. Windows Forms BindingSource 클래스는 이 인터페이스를 검색하는 경우 단일 연결에 대해 GetList()를 세 번 호출합니다. 이 문제를 해결하기 위해 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 저장한 인스턴스당 캐시 하나를 구현하고 항상 동일하게 생성된 컬렉션을 반환합니다.

## <a name="cancellation"></a>취소

<xref:System.ComponentModel.IBindingList>에서는 컨트롤이 바인딩된 컬렉션에서 새 항목을 만드는 데 사용하는 <xref:System.ComponentModel.IBindingList.AddNew%2A> 메서드를 정의합니다. `DataGridView` 컨트롤은 표시된 마지막 행의 헤더에 별이 들어 있는 경우 이 기능을 아주 잘 보여 줍니다. 별은 새 항목을 추가할 수 있다는 것을 나타냅니다.

또한 컬렉션에서는 이 기능 외에 <xref:System.ComponentModel.ICancelAddNew>를 구현합니다. 이 기능을 사용하면 컨트롤에서 새로 편집한 항목을 취소하거나 항목이 유효한지 검사할 수 있습니다.

<xref:System.ComponentModel.ICancelAddNew>는 모든 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 데이터 바인딩 컬렉션(제네릭 `SortableBindingList` 및 제네릭 `EntitySet`)에서 구현됩니다. 두 구현 모두에서 코드는 다음과 같이 수행됩니다.

- 컬렉션에서 항목이 삽입된 다음 제거됩니다.

- UI에서 편집을 커밋하지 않는 한 변경 내용을 추적하지 않습니다.

- 편집을 취소(<xref:System.ComponentModel.ICancelAddNew.CancelNew%2A>)하지 않는 한 변경 내용을 추적하지 않습니다.

- 편집이 커밋되면(<xref:System.ComponentModel.ICancelAddNew.EndNew%2A>) 추적을 허용합니다.

- 새 항목을 <xref:System.ComponentModel.IBindingList.AddNew%2A>에서 가져오지 않은 경우 컬렉션이 정상적으로 동작할 수 있습니다.

## <a name="troubleshooting"></a>문제 해결

이 단원에서는 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 데이터 바인딩 응용 프로그램의 문제를 해결하는 데 도움이 되는 몇 가지 항목을 설명합니다.

- 속성을 사용해야 합니다. 필드만 사용하는 것으로는 충분하지 않습니다. Windows Forms에는 이러한 사용법이 필요합니다.

- 기본적 `image` `timestamp` 으로, 및 데이터베이스 형식은 바이트 배열에 매핑됩니다. `varbinary` `ToString()`은 이 시나리오에서 지원되지 않으므로 이러한 개체를 표시할 수 없습니다.

- 기본 키에 매핑된 클래스 멤버에는 setter가 있지만 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 개체 ID 변경이 지원되지 않습니다. 따라서 매핑에서 사용된 기본/고유 키는 데이터베이스에서 업데이트할 수 없습니다. 표를 변경하면 <xref:System.Data.Linq.DataContext.SubmitChanges%2A>를 호출할 때 예외가 발생합니다.

- 엔터티가 두 개의 다른 표(예: 마스터와 세부 사항)에 바인딩되어 있으면 마스터 표의 `Delete`가 세부 사항 표로 전파되지 않습니다.

## <a name="see-also"></a>참고자료

- [배경 정보](background-information.md)
