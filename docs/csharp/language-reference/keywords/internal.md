---
title: internal - C# 참조
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- internal_CSharpKeyword
- internal
helpviewer_keywords:
- internal keyword [C#]
ms.assetid: 6ee0785c-d7c8-49b8-bb72-0a4dfbcb6461
ms.openlocfilehash: 7d97b7b05645b02a31af848c97758c7a1f6423b9
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2019
ms.locfileid: "69602078"
---
# <a name="internal-c-reference"></a>internal(C# 참조)
`internal` 키워드는 형식 및 형식 멤버에 대한 [액세스 한정자](./access-modifiers.md)입니다. 
  
 > 이 페이지에서는 `internal` 액세스를 설명합니다. `internal` 키워드는 [`protected internal`](./protected-internal.md) 액세스 한정자의 일부이기도 합니다.
  
내부 형식 또는 멤버는 다음 예제와 같이 동일한 어셈블리의 파일 내에서만 액세스할 수 있습니다.  
  
```csharp  
public class BaseClass   
{  
    // Only accessible within the same assembly.
    internal static int x = 0;
}  
```  

 `internal` 및 다른 액세스 한정자와 비교는 [액세스 가능성 수준](./accessibility-levels.md) 및 [액세스 한정자](../../programming-guide/classes-and-structs/access-modifiers.md)를 참조하세요.  
  
 어셈블리에 대한 자세한 내용은 [.NET 어셈블리](../../../standard/assembly/index.md)를 참조하세요.  
  
 내부 액세스는 구성 요소 그룹이 나머지 애플리케이션 코드에 노출되지 않고 비공개 방식으로 상호 작용할 수 있도록 하기 때문에 일반적으로 구성 요소 기반 개발에 사용됩니다. 예를 들어 그래픽 사용자 인터페이스를 빌드하기 위한 프레임워크는 내부 액세스로 멤버를 사용하여 상호 작용하는 `Control` 및 `Form` 클래스를 제공할 수 있습니다. 이러한 멤버는 internal이므로 프레임워크를 사용하는 코드에 노출되지 않습니다.  
  
 정의 시 사용된 어셈블리 외부에서 내부 액세스로 형식 또는 멤버를 참조하면 오류가 발생합니다.  
  
## <a name="example"></a>예  
 이 예제에는 `Assembly1.cs` 및 `Assembly1_a.cs`의 두 파일이 포함되어 있습니다. 첫 번째 파일에는 내부 기본 클래스인 `BaseClass`가 포함되어 있습니다. 두 번째 파일에서 `BaseClass`를 인스턴스화하려고 하면 오류가 발생합니다.  
  
```csharp  
// Assembly1.cs  
// Compile with: /target:library  
internal class BaseClass   
{  
   public static int intM = 0;  
}  
```  
  
```csharp  
// Assembly1_a.cs  
// Compile with: /reference:Assembly1.dll  
class TestAccess   
{  
   static void Main()   
   {  
      var myBase = new BaseClass();   // CS0122  
   }  
}  
```  
  
## <a name="example"></a>예  
 이 예제에서는 예제 1에서 사용한 것과 동일한 파일을 사용하고 `BaseClass`의 액세스 가능성 수준을 `public`으로 변경합니다. 또한 `intM` 멤버의 액세스 가능성 수준을 `internal`로 변경합니다. 이 경우 클래스를 인스턴스화할 수 있지만 내부 멤버에는 액세스할 수 없습니다.  
  
```csharp  
// Assembly2.cs  
// Compile with: /target:library  
public class BaseClass   
{  
   internal static int intM = 0;  
}  
```  
  
```csharp  
// Assembly2_a.cs  
// Compile with: /reference:Assembly2.dll  
public class TestAccess   
{  
   static void Main()   
   {  
      var myBase = new BaseClass();   // Ok.  
      BaseClass.intM = 444;    // CS0117  
   }  
}  
```  
  
## <a name="c-language-specification"></a>C# 언어 사양  

자세한 내용은 [C# 언어 사양](../language-specification/index.md)의 [선언된 내게 필요한 옵션](~/_csharplang/spec/basic-concepts.md#declared-accessibility)을 참조하세요. C# 언어 사양은 C# 구문 및 사용법에 대한 신뢰할 수 있는 소스입니다.
  
## <a name="see-also"></a>참고 항목

- [C# 참조](../index.md)
- [C# 프로그래밍 가이드](../../programming-guide/index.md)
- [C# 키워드](./index.md)
- [액세스 한정자](./access-modifiers.md)
- [액세스 수준](./accessibility-levels.md)
- [한정자](./modifiers.md)
- [public](./public.md)
- [private](./private.md)
- [protected](./protected.md)
