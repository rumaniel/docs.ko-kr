---
title: base 키워드(C# 참조)
description: C#의 파생 클래스 내에서 기본 클래스의 멤버에 액세스하는 데 사용되는 base 키워드에 대해 알아봅니다.
ms.date: 07/20/2015
f1_keywords:
- base
- BaseClass.BaseClass
- base_CSharpKeyword
helpviewer_keywords:
- base keyword [C#]
ms.assetid: 8b645dbe-1a33-49b8-8716-1c401f9a5ea5
ms.openlocfilehash: 8719ab79273701173530760ad1bec837c4f4302d
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2018
ms.locfileid: "48837869"
---
# <a name="base-c-reference"></a>base(C# 참조)

`base` 키워드는 파생 클래스 내에서 기본 클래스의 멤버에 액세스하는 데 사용됩니다.

- 다른 메서드에 의해 재정의된 기본 클래스에서 메서드를 호출합니다.

- 파생 클래스의 인스턴스를 만들 때 호출해야 하는 기본 클래스 생성자를 지정합니다.

기본 클래스 액세스는 생성자, 인스턴스 메서드 또는 인스턴스 속성 접근자에서만 허용됩니다.

정적 메서드 내에서 `base` 키워드를 사용하는 것은 오류입니다.

액세스된 기본 클래스는 클래스 선언에 지정된 기본 클래스입니다. 예를 들어 `class ClassB : ClassA`를 지정할 경우 ClassA의 기본 클래스에 관계없이 ClassA의 멤버는 ClassB에서 액세스됩니다.

## <a name="example"></a>예

이 예제에서 기본 클래스 `Person` 및 파생 클래스 `Employee`에는 둘 다 `Getinfo` 메서드가 있습니다. `base` 키워드를 사용하면 파생 클래스 내에서 기본 클래스에 대해 `Getinfo` 메서드를 호출할 수 있습니다.

[!code-csharp[csrefKeywordsAccess#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsAccess/CS/csrefKeywordsAccess.cs#1)]

추가 예제는 [new](../../../csharp/language-reference/keywords/new.md), [virtual](../../../csharp/language-reference/keywords/virtual.md) 및 [override](../../../csharp/language-reference/keywords/override.md)를 참조하세요.

## <a name="example"></a>예

이 예제에서는 파생 클래스의 인스턴스를 만들 때 호출되는 기본 클래스 생성자를 지정하는 방법을 보여 줍니다.

[!code-csharp[csrefKeywordsAccess#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsAccess/CS/csrefKeywordsAccess.cs#2)]

## <a name="c-language-specification"></a>C# 언어 사양

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>참고 항목

- [C# 참조](../../../csharp/language-reference/index.md)  
- [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)  
- [C# 키워드](../../../csharp/language-reference/keywords/index.md)  
- [this](../../../csharp/language-reference/keywords/this.md)