---
title: abstract - C# 참조
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- abstract
- abstract_CSharpKeyword
helpviewer_keywords:
- abstract keyword [C#]
ms.assetid: b0797770-c1f3-4b4d-9441-b9122602a6bb
ms.openlocfilehash: 547ecd9ff823f61bf3995c02959235b65a4a3979
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69606149"
---
# <a name="abstract-c-reference"></a>abstract(C# 참조)
`abstract` 한정자는 수정되는 항목에 누락되거나 불완전한 구현이 있음을 나타냅니다. abstract 한정자는 클래스, 메서드, 속성, 인덱서 및 이벤트와 함께 사용될 수 있습니다. 클래스 선언에서 `abstract` 한정자를 사용하여 클래스가 자체에서 인스턴스화되지 않고 다른 클래스의 기본 클래스로만 사용됨을 나타냅니다. 추상으로 표시된 멤버는 추상 클래스에서 파생된 비 추상 클래스에 의해 구현되어야 합니다.
  
## <a name="example"></a>예  
 이 예제에서 `Square` 클래스는 `Shape`에서 파생되므로 `GetArea` 구현을 제공해야 합니다.  
  
 [!code-csharp[csrefKeywordsModifiers#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#1)]
  
 다음 기능이 있는 추상 클래스:  
  
- 추상 클래스는 인스턴스화할 수 없습니다.  
  
- 추상 클래스에 추상 메서드 및 접근자가 포함될 수 있습니다.  
  
- [sealed](./sealed.md) 한정자를 사용하여 추상 클래스를 수정할 수는 없습니다. 두 한정자가 상반된 의미가 있기 때문입니다. `sealed` 한정자를 사용하면 클래스가 상속되지 않고 `abstract` 한정자를 사용하려면 클래스가 상속되어야 합니다.  
  
- 추상 클래스에서 추상이 아닌 파생 클래스에는 모든 상속된 메서드 및 접근자의 실제 구현이 포함되어야 합니다.  
  
 메서드 또는 속성 선언에서 `abstract` 한정자를 사용하여 메서드 또는 속성에 구현이 포함되지 않음을 나타냅니다.  
  
 추상 메서드에는 다음과 같은 기능이 있습니다.  
  
- 추상 메서드는 암시적으로 가상 메서드입니다.  
  
- 추상 메서드 선언은 추상 클래스에서만 허용됩니다.  
  
- 추상 메서드 선언은 실제 구현을 제공하지 않으므로 메서드 본문이 없습니다. 메서드 선언은 세미콜론으로 끝나고 시그니처 뒤에 중괄호({ })가 없습니다. 예:  
  
    ```csharp  
    public abstract void MyMethod();  
    ```  
  
     구현은 비추상 클래스의 멤버인 메서드 [override](./override.md)에 의해 제공됩니다.  
  
- 추상 메서드 선언에서 [static](./static.md) 또는 [virtual](./virtual.md) 한정자를 사용하는 것은 오류입니다.  
  
 선언 및 호출 구문의 차이점을 제외하고 추상 속성은 추상 메서드처럼 동작합니다.  
  
- 정적 속성에서 `abstract` 한정자를 사용하는 것은 오류입니다.  
  
- [override](./override.md) 한정자를 사용하는 속성 선언을 포함하여 상속된 추상 속성을 파생 클래스에서 재정의할 수 있습니다.  
  
 추상 클래스에 대한 자세한 내용은 [추상 및 봉인 클래스와 클래스 멤버](../../programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md)를 참조하세요.  
  
 추상 클래스는 모든 인터페이스 멤버에 대한 구현을 제공해야 합니다.  
  
 인터페이스를 구현하는 추상 클래스는 인터페이스 메서드를 추상 메서드에 매핑할 수 있습니다. 예:  
  
[!code-csharp[csrefKeywordsModifiers#2](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#2)]
  
## <a name="example"></a>예  
 이 예제에서 `DerivedClass` 클래스는 추상 클래스 `BaseClass`에서 파생됩니다. 추상 클래스에는 추상 메서드 `AbstractMethod` 및 두 개의 추상 속성 `X` 및 `Y`가 포함됩니다.  
  
[!code-csharp[csrefKeywordsModifiers#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#3)]
  
 앞의 예제에서 다음과 같이 문을 사용하여 추상 클래스를 인스턴스화하려고 하면,  
  
```csharp
BaseClass bc = new BaseClass();   // Error  
```  
  
컴파일러가 추상 클래스 'BaseClass'의 인스턴스를 만들 수 없다는 오류가 표시됩니다.  
  
## <a name="c-language-specification"></a>C# 언어 사양  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [한정자](./modifiers.md)
- [virtual](./virtual.md)
- [override](./override.md)
- [C# 키워드](./index.md)
