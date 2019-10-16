---
title: Let 절(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.QueryLet
helpviewer_keywords:
- queries [Visual Basic], Let
- Let clause [Visual Basic]
- Let statement [Visual Basic]
ms.assetid: 981aa516-16eb-4c53-b1f1-5aa3e82f316e
ms.openlocfilehash: 88166a040823cfefe623f672e556c364d652a7fc
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72004735"
---
# <a name="let-clause-visual-basic"></a>Let 절(Visual Basic)
값을 계산 하 여 쿼리 내의 새 변수에 할당 합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Let variable = expression [, ...]  
```  
  
## <a name="parts"></a>요소  
  
|용어|정의|  
|---|---|  
|`variable`|필수. 제공 된 식의 결과를 참조 하는 데 사용할 수 있는 별칭입니다.|  
|`expression`|필수. 지정 된 변수에 계산 되어 할당 되는 식입니다.|  
  
## <a name="remarks"></a>설명  
 @No__t-0 절을 사용 하면 각 쿼리 결과에 대 한 값을 계산 하 고 별칭을 사용 하 여 참조할 수 있습니다. 별칭은 `Where` 절과 같은 다른 절에서 사용할 수 있습니다. @No__t-0 절을 사용 하면 쿼리에 포함 된 식 절에 별칭을 지정 하 고 expression 절이 사용 될 때마다 별칭을 대체할 수 있기 때문에 더 쉽게 읽을 수 있는 쿼리 문을 만들 수 있습니다.  
  
 @No__t-2 절에는 임의 개수의 `variable` 및 `expression` 할당을 포함할 수 있습니다. 각 할당을 쉼표 (,)로 구분 합니다.  
  
## <a name="example"></a>예제  
 다음 코드 예에서는 `Let` 절을 사용 하 여 제품에 대해 10% 할인을 계산 합니다.  
  
 [!code-vb[VbSimpleQuerySamples#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#16)]  
  
## <a name="see-also"></a>참조

- [Visual Basic의 LINQ 소개](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)
- [쿼리](../../../visual-basic/language-reference/queries/index.md)
- [Select 절](../../../visual-basic/language-reference/queries/select-clause.md)
- [From 절](../../../visual-basic/language-reference/queries/from-clause.md)
- [Where 절](../../../visual-basic/language-reference/queries/where-clause.md)
