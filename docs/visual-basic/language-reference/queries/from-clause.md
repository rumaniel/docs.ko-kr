---
title: From 절(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.QueryFrom
- vb.QueryFromIn
- vb.QueryFromLet
helpviewer_keywords:
- queries [Visual Basic], From
- From clause [Visual Basic]
- From statement [Visual Basic]
ms.assetid: 83e3665e-68a0-4540-a3a3-3d777a0f95d5
ms.openlocfilehash: 781902f1bf28bd029c8d9825aee155a6691cbae9
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72004785"
---
# <a name="from-clause-visual-basic"></a>From 절(Visual Basic)
하나 이상의 범위 변수와 쿼리할 컬렉션을 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
From element [ As type ] In collection [ _ ]  
  [, element2 [ As type2 ] In collection2 [, ... ] ]  
```  
  
## <a name="parts"></a>요소  
  
|용어|정의|  
|---|---|  
|`element`|필수. 컬렉션의 요소를 반복 하는 데 사용 되는 *범위 변수* 입니다. 범위 변수는 쿼리가 `collection`을 반복 하면 `collection`의 각 멤버를 참조 하는 데 사용 됩니다. 는 열거 가능한 형식 이어야 합니다.|  
|`type`|(선택 사항) `element`의 형식입니다. @No__t-0이 지정 되지 않은 경우 `element`의 형식은 `collection`에서 유추 됩니다.|  
|`collection`|필수. 쿼리할 컬렉션을 참조 합니다. 는 열거 가능한 형식 이어야 합니다.|  
  
## <a name="remarks"></a>설명  
 @No__t-0 절은 쿼리의 소스 데이터와 소스 컬렉션의 요소를 참조 하는 데 사용 되는 변수를 식별 하는 데 사용 됩니다. 이러한 변수를 *범위 변수*라고 합니다. @No__t-1 절을 사용 하 여 집계 된 결과만 반환 하는 쿼리를 식별 하는 경우를 제외 하 고는 `From` 절이 필요 합니다. 자세한 내용은 [Aggregate 절](../../../visual-basic/language-reference/queries/aggregate-clause.md)을 참조 하세요.  
  
 쿼리에 여러 개의 `From` 절을 지정 하 여 조인할 여러 컬렉션을 식별할 수 있습니다. 여러 컬렉션을 지정 하는 경우 이러한 컬렉션은 독립적으로 반복 되거나 관련 된 경우 조인할 수 있습니다. @No__t-0 절을 사용 하 여 암시적으로 또는 `Join` 또는 `Group Join` 절을 사용 하 여 명시적으로 컬렉션을 조인할 수 있습니다. 또는 각각의 관련 범위 변수와 컬렉션을 쉼표로 구분 하 여 단일 `From` 절에 여러 범위 변수와 컬렉션을 지정할 수 있습니다. 다음 코드 예에서는 `From` 절에 대 한 두 가지 구문 옵션을 보여 줍니다.  
  
 [!code-vb[VbSimpleQuerySamples#21](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#21)]  
  
 @No__t-0 절은 쿼리 범위를 정의 하며,이는 `For` 루프의 범위와 비슷합니다. 따라서 쿼리 범위에 있는 각 `element` 범위 변수에는 고유한 이름이 있어야 합니다. 쿼리에 대해 여러 개의 `From` 절을 지정할 수 있으므로 후속 `From` 절은 `From` 절의 범위 변수를 참조 하거나 이전 `From` 절의 범위 변수를 참조할 수 있습니다. 예를 들어 다음 예에서는 두 번째 절의 컬렉션이 첫 번째 절의 범위 변수 속성을 기반으로 하는 중첩 된 `From` 절을 보여 줍니다.  
  
 [!code-vb[VbSimpleQuerySamples#22](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#22)]  
  
 각 `From` 절 뒤에는 쿼리를 구체화 하기 위한 추가 쿼리 절의 조합이 올 수 있습니다. 다음과 같은 방법으로 쿼리를 구체화할 수 있습니다.  
  
- @No__t-0 및 `Select` 절을 사용 하 여 명시적으로 또는 `Join` 또는 `Group Join` 절을 사용 하 여 명시적으로 여러 컬렉션을 결합 합니다.  
  
- @No__t-0 절을 사용 하 여 쿼리 결과를 필터링 합니다.  
  
- @No__t-0 절을 사용 하 여 결과를 정렬 합니다.  
  
- @No__t-0 절을 사용 하 여 비슷한 결과를 그룹화 합니다.  
  
- @No__t-0 절을 사용 하 여 전체 쿼리 결과에 대해 평가할 집계 함수를 식별 합니다.  
  
- @No__t-0 절을 사용 하 여 해당 값이 컬렉션이 아닌 식에 의해 결정 되는 반복 변수를 도입할 수 있습니다.  
  
- @No__t-0 절을 사용 하 여 중복 쿼리 결과를 무시 합니다.  
  
- @No__t-0, `Take`, `Skip While` 및 `Take While` 절을 사용 하 여 반환할 결과의 일부를 식별 합니다.  
  
## <a name="example"></a>예제  
 다음 쿼리 식은 `From` 절을 사용 하 여 `customers` 컬렉션의 각 `Customer` 개체에 대해 범위 변수 `cust`을 선언 합니다. @No__t-0 절은 범위 변수를 사용 하 여 지정 된 지역의 고객에 대 한 출력을 제한 합니다. @No__t-0 루프는 쿼리 결과에서 각 고객의 회사 이름을 표시 합니다.  
  
 [!code-vb[VbSimpleQuerySamples#23](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#23)]  
  
## <a name="see-also"></a>참조

- [쿼리](../../../visual-basic/language-reference/queries/index.md)
- [Visual Basic의 LINQ 소개](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)
- [For Each...Next 문](../../../visual-basic/language-reference/statements/for-each-next-statement.md)
- [For...Next 문](../../../visual-basic/language-reference/statements/for-next-statement.md)
- [Select 절](../../../visual-basic/language-reference/queries/select-clause.md)
- [Where 절](../../../visual-basic/language-reference/queries/where-clause.md)
- [Aggregate 절](../../../visual-basic/language-reference/queries/aggregate-clause.md)
- [Distinct 절](../../../visual-basic/language-reference/queries/distinct-clause.md)
- [Join 절](../../../visual-basic/language-reference/queries/join-clause.md)
- [Group Join 절](../../../visual-basic/language-reference/queries/group-join-clause.md)
- [Order By 절](../../../visual-basic/language-reference/queries/order-by-clause.md)
- [Let 절](../../../visual-basic/language-reference/queries/let-clause.md)
- [Skip 절](../../../visual-basic/language-reference/queries/skip-clause.md)
- [Take 절](../../../visual-basic/language-reference/queries/take-clause.md)
- [Skip While 절](../../../visual-basic/language-reference/queries/skip-while-clause.md)
- [Take While 절](../../../visual-basic/language-reference/queries/take-while-clause.md)
