---
title: 기본 쿼리 작업(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- data sources [LINQ in Visual Basic]
- Join clause [LINQ in Visual Basic]
- ordering data [LINQ in Visual Basic]
- projections [LINQ in Visual Basic]
- LINQ [Visual Basic], query operations
- Order By clause [LINQ in Visual Basic]
- joining data [LINQ in Visual Basic]
- queries [LINQ in Visual Basic], basic operations
- selecting data [LINQ in Visual Basic]
- Group By clause [LINQ in Visual Basic]
- grouping data [LINQ in Visual Basic]
- Select clause [LINQ in Visual Basic]
ms.assetid: 1146f6d0-fcb8-4f4d-8223-c9db52620d21
ms.openlocfilehash: 12f10f30dd767f3435044f2bbebe0eb865c29d0c
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69939374"
---
# <a name="basic-query-operations-visual-basic"></a>기본 쿼리 작업(Visual Basic)
이 항목에서는 Visual Basic의 [!INCLUDE[vbteclinqext](~/includes/vbteclinqext-md.md)] 식 및 쿼리에서 수행 하는 몇 가지 일반적인 작업 종류에 대 한 간략 한 소개를 제공 합니다. 자세한 내용은 다음 항목을 참조하세요.  
  
 [Visual Basic의 LINQ 소개](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)  
  
 [쿼리](../../../../visual-basic/language-reference/queries/index.md)  
  
 [연습: Visual Basic에서 쿼리 작성](../../../../visual-basic/programming-guide/concepts/linq/walkthrough-writing-queries.md)  
  
## <a name="specifying-the-data-source-from"></a>데이터 원본 지정 (원본)  
 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리에서 첫 번째 단계는 쿼리 하려는 데이터 원본을 지정 하는 것입니다. 따라서 쿼리의 절 `From` 은 항상 먼저 제공 됩니다. 쿼리 연산자 원본 유형에 따라 결과를 선택 하 고 모양을 합니다.  
  
 [!code-vb[VbLINQBasicOps#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#1)]  
  
 절 `From` 은 `customers`데이터 소스, 및 *범위 변수*를 `cust`지정 합니다. 범위 변수는 쿼리 식에서 실제 반복이 발생 하지 않는다는 점을 제외 하 고 루프 반복 변수와 유사 합니다. `For Each` 루프를 사용 하 여 쿼리를 실행할 때 범위 변수는의 `customers`각 연속 요소에 대 한 참조로 사용 됩니다. 컴파일러에서 `cust` 형식을 유추할 수 있으므로 명시적으로 지정할 필요가 없습니다. 명시적 형식 지정을 사용 하거나 사용 하지 않고 작성 된 쿼리의 예는 [쿼리 작업의 형식 관계 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/type-relationships-in-query-operations.md)를 참조 하세요.  
  
 Visual Basic에서 `From` 절을 사용 하는 방법에 대 한 자세한 내용은 [from 절](../../../../visual-basic/language-reference/queries/from-clause.md)을 참조 하세요.  
  
## <a name="filtering-data-where"></a>데이터 필터링 (Where)  
 가장 일반적인 쿼리 작업은 부울 식의 형태로 필터를 적용 하는 것입니다. 그런 다음이 쿼리는 식이 true 인 요소만 반환 합니다. 필터링을 수행 하는 데 절이사용됩니다.`Where` 필터는 결과 시퀀스에 포함할 데이터 소스의 요소를 지정 합니다. 다음 예에서는 런던에 주소가 있는 고객만 포함 되어 있습니다.  
  
 [!code-vb[VbLINQBasicOps#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#2)]  
  
 `Where` And `And` 와같은논리연산자를사용하여절에서필터식을결합할수있습니다.`Or` 예를 들어 London에서 이름이 Devon 인 고객만 반환 하려면 다음 코드를 사용 합니다.  
  
```vb  
Where cust.City = "London" And cust.Name = "Devon"   
```  
  
 런던 또는 파리에서 고객을 반환 하려면 다음 코드를 사용 합니다.  
  
```vb  
Where cust.City = "London" Or cust.City = "Paris"   
```  
  
 Visual Basic에서 `Where` 절을 사용 하는 방법에 대 한 자세한 내용은 [where 절](../../../../visual-basic/language-reference/queries/where-clause.md)을 참조 하세요.  
  
## <a name="ordering-data-order-by"></a>데이터 순서 지정 (Order By)  
 반환 된 데이터를 특정 순서로 정렬 하는 것이 편리한 경우가 많습니다. `Order By` 절을 지정 하면 반환 된 시퀀스의 요소가 지정 된 필드를 기준으로 정렬 됩니다. 예를 들어 다음 쿼리는 `Name` 속성을 기반으로 결과를 정렬 합니다. 는 `Name` 문자열 이므로 반환 된 데이터는 a에서 Z로 사전순으로 정렬 됩니다.  
  
 [!code-vb[VbLINQBasicOps#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#3)]  
  
 결과를 역순으로 정렬하려면 `Order By...Descending` 절을 사용합니다. 및 `Ascending` `Ascending` 를 모두 지정 하지 않을 경우 기본값은입니다. `Descending`  
  
 Visual Basic에서 `Order By` 절을 사용 하는 방법에 대 한 자세한 내용은 [order by 절](../../../../visual-basic/language-reference/queries/order-by-clause.md)을 참조 하십시오.  
  
## <a name="selecting-data-select"></a>데이터 선택 (Select)  
 절 `Select` 은 반환 된 요소의 형식 및 내용을 지정 합니다. 예를 들어 결과가 전체 `Customer` 개체, 하나의 `Customer` 속성, 속성의 하위 집합, 다양 한 데이터 원본의 속성 조합 또는 계산을 기반으로 하는 몇 가지 새로운 결과 형식으로 구성 될 지 여부를 지정할 수 있습니다. `Select` 절이 소스 요소의 복사본이 아닌 다른 항목을 생성하는 경우 이 작업을 *프로젝션*이라고 합니다.  
  
 전체 `Customer` 개체로 구성 된 컬렉션을 검색 하려면 범위 변수 자체를 선택 합니다.  
  
 [!code-vb[VbLINQBasicOps#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#4)]  
  
 인스턴스가 많은 필드가 포함 된 많은 개체이 고 검색 하려는 모든가 이름인 경우 다음 예제와 같이를 선택할 `cust.Name`수 있습니다. `Customer` 지역 형식 유추는이가 결과 형식을 `Customer` 개체 컬렉션에서 문자열 컬렉션으로 변경 하는 것을 인식 합니다.  
  
 [!code-vb[VbLINQBasicOps#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#5)]  
  
 데이터 원본에서 여러 필드를 선택 하기 위해 다음 두 가지 옵션을 선택할 수 있습니다.  
  
- `Select` 절에서 결과에 포함할 필드를 지정 합니다. 컴파일러는 해당 필드를 속성으로 포함 하는 익명 형식을 정의 합니다. 자세한 내용은 [무명 형식](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)을 참조하세요.  
  
     다음 예제의 반환 된 요소는 무명 형식의 인스턴스 이므로 코드의 다른 위치에서 이름을 기준으로 형식을 참조할 수 없습니다. 형식에 대 한 컴파일러 지정 이름에 일반 Visual Basic 코드에서 유효 하지 않은 문자가 포함 되어 있습니다. 다음 예제에서 쿼리에서 `londonCusts4` 반환 되는 컬렉션의 요소는 무명 형식의 인스턴스입니다.  
  
     [!code-vb[VbLINQBasicOps#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#6)]  
  
     또는  
  
- 결과에 포함 하려는 특정 필드를 포함 하는 명명 된 형식을 정의 하 고 `Select` 절에서 형식의 인스턴스를 만들고 초기화 합니다. 반환 된 컬렉션 외부에서 개별 결과를 사용 해야 하는 경우 또는 메서드 호출에서 매개 변수로 전달 해야 하는 경우에만이 옵션을 사용 합니다. 다음 예제에서 `londonCusts5` 의 형식은 IEnumerable (of NamePhone)입니다.  
  
     [!code-vb[VbLINQBasicOps#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#7)]  
  
     [!code-vb[VbLINQBasicOps#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#8)]  
  
 Visual Basic `Select` 절을 사용 하는 방법에 대 한 자세한 내용은 [select 절](../../../../visual-basic/language-reference/queries/select-clause.md)을 참조 하세요.  
  
## <a name="joining-data-join-and-group-join"></a>데이터 조인 (조인 및 그룹 조인)  
 여러 가지 방법으로 `From` 절에서 둘 이상의 데이터 소스를 결합할 수 있습니다. 예를 들어, 다음 코드는 두 개의 데이터 원본을 사용 하 고 결과에서 둘 다의 속성을 암시적으로 결합 합니다. 이 쿼리는 성이 모음으로 시작 하는 학생을 선택 합니다.  
  
 [!code-vb[VbLINQBasicOps#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#9)]  
  
> [!NOTE]
> 다음 [방법으로 만든 학생 목록을 사용 하 여이 코드를 실행할 수 있습니다. 항목](../../../../visual-basic/programming-guide/concepts/linq/how-to-create-a-list-of-items.md)목록을 만듭니다.  
  
 키워드 `Join` 는 SQL `INNER JOIN` 의와 동일 합니다. 두 컬렉션의 요소 사이에 일치 하는 키 값을 기준으로 두 컬렉션을 결합 합니다. 쿼리에서 일치 하는 키 값이 있는 컬렉션 요소의 전체 또는 일부를 반환 합니다. 예를 들어 다음 코드는 이전 암시적 조인의 작업을 복제 합니다.  
  
 [!code-vb[VbLINQBasicOps#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#10)]  
  
 `Group Join`SQL `LEFT JOIN` 의와 마찬가지로 컬렉션을 단일 계층 구조 컬렉션으로 결합 합니다. 자세한 내용은 [Join 절](../../../../visual-basic/language-reference/queries/join-clause.md) 및 [Group join 절](../../../../visual-basic/language-reference/queries/group-join-clause.md)을 참조 하세요.  
  
## <a name="grouping-data-group-by"></a>데이터 그룹화 (Group By)  
 요소에 있는 하나 `Group By` 이상의 필드에 따라 쿼리 결과의 요소를 그룹화 하는 절을 추가할 수 있습니다. 예를 들어, 다음 코드는 year를 기준으로 학생을 그룹화 합니다.  
  
 [!code-vb[VbLINQBasicOps#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#11)]  
  
 다음 [방법으로 만든 학생 목록을 사용 하 여이 코드를 실행 하는 경우 항목](../../../../visual-basic/programming-guide/concepts/linq/how-to-create-a-list-of-items.md)목록을 만듭니다. `For Each` 문의 출력은 다음과 같습니다.  
  
 연도가 Junior  
  
 Tucker, Michael  
  
 가르시아 섬, Hugo  
  
 가르시아 섬, Debra  
  
 Tucker, Lance  
  
 연도가 부장  
  
 Omelchenko, Svetlana  
  
 Osada, Michiko  
  
 Fakhouri, Fadi  
  
 Feng, 인 hanying  
  
 Adams, Terry  
  
 연도가 Freshman  
  
 Mortensen, Sven  
  
 가르시아 섬, Cesar  
  
 다음 코드에 표시 된 변형은 클래스 연도를 정렬 한 다음 각 연도 내에서 성을 기준으로 학생을 주문 합니다.  
  
 [!code-vb[VbLINQBasicOps#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#12)]  
  
 에 대 한 `Group By`자세한 내용은 [group by 절](../../../../visual-basic/language-reference/queries/group-by-clause.md)을 참조 하십시오.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Collections.Generic.IEnumerable%601>
- [Visual Basic에서 LINQ 시작](../../../../visual-basic/programming-guide/concepts/linq/getting-started-with-linq.md)
- [쿼리](../../../../visual-basic/language-reference/queries/index.md)
- [표준 쿼리 연산자 개요(Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)
- [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)
