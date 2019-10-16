---
title: 개체 상태 및 변경 내용 추적
ms.date: 03/30/2017
ms.assetid: 7a808b00-9c3c-479a-aa94-717280fefd71
ms.openlocfilehash: a9df200f4d2e5f64bf5883c7bc513ba7129dcaad
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781280"
---
# <a name="object-states-and-change-tracking"></a>개체 상태 및 변경 내용 추적

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]개체는 항상 특정 *상태*에 참여 합니다. 예를 들어, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서 새 개체를 만들 경우 개체는 `Unchanged` 상태입니다. 직접 만든 새 개체는 <xref:System.Data.Linq.DataContext>에 알려져 있지 않으며 `Untracked` 상태입니다. <xref:System.Data.Linq.DataContext.SubmitChanges%2A>를 실행하고 나면 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에 알려진 모든 개체는 `Unchanged` 상태가 됩니다. 유일한 예외는 데이터베이스에서 삭제된 개체로 이러한 개체는 `Deleted` 상태이고 해당 <xref:System.Data.Linq.DataContext> 인스턴스에서 사용할 수 없습니다.

## <a name="object-states"></a>개체 상태

다음 표에서는 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 개체의 가능한 상태를 보여 줍니다.

|State|Description|
|-----------|-----------------|
|`Untracked`|[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에 의해 추적되지 않는 개체입니다. 여기에는 다음과 같은 예가 포함됩니다.<br /><br /> -새로 만든 개체와 같이 현재 <xref:System.Data.Linq.DataContext> 을 통해 쿼리하지 않는 개체입니다.<br />-Deserialization을 통해 만든 개체<br />-다른 <xref:System.Data.Linq.DataContext>를 통해 쿼리 되는 개체입니다.|
|`Unchanged`|현재 <xref:System.Data.Linq.DataContext>를 사용하여 검색되었으며 만들어진 이후 수정된 것으로 알려지지 않은 개체입니다.|
|`PossiblyModified`|에 *연결* <xref:System.Data.Linq.DataContext>된 개체입니다. 자세한 내용은 [데이터 검색 및 CUD 작업에서 N 계층 애플리케이션 (LINQ to SQL)](data-retrieval-and-cud-operations-in-n-tier-applications.md)합니다.|
|`ToBeInserted`|현재 <xref:System.Data.Linq.DataContext>를 사용하여 검색되지 않은 개체입니다. 이로 인해 `INSERT` 동안 데이터베이스에 <xref:System.Data.Linq.DataContext.SubmitChanges%2A>가 발생합니다.|
|`ToBeUpdated`|검색된 이후로 수정되었다는 것이 알려진 개체입니다. 이로 인해 `UPDATE` 동안 데이터베이스에 <xref:System.Data.Linq.DataContext.SubmitChanges%2A>가 발생합니다.|
|`ToBeDeleted`|삭제되도록 표시된 개체이며 이로 인해 `DELETE` 동안 데이터베이스에 <xref:System.Data.Linq.DataContext.SubmitChanges%2A>가 발생합니다.|
|`Deleted`|데이터베이스에서 삭제된 개체입니다. 이 상태는 최종 상태이며 더 이상의 전환은 허용되지 않습니다.|

## <a name="inserting-objects"></a>개체 삽입

`Inserts`을 사용하여 <xref:System.Data.Linq.Table%601.InsertOnSubmit%2A>를 명시적으로 요청할 수 있습니다. 또는 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서는 업데이트해야 하는 알려진 개체 중 하나에 연결된 개체를 찾아 `Inserts`를 유추할 수 있습니다. 예를 들어 `Untracked` 개체를 <xref:System.Data.Linq.EntitySet%601>에 추가하거나 <xref:System.Data.Linq.EntityRef%601>을 `Untracked` 개체로 설정할 경우 그래프에서 추적된 개체를 통해 `Untracked` 개체에 연결할 수 있습니다. <xref:System.Data.Linq.DataContext.SubmitChanges%2A>를 처리하는 동안 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]은 추적된 개체를 순회하면서 추적되지 않는 도달 가능한 모든 영구 개체를 검색합니다. 이러한 개체는 데이터베이스에 삽입할 후보입니다.

상속 계층 구조에 있는 클래스의 <xref:System.Data.Linq.Table%601.InsertOnSubmit%2A>경우`o`()도 개체 `o`형식과 일치 하도록 *판별자* 로 지정 된 멤버의 값을 설정 합니다. 기본 판별자 값과 일치하는 형식의 경우 이 작업이 수행되면 판별자 값을 기본값이 덮어씁니다. 자세한 내용은 [상속 지원](inheritance-support.md)을 참조 하세요.

> [!IMPORTANT]
> `Table`에 추가된 개체는 ID 캐시에 없습니다. ID 캐시는 데이터베이스에서 검색된 개체만 반영합니다. <xref:System.Data.Linq.Table%601.InsertOnSubmit%2A> 호출 이후 <xref:System.Data.Linq.DataContext.SubmitChanges%2A>가 완료될 때까지 추가된 엔터티는 데이터베이스에 대한 쿼리에 표시되지 않습니다.

## <a name="deleting-objects"></a>개체 삭제

적절한 `o`에서 <xref:System.Data.Linq.Table%601.DeleteOnSubmit%2A>(o)을 호출하여 추적된 개체 <xref:System.Data.Linq.Table%601>를 삭제 대상으로 표시합니다. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]은 <xref:System.Data.Linq.EntitySet%601>에서 개체를 제거하는 것을 업데이트 작업으로 간주하며 해당 외래 키 값이 null로 설정됩니다. 작업의 대상(`o`)은 해당 테이블에서 삭제되지 않습니다. 예를 들어, `cust.Orders.DeleteOnSubmit(ord)`는 외래 키 `cust`를 null로 설정하여 `ord` 및 `ord.CustomerID` 간의 관계를 끊는 업데이트를 나타냅니다. 이로 인해 `ord`에 해당하는 행이 삭제되지는 않습니다.

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]은 개체가 해당 테이블에서 삭제될 때(<xref:System.Data.Linq.Table%601.DeleteOnSubmit%2A>) 다음 작업을 처리합니다.

- <xref:System.Data.Linq.DataContext.SubmitChanges%2A>가 호출될 경우 `DELETE` 작업이 해당 개체에 대해 수행됩니다.

- 관련 개체가 로드되었는지 여부에 상관없이 제거는 관련 개체에 전파되지 않습니다. 특히 관계 속성을 업데이트하기 위해 관련 개체가 로드되지는 않습니다.

- <xref:System.Data.Linq.DataContext.SubmitChanges%2A>가 실행된 후 개체는 `Deleted` 상태로 설정됩니다. 결과적으로 해당 `id`에서 개체나 개체의 <xref:System.Data.Linq.DataContext>를 사용할 수 없습니다. <xref:System.Data.Linq.DataContext> 인스턴스에 의해 유지 관리되는 내부 캐시는 개체가 데이터베이스에서 삭제된 이후에도 검색되거나 새로 추가되는 개체를 제거하지 않습니다.

<xref:System.Data.Linq.Table%601.DeleteOnSubmit%2A>에 의해 추적되는 개체에서만 <xref:System.Data.Linq.DataContext>을 호출할 수 있습니다. `Untracked` 개체의 경우 <xref:System.Data.Linq.Table%601.Attach%2A>을 호출하기 전에 <xref:System.Data.Linq.Table%601.DeleteOnSubmit%2A>를 호출해야 합니다. <xref:System.Data.Linq.Table%601.DeleteOnSubmit%2A> 개체에서 `Untracked`를 호출하면 예외가 throw됩니다.

> [!NOTE]
> 테이블에서 개체를 제거하면 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]은 `DELETE` 시점에 해당 SQL <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 명령을 생성합니다. 이 작업으로 인해 캐시에서 개체가 제거되거나 관련된 개체에 삭제가 전파되지는 않습니다.
>
> 삭제된 개체의 `id`를 회수하려면 새 <xref:System.Data.Linq.DataContext> 인스턴스를 사용합니다. 관련 개체를 정리 하기 위해 데이터베이스의 *cascade delete* 기능을 사용 하거나 관련 개체를 수동으로 삭제할 수 있습니다.
>
> 데이터베이스에서와 달리 관련 개체를 특정 순서로 삭제할 필요가 없습니다.

## <a name="updating-objects"></a>개체 업데이트

변경 내용에 대한 알림을 확인하여 `Updates`를 감지할 수 있습니다. 알림은 속성 setter의 <xref:System.ComponentModel.INotifyPropertyChanging.PropertyChanging> 이벤트를 통해 제공됩니다. 개체에 대한 첫 번째 변경 내용이 알려질 경우 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]은 개체의 복사본을 만들고 `Update` 문 생성을 위한 후보로 개체를 고려합니다.

<xref:System.ComponentModel.INotifyPropertyChanging>을 구현하지 않는 개체의 경우 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]은 개체가 처음 구체화될 때 갖고 있던 값의 복사본을 유지 관리합니다. <xref:System.Data.Linq.DataContext.SubmitChanges%2A>가 호출되면 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]은 현재 값과 원래 값을 비교하여 개체가 변경되었는지 여부를 확인합니다.

관계 업데이트의 경우 자식에서 부모로의 참조(즉, 외래 키에 해당하는 참조)가 우선권을 가집니다. 반대 방향의 참조(즉, 부모에서 자식으로의 참조)는 선택 사항입니다. 관계 클래스(<xref:System.Data.Linq.EntitySet%601> 및 <xref:System.Data.Linq.EntityRef%601>)는 일대다 및 일대일 관계에서 양방향 참조가 일관되도록 보장합니다. 개체 모델에 <xref:System.Data.Linq.EntitySet%601> 또는 <xref:System.Data.Linq.EntityRef%601>가 사용되지 않는 상태에서 역방향 참조가 존재할 경우 관계 업데이트 시에 역방향 참조와 정방향 참조의 일관성을 유지하는 작업을 직접 수행해야 합니다.

필수 참조와 해당 외래 키를 둘 다 업데이트할 경우 서로 일치하는지 확인해야 합니다. <xref:System.InvalidOperationException>를 호출할 때 두 항목이 동기화되지 않은 경우 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 예외가 throw됩니다. 외래 키 값 변경을 통해 기본 행 업데이트에 충분히 영향을 줄 수 있지만 개체 그래프의 연결과 관계의 양방향 일관성을 유지 관리하기 위해 참조를 변경해야 합니다.

## <a name="see-also"></a>참고자료

- [배경 정보](background-information.md)
- [삽입, 업데이트 및 삭제 작업](insert-update-and-delete-operations.md)
