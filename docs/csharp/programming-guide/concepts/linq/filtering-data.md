---
title: 데이터 필터링(C#)
ms.date: 07/20/2015
ms.assetid: fbaece0d-0f23-47f7-89c5-f3ea8db692b6
ms.openlocfilehash: 17d3a65b6042c9679a263eff0048f5360c4aa546
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69594401"
---
# <a name="filtering-data-c"></a>데이터 필터링(C#)
필터링은 지정된 조건을 충족하는 요소만 포함하도록 결과 집합을 제한하는 작업을 가리킵니다. 필터링은 선택이라고도 합니다.  
  
 다음 그림에서는 문자 시퀀스를 필터링한 결과를 보여 줍니다. 필터링 작업에 대한 조건자는 문자가 'A'가 되도록 지정합니다.  
  
 ![LINQ 필터링 작업을 보여주는 다이어그램](./media/filtering-data/linq-filter-operation.png)  
  
 선택을 수행하는 표준 쿼리 연산자 메서드는 다음 섹션에 나열됩니다.  
  
## <a name="methods"></a>메서드  
  
|메서드 이름|설명|C# 쿼리 식 구문|추가 정보|  
|-----------------|-----------------|---------------------------------|----------------------|  
|OfType|지정된 형식으로 캐스트할 수 있는지 여부에 따라 값을 선택합니다.|해당 사항 없음.|<xref:System.Linq.Enumerable.OfType%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.OfType%2A?displayProperty=nameWithType>|  
|Where|조건자 함수를 기반으로 하는 값을 선택합니다.|`where`|<xref:System.Linq.Enumerable.Where%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Where%2A?displayProperty=nameWithType>|  
  
## <a name="query-expression-syntax-example"></a>쿼리 식 구문 예제  
 다음 예제에서는 `where` 절을 사용하여 배열에서 특정 길이의 문자열을 필터링합니다.  
  
```csharp  
string[] words = { "the", "quick", "brown", "fox", "jumps" };  
  
IEnumerable<string> query = from word in words  
                            where word.Length == 3  
                            select word;  
  
foreach (string str in query)  
    Console.WriteLine(str);  
  
/* This code produces the following output:  
  
    the  
    fox  
*/  
```  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Linq>
- [표준 쿼리 연산자 개요(C#)](./standard-query-operators-overview.md)
- [where 절](../../../language-reference/keywords/where-clause.md)
- [방법: 런타임에 동적으로 조건자 필터 지정](../../linq-query-expressions/how-to-dynamically-specify-predicate-filters-at-runtime.md)
- [방법: 리플렉션을 사용하여 어셈블리의 메타데이터 쿼리(LINQ)(C#)](./how-to-query-an-assembly-s-metadata-with-reflection-linq.md)
- [방법: 지정된 특성 또는 이름을 갖는 파일 쿼리(C#)](./how-to-query-for-files-with-a-specified-attribute-or-name.md)
- [방법: 단어 또는 필드에 따라 텍스트 데이터 정렬 또는 필터링(LINQ)(C#)](./how-to-sort-or-filter-text-data-by-any-word-or-field-linq.md)
