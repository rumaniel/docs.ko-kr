---
title: 왼쪽 외부 조인 수행(C#의 LINQ)
description: C#에서 LINQ를 사용하여 왼쪽 외부 조인을 수행하는 방법을 알아봅니다.
ms.date: 12/01/2016
ms.assetid: f542cee6-3169-4dcf-a631-3a6a79ccd473
ms.openlocfilehash: cc08a1c8670623a10d1e0bf10221d02037a8d7bc
ms.sourcegitcommit: 5dcfeb59179e81071f54840d4902cbe00b184294
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54857582"
---
# <a name="perform-left-outer-joins"></a>왼쪽 우선 외부 조인 수행

왼쪽 우선 외부 조인은 두 번째 컬렉션에 상호 연결된 요소가 있는지 여부에 관계없이 첫 번째 컬렉션의 각 요소가 반환되는 조인입니다. LINQ를 통해 그룹 조인의 결과에서 <xref:System.Linq.Enumerable.DefaultIfEmpty%2A> 메서드를 호출하여 왼쪽 우선 외부 조인을 수행할 수 있습니다.

## <a name="example"></a>예제

다음 예제에서는 그룹 조인의 결과에서 <xref:System.Linq.Enumerable.DefaultIfEmpty%2A> 메서드를 사용하여 왼쪽 우선 외부 조인을 수행하는 방법을 보여 줍니다.

두 컬렉션의 왼쪽 우선 외부 조인을 생성하는 첫 번째 단계는 그룹 조인을 사용하여 내부 조인을 수행하는 것입니다. 이 프로세스에 대한 설명은 [내부 조인 수행](perform-inner-joins.md)을 참조하세요. 이 예제에서 `Person` 개체 목록은 `Pet.Owner`와 일치하는 `Person` 개체를 기준으로 `Pet` 개체 목록에 내부 조인됩니다.

두 번째 단계는 오른쪽 컬렉션에 일치하는 항목이 없는 경우에도 첫 번째(왼쪽) 컬렉션의 각 요소를 결과 집합에 포함하는 것입니다. 이렇게 하려면 그룹 조인에서 일치하는 요소의 각 시퀀스에 대해 <xref:System.Linq.Enumerable.DefaultIfEmpty%2A>를 호출합니다. 이 예제에서는 일치하는 `Pet` 개체의 각 시퀀스에서 <xref:System.Linq.Enumerable.DefaultIfEmpty%2A>를 호출합니다. 메서드는 `Person` 개체에 대해 일치하는 `Pet` 개체의 시퀀스가 비어 있는 경우 단일 기본값을 포함하는 컬렉션을 반환하여 각 `Person` 개체가 결과 컬렉션에 반환되도록 합니다.

> [!NOTE]
> 참조 형식의 기본값은 `null`이므로 예제에서는 각 `Pet` 컬렉션의 각 요소에 액세스하기 전에 null 참조를 확인합니다.

[!code-csharp[CsLINQProgJoining#7](~/samples/snippets/csharp/concepts/linq/how-to-perform-left-outer-joins_1.cs)]

## <a name="see-also"></a>참고 항목

- <xref:System.Linq.Enumerable.Join%2A>
- <xref:System.Linq.Enumerable.GroupJoin%2A>
- [내부 조인 수행](perform-inner-joins.md)
- [그룹화 조인 수행](perform-grouped-joins.md)
- [무명 형식](../programming-guide/classes-and-structs/anonymous-types.md)
