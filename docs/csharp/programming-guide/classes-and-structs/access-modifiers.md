---
title: 액세스 한정자(C# 프로그래밍 가이드)
ms.date: 07/20/2015
helpviewer_keywords:
- C# Language, access modifiers
- access modifiers [C#], about
ms.assetid: 6e81ee82-224f-4a12-9baf-a0dca2656c5b
ms.openlocfilehash: 6be0ae4f6497dfb2db9607f61c4ede5083d57dc7
ms.sourcegitcommit: ea00c05e0995dae928d48ead99ddab6296097b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48036255"
---
# <a name="access-modifiers-c-programming-guide"></a>액세스 한정자(C# 프로그래밍 가이드)
모든 형식과 형식 멤버에는 사용 중인 어셈블리나 기타 어셈블리의 다른 코드에서 사용될 수 있는지 여부를 제어하는 액세스 가능성 수준이 있습니다. 다음 액세스 한정자를 사용하여 형식 또는 멤버를 선언할 때 해당 항목의 액세스 가능성을 지정할 수 있습니다.  
  
 [public](../../../csharp/language-reference/keywords/public.md)  
 동일한 어셈블리의 다른 코드나 해당 어셈블리를 참조하는 다른 어셈블리의 코드에서 형식이나 멤버에 액세스할 수 있습니다. 
  
 [private](../../../csharp/language-reference/keywords/private.md)  
 같은 클래스 또는 구조체의 코드에서만 형식 또는 멤버에 액세스할 수 있습니다.  
  
 [protected](../../../csharp/language-reference/keywords/protected.md)  
 같은 클래스 또는 해당 클래스에서 파생된 클래스의 코드에서만 형식 또는 멤버에 액세스할 수 있습니다.  
 [internal](../../../csharp/language-reference/keywords/internal.md)  
 동일한 어셈블리의 코드에서는 형식이나 멤버에 액세스할 수 있지만 다른 어셈블리의 코드에서는 액세스할 수 없습니다.  
  
 [protected internal](../../../csharp/language-reference/keywords/protected-internal.md) 형식이나 멤버가 선언된 어셈블리의 모든 코드에서 또는 다른 어셈블리의 파생 클래스 내에서 형식 또는 멤버에 액세스할 수 있습니다. 

 [private protected](../../../csharp/language-reference/keywords/private-protected.md) 형식이나 멤버를 선언하는 어셈블리, 같은 클래스나 해당 클래스에서 파생된 형식의 코드에서만 형식 또는 멤버에 액세스할 수 있습니다.
  
 다음 예제에서는 형식 및 멤버에 대해 액세스 한정자를 지정하는 방법을 보여 줍니다.  
  
 [!code-csharp[csProgGuideObjects#72](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/access-modifiers_1.cs)]  
  
 모든 액세스 한정자를 모든 컨텍스트의 모든 형식이나 멤버에서 사용할 수 있는 것은 아니며, 경우에 따라 형식 멤버의 액세스 가능성이 포함하는 형식의 액세스 가능성에 의해 제한됩니다. 다음 섹션에서는 액세스 가능성을 자세히 설명합니다.  
  
## <a name="class-and-struct-accessibility"></a>클래스 및 구조체 액세스 가능성  
 네임스페이스 내에서 직접 선언된(다른 클래스 또는 구조체 내에 중첩되지 않은) 클래스와 구조체는 public 또는 internal 중 하나일 수 있습니다. 액세스 한정자가 지정되지 않은 경우 internal이 기본값입니다.  
  
 중첩 클래스 및 구조체를 포함한 구조체 멤버는 public, internal 또는 private으로 선언될 수 있습니다. 중첩 클래스 및 구조체를 포함한 클래스 멤버는 public, protected internal, protected, internal, private protected 또는 private일 수 있습니다. 중첩 클래스 및 구조체를 포함한 클래스 멤버와 구조체 멤버의 액세스 수준은 기본적으로 private입니다. 포함하는 형식 외부에서는 private 중첩 형식에 액세스할 수 없습니다.  
  
 파생 클래스는 기본 형식보다 큰 액세스 가능성을 가질 수 없습니다. 즉, public 클래스 `B`는 internal 클래스 `A`에서 파생될 수 없습니다. 파생될 수 있다면 파생 클래스에서 `A`의 모든 protected 또는 internal 멤버에 액세스할 수 있기 때문에 결과적으로 `A`가 public으로 설정됩니다.  
  
 다른 특정 어셈블리에서는 InternalsVisibleToAttribute를 사용하여 internal 형식에 액세스할 수 있습니다. 자세한 내용은 [Friend Assemblies](../concepts/assemblies-gac/friend-assemblies.md)(Friend 어셈블리)를 참조하세요.  
  
## <a name="class-and-struct-member-accessibility"></a>클래스 및 구조체 멤버 액세스 가능성  
 중첩 클래스 및 구조체를 포함한 클래스 멤버는 6가지 액세스 형식으로 선언될 수 있습니다. 구조체는 상속을 지원하지 않으므로 구조체 멤버는 protected로 선언될 수 없습니다.  
  
 일반적으로 멤버의 액세스 가능성은 멤버를 포함하는 형식의 액세스 가능성보다 크지 않습니다. 그러나 멤버가 인터페이스 메서드를 구현하거나 public 기본 클래스에 정의된 가상 메서드를 재정의하는 경우에는 어셈블리 외부에서 internal 클래스의 public 멤버에 액세스할 수 있습니다.  
  
 필드, 속성 또는 이벤트인 멤버의 형식은 최소한 멤버 자체만큼 액세스할 수 있어야 합니다. 마찬가지로 메서드, 인덱서 또는 대리자인 멤버의 반환 형식과 매개 변수 형식은 최소한 멤버 자체만큼 액세스할 수 있어야 합니다. 예를 들어 `C` 클래스도 public인 경우에만 public 메서드 `M`이 `C` 클래스를 반환할 수 있습니다. 마찬가지로 `A` 형식이 private으로 선언되면 `A` 형식에는 protected 속성은 있을 수 없습니다.  
  
 사용자 정의 연산자는 public으로 선언되어야 합니다. 자세한 내용은 [연산자(C# 참조)](../../../csharp/language-reference/keywords/operator.md)를 참조하세요.  
  
 종료자에는 접근성 한정자를 사용할 수 없습니다.  
  
 클래스 또는 구조체 멤버의 액세스 수준을 설정하려면 다음 예제와 같이 멤버 선언에 해당 키워드를 추가합니다.  
  
 [!code-csharp[csProgGuideObjects#73](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/access-modifiers_2.cs)]  
  
> [!NOTE]
>  protected internal 액세스 가능성 수준은 protected 및 internal이 아니라 protected 또는 internal을 의미합니다. 즉, 파생 클래스를 포함하여 같은 어셈블리의 모든 클래스에서 protected internal 멤버에 액세스할 수 있습니다. 액세스 가능성을 같은 어셈블리 파생 클래스로만 제한하려면 클래스 자체를 internal로 선언하고 해당 멤버를 protected로 선언합니다. 또한 C# 7.2부터 private protected 액세스 한정자를 사용하여 포함하는 클래스를 internal로 만들 필요 없이 같은 결과를 얻을 수 있습니다.  
  
## <a name="other-types"></a>기타 형식  
 네임스페이스 내에서 직접 선언된 인터페이스는 public 또는 internal로 선언될 수 있고 클래스 및 구조체처럼 인터페이스는 기본적으로 internal 액세스로 설정됩니다. 인터페이스는 다른 형식이 클래스나 구조체에 액세스하는 데 사용되므로 인터페이스 멤버는 항상 public입니다. 액세스 한정자는 인터페이스 멤버에 적용될 수 없습니다.  
  
 열거형 멤버는 항상 public이고 액세스 한정자가 적용될 수 없습니다.  
  
 대리자는 클래스 및 구조체처럼 동작합니다. 기본적으로 대리자는 네임스페이스 내에서 직접 선언될 경우 internal 액세스를 가지고 중첩될 경우 private 액세스를 가집니다.  
  
## <a name="c-language-specification"></a>C# 언어 사양  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)  
- [클래스 및 구조체](../../../csharp/programming-guide/classes-and-structs/index.md)  
- [인터페이스](../../../csharp/programming-guide/interfaces/index.md)  
- [private](../../../csharp/language-reference/keywords/private.md)  
- [public](../../../csharp/language-reference/keywords/public.md)  
- [internal](../../../csharp/language-reference/keywords/internal.md)  
- [protected](../../../csharp/language-reference/keywords/protected.md)  
- [protected internal](../../../csharp/language-reference/keywords/protected-internal.md)  
- [private protected](../../../csharp/language-reference/keywords/private-protected.md)  
- [class](../../../csharp/language-reference/keywords/class.md)  
- [struct](../../../csharp/language-reference/keywords/struct.md)  
- [interface](../../../csharp/language-reference/keywords/interface.md)
