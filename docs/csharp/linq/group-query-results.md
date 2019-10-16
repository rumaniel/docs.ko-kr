---
title: 쿼리 결과 그룹화(C#의 LINQ)
description: C#에서 LINQ를 사용하여 결과를 그룹화하는 방법을 알아봅니다.
ms.date: 12/01/2016
ms.assetid: 2e4ec27f-06fb-4de7-8973-0189906d4520
ms.openlocfilehash: 577a358c31fcf5346e7aab7a2e2b6be10fd1beff
ms.sourcegitcommit: 5dcfeb59179e81071f54840d4902cbe00b184294
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54857855"
---
# <a name="group-query-results"></a>쿼리 결과 그룹화

그룹화는 LINQ의 가장 강력한 기능 중 하나입니다. 다음 예제에서는 다양한 방법으로 데이터를 그룹화하는 방법을 보여 줍니다.

- 단일 속성 사용.

- 문자열 속성의 첫 문자 사용.

- 계산된 숫자 범위 사용.

- 부울 조건자 또는 기타 식 사용.

- 복합 키 사용.

또한 마지막 두 개의 쿼리는 학생의 이름과 성만 포함된 새 무명 형식으로 결과를 프로젝션합니다. 자세한 내용은 [group 절](../language-reference/keywords/group-clause.md)을 참조하세요.

## <a name="example"></a>예제

이 항목의 모든 예제에는 다음 도우미 클래스 및 데이터 소스가 사용됩니다.

[!code-csharp[csProgGuideLINQ#15](~/samples/snippets/csharp/concepts/linq/how-to-group-query-results_1.cs)]

## <a name="example"></a>예제

다음 예제에서는 요소의 단일 속성을 그룹 키로 사용하여 소스 요소를 그룹화하는 방법을 보여 줍니다. 이 경우 키는 학생의 성인 `string`입니다. 키에 부분 문자열을 사용할 수도 있습니다. 그룹화 작업에는 형식에 대한 기본 같음 비교자가 사용됩니다.

`StudentClass` 클래스에 다음 메서드를 붙여넣습니다. `Main` 메서드에서 호출 문을 `sc.GroupBySingleProperty()`으로 변경합니다.

[!code-csharp[csProgGuideLINQ#17](~/samples/snippets/csharp/concepts/linq/how-to-group-query-results_2.cs)]

## <a name="example"></a>예제

다음 예제에서는 개체의 속성이 아닌 다른 항목을 그룹 키에 사용하여 소스 요소를 그룹화하는 방법을 보여 줍니다. 이 예제에서 키는 학생 성의 첫 번째 문자입니다.

`StudentClass` 클래스에 다음 메서드를 붙여넣습니다. `Main` 메서드에서 호출 문을 `sc.GroupBySubstring()`으로 변경합니다.

[!code-csharp[csProgGuideLINQ#18](~/samples/snippets/csharp/concepts/linq/how-to-group-query-results_3.cs)]

## <a name="example"></a>예제

다음 예제에서는 숫자 범위를 그룹 키로 사용하여 소스 요소를 그룹화하는 방법을 보여 줍니다. 그런 다음 쿼리는 이름과 성 및 학생이 속한 백분위수 범위만 포함된 무명 형식으로 결과를 프로젝션합니다. 결과를 표시하는 데 완전한 `Student` 개체를 사용할 필요가 없으므로 무명 형식이 사용됩니다. `GetPercentile`은 학생의 평균 점수를 기준으로 백분위수를 계산하는 도우미 함수입니다. 이 메서드는 0~10 사이의 정수를 반환합니다.

[!code-csharp[csProgGuideLINQ#50](~/samples/snippets/csharp/concepts/linq/how-to-group-query-results_4.cs)]

`StudentClass` 클래스에 다음 메서드를 붙여넣습니다. `Main` 메서드에서 호출 문을 `sc.GroupByRange()`으로 변경합니다.

[!code-csharp[csProgGuideLINQ#19](~/samples/snippets/csharp/concepts/linq/how-to-group-query-results_5.cs)]

## <a name="example"></a>예제

다음 예제에서는 부울 비교 식을 사용하여 소스 요소를 그룹화하는 방법을 보여 줍니다. 이 예제에서는 부울 식은 학생의 평균 시험 점수가 75보다 큰지 테스트합니다. 이전 예제처럼 완전한 소스 요소가 필요하지 않으므로 결과는 무명 형식으로 프로젝션됩니다. 무명 형식의 속성은 `Key` 멤버에 대한 속성이 되고 쿼리가 실행될 때 이름으로 액세스할 수 있습니다.

`StudentClass` 클래스에 다음 메서드를 붙여넣습니다. `Main` 메서드에서 호출 문을 `sc.GroupByBoolean()`으로 변경합니다.

[!code-csharp[csProgGuideLINQ#20](~/samples/snippets/csharp/concepts/linq/how-to-group-query-results_6.cs)]

## <a name="example"></a>예제

다음 예제에서는 무명 형식을 사용하여 여러 값이 포함된 키를 캡슐화하는 방법을 보여 줍니다. 이 예제에서 첫 번째 키 값은 학생 성의 첫 번째 문자입니다. 두 번째 키 값은 첫 번째 시험에서 학생의 점수가 85보다 큰지 여부를 지정하는 부울입니다. 키의 속성을 기준으로 그룹 순서를 지정할 수 있습니다.

`StudentClass` 클래스에 다음 메서드를 붙여넣습니다. `Main` 메서드에서 호출 문을 `sc.GroupByCompositeKey()`으로 변경합니다.

[!code-csharp[csProgGuideLINQ#21](~/samples/snippets/csharp/concepts/linq/how-to-group-query-results_7.cs)]

## <a name="see-also"></a>참고 항목

- <xref:System.Linq.Enumerable.GroupBy%2A>
- <xref:System.Linq.IGrouping%602>
- [LINQ(Language-Integrated Query)](index.md)
- [group 절](../language-reference/keywords/group-clause.md)
- [익명 형식](../programming-guide/classes-and-structs/anonymous-types.md)
- [그룹화 작업에서 하위 쿼리 수행](perform-a-subquery-on-a-grouping-operation.md)
- [중첩 그룹 만들기](create-a-nested-group.md)
- [데이터 그룹화](../programming-guide/concepts/linq/grouping-data.md)
