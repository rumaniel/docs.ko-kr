---
title: 정적 클래스 및 정적 클래스 멤버(C# 프로그래밍 가이드)
ms.date: 07/20/2015
helpviewer_keywords:
- C# language, static members
- static members [C#]
- static classes [C#]
- C# language, static classes
- static class members [C#]
ms.assetid: 235614b5-1371-4dbd-9abd-b406a8b0298b
ms.openlocfilehash: 60a75946d30b1555aea01507d846e790dd00f767
ms.sourcegitcommit: 15d99019aea4a5c3c91ddc9ba23692284a7f61f3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49122724"
---
# <a name="static-classes-and-static-class-members-c-programming-guide"></a>정적 클래스 및 정적 클래스 멤버(C# 프로그래밍 가이드)
[정적](../../../csharp/language-reference/keywords/static.md) 클래스는 기본적으로 비정적 클래스와 동일하지만, 정적 클래스는 인스턴스화할 수 없다는 한 가지 차이점이 있습니다. 즉, [new](../../../csharp/language-reference/keywords/new.md) 키워드를 사용하여 클래스 형식의 변수를 만들 수 없습니다. 인스턴스 변수가 없기 때문에 클래스 이름 자체를 사용하여 정적 클래스의 멤버에 액세스합니다. 예를 들어 public 메서드 `MethodA`를 포함하는 `UtilityClass`라는 정적 클래스가 있는 경우 다음 예제와 같이 메서드를 호출합니다.  
  
```csharp  
UtilityClass.MethodA();  
```  
  
 정적 클래스는 입력 매개 변수에 대해서만 작동하고 내부 인스턴스 필드를 가져오거나 설정할 필요가 없는 메서드 집합에 대한 편리한 컨테이너로 사용할 수 있습니다. 예를 들어 .NET Framework 클래스 라이브러리의 정적 <xref:System.Math?displayProperty=nameWithType> 클래스에는 <xref:System.Math> 클래스의 특정 인스턴스에 고유한 데이터를 저장하거나 검색할 필요 없이 수학 연산을 수행하는 메서드가 포함되어 있습니다. 즉, 다음 예제와 같이 클래스 이름과 메서드 이름을 지정하여 클래스의 멤버를 적용합니다.  
  
```csharp  
double dub = -3.14;  
Console.WriteLine(Math.Abs(dub));  
Console.WriteLine(Math.Floor(dub));  
Console.WriteLine(Math.Round(Math.Abs(dub)));  
  
// Output:  
// 3.14  
// -4  
// 3  
```  
  
 모든 클래스 형식과 마찬가지로, 정적 클래스에 대한 형식 정보는 클래스를 참조하는 프로그램이 로드될 때 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] CLR(공용 언어 런타임)에 의해 로드됩니다. 프로그램에서 클래스가 로드되는 시기를 정확하게 지정할 수는 없습니다. 그러나 클래스가 로드되도록 하고, 프로그램에서 클래스를 처음으로 참조하기 전에 해당 필드가 초기화되고 정적 생성자가 호출되도록 합니다. 정적 생성자는 한 번만 호출되며, 프로그램이 있는 응용 프로그램 도메인의 수명 동안 정적 클래스가 메모리에 유지됩니다.  
  
> [!NOTE]
>  자체 인스턴스 하나만 생성될 수 있도록 하는 비정적 클래스를 만들려면 [C#에서 Singleton 구현](https://msdn.microsoft.com/library/ms998558.aspx)을 참조하세요.  
  
 다음 목록은 정적 클래스의 주요 기능을 제공합니다.  
  
-   정적 멤버만 포함합니다.  
  
-   인스턴스화할 수 없습니다.  
  
-   봉인되어 있습니다.  
  
-   [인스턴스 생성자](../../../csharp/programming-guide/classes-and-structs/instance-constructors.md)를 포함할 수 없습니다.  
  
 따라서 정적 클래스를 만드는 것은 기본적으로 정적 멤버와 private 생성자만 포함된 클래스를 만드는 것과 동일합니다. private 생성자는 클래스가 인스턴스화되지 않도록 합니다. 정적 클래스를 사용하면 컴파일러에서 인스턴스 멤버가 실수로 추가되지 않도록 확인할 수 있다는 장점이 있습니다. 컴파일러는 이 클래스의 인스턴스를 만들 수 없도록 합니다.  
  
 정적 클래스는 봉인되므로 상속할 수 없습니다. <xref:System.Object>를 제외하고 어떤 클래스에서도 상속할 수 없습니다. 정적 클래스는 인스턴스 생성자를 포함할 수 없지만 정적 생성자를 포함할 수 있습니다. 또한 클래스에 특수한 초기화가 필요한 정적 멤버가 포함된 경우 비정적 클래스에서 정적 생성자도 정의해야 합니다. 자세한 내용은 [정적 생성자](../../../csharp/programming-guide/classes-and-structs/static-constructors.md)를 참조하세요.  
  
## <a name="example"></a>예  
 온도를 섭씨에서 화씨로, 화씨에서 섭씨로 변환하는 두 메서드를 포함하는 정적 클래스의 예는 다음과 같습니다.  
  
 [!code-csharp[csProgGuideObjects#31](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/static-classes-and-static-class-members_1.cs)]  
  
## <a name="static-members"></a>정적 멤버  
 비정적 클래스는 정적 메서드, 필드, 속성 또는 이벤트를 포함할 수 있습니다. 정적 멤버는 클래스 인스턴스가 생성되지 않은 경우에도 클래스에 대해 호출할 수 있습니다. 정적 멤버는 항상 인스턴스 이름이 아니라 클래스 이름으로 액세스됩니다. 생성된 클래스 인스턴스 개수에 관계없이 정적 멤버의 복사본 한 개만 있습니다. 정적 메서드 및 속성은 포함하는 형식의 비정적 필드 및 이벤트에 액세스할 수 없으며, 메서드 매개 변수에 명시적으로 전달되지 않은 경우 개체의 인스턴스 변수에 액세스할 수 없습니다.  
  
 전체 클래스를 static으로 선언하는 것보다 일부 정적 멤버가 포함된 비정적 클래스를 선언하는 것이 더 일반적입니다. 정적 필드의 두 가지 일반적인 사용은 인스턴스화된 개체 개수를 유지하거나 모든 인스턴스 간에 공유해야 하는 값을 저장하는 것입니다.  
  
 정적 메서드는 클래스 인스턴스가 아니라 클래스에 속해 있으므로 오버로드할 수 있지만 재정의할 수 없습니다.  
  
 필드를 `static const`로 선언할 수는 없지만, [const](../../../csharp/language-reference/keywords/const.md) 필드는 기본적으로 정적으로 동작합니다. 형식의 인스턴스가 아니라 형식에 속합니다. 따라서 정적 필드에 사용되는 것과 동일한 `ClassName.MemberName` 표기법을 사용하여 const 필드에 액세스할 수 있습니다. 개체 인스턴스는 필요하지 않습니다.  
  
 C#은 정적 지역 변수(메서드 범위 내에서 선언된 변수)를 지원하지 않습니다.  
  
 다음 예제와 같이 멤버의 반환 형식 앞에 `static` 키워드를 사용하여 정적 클래스 멤버를 선언합니다.  
  
 [!code-csharp[csProgGuideObjects#29](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/static-classes-and-static-class-members_2.cs)]  
  
 정적 멤버는 정적 멤버를 처음으로 액세스하기 전, 정적 생성자가 있을 경우 호출되기 전에 초기화됩니다. 정적 클래스 멤버에 액세스하려면 다음 예제와 같이 변수 이름 대신 클래스 이름을 사용하여 멤버의 위치를 지정합니다.  
  
 [!code-csharp[csProgGuideObjects#30](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/static-classes-and-static-class-members_3.cs)]  
  
 클래스에 정적 필드가 포함된 경우 클래스가 로드될 때 정적 필드를 초기화하는 정적 생성자를 제공합니다.  
  
 정적 메서드를 호출하면 MSIL(Microsoft Intermediate Language)로 호출 명령이 생성되는 반면, 인스턴스 메서드를 호출하면 null 개체 참조도 확인하는 `callvirt` 명령이 생성됩니다. 그러나 대부분의 경우 둘 간의 성능 차이는 크지 않습니다.  
  
## <a name="c-language-specification"></a>C# 언어 사양  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)  
- [static](../../../csharp/language-reference/keywords/static.md)  
- [클래스](../../../csharp/programming-guide/classes-and-structs/classes.md)  
- [class](../../../csharp/language-reference/keywords/class.md)  
- [정적 생성자](../../../csharp/programming-guide/classes-and-structs/static-constructors.md)  
- [인스턴스 생성자](../../../csharp/programming-guide/classes-and-structs/instance-constructors.md)
