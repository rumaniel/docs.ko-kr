---
title: '방법: 조인 (Visual Basic)를 사용 하 여 데이터와 LINQ 결합'
ms.date: 07/20/2015
helpviewer_keywords:
- queries [LINQ in Visual Basic], joins
- joins [LINQ in Visual Basic]
- Join clause [LINQ in Visual Basic]
- Group Join clause [Visual Basic]
- joining [LINQ in Visual Basic]
- queries [LINQ in Visual Basic], how-to topics
ms.assetid: 5b00a478-035b-41c6-8918-be1a97728396
ms.openlocfilehash: 127e1afa7707f31584e93f3d4b08e865d7fcedf6
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61775884"
---
# <a name="how-to-combine-data-with-linq-by-using-joins-visual-basic"></a>방법: 조인 (Visual Basic)를 사용 하 여 데이터와 LINQ 결합
Visual Basic에서 제공 합니다 `Join` 고 `Group Join` 쿼리 절을 사용 하면 컬렉션 간의 공통 값을 기반으로 하는 여러 컬렉션의 콘텐츠를 결합할 수 있습니다. 이러한 값 이라고 *키* 값입니다. 관계형 데이터베이스 개념에 익숙한 개발자는 `Join` INNER JOIN으로 절 및 `Group Join` 으로 효과적으로 LEFT OUTER JOIN 절.  
  
 이 항목의 예제를 사용 하 여 데이터를 결합 하는 몇 가지 방법을 설명 합니다 `Join` 및 `Group Join` 쿼리 절.  
  
## <a name="create-a-project-and-add-sample-data"></a>프로젝트를 만들고 샘플 데이터 추가  
  
#### <a name="to-create-a-project-that-contains-sample-data-and-types"></a>샘플 데이터 및 유형을 포함 하는 프로젝트를 만들려면  
  
1. 이 항목의 샘플을 실행 하려면 Visual Studio를 열고 새 Visual Basic 콘솔 응용 프로그램 프로젝트를 추가 합니다. Visual Basic에서 생성 된 Module1.vb 파일을 두 번 클릭 합니다.  
  
2. 이 항목에서는 사용 샘플은 `Person` 및 `Pet` 유형 및 다음 코드 예제에서 데이터입니다. 이 코드는 기본 복사 `Module1` Visual Basic에서 생성 하는 모듈입니다.  
  
     [!code-vb[VbLINQHowTos#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQHowTos/VB/Module1.vb#1)]  
    [!code-vb[VbLINQHowTos#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQHowTos/VB/Module1.vb#2)]  
  
## <a name="perform-an-inner-join-by-using-the-join-clause"></a>Join 절을 사용 하 여 내부 조인 수행  
 INNER JOIN 두 컬렉션에서 데이터를 결합합니다. 지정된 된 키 값과 일치 하는 항목이 포함 됩니다. 다른 컬렉션에 일치 하는 항목이 없는 두 컬렉션에서 모든 항목은 제외 됩니다.  
  
 Visual Basic의 LINQ 내부 조인을 수행 하는 것에 대 한 두 가지 옵션을 제공 합니다: 암시적 조인 및 명시적 조인을 합니다.  
  
 암시적 조인을 지정 조인할 컬렉션을 `From` 절에서 일치 하는 키 필드를 식별 하 고는 `Where` 절. Visual Basic에는 암시적으로 지정 된 키 필드를 기반으로 두 컬렉션 조인 합니다.  
  
 명시적 조인을 사용 하 여 지정할 수 있습니다는 `Join` 절에 조인에 사용 하는 키 필드에 대 한 정확 하 게 하려는 경우. 이 경우에 `Where` 절을 사용 하 여 쿼리 결과 필터링 할 수 있습니다.  
  
#### <a name="to-perform-an-inner-join-by-using-the-join-clause"></a>Join 절을 사용 하 여 Inner Join을 수행 하려면  
  
1. 다음 코드를 추가 합니다 `Module1` 모두 암시적 및 명시적 내부 조인 예제를 볼 프로젝트에서 모듈입니다.  
  
     [!code-vb[VbLINQHowTos#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQHowTos/VB/Module1.vb#4)]  
  
## <a name="perform-a-left-outer-join-by-using-the-group-join-clause"></a>Group Join 절을 사용 하 여 왼쪽된 우선 외부 조인 수행  
 LEFT OUTER JOIN 조인 및 값 조인의 오른쪽에 있는 컬렉션에서 일치 하는 왼쪽 컬렉션에서 모든 항목을 포함 합니다. 왼쪽 컬렉션의 일치 하는 항목이 없는 조인의 오른쪽에 있는 컬렉션에서 모든 항목은 쿼리 결과에서 제외 됩니다.  
  
 `Group Join` 절 수행, 실제로 LEFT OUTER JOIN입니다. 일반적으로 라고 LEFT OUTER JOIN 및 간의 차이 `Group Join` 절은 반환는 `Group Join` 왼쪽 컬렉션의 각 항목에 대 한 조인의 오른쪽에 있는 컬렉션에서 절 그룹 결과. 관계형 데이터베이스, LEFT OUTER JOIN 조인에 두 컬렉션에서 일치 하는 항목을 포함 하는 쿼리의 각 항목에는 결과 그룹화 되지 않은 결과 반환 합니다. 이 경우 조인 왼쪽 컬렉션의 항목 오른쪽에 있는 컬렉션에서 일치 하는 각 항목에 대해 반복 됩니다. 이 내용을 다음 절차를 완료 하는 것이 나타납니다.  
  
 결과 검색할 수는 `Group Join` 각 그룹화 된 쿼리 결과 대 한 항목을 반환 하려면 쿼리를 확장 하 여 그룹화 되지 않은 결과 쿼리 합니다. 이렇게 하려면에서 쿼리를 확인 해야 합니다 `DefaultIfEmpty` 그룹화 된 컬렉션의 메서드. 이렇게 하면 있다면 오른쪽 컬렉션에서 일치 하는 아무 것도 조인의 왼쪽 컬렉션의 항목이 쿼리 결과에 포함 계속 됩니다. 조인의 오른쪽에 있는 컬렉션에서 일치 하는 값이 없을 때 기본 결과 값을 제공 하 여 쿼리 코드를 추가할 수 있습니다.  
  
#### <a name="to-perform-a-left-outer-join-by-using-the-group-join-clause"></a>Group Join 절을 사용 하 여 Left Outer Join을 수행 하려면  
  
1. 다음 코드를 추가 합니다 `Module1` 그룹화 된 왼쪽된 외부 조인 및 그룹화 되지 않은 왼쪽된 외부 조인을 둘 다의 예제를 보려면 프로젝트에서 모듈입니다.  
  
     [!code-vb[VbLINQHowTos#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQHowTos/VB/Module1.vb#3)]  
  
## <a name="perform-a-join-by-using-a-composite-key"></a>복합 키를 사용 하 여 조인 수행  
 사용할 수는 `And` 키워드를 `Join` 또는 `Group Join` 조인 중인 컬렉션에서 일치 시킬 때 사용 하는 여러 키 필드를 식별 하는 절 값입니다. `And` 키워드 지정는 모든 조인할 수는 항목에 대 한 키 필드와 일치 해야 합니다.  
  
#### <a name="to-perform-a-join-by-using-a-composite-key"></a>복합 키를 사용 하 여 조인 수행  
  
1. 다음 코드를 추가 합니다 `Module1` 의 복합 키를 사용 하는 조인 예제를 보려면 프로젝트에서 모듈입니다.  
  
     [!code-vb[VbLINQHowTos#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQHowTos/VB/Module1.vb#5)]  
  
## <a name="run-the-code"></a>코드를 실행 합니다.  
  
#### <a name="to-add-code-to-run-the-examples"></a>예제를 실행 하는 코드를 추가 하려면  
  
1. 대체는 `Sub Main` 에 `Module1` 이 항목의 예제를 실행 하려면 다음 코드를 사용 하 여 프로젝트에서 모듈입니다.  
  
     [!code-vb[VbLINQHowTos#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQHowTos/VB/Module1.vb#6)]  
  
2. F5 키를 눌러 예제를 실행 합니다.  
  
## <a name="see-also"></a>참고자료

- [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)
- [Visual Basic의 LINQ 소개](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)
- [Join 절](../../../../visual-basic/language-reference/queries/join-clause.md)
- [Group Join 절](../../../../visual-basic/language-reference/queries/group-join-clause.md)
- [From 절](../../../../visual-basic/language-reference/queries/from-clause.md)
- [Where 절](../../../../visual-basic/language-reference/queries/where-clause.md)
- [쿼리](../../../../visual-basic/language-reference/queries/index.md)
- [LINQ를 통한 데이터 변환(C#)](../../../../csharp/programming-guide/concepts/linq/data-transformations-with-linq.md)
