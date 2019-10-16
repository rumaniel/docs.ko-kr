---
title: Select 절(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.QuerySelect
helpviewer_keywords:
- Select statement [Visual Basic]
- Select clause [Visual Basic]
- queries [Visual Basic], Select
ms.assetid: 27a3f61c-5960-4692-9b91-4d0c4b6178fe
ms.openlocfilehash: 087472c51d203be083fea0d39ade6f12066cfcb4
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72004742"
---
# <a name="select-clause-visual-basic"></a>Select 절(Visual Basic)
쿼리 결과를 정의 합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Select [ var1 = ] fieldName1 [, [ var2 = ] fieldName2 [...] ]  
```  
  
## <a name="parts"></a>요소  
 `var1`  
 (선택 사항) 열 식의 결과를 참조 하는 데 사용할 수 있는 별칭입니다.  
  
 `fieldName1`  
 필수. 쿼리 결과에 반환할 필드의 이름입니다.  
  
## <a name="remarks"></a>설명  
 @No__t-0 절을 사용 하 여 쿼리에서 반환할 결과를 정의할 수 있습니다. 이렇게 하면 쿼리로 생성 된 새 익명 형식의 멤버를 정의 하거나 쿼리에서 반환 되는 명명 된 형식의 멤버를 대상으로 지정할 수 있습니다. @No__t-0 절은 쿼리에 필요 하지 않습니다. @No__t-0 절을 지정 하지 않으면 쿼리는 현재 범위에 대해 식별 된 범위 변수의 모든 멤버를 기반으로 하는 형식을 반환 합니다. 자세한 내용은 [무명 형식](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)을 참조하세요. 쿼리에서 명명 된 형식을 만들면 <xref:System.Collections.Generic.IEnumerable%601> 형식의 결과가 반환 됩니다. 여기서 `T`은 생성 된 형식입니다.  
  
 @No__t-0 절은 현재 범위에 있는 모든 변수를 참조할 수 있습니다. 여기에는 `From` 절 (또는 `From` 절)에서 식별 된 범위 변수가 포함 됩니다. 또한 `Aggregate`, `Let`, `Group By` 또는 `Group Join` 절을 사용 하 여 별칭을 사용 하 여 만든 새 변수 또는 쿼리 식에 있는 이전 `Select` 절의 변수를 포함 합니다. @No__t-0 절에는 정적 값이 포함 될 수도 있습니다. 예를 들어 다음 코드 예제에서는 `Select` 절이 쿼리 결과를 4 개의 멤버 (`ProductName`, `Price`, `Discount` 및 `DiscountedPrice`)를 사용 하 여 새 무명 형식으로 정의 하는 쿼리 식을 보여 줍니다. @No__t-0 및 `Price` 멤버 값은 `From` 절에 정의 된 product range 변수에서 가져옵니다. @No__t-0 멤버 값은 `Let` 절에서 계산 됩니다. @No__t-0 멤버는 정적 값입니다.  
  
 [!code-vb[VbSimpleQuerySamples#27](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#27)]  
  
 @No__t-0 절은 후속 쿼리 절에 대해 새로운 범위 변수 집합을 도입 하 고 이전 범위 변수는 더 이상 범위에 있지 않습니다. 쿼리 식의 마지막 `Select` 절은 쿼리의 반환 값을 결정 합니다. 예를 들어 다음 쿼리는 합계가 500를 초과 하는 모든 고객 주문에 대 한 회사 이름 및 주문 ID를 반환 합니다. 첫 번째 `Select` 절은 `Where` 절과 두 번째 `Select` 절의 범위 변수를 식별 합니다. 두 번째 `Select` 절은 쿼리에서 반환 되는 값을 새 익명 형식으로 식별 합니다.  
  
 [!code-vb[VbSimpleQuerySamples#28](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#28)]  
  
 @No__t-0 절이 반환할 단일 항목을 식별 하는 경우 쿼리 식은 해당 단일 항목 형식의 컬렉션을 반환 합니다. @No__t-0 절에서 반환할 여러 항목을 식별 하는 경우 쿼리 식은 선택한 항목을 기반으로 새 익명 형식의 컬렉션을 반환 합니다. 예를 들어 다음 두 쿼리는 `Select` 절을 기반으로 하는 두 가지 형식의 컬렉션을 반환 합니다. 첫 번째 쿼리는 회사 이름 컬렉션을 문자열로 반환 합니다. 두 번째 쿼리는 회사 이름과 주소 정보를 사용 하 여 채워진 @no__t 0 개체의 컬렉션을 반환 합니다.  
  
 [!code-vb[VbSimpleQuerySamples#29](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#29)]  
  
## <a name="example"></a>예제  
 다음 쿼리 식은 `From` 절을 사용 하 여 `customers` 컬렉션에 대해 범위 변수 `cust`로 선언 합니다. @No__t-0 절은 고객 이름 및 ID 값을 선택 하 고 새 범위 변수의 `CompanyName` 및 `CustomerID` 열을 채웁니다. @No__t-0 문은 반환 된 각 개체를 반복 하 고 각 레코드에 대해 `CompanyName` 및 `CustomerID` 열을 표시 합니다.  
  
 [!code-vb[VbSimpleQuerySamples#30](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#30)]  
  
## <a name="see-also"></a>참조

- [Visual Basic의 LINQ 소개](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)
- [쿼리](../../../visual-basic/language-reference/queries/index.md)
- [From 절](../../../visual-basic/language-reference/queries/from-clause.md)
- [Where 절](../../../visual-basic/language-reference/queries/where-clause.md)
- [Order By 절](../../../visual-basic/language-reference/queries/order-by-clause.md)
- [익명 형식](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)
