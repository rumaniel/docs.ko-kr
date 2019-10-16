---
title: 쿼리 결과를 메모리에 저장
description: 결과 저장 방법
ms.date: 11/30/2016
ms.assetid: 5b863961-1750-4cf9-9607-acea5054d15a
ms.openlocfilehash: 66a7a95c74db4062e76c54d4339ccb7343f44067
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65633561"
---
# <a name="store-the-results-of-a-query-in-memory"></a>쿼리 결과를 메모리에 저장

쿼리는 기본적으로 데이터를 검색하고 구성하는 방법에 대한 명령 집합입니다. 쿼리는 결과의 각 후속 항목이 요청될 때 지연 실행됩니다. `foreach`를 사용하여 결과를 반복하는 경우 항목이 액세스될 때 반환됩니다. 쿼리를 평가한 후 `foreach` 루프를 실행하지 않고 결과를 저장하려면 쿼리 변수에 대해 다음 메서드 중 하나를 호출합니다.

- <xref:System.Linq.Enumerable.ToList%2A>

- <xref:System.Linq.Enumerable.ToArray%2A>

- <xref:System.Linq.Enumerable.ToDictionary%2A>

- <xref:System.Linq.Enumerable.ToLookup%2A>

 쿼리 결과를 저장하는 경우 다음 예제와 같이 반환된 컬렉션 개체를 새 변수에 할당하는 것이 좋습니다.

## <a name="example"></a>예제

[!code-csharp[csProgGuideLINQ#25](~/samples/snippets/csharp/concepts/linq/how-to-store-the-results-of-a-query-in-memory_1.cs)]

## <a name="see-also"></a>참고 항목

- [LINQ(Language-Integrated Query)](index.md)
