---
title: 데이터 그룹화(C#)
ms.date: 07/20/2015
ms.assetid: e414e9e4-343a-4e6e-858f-4a30c5e64492
ms.openlocfilehash: 15dafdb144ee9fd4184d4c8281d041e03161a16b
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69594197"
---
# <a name="grouping-data-c"></a>데이터 그룹화(C#)
그룹화는 데이터를 그룹에 넣어 각 그룹의 요소가 공통 특성을 공유하게 하는 작업을 가리킵니다.  
  
 다음 그림은 문자 시퀀스를 그룹화한 결과를 보여 줍니다. 각 그룹에 대한 키는 문자입니다.  
  
 ![LINQ 그룹화 작업을 보여주는 다이어그램.](./media/grouping-data/linq-group-operation.png)  
  
 데이터 요소를 그룹화하는 표준 쿼리 연산자 메서드가 다음 섹션에 나와 있습니다.  
  
## <a name="methods"></a>메서드  
  
|메서드 이름|설명|C# 쿼리 식 구문|추가 정보|  
|-----------------|-----------------|---------------------------------|----------------------|  
|GroupBy|공통 특성을 공유하는 요소를 그룹화합니다. 각 그룹은 <xref:System.Linq.IGrouping%602> 개체로 표시됩니다.|`group … by`<br /><br /> 또는<br /><br /> `group … by … into …`|<xref:System.Linq.Enumerable.GroupBy%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.GroupBy%2A?displayProperty=nameWithType>|  
|ToLookup|키 선택기 함수에 따라 <xref:System.Linq.Lookup%602>(일대다 사전)에 요소를 삽입합니다.|해당 사항 없음.|<xref:System.Linq.Enumerable.ToLookup%2A?displayProperty=nameWithType>|  
  
## <a name="query-expression-syntax-example"></a>쿼리 식 구문 예제  
 다음 코드 예제에서는 `group by` 절을 사용하여 짝수 또는 홀수인지에 따라 목록에서 정수를 그룹화합니다.  
  
```csharp  
List<int> numbers = new List<int>() { 35, 44, 200, 84, 3987, 4, 199, 329, 446, 208 };  
  
IEnumerable<IGrouping<int, int>> query = from number in numbers  
                                         group number by number % 2;  
  
foreach (var group in query)  
{  
    Console.WriteLine(group.Key == 0 ? "\nEven numbers:" : "\nOdd numbers:");  
    foreach (int i in group)  
        Console.WriteLine(i);  
}  
  
/* This code produces the following output:  
  
    Odd numbers:  
    35  
    3987  
    199  
    329  
  
    Even numbers:  
    44  
    200  
    84  
    4  
    446  
    208  
*/  
```  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Linq>
- [표준 쿼리 연산자 개요(C#)](./standard-query-operators-overview.md)
- [group 절](../../../language-reference/keywords/group-clause.md)
- [방법: 중첩 그룹 만들기](../../linq-query-expressions/how-to-create-a-nested-group.md)
- [방법: 확장명에 따라 파일 그룹화(LINQ)(C#)](./how-to-group-files-by-extension-linq.md)
- [방법: 쿼리 결과 그룹화](../../linq-query-expressions/how-to-group-query-results.md)
- [방법: 그룹화 작업에서 하위 쿼리 수행](../../linq-query-expressions/how-to-perform-a-subquery-on-a-grouping-operation.md)
- [방법: 그룹을 사용하여 파일을 여러 파일로 분할(LINQ)(C#)](./how-to-split-a-file-into-many-files-by-using-groups-linq.md)
