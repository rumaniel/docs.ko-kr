---
title: public 키워드 - C# 참조
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- public
- public_CSharpKeyword
helpviewer_keywords:
- public keyword [C#]
ms.assetid: 0ae45d16-a551-4b74-9845-57208de1328e
ms.openlocfilehash: a68cbf3af2568cd3c197eaece9e2d5a25cdb4a6a
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65633707"
---
# <a name="public-c-reference"></a>public(C# 참조)

`public` 키워드는 형식 및 형식 멤버에 대한 액세스 한정자입니다. 공용 액세스는 허용 범위가 가장 큰 액세스 수준입니다. 다음 예제와 같이, 공용 멤버 액세스에 대한 제한은 없습니다.

```csharp
class SampleClass
{
    public int x; // No access restrictions.
}
```

자세한 내용은 [액세스 한정자](../../programming-guide/classes-and-structs/access-modifiers.md) 및 [액세스 가능성 수준](accessibility-levels.md)을 참조하세요.

## <a name="example"></a>예제

다음 예제에서는 두 개의 클래스, `PointTest` 및 `MainClass`를 선언합니다. `PointTest`의 공용 멤버 `x` 및 `y`는 `MainClass`에서 직접 액세스합니다.

[!code-csharp[csrefKeywordsModifiers#13](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#13)]

`public` 액세스 수준을 [private](private.md) 또는 [protected](protected.md)로 변경하면 오류 메시지가 표시됩니다.

보호 수준 때문에 'PointTest.y'에 액세스할 수 없습니다.

## <a name="c-language-specification"></a>C# 언어 사양  

자세한 내용은 [C# 언어 사양](../language-specification/index.md)의 [선언된 내게 필요한 옵션](~/_csharplang/spec/basic-concepts.md#declared-accessibility)을 참조하세요. C# 언어 사양은 C# 구문 및 사용법에 대한 신뢰할 수 있는 소스입니다.

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [액세스 한정자](../../programming-guide/classes-and-structs/access-modifiers.md)
- [C# 키워드](index.md)
- [액세스 한정자](access-modifiers.md)
- [액세스 수준](accessibility-levels.md)
- [한정자](modifiers.md)
- [private](private.md)
- [protected](protected.md)
- [internal](internal.md)
