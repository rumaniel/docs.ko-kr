---
title: join 절 - C# 참조
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- join
- join_CSharpKeyword
helpviewer_keywords:
- join clause [C#]
- join keyword [C#]
ms.assetid: 76e9df84-092c-41a6-9537-c3f1cbd7f0fb
ms.openlocfilehash: 21d4d1f9878fb7df4692fdeacd23b042680c14f1
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65633617"
---
# <a name="join-clause-c-reference"></a>join 절(C# 참조)

`join` 절은 개체 모델에서 직접적인 관계가 없는 서로 다른 소스 시퀀스의 요소를 연결하는 데 유용합니다. 각 소스의 요소가 같은지 비교할 수 있는 일부 값을 공유하기만 하면 됩니다. 예를 들어 식품 유통업체에는 특정 제품의 공급업체 목록과 구매자 목록이 있을 수 있습니다. 예를 들어 `join` 절은 모두 동일한 지역에 있는, 해당 제품의 공급업체 및 구매자 목록을 만드는 데 사용할 수 있습니다.

`join` 절은 두 개의 소스 시퀀스를 입력으로 사용합니다. 각 시퀀스의 요소는 다른 시퀀스의 속성과 비교할 수 있는 속성이거나 해당 속성을 포함해야 합니다. `join` 절은 특수한 `equals` 키워드를 사용하여 지정된 키가 같은지 비교합니다. `join` 절로 수행된 모든 조인은 동등 조인입니다. `join` 절의 출력 형태는 수행하는 조인의 특정 유형에 따라 달라집니다. 다음은 세 가지 가장 일반적인 조인 유형입니다.

- 내부 조인

- 그룹 조인

- 왼쪽 우선 외부 조인

## <a name="inner-join"></a>내부 조인

다음 예제에서는 간단한 내부 동등 조인을 보여 줍니다. 이 쿼리는 "제품 이름/범주" 쌍의 기본 시퀀스를 생성합니다. 동일한 범주 문자열이 여러 요소에 나타납니다. `categories`의 요소에 일치하는 `products`가 없는 경우 해당 범주는 결과에 나타나지 않습니다.

[!code-csharp[cscsrefQueryKeywords#24](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Join.cs#24)]

자세한 내용은 [내부 조인 수행](../../linq/perform-inner-joins.md)을 참조하세요.

## <a name="group-join"></a>그룹 조인

`into` 식을 포함한 `join` 절을 그룹 조인이라고 합니다.

[!code-csharp[cscsrefQueryKeywords#25](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Join.cs#25)]

그룹 조인은 왼쪽 소스 시퀀스의 요소를 오른쪽 소스 시퀀스에서 일치하는 하나 이상의 요소와 연결하는 계층적 결과 시퀀스를 생성합니다. 관계적인 측면에서 그룹 조인에는 해당 항목이 없으며, 그룹 조인은 기본적으로 개체 배열의 시퀀스입니다.

왼쪽 소스의 요소와 일치하는 오른쪽 소스 시퀀스의 요소가 없을 경우 `join` 절은 해당 항목에 대해 빈 배열을 생성합니다. 따라서 결과 시퀀스가 그룹으로 구성된다는 점을 제외하면 그룹 조인은 기본적으로 내부 동등 조인입니다.

그룹 조인의 결과를 선택하는 경우 항목에 액세스할 수 있지만 항목이 일치되는 키를 식별할 수는 없습니다. 따라서 이전 예제와 같이 키 이름도 포함하는 새로운 유형으로 그룹 조인의 결과를 선택하는 것이 일반적으로 더 유용합니다.

또한 그룹 조인의 결과를 또 다른 하위 쿼리의 생성기로 사용할 수도 있습니다.

[!code-csharp[cscsrefQueryKeywords#26](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Join.cs#26)]

자세한 내용은 [그룹화 조인 수행](../../linq/perform-grouped-joins.md)을 참조하세요.

## <a name="left-outer-join"></a>왼쪽 우선 외부 조인

왼쪽 우선 외부 조인에서는 오른쪽 시퀀스에 일치하는 요소가 없는 경우에도 왼쪽 소스 시퀀스의 모든 요소가 반환됩니다. [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)]에서 왼쪽 우선 외부 조인을 수행하려면 그룹 조인과 함께 `DefaultIfEmpty` 메서드를 사용하여 왼쪽 요소에 일치하는 요소가 없을 경우 생성할 기본 오른쪽 요소를 지정합니다. `null`을 모든 참조 형식의 기본값으로 사용하거나 사용자 정의 기본 형식을 지정할 수 있습니다. 다음 예제에서는 사용자 정의 기본 형식을 보여 줍니다.

[!code-csharp[cscsrefQueryKeywords#27](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Join.cs#27)]

자세한 내용은 [왼쪽 우선 외부 조인 수행](../../linq/perform-left-outer-joins.md)을 참조하세요.

## <a name="the-equals-operator"></a>같음 연산자

`join` 절은 동등 조인을 수행합니다. 즉, 일치 항목만을 기준으로 두 키가 같은지 비교할 수 있습니다. "보다 큼"이나 "같지 않음"과 같은 다른 유형의 비교는 지원되지 않습니다. 모든 조인이 동등 조인인지 확인하기 위해 `join` 절은 `==` 연산자 대신 `equals` 키워드를 사용합니다. `equals` 키워드는 `join` 절에서만 사용할 수 있으며 한 가지 중요한 측면에서 `==` 연산자와 다릅니다. `equals`를 사용할 경우 왼쪽 키는 외부 소스 시퀀스를 사용하고 오른쪽 키는 내부 소스를 사용합니다. 외부 소스는 `equals`의 왼쪽 범위에만 있고 내부 소스 시퀀스는 오른쪽 범위에만 있습니다.

## <a name="non-equijoins"></a>비동등 조인

여러 개의 `from` 절을 사용하여 비동등 조인, 크로스 조인 및 기타 사용자 지정 조인 작업을 수행하면 새 시퀀스를 독립적으로 쿼리에 지정할 수 있습니다. 자세한 내용은 [사용자 지정 조인 작업 수행](../../linq/perform-custom-join-operations.md)을 참조하세요.

## <a name="joins-on-object-collections-vs-relational-tables"></a>개체 컬렉션 및 관계형 테이블에서 조인

[!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리 식에서 조인 작업은 개체 컬렉션에서 수행됩니다. 개체 컬렉션은 두 개의 관계형 테이블과 정확히 동일한 방식으로 "조인"할 수 없습니다. [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)]에서는 두 소스 시퀀스가 관계로 연결되지 않는 경우에만 명시적 `join` 절이 필요합니다. [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)]로 작업할 때 외래 키 테이블은 기본 테이블의 속성으로 개체 모델에 표시됩니다. 예를 들어 Northwind 데이터베이스에서 Customer 테이블은 Orders 테이블과 외래 키 관계가 있습니다. 테이블을 개체 모델에 매핑하면 Customer 클래스는 해당 Customer와 연결된 Orders 컬렉션을 포함하는 Orders 속성을 갖습니다. 사실상 조인은 이미 수행된 것입니다.

[!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] 컨텍스트에서 관련 테이블을 쿼리하는 방법에 대한 자세한 내용은 [방법: 데이터베이스 관계 매핑](../../../framework/data/adonet/sql/linq/how-to-map-database-relationships.md)을 참조하세요.

## <a name="composite-keys"></a>복합 키

복합 키를 사용하여 여러 값이 같은지 여부를 테스트할 수 있습니다. 자세한 내용은 [복합 키를 사용하여 조인](../../linq/join-by-using-composite-keys.md)을 참조하세요. 복합 키는 `group` 절에서도 사용할 수 있습니다.

## <a name="example"></a>예제

다음 예제에서는 동일한 데이터 소스에서 동일한 일치하는 키를 사용하여 내부 조인, 그룹 조인 및 왼쪽 우선 외부 조인의 결과를 비교합니다. 콘솔 디스플레이에 결과를 명확하게 나타내기 위해 이러한 예제에 몇 가지 추가 코드를 추가합니다.

[!code-csharp[cscsrefQueryKeywords#23](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Join.cs#23)]

## <a name="remarks"></a>주의

뒤에 `into`가 오지 않는 `join` 절은 <xref:System.Linq.Enumerable.Join%2A> 메서드 호출로 변환됩니다. 뒤에 `into`가 오는 `join` 절은 <xref:System.Linq.Enumerable.GroupJoin%2A> 메서드 호출로 변환됩니다.

## <a name="see-also"></a>참고 항목

- [쿼리 키워드(LINQ)](query-keywords.md)
- [LINQ(Language-Integrated Query)](../../linq/index.md)
- [조인 작업](../../programming-guide/concepts/linq/join-operations.md)
- [group 절](group-clause.md)
- [왼쪽 우선 외부 조인 수행](../../linq/perform-left-outer-joins.md)
- [내부 조인 수행](../../linq/perform-inner-joins.md)
- [그룹화 조인 수행](../../linq/perform-grouped-joins.md)
- [Join 절 결과를 서순대로 정렬](../../linq/order-the-results-of-a-join-clause.md)
- [복합 키를 사용하여 조인](../../linq/join-by-using-composite-keys.md)
- [Visual Studio용 호환 데이터베이스 시스템](/visualstudio/data-tools/installing-database-systems-tools-and-samples)
