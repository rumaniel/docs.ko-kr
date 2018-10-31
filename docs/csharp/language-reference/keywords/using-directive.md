---
title: using 지시문(C# 참조)
ms.date: 07/20/2015
helpviewer_keywords:
- using directive [C#]
ms.assetid: b42b8e61-5e7e-439c-bb71-370094b44ae8
ms.openlocfilehash: d3fa8a1a1b378fe1e18a63fec1c0d2f9eb40ecb3
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50181058"
---
# <a name="using-directive-c-reference"></a>using 지시문(C# 참조)
`using` 지시문에는 다음 세 가지 용도가 있습니다.  
  
-   네임스페이스에서 형식 사용을 한정할 필요가 없도록 해당 네임스페이스에서 형식 사용을 허용합니다.  
  
    ```csharp  
    using System.Text;  
    ```  
  
-   형식 이름을 사용하여 액세스를 한정할 필요 없이 형식의 정적 멤버 및 중첩 형식에 액세스하도록 허용합니다. 
  
    ```csharp  
    using static System.Math;  
    ```  
     
    자세한 내용은 [using 정적 지시문](using-static.md)을 참조하세요.

-   네임스페이스 또는 형식에 대한 별칭을 만듭니다. 이를 *using 별칭 지시문*이라고 합니다.  
  
    ```csharp  
    using Project = PC.MyCompany.Project;  
    ```  
  
 `using` 키워드는 파일 및 글꼴과 같은 <xref:System.IDisposable> 개체가 제대로 처리될 수 있게 도와주는 *using 문*을 만드는 데도 사용됩니다. 자세한 내용은 [using 문](../../../csharp/language-reference/keywords/using-statement.md)을 참조하세요.  
  
## <a name="using-static-type"></a>정적 형식 사용  
 형식 이름을 사용하여 액세스를 한정할 필요 없이 형식의 정적 멤버에 액세스할 수 있습니다.  
  
```csharp  
using static System.Console;   
using static System.Math;  
class Program   
{   
    static void Main()   
    {   
        WriteLine(Sqrt(3*3 + 4*4));   
    }   
}  
```  
  
## <a name="remarks"></a>설명  
 `using` 지시문의 범위는 지시문이 나타내는 파일로 제한됩니다.
 
 `using` 지시문이 나타날 수 있습니다.
- 모든 네임스페이스 또는 형식 정의 전에 소스 파일을 시작합니다.
- 모든 네임스페이스에 있지만 이 네임스페이스에 선언된 네임스페이스 또는 형식 앞에 있어야 합니다.

이렇게 하지 않으면 컴파일러 오류 [CS1529](../../misc/cs1529.md)가 생성됩니다.
  
 `using` 별칭 지시문을 만들면 네임스페이스 또는 형식에 대한 식별자를 더 쉽게 한정할 수 있습니다. 모든 `using` 지시문에서 앞에 오는 `using` 지시문에 관계없이 정규화된 네임스페이스 또는 형식을 사용해야 합니다. `using` 별칭은 `using` 지시문 선언에 사용할 수 없습니다. 예를 들어, 다음은 컴파일러 오류를 생성합니다.
 ```csharp
 using s = System.Text;
 using s.RegularExpressions; 
 ```
  
 `using` 지시문을 만들어서 네임스페이스를 지정할 필요 없이 네임스페이스에서 이 형식을 사용합니다. `using` 지시문은 지정한 네임스페이스에 중첩된 모든 네임스페이스에 대한 액세스 권한을 제공하지 않습니다.  
  
 네임스페이스는 두 가지 범주인 사용자 정의 및 시스템 정의로 구분됩니다. 사용자 정의 네임스페이스는 코드에서 정의된 네임스페이스입니다. 시스템 정의 네임스페이스 목록은 [.NET API 브라우저](https://docs.microsoft.com/dotnet/api/)를 참조하세요.  
  
 다른 어셈블리의 메서드를 참조하는 예제는 [명령줄을 사용하여 어셈블리 만들기 및 사용](../../programming-guide/concepts/assemblies-gac/how-to-create-and-use-assemblies-using-the-command-line.md)을 참조하세요.  
  
## <a name="example-1"></a>예제 1  
  
 다음 예제에서는 `using` 네임스페이스에 대한 별칭을 정의 및 사용하는 방법을 보여 줍니다.  
  
 [!code-csharp[csrefKeywordsNamespace#8](../../../csharp/language-reference/keywords/codesnippet/CSharp/using-directive_1.cs)]  
  
 using alias 지시문의 오른쪽에는 공개 제네릭 형식이 포함될 수 없습니다. 예를 들어 List\<T>에 대해서는 using 별칭을 만들 수 없지만 List\<int>에 대해서는 만들 수 있습니다.  
  
## <a name="example-2"></a>예제 2  
  
 다음 예제에서는 클래스에 대한 `using` 지시문 및 `using` 별칭을 정의하는 방법을 보여 줍니다.  
  
 [!code-csharp[csrefKeywordsNamespace#9](../../../csharp/language-reference/keywords/codesnippet/CSharp/using-directive_2.cs)]  
  
## <a name="c-language-specification"></a>C# 언어 사양  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>참고 항목

- [C# 참조](../../../csharp/language-reference/index.md)  
- [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)  
- [네임스페이스 사용](../../../csharp/programming-guide/namespaces/using-namespaces.md)  
- [C# 키워드](../../../csharp/language-reference/keywords/index.md)  
- [네임스페이스 키워드](../../../csharp/language-reference/keywords/namespace-keywords.md)  
- [네임스페이스](../../../csharp/programming-guide/namespaces/index.md)  
- [using 문](../../../csharp/language-reference/keywords/using-statement.md)
