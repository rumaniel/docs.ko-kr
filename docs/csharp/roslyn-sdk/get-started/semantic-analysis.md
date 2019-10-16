---
title: 의미 체계 분석 시작
description: 이 자습서는 .NET Compiler SDK를 사용하여 의미 체계 분석으로 작업하는 방법의 개요를 제공합니다.
ms.date: 02/06/2018
ms.custom: mvc
ms.openlocfilehash: 80a814054ab95a5b6585289e8580a725b18ca44e
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252939"
---
# <a name="get-started-with-semantic-analysis"></a>의미 체계 분석 시작

이 자습서는 사용자가 구문 API에 익숙하다고 가정합니다. [구문 분석 작업 시작](syntax-analysis.md) 아티클에서는 소개를 충분히 설명합니다.

이 자습서에서는 **기호** 및 **바인딩 API**를 탐색합니다. 이러한 API는 프로그램의 _의미 체계_에 대한 정보를 제공합니다. 이를 통해 프로그램에서 기호를 나타내는 형식에 대해 질문하고 대답할 수 있습니다.

**.NET Compiler Platform SDK**를 설치해야 합니다.

[!INCLUDE[interactive-note](~/includes/roslyn-installation.md)]

## <a name="understanding-compilations-and-symbols"></a>컴파일 및 기호 이해

.NET Compiler SDK에서 작업하게 되면 구문 API와 의미 체계 API 간의 차이점을 이해할 수 있게 됩니다. **구문 API**를 사용하면 프로그램의 _구조_를 볼 수 있습니다. 그러나 프로그램의 의미 체계 또는 _의미_에 대해 더 다양한 정보가 필요할 수 있습니다. 느슨한 코드 파일 또는 VB 또는 C#의 코드 조각은 격리에서 구문을 분석할 수 있습니다. "이 변수의 형식이란?"과 같은 질문은 의미가 없습니다. 형식 이름의 의미는 어셈블리 참조, 네임스페이스 가져오기 또는 기타 코드 파일에 종속될 수 있습니다. **의미 체계 API**, 특히 <xref:Microsoft.CodeAnalysis.Compilation?displayProperty=nameWithType> 클래스를 사용하여 해당 질문에 대답합니다.

<xref:Microsoft.CodeAnalysis.Compilation>의 인스턴스는 컴파일러에서 보는 단일 프로젝트와 유사하고, Visual Basic 또는 C# 프로그램을 컴파일하는 데 필요한 모든 항목을 나타냅니다. **컴파일**에는 컴파일할 원본 파일, 어셈블리 참조 및 컴파일러 옵션의 집합이 포함됩니다. 이 컨텍스트에서 다른 모든 정보를 사용하여 코드의 의미에 대해 추정할 수 있습니다. <xref:Microsoft.CodeAnalysis.Compilation>을 사용하면 이름 및 다른 식이 참조하는 형식, 네임스페이스, 멤버 및 변수 등의 엔터티인 **기호**를 찾을 수 있습니다. **기호**를 사용하여 이름 및 식을 연결하는 프로세스를 **바인딩**이라고 합니다.

<xref:Microsoft.CodeAnalysis.SyntaxTree?displayProperty=nameWithType>과 마찬가지로 <xref:Microsoft.CodeAnalysis.Compilation>은 언어별 파생물을 포함하는 추상 클래스입니다. 컴파일의 인스턴스를 만들 때 <xref:Microsoft.CodeAnalysis.CSharp.CSharpCompilation?displayProperty=nameWithType>(또는 <xref:Microsoft.CodeAnalysis.VisualBasic.VisualBasicCompilation?displayProperty=nameWithType>) 클래스에서 팩터리 메서드를 호출해야 합니다.

## <a name="querying-symbols"></a>기호 쿼리

이 자습서에서는 "Hello World" 프로그램을 다시 확인합니다. 이번에는 프로그램의 기호를 쿼리하여 해당 기호가 나타내는 형식을 이해합니다. 네임스페이스의 형식에 대해 쿼리하고 형식에 사용할 수 있는 메서드를 찾는 방법을 알아봅니다.

[GitHub 리포지토리](https://github.com/dotnet/samples/tree/master/csharp/roslyn-sdk/SemanticQuickStart)에서 이 샘플의 완성된 코드를 볼 수 있습니다.

> [!NOTE]
> 구문 트리 형식은 상속을 사용하여 프로그램의 여러 위치에서 유효한 다른 구문 요소를 설명합니다. 종종 이러한 API를 사용하면 속성이나 컬렉션 멤버를 파생된 특정 형식에 캐스팅하게 됩니다. 다음 예제에서 할당 및 캐스팅은 명시적으로 형식화된 변수를 사용하는 별도의 문입니다. API의 반환 형식 및 반환되는 개체의 런타임 형식을 확인하기 위해 코드를 읽을 수 있습니다. 이 연습에서는 암시적으로 형식화된 변수를 사용하고 API 이름을 사용하여 검사된 개체의 형식을 설명하는 것이 더 일반적입니다.

새 C# **독립 실행형 코드 분석 도구** 프로젝트를 만듭니다.

* Visual Studio에서 **파일** > **새로 만들기** > **프로젝트**를 선택하여 새 프로젝트 대화 상자를 표시합니다.
* **Visual C#**  > **확장성** 아래에서 **독립 실행형 코드 분석 도구**를 선택합니다.
* 프로젝트 이름을 "**SemanticQuickStart**"로 지정하고 확인을 클릭합니다.

앞에 표시된 기본 "Hello World!" 프로그램을 분석하려고 합니다.
Hello World 프로그램의 텍스트를 `Program` 클래스의 상수로 추가합니다.

[!code-csharp[Declare the program test](../../../../samples/csharp/roslyn-sdk/SemanticQuickStart/Program.cs#1 "Declare a constant string for the program text to analyze")]

다음으로 `programText` 상수에서 코드 텍스트의 구문 트리를 빌드하는 다음 코드를 추가합니다.  `Main` 메서드에 다음 줄을 추가합니다.

[!code-csharp[Create the tree](../../../../samples/csharp/roslyn-sdk/SemanticQuickStart/Program.cs#2 "Create the syntax tree")]

다음으로 이미 만든 트리에서 <xref:Microsoft.CodeAnalysis.CSharp.CSharpCompilation>을 빌드합니다. "Hello World" 샘플은 <xref:System.String> 및 <xref:System.Console> 형식으로 사용합니다. 컴파일에서 두 가지 해당 형식을 선언하는 어셈블리를 참조해야 합니다. 다음 줄을 `Main` 메서드에 추가하여 적절한 어셈블리에 대한 참조를 비롯한 구문 트리의 컴파일을 만듭니다.

[!code-csharp[Create the compilation](../../../../samples/csharp/roslyn-sdk/SemanticQuickStart/Program.cs#3 "Create the compilation for the semantic model")]

<xref:Microsoft.CodeAnalysis.CSharp.CSharpCompilation.AddReferences%2A?displayProperty=nameWithType> 메서드는 컴파일에 참조를 추가합니다. <xref:Microsoft.CodeAnalysis.MetadataReference.CreateFromFile%2A?displayProperty=nameWithType> 메서드는 어셈블리를 참조로 로드합니다.

## <a name="querying-the-semantic-model"></a>의미 체계 모델 쿼리

<xref:Microsoft.CodeAnalysis.Compilation>이 있다면 <xref:Microsoft.CodeAnalysis.SemanticModel>에 대해 해당 <xref:Microsoft.CodeAnalysis.Compilation>에 포함된 <xref:Microsoft.CodeAnalysis.SyntaxTree>를 요청할 수 있습니다. 일반적으로 모든 정보의 원본을 IntelliSense에서 가져오는 경우 의미 체계 모델을 고려할 수 있습니다. <xref:Microsoft.CodeAnalysis.SemanticModel>은 "이 위치에서 범위에 있는 이름은 무엇입니까?", "이 메서드에서 어떤 멤버에 액세스할 수 있습니까?", "이 텍스트의 블록에서 사용되는 변수는 무엇입니까?" 및 "이 이름/식은 무엇을 참조합니까?"와 같은 질문에 대답할 수 있습니다. 의미 체계 모델을 만드는 이 문을 추가합니다.

[!code-csharp[Create the semantic model](../../../../samples/csharp/roslyn-sdk/SemanticQuickStart/Program.cs#4 "Create the semantic model")]

## <a name="binding-a-name"></a>이름 바인딩

<xref:Microsoft.CodeAnalysis.Compilation>은 <xref:Microsoft.CodeAnalysis.SyntaxTree>에서 <xref:Microsoft.CodeAnalysis.SemanticModel>을 만듭니다. 모델을 만든 후에 쿼리하여 첫 번째 `using` 지시문을 찾고 `System` 네임스페이스에 대한 기호 정보를 검색할 수 있습니다. `Main` 메서드에 두 줄을 추가하여 의미 체계 모델을 만들고 첫 번째 using 문에 대한 기호를 검색합니다.

[!code-csharp[Find the namespace symbol for the first using](../../../../samples/csharp/roslyn-sdk/SemanticQuickStart/Program.cs#5 "Find the namespace symbol for the first using")]

위의 코드는 첫 번째 `using` 지시문의 이름을 바인딩하여 `System` 네임스페이스에서 <xref:Microsoft.CodeAnalysis.SymbolInfo?displayProperty=nameWithType>을 검색하는 방법을 보여 줍니다. 또한 위의 코드에서는 **구문 모델**을 사용하여 코드의 구조를 찾는 것을 설명합니다. **의미 체계 모델**을 사용하여 해당 의미를 이해합니다. **구문 모델**은 using 문에서 `System` 문자열을 찾습니다. **의미 체계 모델**에는 `System` 네임스페이스에서 정의된 형식에 대한 모든 정보가 있습니다.

<xref:Microsoft.CodeAnalysis.SymbolInfo> 개체에서 <xref:Microsoft.CodeAnalysis.SymbolInfo.Symbol?displayProperty=nameWithType> 속성을 사용하여 <xref:Microsoft.CodeAnalysis.ISymbol?displayProperty=nameWithType>를 가져올 수 있습니다. 이 속성은 이 식에서 참조하는 기호를 반환합니다. 아무것도 참조하지 않은 식(예: 숫자 리터럴)의 경우 이 속성은 `null`입니다. <xref:Microsoft.CodeAnalysis.SymbolInfo.Symbol?displayProperty=nameWithType>이 null이 아니면 <xref:Microsoft.CodeAnalysis.ISymbol.Kind?displayProperty=nameWithType>은 기호의 형식을 나타냅니다. 다음 예제에서 <xref:Microsoft.CodeAnalysis.ISymbol.Kind?displayProperty=nameWithType> 속성은 <xref:Microsoft.CodeAnalysis.SymbolKind.Namespace?displayProperty=nameWithType>입니다. `Main` 메서드에 다음 코드를 추가합니다. `System` 네임스페이스에 대한 기호를 검색한 다음, `System` 네임스페이스에 선언된 모든 자식 네임스페이스를 표시합니다.

[!code-csharp[Display all the child namespaces](../../../../samples/csharp/roslyn-sdk/SemanticQuickStart/Program.cs#6 "Display all the child namespaces from this compilation")]

프로그램을 실행하고 다음과 같은 출력이 표시됩니다.

```output
System.Collections
System.Configuration
System.Deployment
System.Diagnostics
System.Globalization
System.IO
System.Numerics
System.Reflection
System.Resources
System.Runtime
System.Security
System.StubHelpers
System.Text
System.Threading
Press any key to continue . . .
```

> [!NOTE]
> 출력에는 `System` 네임스페이스의 자식 네임스페이스인 모든 네임스페이스가 포함되지 않습니다. 이 컴파일에서 나타나는 모든 네임스페이스가 표시됩니다. 여기서는 `System.String`이 선언하는 어셈블리만을 참조합니다. 다른 어셈블리에 선언된 모든 네임스페이스가 이 컴파일에 알려지지 않았습니다.

### <a name="binding-an-expression"></a>식 바인딩

위의 코드에서는 이름에 바인딩하여 기호를 찾는 방법을 보여줍니다. 바인딩될 수 있는 C# 프로그램에 이름이 아닌 다른 식이 있습니다. 이 기능을 보여주기 위해 간단한 문자열 리터럴에 대한 바인딩에 액세스하겠습니다.

"Hello World" 프로그램에는 콘솔에 표시된 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.LiteralExpressionSyntax?displayProperty=nameWithType>, "Hello, World!" 문자열이 있습니다.

프로그램에 단일 리터럴 문자열을 배치하여 "Hello, World!" 문자열을 찾습니다. 그런 다음, 구문 노드를 찾으면 의미 체계 모델에서 노드의 형식 정보를 가져옵니다. `Main` 메서드에 다음 코드를 추가합니다.

[!code-csharp[Find the namespace symbol for the only using](../../../../samples/csharp/roslyn-sdk/SemanticQuickStart/Program.cs#7 "Find the namespace symbol for the only using")]

<xref:Microsoft.CodeAnalysis.TypeInfo?displayProperty=nameWithType> 구조체에는 리터럴 형식에 대한 의미 체계 정보에 액세스할 수 있는 <xref:Microsoft.CodeAnalysis.TypeInfo.Type?displayProperty=nameWithType> 속성이 포함됩니다. 이 예제에서는 `string` 형식입니다. 이 속성을 지역 변수에 할당하는 선언을 추가합니다.

[!code-csharp[Find the semantic information about the string type](../../../../samples/csharp/roslyn-sdk/SemanticQuickStart/Program.cs#8 "Use the string literal to access the semantic information in the string type.")]

이 자습서를 완료하려면 `string`을 반환하는 `string` 형식에 선언된 모든 공용 메서드의 시퀀스를 생성하는 LINQ 쿼리를 빌드하겠습니다. 이 쿼리가 복잡해집니다. 따라서 한 줄씩 빌드한 다음, 단일 쿼리로 다시 생성합니다. 이 쿼리의 원본은 `string` 형식에 선언된 모든 멤버의 시퀀스입니다.

[!code-csharp[Access the sequence of members on the string type](../../../../samples/csharp/roslyn-sdk/SemanticQuickStart/Program.cs#9 "Access the sequence of members on the string type.")]

해당 소스 시퀀스에는 속성 및 필드를 비롯한 모든 멤버가 포함됩니다. 따라서 <xref:Microsoft.CodeAnalysis.IMethodSymbol?displayProperty=nameWithType> 개체인 요소를 찾기 위해 <xref:System.Collections.Immutable.ImmutableArray%601.OfType%2A?displayProperty=nameWithType> 메서드를 사용하여 필터링합니다.

[!code-csharp[Filter the sequence to only methods](../../../../samples/csharp/roslyn-sdk/SemanticQuickStart/Program.cs#10 "Find the subset of the collection that is the methods.")]

다음으로 공용이며 `string`을 반환하는 해당 메서드만을 반환하는 다른 필터를 추가합니다.

[!code-csharp[Filter on return type and accessibility](../../../../samples/csharp/roslyn-sdk/SemanticQuickStart/Program.cs#11 "Find only the public methods that return a string.")]

이름 속성만을 선택하고, 오버로드를 제거하여 고유 이름만을 선택합니다.

[!code-csharp[find the distinct names.](../../../../samples/csharp/roslyn-sdk/SemanticQuickStart/Program.cs#12 "Use the string literal to access the semantic information in the string type.")]

LINQ 쿼리 구문을 사용하여 전체 쿼리를 빌드한 다음, 콘솔에서 모든 메서드 이름을 표시할 수 있습니다.

[!code-csharp[build and display the results of this query.](../../../../samples/csharp/roslyn-sdk/SemanticQuickStart/Program.cs#13 "Build and display the results of the query.")]

프로그램을 빌드하고 실행합니다. 다음과 같은 내용이 출력됩니다.

```output
Join
Substring
Trim
TrimStart
TrimEnd
Normalize
PadLeft
PadRight
ToLower
ToLowerInvariant
ToUpper
ToUpperInvariant
ToString
Insert
Replace
Remove
Format
Copy
Concat
Intern
IsInterned
Press any key to continue . . .
```

이 프로그램의 일부인 기호에 대한 정보를 찾고 표시하기 위해 의미 체계 API를 사용했습니다.
