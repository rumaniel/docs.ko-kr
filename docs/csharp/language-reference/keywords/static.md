---
title: static 한정자 - C# 참조
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- static
- static_CSharpKeyword
helpviewer_keywords:
- static keyword [C#]
ms.assetid: 5509e215-2183-4da3-bab4-6b7e607a4fdf
ms.openlocfilehash: b288e57d9241e294a0fa18edafe72eec675327a7
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65633182"
---
# <a name="static-c-reference"></a>static(C# 참조)

`static` 한정자를 사용하여 특정 개체가 아니라 형식 자체에 속하는 정적 멤버를 선언할 수 있습니다. `static` 한정자는 클래스, 필드, 메서드, 속성, 연산자, 이벤트 및 생성자와 함께 사용할 수 있지만 인덱서, 종료자 또는 클래스 이외의 형식에는 사용할 수 없습니다. 자세한 내용은 [static 클래스 및 static 클래스 멤버](../../programming-guide/classes-and-structs/static-classes-and-static-class-members.md)를 참조하세요.

## <a name="example"></a>예제

다음 클래스는 `static`으로 선언되며 `static` 메서드만 포함합니다.

[!code-csharp[csrefKeywordsModifiers#18](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#18)]

상수 또는 형식 선언은 암시적으로 정적 멤버입니다.

정적 멤버는 인스턴스를 통해 참조할 수 없습니다. 대신, 형식 이름을 통해 참조됩니다. 예를 들어 다음 클래스를 예로 들어 볼 수 있습니다.

[!code-csharp[csrefKeywordsModifiers#19](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#19)]

정적 멤버 `x`를 참조하려면 동일한 범위에서 멤버에 액세스할 수 없는 경우 정규화된 이름 `MyBaseC.MyStruct.x`를 사용합니다.

```csharp
Console.WriteLine(MyBaseC.MyStruct.x);
```

클래스 인스턴스에는 클래스의 모든 인스턴스 필드에 대한 별도 복사본이 포함되지만 각 정적 필드의 복사본은 한 개만 있습니다.

[this](this.md)를 사용하여 정적 메서드 또는 속성 접근자를 참조할 수 없습니다.

`static` 키워드가 클래스에 적용된 경우 클래스의 모든 멤버가 정적이어야 합니다.

클래스 및 정적 클래스에 정적 생성자가 있을 수 있습니다. 프로그램이 시작된 후, 클래스가 인스턴스화되기 전에 정적 생성자가 호출됩니다.

> [!NOTE]
> `static` 키워드는 C++보다 사용이 제한적입니다. C++ 키워드와 비교하려면 [스토리지 클래스(C++)](/cpp/cpp/storage-classes-cpp#static)를 참조하세요.

정적 멤버를 보여 주려면 회사 직원을 나타내는 클래스를 고려해 보세요. 클래스에 직원 수를 구하는 메서드와 직원 수를 저장하는 필드가 포함되어 있다고 가정합니다. 메서드와 필드는 둘 다 인스턴스 직원에 속하지 않습니다. 대신 회사 클래스에 속해 있습니다. 따라서 클래스의 정적 멤버로 선언해야 합니다.

## <a name="example"></a>예제

이 예제에서는 새 직원의 이름 및 ID를 읽고, 직원 카운터를 1만큼 늘린 다음 새 직원에 대한 정보와 새 직원 수를 표시합니다. 간단히 하기 위해 이 프로그램은 키보드에서 현재 직원 수를 읽습니다. 실제 애플리케이션에서는 이 정보를 파일에서 읽어야 합니다.

[!code-csharp[csrefKeywordsModifiers#20](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#20)]  

## <a name="example"></a>예제

이 예제에서는 아직 선언되지 않은 다른 정적 필드를 사용하여 정적 필드를 초기화할 수 있지만 정적 필드에 값을 명시적으로 할당할 때까지 결과가 정의되지 않음을 보여 줍니다.

[!code-csharp[csrefKeywordsModifiers#21](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#21)]  

## <a name="c-language-specification"></a>C# 언어 사양

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [C# 키워드](index.md)
- [한정자](modifiers.md)
- [정적 클래스 및 정적 클래스 멤버](../../programming-guide/classes-and-structs/static-classes-and-static-class-members.md)
