---
title: new 제약 조건 - C# 참조
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- new constraint keyword [C#]
ms.assetid: 58850b64-cb97-4136-be50-1f3bc7fc1da9
ms.openlocfilehash: 7c788be52010cdfadbd3c03f9e570815d25bdbef
ms.sourcegitcommit: bab17fd81bab7886449217356084bf4881d6e7c8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2019
ms.locfileid: "67401489"
---
# <a name="new-constraint-c-reference"></a>new 제약 조건(C# 참조)

`new` 제약 조건은 제네릭 클래스 선언의 형식 인수에 공용 매개 변수가 없는 생성자가 있어야 함을 지정합니다. `new` 제약 조건을 사용하기 위해 유형을 추상화할 수 없습니다.

다음 예제와 같이 제네릭 클래스가 형식의 새 인스턴스를 만드는 경우 형식 매개 변수에 `new` 제약 조건을 적용합니다.

[!code-csharp[csrefKeywordsOperator#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsOperator/CS/csrefKeywordsOperators.cs#5)]

다른 제약 조건과 함께 `new()` 제약 조건을 사용하는 경우 마지막에 지정해야 합니다.

[!code-csharp[csrefKeywordsOperator#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsOperator/CS/csrefKeywordsOperators.cs#6)]

자세한 내용은 [형식 매개 변수에 대한 제약 조건](../../programming-guide/generics/constraints-on-type-parameters.md)을 참조하세요.

`new` 키워드를 사용하여 [형식의 인스턴스를 만들](../operators/new-operator.md)거나 [멤버 선언 한정자](new-modifier.md)로 만들 수도 있습니다.

## <a name="c-language-specification"></a>C# 언어 사양

자세한 내용은 [C# 언어 사양](~/_csharplang/spec/introduction.md)의 [유형 매개 변수 제약 조건](~/_csharplang/spec/classes.md#type-parameter-constraints) 섹션을 참조하세요.

## <a name="see-also"></a>참고 항목

- [C# 참조](../../language-reference/index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [C# 키워드](index.md)
- [제네릭](../../programming-guide/generics/index.md)
