---
title: Aggregate 절(Visual Basic)
ms.date: 08/28/2018
f1_keywords:
- vb.QueryAggregateIn
- vb.QueryAggregate
- vb.QueryAggregateInto
helpviewer_keywords:
- Aggregate clause [Visual Basic]
- Aggregate statement [Visual Basic]
- queries [Visual Basic], Aggregate
ms.assetid: 1315a814-5db6-4077-b34b-b141e11cc0eb
ms.openlocfilehash: 50a53cd45cc428541c90fbf82089518be2212fae
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72004812"
---
# <a name="aggregate-clause-visual-basic"></a>Aggregate 절(Visual Basic)
하나 이상의 집계 함수를 컬렉션에 적용 합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Aggregate element [As type] In collection _  
  [, element2 [As type2] In collection2, [...]]  
  [ clause ]  
  Into expressionList  
```  
  
## <a name="parts"></a>요소  
  
|용어|정의|  
|---|---|  
|`element`|필수. 컬렉션의 요소를 반복 하는 데 사용 되는 변수입니다.|  
|`type`|(선택 사항) `element`의 형식입니다. 형식이 지정 되지 않은 경우 `element`의 형식이 `collection`에서 유추 됩니다.|  
|`collection`|필수. 작업할 컬렉션을 참조 합니다.|  
|`clause`|(선택 사항) 집계 절 또는 절을에 적용 하는 쿼리 결과를 구체화 하는 `Where` 절과 같은 하나 이상의 쿼리 절입니다.|  
|`expressionList`|필수. 컬렉션에 적용할 집계 함수를 식별 하는 쉼표로 구분 된 하나 이상의 식입니다. 집계 함수에 별칭을 적용 하 여 쿼리 결과의 멤버 이름을 지정할 수 있습니다. 별칭을 제공 하지 않으면 집계 함수의 이름이 사용 됩니다. 예제는이 항목의 뒷부분에 나오는 집계 함수에 대 한 섹션을 참조 하세요.|  
  
## <a name="remarks"></a>설명  
 @No__t-0 절은 쿼리에 집계 함수를 포함 하는 데 사용할 수 있습니다. 집계 함수는 값 집합에 대 한 검사 및 계산을 수행 하 고 단일 값을 반환 합니다. 쿼리 결과 형식의 멤버를 사용 하 여 계산 된 값에 액세스할 수 있습니다. 사용할 수 있는 표준 집계 함수는 `All`, `Any`, `Average`, `Count`, `LongCount`, `Max`, `Sum` 함수입니다. 이러한 함수는 SQL의 집계에 대해 잘 알고 있는 개발자에 게 친숙 합니다. 이러한 내용은이 항목의 다음 섹션에 설명 되어 있습니다.  
  
 집계 함수의 결과는 쿼리 결과 형식의 필드로 쿼리 결과에 포함 됩니다. 집계 함수 결과에 대 한 별칭을 제공 하 여 집계 값을 포함 하는 쿼리 결과 형식의 멤버 이름을 지정할 수 있습니다. 별칭을 제공 하지 않으면 집계 함수의 이름이 사용 됩니다.  
  
 @No__t-0 절은 쿼리를 시작 하거나 쿼리에 추가 절로 포함 될 수 있습니다. @No__t-0 절이 쿼리를 시작 하는 경우 결과는 `Into` 절에 지정 된 집계 함수의 결과인 단일 값입니다. @No__t-0 절에 둘 이상의 집계 함수가 지정 된 경우 쿼리는 `Into` 절에서 각 집계 함수의 결과를 참조 하는 별도의 속성이 있는 단일 형식을 반환 합니다. @No__t-0 절이 쿼리에 추가 절로 포함 된 경우 쿼리 컬렉션에서 반환 되는 형식에는 `Into` 절에서 각 집계 함수의 결과를 참조 하는 별도의 속성이 포함 됩니다.  
  
## <a name="aggregate-functions"></a>집계 함수

다음은 `Aggregate` 절과 함께 사용할 수 있는 표준 집계 함수입니다.  
  
### <a name="all"></a>모두

컬렉션의 모든 요소가 지정 된 조건을 만족 하는 경우 `true`을 반환 합니다. 그렇지 않으면-1 @no__t 반환 합니다. 예를 들면 다음과 같습니다.

 [!code-vb[VbSimpleQuerySamples#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#5)]

### <a name="any"></a>임의의 값

컬렉션의 요소가 지정 된 조건을 만족 하는 경우 `true`을 반환 합니다. 그렇지 않으면-1 @no__t 반환 합니다. 예를 들면 다음과 같습니다.

 [!code-vb[VbSimpleQuerySamples#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#6)]

### <a name="average"></a>평균

컬렉션의 모든 요소에 대 한 평균을 계산 하거나 컬렉션의 모든 요소에 대해 제공 된 식을 계산 합니다. 예를 들면 다음과 같습니다.

 [!code-vb[VbSimpleQuerySamples#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#7)]

### <a name="count"></a>개수

컬렉션의 요소 수를 셉니다. 선택적 `Boolean` 식을 제공 하 여 컬렉션에서 조건에 맞는 요소 수만 계산할 수 있습니다. 예를 들면 다음과 같습니다.

 [!code-vb[VbSimpleQuerySamples#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#8)]

### <a name="group"></a>그룹

@No__t-0 또는 `Group Join` 절의 결과로 그룹화 되는 쿼리 결과를 나타냅니다. @No__t-0 함수는 `Group By` 또는 `Group Join` 절의 `Into` 절 에서만 사용할 수 있습니다. 자세한 내용 및 예제는 [Group By 절](../../../visual-basic/language-reference/queries/group-by-clause.md) 및 [group Join 절](../../../visual-basic/language-reference/queries/group-join-clause.md)을 참조 하세요.

### <a name="longcount"></a>LongCount

컬렉션의 요소 수를 셉니다. 선택적 `Boolean` 식을 제공 하 여 컬렉션에서 조건에 맞는 요소 수만 계산할 수 있습니다. 결과를 `Long`으로 반환 합니다. 예는 `Count` 집계 함수를 참조 하세요.

### <a name="max"></a>최대

컬렉션에서 최 댓 값을 계산 하거나 컬렉션의 모든 요소에 대해 제공 된 식을 계산 합니다. 예를 들면 다음과 같습니다.

 [!code-vb[VbSimpleQuerySamples#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#9)]

### <a name="min"></a>최소

컬렉션의 최소값을 계산 하거나 컬렉션의 모든 요소에 대해 제공 된 식을 계산 합니다. 예를 들면 다음과 같습니다.

 [!code-vb[VbSimpleQuerySamples#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#10)]

### <a name="sum"></a>Sum

컬렉션에 있는 모든 요소의 합계를 계산 하거나 컬렉션의 모든 요소에 대해 제공 된 식을 계산 합니다. 예를 들면 다음과 같습니다.

 [!code-vb[VbSimpleQuerySamples#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#15)]

## <a name="example"></a>예제  

다음 예에서는 `Aggregate` 절을 사용 하 여 쿼리 결과에 집계 함수를 적용 하는 방법을 보여 줍니다.  
  
 [!code-vb[VbSimpleQuerySamples#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#4)]  
  
## <a name="creating-user-defined-aggregate-functions"></a>사용자 정의 집계 함수 만들기

 @No__t-0 형식에 확장 메서드를 추가 하 여 쿼리 식에 사용자 지정 집계 함수를 포함할 수 있습니다. 그런 다음 사용자 지정 메서드는 집계 함수를 참조 하는 열거 가능한 컬렉션에 대해 계산 또는 연산을 수행할 수 있습니다. 확장 메서드에 대한 자세한 내용은 [확장 메서드](../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)를 참조하세요.  
  
 예를 들어 다음 예제에서는 숫자 컬렉션의 중앙값을 계산 하는 사용자 지정 집계 함수를 보여 줍니다. @No__t-0 확장 메서드에는 두 개의 오버 로드가 있습니다. 첫 번째 오버 로드는 `IEnumerable(Of Double)` 형식의 컬렉션인 입력으로 받아들입니다. @No__t-1 형식의 쿼리 필드에 대해 `Median` 집계 함수를 호출 하면이 메서드가 호출 됩니다. @No__t-0 메서드의 두 번째 오버 로드는 모든 제네릭 형식으로 전달 될 수 있습니다. @No__t-0 메서드의 제네릭 오버 로드는 `Func(Of T, Double)` 람다 식을 참조 하는 두 번째 매개 변수를 사용 하 여 컬렉션에서 형식의 값을 `Double` 형식의 해당 값으로 프로젝션 합니다. 그런 다음 `Median` 메서드의 다른 오버 로드에 중앙값 값의 계산을 위임 합니다. 람다 식에 대한 자세한 내용은 [람다 식](../../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md)을 참조하세요.  
  
 [!code-vb[VbSimpleQuerySamples#18](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/UserDefinedAggregates.vb#18)]  
  
 다음 예에서는 `Integer` 형식의 컬렉션에서 `Median` 집계 함수를 호출 하는 예제 쿼리와 `Double` 형식의 컬렉션을 보여 줍니다. @No__t-1 형식의 컬렉션에서 `Median` 집계 함수를 호출 하는 쿼리는 `Double` 형식의 컬렉션을 입력으로 허용 하는 `Median` 메서드의 오버 로드를 호출 합니다. @No__t-1 형식의 컬렉션에서 `Median` 집계 함수를 호출 하는 쿼리는 `Median` 메서드의 제네릭 오버 로드를 호출 합니다.  
  
 [!code-vb[VbSimpleQuerySamples#19](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/UserDefinedAggregates.vb#19)]  
  
## <a name="see-also"></a>참조

- [Visual Basic의 LINQ 소개](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)
- [쿼리](../../../visual-basic/language-reference/queries/index.md)
- [Select 절](../../../visual-basic/language-reference/queries/select-clause.md)
- [From 절](../../../visual-basic/language-reference/queries/from-clause.md)
- [Where 절](../../../visual-basic/language-reference/queries/where-clause.md)
- [Group By 절](../../../visual-basic/language-reference/queries/group-by-clause.md)
