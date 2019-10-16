---
title: 기본 LINQ 쿼리 작업(C#)
ms.date: 07/20/2015
helpviewer_keywords:
- orderby clause [LINQ in C#]
- ordering data [LINQ in C#]
- selecting data [LINQ in C#]
- queries [LINQ in C#], basic operations
- grouping data [LINQ in C#]
- data sources [LINQ in C#]
- sorting data [LINQ in C#]
- projections [LINQ in C#]
- filtering data [LINQ in C#]
- joining data [LINQ in C#]
- select clause [LINQ in C#]
- LINQ [C#], basic query operations
- join clause [LINQ in C#]
- group clause [LINQ in C#]
ms.assetid: a7ea3421-1cf4-4df7-832a-aa22fe6379e9
ms.openlocfilehash: 013e1960e6c5721e0bd7ce6998848ddce15a4e4d
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69924387"
---
# <a name="basic-linq-query-operations-c"></a>기본 LINQ 쿼리 작업(C#)
이 항목에서는 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리 식 및 쿼리에서 수행하는 일부 일반적인 작업을 간단히 소개합니다. 자세한 내용은 다음 항목을 참조하세요.  
  
 [LINQ 쿼리 식](../../linq-query-expressions/index.md)  
  
 [표준 쿼리 연산자 개요(C#)](./standard-query-operators-overview.md)  
  
 [연습: C#에서 쿼리 작성](./walkthrough-writing-queries-linq.md)  
  
> [!NOTE]
> SQL 또는 XQuery와 같은 쿼리 언어를 이미 잘 알고 있으면 이 항목의 대부분을 건너뛸 수 있습니다. [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리 식에서 절의 순서를 알아보려면 "`from` 절"을 확인하세요.  
  
## <a name="obtaining-a-data-source"></a>데이터 소스 가져오기  
 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리에서 첫 번째 단계는 데이터 소스를 지정하는 것입니다. 대부분의 프로그래밍 언어에서처럼 C#에서 변수는 선언된 후 사용되어야 합니다. [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리에서는 데이터 소스(`customers`) 및 *범위 변수*(`cust`)를 소개하기 위해 `from` 절이 먼저 나옵니다.  
  
 [!code-csharp[csLINQGettingStarted#23](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#23)]  
  
 쿼리 식에서는 실제 반복이 발생하지 않는다는 점을 제외하고 범위 변수는 `foreach` 루프의 반복 변수와 비슷합니다. 쿼리가 실행될 때 범위 변수는 `customers`에서 각 연속 요소에 대한 참조로 사용됩니다. 컴파일러에서 `cust` 형식을 유추할 수 있으므로 명시적으로 지정할 필요가 없습니다. 추가 범위 변수는 `let` 절에 의해 소개될 수 있습니다. 자세한 내용은 [let 절](../../../language-reference/keywords/let-clause.md)을 참조하세요.  
  
> [!NOTE]
> <xref:System.Collections.ArrayList>와 같은 제네릭이 아닌 데이터 소스의 경우 범위 변수를 명시적으로 형식화해야 합니다. 자세한 내용은 [방법: LINQ를 사용하여 ArrayList 쿼리(C#)](./how-to-query-an-arraylist-with-linq.md) 및 [from 절](../../../language-reference/keywords/from-clause.md)을 참조하세요.  
  
## <a name="filtering"></a>필터링  
 대부분의 일반적인 쿼리 작업에서는 부울 식 형태로 필터를 적용합니다. 필터를 사용하면 쿼리에서는 식이 true인 요소만 반환합니다. 결과는 `where` 절에 따라 반환됩니다. 적용되는 필터는 소스 시퀀스에서 제외할 요소를 지정합니다. 다음 예제에서는 London에 주소가 있는 `customers`만 반환됩니다.  
  
 [!code-csharp[csLINQGettingStarted#24](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#24)]  
  
 친숙한 C# 논리 `AND` 및 `OR` 연산자를 사용하여 `where` 절에서 필요한 만큼 필터 식을 적용할 수 있습니다. 예를 들어 "London"에 있고(`AND`) 이름이 "Devon"인 고객만 반환하려면 다음 코드를 작성합니다.  
  
 [!code-csharp[csLINQGettingStarted#25](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#25)]  
  
 London 또는 Paris에 있는 고객을 반환하려면 다음 코드를 작성합니다.  
  
 [!code-csharp[csLINQGettingStarted#26](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#26)]  
  
 자세한 내용은 [where 절](../../../language-reference/keywords/where-clause.md)을 참조하세요.  
  
## <a name="ordering"></a>순서 지정  
 보통 반환된 데이터를 정렬하는 것이 편리합니다. `orderby` 절을 사용하면 반환된 시퀀스의 요소가 정렬되는 형식의 기본 비교자에 따라 정렬됩니다. 예를 들어 `Name` 속성에 따라 결과를 정렬하도록 다음 쿼리를 확장할 수 있습니다. `Name`이 문자열이면 기본 비교자는 A에서 Z까지 사전순 정렬을 수행합니다.  
  
 [!code-csharp[csLINQGettingStarted#27](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#27)]  
  
 결과를 역순으로 정렬하려면 `orderby…descending` 절을 사용합니다.  
  
 자세한 내용은 [orderby 절](../../../language-reference/keywords/orderby-clause.md)을 참조하세요.  
  
## <a name="grouping"></a>그룹화  
 `group` 절을 사용하면 지정한 키를 기준으로 결과를 그룹화할 수 있습니다. 예를 들어 결과가 `City`별로 그룹화되어 London 또는 Paris의 모든 고객이 개별 그룹에 포함되도록 지정할 수 있습니다. 이 경우 `cust.City`가 키입니다.  
  
 [!code-csharp[csLINQGettingStarted#28](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#28)]  
  
 쿼리를 `group` 절로 종료하면 결과에 여러 목록으로 구성된 목록 형식이 사용됩니다. 목록의 각 요소는 `Key` 멤버 및 해당 키로 그룹화된 요소 목록이 포함된 개체입니다. 그룹 시퀀스를 생성하는 쿼리를 반복할 경우 중첩된 `foreach` 루프를 사용해야 합니다. 외부 루프는 각 그룹을 반복하고 내부 루프는 각 그룹의 멤버를 반복합니다.  
  
 그룹 작업의 결과를 참조해야 할 경우 `into` 키워드를 사용하여 추가로 쿼리될 수 있는 식별자를 만들 수 있습니다. 다음 쿼리는 세 명 이상의 고객이 포함된 그룹만 반환합니다.  
  
 [!code-csharp[csLINQGettingStarted#29](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#29)]  
  
 자세한 내용은 [group 절](../../../language-reference/keywords/group-clause.md)을 참조하세요.  
  
## <a name="joining"></a>조인  
 조인 작업은 데이터 소스에서 명시적으로 모델링되지 않은 시퀀스 간 연결을 만듭니다. 예를 들어 같은 위치를 가진 모든 고객 및 배포자를 찾는 조인을 수행할 수 있습니다. [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)]에서 `join` 절은 항상 직접 데이터베이스 테이블이 아닌 개체 컬렉션에 대해 작동합니다.  
  
 [!code-csharp[csLINQGettingStarted#36](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#36)]  
  
 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)]의 외래 키는 개체 모델에서 항목 컬렉션을 포함하는 속성으로 표현되므로 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)]에서는 SQL에서처럼 자주 `join`을 사용할 필요가 없습니다. 예를 들어 `Customer` 개체에는 `Order` 개체의 컬렉션이 포함됩니다. 조인을 수행하지 않고 점 표기법을 사용하여 주문에 액세스합니다.  
  
```csharp
from order in Customer.Orders...  
```  
  
 자세한 내용은 [join 절](../../../language-reference/keywords/join-clause.md)을 참조하세요.  
  
## <a name="selecting-projections"></a>선택(프로젝션)  
 `select` 절은 쿼리 결과를 생성하고 각 반환된 요소의 “모양" 또는 형식을 지정합니다. 예를 들어 결과가 계산 또는 새 개체 만들기에 따라 전체 `Customer` 개체, 하나의 멤버만, 멤버 하위 집합 또는 일부 완전히 다른 결과 형식으로 구성될지 지정할 수 있습니다. `select` 절이 소스 요소의 복사본이 아닌 다른 항목을 생성하는 경우 이 작업을 *프로젝션*이라고 합니다. 프로젝션을 사용하여 데이터를 변환하는 것은 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리 식의 강력한 기능입니다. 자세한 내용은 [LINQ를 통한 데이터 변환(C#)](./data-transformations-with-linq.md) 및 [select 절](../../../language-reference/keywords/select-clause.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [LINQ 쿼리 식](../../linq-query-expressions/index.md)
- [연습: C#에서 쿼리 작성](./walkthrough-writing-queries-linq.md)
- [쿼리 키워드(LINQ)](../../../language-reference/keywords/query-keywords.md)
- [익명 형식](../../classes-and-structs/anonymous-types.md)
