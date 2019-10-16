---
title: 내부 조인 수행(C#의 LINQ)
description: C#에서 LINQ를 사용하여 내부 조인을 수행하는 방법을 알아봅니다.
ms.date: 12/01/2016
ms.assetid: 45bceed6-f549-4114-a9b1-b44feb497742
ms.openlocfilehash: a3e8e9bd97ec630797bc48a3302b27ed45d9103e
ms.sourcegitcommit: 5dcfeb59179e81071f54840d4902cbe00b184294
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54857959"
---
# <a name="perform-inner-joins"></a>내부 조인 수행

관계형 데이터베이스 용어에서 *내부 조인*은 첫 번째 컬렉션의 각 요소가 두 번째 컬렉션에서 일치하는 모든 요소에 대해 한 번 표시되는 결과 집합을 생성합니다. 첫 번째 컬렉션의 요소에 일치하는 요소가 없는 경우에는 결과 집합에 표시되지 않습니다. C#에서 `join` 절에 의해 호출되는 <xref:System.Linq.Enumerable.Join%2A> 메서드는 내부 조인을 구현합니다.

이 문서에서는 내부 조인의 네 가지 변환을 수행하는 방법을 보여 줍니다.

- 단순 키에 따라 두 데이터 소스의 요소를 상호 연결하는 간단한 내부 조인

- *복합* 키에 따라 두 데이터 소스의 요소를 상호 연결하는 내부 조인. 둘 이상의 값으로 구성된 키인 복합 키를 사용하면 둘 이상의 속성에 따라 요소를 상호 연결할 수 있습니다.

- 연속 조인 작업이 서로 추가되는 *여러 조인*

- 그룹 조인을 사용하여 구현되는 내부 조인

## <a name="example---simple-key-join"></a>예제 - 단순 키 조인

다음 예제에서는 두 개의 사용자 정의 형식인 `Person` 및 `Pet`의 개체를 포함하는 두 개의 컬렉션을 만듭니다. 쿼리는 C#의 `join` 절을 사용하여 `Person` 개체를 `Owner`가 해당 `Person`인 `Pet` 개체와 일치시킵니다. C#의 `select` 절은 결과 개체의 모양을 정의합니다. 이 예제에서 결과 개체는 소유자의 이름과 애완 동물의 이름으로 구성된 무명 형식입니다.

[!code-csharp[CsLINQProgJoining#1](~/samples/snippets/csharp/concepts/linq/how-to-perform-inner-joins_1.cs)]

`LastName`이 "Huff"인 `Person` 개체는 `Pet.Owner`가 `Person`과 같은 `Pet` 개체가 없기 때문에 결과 집합에 표시되지 않습니다.

## <a name="example---composite-key-join"></a>예제 - 복합 키 조인

속성 하나만 기준으로 요소를 상호 연결하는 대신 복합 키를 사용하여 여러 속성을 기준으로 요소를 비교할 수 있습니다. 이렇게 하려면 비교하려는 속성으로 구성된 무명 형식을 반환할 각 컬렉션에 대한 키 선택기 함수를 지정합니다. 속성에 레이블을 지정하는 경우 각 키의 무명 형식에 동일한 레이블이 있어야 합니다. 또한 속성은 동일한 순서로 나타나야 합니다.

다음 예제에서는 `Employee` 개체 목록과 `Student` 개체 목록을 사용하여 학생이기도 한 직원을 확인합니다. 이러한 형식에는 둘 다 <xref:System.String> 형식의 `FirstName` 및 `LastName` 속성이 있습니다. 각 목록의 요소에서 조인 키를 만드는 함수는 각 요소의 `FirstName` 및 `LastName` 속성으로 구성된 무명 형식을 반환합니다. 조인 작업은 이러한 복합 키가 같은지 비교하고 각 목록에서 이름과 성이 둘 다 일치하는 개체 쌍을 반환합니다.

[!code-csharp[CsLINQProgJoining#2](~/samples/snippets/csharp/concepts/linq/how-to-perform-inner-joins_2.cs)]

## <a name="example---multiple-join"></a>예제 - 여러 조인

개수에 제한없이 조인 작업을 서로 추가하여 여러 조인을 수행할 수 있습니다. C#의 각 `join` 절은 지정된 데이터 소스를 이전 조인의 결과와 상호 연결합니다.

다음 예제에서는 `Person` 개체 목록, `Cat` 개체 목록, `Dog` 개체 목록의 세 가지 컬렉션을 만듭니다.

C#의 첫 번째 `join` 절은 `Cat.Owner`와 일치하는 `Person`을 기준으로 사람과 고양이를 일치시킵니다. `Person` 개체 및 `Cat.Name`을 포함하는 무명 형식의 시퀀스를 반환합니다.

C#의 두 번째 `join` 절은 `Person` 형식의 `Owner` 속성과 동물 이름의 첫 글자로 구성된 복합 키를 기준으로 제공된 개 목록의 `Dog` 개체와 첫 번째 조인에서 반환된 무명 형식을 상호 연결합니다. 일치하는 각 쌍의 `Cat.Name` 및 `Dog.Name` 속성을 포함하는 무명 형식의 시퀀스를 반환합니다. 내부 조인이기 때문에 두 번째 데이터 소스에 일치 항목이 있는 첫 번째 데이터 소스의 개체만 반환됩니다.

[!code-csharp[CsLINQProgJoining#3](~/samples/snippets/csharp/concepts/linq/how-to-perform-inner-joins_3.cs)]

## <a name="example---inner-join-by-using-grouped-join"></a>예제 - 그룹화된 조인을 사용하는 내부 조인

다음 예제에서는 그룹 조인을 사용하여 내부 조인을 구현하는 방법을 보여 줍니다.

`query1`에서 `Person` 개체 목록은 `Pet.Owner` 속성과 일치하는 `Person`을 기준으로 `Pet` 개체 목록에 그룹 조인됩니다. 그룹 조인은 각 그룹이 `Person` 개체 및 일치하는 `Pet` 개체 시퀀스로 구성된 중간 그룹 컬렉션을 만듭니다.

두 번째 `from` 절을 쿼리에 추가하여 이 시퀀스의 시퀀스를 더 긴 시퀀스에 결합(또는 평면화)할 수 있습니다. 최종 시퀀스의 요소 형식은 `select` 절에 의해 지정됩니다. 이 예제에서 해당 형식은 일치하는 각 쌍의 `Person.FirstName` 및 `Pet.Name` 속성으로 구성된 무명 형식입니다.

`query1`의 결과는 `into` 절 없이 `join` 절을 사용해서 내부 조인을 수행하여 얻은 결과 집합과 같습니다. `query2` 변수는 이와 동일한 쿼리를 보여 줍니다.

[!code-csharp[CsLINQProgJoining#4](~/samples/snippets/csharp/concepts/linq/how-to-perform-inner-joins_4.cs)]

## <a name="see-also"></a>참고 항목

- <xref:System.Linq.Enumerable.Join%2A>
- <xref:System.Linq.Enumerable.GroupJoin%2A>
- [그룹화 조인 수행](perform-grouped-joins.md)
- [왼쪽 우선 외부 조인 수행](perform-left-outer-joins.md)
- [무명 형식](../programming-guide/classes-and-structs/anonymous-types.md)
