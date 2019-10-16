---
title: Order By 절(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.QueryOrderBy
- vb.QueryAscending
- vb.QueryDescending
helpviewer_keywords:
- queries [Visual Basic], Order By
- Order By clause [Visual Basic]
- Order By statement [Visual Basic]
ms.assetid: fa911282-6b81-44c7-acfa-46b5bb93df75
ms.openlocfilehash: f8ee46b12e84f99629c3a92057fc3a7bb8a3c2e8
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72004944"
---
# <a name="order-by-clause-visual-basic"></a>Order By 절(Visual Basic)
쿼리 결과의 정렬 순서를 지정 합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Order By orderExp1 [ Ascending | Descending ] [, orderExp2 [...] ]  
```  
  
## <a name="parts"></a>요소  
 `orderExp1`  
 필수. 반환 된 값의 순서를 지정 하는 방법을 식별 하는 현재 쿼리 결과에서 하나 이상의 필드입니다. 필드 이름은 쉼표 (,)로 구분 해야 합니다. @No__t-0 또는 `Descending` 키워드를 사용 하 여 각 필드를 오름차순 또는 내림차순으로 정렬 하 여 식별할 수 있습니다. @No__t-0 또는 `Descending` 키워드가 지정 되지 않은 경우 기본 정렬 순서는 오름차순입니다. 정렬 순서 필드는 왼쪽에서 오른쪽으로 우선 순위가 지정 됩니다.  
  
## <a name="remarks"></a>설명  
 @No__t-0 절을 사용 하 여 쿼리 결과를 정렬할 수 있습니다. @No__t-0 절은 현재 범위에 대 한 범위 변수에 따라 결과만 정렬할 수 있습니다. 예를 들어 `Select` 절은 쿼리 식에서 해당 범위에 대 한 새 반복 변수를 사용 하 여 새 범위를 도입 합니다. @No__t-1 절 이후 쿼리에서 `Select` 절 앞에 정의 된 범위 변수를 사용할 수 없습니다. 따라서 `Select` 절에서 사용할 수 없는 필드를 기준으로 결과를 정렬 하려면 `Order By` 절을 `Select` 절 앞에 배치 해야 합니다. 이 작업을 수행 해야 하는 한 가지 예는 결과의 일부로 반환 되지 않는 필드를 기준으로 쿼리를 정렬 하려는 경우입니다.  
  
 필드에 대 한 오름차순 및 내림차순은 필드의 데이터 형식에 대 한 <xref:System.IComparable> 인터페이스의 구현에 의해 결정 됩니다. 데이터 형식이 <xref:System.IComparable> 인터페이스를 구현 하지 않는 경우 정렬 순서는 무시 됩니다.  
  
## <a name="example"></a>예제  
 다음 쿼리 식은 `From` 절을 사용 하 여 `books` 컬렉션에 대해 범위 변수 `book`로 선언 합니다. @No__t-0 절은 가격을 기준으로 쿼리 결과를 오름차순 (기본값)으로 정렬 합니다. 가격이 동일한 책은 제목으로 오름차순으로 정렬 됩니다. @No__t-0 절은 쿼리에서 반환 된 값으로 `Title` 및 `Price` 속성을 선택 합니다.  
  
 [!code-vb[VbSimpleQuerySamples#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#24)]  
  
## <a name="example"></a>예제  
 다음 쿼리 식은 `Order By` 절을 사용 하 여 가격을 기준으로 내림차순으로 쿼리 결과를 정렬 합니다. 가격이 동일한 책은 제목으로 오름차순으로 정렬 됩니다.  
  
 [!code-vb[VbSimpleQuerySamples#25](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#25)]  
  
## <a name="example"></a>예제  
 다음 쿼리 식은 `Select` 절을 사용 하 여 책 제목, 가격, 게시 날짜 및 작성자를 선택 합니다. 그런 다음 새 범위에 대 한 범위 변수의 `Title`, `Price`, `PublishDate` 및 `Author` 필드를 채웁니다. @No__t-0 절은 새 범위 변수를 저자 이름, 책 제목 및 가격을 기준으로 정렬 합니다. 각 열은 기본 순서 (오름차순)로 정렬 됩니다.  
  
 [!code-vb[VbSimpleQuerySamples#26](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#26)]  
  
## <a name="see-also"></a>참조

- [Visual Basic의 LINQ 소개](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)
- [쿼리](../../../visual-basic/language-reference/queries/index.md)
- [Select 절](../../../visual-basic/language-reference/queries/select-clause.md)
- [From 절](../../../visual-basic/language-reference/queries/from-clause.md)
