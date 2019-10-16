---
title: <variable> 범위 변수가 바깥쪽 블록의 변수, 이전에 정의한 범위 변수 또는 쿼리 식에 암시적으로 선언한 변수를 숨깁니다.
ms.date: 07/20/2015
f1_keywords:
- bc36633
- vbc36633
helpviewer_keywords:
- BC36633
ms.assetid: 5d5470e4-3de5-49c2-8831-1087625f4a77
ms.openlocfilehash: 5e071970eec70828841c686e89aa673d38ff9918
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64661617"
---
# <a name="range-variable-variable-hides-a-variable-in-an-enclosing-block-a-previously-defined-range-variable-or-an-implicitly-declared-variable-in-a-query-expression"></a>범위 변수 \<변수 >의 변수는 바깥쪽 블록, 이전에 정의한 범위 변수 또는 쿼리 식에서 암시적으로 선언한 변수를 숨깁니다.
에 지정 된 범위 변수 이름이 `Select`, `From`를 `Aggregate`, 또는 `Let` 절 쿼리 또는 쿼리에 의해 암시적으로 선언 된 변수 이름에 이미 이전에 지정한 범위 변수 이름과 중복 필드 이름 등을 집계 함수의 이름입니다.  
  
 **오류 ID:** BC36633  
  
## <a name="to-correct-this-error"></a>이 오류를 해결하려면  
  
- 특정 쿼리 범위 안에 있는 모든 범위 변수 이름이 고유한 지 확인 합니다. 쿼리를 중첩된 쿼리 고유한 범위를 갖도록 괄호로 묶을 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- [Visual Basic의 LINQ 소개](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)
- [From 절](../../../visual-basic/language-reference/queries/from-clause.md)
- [Let 절](../../../visual-basic/language-reference/queries/let-clause.md)
- [Aggregate 절](../../../visual-basic/language-reference/queries/aggregate-clause.md)
- [Select 절](../../../visual-basic/language-reference/queries/select-clause.md)
