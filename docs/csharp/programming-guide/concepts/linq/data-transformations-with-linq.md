---
title: LINQ를 통한 데이터 변환(C#)
ms.date: 07/20/2015
helpviewer_keywords:
- LINQ [C#], data transformations
- source elements [LINQ in C#]
- joining multiple inputs [LINQ in C#]
- multiple outputs for one output sequence [LINQ in C#]
- subset of source elements [LINQ in C#]
- data sources [LINQ in C#], data transformations
- data transformations [LINQ in C#]
ms.assetid: 674eae9e-bc72-4a88-aed3-802b45b25811
ms.openlocfilehash: f042042f36e373ec05e8f0f15c14027463653578
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69924312"
---
# <a name="data-transformations-with-linq-c"></a>LINQ를 통한 데이터 변환(C#)
[!INCLUDE[vbteclinqext](~/includes/vbteclinqext-md.md)]는 데이터 검색만을 위한 도구는 아닙니다. 데이터 변환을 위한 강력한 도구이기도 합니다. [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리를 사용하여 소스 시퀀스를 입력으로 사용하고 다양한 방법으로 수정하여 새 출력 시퀀스를 만들 수 있습니다. 정렬 및 그룹화를 통해 요소 자체를 수정하지 않고 시퀀스 자체를 수정할 수 있습니다. 하지만 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리의 가장 강력한 기능은 새 형식을 만드는 기능일 것입니다. 이 작업은 [select](../../../language-reference/keywords/select-clause.md) 절에서 수행합니다. 예를 들어, 아래와 같은 작업을 수행할 수 있습니다.  
  
- 여러 입력 시퀀스를 새 형식을 가진 단일 출력 시퀀스로 병합합니다.  
  
- 소스 시퀀스에 있는 각 요소의 속성 하나만으로 또는 여러 속성으로 구성된 출력 시퀀스를 만듭니다.  
  
- 요소가 소스 데이터에서 수행된 작업의 결과로 구성된 출력 시퀀스를 만듭니다.  
  
- 출력 시퀀스를 다른 형식으로 만듭니다. 예를 들어 데이터를 SQL 행 또는 텍스트 파일에서 XML로 변환할 수 있습니다.  
  
 이것은 몇 가지 예일 뿐입니다. 물론 같은 쿼리에서 다양한 방법으로 이러한 변환을 결합할 수 있습니다. 또한 한 쿼리의 출력 시퀀스는 새 쿼리에 대한 입력 시퀀스로 사용할 수 있습니다.  
  
## <a name="joining-multiple-inputs-into-one-output-sequence"></a>여러 입력을 단일 출력 시퀀스로 결합  
 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리를 사용하여 두 개 이상의 입력 시퀀스에서 생성된 요소가 포함된 출력 시퀀스를 만들 수 있습니다. 다음 예제에서는 두 개의 메모리 내 데이터 구조를 결합하는 방법을 보여 주지만 XML, SQL 또는 DataSet 소스에서 데이터를 결합하는 데는 같은 원칙을 적용할 수 있습니다. 다음 두 가지 클래스 형식을 가정합니다.  
  
 [!code-csharp[CsLINQGettingStarted#7](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#7)]  
  
 다음 예제에서는 쿼리를 보여 줍니다.  
  
 [!code-csharp[CSLinqGettingStarted#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#8)]  
  
 자세한 내용은 [join 절](../../../language-reference/keywords/join-clause.md) 및 [select 절](../../../language-reference/keywords/select-clause.md)을 참조하세요.  
  
## <a name="selecting-a-subset-of-each-source-element"></a>각 소스 요소의 하위 집합 선택  
 소스 시퀀스에서 각 요소의 하위 집합을 선택하는 두 가지 기본 방법은 다음과 같습니다.  
  
1. 소스 요소의 멤버를 하나만 선택하려면 점 작업을 사용합니다. 다음 예제에서는 `Customer` 개체에 `City` 문자열을 비롯한 여러 public 속성이 포함된다고 가정합니다. 실행될 경우 이 쿼리는 문자열의 출력 시퀀스를 생성합니다.  
  
    ```csharp
    var query = from cust in Customers  
                select cust.City;  
    ```  
  
2. 소스 요소의 속성의 두 개 이상 포함된 요소를 만들려면 개체 이니셜라이저를 명명된 개체 또는 무명 형식과 함께 사용합니다. 다음 예제에서는 무명 형식을 사용하여 각 `Customer` 요소의 두 개 속성을 캡슐화하는 방법을 보여 줍니다.  
  
    ```csharp
    var query = from cust in Customer  
                select new {Name = cust.Name, City = cust.City};  
    ```  
  
 자세한 내용은 [개체 및 컬렉션 이니셜라이저](../../classes-and-structs/object-and-collection-initializers.md) 및 [무명 형식](../../classes-and-structs/anonymous-types.md)을 참조하세요.  
  
## <a name="transforming-in-memory-objects-into-xml"></a>메모리 내 개체를 XML로 변환  
 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리를 통해 메모리 내 데이터 구조, SQL 데이터베이스, ADO.NET 데이터 세트 및 XML 스트림이나 문서 간에 손쉽게 데이터를 변환할 수 있습니다. 다음 예제에서는 메모리 내 데이터 구조의 개체를 XML 요소로 변환합니다.  
  
 [!code-csharp[CsLINQGettingStarted#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#9)]  
  
 이 코드에서는 다음 XML 출력을 생성합니다.  
  
```xml  
<Root>  
  <student>  
    <First>Svetlana</First>  
    <Last>Omelchenko</Last>  
    <Scores>97,92,81,60</Scores>  
  </student>  
  <student>  
    <First>Claire</First>  
    <Last>O'Donnell</Last>  
    <Scores>75,84,91,39</Scores>  
  </student>  
  <student>  
    <First>Sven</First>  
    <Last>Mortensen</Last>  
    <Scores>88,94,65,91</Scores>  
  </student>  
</Root>  
```  
  
 자세한 내용은 [C#에서 XML 트리 만들기(LINQ to XML)](./creating-xml-trees-linq-to-xml-2.md)를 참조하세요.  
  
## <a name="performing-operations-on-source-elements"></a>소스 요소에서 작업 수행  
 출력 시퀀스에 소스 시퀀스의 요소 또는 요소 속성이 포함되어 있지 않을 수 있습니다. 대신에 출력이 소스 요소를 입력 인수로 사용하여 계산되는 값 시퀀스일 수 있습니다. 다음 간단한 쿼리는 실행 시 값이 `double` 형식 요소의 소스 시퀀스에 기반을 둔 계산을 나타내는 문자열 시퀀스를 출력합니다.  
  
> [!NOTE]
> 쿼리가 일부 다른 도메인으로 변환될 경우 쿼리 식에서 메서드를 호출할 수 없습니다. 예를 들어 SQL Server에는 관련 컨텍스트가 없으므로 [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)]에서 일반 C# 메서드를 호출할 수 없습니다. 그러나 저장 프로시저를 메서드에 매핑하고 저장 프로시저를 호출할 수 있습니다. 자세한 내용은 [저장 프로시저](../../../../framework/data/adonet/sql/linq/stored-procedures.md)를 참조하세요.  
  
 [!code-csharp[CsLINQGettingStarted#10](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsLINQGettingStarted/CS/Class1.cs#10)]  
  
## <a name="see-also"></a>참고 항목

- [LINQ(Language-Integrated Query)(C#)](./index.md)
- [LINQ to SQL](../../../../framework/data/adonet/sql/linq/index.md)
- [LINQ to DataSet](../../../../framework/data/adonet/linq-to-dataset.md)
- [LINQ to XML(C#)](./linq-to-xml-overview.md)
- [LINQ 쿼리 식](../../linq-query-expressions/index.md)
- [select 절](../../../language-reference/keywords/select-clause.md)
