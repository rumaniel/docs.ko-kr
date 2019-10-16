---
title: 구문 변환 시작(Roslyn API)
description: 구문 트리를 트래버스하고, 탐색하고, 쿼리하는 방법을 소개합니다.
ms.date: 06/01/2018
ms.custom: mvc
ms.openlocfilehash: bbd56f445a9f06b530a7d094b06f60e6123788da
ms.sourcegitcommit: a970268118ea61ce14207e0916e17243546a491f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/21/2019
ms.locfileid: "67306924"
---
# <a name="get-started-with-syntax-transformation"></a>구문 변환 시작

이 자습서는 [구문 분석 시작](syntax-analysis.md) 및 [의미 체계 분석 시작](semantic-analysis.md) 빠른 시작에서 살펴본 개념과 기술을 기반으로 구성됩니다. 아직 완료하지 않은 경우 이 자습서를 시작하기 전에 해당 빠른 시작을 완료해야 합니다.

이 빠른 시작에서는 구문 트리를 만들고 변환하는 기술을 살펴봅니다. 이전 빠른 시작에서 알아본 기술을 함께 사용하여 첫 번째 명령줄 리팩터링을 만듭니다.

[!INCLUDE[interactive-note](~/includes/roslyn-installation.md)]

## <a name="immutability-and-the-net-compiler-platform"></a>불변성 및 .NET 컴파일러 플랫폼

**불변성**은 .NET 컴파일러 플랫폼의 기본 원리입니다. 변경 불가능한 데이터 구조는 생성된 후 변경할 수 없습니다. 변경 불가능한 데이터 구조는 여러 소비자가 동시에 안전하게 공유하고 분석할 수 있습니다. 한 소비자가 예기치 않은 방식으로 다른 소비자에게 영향을 줄 위험이 없습니다. 분석기에는 잠금이나 기타 동시성 측정값이 필요하지 않습니다. 이 규칙은 구문 트리, 컴파일, 기호, 의미 체계 모델 및 사용자에게 나타나는 모든 기타 데이터 구조에 적용됩니다. 기존 구조를 수정하는 대신 API는 지정된 차이점을 기반으로 새 개체를 만듭니다. 이 개념을 구문 트리에 적용하여 변환을 통해 새 트리를 만듭니다.

## <a name="create-and-transform-trees"></a>트리 만들기 및 변환

구문 변환에 대해 두 가지 전략 중 하나를 선택합니다. **팩터리 메서드**는 대체할 특정 노드를 검색하거나 새 코드를 삽입할 특정 위치를 검색할 때 가장 유용합니다. **재작성기**는 대체할 코드 패턴을 전체 프로젝트에서 검색하려는 경우 가장 적합합니다.

### <a name="create-nodes-with-factory-methods"></a>팩터리 메서드를 사용하여 노드 만들기

첫 번째 구문 변환은 팩터리 메서드를 보여 줍니다. `using System.Collections;` 문을 `using System.Collections.Generic;` 문으로 바꾸려고 합니다. 이 예제는 <xref:Microsoft.CodeAnalysis.CSharp.SyntaxFactory?displayProperty=nameWithType> 팩터리 메서드를 사용하여 <xref:Microsoft.CodeAnalysis.CSharp.CSharpSyntaxNode?displayProperty=nameWithType> 개체를 만드는 방법을 보여 줍니다. 각 종류의 **노드**, **토큰** 또는 **기타 정보**에 대해 해당 형식의 인스턴스를 만드는 팩터리 메서드가 있습니다. 노드를 상향식 계층 구조로 작성하여 구문 트리를 만듭니다. 그런 다음, 기존 노드를 직접 만든 새 트리로 바꿔서 기존 프로그램을 변환합니다.

Visual Studio를 시작하고 새 C# **독립 실행형 코드 분석 도구** 프로젝트를 만듭니다. Visual Studio에서 **파일** > **새로 만들기** > **프로젝트**를 선택하여 새 프로젝트 대화 상자를 표시합니다. **Visual C#**  > **확장성** 아래에서 **독립 실행형 코드 분석 도구**를 선택합니다. 이 빠른 시작에는 두 개의 예제 프로젝트가 있으므로 솔루션 이름을 **SyntaxTransformationQuickStart**로 지정하고 프로젝트 이름을 **ConstructionCS**로 지정합니다. **확인**을 클릭합니다.

이 프로젝트는 <xref:Microsoft.CodeAnalysis.CSharp.SyntaxFactory?displayProperty=nameWithType> 클래스 메서드를 사용하여 `System.Collections.Generic` 네임스페이스를 나타내는 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.NameSyntax?displayProperty=nameWithType>를 생성합니다.

다음 using 지시문을 `Program.cs` 파일의 맨 위에 추가하여 <xref:Microsoft.CodeAnalysis.CSharp.SyntaxFactory> 클래스의 팩터리 메서드와 <xref:System.Console>의 메서드를 가져오면 나중에 이러한 항목을 정규화하지 않고 사용할 수 있습니다.

[!code-csharp[import the SyntaxFactory class](../../../../samples/csharp/roslyn-sdk/SyntaxTransformationQuickStart/ConstructionCS/Program.cs#StaticUsings "import the Syntax Factory class and the System.Console class")]

**name syntax nodes**를 만들어 `using System.Collections.Generic;` 문을 나타내는 트리를 빌드합니다. <xref:Microsoft.CodeAnalysis.CSharp.Syntax.NameSyntax>는 C#에 나타나는 네 가지 형식의 이름에 대한 기본 클래스입니다. 다음 네 가지 형식의 이름을 함께 작성하여 C# 언어로 표시할 수 있는 이름을 만듭니다.

* <xref:Microsoft.CodeAnalysis.CSharp.Syntax.NameSyntax?displayProperty=nameWithType> - `System` 및 `Microsoft` 같은 단순 단일 식별자 이름을 나타냅니다.
* <xref:Microsoft.CodeAnalysis.CSharp.Syntax.GenericNameSyntax?displayProperty=nameWithType> - `List<int>` 같은 제네릭 형식 또는 메서드 이름을 나타냅니다.
* <xref:Microsoft.CodeAnalysis.CSharp.Syntax.QualifiedNameSyntax?displayProperty=nameWithType> - `System.IO` 같은 폼 `<left-name>.<right-identifier-or-generic-name>`의 정규화된 이름을 나타냅니다.
* <xref:Microsoft.CodeAnalysis.CSharp.Syntax.AliasQualifiedNameSyntax?displayProperty=nameWithType> - `LibraryV2::Foo` 같은 어셈블리 extern 별칭을 사용하는 이름을 나타냅니다.

<xref:Microsoft.CodeAnalysis.CSharp.SyntaxFactory.IdentifierName(System.String)> 메서드를 사용하여 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.NameSyntax> 노드를 만듭니다. `Program.cs`에서 `Main` 메서드에 다음 코드를 추가합니다.

[!code-csharp[create the system identifier](../../../../samples/csharp/roslyn-sdk/SyntaxTransformationQuickStart/ConstructionCS/Program.cs#CreateIdentifierName "Create and display the system name identifier")]

앞의 코드는 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.IdentifierNameSyntax> 개체를 만들고 이를 `name` 변수에 할당합니다. 대부분 Roslyn API는 기본 클래스를 반환하므로 관련 형식을 더 쉽게 사용할 수 있습니다. <xref:Microsoft.CodeAnalysis.CSharp.Syntax.QualifiedNameSyntax>를 빌드할 때 `name` 변수인 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.NameSyntax>를 재사용할 수 있습니다. 샘플을 빌드할 때 형식 유추를 사용하지 마세요. 이 프로젝트에서 해당 단계를 자동화합니다.

이름을 만들었습니다. 이제 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.QualifiedNameSyntax>를 빌드하여 더 많은 노드를 트리로 빌드해 보겠습니다. 새 트리는 `name`을 이름의 왼쪽으로 사용하고 `Collections` 네임스페이스의 새 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.IdentifierNameSyntax>를 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.QualifiedNameSyntax>의 오른쪽으로 사용합니다. 다음 코드를 `program.cs`에 추가합니다.

[!code-csharp[create the collections identifier](../../../../samples/csharp/roslyn-sdk/SyntaxTransformationQuickStart/ConstructionCS/Program.cs#CreateQualifiedIdentifierName "Build the System.Collections identifier")]

코드를 다시 실행하고 결과를 확인합니다. 코드를 나타내는 노드 트리를 빌드하고 있습니다. 이 패턴을 계속해서 네임스페이스 `System.Collections.Generic`에 대한 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.QualifiedNameSyntax>를 빌드합니다. 다음 코드를 `Program.cs`에 추가합니다.

[!code-csharp[create the full identifier](../../../../samples/csharp/roslyn-sdk/SyntaxTransformationQuickStart/ConstructionCS/Program.cs#CreateFullNamespace "Build the System.Collections.Generic identifier")]

프로그램을 다시 실행하여 추가할 코드에 대한 트리를 빌드했는지 확인합니다.

### <a name="create-a-modified-tree"></a>수정된 트리 만들기

하나의 문을 포함하는 작은 구문 트리를 빌드했습니다. 단일 문 또는 기타 작은 코드 블록을 만드는 데는 새 노드를 만드는 API를 사용하는 것이 적합합니다. 그러나 더 큰 코드 블록을 빌드하려면 노드를 바꾸거나 노드를 기존 트리에 삽입하는 메서드를 사용해야 합니다. 구문 트리는 변경할 수 없습니다. **구문 API**는 생성 후 기존 구문 트리를 수정하기 위한 메커니즘을 제공하지 않습니다. 대신 기존 트리에 대한 변경 내용을 기반으로 새 트리를 생성하는 메서드를 제공합니다. `With*` 메서드는 <xref:Microsoft.CodeAnalysis.SyntaxNodeExtensions> 클래스에서 선언된 확장 메서드 또는 <xref:Microsoft.CodeAnalysis.SyntaxNode>에서 파생되는 구체적인 클래스에서 정의됩니다. 이러한 메서드는 기존 노드의 자식 속성에 변경 내용을 적용하여 새 노드를 만듭니다. 또한 <xref:Microsoft.CodeAnalysis.SyntaxNodeExtensions.ReplaceNode%2A> 확장 메서드를 사용하여 하위 트리의 하위 노드를 바꿀 수 있습니다. 이 메서드는 새로 만들어진 자식을 가리키도록 부모를 업데이트하고, 전체 트리에서 이 프로세스를 반복합니다(트리 ‘재회전’으로 알려진 프로세스). 

다음 단계에서는 전체(작은) 프로그램을 나타내는 트리를 만든 다음, 수정합니다. 다음 코드를 `Program` 클래스의 시작 부분에 추가합니다.

[!code-csharp[create a parse tree](../../../../samples/csharp/roslyn-sdk/SyntaxTransformationQuickStart/ConstructionCS/Program.cs#DeclareSampleCode "Create a tree that represents a small program")]

> [!NOTE]
> 예제 코드는 `System.Collections.Generic` 네임스페이스가 아닌 `System.Collections` 네임스페이스를 사용합니다.

다음으로 `Main` 메서드의 맨 아래에 다음 코드를 추가하여 텍스트를 구문 분석하고 트리를 만듭니다.

[!code-csharp[create a parse tree](../../../../samples/csharp/roslyn-sdk/SyntaxTransformationQuickStart/ConstructionCS/Program.cs#CreateParseTree "Create a tree that represents a small program")]

이 예제는 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.UsingDirectiveSyntax.WithName(Microsoft.CodeAnalysis.CSharp.Syntax.NameSyntax)?displayProperty=NameWithType> 메서드를 사용하여 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.UsingDirectiveSyntax> 노드의 이름을 이전 코드에서 생성된 이름으로 바꿉니다.

<xref:Microsoft.CodeAnalysis.CSharp.Syntax.UsingDirectiveSyntax.WithName(Microsoft.CodeAnalysis.CSharp.Syntax.NameSyntax)> 메서드를 통해 새 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.UsingDirectiveSyntax> 노드를 만들어 `System.Collections` 이름을 이전 코드에서 만든 이름으로 업데이트합니다. `Main` 메서드의 맨 아래에 다음 코드를 추가합니다.

[!code-csharp[create a new subtree](../../../../samples/csharp/roslyn-sdk/SyntaxTransformationQuickStart/ConstructionCS/Program.cs#BuildNewUsing "Create the subtree with the replaced namespace")]

프로그램을 실행하고 출력을 신중하게 확인합니다. `newusing`이 루트 트리에 없습니다. 원래 트리가 변경되지 않았습니다.

<xref:Microsoft.CodeAnalysis.SyntaxNodeExtensions.ReplaceNode%2A> 확장 메서드를 통해 다음 코드를 추가하여 새 트리를 만듭니다. 새 트리는 기존 가져오기를 업데이트된 `newUsing` 노드로 바꾼 결과입니다. 기존 `root` 변수에 이 새 트리를 할당합니다.

[!code-csharp[create a new root tree](../../../../samples/csharp/roslyn-sdk/SyntaxTransformationQuickStart/ConstructionCS/Program.cs#TransformTree "Create the transformed root tree with the replaced namespace")]

프로그램을 다시 실행합니다. 이제 트리가 `System.Collections.Generic` 네임스페이스를 올바르게 가져옵니다.

### <a name="transform-trees-using-syntaxrewriters"></a>`SyntaxRewriters`를 사용하여 트리 변환

`With*` 및 <xref:Microsoft.CodeAnalysis.SyntaxNodeExtensions.ReplaceNode%2A> 메서드는 구문 트리의 개별 분기를 변환하는 편리한 수단을 제공합니다. <xref:Microsoft.CodeAnalysis.CSharp.CSharpSyntaxRewriter?displayProperty=nameWithType> 클래스는 구문 트리에서 여러 변환을 수행합니다. <xref:Microsoft.CodeAnalysis.CSharp.CSharpSyntaxRewriter?displayProperty=nameWithType> 클래스는 <xref:Microsoft.CodeAnalysis.CSharp.CSharpSyntaxVisitor%601?displayProperty=nameWithType>의 서브클래스입니다. <xref:Microsoft.CodeAnalysis.CSharp.CSharpSyntaxRewriter>은 특정 형식의 <xref:Microsoft.CodeAnalysis.SyntaxNode>에 변환을 적용합니다. 구문 트리에 나타날 때마다 여러 형식의 <xref:Microsoft.CodeAnalysis.SyntaxNode> 개체에 변환을 적용할 수 있습니다. 이 빠른 시작의 두 번째 프로젝트는 형식 유추를 사용할 수 있는 모든 위치에서 지역 변수 선언의 명시적 형식을 제거하는 명령줄 리팩터링을 만듭니다.

새 C# **독립 실행형 코드 분석 도구** 프로젝트를 만듭니다. Visual Studio에서 `SyntaxTransformationQuickStart` 솔루션 노드를 마우스 오른쪽 단추로 클릭합니다. **추가** > **새 프로젝트**를 선택하여 **새 프로젝트 대화 상자**를 표시합니다. **Visual C#**  > **확장성** 아래에서 **독립 실행형 코드 분석 도구**를 선택합니다. 프로젝트 이름을 `TransformationCS`로 지정하고 [확인]을 클릭합니다.

첫 번째 단계는 <xref:Microsoft.CodeAnalysis.CSharp.CSharpSyntaxRewriter>에서 파생되는 클래스를 만들어 변환을 수행하는 것입니다. 프로젝트에 새 클래스 파일을 추가합니다. Visual Studio에서 **프로젝트** > **클래스 추가...** 를 선택합니다. **새 항목 추가** 대화 상자에서 파일 이름으로 `TypeInferenceRewriter.cs`를 입력합니다.

다음 using 지시문을 `TypeInferenceRewriter.cs` 파일에 추가합니다.

[!code-csharp[add necessary usings](../../../../samples/csharp/roslyn-sdk/SyntaxTransformationQuickStart/TransformationCS/TypeInferenceRewriter.cs#AddUsings "Add required usings")]

다음으로 `TypeInferenceRewriter` 클래스가 <xref:Microsoft.CodeAnalysis.CSharp.CSharpSyntaxRewriter> 클래스를 확장하도록 합니다.

[!code-csharp[add base class](../../../../samples/csharp/roslyn-sdk/SyntaxTransformationQuickStart/TransformationCS/TypeInferenceRewriter.cs#BaseClass "Add base class")]

다음 코드를 추가하여 <xref:Microsoft.CodeAnalysis.SemanticModel>을 포함할 전용 읽기 전용 필드를 선언하고 생성자에서 초기화합니다. 이 필드는 나중에 형식 유추를 사용할 수 있는 위치를 판별하는 데 필요합니다.

[!code-csharp[initialize members](../../../../samples/csharp/roslyn-sdk/SyntaxTransformationQuickStart/TransformationCS/TypeInferenceRewriter.cs#Construction "Declare and initialize member variables")]

<xref:Microsoft.CodeAnalysis.CSharp.CSharpSyntaxRewriter.VisitLocalDeclarationStatement(Microsoft.CodeAnalysis.CSharp.Syntax.LocalDeclarationStatementSyntax)> 메서드를 재정의합니다.

```csharp
public override SyntaxNode VisitLocalDeclarationStatement(LocalDeclarationStatementSyntax node)
{

}
```

> [!NOTE]
> 많은 Roslyn API는 반환된 실제 런타임 형식의 기본 클래스인 반환 형식을 선언합니다. 대부분 시나리오에서 한 종류의 노드는 다른 종류의 노드로 완전히 바뀌거나 제거될 수도 있습니다. 이 예제에서 <xref:Microsoft.CodeAnalysis.CSharp.CSharpSyntaxRewriter.VisitLocalDeclarationStatement(Microsoft.CodeAnalysis.CSharp.Syntax.LocalDeclarationStatementSyntax)> 메서드는 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.LocalDeclarationStatementSyntax> 파생 형식 대신 <xref:Microsoft.CodeAnalysis.SyntaxNode>를 반환합니다. 이 재작성기는 기존 노드를 기반으로 새 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.LocalDeclarationStatementSyntax> 노드를 반환합니다.

이 빠른 시작은 지역 변수 선언을 처리합니다. 이 선언은 `foreach` 루프, `for` 루프, LINQ식 및 람다 식과 같은 다른 선언으로 확장할 수 있습니다. 또한 이 재작성기는 가장 단순한 형식의 선언만 변환합니다.

```csharp
Type variable = expression;
```

혼자서 살펴보려면 다음 형식의 변수 선언에 대한 완료된 샘플을 확장해 보세요.

```csharp
// Multiple variables in a single declaration.
Type variable1 = expression1,
     variable2 = expression2;
// No initializer.
Type variable;
```

다음 코드를 `VisitLocalDeclarationStatement` 메서드의 본문에 추가하여 이러한 선언 형식의 재작성을 건너뜁니다.

[!code-csharp[exclude other declarations](../../../../samples/csharp/roslyn-sdk/SyntaxTransformationQuickStart/TransformationCS/TypeInferenceRewriter.cs#Exclusions "Exclude variables declarations not processed by this sample")]

이 메서드는 수정되지 않은 `node` 매개 변수를 반환하여 재작성이 발생하지 않음을 나타냅니다. 해당 `if` 식 모두가 true가 아닌 경우 노드는 초기화를 통해 가능한 선언을 나타냅니다. 다음 문을 추가하여 선언에 지정된 형식 이름을 추출하고 <xref:Microsoft.CodeAnalysis.SemanticModel> 필드를 통해 형식 이름을 바인딩하여 형식 기호를 얻습니다.

[!code-csharp[extract type name](../../../../samples/csharp/roslyn-sdk/SyntaxTransformationQuickStart/TransformationCS/TypeInferenceRewriter.cs#ExtractTypeSymbol "Extract the type name specified by the declaration")]

이제 이 문을 추가하여 이니셜라이저 식을 바인딩합니다.

[!code-csharp[bind initializer](../../../../samples/csharp/roslyn-sdk/SyntaxTransformationQuickStart/TransformationCS/TypeInferenceRewriter.cs#BindInitializer "Bind the initializer expressions")]

마지막으로 다음 `if` 문을 추가하여 이니셜라이저 식의 형식이 지정된 형식과 일치하는 경우 기존 형식 이름을 `var` 키워드로 바꿉니다.

[!code-csharp[ReplaceNode](../../../../samples/csharp/roslyn-sdk/SyntaxTransformationQuickStart/TransformationCS/TypeInferenceRewriter.cs#ReplaceNode "Replace the initializer node")]

선언은 이니셜라이저 식을 기본 클래스 또는 인터페이스로 캐스트할 수 있기 때문에 조건이 필요합니다. 필요한 경우 할당의 왼쪽 및 오른쪽에 있는 형식이 일치하지 않습니다. 이러한 사례에서 명시적 형식을 제거하면 프로그램의 의미 체계가 변경됩니다. `var`은 상황별 키워드이므로 `var`은 키워드가 아니라 식별자로 지정됩니다. 선행 및 후행 기타 정보(공백)는 세로 공백과 들여쓰기를 유지하기 위해 이전 형식 이름에서 `var` 키워드로 전송됩니다. 형식 이름은 실제로 선언문의 손자이므로 `With*` 대신 `ReplaceNode`를 사용하여 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.LocalDeclarationStatementSyntax>를 변환하는 것이 더 간단합니다.

`TypeInferenceRewriter`를 완료했습니다. 이제 `Program.cs` 파일로 돌아가서 예제를 완료합니다. 테스트 <xref:Microsoft.CodeAnalysis.Compilation>을 만들고 <xref:Microsoft.CodeAnalysis.SemanticModel>을 가져옵니다. <xref:Microsoft.CodeAnalysis.SemanticModel>을 사용하여 `TypeInferenceRewriter`를 시도합니다. 이 단계는 마지막으로 수행합니다. 그동안 테스트 컴파일을 나타내는 자리 표시자 변수를 선언합니다.

[!code-csharp[DeclareCompilation](../../../../samples/csharp/roslyn-sdk/SyntaxTransformationQuickStart/TransformationCS/Program.cs#DeclareTestCompilation "Declare the test compilation")]

잠시 후에 `CreateTestCompilation` 메서드가 없음을 보고하는 오류 물결선이 표시됩니다. **Ctrl+마침표**를 눌러 전구를 열고 Enter 키를 눌러 **메서드 스텁 생성** 명령을 호출합니다. 이 명령은 `Program` 클래스에서 `CreateTestCompilation` 메서드에 대한 메서드 스텁을 생성합니다. 나중에 돌아와서 이 메서드를 입력합니다.

![사용법에서 C# 메서드 생성](./media/syntax-transformation/generate-from-usage.png)

다음 코드를 작성하여 테스트 <xref:Microsoft.CodeAnalysis.Compilation>에서 각 <xref:Microsoft.CodeAnalysis.SyntaxTree>를 반복합니다. 각 트리에 대해 해당 트리의 <xref:Microsoft.CodeAnalysis.SemanticModel>을 사용하여 새 `TypeInferenceRewriter`를 초기화합니다.

[!code-csharp[IterateTrees](../../../../samples/csharp/roslyn-sdk/SyntaxTransformationQuickStart/TransformationCS/Program.cs#IterateTrees "Iterate all the source trees in the test compilation")]

직접 만든 `foreach` 문 내부에 다음 코드를 추가하여 각 소스 트리에서 변환을 수행합니다. 이 코드는 편집이 수행된 경우 변환된 새 트리를 조건부로 작성합니다. 재작성기는 형식 유추를 사용하여 단순화할 수 있는 하나 이상의 지역 변수 선언이 발생하는 경우에만 트리를 수정해야 합니다.

[!code-csharp[TransformTrees](../../../../samples/csharp/roslyn-sdk/SyntaxTransformationQuickStart/TransformationCS/Program.cs#TransformTrees "Transform and save any trees that are modified by the rewriter")]

`File.WriteAllText` 코드 아래에 물결선이 표시됩니다. 전구를 선택하고 필요한 `using System.IO;` 문을 추가합니다.

거의 완료되었습니다. 한 단계가 남았습니다. 테스트 <xref:Microsoft.CodeAnalysis.Compilation> 만들기. 이 빠른 시작 중에 형식 유추를 사용하지 않았으므로 완벽한 테스트 사례를 만들었습니다. 그러나 C# 프로젝트 파일에서 컴파일을 만드는 작업은 이 연습의 범위를 벗어납니다. 그래도 지침을 신중하게 수행했다면 희망적입니다. `CreateTestCompilation` 메서드의 내용을 다음 코드로 대체합니다. 이 코드는 이 빠른 시작에 설명된 프로젝트와 조건부로 일치하는 테스트 컴파일을 만듭니다.

[!code-csharp[CreateTestCompilation](../../../../samples/csharp/roslyn-sdk/SyntaxTransformationQuickStart/TransformationCS/Program.cs#CreateTestCompilation "Create a test compilation using the code written for this quickstart.")]

행운을 빌고 프로젝트를 실행합니다. Visual Studio에서 **디버그** > **디버깅 시작**을 선택합니다. Visual Studio에서 프로젝트의 파일이 변경되었다는 메시지가 표시됩니다. “**모두 예**”를 클릭하여 수정된 파일을 다시 로드합니다. 해당 파일을 살펴보면 놀라운 것을 관찰할 수 있습니다. 모든 명시적 및 중복 형식 지정자가 없는 코드는 놀라울 정도로 깔끔해 보입니다.

지금까지 **컴파일러 API**를 사용하여 C# 프로젝트에서 특정 구문 패턴에 대한 모든 파일을 검색하고, 해당 패턴과 일치하는 소스 코드의 의미 체계를 분석하고, 소스 코드를 변환하는 고유한 리팩터링을 작성했습니다. 이제 공식적으로 리팩터링 작성자가 되었습니다.
