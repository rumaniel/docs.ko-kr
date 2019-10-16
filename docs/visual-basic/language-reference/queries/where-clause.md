---
title: Where 절(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.QueryWhere
helpviewer_keywords:
- Where statement [Visual Basic]
- queries [Visual Basic], Where
- Where clause [Visual Basic]
ms.assetid: 48b5c2c5-3181-429c-8545-894296798c89
ms.openlocfilehash: 404dd848058f7e5c9bc8a74b6d89df18c6c55fad
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005004"
---
# <a name="where-clause-visual-basic"></a>Where 절(Visual Basic)
쿼리의 필터링 조건을 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Where condition  
```  
  
## <a name="parts"></a>요소  
 `condition`  
 필수. 컬렉션의 현재 항목에 대 한 값이 출력 컬렉션에 포함 되는지 여부를 결정 하는 식입니다. 식은 `Boolean` 값 또는 `Boolean` 값에 해당 하는 값으로 계산 되어야 합니다. 조건이 `True`으로 평가 되 면 요소가 쿼리 결과에 포함 됩니다. 그렇지 않으면 요소가 쿼리 결과에서 제외 됩니다.  
  
## <a name="remarks"></a>설명  
 @No__t-0 절은 특정 조건을 충족 하는 요소만 선택 하 여 쿼리 데이터를 필터링 할 수 있도록 합니다. 값이 `Where` 절이 `True`로 계산 되는 요소는 쿼리 결과에 포함 됩니다. 다른 요소는 제외 됩니다. @No__t-0 절에 사용 되는 식은 `Boolean` 또는 해당 값이 0 일 때 `False`으로 계산 되는 정수와 같은 `Boolean`에 해당 하는 값으로 계산 되어야 합니다. @No__t-1, `Or`, `AndAlso`, `OrElse`, `Is`, `IsNot`과 같은 논리 연산자를 사용 하 여 `Where` 절에서 여러 식을 결합할 수 있습니다.  
  
 기본적으로 쿼리 식은 액세스 될 때까지 계산 되지 않습니다. 예를 들어, `For` 루프에서 데이터 바인딩되거나 반복 될 때 쿼리 식이 계산 됩니다. 따라서 `Where` 절은 쿼리를 액세스할 때까지 평가 되지 않습니다. @No__t-0 절에서 사용 되는 쿼리 외부 값이 있는 경우에는 쿼리가 실행 될 때 `Where` 절에서 적절 한 값을 사용 해야 합니다. 쿼리 실행에 대 한 자세한 내용은 [첫 번째 LINQ 쿼리 작성](../../../visual-basic/programming-guide/concepts/linq/writing-your-first-linq-query.md)을 참조 하세요.  
  
 @No__t-0 절 내에서 함수를 호출 하 여 컬렉션의 현재 요소에서 값에 대 한 계산 또는 연산을 수행할 수 있습니다. @No__t-0 절에서 함수를 호출 하면 쿼리가 액세스 될 때가 아니라 정의 될 때 쿼리를 즉시 실행할 수 있습니다. 쿼리 실행에 대 한 자세한 내용은 [첫 번째 LINQ 쿼리 작성](../../../visual-basic/programming-guide/concepts/linq/writing-your-first-linq-query.md)을 참조 하세요.  
  
## <a name="example"></a>예제  
 다음 쿼리 식은 `From` 절을 사용 하 여 `customers` 컬렉션의 각 `Customer` 개체에 대해 범위 변수 `cust`을 선언 합니다. @No__t-0 절은 범위 변수를 사용 하 여 지정 된 지역의 고객에 대 한 출력을 제한 합니다. @No__t-0 루프는 쿼리 결과에서 각 고객의 회사 이름을 표시 합니다.  
  
 [!code-vb[VbSimpleQuerySamples#23](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#23)]  
  
## <a name="example"></a>예제  
 다음 예에서는 `Where` 절에 `And` 및 `Or` 논리 연산자를 사용 합니다.  
  
 [!code-vb[VbSimpleQuerySamples#31](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#31)]  
  
## <a name="see-also"></a>참조

- [Visual Basic의 LINQ 소개](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)
- [쿼리](../../../visual-basic/language-reference/queries/index.md)
- [From 절](../../../visual-basic/language-reference/queries/from-clause.md)
- [Select 절](../../../visual-basic/language-reference/queries/select-clause.md)
- [For Each...Next 문](../../../visual-basic/language-reference/statements/for-each-next-statement.md)
