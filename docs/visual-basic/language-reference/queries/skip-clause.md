---
title: Skip 절(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.QuerySkip
helpviewer_keywords:
- queries [Visual Basic], Skip
- Skip statement [Visual Basic]
- Skip clause [Visual Basic]
ms.assetid: f00eb172-3907-4c43-9745-d8546ab86234
ms.openlocfilehash: e52de186e1475bfabd02821a0cd2384d8350eed3
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72004770"
---
# <a name="skip-clause-visual-basic"></a>Skip 절(Visual Basic)
컬렉션에서 지정된 수의 요소를 무시하고 나머지 요소를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Skip count  
```  
  
## <a name="parts"></a>요소  
 `count`  
 필수. 건너뛸 시퀀스의 요소 수로 계산 되는 값 또는 식입니다.  
  
## <a name="remarks"></a>설명  
 @No__t-0 절을 사용 하면 쿼리에서 결과 목록의 시작 부분에 있는 요소를 무시 하 고 나머지 요소를 반환 합니다. 건너뛸 요소의 수는 `count` 매개 변수로 식별 됩니다.  
  
 @No__t-0 절을 `Take` 절과 함께 사용 하 여 쿼리 세그먼트의 데이터 범위를 반환할 수 있습니다. 이렇게 하려면 범위의 첫 번째 요소 인덱스를 `Skip` 절에 전달 하 고 범위의 크기를 `Take` 절에 전달 합니다.  
  
 쿼리에서 `Skip` 절을 사용 하는 경우 `Skip` 절이 의도 한 결과를 무시 하도록 하는 순서로 결과가 반환 되는지 확인 해야 할 수도 있습니다. 쿼리 결과를 정렬 하는 방법에 대 한 자세한 내용은 [Order By 절](../../../visual-basic/language-reference/queries/order-by-clause.md)을 참조 하십시오.  
  
 @No__t-0 절을 사용 하 여 제공 된 조건에 따라 특정 요소만 무시 하도록 지정할 수 있습니다.  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 `Take` 절과 함께 `Skip` 절을 사용 하 여 페이지의 쿼리에서 데이터를 반환 합니다. @No__t-0 함수는 `Skip` 절을 사용 하 여 제공 된 시작 인덱스 값까지 목록의 고객을 무시 하 고, `Take` 절을 사용 하 여 해당 인덱스 값에서 시작 하는 고객의 페이지를 반환 합니다.  
  
 [!code-vb[VbSimpleQuerySamples#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#1)]  
  
## <a name="see-also"></a>참조

- [Visual Basic의 LINQ 소개](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)
- [쿼리](../../../visual-basic/language-reference/queries/index.md)
- [Select 절](../../../visual-basic/language-reference/queries/select-clause.md)
- [From 절](../../../visual-basic/language-reference/queries/from-clause.md)
- [Order By 절](../../../visual-basic/language-reference/queries/order-by-clause.md)
- [Skip While 절](../../../visual-basic/language-reference/queries/skip-while-clause.md)
- [Take 절](../../../visual-basic/language-reference/queries/take-clause.md)
