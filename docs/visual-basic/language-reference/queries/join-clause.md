---
title: Join 절(Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.QueryJoinIn
- vb.QueryJoin
- vb.QueryJoinOn
helpviewer_keywords:
- queries [Visual Basic], Join
- Join statement [Visual Basic]
- Join clause [Visual Basic]
ms.assetid: 6dd37936-b27c-4e00-98ad-154b23f4de64
ms.openlocfilehash: 8eab7db00515f55b086b5e1beddd149f966cb27a
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72001928"
---
# <a name="join-clause-visual-basic"></a>Join 절(Visual Basic)
두 컬렉션을 단일 컬렉션으로 결합합니다. 조인 작업은 일치 하는 키를 기반으로 하며 `Equals` 연산자를 사용 합니다.  
  
## <a name="syntax"></a>구문  
  
```vb  
Join element In collection _  
  [ joinClause _ ]   
  [ groupJoinClause ... _ ]   
On key1 Equals key2 [ And key3 Equals key4 [... ]  
```  
  
## <a name="parts"></a>요소  
 `element`  
 필수. 조인 되는 컬렉션에 대 한 제어 변수입니다.  
  
 `collection`  
 필수. @No__t-0 연산자의 왼쪽에서 식별 된 컬렉션과 결합할 컬렉션입니다. @No__t-0 절은 다른 `Join` 절 또는 `Group Join` 절에 중첩 될 수 있습니다.  
  
 `joinClause`  
 (선택 사항) 쿼리를 구체화 하는 하나 이상의 추가 `Join` 절입니다.  
  
 `groupJoinClause`  
 (선택 사항) 쿼리를 구체화 하는 하나 이상의 추가 `Group Join` 절입니다.  
  
 `key1` `Equals` `key2`  
 필수. 조인 되는 컬렉션의 키를 식별 합니다. 조인 되는 컬렉션의 키를 비교 하려면 `Equals` 연산자를 사용 해야 합니다. @No__t-0 연산자를 사용 하 여 여러 키를 식별 하는 조인 조건을 결합할 수 있습니다. `key1`은 `Join` 연산자의 왼쪽에 있는 컬렉션에 있어야 합니다. `key2`은 `Join` 연산자의 오른쪽에 있는 컬렉션에 있어야 합니다.  
  
 조인 조건에 사용 되는 키는 컬렉션에서 두 개 이상의 항목을 포함 하는 식일 수 있습니다. 그러나 각 키 식에는 해당 컬렉션의 항목만 포함할 수 있습니다.  
  
## <a name="remarks"></a>설명  
 @No__t-0 절은 조인 중인 컬렉션에서 일치 하는 키 값을 기준으로 두 개의 컬렉션을 결합 합니다. 결과 컬렉션은 `Join` 연산자의 왼쪽에서 식별 된 컬렉션의 모든 값 조합 및 `Join` 절에서 식별 된 컬렉션을 포함할 수 있습니다. 이 쿼리는 `Equals` 연산자로 지정 된 조건이 충족 되는 결과만 반환 합니다. 이는 SQL의 `INNER JOIN`과 동일 합니다.  
  
 쿼리에서 여러 `Join` 절을 사용 하 여 둘 이상의 컬렉션을 단일 컬렉션으로 조인할 수 있습니다.  
  
 @No__t-0 절이 없으면 암시적 조인을 수행 하 여 컬렉션을 결합할 수 있습니다. 이렇게 하려면 `From` 절에 여러 `In` 절을 포함 하 고 조인에 사용할 키를 식별 하는 `Where` 절을 지정 합니다.  
  
 @No__t-0 절을 사용 하 여 컬렉션을 단일 계층 구조 컬렉션으로 결합할 수 있습니다. 이는 SQL의 `LEFT OUTER JOIN`과 비슷합니다.  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 암시적 조인을 수행 하 여 고객 목록을 주문과 결합 합니다.  
  
 [!code-vb[VbSimpleQuerySamples#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#13)]  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 `Join` 절을 사용 하 여 두 컬렉션을 조인 합니다.  
  
 [!code-vb[VbSimpleQuerySamples#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples2.vb#12)]  
  
 이 예제는 다음과 유사한 출력을 생성 합니다.  
  
 `winlogon (968), Windows Logon`  
  
 `explorer (2424), File Explorer`  
  
 `cmd (5136), Command Window`  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 두 개의 키 열이 있는 `Join` 절을 사용 하 여 두 컬렉션을 조인 합니다.  
  
 [!code-vb[VbSimpleQuerySamples#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples3.vb#17)]  
  
 예제는 다음과 유사한 출력을 생성 합니다.  
  
 `winlogon (968), Windows Logon, Priority = 13`  
  
 `cmd (700), Command Window, Priority = 8`  
  
 `explorer (2424), File Explorer, Priority = 8`  
  
## <a name="see-also"></a>참조

- [Visual Basic의 LINQ 소개](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)
- [쿼리](../../../visual-basic/language-reference/queries/index.md)
- [Select 절](../../../visual-basic/language-reference/queries/select-clause.md)
- [From 절](../../../visual-basic/language-reference/queries/from-clause.md)
- [Group Join 절](../../../visual-basic/language-reference/queries/group-join-clause.md)
- [Where 절](../../../visual-basic/language-reference/queries/where-clause.md)
