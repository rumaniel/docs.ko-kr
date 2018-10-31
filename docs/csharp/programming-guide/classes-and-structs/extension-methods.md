---
title: 확장명 메서드(C# 프로그래밍 가이드)
ms.date: 07/20/2015
helpviewer_keywords:
- methods [C#], adding to existing types
- extension methods [C#]
- methods [C#], extension
ms.assetid: 175ce3ff-9bbf-4e64-8421-faeb81a0bb51
ms.openlocfilehash: 7ebd04665d91f599edcb4a5c07680216dfb8925a
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2018
ms.locfileid: "48840903"
---
# <a name="extension-methods-c-programming-guide"></a>확장명 메서드(C# 프로그래밍 가이드)
확장명 메서드를 사용하면 새 파생 형식을 만들거나 다시 컴파일하거나 원래 형식을 수정하지 않고도 기존 형식에 메서드를 "추가"할 수 있습니다. 확장 메서드는 특수한 종류의 정적 메서드이지만 확장 형식의 인스턴스 메서드인 것처럼 호출됩니다. C#, F# 및 Visual Basic에서 작성된 클라이언트 코드의 경우 확장명 메서드를 호출하는 것과 형식에 실제로 정의된 메서드를 호출하는 데는 명백한 차이가 없습니다.  
  
 가장 일반적인 확장명 메서드는 쿼리 기능을 기존 <xref:System.Collections.IEnumerable?displayProperty=nameWithType> 및 <xref:System.Collections.Generic.IEnumerable%601?displayProperty=nameWithType> 형식에 추가하는 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 표준 쿼리 연산자입니다. 표준 쿼리 연산자를 사용하려면 `using System.Linq` 지시문을 사용해서 먼저 범위를 지정합니다. 그러면 <xref:System.Collections.Generic.IEnumerable%601>을 구현하는 모든 형식에 <xref:System.Linq.Enumerable.GroupBy%2A>, <xref:System.Linq.Enumerable.OrderBy%2A>, <xref:System.Linq.Enumerable.Average%2A> 등의 인스턴스 메서드가 있는 것처럼 나타납니다. <xref:System.Collections.Generic.List%601> 또는 <xref:System.Array>와 같은 <xref:System.Collections.Generic.IEnumerable%601> 형식의 인스턴스 뒤에 "dot"를 입력하면 IntelliSense 문 완성에서 이러한 추가 메서드를 볼 수 있습니다.  
  
 다음 예제에서는 정수 배열에서 표준 쿼리 연산자 `OrderBy`를 호출하는 방법을 보여 줍니다. 괄호 안의 식은 람다 식입니다. 많은 표준 쿼리 연산자가 람다 식을 매개 변수로 사용하지만 확장명 메서드에 대한 요구 사항은 아닙니다. 자세한 내용은 [람다 식](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)을 참조하세요.  
  
 [!code-csharp[csProgGuideExtensionMethods#3](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/extension-methods_1.cs)]  
  
 확장명 메서드는 정적 메서드로 정의되지만 인스턴스 메서드 구문을 사용하여 호출됩니다. 확장 메서드의 첫 번째 매개 변수는 메서드가 작동하는 형식을 지정하며 매개 변수 앞에 [this](../../../csharp/language-reference/keywords/this.md) 한정자가 있습니다. 확장 메서드는 `using` 지시문을 사용하여 명시적으로 네임스페이스를 소스 코드로 가져오는 경우에만 범위에 있습니다.  
  
 다음 예제에서는 <xref:System.String?displayProperty=nameWithType> 클래스에 대해 정의된 확장 메서드를 보여 줍니다. 이 확장 메서드는 제네릭이 아닌 비중첩 정적 클래스 내부에서 정의됩니다.  
  
 [!code-csharp[csProgGuideExtensionMethods#4](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/extension-methods_2.cs)]  
  
 `WordCount` 지시문을 사용하여 `using` 확장 메서드를 범위로 가져올 수 있습니다.  
  
```csharp  
using ExtensionMethods;  
```  
  
 또한 다음 구문을 사용하여 응용 프로그램에서 확장 메서드를 호출할 수 있습니다.  
  
```csharp  
string s = "Hello Extension Methods";  
int i = s.WordCount();  
```  
  
 코드에서 인스턴스 메서드 구문을 사용하여 확장 메서드를 호출합니다. 그러나 컴파일러에서 생성된 IL(중간 언어)이 코드를 정적 메서드 호출로 변환합니다. 따라서 실제로 캡슐화의 원칙을 위반하지 않습니다. 사실상 확장명 메서드는 확장하는 형식의 private 변수에 액세스할 수 없습니다.  
  
 자세한 내용은 [방법: 사용자 지정 확장 메서드 구현 및 호출](../../../csharp/programming-guide/classes-and-structs/how-to-implement-and-call-a-custom-extension-method.md)을 참조하세요.  
  
 일반적으로 확장명 메서드를 직접 구현하는 것보다 호출하는 경우가 훨씬 많습니다. 확장 메서드는 인스턴스 메서드 구문을 사용하여 호출되므로 특별한 지식이 없어도 클라이언트 코드에서 확장 메서드를 사용할 수 있습니다. 특정 형식의 확장 메서드를 사용하려면 해당 메서드가 정의된 네임스페이스에 대해 `using` 지시문을 추가합니다. 예를 들어 표준 쿼리 연산자를 사용하려면 다음 `using` 지시문을 코드에 추가합니다.  
  
```csharp  
using System.Linq;  
```  
  
 System.Core.dll에 대한 참조를 추가해야 할 수도 있습니다. 이제 표준 쿼리 연산자가 대부분의 <xref:System.Collections.Generic.IEnumerable%601> 형식에 사용할 수 있는 추가 메서드로 IntelliSense에 표시됩니다.  
  
## <a name="binding-extension-methods-at-compile-time"></a>컴파일 타임에 확장 메서드 바인딩  
 확장 메서드를 사용하여 클래스 또는 인터페이스를 확장할 수 있지만 재정의할 수는 없습니다. 이름과 시그니처가 인터페이스 또는 클래스 메서드와 동일한 확장 메서드는 호출되지 않습니다. 컴파일 시간에 확장 메서드는 항상 형식 자체에서 정의된 인스턴스 메서드보다 우선 순위가 낮습니다. 즉, 형식에 `Process(int i)`라는 메서드가 있고 동일한 시그니처를 가진 확장 메서드가 있는 경우 컴파일러는 항상 인스턴스 메서드에 바인딩합니다. 컴파일러는 메서드 호출을 발견할 경우 먼저 형식의 인스턴스 메서드에서 일치 항목을 찾습니다. 일치 항목이 없으면 형식에 대해 정의된 확장 메서드를 검색하고 찾은 첫 번째 확장 메서드에 바인딩합니다. 다음 예제에서는 컴파일러가 바인딩할 확장명 메서드 또는 인스턴스 메서드를 확인하는 방법을 보여 줍니다.  
  
## <a name="example"></a>예  
 다음 예제에서는 C# 컴파일러가 메서드 호출을 형식의 인스턴스 메서드 또는 확장명 메서드에 바인딩할 것인지 결정할 때 따르는 규칙을 보여 줍니다. 정적 클래스 `Extensions`는 `IMyInterface`를 구현하는 모든 형식에 대해 정의된 확장 메서드를 포함합니다. `A`, `B` 및 `C` 클래스는 모두 인터페이스를 구현합니다.  
  
 `MethodB` 확장 메서드는 이름과 시그니처가 클래스에서 이미 구현된 메서드와 정확하게 일치하므로 호출되지 않습니다.  
  
 일치하는 시그니처를 가진 인스턴스 메서드를 찾을 수 없으면 컴파일러는 일치하는 확장명 메서드(있는 경우)에 바인딩합니다.  
  
 [!code-csharp[csProgGuideExtensionMethods#5](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/extension-methods_3.cs)]  
  
## <a name="general-guidelines"></a>일반 지침  
 일반적으로 반드시 필요한 경우에만 드물게 확장 메서드를 구현하는 것이 좋습니다. 가능하면 기존 형식을 확장해야 하는 클라이언트 코드는 기존 형식에서 파생된 새 형식을 만들어 이 작업을 수행해야 합니다. 자세한 내용은 [상속](../../../csharp/programming-guide/classes-and-structs/inheritance.md)을 참조하세요.  
  
 기존 메서드를 사용하여 소스 코드를 변경할 수 없는 형식을 확장하는 경우 형식의 구현이 변경되어 확장명 메서드가 손상될 수도 있습니다.  
  
 지정된 형식에 대해 확장 메서드를 구현하는 경우 다음 사항에 유의하세요.  
  
-   시그니처가 형식에 정의된 메서드와 동일한 확장 메서드는 호출되지 않습니다.  
  
-   확장 메서드는 네임스페이스 수준에서 범위로 가져옵니다. 예를 들어 `Extensions`라는 단일 네임스페이스에 확장 메서드를 포함하는 여러 개의 정적 클래스가 있는 경우 `using Extensions;` 지시문을 통해 모두 범위로 가져옵니다.  
  
 구현된 클래스 라이브러리의 경우 어셈블리의 버전 번호가 증가되는 것을 방지하기 위해 확장 메서드를 사용해서는 안 됩니다. 소스 코드를 소유하고 있는 라이브러리에 중요 기능을 추가하려는 경우 어셈블리 버전 관리를 위한 표준 .NET Framework 지침을 따라야 합니다. 자세한 내용은 [어셈블리 버전 관리](../../../../docs/framework/app-domains/assembly-versioning.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)  
- [병렬 프로그래밍 샘플(많은 예제 확장 메서드 포함)](https://code.msdn.microsoft.com/Samples-for-Parallel-b4b76364)  
- [람다 식](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)  
- [표준 쿼리 연산자 개요](../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)
- [인스턴스 매개 변수의 변환 규칙 및 그에 따른 영향](https://blogs.msdn.microsoft.com/sreekarc/2007/10/11/conversion-rules-for-instance-parameters-and-their-impact)  
- [언어 간 확장 메서드 상호 운용성](https://blogs.msdn.microsoft.com/sreekarc/2007/10/11/extension-methods-interoperability-between-languages)  
- [확장 메서드 및 대리자 변환](https://blogs.msdn.microsoft.com/sreekarc/2007/05/01/extension-methods-and-curried-delegates)  
- [확장 메서드 바인딩 및 오류 보고](https://blogs.msdn.microsoft.com/sreekarc/2007/04/26/extension-method-binding-and-error-reporting)
