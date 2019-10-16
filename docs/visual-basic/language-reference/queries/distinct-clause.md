---
title: Distinct 절(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.QueryDistinct
helpviewer_keywords:
- Distinct clause [Visual Basic]
- Distinct statement [Visual Basic]
- queries [Visual Basic], Distinct
ms.assetid: 86f42614-0d8f-4ffc-b888-ce8a37a8d36a
ms.openlocfilehash: e8d3e38261a04c4d29faab351d24d6710413b09a
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72004796"
---
# <a name="distinct-clause-visual-basic"></a>Distinct 절(Visual Basic)
후속 쿼리 절에서 중복 값을 제거 하도록 현재 범위 변수의 값을 제한 합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Distinct  
```  
  
## <a name="remarks"></a>설명  
 @No__t-0 절을 사용 하 여 고유한 항목의 목록을 반환할 수 있습니다. @No__t-0 절은 쿼리가 중복 쿼리 결과를 무시 하도록 합니다. @No__t-0 절은 `Select` 절에서 지정한 모든 반환 필드에 대해 중복 값에 적용 됩니다. @No__t-0 절이 지정 되지 않은 경우 `Distinct` 절은 `From` 절에서 식별 된 쿼리의 범위 변수에 적용 됩니다. 범위 변수가 변경할 수 없는 형식이 아닌 경우에는 해당 형식의 모든 멤버가 기존 쿼리 결과와 일치 하는 경우에만 쿼리 결과가 무시 됩니다.  
  
## <a name="example"></a>예제  
 다음 쿼리 식은 고객 목록과 고객 주문 목록을 조인 합니다. 고유 고객 이름과 주문 날짜 목록을 반환 하는 `Distinct` 절이 포함 되어 있습니다.  
  
 [!code-vb[VbSimpleQuerySamples#20](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#20)]  
  
## <a name="see-also"></a>참조

- [Visual Basic의 LINQ 소개](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)
- [쿼리](../../../visual-basic/language-reference/queries/index.md)
- [From 절](../../../visual-basic/language-reference/queries/from-clause.md)
- [Select 절](../../../visual-basic/language-reference/queries/select-clause.md)
- [Where 절](../../../visual-basic/language-reference/queries/where-clause.md)
