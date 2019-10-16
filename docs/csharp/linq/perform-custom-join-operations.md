---
title: 사용자 지정 조인 작업 수행(C#의 LINQ)
description: C#에서 사용자 지정 LINQ 조인 작업을 수행하는 방법에 대해 알아봅니다.
ms.date: 12/01/2016
ms.assetid: 56a2a4a5-7299-497d-b3c3-23c848678911
ms.openlocfilehash: 7051007c67bd64cd11ede2f4d5352ce3d497255f
ms.sourcegitcommit: 5dcfeb59179e81071f54840d4902cbe00b184294
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54857868"
---
# <a name="perform-custom-join-operations"></a>사용자 지정 조인 작업 수행

이 예제에서는 `join` 절에 사용할 수 없는 조인 작업을 수행하는 방법을 보여 줍니다. 쿼리 식에서 `join` 절은 조인 작업의 가장 일반적인 형식인 동등 조인으로 제한되고 최적화되었습니다. 동등 조인을 수행하는 경우 `join` 절을 사용하면 항상 최상의 성능을 얻을 수 있습니다.

그러나 `join` 절은 다음과 같은 경우에 사용할 수 없습니다.

- 조인이 같지 않음(비동등 조인)의 식에서 서술된 경우

- 조인이 둘 이상의 같음 또는 같지 않음에서 서술된 경우

- 조인 작업 앞에서 오른쪽(내부) 시퀀스에 대한 임시 범위 변수를 도입해야 하는 경우

 조인 동등이 아닌 조인을 수행하려면 여러 개의 `from` 절을 사용하여 각 데이터 소스를 독립적으로 도입할 수 있습니다. 그런 다음 `where` 절의 조건자 식을 각 소스에 대한 범위 변수에 적용합니다. 식은 메서드 호출의 형식을 사용할 수도 있습니다.

> [!NOTE]
> 여러 `from` 절을 사용하여 내부 컬렉션에 액세스하는 경우와 이러한 종류의 사용자 지정 조인 작업을 혼동하지 마세요. 자세한 내용은 [join 절](../language-reference/keywords/join-clause.md)을 참조하세요.

## <a name="example"></a>예제

다음 예제의 첫 번째 메서드는 간단한 크로스 조인을 보여 줍니다. 크로스 조인은 매우 큰 결과 집합을 생성할 수 있으므로 주의해서 사용해야 합니다. 그러나 추가 쿼리가 실행되는 소스 시퀀스를 만들기 위해 일부 시나리오에서 사용할 수 있습니다.

두 번째 메서드는 범주 ID가 왼쪽의 범주 목록에 나열된 모든 제품의 시퀀스를 생성합니다. `let` 절과 `Contains` 메서드를 사용하여 임시 배열을 만듭니다. 또한 쿼리 앞에서 배열을 만들고 첫 번째 `from` 절을 제거할 수도 있습니다.

[!code-csharp[csProgGuideLINQ#64](~/samples/snippets/csharp/concepts/linq/how-to-perform-custom-join-operations_1.cs)]

## <a name="example"></a>예제

다음 예제에서는 쿼리가 내부(오른쪽) 시퀀스의 경우 조인 절 앞에서 가져올 수 없는 일치 키에 따라 두 시퀀스를 조인해야 합니다. `join` 절을 사용하여 이 조인을 수행하는 경우 각 요소에 대해 `Split` 메서드를 호출해야 합니다. 여러 개의 `from` 절을 사용하면 쿼리에서 반복된 메서드 호출의 오버헤드를 방지할 수 있습니다. 그러나 `join`이 최적화되었으므로 이 특정 사례에서는 여러 개의 `from` 절을 사용하는 것보다 더 빠를 수 있습니다. 결과는 주로 메서드 호출이 얼마나 광범위한지에 따라 달라집니다.

[!code-csharp[csProgGuideLINQ#13](~/samples/snippets/csharp/concepts/linq/how-to-perform-custom-join-operations_2.cs)]

## <a name="see-also"></a>참고 항목

- [LINQ(Language-Integrated Query)](index.md)
- [join 절](../language-reference/keywords/join-clause.md)
- [Join 절 결과를 서순대로 정렬](order-the-results-of-a-join-clause.md)
