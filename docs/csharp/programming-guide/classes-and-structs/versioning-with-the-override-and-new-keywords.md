---
title: Override 및 New 키워드를 사용하여 버전 관리 - C# 프로그래밍 가이드
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- C# language, versioning
- C# language, override and new
ms.assetid: 88247d07-bd0d-49e9-a619-45ccbbfdf0c5
ms.openlocfilehash: 58023498c499569eebb9a0506bea434d2669de45
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69596003"
---
# <a name="versioning-with-the-override-and-new-keywords-c-programming-guide"></a>Override 및 New 키워드를 사용하여 버전 관리(C# 프로그래밍 가이드)
C# 언어는 서로 다른 라이브러리의 [기본](../../language-reference/keywords/base.md) 및 파생 클래스 간 버전 관리를 개발하고 이전 버전과의 호환성을 유지할 수 있도록 설계되었습니다. 예를 들어 파생 클래스의 멤버와 동일한 이름을 가진 기본 [클래스](../../language-reference/keywords/class.md)에 새 멤버가 추가되면 C#이 완전히 지원되고 예기치 않은 동작이 발생하지 않습니다. 따라서 클래스는 메서드가 상속된 메서드를 재정의할지 아니면 메서드가 유사한 이름의 상속된 메서드를 숨기는 새 메서드인지를 명시적으로 지정해야 합니다.  
  
 C#에서 파생 클래스는 기본 클래스 메서드와 동일한 이름 가진 메서드를 포함할 수 있습니다.  
  
- 기본 클래스 메서드를 [virtual](../../language-reference/keywords/virtual.md)로 정의해야 합니다.  
  
- 파생 클래스의 메서드 앞에 [new](../../language-reference/keywords/new-modifier.md) 또는 [override](../../language-reference/keywords/override.md) 키워드가 있으면 컴파일러는 경고를 표시하고 메서드는 `new` 키워드가 있는 것처럼 작동합니다.  
  
- 파생 클래스의 메서드 앞에 `new` 키워드가 있는 경우 이 메서드는 기본 클래스의 메서드와 독립적으로 정의됩니다.  
  
- 파생 클래스의 메서드 앞에 `override` 키워드가 있는 경우 파생 클래스의 개체는 기본 클래스 메서드 대신 해당 메서드를 호출합니다.  
  
- 기본 클래스 메서드는 `base` 키워드를 사용하여 파생 클래스 내에서 호출할 수 있습니다.  
  
- `override`, `virtual`, 및 `new` 키워드는 속성, 인덱서 및 이벤트에도 적용될 수 있습니다.  
  
 기본적으로 C# 메서드는 가상입니다. 메서드가 가상으로 선언되면 이 메서드를 상속하는 클래스는 자체 버전을 구현할 수 있습니다. 메서드를 가상으로 만들려면 기본 클래스의 메서드 선언에서 `virtual` 한정자를 사용합니다. 파생 클래스는 `override` 키워드를 사용하여 기본 가상 메서드를 재정의하거나 `new` 키워드를 사용하여 기본 클래스에서 가상 메서드를 숨길 수 있습니다. `override` 키워드와 `new` 키워드가 모두 지정되지 않은 경우 컴파일러는 경고를 표시하고 파생 클래스의 메서드는 기본 클래스의 메서드를 숨깁니다.  
  
 이를 실증적으로 보여 주기 위해, A 회사가 프로그램에서 사용하는 `GraphicsClass`라는 클래스를 만들었다고 잠시 가정해 보겠습니다. 다음은 `GraphicsClass`입니다.  
  
 [!code-csharp[csProgGuideInheritance#27](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#27)]  
  
 회사에서 이 클래스를 사용하며, 사용자는 이를 사용하여 고유한 클래스를 파생시키고 새 메서드를 추가합니다.  
  
 [!code-csharp[csProgGuideInheritance#28](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#28)]  
  
 회사 A에서 `GraphicsClass`의 새 버전을 출시할 때까지 애플리케이션은 문제없이 사용됩니다. 새 버전은 다음 코드와 유사합니다.  
  
 [!code-csharp[csProgGuideInheritance#29](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#29)]  
  
 `GraphicsClass`의 새 버전에는 이제 `DrawRectangle`이라는 메서드가 포함되어 있습니다. 처음에는 아무것도 발생하지 않습니다. 새 버전은 여전히 이전 버전과 호환되는 이진입니다. 새 클래스가 해당 컴퓨터 시스템에 설치되어 있어도 사용자가 배포한 소프트웨어는 계속 작동합니다. `DrawRectangle` 메서드에 대한 호출은 파생 클래스에서 계속 해당 버전을 참조합니다.  
  
 그러나 `GraphicsClass`의 새 버전을 사용하여 애플리케이션을 다시 컴파일하자마자 컴파일러에서 경고(CS0108)를 표시합니다. 이 경고는 `DrawRectangle` 메서드가 애플리케이션에서 어떻게 작동할지를 고려해야 한다고 알립니다.  
  
 메서드가 새로운 기본 클래스 메서드를 재정의하도록 하려면 `override` 키워드를 사용합니다.  
  
 [!code-csharp[csProgGuideInheritance#30](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#30)]  
  
 `override` 키워드는 `YourDerivedGraphicsClass`에서 파생된 개체가 `DrawRectangle`의 파생 클래스 버전을 사용하도록 합니다. `YourDerivedGraphicsClass`에서 파생된 개체는 기본 키워드를 사용하여 여전히 `DrawRectangle`의 기본 클래스 버전에 액세스할 수 있습니다.  
  
 [!code-csharp[csProgGuideInheritance#44](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#44)]  
  
 메서드가 새 기본 클래스 메서드를 재정의하도록 하지 않으려면 다음 고려 사항을 적용하세요. 두 메서드 간 혼동을 피하려면 메서드의 이름을 바꿀 수 있습니다. 이 방법은 시간이 오래 걸리고 오류가 발생하기 쉬우며 어떤 경우에는 실용적이지 않습니다. 그러나 프로젝트 규모가 비교적 작으면 Visual Studio 리팩터링 옵션을 사용하여 메서드의 이름을 바꿀 수 있습니다. 자세한 내용은 [클래스 및 형식 리팩터링(클래스 디자이너)](/visualstudio/ide/refactoring-classes-and-types-class-designer)을 참조하세요.  
  
 또는 파생 클래스 정의에서 `new` 키워드를 사용하여 경고를 방지할 수 있습니다.  
  
 [!code-csharp[csProgGuideInheritance#31](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#31)]  
  
 `new` 키워드는 사용자 정의가 기본 클래스에 포함된 정의를 숨긴다는 것을 컴파일러에 알립니다. 이것은 기본적인 동작입니다.  
  
## <a name="override-and-method-selection"></a>재정의 및 메서드 선택  
 클래스에서 메서드 이름을 지정할 때, 동일한 이름을 가진 두 개의 메서드가 있고 전달된 매개 변수와 호환되는 매개 변수가 있는 경우와 같이 둘 이상의 메서드가 호출과 호환되는 경우, C# 컴파일러는 호출할 수 있는 최상의 메서드를 선택합니다. 다음 메서드는 호환 가능합니다.  
  
 [!code-csharp[csProgGuideInheritance#32](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#32)]  
  
 `Derived`의 인스턴스에서 `DoWork`가 호출되면 C# 컴파일러는 호출이 원래 `Derived`에 선언된 `DoWork` 버전과 호환되도록 만들려고 시도합니다. 재정의 메서드는 클래스에서 선언된 것으로 간주되지 않습니다. 재정의 메서드는 기본 클래스에서 선언된 메서드의 새로운 구현입니다. C# 컴파일러는 메서드 호출을 `Derived`의 원래 메서드와 일치시킬 수 없는 경우에만, 재정의된 메서드에 대한 호출을 동일한 이름 및 호환되는 매개 변수와 일치시키려고 시도합니다. 예:  
  
 [!code-csharp[csProgGuideInheritance#33](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#33)]  
  
 `val` 변수를 double로 암시적으로 변환할 수 있으므로 C# 컴파일러는 `DoWork(int)` 대신 `DoWork(double)`을 호출합니다. 이것을 방지할 수 있는 두 가지 방법이 있습니다. 첫째, 가상 메서드와 동일한 이름을 가진 새 메서드를 선언하지 않습니다. 둘째, `Derived`의 인스턴스를 `Base`에 캐스팅하여 기본 클래스 메서드 목록을 검색하게 함으로써 가상 메서드를 호출하도록 C# 컴파일러에 지시할 수 있습니다. 메서드는 가상이므로 `Derived`에서 `DoWork(int)`의 구현이 호출됩니다. 예:  
  
 [!code-csharp[csProgGuideInheritance#34](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideInheritance/CS/Inheritance.cs#34)]  
  
 `new` 및 `override`의 추가 예제는 [Override 및 New 키워드를 사용해야 하는 경우](./knowing-when-to-use-override-and-new-keywords.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../index.md)
- [클래스 및 구조체](./index.md)
- [메서드](./methods.md)
- [상속](./inheritance.md)
