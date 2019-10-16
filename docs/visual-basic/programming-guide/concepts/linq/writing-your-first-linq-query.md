---
title: LINQ 쿼리 처음 작성(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- queries [LINQ in Visual Basic], writing
- LINQ queries [Visual Basic]
- LINQ [Visual Basic], writing queries
ms.assetid: 4affb732-3e9b-4479-aa31-1f9bd8183cbe
ms.openlocfilehash: 5c83d888f65ce5c216327e94c5d4d1267fb93c29
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69952006"
---
# <a name="writing-your-first-linq-query-visual-basic"></a>LINQ 쿼리 처음 작성(Visual Basic)
*쿼리*는 데이터 소스에서 데이터를 검색하는 식입니다. 쿼리는 전용 쿼리 언어로 표현 됩니다. 시간이 지남에 따라 다양 한 유형의 데이터 원본에 대해 다양 한 언어 (예: 관계형 데이터베이스의 경우 SQL, XML 용 XQuery)가 개발 되었습니다. 이를 통해 응용 프로그램 개발자는 지원 되는 데이터 원본 또는 데이터 형식에 따라 새로운 쿼리 언어를 배워야 합니다.  
  
 [!INCLUDE[vbteclinqext](~/includes/vbteclinqext-md.md)]에서는 다양 한 종류의 데이터 원본 및 형식에서 데이터를 사용 하기 위한 일관 된 모델을 제공 하 여 상황을 단순화 합니다. [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리에서는 항상 개체를 사용하고 있습니다. 동일한 기본 코딩 패턴을 사용 하 여 XML 문서, SQL 데이터베이스, ADO.NET 데이터 집합 및 엔터티, .NET Framework 컬렉션 및 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 공급자를 사용할 수 있는 다른 모든 원본 또는 형식에서 데이터를 쿼리하고 변환 합니다. 이 문서에서는 기본 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리를 만들고 사용 하는 세 단계에 대해 설명 합니다.  
  
## <a name="three-stages-of-a-query-operation"></a>쿼리 작업의 세 단계  
 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)]쿼리 작업은 다음과 같은 세 가지 작업으로 구성 됩니다.  
  
1. 데이터 소스를 가져옵니다.  
  
2. 쿼리 만들기.  
  
3. 쿼리 실행.  
  
 에서 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)]쿼리 실행은 쿼리를 만드는 것과는 다릅니다. 쿼리를 만들어 데이터를 검색 하지 않습니다. 이 내용에 대해서는 이 항목의 뒷부분에서 자세히 설명합니다.  
  
 다음 예에서는 쿼리 작업의 세 부분을 보여 줍니다. 예제에서는 데모를 위해 정수 배열을 편리한 데이터 소스로 사용 합니다. 그러나 다른 데이터 소스에도 동일한 개념이 적용 됩니다.  
  
> [!NOTE]
> [컴파일 페이지, 프로젝트 디자이너 (Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic)에서 **옵션 유추** 가 **On**으로 설정 되어 있는지 확인 합니다.  
  
 [!code-vb[VbLINQFirstQuery#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQFirstQuery/VB/Class1.vb#1)]  
  
 출력:  
  
 `0 2 4 6`  
  
## <a name="the-data-source"></a>데이터 소스  
 이전 예제의 데이터 소스는 배열 이기 때문에 제네릭 <xref:System.Collections.Generic.IEnumerable%601> 인터페이스를 암시적으로 지원 합니다. 이 사실은 배열을 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리의 데이터 원본으로 사용할 수 있도록 하는 것입니다. <xref:System.Collections.Generic.IEnumerable%601> 또는 제네릭 <xref:System.Linq.IQueryable%601> 같은 파생된 인터페이스를 지원하는 형식을 *쿼리 가능 형식*이라고 합니다.  
  
 암시적으로 쿼리 가능한 형식으로 배열에는 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 데이터 원본으로 사용할 수정 또는 특별 한 처리가 필요 하지 않습니다. .NET Framework 클래스 라이브러리의 제네릭 <xref:System.Collections.Generic.IEnumerable%601> <xref:System.Collections.Generic.List%601>, <xref:System.Collections.Generic.Dictionary%602>및 기타 클래스를 포함 하 여를 지 원하는 모든 컬렉션 형식의 경우에도 마찬가지입니다.  
  
 원본 데이터가 아직 구현 <xref:System.Collections.Generic.IEnumerable%601>되지 않은 경우 공급자는 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 해당 데이터 원본에 대 한 *표준 쿼리 연산자* 의 기능을 구현 해야 합니다. 예 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 를 들어은 다음 예제와 같이 쿼리 <xref:System.Xml.Linq.XElement> 가능한 형식으로 XML 문서를 로드 하는 작업을 처리 합니다. 표준 쿼리 연산자에 대 한 자세한 내용은 [표준 쿼리 연산자 개요 (Visual Basic)](standard-query-operators-overview.md)를 참조 하세요.  
  
 [!code-vb[VbLINQFirstQuery#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQFirstQuery/VB/Class1.vb#2)]  
  
 를 [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)]사용 하면 디자인 타임에 수동으로 또는 visual studio의 [visual studio에서 LINQ to SQL 도구](/visualstudio/data-tools/linq-to-sql-tools-in-visual-studio2) 를 사용 하 여 개체 관계형 매핑을 만들 수 있습니다. 개체에 대해 쿼리를 작성하면 런타임에 [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)]에서 데이터베이스와의 통신을 처리합니다. 다음 예에서는가 `customers` 데이터베이스 <xref:System.Data.Linq.Table%601> 의 특정 테이블을 나타내며 제네릭을 <xref:System.Linq.IQueryable%601>지원 합니다.  
  
```vb  
' Create a data source from a SQL table.  
Dim db As New DataContext("C:\Northwind\Northwnd.mdf")  
Dim customers As Table(Of Customer) = db.GetTable(Of Customer)  
```  
  
 특정 형식의 데이터 소스를 만드는 방법에 대한 자세한 내용은 다양한 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 공급자에 대한 설명서를 참조하세요. 이러한 공급자 목록은 [LINQ (통합 언어 쿼리)](../../../../visual-basic/programming-guide/concepts/linq/index.md)를 참조 하세요. 기본 규칙은 단순 합니다. [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 즉, 데이터 소스는 제네릭 <xref:System.Collections.Generic.IEnumerable%601> 인터페이스 또는이 인터페이스에서 상속 된 인터페이스를 지 원하는 개체입니다.  
  
> [!NOTE]
> 제네릭이 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] <xref:System.Collections.ArrayList> 아닌인터페이스를지원하는등의형식을데이터소스로사용할수도있습니다.<xref:System.Collections.IEnumerable> 을 사용 <xref:System.Collections.ArrayList>하는 예제를 보려면 [방법: LINQ (Visual Basic)](how-to-query-an-arraylist-with-linq.md)를 사용 하 여 ArrayList를 쿼리 합니다.  
  
## <a name="the-query"></a>쿼리  
 쿼리에서 데이터 원본에서 검색 하려는 정보를 지정 합니다. 또한 정보를 반환 하기 전에 정보를 정렬 하거나 그룹화 하거나 구조화 하는 방법을 지정할 수 있습니다. 쿼리 생성을 사용 하도록 설정 하기 위해 Visual Basic 새 쿼리 구문을 언어로 통합 했습니다.  
  
 실행 될 때 다음 예제의 쿼리는 정수 배열에서 모든 짝수를 `numbers`반환 합니다.  
  
 [!code-vb[VbLINQFirstQuery#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQFirstQuery/VB/Class1.vb#1)]  
  
 쿼리 식에는 `From`, 및 `Select`라는 세 `Where`개의 절이 포함 되어 있습니다. 각 쿼리 식 절의 특정 함수 및 용도는 [기본 쿼리 작업 (Visual Basic)](basic-query-operations.md)에서 설명 합니다. 자세한 내용은 [쿼리](../../../../visual-basic/language-reference/queries/index.md)를 참조 하세요. 에서 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)]쿼리 정의는 종종 변수에 저장 되 고 나중에 실행 됩니다. 이전 예제와 `evensQuery` 같은 쿼리 변수는 쿼리 가능한 형식 이어야 합니다. `evensQuery` 의`IEnumerable(Of Integer)`형식은 로컬 형식 유추를 사용 하 여 컴파일러에서 할당 된입니다.  
  
 쿼리 변수 자체는 아무 작업도 수행 하지 않으며 데이터를 반환 하지 않는다는 점을 기억해 야 합니다. 쿼리 정의만 저장 합니다. 이전 예제 `For Each` 에서는 쿼리를 실행 하는 루프입니다.  
  
## <a name="query-execution"></a>쿼리 실행  
 쿼리 실행은 쿼리 생성과는 별개입니다. 쿼리를 만들 때 쿼리를 정의 하지만 실행은 다른 메커니즘에 의해 트리거됩니다. 쿼리를 정의 하는 즉시 실행 하거나 (*즉시 실행*) 정의를 저장 하 고 나중에 쿼리를 실행할 수 있습니다 (*지연 된 실행*).  
  
### <a name="deferred-execution"></a>지연된 실행  
 일반적인 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리는 `evensQuery` 가 정의 된 이전 예제와 유사 합니다. 쿼리를 만들지만 즉시 실행 하지는 않습니다. 대신 쿼리 정의는 쿼리 변수에 `evensQuery`저장 됩니다. 나중에 쿼리를 실행 합니다. 일반적으로는 `For Each` 루프를 사용 하 여 값의 시퀀스를 반환 하거나 또는 `Max`와 `Count` 같은 표준 쿼리 연산자를 적용 하 여 쿼리를 실행 합니다. 이 프로세스를 *지연 된 실행*이라고 합니다.  
  
 [!code-vb[VbLINQFirstQuery#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQFirstQuery/VB/Class1.vb#7)]  
  
 값 시퀀스의 경우 `For Each` 루프의 반복 변수 (`number` 이전 예제에서는)를 사용 하 여 검색 된 데이터에 액세스 합니다. 쿼리 변수 `evensQuery`는 쿼리 결과가 아닌 쿼리 정의를 포함 하기 때문에 쿼리 변수를 두 번 이상 사용 하 여 쿼리 변수를 원하는 만큼 자주 실행할 수 있습니다. 예를 들어 응용 프로그램에 별도의 응용 프로그램에서 지속적으로 업데이트 되는 데이터베이스가 있을 수 있습니다. 해당 데이터베이스에서 데이터를 검색 하는 쿼리를 만든 후 `For Each` 루프를 사용 하 여 쿼리를 반복적으로 실행 하 여 매번 최신 데이터를 검색할 수 있습니다.  
  
 다음 예에서는 지연 된 실행이 작동 하는 방법을 보여 줍니다. 이전 `evensQuery2` 예제와 같이가 정의 되 `For Each` 고 루프를 사용 하 여 실행 된 후에는 데이터 원본의 `numbers` 일부 요소가 변경 됩니다. 그런 다음 두 `For Each` 번째 루프가 `evensQuery2` 다시 실행 됩니다. 루프는 `For Each` 의 `numbers`새 값을 사용 하 여 쿼리를 다시 실행 하기 때문에 결과는 두 번째 시간 마다 다릅니다.  
  
 [!code-vb[VbLINQFirstQuery#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQFirstQuery/VB/Class1.vb#3)]  
  
 출력:  
  
 `Evens in original array:`  
  
 `0  2  4  6`  
  
 `Evens in changed array:`  
  
 `0  10  2  22  8`  
  
### <a name="immediate-execution"></a>즉시 실행  
 쿼리의 지연 된 실행에서 쿼리 정의는 나중에 실행 하기 위해 쿼리 변수에 저장 됩니다. 즉시 실행 시 쿼리는 정의 시 실행 됩니다. 쿼리 결과의 개별 요소에 액세스 해야 하는 메서드를 적용 하는 경우 실행이 트리거됩니다. 즉시 실행은 단일 값을 반환 하는 표준 쿼리 연산자 중 하나를 사용 하 여 강제로 적용 됩니다. `Count`예 를들면`Max`, ,및`First`입니다. `Average` 이러한 표준 쿼리 연산자는 단일 결과를 계산 하 고 반환 하기 위해 적용 되는 즉시 쿼리를 실행 합니다. 단일 값을 반환 하는 표준 쿼리 연산자에 대 한 자세한 내용은 [집계 작업](aggregation-operations.md), [요소 작업](element-operations.md)및 [수량자 작업](quantifier-operations.md)을 참조 하세요.  
  
 다음 쿼리는 정수 배열에서 짝수의 수를 반환 합니다. 쿼리 정의는 저장 `numEvens` 되지 않으며 단순 `Integer`합니다.  
  
 [!code-vb[VbLINQFirstQuery#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQFirstQuery/VB/Class1.vb#4)]  
  
 메서드를 `Aggregate` 사용 하 여 동일한 결과를 얻을 수 있습니다.  
  
 [!code-vb[VbLINQFirstQuery#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQFirstQuery/VB/Class1.vb#5)]  
  
 다음 코드에 표시 된 것 처럼 쿼리 (즉시) `ToList` 또는 `ToArray` 쿼리 변수 (지연)에 대해 또는 메서드를 호출 하 여 쿼리를 강제로 실행할 수도 있습니다.  
  
 [!code-vb[VbLINQFirstQuery#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQFirstQuery/VB/Class1.vb#6)]  
  
 앞의 예제 `evensQuery3` 에서는 쿼리 변수 이지만 `evensList` 은 목록이 고 `evensArray` 는 배열입니다.  
  
 즉시 `ToList` 실행 `ToArray` 을 강제 실행 하려면 또는를 사용 하 여 쿼리를 즉시 실행 하 고 결과를 단일 컬렉션 개체에 캐시 하려는 시나리오에서 특히 유용 합니다. 이러한 메서드에 대 한 자세한 내용은 [데이터 형식 변환](converting-data-types.md)을 참조 하세요.  
  
 메서드와<xref:Microsoft.VisualBasic.Collection.System%23Collections%23IEnumerable%23GetEnumerator%2A> 같은 `IEnumerable` 메서드를 사용 하 여 쿼리를 실행할 수도 있습니다.  
  
## <a name="see-also"></a>참고자료

- [Visual Basic에서 LINQ 시작](getting-started-with-linq.md)
- [지역 형식 유추](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)
- [표준 쿼리 연산자 개요(Visual Basic)](standard-query-operators-overview.md)
- [Visual Basic의 LINQ 소개](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)
- [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)
- [쿼리](../../../../visual-basic/language-reference/queries/index.md)
