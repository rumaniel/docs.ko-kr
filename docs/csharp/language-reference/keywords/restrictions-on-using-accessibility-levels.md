---
title: 액세스 가능성 수준 사용에 대한 제한 - C# 참조
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- access modifiers [C#], accessibility level restrictions
ms.assetid: 987e2f22-46bf-4fea-80ee-270b9cd01045
ms.openlocfilehash: 13adfbb96cea2c192b84931b529bf92fd2b50116
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69922325"
---
# <a name="restrictions-on-using-accessibility-levels-c-reference"></a>액세스 가능성 수준 사용에 대한 제한(C# 참조)

선언에서 형식을 지정하는 경우, 형식의 액세스 가능성 수준이 멤버 또는 다른 형식의 액세스 가능성 수준에 따라 달라지는지를 확인합니다. 예를 들어 직접 기본 클래스는 적어도 파생 클래스 수준만큼 액세스 가능해야 합니다. 다음 선언에서는 기본 클래스 `BaseClass`가 `MyClass`보다 액세스 가능성이 낮기 때문에 컴파일러 오류가 발생합니다.

```csharp
class BaseClass {...}
public class MyClass: BaseClass {...} // Error
```

다음 표에는 선언된 액세스 가능성 수준에 대한 제한이 요약되어 있습니다.

|컨텍스트|설명|
|-------------|-------------|
|[클래스](../../programming-guide/classes-and-structs/classes.md)|클래스 형식의 직접 기본 클래스는 적어도 클래스 형식 자체 수준만큼 액세스 가능해야 합니다.|
|[인터페이스](../../programming-guide/interfaces/index.md)|인터페이스 형식의 명시적 기본 인터페이스는 적어도 인터페이스 형식 자체 수준만큼 액세스 가능해야 합니다.|
|[대리자](../../programming-guide/delegates/index.md)|대리자 형식의 반환 형식 및 매개 변수 형식은 적어도 대리자 형식 자체 수준만큼 액세스 가능해야 합니다.|
|[상수](../../programming-guide/classes-and-structs/constants.md)|상수의 형식은 적어도 상수 자체 수준만큼 액세스 가능해야 합니다.|
|[필드](../../programming-guide/classes-and-structs/fields.md)|필드의 형식은 적어도 필드 자체 수준만큼 액세스 가능해야 합니다.|
|[메서드](../../programming-guide/classes-and-structs/methods.md)|메서드의 반환 형식 및 매개 변수 형식은 적어도 메서드 자체 수준만큼 액세스 가능해야 합니다.|
|[속성](../../programming-guide/classes-and-structs/properties.md)|속성의 형식은 적어도 속성 자체 수준만큼 액세스 가능해야 합니다.|
|[이벤트](../../programming-guide/events/index.md)|이벤트의 형식은 적어도 이벤트 자체 수준만큼 액세스 가능해야 합니다.|
|[인덱서](../../programming-guide/indexers/index.md)|인덱서의 형식 및 매개 변수 형식은 적어도 인덱서 자체 수준만큼 액세스 가능해야 합니다.|
|[연산자](../operators/index.md)|연산자의 반환 형식 및 매개 변수 형식은 적어도 연산자 자체 수준만큼 액세스 가능해야 합니다.|
|[생성자](../../programming-guide/classes-and-structs/constructors.md)|생성자의 매개 변수 형식은 적어도 생성자 자체 수준만큼 액세스 가능해야 합니다.|

## <a name="example"></a>예

다음 예제에는 다양한 종류의 잘못된 선언이 포함되어 있습니다. 각 선언 다음의 주석은 예상된 컴파일러 오류를 나타냅니다.

```csharp
// Restrictions on Using Accessibility Levels
// CS0052 expected as well as CS0053, CS0056, and CS0057
// To make the program work, change access level of both class B
// and MyPrivateMethod() to public.

using System;

// A delegate:
delegate int MyDelegate();

class B
{
    // A private method:
    static int MyPrivateMethod()
    {
        return 0;
    }
}

public class A
{
    // Error: The type B is less accessible than the field A.myField.
    public B myField = new B();

    // Error: The type B is less accessible
    // than the constant A.myConst.
    public readonly B myConst = new B();

    public B MyMethod()
    {
        // Error: The type B is less accessible 
        // than the method A.MyMethod.
        return new B();
    }

    // Error: The type B is less accessible than the property A.MyProp
    public B MyProp
    {
        set
        {
        }
    }

    MyDelegate d = new MyDelegate(B.MyPrivateMethod);
    // Even when B is declared public, you still get the error: 
    // "The parameter B.MyPrivateMethod is not accessible due to 
    // protection level."

    public static B operator +(A m1, B m2)
    {
        // Error: The type B is less accessible
        // than the operator A.operator +(A,B)
        return new B();
    }

    static void Main()
    {
        Console.Write("Compiled successfully");
    }
}
```

## <a name="c-language-specification"></a>C# 언어 사양

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>참고 항목

- [C# 참조](../../language-reference/index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [C# 키워드](../../language-reference/keywords/index.md)
- [액세스 한정자](../../language-reference/keywords/access-modifiers.md)
- [접근성 도메인](../../language-reference/keywords/accessibility-domain.md)
- [액세스 수준](../../language-reference/keywords/accessibility-levels.md)
- [액세스 한정자](../../programming-guide/classes-and-structs/access-modifiers.md)
- [public](../../language-reference/keywords/public.md)
- [private](../../language-reference/keywords/private.md)
- [protected](../../language-reference/keywords/protected.md)
- [internal](../../language-reference/keywords/internal.md)
