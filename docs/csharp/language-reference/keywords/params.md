---
title: params 키워드(C# 참조)
ms.date: 07/20/2015
f1_keywords:
- params_CSharpKeyword
- params
helpviewer_keywords:
- parameters [C#], params
- params keyword [C#]
ms.assetid: 1690815e-b52b-4967-8380-5780aff08012
ms.openlocfilehash: 089e31f3aad12c2303619e2a1998d0d6a5a0ad86
ms.sourcegitcommit: 8c28ab17c26bf08abbd004cc37651985c68841b8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/08/2018
ms.locfileid: "48844100"
---
# <a name="params-c-reference"></a>params(C# 참조)

`params` 키워드를 사용하면 가변 개수의 인수를 사용하는 [메서드 매개 변수](method-parameters.md)를 지정할 수 있습니다.

매개 변수 선언이나 지정된 형식의 인수 배열에 지정된 형식의 쉼표로 구분된 인수 목록을 보낼 수 있습니다. 인수를 보내지 않을 수도 있습니다. 인수를 보내지 않는 경우 `params` 목록의 길이는 0입니다.

메서드 선언에서 `params` 키워드 뒤에는 추가 매개 변수가 허용되지 않으며, `params` 키워드 하나만 메서드 선언에 사용할 수 있습니다.

`params` 매개 변수의 선언된 형식은 다음 예제와 같이 1차원 배열이어야 합니다. 그렇지 않으면 컴파일러 오류 [CS0225](../../misc/cs0225.md)가 발생합니다.

## <a name="example"></a>예

다음 예제에서는 `params` 매개 변수에 인수를 보낼 수 있는 다양한 방법을 보여 줍니다.

[!code-csharp[csrefKeywordsMethodParams#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsMethodParams/CS/csrefKeywordsMethodParams.cs#5)] 

## <a name="c-language-specification"></a>C# 언어 사양

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [C# 키워드](index.md)
- [메서드 매개 변수](method-parameters.md)