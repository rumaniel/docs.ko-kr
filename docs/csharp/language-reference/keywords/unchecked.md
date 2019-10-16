---
title: unchecked 키워드 - C# 참조
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- unchecked_CSharpKeyword
- unchecked
helpviewer_keywords:
- unchecked keyword [C#]
ms.assetid: 0c021f7c-923f-4b3d-a58f-55336f5ac27e
ms.openlocfilehash: c31f1243b1394bfe826b02c14c73faf402640849
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69608420"
---
# <a name="unchecked-c-reference"></a>unchecked(C# 참조)

`unchecked` 키워드는 정수 형식 산술 연산 및 변환에 대한 오버플로 검사를 비활성화하는 데 사용됩니다.

unchecked 컨텍스트에서 식이 대상 형식의 범위를 벗어난 값을 생성하는 경우 오버플로에 플래그가 지정되지 않습니다. 예를 들어 다음 예제의 계산은 `unchecked` 블록 또는 식에서 수행되므로 결과가 정수에 비해 너무 크다는 사실이 무시되며 `int1`에 -2,147,483,639 값이 할당됩니다.

[!code-csharp[csrefKeywordsChecked#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsChecked/CS/csrefKeywordsChecked.cs#5)]

`unchecked` 환경을 제거하면 컴파일 오류가 발생합니다. 식의 모든 항이 상수이기 때문에 컴파일 시간에 오버플로가 검색될 수 있습니다.

상수가 아닌 항을 포함하는 식은 컴파일 시간 및 런타임에 기본적으로 확인되지 않습니다. checked 환경을 사용하도록 설정하는 방법에 대한 자세한 내용은 [checked](checked.md)를 참조하세요.

오버플로를 확인하는 데 시간이 걸리기 때문에 오버플로 위험이 없는 상황에서는 unchecked 코드를 사용하여 성능을 향상할 수 있습니다. 그러나 오버플로가 발생할 가능성이 있는 경우 checked 환경을 사용해야 합니다.

## <a name="example"></a>예

이 샘플에서는 `unchecked` 키워드를 사용하는 방법을 보여 줍니다.

[!code-csharp[csrefKeywordsChecked#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsChecked/CS/csrefKeywordsChecked.cs#2)]

## <a name="c-language-specification"></a>C# 언어 사양

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [C# 키워드](index.md)
- [Checked 및 Unchecked](checked-and-unchecked.md)
- [checked](checked.md)
