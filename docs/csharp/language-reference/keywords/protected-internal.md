---
title: protected internal(C# 참조)
ms.date: 11/15/2017
author: sputier
ms.openlocfilehash: e5763830a29d4e627dbb8efa0e86fca536bbb26c
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50193775"
---
# <a name="protected-internal-c-reference"></a>protected internal(C# 참조)

`protected internal` 키워드 조합은 멤버 액세스 한정자입니다. protected internal 멤버는 포함하는 클래스에서 파생된 형식이나 현재 어셈블리에서 액세스할 수 있습니다. `protected internal` 및 다른 액세스 한정자와 비교는 [액세스 가능성 수준](accessibility-levels.md)을 참조하세요.

## <a name="example"></a>예

기본 클래스의 protected internal 멤버는 포함하는 어셈블리 내의 모든 형식에서 액세스할 수 있습니다. 또한 액세스가 파생된 클래스 형식의 변수를 통해 발생하는 경우에만 다른 어셈블리에 있는 파생 클래스에서 액세스할 수 있습니다. 예를 들어 다음 코드 세그먼트를 고려하세요.

```csharp
// Assembly1.cs
// Compile with: /target:library
public class BaseClass
{
   protected internal int myValue = 0;
}

class TestAccess
{
    void Access()
    {
        BaseClass baseObject = new BaseClass();
        baseObject.myValue = 5;
    }
}
```

```csharp
// Assembly2.cs
// Compile with: /reference:Assembly1.dll
class DerivedClass : BaseClass
{
    static void Main()
    {
        BaseClass baseObject = new BaseClass();
        DerivedClass derivedObject = new DerivedClass();

        // Error CS1540, because myValue can only be accessed by
        // classes derived from BaseClass.
        // baseObject.myValue = 10;

        // OK, because this class derives from BaseClass.
        derivedObject.myValue = 10;
    }
}
```
이 예제에는 `Assembly1.cs` 및 `Assembly2.cs`의 두 파일이 포함되어 있습니다.
첫 번째 파일은 공용 기본 클래스인 `BaseClass`와 다른 클래스인 `TestAccess`을 포함합니다. `BaseClass`는 `TestAccess` 형식으로 액세스되는 protected internal 멤버인 `myValue`를 소유합니다.
두 번째 파일에서 `BaseClass`의 인스턴스를 통한 `myValue` 액세스의 시도는 오류를 생성하지만 파생된 클래스 `DerivedClass`의 인스턴스를 통한 이 멤버로의 액세스는 성공합니다.

구조체를 상속할 수 없기 때문에 구조체 멤버는 `protected internal`일 수 없습니다.

## <a name="c-language-specification"></a>C# 언어 사양

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [C# 키워드](index.md)
- [액세스 한정자](access-modifiers.md)
- [액세스 수준](accessibility-levels.md)
- [한정자](modifiers.md)
- [public](public.md)
- [private](private.md)
- [internal](internal.md)
- [internal virtual 키워드에 대한 보안 문제](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/heyd8kky(v=vs.100))