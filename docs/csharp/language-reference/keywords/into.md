---
title: into - C# 참조
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- into_CSharpKeyword
- into
helpviewer_keywords:
- into keyword [C#]
ms.assetid: 81ec62c1-f0b1-4755-8a31-959876e77f65
ms.openlocfilehash: dc1e2ee004c21bb3d05155eec3e42ea80bf641a1
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69608643"
---
# <a name="into-c-reference"></a>into(C# 참조)

`into` 상황별 키워드를 사용하여 [group](group-clause.md), [join](join-clause.md), [select](select-clause.md) 절의 결과를 새 식별자에 저장하기 위한 임시 식별자를 만들 수 있습니다. 이 식별자 자체는 추가 쿼리 명령의 생성기일 수 있습니다. `group` 또는 `select` 절에 사용할 경우 새 식별자의 사용을 *연속*이라고도 합니다.

## <a name="example"></a>예

다음 예제에서는 `into` 키워드를 사용하여 임시 식별자 `fruitGroup`을 활성화하는 방법을 보여 줍니다. 이 식별자는 `IGrouping`의 유추된 형식을 갖습니다. 식별자를 사용하여 각 그룹에서 <xref:System.Linq.Enumerable.Count%2A> 메서드를 호출하고 둘 이상의 단어를 포함하는 그룹만 선택할 수 있습니다.

[!code-csharp[cscsrefQueryKeywords#18](~/samples/snippets/csharp/VS_Snippets_VBCSharp/CsCsrefQueryKeywords/CS/Into.cs#18)]

각 그룹에서 추가 쿼리 작업을 수행하려는 경우에만 `group` 절에 `into`를 사용하면 됩니다. 자세한 내용은 [group 절](group-clause.md)을 참조하세요.

`join` 절에 `into`를 사용하는 방법의 예는 [join 절](join-clause.md)을 참조하세요.

## <a name="see-also"></a>참고 항목

- [쿼리 키워드(LINQ)](query-keywords.md)
- [LINQ 쿼리 식](../../programming-guide/linq-query-expressions/index.md)
- [group 절](group-clause.md)
