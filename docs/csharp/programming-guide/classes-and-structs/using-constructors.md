---
title: 생성자 사용 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- constructors [C#], about constructors
ms.assetid: 464253b2-fd5d-469a-836d-df0fdf2a43f7
ms.openlocfilehash: dab8466b4d40e318bbb9915c06ce4ac836c0ead0
ms.sourcegitcommit: 2d792961ed48f235cf413d6031576373c3050918
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/31/2019
ms.locfileid: "70205435"
---
# <a name="using-constructors-c-programming-guide"></a>생성자 사용(C# 프로그래밍 가이드)

[class](../../language-reference/keywords/class.md) 또는 [struct](../../language-reference/keywords/struct.md)가 만들어지면 생성자가 호출됩니다. 생성자는 클래스 또는 구조체와 이름이 같으며 일반적으로 새 개체의 데이터 멤버를 초기화합니다.  
  
 다음 예제에서는 간단한 생성자를 사용하여 `Taxi`란 이름의 클래스를 정의합니다. 그런 다음 [new](../../language-reference/operators/new-operator.md) 연산자를 사용하여 이 클래스를 인스턴스화합니다. 새 개체에 메모리가 할당된 직후 `new` 연산자가 `Taxi` 생성자를 호출합니다.  
  
 [!code-csharp[csProgGuideObjects#53](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#53)]  
  
 매개 변수가 없는 생성자를 *매개 변수 없는 생성자*라고 합니다. `new` 연산자를 사용하여 개체가 인스턴스화되고 `new`에 제공된 인수가 없을 때마다 매개 변수가 없는 생성자가 호출됩니다. 자세한 내용은 [인스턴스 생성자](./instance-constructors.md)를 참조하세요.  
  
 클래스가 [정적](../../language-reference/keywords/static.md)이 아닌 경우 생성자가 없는 클래스에는 클래스 인스턴스화를 사용할 수 있도록 C# 컴파일러에서 공용 매개 변수 없는 생성자가 제공됩니다. 자세한 내용은 [static 클래스 및 static 클래스 멤버](./static-classes-and-static-class-members.md)를 참조하세요.  
  
 다음과 같이 생성자를 비공개로 설정하여 클래스의 인스턴스화를 방지할 수 있습니다.  
  
 [!code-csharp[csProgGuideObjects#11](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#11)]  
  
 자세한 내용은 [전용 생성자](./private-constructors.md)를 참조하세요.  
  
 [struct](../../language-reference/keywords/struct.md) 형식의 생성자는 class 생성자와 비슷하지만, `structs`는 컴파일러에서 자동으로 제공되므로 명시적 매개 변수 없는 생성자를 포함할 수 없습니다. 이 생성자는 `struct`의 각 필드를 기본값으로 초기화합니다. 자세한 내용은 [기본값 표](../../language-reference/keywords/default-values-table.md)를 참조하세요. 그러나 이 매개 변수 없는 생성자는 `struct`가 `new`로 인스턴스화될 경우에만 호출됩니다. 예를 들어, 이 코드는 <xref:System.Int32>에 매개 변수 없는 생성자를 사용하므로 정수가 초기화되었음을 확신할 수 있습니다.  
  
```csharp  
int i = new int();  
Console.WriteLine(i);  
```  
  
 그러나 다음 코드는 `new`를 사용하지 않으므로, 그리고 초기화되지 않은 개체를 사용하려고 하므로 컴파일러 오류를 일으킵니다.  
  
```csharp  
int i;  
Console.WriteLine(i);  
```  
  
 또는 `structs` 기반의 개체(모든 기본 제공 숫자 형식 포함)를 초기화하거나 할당한 후 다음 예제와 같이 사용할 수 있습니다.  
  
```csharp  
int a = 44;  // Initialize the value type...  
int b;  
b = 33;      // Or assign it before using it.  
Console.WriteLine("{0}, {1}", a, b);  
```  
  
 따라서 값 형식에 대해 매개 변수 없는 생성자를 호출할 필요가 없습니다.  
  
 클래스와 `structs` 모두 매개 변수를 사용하는 생성자를 정의할 수 있습니다. 매개 변수를 사용하는 생성자는 `new` 문 또는 [base](../../language-reference/keywords/base.md) 문을 통해 호출해야 합니다. 클래스 및 `structs`는 여러 생성자를 정의할 수 있으며, 매개 변수 없는 생성자를 정의하는 데에는 둘 다 필요하지 않습니다. 예:  
  
 [!code-csharp[csProgGuideObjects#54](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#54)]  
  
 다음 문 중 하나를 사용하여 이 클래스를 만들 수 있습니다.  
  
 [!code-csharp[csProgGuideObjects#55](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#55)]  
  
 생성자는 `base` 키워드를 사용하여 기본 클래스의 생성자를 호출할 수 있습니다. 예:  
  
 [!code-csharp[csProgGuideObjects#56](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#56)]  
  
 이 예제에서는 생성자의 블록이 실행되기 전에 기본 클래스의 생성자가 호출됩니다. `base` 키워드는 매개 변수와 함께 또는 매개 변수 없이 사용할 수 있습니다. 생성자에 대한 매개 변수는 `base`에 대한 매개 변수로 또는 식의 일부로 사용할 수 있습니다. 자세한 내용은 [base](../../language-reference/keywords/base.md)를 참조하세요.  
  
 파생 클래스에서는 `base` 키워드를 사용해 매개 변수 없는 클래스 생성자를 명시적으로 호출하지 않으면, 기본 생성자(있는 경우)가 암시적으로 호출됩니다. 즉, 다음과 같은 생성자 선언은 실제로 동일합니다.  
  
 [!code-csharp[csProgGuideObjects#58](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#58)]  
  
 [!code-csharp[csProgGuideObjects#57](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#57)]  
  
 기본 클래스가 매개 변수 없는 생성자를 제공하지 않으면 파생 클래스는 `base`를 사용해 기본 생성자를 명시적으로 호출해야 합니다.  
  
 생성자는 [this](../../language-reference/keywords/this.md) 키워드를 사용해 동일한 개체의 다른 생성자를 호출할 수 있습니다. `base`와 마찬가지로 `this`도 매개 변수 유무와 상관없이 사용할 수 있으며, 생성자에 대한 매개 변수는 `this`에 대한 매개 변수로 또는 식의 일부로 사용할 수 있습니다. 예를 들어, 이전 예제의 두 번째 생성자는 `this`를 사용해 다시 작성할 수 있습니다.  
  
 [!code-csharp[csProgGuideObjects#59](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#59)]  
  
 이전 예제에서 `this` 키워드를 사용하면 이 생성자가 호출됩니다.  
  
 [!code-csharp[csProgGuideObjects#60](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideObjects/CS/Objects.cs#60)]  
  
 생성자는 [public](../../language-reference/keywords/public.md), [private](../../language-reference/keywords/private.md), [protected](../../language-reference/keywords/protected.md), [internal](../../language-reference/keywords/internal.md), [protected internal](../../language-reference/keywords/protected-internal.md) 또는 [private protected](../../language-reference/keywords/private-protected.md)로 표시될 수 있습니다. 이러한 액세스 한정자는 클래스의 사용자가 클래스를 생성하는 방법을 정의합니다. 자세한 내용은 [액세스 한정자](./access-modifiers.md)를 참조하세요.  
  
 [static](../../language-reference/keywords/static.md) 키워드를 사용하여 생성자를 정적으로 선언할 수 있습니다. 정적 생성자는 정적 필드에 액세스하기 직전에 자동으로 호출되며 일반적으로 정적 클래스 멤버를 초기화하는 데 사용됩니다. 자세한 내용은 [정적 생성자](./static-constructors.md)를 참조하세요.  
  
## <a name="c-language-specification"></a>C# 언어 사양  

자세한 내용은 [C# 언어 사양](../../language-reference/language-specification/index.md)의 [인스턴스 생성자](~/_csharplang/spec/classes.md#instance-constructors) 및 [정적 생성자](~/_csharplang/spec/classes.md#static-constructors)를 참조하세요. 언어 사양은 C# 구문 및 사용법에 대 한 신뢰할 수 있는 소스 됩니다.
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [클래스 및 구조체](./index.md)
- [생성자](./constructors.md)
- [종료자](./destructors.md)
