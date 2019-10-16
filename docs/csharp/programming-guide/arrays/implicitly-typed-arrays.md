---
title: 암시적으로 형식화된 배열 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- arrays [C#], implicitly-typed
- implicitly-typed arrays [C#]
- C# language, implicitly typed arrays
ms.assetid: e05be95c-6732-403d-ae42-b35f057cbbea
ms.openlocfilehash: 36ca18adc392643107b43a947656846f3b94a2eb
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69597348"
---
# <a name="implicitly-typed-arrays-c-programming-guide"></a>암시적으로 형식화된 배열(C# 프로그래밍 가이드)

배열 인스턴스의 형식이 배열 이니셜라이저에 지정된 요소에서 유추되는 암시적으로 형식화된 배열을 만들 수 있습니다. 암시적으로 형식화된 변수에 대한 규칙은 암시적으로 형식화된 배열에도 적용됩니다. 자세한 내용은 [암시적으로 형식화된 지역 변수](../classes-and-structs/implicitly-typed-local-variables.md)를 참조하세요.

암시적으로 형식화된 배열은 일반적으로 무명 형식, 개체 및 컬렉션 이니셜라이저와 함께 쿼리 식에 사용됩니다.

다음 예제에서는 암시적으로 형식화된 배열을 만드는 방법을 보여 줍니다.

[!code-csharp[csProgGuideLINQ#37](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideLINQ/CS/csRef30LangFeatures_2.cs#37)]

앞의 예제에서 암시적으로 형식화된 배열의 경우 초기화 문의 왼쪽에 대괄호가 사용되지 않는 것을 확인합니다. 또한 가변 배열이 1차원 배열과 마찬가지로 `new []`를 사용하여 초기화됩니다.

## <a name="implicitly-typed-arrays-in-object-initializers"></a>개체 이니셜라이저의 암시적으로 형식화된 배열

배열이 포함된 무명 형식을 만드는 경우 해당 형식의 개체 이니셜라이저에서 배열을 암시적으로 형식화해야 합니다. 다음 예제에서 `contacts`는 각각 `PhoneNumbers`라는 배열이 포함된 무명 형식의 암시적으로 형식화된 배열입니다. `var` 키워드는 개체 이니셜라이저 내부에서 사용되지 않았습니다.

[!code-csharp[csProgGuideLINQ#38](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideLINQ/CS/csRef30LangFeatures_2.cs#38)]

## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [암시적 형식 지역 변수](../classes-and-structs/implicitly-typed-local-variables.md)
- [배열](./index.md)
- [익명 형식](../classes-and-structs/anonymous-types.md)
- [개체 이니셜라이저 및 컬렉션 이니셜라이저](../classes-and-structs/object-and-collection-initializers.md)
- [var](../../language-reference/keywords/var.md)
- [LINQ 쿼리 식](../linq-query-expressions/index.md)
