---
title: 쿼리 작업의 형식 관계(Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- variable relationships [LINQ in Visual Basic]
- type information inferred [LINQ in Visual Basic]
- type relationships [LINQ in Visual Basic]
- queries [LINQ in Visual Basic], type relationships
- data sources [LINQ in Visual Basic], type relationships
- LINQ [Visual Basic], type relationships
- inferring type information [LINQ in Visual Basic]
- relationships [LINQ in Visual Basic]
ms.assetid: b5ff4da5-f3fd-4a8e-aaac-1cbf52fa16f6
ms.openlocfilehash: 4851d0a74de38f0fb6b6deee34cf7b3e66eb11b4
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69937488"
---
# <a name="type-relationships-in-query-operations-visual-basic"></a>쿼리 작업의 형식 관계(Visual Basic)
쿼리 작업에 [!INCLUDE[vbteclinqext](~/includes/vbteclinqext-md.md)] 사용 되는 변수는 강력 하 게 형식화 되며 서로 호환 되어야 합니다. 강력한 형식 지정은 데이터 소스, 쿼리 자체 및 쿼리 실행에서 사용 됩니다. 다음 그림은 쿼리를 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 설명 하는 데 사용 되는 용어를 나타냅니다. 쿼리 파트에 대 한 자세한 내용은 [기본 쿼리 작업 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/basic-query-operations.md)을 참조 하세요.  
  
 ![요소가 강조 표시 된 의사 코드 쿼리를 보여 주는 스크린샷](./media/type-relationships-in-query-operations/linq-query-description-terms.png)  
  
 쿼리의 범위 변수 형식은 데이터 소스에 있는 요소의 형식과 호환 되어야 합니다. 쿼리 변수의 형식은 `Select` 절에 정의 된 sequence 요소와 호환 되어야 합니다. 마지막으로 시퀀스 요소의 형식은 쿼리를 실행 하는 `For Each` 문에 사용 되는 루프 제어 변수의 형식과도 호환 되어야 합니다. 이 강력한 형식화는 컴파일 시간에 형식 오류의 식별을 용이 하 게 합니다.  
  
 Visual Basic는 *암시적*형식이 라고도 하는 로컬 형식 유추를 구현 하 여 강력한 형식화를 편리 하 게 만듭니다. 이전 예제에서이 기능을 사용 하 고 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 샘플 및 설명서 전체에서이 기능을 사용 하는 것을 볼 수 있습니다. Visual Basic에서는 `Dim` `As` 절이 없는 문을 사용 하 여 로컬 형식 유추를 간단히 수행 합니다. 다음 예제에서는 문자열로 `city` 강력 하 게 형식화 됩니다.  
  
 [!code-vb[VbLINQTypeRels#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQTypeRels/VB/Class1.vb#1)]  
  
> [!NOTE]
> 로컬 형식 유추는가로 `Option Infer` 설정 된 경우 `On`에만 작동 합니다. 자세한 내용은 [Option 유추 문](../../../../visual-basic/language-reference/statements/option-infer-statement.md)을 참조 하세요.  
  
 그러나 쿼리에서 로컬 형식 유추를 사용 하는 경우에도 데이터 원본의 변수, 쿼리 변수 및 쿼리 실행 루프 사이에 동일한 형식 관계가 있습니다. 쿼리를 작성 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 하거나 설명서의 샘플 및 코드 예제를 사용 하는 경우 이러한 형식 관계를 기본적으로 이해 하는 것이 유용 합니다.  
  
 데이터 원본에서 반환 되는 형식과 일치 하지 않는 범위 변수에 대 한 명시적 형식을 지정 해야 할 수도 있습니다. `As` 절을 사용 하 여 범위 변수의 형식을 지정할 수 있습니다. 그러나 변환이 [축소 변환](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md) 되 고 `Option Strict` 가로 `On`설정 된 경우이로 인해 오류가 발생 합니다. 따라서 데이터 원본에서 검색 된 값에 대해 변환을 수행 하는 것이 좋습니다. 메서드를 <xref:System.Linq.Enumerable.Cast%2A> 사용 하 여 데이터 소스의 값을 명시적 범위 변수 형식으로 변환할 수 있습니다. 또한 `Select` 절에서 선택한 값을 범위 변수의 형식과 다른 명시적 형식으로 캐스팅할 수도 있습니다. 이러한 요소는 다음 코드에 나와 있습니다.  
  
 [!code-vb[VbLINQTypeRels#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQTypeRels/VB/Class1.vb#4)]  
  
## <a name="queries-that-return-entire-elements-of-the-source-data"></a>원본 데이터의 전체 요소를 반환 하는 쿼리  
 다음 예에서는 원본 데이터 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 에서 선택한 요소의 시퀀스를 반환 하는 쿼리 작업을 보여 줍니다. 원본 `names`에는 문자열 배열이 포함 되 고 쿼리 출력은 문자 M으로 시작 하는 문자열을 포함 하는 시퀀스입니다.  
  
 [!code-vb[VbLINQTypeRels#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQTypeRels/VB/Class1.vb#2)]  
  
 이는 다음 코드와 동일 하지만 훨씬 짧고 더 쉽게 작성할 수 있습니다. 쿼리에서의 로컬 형식 유추에 의존 하는 것은 Visual Basic에서 선호 되는 스타일입니다.  
  
 [!code-vb[VbLINQTypeRels#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQTypeRels/VB/Class1.vb#3)]  
  
 형식이 암시적 또는 명시적으로 결정 되는지에 관계 없이 앞의 코드 예제에는 다음 관계가 모두 있습니다.  
  
1. 데이터 소스 `names`에 있는 요소의 형식 ()은 쿼리에서 범위 `name`변수의 형식입니다.  
  
2. 선택 `name`된 개체의 형식으로, 쿼리 `mNames`변수의 형식을 결정 합니다. 다음 `name` 은 문자열 이므로 쿼리 변수는 Visual Basic의 IEnumerable (문자열)입니다.  
  
3. 에서 `mNames` 정의 된 쿼리는 `For Each` 루프에서 실행 됩니다. 루프는 쿼리를 실행 한 결과를 반복 합니다. 실행 되는 경우는 문자열 시퀀스를 반환 하 고 루프 반복 `nm`변수인도 문자열입니다. `mNames`  
  
## <a name="queries-that-return-one-field-from-selected-elements"></a>선택한 요소에서 한 필드를 반환 하는 쿼리  
 다음 예에서는 데이터 소스 [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] 에서 선택한 각 요소의 한 부분만 포함 된 시퀀스를 반환 하는 쿼리 작업을 보여 줍니다. 이 쿼리는 개체의 `Customer` 컬렉션을 데이터 원본으로 사용 하 고 결과의 속성만 프로젝션 `Name` 합니다. 고객 이름이 문자열 이기 때문에 쿼리는 문자열 시퀀스를 출력으로 생성 합니다.  
  
```vb  
' Method GetTable returns a table of Customer objects.  
Dim customers = db.GetTable(Of Customer)()  
Dim custNames = From cust In customers   
                Where cust.City = "London"   
                Select cust.Name  
  
For Each custName In custNames  
    Console.WriteLine(custName)  
Next  
```  
  
 변수 간의 관계는 간단한 예제와 유사 합니다.  
  
1. 데이터 소스 `customers`에 있는 요소의 형식 ()은 쿼리에서 범위 `cust`변수의 형식입니다. 이 예제에서 해당 형식은 `Customer`입니다.  
  
2. 문은 전체 개체 대신 `Name` 각 `Customer` 개체의 속성을 반환 합니다. `Select` 가 `Name` 문자열 이기 때문에 쿼리 `custNames`변수는가 아닌 IEnumerable ( `Customer`문자열)입니다.  
  
3. 는 문자열 시퀀스를 `For Each` `custName`나타내므로루프의 반복 변수는 문자열 이어야 합니다. `custNames`  
  
 로컬 형식 유추가 없으면 다음 예제와 같이 앞의 예제를 작성 하 고 이해 하기가 더 복잡 합니다.  
  
```vb  
' Method GetTable returns a table of Customer objects.  
 Dim customers As Table(Of Customer) = db.GetTable(Of Customer)()  
 Dim custNames As IEnumerable(Of String) =  
     From cust As Customer In customers   
     Where cust.City = "London"   
     Select cust.Name  
  
 For Each custName As String In custNames  
     Console.WriteLine(custName)  
 Next  
```  
  
## <a name="queries-that-require-anonymous-types"></a>익명 형식이 필요한 쿼리  
 다음 예제에서는 좀 더 복잡 한 상황을 보여 줍니다. 이전 예제에서는 모든 변수에 대해 명시적으로 형식을 지정 하는 것이 불편할 수 있었습니다. 이 예에서는 불가능 합니다. 이 쿼리의 절은 `Customer` `Select` 데이터 소스에서 전체 요소를 선택 하는 대신 또는 각 요소의 단일 필드를 선택 하는 대신 원래 `Customer` 개체인 `Name` 및 `City`의 두 속성을 반환 합니다. `Select` 절에 대 한 응답으로 컴파일러는 이러한 두 속성을 포함 하는 익명 형식을 정의 합니다. 루프에서를 실행 `nameCityQuery` 한 결과는 새 익명 형식의 인스턴스 컬렉션입니다. `For Each` 익명 형식에는 사용할 수 있는 이름이 없으므로 또는 `nameCityQuery` `custInfo` 의 형식을 명시적으로 지정할 수 없습니다. 즉, 무명 형식의 경우 `String` 에서 `IEnumerable(Of String)`대신 사용할 형식 이름이 없습니다. 자세한 내용은 [무명 형식](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)을 참조하세요.  
  
```vb  
' Method GetTable returns a table of Customer objects.  
Dim customers = db.GetTable(Of Customer)()  
Dim nameCityQuery = From cust In customers   
                    Where cust.City = "London"   
                    Select cust.Name, cust.City  
  
For Each custInfo In nameCityQuery  
    Console.WriteLine(custInfo.Name)  
Next  
```  
  
 이전 예제에서 모든 변수에 대 한 형식을 지정 하려면 가능한 경우에 관계 ֿ ´.  
  
1. 데이터 소스에 있는 요소의 형식이 다시 쿼리의 범위 변수 형식입니다. 이 예에서 `cust` 의 인스턴스가 `Customer`합니다.  
  
2. 이 문은 무명 형식을 생성 하므로 쿼리 `nameCityQuery`변수는 무명 형식으로 암시적으로 형식화 되어야 합니다. `Select` 익명 형식에는 사용할 수 있는 이름이 없으므로 명시적으로 지정할 수 없습니다.  
  
3. `For Each` 루프의 반복 변수 형식은 2 단계에서 만든 익명 형식입니다. 형식에 사용할 수 있는 이름이 없으므로 루프 반복 변수의 형식은 암시적으로 결정 되어야 합니다.  
  
## <a name="see-also"></a>참고자료

- [Visual Basic에서 LINQ 시작](../../../../visual-basic/programming-guide/concepts/linq/getting-started-with-linq.md)
- [익명 형식](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)
- [지역 형식 유추](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)
- [Visual Basic의 LINQ 소개](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)
- [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)
- [쿼리](../../../../visual-basic/language-reference/queries/index.md)
