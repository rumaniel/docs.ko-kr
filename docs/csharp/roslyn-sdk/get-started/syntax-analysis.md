---
title: 구문 분석 시작(Roslyn API)
description: 구문 트리를 트래버스하고, 탐색하고, 쿼리하는 방법을 소개합니다.
ms.date: 02/05/2018
ms.custom: mvc
ms.openlocfilehash: e377fe10e094e958627c3503fc39b7e2d02b3d7a
ms.sourcegitcommit: e614e0f3b031293e4107f37f752be43652f3f253
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/26/2018
ms.locfileid: "42931761"
---
# <a name="get-started-with-syntax-analysis"></a>구문 분석 시작

이 자습서에서는 **구문 API**를 탐색합니다. 구문 API는 C# 또는 Visual Basic 프로그램을 설명하는 데이터 구조에 대한 액세스를 제공합니다. 이러한 데이터 구조에는 모든 규모의 프로그램을 완벽하게 나타낼 수 있는 충분한 세부 정보가 있습니다. 이러한 구조는 컴파일하고 올바르게 실행하는 전체 프로그램을 설명할 수 있습니다. 또한 편집기에서 작성한 대로 불완전한 프로그램을 설명합니다.

다양한 식을 사용하도록 설정하려면 구문 API를 구성하는 데이터 구조 및 API는 복잡해질 수 밖에 없습니다. 일반적인 "Hello World" 프로그램에 있는 데이터 구조의 모양부터 시작하겠습니다.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

namespace HelloWorld
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}
```

이전 프로그램의 텍스트를 확인합니다. 친숙한 요소를 인식합니다. 전체 텍스트는 단일 원본 파일 또는 **컴파일 단위**를 나타냅니다. 해당 원본 파일의 처음 세 줄은 **using 지시문**입니다. 나머지 원본은 **네임스페이스 선언**에 포함됩니다. 네임스페이스 선언에는 자식 **클래스 선언**이 포함됩니다. 클래스 선언에는 하나의 **메서드 선언**이 포함됩니다.

구문 API는 컴파일 단위를 나타내는 루트를 사용하여 트리 구조를 만듭니다. 트리의 노드는 using 지시문, 네임스페이스 선언 및 프로그램의 다른 모든 요소를 나타냅니다. 트리 구조는 가장 낮은 수준인 문자열 "Hello World!"까지 계속되고 **인수**의 하위 항목인 **문자열 리터럴 토큰**입니다. 구문 API는 프로그램의 구조에 대한 액세스를 제공합니다. 특정 코드 사례에 대해 쿼리하고, 전체 트리를 통해 코드를 이해하고, 기존 트리를 수정하여 새 트리를 만들 수 있습니다.

간략한 설명을 통해 구문 API를 사용하여 액세스할 수 있는 정보의 종류에 대한 개요를 제공합니다. 구문 API는 C#에서 알아낸 친숙한 코드 구문을 설명하는 공식 API입니다. 줄 바꿈, 공백 및 들여쓰기를 비롯하여 코드의 형식을 지정하는 방법에 대한 정보가 포함된 완전한 기능입니다. 이 정보를 사용하여 코드를 작성한 대로 완벽하게 나타내고 휴먼 프로그래머 또는 컴파일러가 읽을 수 있습니다. 이 구조를 사용하면 의미 있는 수준에서 소스 코드와 상호 작용할 수 있습니다. 더 이상 텍스트 문자열이 아니지만 C# 프로그램의 구조를 나타내는 데이터입니다.

시작하려면 **.NET Compiler Platform SDK**를 설치해야 합니다.

[!INCLUDE[interactive-note](~/includes/roslyn-installation.md)]

## <a name="understanding-syntax-trees"></a>구문 트리 이해

C# 코드 구조의 분석에 구문 API를 사용합니다. **구문 API**는 구문 트리를 분석하고 생성하기 위한 파서, 구문 트리 및 유틸리티를 노출합니다. 그렇게 특정 구문 요소에 대한 코드를 검색하거나 프로그램에 대한 코드를 읽을 수 있습니다.

구문 트리는 C# 및 Visual Basic 프로그램을 이해하기 위해 C# 및 Visual Basic 컴파일러에서 사용하는 데이터 구조입니다. 구문 트리는 프로젝트가 빌드되거나 개발자가 F5 키를 누를 때 실행되는 동일한 파서에서 생성됩니다. 구문 트리는 언어를 완전히 제공합니다. 코드 파일의 모든 정보가 트리에 표시됩니다. 텍스트에 대한 구문 트리를 작성하면 구문 분석된 정확한 원본 텍스트를 재현합니다. 또한 구문 트리는 **변경할 수 없습니다**. 만들어진 구문 트리는 변경할 수 없습니다. 트리의 소비자는 잠금 또는 기타 동시성 조치 없이 여러 스레드에서 트리를 분석할 수 있으며 데이터가 바뀌지 않는다는 점을 인식합니다. API를 사용하여 기존 트리를 수정한 결과로 나타난 새 트리를 만들 수 있습니다.

구문 트리의 네 가지 기본 구성 요소는 다음과 같습니다.

* <xref:Microsoft.CodeAnalysis.SyntaxTree?displayProperty=nameWithType> 클래스는 전체 구문 분석 트리를 나타내는 인스턴스입니다. <xref:Microsoft.CodeAnalysis.SyntaxTree>은 언어별 파생물을 포함하는 추상 클래스입니다. <xref:Microsoft.CodeAnalysis.CSharp.CSharpSyntaxTree?displayProperty=nameWithType>(또는 <xref:Microsoft.CodeAnalysis.VisualBasic.VisualBasicSyntaxTree?displayProperty=nameWithType>) 클래스의 구문 분석 메서드를 사용하여 C# 또는 VB 텍스트를 구문 분석합니다.
* <xref:Microsoft.CodeAnalysis.SyntaxNode?displayProperty=nameWithType> 클래스는 선언, 명령문, 절 및 식과 같은 구문 구조를 나타내는 인스턴스입니다.
* <xref:Microsoft.CodeAnalysis.SyntaxToken?displayProperty=nameWithType> 구조는 개별 키워드, 식별자, 연산자 또는 문장 부호를 나타냅니다.
* 마지막으로 <xref:Microsoft.CodeAnalysis.SyntaxTrivia?displayProperty=nameWithType> 구조는 토큰 간의 공백, 전처리 지시문 및 주석 등의 구문상으로 중요하지 않은 정보를 나타냅니다.

퀴즈, 토큰 및 노드는 Visual Basic 또는 C# 코드의 일부에 있는 모든 항목을 완전치 나타내는 트리를 형성하기 위해 계층적으로 구성됩니다. **구문 시각화 도우미** 창을 사용하여 이 구조를 확인할 수 있습니다. Visual Studio에서 **보기** > **다른 창** > **구문 시각화 도우미**를 선택합니다. 예를 들어 **구문 시각화 도우미**를 사용하여 검사된 위의 C# 원본 파일은 다음 그림처럼 표시됩니다.

**SyntaxNode**: 파랑 | **SyntaxToken**: 초록색 | **SyntaxTrivia**: 빨강 ![C# 코드 파일](media/walkthrough-csharp-syntax-figure1.png)

이 트리 구조를 탐색하여 코드 파일에서 문, 식, 토큰 또는 공백을 찾을 수 있습니다.

구문 API를 사용하여 코드 파일에서 무언가 찾을 수 있지만 대부분의 시나리오에는 작은 코드 조각을 검사하거나 특정 문 또는 조각을 검색하는 작업이 포함됩니다. 이후의 두 가지 예제에서는 코드의 구조를 찾거나 단일 문을 검색하는 일반적인 사용법을 보여줍니다.

## <a name="traversing-trees"></a>트리 트래버스

두 가지 방법으로 구문 트리에서 노드를 검사할 수 있습니다. 트리를 트래버스하여 각 노드를 검사하거나 특정 요소 또는 노드에 대해 쿼리할 수 있습니다.

### <a name="manual-traversal"></a>수동 트래버스

[GitHub 리포지토리](https://github.com/dotnet/samples/tree/master/csharp/roslyn-sdk/SyntaxQuickStart)에서 이 샘플의 완성된 코드를 볼 수 있습니다.

> [!NOTE]
> 구문 트리 형식은 상속을 사용하여 프로그램의 여러 위치에서 유효한 다른 구문 요소를 설명합니다. 종종 이러한 API를 사용하면 속성이나 컬렉션 멤버를 파생된 특정 형식에 캐스팅하게 됩니다. 다음 예제에서 할당 및 캐스팅은 명시적으로 형식화된 변수를 사용하는 별도의 문입니다. API의 반환 형식 및 반환되는 개체의 런타임 형식을 확인하기 위해 코드를 읽을 수 있습니다. 이 연습에서는 암시적으로 형식화된 변수를 사용하고 API 이름을 사용하여 검사된 개체의 형식을 설명하는 것이 더 일반적입니다.

새 C# **독립 실행형 코드 분석 도구** 프로젝트를 만듭니다.

* Visual Studio에서 **파일** > **새로 만들기** > **프로젝트**를 선택하여 새 프로젝트 대화 상자를 표시합니다.
* **Visual C#** > **확장성** 아래에서 **독립 실행형 코드 분석 도구**를 선택합니다.
* 프로젝트 이름을 "**SyntaxTreeManualTraversal**"이라고 지정하고 확인을 클릭합니다.

앞에 표시된 기본 "Hello World!" 프로그램을 분석하려고 합니다.
Hello World 프로그램의 텍스트를 `Program` 클래스의 상수로 추가합니다.

[!code-csharp[Declare the program text](../../../../samples/csharp/roslyn-sdk/SyntaxQuickStart/HelloSyntaxTree/Program.cs#1 "Declare a constant string for the program text to analyze")]

다음으로 `programText` 상수에서 코드 텍스트의 **구문 트리**를 빌드하는 다음 코드를 추가합니다.  `Main` 메서드에 다음 줄을 추가합니다.

[!code-csharp[Create the tree](../../../../samples/csharp/roslyn-sdk/SyntaxQuickStart/HelloSyntaxTree/Program.cs#2 "Create the syntax tree")]

해당 두 줄은 트리를 만들고 해당 트리의 루트 노드를 검색합니다. 이제 트리에서 노드를 검사할 수 있습니다. 다음과 같은 줄을 `Main` 메서드에 추가하여 트리에서 루트 노드 속성 중 일부를 표시합니다.

[!code-csharp[Examine the root node](../../../../samples/csharp/roslyn-sdk/SyntaxQuickStart/HelloSyntaxTree/Program.cs#3 "Examine the root node")]

애플리케이션을 실행하여 코드가 이 트리에서 루트 노드에 대해 검색한 내용을 확인합니다.

일반적으로 코드에 대해 자세히 알아보려면 트리를 탐색합니다. 이 예제에서는 API를 탐색하기 위해 알아야 하는 코드를 분석합니다. 다음 코드를 추가하여 `root` 노드의 첫 번째 멤버를 검사합니다.

[!code-csharp[Find the first member](../../../../samples/csharp/roslyn-sdk/SyntaxQuickStart/HelloSyntaxTree/Program.cs#4 "Find the first member")]

해당 멤버는 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.NamespaceDeclarationSyntax?displayProperty=nameWithType>입니다. `namespace HelloWorld` 선언 범위에 있는 모든 항목을 나타냅니다. 다음 코드를 추가하여 노드가 `HelloWorld` 네임스페이스 내에서 선언된 내용을 검사합니다.

[!code-csharp[Find the class declaration](../../../../samples/csharp/roslyn-sdk/SyntaxQuickStart/HelloSyntaxTree/Program.cs#5 "Find the class declaration")]

배운 내용을 확인하기 위해 프로그램을 실행합니다.

이제 선언이 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.ClassDeclarationSyntax?displayProperty=nameWithType>임을 알았으므로 해당 형식의 새로운 변수를 선언하여 클래스 선언을 검사합니다. 이 클래스에는 `Main` 메서드라는 하나의 멤버만이 포함됩니다. 다음 코드를 추가하여 `Main` 메서드를 찾고 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.MethodDeclarationSyntax?displayProperty=nameWithType>로 캐스팅합니다.

[!code-csharp[Find the main declaration](../../../../samples/csharp/roslyn-sdk/SyntaxQuickStart/HelloSyntaxTree/Program.cs#6 "Find the main declaration")]

메서드 선언 노드에는 메서드에 대한 모든 구문 정보가 포함됩니다. `Main` 메서드의 반환 형식, 인수의 수와 형식 및 메서드의 본문 텍스트를 표시하겠습니다. 다음 코드를 추가합니다.

[!code-csharp[Examine the syntax of the main method](../../../../samples/csharp/roslyn-sdk/SyntaxQuickStart/HelloSyntaxTree/Program.cs#7 "Display information about the main method")]

프로그램을 실행하여 이 프로그램에 대해 알게 된 모든 정보를 확인합니다.

```text
The tree is a CompilationUnit node.
The tree has 1 elements in it.
The tree has 4 using statements. They are:
        System
        System.Collections
        System.Linq
        System.Text
The first member is a NamespaceDeclaration.
There are 1 members declared in this namespace.
The first member is a ClassDeclaration.
There are 1 members declared in the Program class.
The first member is a MethodDeclaration.
The return type of the Main method is void.
The method has 1 parameters.
The type of the args parameter is string[].
The body text of the Main method follows:
        {
            Console.WriteLine("Hello, World!");
        }
```

### <a name="query-methods"></a>쿼리 메서드

트리를 트래버스하는 것 외에도 <xref:Microsoft.CodeAnalysis.SyntaxNode?displayProperty=nameWithType>에 정의된 쿼리 메서드를 사용하여 구문 트리를 탐색할 수 있습니다. 이러한 메서드는 XPath에 익숙한 사용자라면 누구나 즉시 익숙해질 것입니다. LINQ에서 이러한 메서드를 사용하여 트리에서 신속히 작업할 수 있습니다. <xref:Microsoft.CodeAnalysis.SyntaxNode>에는 <xref:Microsoft.CodeAnalysis.SyntaxNode.DescendantNodes%2A>, <xref:Microsoft.CodeAnalysis.SyntaxNode.AncestorsAndSelf%2A> 및 <xref:Microsoft.CodeAnalysis.SyntaxNode.ChildNodes%2A> 등의 쿼리 메서드가 있습니다.

이러한 쿼리 메서드를 사용하여 트리를 탐색하는 대신 `Main` 메서드에 대한 인수를 찾을 수 있습니다. `Main` 메서드의 맨 아래에 다음 코드를 추가합니다.

[!code-csharp[Query the tree for the arguments to Main](../../../../samples/csharp/roslyn-sdk/SyntaxQuickStart/HelloSyntaxTree/Program.cs#8 "Query the tree for the arguments to Main")]

첫 번째 문은 LINQ 식 및 <xref:Microsoft.CodeAnalysis.SyntaxNode.DescendantNodes%2A> 메서드를 사용하여 앞의 예제와 동일한 매개 변수를 찾습니다.

프로그램을 실행하고, LINQ 식이 트리를 수동으로 탐색할 때와 동일한 매개 변수를 찾았는지 확인할 수 있습니다.

이 샘플에서는 `WriteLine` 문을 사용하여 트래버스한 대로 구문 트리에 대한 정보를 표시합니다. 디버거에서 완성된 프로그램을 실행하여 자세히 알아볼 수 있습니다. Hello World 프로그램에서 만든 구문 트리의 일부인 속성 및 메서드를 자세히 검사할 수 있습니다.

## <a name="syntax-walkers"></a>구문 워커

구문 트리에서 특정 종류의 모든 노드를 찾을 수도 있습니다(예: 파일의 모든 속성 선언). <xref:Microsoft.CodeAnalysis.CSharp.CSharpSyntaxWalker?displayProperty=nameWithType> 클래스를 확장하고 <xref:Microsoft.CodeAnalysis.CSharp.CSharpSyntaxVisitor.VisitPropertyDeclaration(Microsoft.CodeAnalysis.CSharp.Syntax.PropertyDeclarationSyntax)> 메서드를 재정의하여 해당 구조를 미리 알지 못해도 구문 트리에서 모든 속성 선언을 처리할 수 있습니다. <xref:Microsoft.CodeAnalysis.CSharp.CSharpSyntaxWalker>는 노드와 해당 자식 항목을 재귀적으로 방문하는 특정 종류의 <xref:Microsoft.CodeAnalysis.CSharp.CSharpSyntaxVisitor>입니다.

이 예제에서는 구문 트리를 검사하는 <xref:Microsoft.CodeAnalysis.CSharp.CSharpSyntaxWalker>를 구현합니다. `System` 네임스페이스를 가져오지 않는 `using` 지시문을 찾아 수집합니다.

새 C# **독립 실행형 코드 분석 도구** 프로젝트를 만들고 이름을 "**SyntaxWalker**"로 지정합니다.

[GitHub 리포지토리](https://github.com/dotnet/samples/tree/master/csharp/roslyn-sdk/SyntaxQuickStart)에서 이 샘플의 완성된 코드를 볼 수 있습니다. GitHub의 샘플에는 이 자습서에 설명된 모든 프로젝트가 포함됩니다.

앞의 예제와 같이 분석하려는 프로그램의 텍스트를 포함하도록 문자열 상수를 정의할 수 있습니다.

[!code-csharp[Define the code text to analyzer](../../../../samples/csharp/roslyn-sdk/SyntaxQuickStart/SyntaxWalker/Program.cs#1 "Define the program text to analyze")]

이 원본 텍스트에는 파일 수준, 최상위 네임스페이스 및 두 개의 중첩된 네임스페이스와 같은 네 가지 위치에 분산된 `using` 지시문이 포함됩니다. 이 예제에서는 코드를 쿼리하는 <xref:Microsoft.CodeAnalysis.CSharp.CSharpSyntaxWalker> 클래스를 사용하는 핵심 시나리오를 강조 표시합니다. using 선언을 찾기 위해 루트 구문 트리에서 모든 노드를 방문하기는 번거롭습니다. 대신, 파생된 클래스를 만들고 트리의 현재 노드가 using 지시문인 경우에만 호출되는 메서드를 재정의합니다. 방문자는 다른 노드 형식에서 작업을 수행하지 않습니다. 이 단일 메서드는 각 `using` 문을 검사하고 `System` 네임스페이스에 위치하지 않는 네임스페이스의 컬렉션을 빌드합니다. 모든 `using` 문이 아닌 `using` 문을 검사하는 <xref:Microsoft.CodeAnalysis.CSharp.CSharpSyntaxWalker>를 빌드합니다.

이제 프로그램 텍스트를 정의했으므로 `SyntaxTree`를 만들고 해당 트리의 루트를 가져와야 합니다.

[!code-csharp[Create the Syntax tree and access the root](../../../../samples/csharp/roslyn-sdk/SyntaxQuickStart/SyntaxWalker/Program.cs#2 "Create the Syntax tree and access the root node.")]

다음으로 새 클래스를 만듭니다. Visual Studio에서 **프로젝트** > **새 항목 추가**를 선택합니다. **새 항목 추가** 대화 상자에서 파일 이름으로 *UsingCollector.cs*를 입력합니다.

`UsingCollector` 클래스에서 `using` 방문자 기능을 구현합니다. <xref:Microsoft.CodeAnalysis.CSharp.CSharpSyntaxWalker>에서 파생된 `UsingCollector` 클래스를 만들기 시작합니다.

[!code-csharp[Declare the base class for the using collector](../../../../samples/csharp/roslyn-sdk/SyntaxQuickStart/SyntaxWalker/UsingCollector.cs#3 "Declare the base class for the UsingCollector")]

수집 중인 네임스페이스 노드를 포함하는 스토리지가 있어야 합니다.  `UsingCollector` 클래스에서 공용 읽기 전용 속성을 선언합니다. 이 변수를 사용하여 찾은 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.UsingDirectiveSyntax> 노드를 저장합니다.

[!code-csharp[Declare storage for the using syntax nodes](../../../../samples/csharp/roslyn-sdk/SyntaxQuickStart/SyntaxWalker/UsingCollector.cs#4 "Declare storage for the using syntax nodes")]

<xref:Microsoft.CodeAnalysis.CSharp.CSharpSyntaxWalker> 기본 클래스는 구문 트리에서 각 노드를 방문하는 논리를 구현합니다. 파생된 클래스는 관심이 있는 특정 노드에 호출되는 메서드를 재정의합니다. 이 경우에 `using` 지시문을 사용합니다. 즉, <xref:Microsoft.CodeAnalysis.CSharp.CSharpSyntaxVisitor.VisitUsingDirective(Microsoft.CodeAnalysis.CSharp.Syntax.UsingDirectiveSyntax)> 메서드를 재정의해야 합니다. 이 메서드에 대한 인수는 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.UsingDirectiveSyntax?displayProperty=nameWithType> 개체입니다. 방문자를 사용하는 중요한 장점은 특정 노드 형식에 캐스팅된 인수를 사용하여 재정의된 메서드를 호출한다는 것입니다. <xref:Microsoft.CodeAnalysis.CSharp.Syntax.UsingDirectiveSyntax?displayProperty=nameWithType> 클래스에는 가져온 네임스페이스의 이름을 저장하는 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.UsingDirectiveSyntax.Name> 속성이 있습니다. <xref:Microsoft.CodeAnalysis.CSharp.Syntax.NameSyntax?displayProperty=nameWithType>입니다. <xref:Microsoft.CodeAnalysis.CSharp.CSharpSyntaxVisitor.VisitUsingDirective(Microsoft.CodeAnalysis.CSharp.Syntax.UsingDirectiveSyntax)> 재정의에서 다음 코드를 추가합니다.

[!code-csharp[Examine using nodes for the System namespace](../../../../samples/csharp/roslyn-sdk/SyntaxQuickStart/SyntaxWalker/UsingCollector.cs#5 "Examine all using nodes for the System namespace.")]

이전 예제에서 다양한 `WriteLine` 문을 추가하여 이 메서드를 이해할 수 있었습니다. 호출할 시기 및 이 때 전달된 인수를 확인할 수 있습니다.

마지막으로 `UsingCollector`를 만들고 루트 노드를 방문하게 만드는 두 개의 코드 줄을 추가해야 합니다. 그러면 모든 `using` 문을 수집합니다. 그런 다음, `foreach` 루프를 추가하여 수집기에서 찾은 `using` 문을 모두 표시합니다.

[!code-csharp[Create the UsingCollector and visit the root node.](../../../../samples/csharp/roslyn-sdk/SyntaxQuickStart/SyntaxWalker/Program.cs#6 "Create the UsingCollector and visit the root node.")]

프로그램을 컴파일하고 실행합니다. 다음과 같은 내용이 출력됩니다.

```console
        VisitUsingDirective called with System.
        VisitUsingDirective called with System.Collections.Generic.
        VisitUsingDirective called with System.Linq.
        VisitUsingDirective called with System.Text.
        VisitUsingDirective called with Microsoft.CodeAnalysis.
                Success. Adding Microsoft.CodeAnalysis.
        VisitUsingDirective called with Microsoft.CodeAnalysis.CSharp.
                Success. Adding Microsoft.CodeAnalysis.CSharp.
        VisitUsingDirective called with Microsoft.
                Success. Adding Microsoft.
        VisitUsingDirective called with System.ComponentModel.
        VisitUsingDirective called with Microsoft.Win32.
                Success. Adding Microsoft.Win32.
        VisitUsingDirective called with System.Runtime.InteropServices.
        VisitUsingDirective called with System.CodeDom.
        VisitUsingDirective called with Microsoft.CSharp.
                Success. Adding Microsoft.CSharp.
Microsoft.CodeAnalysis
Microsoft.CodeAnalysis.CSharp
Microsoft
Microsoft.Win32
Microsoft.CSharp
Press any key to continue . . .
```

지금까지 **구문 API**를 사용하여 C# 소스 코드에서 특정 종류의 C# 문 및 선언을 찾았습니다.
