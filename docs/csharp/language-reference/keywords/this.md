---
title: this 키워드 - C# 참조
ms.custom: seodec18
description: this 키워드(C# 참조)
ms.date: 07/20/2015
f1_keywords:
- this
- this_CSharpKeyword
helpviewer_keywords:
- this keyword [C#]
ms.assetid: d4f827fe-4710-410b-89b8-867dad44b8a3
ms.openlocfilehash: 4a3342e73fef3effd54f72e68283eb6085eef5b5
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69608440"
---
# <a name="this-c-reference"></a>this(C# 참조)

`this` 키워드는 클래스의 현재 인스턴스를 가리키며 확장 메서드의 첫 번째 매개 변수에 대한 한정자로도 사용됩니다.

> [!NOTE]
> 이 문서에서는 클래스 인스턴스와 함께 `this`를 사용하는 방법을 설명합니다. 확장 메서드에서 사용하는 방법에 대한 자세한 내용은 [확장 메서드](../../programming-guide/classes-and-structs/extension-methods.md)를 참조하세요.

`this`의 일반적인 사용은 다음과 같습니다.

- 비슷한 이름으로 숨겨진 멤버를 한정합니다. 예를 들면 다음과 같습니다.

  [!code-csharp[csrefKeywordsAccess#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsAccess/CS/csrefKeywordsAccess.cs#4)]  

- 개체를 다른 메서드에 매개 변수로 전달합니다. 예를 들면 다음과 같습니다.

  ```csharp
  CalcTax(this);
  ```

- 인덱서를 선언합니다. 예를 들면 다음과 같습니다.

  [!code-csharp[csrefKeywordsAccess#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsAccess/CS/csrefKeywordsAccess.cs#5)]

정적 멤버 함수는 개체의 일부가 아니라 클래스 수준에 있기 때문에 `this` 포인터가 없습니다. 정적 메서드에서 `this`를 참조하면 오류가 발생합니다.

## <a name="example"></a>예

이 예제에서는 `this`를 사용하여 유사한 이름으로 숨겨진 `Employee` 클래스 멤버 `name` 및 `alias`를 한정합니다. 다른 클래스에 속하는 `CalcTax` 메서드에 개체를 전달하는 데에도 사용됩니다.

[!code-csharp[csrefKeywordsAccess#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsAccess/CS/csrefKeywordsAccess.cs#3)]

## <a name="c-language-specification"></a>C# 언어 사양

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [C# 키워드](index.md)
- [base](base.md)
- [메서드](../../programming-guide/classes-and-structs/methods.md)
