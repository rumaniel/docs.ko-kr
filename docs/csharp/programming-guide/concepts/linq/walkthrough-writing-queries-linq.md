---
title: '연습: C#에서 쿼리 작성(LINQ)'
ms.date: 07/20/2015
helpviewer_keywords:
- LINQ [C#], walkthroughs
- LINQ [C#], writing queries
- queries [LINQ in C#], writing
- writing LINQ queries
ms.assetid: 2962a610-419a-4276-9ec8-4b7f2af0c081
ms.openlocfilehash: 9b6592405d3047c8663b48137aa5b1f0eb14bdb4
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69924102"
---
# <a name="walkthrough-writing-queries-in-c-linq"></a>연습: C#에서 쿼리 작성(LINQ)
이 연습에서는 LINQ 쿼리 식을 작성하는 데 사용되는 C # 언어 기능을 보여 줍니다.  
  
## <a name="create-a-c-project"></a>C# 프로젝트 만들기  
  
> [!NOTE]
> 다음 지침은 Visual Studio용입니다. 다른 개발 환경을 사용하는 경우 System.Core.dll에 대한 참조와 <xref:System.Linq?displayProperty=nameWithType> 네임스페이스에 대한 `using` 지시문을 사용하여 콘솔 프로젝트를 만듭니다.  
  
#### <a name="to-create-a-project-in-visual-studio"></a>Visual Studio에서 프로젝트를 만들려면  
  
1. Visual Studio를 시작합니다.  
  
2. 메뉴 모음에서 **파일**, **새로 만들기**, **프로젝트**를 차례로 선택합니다.  
  
     **새 프로젝트** 대화 상자가 열립니다.  
  
3. **설치됨**, **템플릿**, **Visual C#** 을 차례로 확장하고 **콘솔 애플리케이션**을 선택합니다.  
  
4. **이름** 텍스트 상자에 다른 이름을 입력하거나 기본 이름을 선택한 다음 **확인** 단추를 선택합니다.  
  
     **솔루션 탐색기**에 새 프로젝트가 표시됩니다.  
  
5. 프로젝트에 System.Core.dll에 대한 참조 및 <xref:System.Linq?displayProperty=nameWithType> 네임스페이스에 대한 `using` 지시문이 있습니다.  
  
## <a name="create-an-in-memory-data-source"></a>메모리 내 데이터 소스 만들기  
 쿼리의 데이터 소스는 간단한 `Student` 개체 목록입니다. 각 `Student` 레코드에는 이름, 성 및 클래스의 테스트 점수를 나타내는 정수 배열이 있습니다. 프로젝트에 이 코드를 복사합니다. 다음 특성에 주의합니다.  
  
- `Student` 클래스는 자동으로 구현된 속성으로 구성됩니다.  
  
- 목록의 각 학생은 개체 이니셜라이저로 초기화됩니다.  
  
- 목록 자체는 컬렉션 이니셜라이저로 초기화됩니다.  
  
 이 전체 데이터 구조는 생성자 또는 명시적 멤버 액세스에 대한 명시적 호출 없이 초기화되고 인스턴스화됩니다. 이러한 새로운 기능에 대한 자세한 내용은 [자동으로 구현된 속성](../../classes-and-structs/auto-implemented-properties.md) 및 [개체 및 컬렉션 이니셜라이저](../../classes-and-structs/object-and-collection-initializers.md)를 참조하세요.  
  
#### <a name="to-add-the-data-source"></a>데이터 소스를 추가하려면  
  
- `Student` 클래스 및 초기화된 학생 목록을 프로젝트의 `Program` 클래스에 추가합니다.  
  
     [!code-csharp[CsLinqGettingStarted#11](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#11)]  
  
#### <a name="to-add-a-new-student-to-the-students-list"></a>학생 목록에 새 학생을 추가하려면  
  
1. 새 `Student`를 `Students` 목록에 추가하고 원하는 이름 및 시험 점수를 사용합니다. 개체 이니셜라이저의 구문을 더 잘 알 수 있도록 새로운 학생 정보를 모두 입력해 보세요.  
  
## <a name="create-the-query"></a>쿼리 만들기  
  
#### <a name="to-create-a-simple-query"></a>단순 쿼리를 작성하려면  
  
- 애플리케이션의 `Main` 메서드에서, 실행 시 첫 번째 테스트의 점수가 90보다 큰 모든 학생의 목록을 생성하는 간단한 쿼리를 만듭니다. 전체 `Student` 개체가 선택되므로 쿼리의 형식은 `IEnumerable<Student>`입니다. [var](../../../language-reference/keywords/var.md) 키워드를 사용하여 코드에서 암시적 형식을 사용할 수도 있지만, 결과를 명확하게 설명하기 위해 명시적 형식이 사용됩니다. `var`에 대한 자세한 내용은 [암시적으로 형식화된 지역 변수](../../classes-and-structs/implicitly-typed-local-variables.md)를 참조하세요.  
  
     또한 쿼리의 범위 변수 `student`는 소스의 각 `Student`에 대한 참조로 사용되며, 각 개체에 대한 멤버 액세스를 제공합니다.  
  
 [!code-csharp[CsLINQGettingStarted#12](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#12)]  
  
## <a name="execute-the-query"></a>쿼리 실행  
  
#### <a name="to-execute-the-query"></a>쿼리를 실행하려면  
  
1. 이제 쿼리를 실행하도록 할 `foreach` 루프를 작성합니다. 다음은 코드에 대한 유의 사항입니다.  
  
    - 반환된 시퀀스의 각 요소는 `foreach` 루프의 반복 변수를 통해 액세스됩니다.  
  
    - 이 변수의 형식은 `Student`이며, 쿼리 변수 형식은 `IEnumerable<Student>`과 호환됩니다.  
  
2. 이 코드를 추가한 후 애플리케이션을 빌드하고 실행하고 **콘솔** 창에서 결과를 확인하세요.  
  
 [!code-csharp[CsLINQGettingStarted#13](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#13)]  
  
#### <a name="to-add-another-filter-condition"></a>다른 필터 조건을 추가하려면  
  
1. 쿼리를 구체화하기 위해 `where` 절에서 여러 부울 조건을 결합할 수 있습니다. 다음 코드는 쿼리를 실행하여 첫 번째 점수가 90을 초과하고 마지막 점수가 80 미만인 학생들을 반환하도록 하는 조건을 추가합니다. `where` 절은 다음 코드와 유사합니다.  
  
    ```csharp
    where student.Scores[0] > 90 && student.Scores[3] < 80  
    ```  
  
     자세한 내용은 [where 절](../../../language-reference/keywords/where-clause.md)을 참조하세요.  
  
## <a name="modify-the-query"></a>쿼리 수정  
  
#### <a name="to-order-the-results"></a>결과를 정렬하려면  
  
1. 특정 순서로 되어 있는 경우 결과를 더 쉽게 검색할 수 있습니다. 반환된 시퀀스를 소스 요소에서 액세스 가능한 필드 기준으로 정렬할 수 있습니다. 예를 들어, 다음 `orderby` 절은 각 학생의 성에 따라 결과를 사전순으로 정렬합니다. `where` 문 바로 다음과 `select` 문 앞에서 다음 `orderby` 절을 쿼리에 추가합니다.  
  
    ```csharp
    orderby student.Last ascending  
    ```  
  
2. 이제 가장 높은 점수에서 가장 낮은 점수까지 첫 번째 테스트의 점수에 따라 역순으로 결과를 정렬하도록 `orderby` 절을 변경합니다.  
  
    ```csharp
    orderby student.Scores[0] descending  
    ```  
  
3. 점수를 볼 수 있도록 `WriteLine` 형식 문자열을 변경합니다.  
  
    ```csharp
    Console.WriteLine("{0}, {1} {2}", student.Last, student.First, student.Scores[0]);  
    ```  
  
     자세한 내용은 [orderby 절](../../../language-reference/keywords/orderby-clause.md)을 참조하세요.  
  
#### <a name="to-group-the-results"></a>결과를 그룹화하려면  
  
1. 그룹화는 쿼리 식의 강력한 기능입니다. 그룹 절이 있는 쿼리는 그룹 시퀀스를 생성하며, 각 그룹 자체는 `Key` 및 해당 그룹의 모든 멤버로 구성된 시퀀스를 포함합니다. 다음과 같은 새 쿼리는 학생 성의 첫 글자를 키로 사용하여 학생들을 그룹화합니다.  
  
     [!code-csharp[CsLINQGettingStarted#14](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#14)]  
  
2. 이제 쿼리 형식이 변경되었습니다. 이제 쿼리를 실행하면 `char` 형식을 키로 가지고 있고 `Student` 개체의 시퀀스를 가지고 있는 그룹의 시퀀스가 생성됩니다. 쿼리 형식이 변경되었으므로 다음 코드는 `foreach` 실행 루프도 변경합니다.  
  
     [!code-csharp[CsLINQGettingStarted#15](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#15)]  
  
3. 애플리케이션을 실행하고 **콘솔** 창에서 결과를 봅니다.  
  
     자세한 내용은 [group 절](../../../language-reference/keywords/group-clause.md)을 참조하세요.  
  
#### <a name="to-make-the-variables-implicitly-typed"></a>변수를 암시적으로 형식화하려면  
  
1. `IGroupings`의 `IEnumerables`를 명시적으로 코딩하는 작업은 지루할 수 있습니다. `var`을 사용하여 동일한 쿼리 및 `foreach` 루프를 훨씬 더 편리하게 작성할 수 있습니다. `var` 키워드는 개체 형식을 변경하지 않고, 형식을 추론하도록 컴파일러에 지시합니다. `studentQuery`의 형식 및 `group` 반복 변수를 `var`로 변경하고 쿼리를 다시 실행합니다. 내부 `foreach` 루프에서 반복 변수의 형식은 여전히 `Student`로 지정되며 쿼리는 이전과 마찬가지로 작동합니다. `s` 반복 변수를 `var`로 변경하고 쿼리를 다시 실행합니다. 정확히 동일한 결과가 표시됩니다.  
  
     [!code-csharp[CsLINQGettingStarted#16](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#16)]  
  
     [var](../../../language-reference/keywords/var.md)에 대한 자세한 내용은 [암시적으로 형식화된 지역 변수](../../classes-and-structs/implicitly-typed-local-variables.md)를 참조하세요.  
  
#### <a name="to-order-the-groups-by-their-key-value"></a>키 값을 기준으로 그룹을 정렬하려면  
  
1. 이전 쿼리를 실행하면 그룹이 사전순으로 표시되지 않습니다. 이를 변경하려면 `group` 절 뒤에 `orderby` 절을 제공해야 합니다. 그러나 `orderby` 절을 사용하려면 우선 `group` 절로 만든 그룹에 대한 참조 역할을 하는 식별자가 필요합니다. 다음과 같이 `into` 키워드를 사용하여 식별자를 제공합니다.  
  
     [!code-csharp[csLINQGettingStarted#17](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#17)]  
  
     이 쿼리를 실행하면 이제 그룹이 사전순으로 정렬되는 것을 알 수 있습니다.  
  
#### <a name="to-introduce-an-identifier-by-using-let"></a>let을 사용하여 식별자를 소개하려면  
  
1. `let` 키워드를 사용하여 쿼리 식의 식 결과에 대한 식별자를 소개할 수 있습니다. 이 식별자는 다음 예제에서처럼 편리하게 사용할 수도 있고, 여러 번 계산할 필요가 없도록 표현식의 결과를 저장하여 성능을 향상시킬 수도 있습니다.  
  
     [!code-csharp[csLINQGettingStarted#18](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#18)]  
  
     자세한 내용은 [let 절](../../../language-reference/keywords/let-clause.md)을 참조하세요.  
  
#### <a name="to-use-method-syntax-in-a-query-expression"></a>쿼리 식에서 메서드 구문을 사용하려면  
  
1. [LINQ의 쿼리 구문 및 메서드 구문](./query-syntax-and-method-syntax-in-linq.md)에 설명된 대로 일부 쿼리 작업은 메서드 구문을 사용해야만 표현할 수 있습니다. 다음 코드는 소스 시퀀스의 각 `Student`에 대한 총 점수를 계산한 다음, 해당 쿼리의 결과에 대해 `Average()` 메서드를 호출하여 클래스의 평균 점수를 계산합니다.
  
     [!code-csharp[csLINQGettingStarted#19](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#19)]  
  
#### <a name="to-transform-or-project-in-the-select-clause"></a>select 절에서 변환 또는 프로젝션하려면  
  
1. 쿼리가 소스 시퀀스의 요소와 다른 요소를 갖는 시퀀스를 생성하는 것은 매우 일반적입니다. 이전 쿼리 및 실행 루프를 삭제하거나 주석으로 처리하고 다음 코드로 바꿉니다. 쿼리는 문자열 시퀀스(`Students` 아님)를 반환하며 이 사실은 `foreach` 루프에 반영됩니다.  
  
     [!code-csharp[csLINQGettingStarted#20](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#20)]  
  
2. 이 연습의 앞부분에 있는 코드는 평균 클래스 점수가 약 334임을 나타냅니다. 총점이 클래스 평균보다 큰 `Students`의 시퀀스를 `Student ID`와 함께 생성하려면 `select` 문에서 무명 형식을 사용할 수 있습니다.  
  
     [!code-csharp[csLINQGettingStarted#21](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#21)]  
  
## <a name="next-steps"></a>다음 단계  
 C#에서 쿼리 작업의 기본 사항에 익숙해지면 관심이 있는 특정 LINQ 공급자 형식에 대한 설명서와 샘플을 읽을 준비가 된 것입니다.  
  
 [LINQ to SQL](../../../../framework/data/adonet/sql/linq/index.md)  
  
 [LINQ to DataSet](../../../../framework/data/adonet/linq-to-dataset.md)  
  
 [LINQ to XML(C#)](./linq-to-xml-overview.md)  
  
 [LINQ to Objects(C#)](./linq-to-objects.md)  
  
## <a name="see-also"></a>참고 항목

- [LINQ(Language-Integrated Query)(C#)](./index.md)
- [LINQ 쿼리 식](../../linq-query-expressions/index.md)
