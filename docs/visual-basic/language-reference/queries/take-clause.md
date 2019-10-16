---
title: Take 절(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.QueryTake
helpviewer_keywords:
- Take statement [Visual Basic]
- queries [Visual Basic], Take
- Take clause [Visual Basic]
ms.assetid: 77bf87b2-1476-4456-957f-fee922fbad8c
ms.openlocfilehash: 32a4c7fd7f1e2f6fe640f3f53f15579f014759d5
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72004721"
---
# <a name="take-clause-visual-basic"></a>Take 절(Visual Basic)
컬렉션의 시작 위치에서 지정된 수의 연속 요소를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Take count  
```  
  
## <a name="parts"></a>요소  
 `count`  
 필수. 반환할 시퀀스의 요소 수로 계산 되는 값 또는 식입니다.  
  
## <a name="remarks"></a>설명  
 @No__t-0 절은 쿼리가 결과 목록의 시작 부분에서 지정 된 개수의 연속 요소를 포함 하도록 합니다. 포함할 요소의 수는 `count` 매개 변수로 지정 됩니다.  
  
 @No__t-0 절을 `Skip` 절과 함께 사용 하 여 쿼리 세그먼트의 데이터 범위를 반환할 수 있습니다. 이렇게 하려면 범위의 첫 번째 요소 인덱스를 `Skip` 절에 전달 하 고 범위의 크기를 `Take` 절에 전달 합니다. 이 경우 `Skip` 절 뒤에 `Take` 절을 지정 해야 합니다.  
  
 쿼리에서 `Take` 절을 사용 하는 경우에는 `Take` 절에서 원하는 결과를 포함할 수 있도록 결과가 순서 대로 반환 되는지 확인 해야 할 수도 있습니다. 쿼리 결과를 정렬 하는 방법에 대 한 자세한 내용은 [Order By 절](../../../visual-basic/language-reference/queries/order-by-clause.md)을 참조 하십시오.  
  
 @No__t-0 절을 사용 하 여 제공 된 조건에 따라 특정 요소만 반환 되도록 지정할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 `Skip` 절과 함께 `Take` 절을 사용 하 여 페이지의 쿼리에서 데이터를 반환 합니다. GetCustomers 함수는 `Skip` 절을 사용 하 여 제공 된 시작 인덱스 값까지 목록의 고객을 우회 하 고 `Take` 절을 사용 하 여 해당 인덱스 값에서 시작 하는 고객의 페이지를 반환 합니다.  
  
 [!code-vb[VbSimpleQuerySamples#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#1)]  
  
## <a name="see-also"></a>참조

- [Visual Basic의 LINQ 소개](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)
- [쿼리](../../../visual-basic/language-reference/queries/index.md)
- [Select 절](../../../visual-basic/language-reference/queries/select-clause.md)
- [From 절](../../../visual-basic/language-reference/queries/from-clause.md)
- [Order By 절](../../../visual-basic/language-reference/queries/order-by-clause.md)
- [Take While 절](../../../visual-basic/language-reference/queries/take-while-clause.md)
- [Skip 절](../../../visual-basic/language-reference/queries/skip-clause.md)
