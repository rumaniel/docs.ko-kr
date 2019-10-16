---
title: '자습서: 첫 번째 분석기 및 코드 수정 작성'
description: 이 자습서에서는 .NET Complier SDK(Roslyn API)를 사용하여 분석기 및 코드 수정 사항을 빌드하는 단계별 지침을 제공합니다.
ms.date: 08/01/2018
ms.custom: mvc
ms.openlocfilehash: d6645a2a6e83f68c1959c255756393c9251dc1ba
ms.sourcegitcommit: 6f28b709592503d27077b16fff2e2eacca569992
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/28/2019
ms.locfileid: "70105753"
---
# <a name="tutorial-write-your-first-analyzer-and-code-fix"></a>자습서: 첫 번째 분석기 및 코드 수정 작성

.NET Compiler Platform SDK는 C# 또는 Visual Basic 코드를 대상으로 하는 사용자 지정 경고를 만드는 데 필요한 도구를 제공합니다. **분석기**에는 규칙 위반을 인식하는 코드가 포함됩니다. **코드 수정 사항**에는 위반을 수정하는 코드가 포함됩니다. 구현하는 규칙은 코드 구조에서 코딩 스타일, 명명 규칙 등에 이를 수 있습니다. .NET Compiler Platform은 개발자가 코드를 작성할 때 분석을 실행하기 위한 프레임워크와 코드를 수정하기 위한 모든 Visual Studio UI 기능(편집기에 물결선 표시, Visual Studio 오류 목록 채우기, “전구” 제안 만들기, 제안된 수정 사항의 다양한 미리 보기 표시)을 제공합니다.

이 자습서에서는 Roslyn API를 사용하여 **분석기** 및 함께 제공되는 **코드 수정 사항**을 만드는 방법을 살펴봅니다. 분석기는 소스 코드 분석을 수행하고 사용자에게 문제를 보고하는 방법입니다. 필요한 경우 분석기는 사용자의 소스 코드에 대한 수정 사항을 나타내는 코드 수정 사항도 제공할 수 있습니다. 이 자습서에서는 `const` 한정자를 사용하여 선언할 수 있는 지역 변수 선언을 찾는 분석기를 만듭니다. 함께 제공되는 코드 수정 사항은 해당 선언을 수정하여 `const` 한정자를 추가합니다.

## <a name="prerequisites"></a>전제 조건

- [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/#visual-studio-2017-and-other-products)
- [Visual Studio 2019](https://www.visualstudio.com/downloads)

Visual Studio Intaller를 통해 **.NET Compiler Platform SDK**를 설치해야 합니다.

[!INCLUDE[interactive-note](~/includes/roslyn-installation.md)]

분석기를 만들고 유효성 검사하는 단계는 다음과 같습니다.

1. 솔루션을 만듭니다.
1. 분석기 이름 및 설명을 등록합니다.
1. 분석기 경고 및 권장 사항을 보고합니다.
1. 권장 사항을 허용하도록 코드 수정 사항을 구현합니다.
1. 단위 테스트를 통해 분석을 개선합니다.

## <a name="explore-the-analyzer-template"></a>분석기 템플릿 살펴보기

분석기는 지역 상수로 변환할 수 있는 모든 지역 변수 선언을 사용자에게 보고합니다. 예를 들어, 다음 코드를 고려하세요.

```csharp
int x = 0;
Console.WriteLine(x);
```

위의 코드에서 `x`는 상수 값이 할당되고 수정되지 않습니다. `const` 한정자를 사용하여 선언할 수 있습니다.

```csharp
const int x = 0;
Console.WriteLine(x);
```

변수를 상수로 설정할 수 있는지 여부를 판별하기 위한 분석이 포함되며, 변수가 작성되지 않는지 확인하려면 구문 분석, 상수 분석, 이니셜라이저 식의 상수 분석 및 데이터 흐름 분석이 필요합니다. .NET Compiler Platform은 이 분석을 보다 쉽게 수행할 수 있는 API를 제공합니다. 첫 번째 단계는 새로운 C# **코드 수정 사항이 포함된 분석기** 프로젝트는 만드는 것입니다.

- Visual Studio에서 **파일 > 새로 만들기 > 프로젝트...** 를 선택하여 [새 프로젝트] 대화 상자를 표시합니다.
- **Visual C# > 확장성**에서 **코드 수정 사항이 포함된 분석기(.NET Standard)** 를 선택합니다.
- 프로젝트 이름을 “**MakeConst**”로 지정하고 [확인]을 클릭합니다.

코드 수정 사항 템플릿이 포함된 분석기는 세 개의 프로젝트를 만듭니다. 하나에는 분석기 및 코드 수정 사항이 포함되고, 두 번째는 단위 테스트 프로젝트이고, 세 번째는 VSIX 프로젝트입니다. 기본 시작 프로젝트는 VSIX 프로젝트입니다. **F5** 키를 눌러 VSIX 프로젝트를 시작합니다. 그러면 새 분석기를 로드한 Visual Studio의 두 번째 인스턴스가 시작됩니다.

> [!TIP]
> 분석기를 실행할 때 Visual Studio의 두 번째 복사본을 시작합니다. 이 두 번째 복사본은 다른 레지스트리 하이브를 사용하여 설정을 저장합니다. 이렇게 하면 Visual Studio의 두 복사본에서 시각적 설정을 구별할 수 있습니다. Visual Studio의 실험 실행에 서로 다른 테마를 선택할 수 있습니다. 또한 Visual Studio의 실험 실행을 사용하여 사용자 설정 또는 로그인을 Visual Studio 계정에 로밍하지 마세요. 이렇게 하면 설정이 다르게 유지됩니다.

방금 시작한 두 번째 Visual Studio 인스턴스에서 새 C# 콘솔 애플리케이션 프로젝트를 만듭니다(.NET Core 또는 .NET Framework 프로젝트가 작동함 - 분석기는 소스 수준에서 작동함). 물결 무늬 밑줄이 있는 토큰을 마우스로 가리키면 분석기가 제공하는 경고 텍스트가 나타납니다.

템플릿은 다음 그림에 표시된 대로 형식 이름에 소문자가 포함된 각 형식 선언에 대한 경고를 보고하는 분석기를 만듭니다.

![분석기 보고 경고](media/how-to-write-csharp-analyzer-code-fix/report-warning.png)

또한 템플릿은 소문자를 포함하는 형식 이름을 모두 대문자로 변경하는 코드 수정 사항을 제공합니다. 경고와 함께 표시된 전구를 클릭하여 제안된 변경 내용을 확인할 수 있습니다. 제안된 변경 내용을 적용하면 솔루션에서 형식 이름과 해당 형식에 대한 모든 참조가 업데이트됩니다. 이제 초기 분석기가 작동 중임을 확인했으므로 두 번째 Visual Studio 인스턴스를 닫고 분석기 프로젝트로 돌아갑니다.

분석기의 모든 변경 내용을 테스트하기 위해 Visual Studio의 두 번째 복사본을 시작하고 새 코드를 만들 필요가 없습니다. 템플릿은 사용자 대신 단위 테스트 프로젝트를 만듭니다. 해당 프로젝트에는 두 개의 테스트가 포함됩니다. `TestMethod1`은 진단을 트리거하지 않고 코드를 분석하는 테스트의 일반적인 형식을 보여 줍니다. `TestMethod2`는 진단을 트리거하는 테스트의 형식을 보여 준 후 제안된 코드 수정 사항을 적용합니다. 분석기 및 코드 수정 사항을 빌드할 때 여러 코드 구조에 대한 테스트를 작성하여 작업을 확인합니다. 분석기에 대한 단위 테스트는 Visual Studio와 대화형으로 테스트하는 것보다 훨씬 빠릅니다.

> [!TIP]
> 분석기 단위 테스트는 분석기를 트리거해야 하는 코드 구문과 트리거하면 안 되는 코드 구문을 알고 있을 경우 유용한 도구입니다. Visual Studio의 또 다른 복사본에서 분석기를 로드하는 기능은 아직 고려하지 않은 구문을 탐색하고 찾는 데 유용한 도구입니다.

## <a name="create-analyzer-registrations"></a>분석기 등록 만들기

템플릿은 **MakeConstAnalyzer.cs** 파일에서 초기 `DiagnosticAnalyzer` 클래스를 만듭니다. 이 초기 분석기는 모든 분석기의 두 가지 중요한 속성을 표시합니다.

- 모든 진단 분석기는 사용되는 언어를 설명하는 `[DiagnosticAnalyzer]` 특성을 제공해야 합니다.
- 모든 진단 분석기는 <xref:Microsoft.CodeAnalysis.Diagnostics.DiagnosticAnalyzer> 클래스에서 파생되어야 합니다.

템플릿은 분석기의 일부인 기본 기능도 표시합니다.

1. 작업을 등록합니다. 작업은 코드에서 위반을 검사하기 위해 분석기를 트리거해야 하는 코드 변경을 나타냅니다. Visual Studio는 등록된 작업과 일치하는 코드 편집을 검색하면 분석기의 등록된 메서드를 호출합니다.
1. 진단을 만듭니다. 분석기는 위반을 검색하면 Visual Studio가 사용자에게 위반 사실을 알리는 데 사용하는 진단 개체를 만듭니다.

<xref:Microsoft.CodeAnalysis.Diagnostics.DiagnosticAnalyzer.Initialize(Microsoft.CodeAnalysis.Diagnostics.AnalysisContext)?displayProperty=nameWithType> 메서드의 재정의에 작업을 등록합니다. 이 자습서에서는 로컬 선언을 검색하는 **구문 노드**를 방문하고 그 중 상수 값이 있는 노드를 확인합니다. 선언이 상수일 수 있으면 분석기는 진단을 만들고 보고합니다.

첫 번째 단계는 이러한 상수가 “Make Const” 분석기를 나타내도록 등록 상수 및 `Initialize` 메서드를 업데이트하는 것입니다. 대부분의 문자열 상수는 문자열 리소스 파일에 정의됩니다. 더 쉽게 지역화하려면 해당 사례를 따라야 합니다. **MakeConst** 분석기 프로젝트에 대한 **Resources.resx** 파일을 엽니다. 리소스 편집기가 표시됩니다. 다음과 같이 문자열 리소스를 업데이트합니다.

- `AnalyzerTitle`을 “Variable can be made constant”(변수를 상수로 설정할 수 있음)로 변경합니다.
- `AnalyzerMessageFormat`을 “Can be made constant”(상수로 설정할 수 있음)로 변경합니다.
- `AnalyzerDescription`을 “Make Constant”(상수 만들기)로 변경합니다.

또한 **액세스 한정자** 드롭다운을 `public`으로 변경합니다. 이렇게 하면 단위 테스트에서 이러한 상수를 더 쉽게 사용할 수 있습니다. 작업을 마치면 리소스 편집기가 다음 그림과 같이 표시됩니다.

![문자열 리소스 업데이트](media/how-to-write-csharp-analyzer-code-fix/update-string-resources.png)

나머지 변경 내용은 분석기 파일에 있습니다. Visual Studio에서 **MakeConstAnalyzer.cs**를 엽니다. 등록된 작업을 기호에 적용되는 작업에서 구문에 적용되는 작업으로 변경합니다. `MakeConstAnalyzerAnalyzer.Initialize` 메서드에서 기호에 대한 작업을 등록하는 줄을 찾습니다.

```csharp
context.RegisterSymbolAction(AnalyzeSymbol, SymbolKind.NamedType);
```

해당 줄을 다음 줄로 바꿉니다.

[!code-csharp[Register the node action](~/samples/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst/MakeConstAnalyzer.cs#RegisterNodeAction "Register a node action")]

변경한 후 `AnalyzeSymbol` 메서드를 삭제할 수 있습니다. 이 분석기는 <xref:Microsoft.CodeAnalysis.SymbolKind.NamedType?displayProperty=nameWithType> 문이 아니라 <xref:Microsoft.CodeAnalysis.CSharp.SyntaxKind.LocalDeclarationStatement?displayProperty=nameWithType>을 검사합니다. `AnalyzeNode` 아래에 빨간색 물결선이 있습니다. 방금 추가한 코드는 선언되지 않은 `AnalyzeNode` 메서드를 참조합니다. 다음 코드를 사용하여 메서드를 선언합니다.

```csharp
private void AnalyzeNode(SyntaxNodeAnalysisContext context)
{
}
```

다음 코드에 표시된 대로 **MakeConstAnalyzer.cs**에서 `Category`를 “Usage”(사용법)로 변경합니다.

```csharp
private const string Category = "Usage";
```

## <a name="find-local-declarations-that-could-be-const"></a>const일 수 있는 로컬 선언 찾기

이제 `AnalyzeNode` 메서드의 첫 번째 버전을 작성하겠습니다. 다음 코드와 같이 `const`일 수 있지만 그렇지 않은 단일 로컬 선언을 찾아야 합니다.

```csharp
int x = 0;
Console.WriteLine(x);
```

첫 번째 단계는 로컬 선언을 찾는 것입니다. **MakeConstAnalyzer.cs**에서 `AnalyzeNode`에 다음 코드를 추가합니다.

```csharp
var localDeclaration = (LocalDeclarationStatementSyntax)context.Node;
```

분석기는 로컬 선언의 변경 내용 및 로컬 선언만을 위해 등록되었으므로 이 캐스트는 항상 성공합니다. 다른 노드 형식은 `AnalyzeNode` 메서드 호출을 트리거하지 않습니다. 그런 다음, 선언에서 `const` 한정자를 확인합니다. 한정자를 찾으면 즉시 반환합니다. 다음 코드는 로컬 선언에서 `const` 한정자를 검색합니다.

```csharp
// make sure the declaration isn't already const:
if (localDeclaration.Modifiers.Any(SyntaxKind.ConstKeyword))
{
    return;
}
```

마지막으로 변수가 `const`일 수 있는지 확인해야 합니다. 즉, 초기화된 후 절대 할당되지 않는지 확인합니다.

<xref:Microsoft.CodeAnalysis.Diagnostics.SyntaxNodeAnalysisContext>를 사용하여 몇 가지 의미 체계 분석을 수행합니다. `context` 인수를 사용하여 지역 변수 선언을 `const`로 설정할 수 있는지 확인합니다. <xref:Microsoft.CodeAnalysis.SemanticModel?displayProperty=nameWithType>은 단일 소스 파일에 있는 모든 의미 체계 정보를 나타냅니다. [의미 체계 모델](../work-with-semantics.md)을 다루는 문서에서 자세히 알아볼 수 있습니다. <xref:Microsoft.CodeAnalysis.SemanticModel?displayProperty=nameWithType>을 사용하여 로컬 선언 문에 대한 데이터 흐름 분석을 수행합니다. 그런 다음, 이 데이터 흐름 분석의 결과를 사용하여 지역 변수가 다른 곳에서 새 값으로 작성되지 않았는지 확인합니다. <xref:Microsoft.CodeAnalysis.ModelExtensions.GetDeclaredSymbol%2A> 확장 메서드를 호출하여 변수의 <xref:Microsoft.CodeAnalysis.ILocalSymbol>을 검색하고 해당 변수가 데이터 흐름 분석의 <xref:Microsoft.CodeAnalysis.DataFlowAnalysis.WrittenOutside%2A?displayProperty=nameWithType> 컬렉션에 포함되어 있지 않은지 확인합니다. `AnalyzeNode` 메서드의 끝에 다음 코드를 추가합니다.

```csharp
// Perform data flow analysis on the local declaration.
var dataFlowAnalysis = context.SemanticModel.AnalyzeDataFlow(localDeclaration);

// Retrieve the local symbol for each variable in the local declaration
// and ensure that it is not written outside of the data flow analysis region.
var variable = localDeclaration.Declaration.Variables.Single();
var variableSymbol = context.SemanticModel.GetDeclaredSymbol(variable);
if (dataFlowAnalysis.WrittenOutside.Contains(variableSymbol))
{
    return;
}
```

방금 추가된 코드는 변수가 수정되지 않았고 이에 따라 `const`로 설정될 수 있는지 확인합니다. 이제 진단을 실행하겠습니다. 다음 코드를 `AnalyzeNode`의 마지막 줄로 추가합니다.

```csharp
context.ReportDiagnostic(Diagnostic.Create(Rule, context.Node.GetLocation()));
```

**F5** 키를 눌러 분석기를 실행하여 진행 상황을 확인할 수 있습니다. 이전에 만든 콘솔 애플리케이션을 로드한 후 다음 테스트 코드를 추가할 수 있습니다.

```csharp
int x = 0;
Console.WriteLine(x);
```

전구가 표시되고 분석기가 진단을 보고해야 합니다. 그러나 전구는 템플릿에서 생성된 코드 수정 사항을 계속 사용하고 대문자로 설정될 수 있음을 알려 줍니다. 다음 섹션에서는 코드 수정 사항을 작성하는 방법을 설명합니다.

## <a name="write-the-code-fix"></a>코드 수정 사항 작성

분석기는 하나 이상의 코드 수정 사항을 제공할 수 있습니다. 코드 수정 사항은 보고된 문제를 해결하는 편집을 정의합니다. 직접 작성한 분석기의 경우 const 키워드를 삽입하는 코드 수정 사항을 제공할 수 있습니다.

```csharp
const int x = 0;
Console.WriteLine(x);
```

사용자가 편집기에서 전구 UI를 선택하면 Visual Studio가 코드를 변경합니다.

템플릿에서 추가된 **MakeConstCodeFixProvider.cs** 파일을 엽니다.  이 코드 수정 사항은 진단 분석기에서 생성된 진단 ID에 연결되어 있지만 아직 적합한 코드 변환을 구현하지 않습니다. 먼저 일부 템플릿 코드를 제거해야 합니다. 제목 문자열을 “Make constant”(상수 만들기)로 변경합니다.

[!code-csharp[Update the CodeFix title](~/samples/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst/MakeConstCodeFixProvider.cs#CodeFixTitle "Update the CodeFix title")]

그런 다음, `MakeUppercaseAsync` 메서드를 삭제합니다. 코드가 더 이상 적용되지 않습니다.

모든 코드 픽스 공급자는 <xref:Microsoft.CodeAnalysis.CodeFixes.CodeFixProvider>에서 파생됩니다. 모두 <xref:Microsoft.CodeAnalysis.CodeFixes.CodeFixProvider.RegisterCodeFixesAsync(Microsoft.CodeAnalysis.CodeFixes.CodeFixContext)?displayProperty=nameWithType>을 재정의하여 사용 가능한 코드 수정 사항을 보고합니다. `RegisterCodeFixesAsync`에서 진단과 일치하도록 검색 중인 상위 노드 형식을 <xref:Microsoft.CodeAnalysis.CSharp.Syntax.LocalDeclarationStatementSyntax>로 변경합니다.

[!code-csharp[Find local declaration node](~/samples/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst/MakeConstCodeFixProvider.cs#FindDeclarationNode  "Find the local declaration node that raised the diagnostic")]

그런 다음, 마지막 줄을 변경하여 코드 수정 사항을 등록합니다. 이 수정은 기존 선언에 `const` 한정자를 추가함으로써 생성되는 새 문서를 만듭니다.

[!code-csharp[Register the new code fix](~/samples/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst/MakeConstCodeFixProvider.cs#RegisterCodeFix  "Register the new code fix")]

방금 추가한 기호 `MakeConstAsync`에 대한 코드에 빨간색 물결선이 표시됩니다. 다음 코드와 같이 `MakeConstAsync`에 대한 선언을 추가합니다.

```csharp
private async Task<Document> MakeConstAsync(Document document,
   LocalDeclarationStatementSyntax localDeclaration,
   CancellationToken cancellationToken)
{
}
```

새 `MakeConstAsync` 메서드는 사용자의 소스 파일을 나타내는 <xref:Microsoft.CodeAnalysis.Document>를 현재 `const` 선언이 포함된 새 <xref:Microsoft.CodeAnalysis.Document>로 변환합니다.

선언 문 앞에 삽입할 새 `const` 키워드 토큰을 만듭니다. 먼저 선언 문의 첫 번째 토큰에서 선행 trivia를 제거하고 이를 `const` 토큰에 연결해야 합니다. `MakeConstAsync` 메서드에 다음 코드를 추가합니다.

[!code-csharp[Create a new const keyword token](~/samples/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst/MakeConstCodeFixProvider.cs#CreateConstToken  "Create the new const keyword token")]

그런 다음, 다음 코드를 사용하여 `const` 토큰을 선언에 추가합니다.

```csharp
// Insert the const token into the modifiers list, creating a new modifiers list.
var newModifiers = trimmedLocal.Modifiers.Insert(0, constToken);
// Produce the new local declaration.
var newLocal = trimmedLocal
    .WithModifiers(newModifiers)
    .WithDeclaration(localDeclaration.Declaration);
```

그런 다음, C# 형식 지정 규칙과 일치하도록 새 선언의 형식을 지정합니다. 기존 코드와 일치하도록 변경 내용의 형식을 지정하면 향상된 환경이 생성됩니다. 기존 코드 바로 뒤에 다음 문을 추가합니다.

[!code-csharp[Format the new declaration](~/samples/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst/MakeConstCodeFixProvider.cs#FormatLocal  "Format the new declaration")]

이 코드에는 새 네임스페이스가 필요합니다. 다음 `using` 문을 파일의 맨 위에 추가합니다.

```csharp
using Microsoft.CodeAnalysis.Formatting;
```

마지막 단계는 편집을 만드는 것입니다. 이 프로세스는 다음 3개 단계로 구성됩니다.

1. 기존 문서에 대한 핸들을 가져옵니다.
1. 기존 선언을 새 선언으로 바꿔서 새 문서를 만듭니다.
1. 새 문서를 반환합니다.

`MakeConstAsync` 메서드의 끝에 다음 코드를 추가합니다.

[!code-csharp[replace the declaration](~/samples/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst/MakeConstCodeFixProvider.cs#ReplaceDocument  "Generate a new document by replacing the declaration")]

코드 수정 사항을 시도할 준비가 되었습니다.  F5 키를 눌러 Visual Studio의 두 번째 인스턴스에서 분석기 프로젝트를 실행합니다. Visual Studio의 두 번째 인스턴스에서 새 C# 콘솔 애플리케이션 프로젝트를 만들고 상수 값으로 초기화된 몇 개의 지역 변수 선언을 Main 메서드에 추가합니다. 아래와 같이 경고로 보고되었음을 알 수 있습니다.

![const 경고를 만들 수 있음](media/how-to-write-csharp-analyzer-code-fix/make-const-warning.png)

많은 과정을 진행했습니다. `const`로 설정될 수 있는 선언 아래에 물결선이 있습니다. 그러나 아직 해야 할 일이 있습니다. `i`, `j` 및 `k`로 시작하는 세 개의 선언에 순서대로 `const`를 추가하면 이 코드가 제대로 작동합니다. 그러나 `const` 한정자를 `k`부터 다른 순서로 추가하면 분석기에서 오류가 발생합니다. `i` 및 `j`가 둘 다 `const`가 될 때까지 `k`는 `const`로 선언될 수 없습니다. 변수를 선언하고 초기화할 수 있는 다양한 방법을 처리하도록 하려면 추가 분석을 수행해야 합니다.

## <a name="build-data-driven-tests"></a>데이터 기반 테스트 빌드

분석기 및 코드 수정 사항은 const로 설정될 수 있는 단일 선언의 간단한 사례에 적용됩니다. 이 구현으로 인해 오류가 발생할 수 있는 많은 선언 문이 있습니다. 템플릿에서 작성된 단위 테스트 라이브러리를 사용하여 이러한 사례를 해결합니다. 이 방법은 Visual Studio의 두 번째 복사본을 반복적으로 여는 것보다 훨씬 더 빠릅니다.

단위 테스트 프로젝트에서 **MakeConstUnitTests.cs** 파일을 엽니다. 템플릿은 분석기 및 코드 수정 사항 단위 테스트에 대한 두 개의 공통 패턴을 따르는 두 개의 테스트를 만들었습니다. `TestMethod1`은 분석기가 보고하면 안 될 때 진단을 보고하지 않는지 확인하는 테스트 패턴을 보여 줍니다. `TestMethod2`는 진단을 보고하고 코드 수정 사항을 실행하기 위한 패턴을 보여 줍니다.

분석기의 거의 모든 테스트에 대한 코드는 이러한 두 패턴 중 하나를 따릅니다. 첫 번째 단계에서는 이러한 테스트를 데이터 기반 테스트로 재작업할 수 있습니다. 그런 다음, 다른 테스트 입력을 나타내기 위한 새 문자열 상수를 추가하여 새 테스트를 쉽게 만들 수 있습니다.

효율성을 위해 첫 번째 단계는 두 테스트를 데이터 기반 테스트로 리팩터링하는 것입니다. 그런 다음, 각각 새 테스트에 대한 두 개의 문자열 상수를 정의하면 됩니다. 리팩터링하는 동안 두 메서드의 이름을 더 나은 이름으로 바꿉니다. `TestMethod1`을 진단이 실행되지 않는지 확인하는 이 테스트로 바꿉니다.

```csharp
[DataTestMethod]
[DataRow("")]
public void WhenTestCodeIsValidNoDiagnosticIsTriggered(string testCode)
{
    VerifyCSharpDiagnostic(testCode);
}
```

진단이 경고를 트리거하지 않도록 해야 하는 코드 조각을 정의하여 이 테스트에 대한 새 데이터 행을 만들 수 있습니다. `VerifyCSharpDiagnostic`의 이 오버로드는 소스 코드 조각에 대해 트리거된 진단이 없는 경우에 성공합니다.

다음으로, `TestMethod2`를 진단이 실행되고 소스 코드 조각에 대한 코드 수정 사항이 적용되는지 확인하는 이 테스트로 바꿉니다.

```csharp
[DataTestMethod]
[DataRow(LocalIntCouldBeConstant, LocalIntCouldBeConstantFixed, 10, 13)]
public void WhenDiagnosticIsRaisedFixUpdatesCode(
    string test,
    string fixTest,
    int line,
    int column)
{
    var expected = new DiagnosticResult
    {
        Id = MakeConstAnalyzer.DiagnosticId,
        Message = new LocalizableResourceString(nameof(MakeConst.Resources.AnalyzerMessageFormat), MakeConst.Resources.ResourceManager, typeof(MakeConst.Resources)).ToString(),
        Severity = DiagnosticSeverity.Warning,
        Locations =
            new[] {
                    new DiagnosticResultLocation("Test0.cs", line, column)
                }
    };

    VerifyCSharpDiagnostic(test, expected);

    VerifyCSharpFix(test, fixTest);
}
```

이전 코드에서도 예상 진단 결과를 빌드하는 두 개의 변경 내용을 코드에 적용했습니다. 이전 코드는 `MakeConst` 분석기에 등록된 공용 상수를 사용합니다. 또한 입력 및 수정된 소스에 두 개의 문자열 상수를 사용합니다. `UnitTest` 클래스에 다음 문자열 상수를 추가합니다.

[!code-csharp[string constants for fix test](~/samples/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst.Test/MakeConstUnitTests.cs#FirstFixTest "string constants for fix test")]

이러한 두 테스트를 실행하여 성공하는지 확인합니다. Visual Studio에서 **테스트** > **Windows** > **테스트 탐색기**를 선택하여 **테스트 탐색기**를 엽니다.  **모두 실행** 링크를 누릅니다.

## <a name="create-tests-for-valid-declarations"></a>유효한 선언에 대한 테스트 만들기

일반적으로 분석기는 가능한 한 빨리 종료되어야 하므로 최소한의 작업을 수행합니다. Visual Studio는 등록된 분석기를 사용자 편집 코드로 호출합니다. 응답은 키 요구 사항입니다. 진단을 실행하지 않아야 하는 코드에 대한 여러 가지 테스트 사례가 있습니다. 분석기가 이미 이러한 테스트 중 하나를 처리합니다. 이 경우 변수는 초기화된 후에 할당됩니다. 다음 문자열 상수를 테스트에 추가하여 해당 사례를 나타냅니다.

[!code-csharp[variable assigned](~/samples/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst.Test/MakeConstUnitTests.cs#VariableAssigned "a variable that is assigned after being initialized won't raise the diagnostic")]

그런 다음, 아래 코드 조각에 표시된 대로 이 테스트의 데이터 행을 추가합니다.

```csharp
[DataTestMethod]
[DataRow(""),
 DataRow(VariableAssigned)]
public void WhenTestCodeIsValidNoDiagnosticIsTriggered(string testCode)
```

이 테스트도 성공합니다. 다음으로, 아직 처리하지 않은 조건에 대한 상수를 추가합니다.

- 이미 상수이므로 이미 `const`인 선언:

   [!code-csharp[already const declaration](~/samples/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst.Test/MakeConstUnitTests.cs#AlreadyConst "a declaration that is already const should not raise the diagnostic")]

- 사용할 값이 없으므로 이니셜라이저가 없는 선언:

   [!code-csharp[declarations that have no initializer](~/samples/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst.Test/MakeConstUnitTests.cs#NoInitializer "a declaration that has no initializer should not raise the diagnostic")]

- 컴파일 시간 상수일 수 없으므로 이니셜라이저가 상수가 아닌 선언:

   [!code-csharp[declarations where the initializer isn't const](~/samples/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst.Test/MakeConstUnitTests.cs#InitializerNotConstant "a declaration where the initializer is not a compile-time constant should not raise the diagnostic")]

C#은 여러 선언을 하나의 문으로 허용하므로 훨씬 더 복잡할 수 있습니다. 다음 테스트 사례 문자열 상수를 고려합니다.

[!code-csharp[multiple initializers](~/samples/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst.Test/MakeConstUnitTests.cs#MultipleInitializers "A declaration can be made constant only if all variables in that statement can be made constant")]

`i` 변수는 상수로 설정될 수 있지만, `j` 변수는 상수로 설정될 수 없습니다. 따라서 이 문은 const 선언으로 설정될 수 없습니다. 다음 모든 테스트에 대한 `DataRow` 선언을 추가합니다.

```csharp
[DataTestMethod]
[DataRow(""),
    DataRow(VariableAssigned),
    DataRow(AlreadyConst),
    DataRow(NoInitializer),
    DataRow(InitializerNotConstant),
    DataRow(MultipleInitializers)]
public void WhenTestCodeIsValidNoDiagnosticIsTriggered(string testCode)
```

테스트를 다시 실행하면 새 테스트 사례가 실패합니다.

## <a name="update-your-analyzer-to-ignore-correct-declarations"></a>올바른 선언을 무시하도록 분석기 업데이트

이러한 조건과 일치하는 코드를 필터링하려면 분석기의 `AnalyzeNode` 메서드에 대한 몇 가지 개선 사항이 필요합니다. 개선 사항은 모두 관련된 조건이므로 유사한 변경 내용이 이러한 모든 조건을 수정합니다. `AnalyzeNode`에 다음 변경 내용을 적용합니다.

- 의미 체계 분석이 단일 변수 선언을 검사했습니다. 이 코드는 동일한 문에 선언된 모든 변수를 검사하는 `foreach` 루프에 있어야 합니다.
- 선언된 각 변수에는 이니셜라이저가 있어야 합니다.
- 선언된 각 변수의 이니셜라이저는 컴파일 시간 상수여야 합니다.

`AnalyzeNode` 메서드에서 다음 원래 의미 체계 분석을

```csharp
// Perform data flow analysis on the local declaration.
var dataFlowAnalysis = context.SemanticModel.AnalyzeDataFlow(localDeclaration);

// Retrieve the local symbol for each variable in the local declaration
// and ensure that it is not written outside of the data flow analysis region.
var variable = localDeclaration.Declaration.Variables.Single();
var variableSymbol = context.SemanticModel.GetDeclaredSymbol(variable);
if (dataFlowAnalysis.WrittenOutside.Contains(variableSymbol))
{
    return;
}
```

다음 코드 조각으로 바꿉니다.

```csharp
// Ensure that all variables in the local declaration have initializers that
// are assigned with constant values.
foreach (var variable in localDeclaration.Declaration.Variables)
{
    var initializer = variable.Initializer;
    if (initializer == null)
    {
        return;
    }

    var constantValue = context.SemanticModel.GetConstantValue(initializer.Value);
    if (!constantValue.HasValue)
    {
        return;
    }
}

// Perform data flow analysis on the local declaration.
var dataFlowAnalysis = context.SemanticModel.AnalyzeDataFlow(localDeclaration);

foreach (var variable in localDeclaration.Declaration.Variables)
{
    // Retrieve the local symbol for each variable in the local declaration
    // and ensure that it is not written outside of the data flow analysis region.
    var variableSymbol = context.SemanticModel.GetDeclaredSymbol(variable);
    if (dataFlowAnalysis.WrittenOutside.Contains(variableSymbol))
    {
        return;
    }
}
```

첫 번째 `foreach` 루프는 구문 분석을 사용하여 각 변수 선언을 검사합니다. 첫 번째 검사는 변수에 이니셜라이저가 포함되도록 합니다. 두 번째 검사는 이니셜라이저가 상수가 되도록 합니다. 두 번째 루프에는 원래 의미 체계 분석이 있습니다. 의미 체계 검사는 성능에 더 큰 영향을 주므로 별도의 루프에 있습니다. 테스트를 다시 실행하면 테스트가 모두 성공으로 표시되어야 합니다.

## <a name="add-the-final-polish"></a>최종 폴란드어 추가

거의 완료되었습니다. 분석기가 처리할 몇 가지 추가 조건이 있습니다. 사용자가 코드를 작성하는 동안 Visual Studio가 분석기를 호출합니다. 분석기가 컴파일되지 않는 코드를 위해 호출되는 경우도 있습니다. 진단 분석기의 `AnalyzeNode` 메서드는 상수 값이 변수 형식으로 변환될 수 있는지 확인하지 않습니다. 따라서 현재 구현은 int i = "abc"'와 같은 잘못된 선언을 로컬 상수로 변환합니다. 해당 조건에 대한 소스 문자열 상수를 추가합니다.

[!code-csharp[Mismatched types don't raise diagnostics](~/samples/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst.Test/MakeConstUnitTests.cs#DeclarationIsInvalid "When the variable type and the constant type don't match, there's no diagnostic")]

또한 참조 형식이 제대로 처리되지 않습니다. 참조 형식에 허용되는 유일한 상수 값은 문자열 리터럴을 허용하는 <xref:System.String?displayProperty=nameWIthType>의 이 경우를 제외하고 `null`입니다. 즉, `const string s = "abc"`는 적합하지만 `const object s = "abc"`는 적합하지 않습니다. 이 코드 조각은 해당 조건을 확인합니다.

[!code-csharp[Reference types don't raise diagnostics](~/samples/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst.Test/MakeConstUnitTests.cs#DeclarationIsntString "When the variable type is a reference type other than string, there's no diagnostic")]

철저하게 하려면 문자열에 대한 상수 선언을 만들 수 있는지 확인하는 또 다른 테스트를 추가해야 합니다. 다음 코드 조각은 진단을 실행하는 코드 및 수정 사항이 적용된 후의 코드를 둘 다 정의합니다.

[!code-csharp[string reference types raise diagnostics](~/samples/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst.Test/MakeConstUnitTests.cs#ConstantIsString "When the variable type is string, it can be constant")]

마지막으로 변수가 `var` 키워드를 사용하여 선언된 경우 코드 수정 사항은 잘못된 작업을 수행하고 `const var` 선언을 생성하며, 이는 C# 언어에서 지원되지 않습니다. 이 버그를 수정하려면 코드 수정 사항이 `var` 키워드를 유추 형식 이름으로 바꾸어야 합니다.

[!code-csharp[var references need to use the inferred types](~/samples/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst.Test/MakeConstUnitTests.cs#VarDeclarations "Declarations made using var must have the type replaced with the inferred type")]

이러한 변경은 두 테스트에 대한 데이터 행 선언을 업데이트합니다. 다음 코드는 모든 데이터 행 특성을 사용하여 이러한 테스트를 보여 줍니다.

[!code-csharp[The finished tests](~/samples/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst.Test/MakeConstUnitTests.cs#FinishedTests "The finished tests for the make const analyzer")]

다행히도 위의 버그는 모두 방금 알아본 동일한 기술을 사용하여 해결할 수 있습니다.

첫 번째 버그를 수정하려면 먼저 **DiagnosticAnalyzer.cs**를 열고 상수 값과 함께 할당되었는지 확인하기 위해 각 로컬 선언의 이니셜라이저가 검사되는 foreach 루프를 찾습니다. 첫 번째 foreach 루프 바로 ‘앞’에서 `context.SemanticModel.GetTypeInfo()`를 호출하여 로컬 선언의 선언된 형식에 대한 자세한 정보를 검색합니다. 

```csharp
var variableTypeName = localDeclaration.Declaration.Type;
var variableType = context.SemanticModel.GetTypeInfo(variableTypeName).ConvertedType;
```

그런 다음, `foreach` 루프 내부에서 각 이니셜라이저를 검사하여 변수 형식으로 변환할 수 있는지 확인합니다. 이니셜라이저가 상수인지 확인한 후 다음 검사를 추가합니다.

```csharp
// Ensure that the initializer value can be converted to the type of the
// local declaration without a user-defined conversion.
var conversion = context.SemanticModel.ClassifyConversion(initializer.Value, variableType);
if (!conversion.Exists || conversion.IsUserDefined)
{
    return;
}
```

다음 변경은 마지막 항목을 기반으로 빌드됩니다. 첫 번째 foreach 루프의 닫는 중괄호 앞에 다음 코드를 추가하여 상수가 문자열 또는 null일 때 로컬 선언의 형식을 검사합니다.

```csharp
// Special cases:
//  * If the constant value is a string, the type of the local declaration
//    must be System.String.
//  * If the constant value is null, the type of the local declaration must
//    be a reference type.
if (constantValue.Value is string)
{
    if (variableType.SpecialType != SpecialType.System_String)
    {
        return;
    }
}
else if (variableType.IsReferenceType && constantValue.Value != null)
{
    return;
}
```

var' 키워드를 올바른 형식 이름으로 바꾸려면 코드 수정 사항 공급자에서 약간의 코드를 추가로 작성해야 합니다. **CodeFixProvider.cs**로 돌아갑니다. 추가할 코드는 다음 단계를 수행합니다.

- 선언이 `var` 선언인지, 그리고 다음과 같은지 검사합니다.
- 유추 형식에 대한 새 형식을 만듭니다.
- 형식 선언이 별칭이 아닌지 확인합니다. 별칭이 아니면 `const var`을 선언하는 것이 적합합니다.
- `var`이 이 프로그램의 형식 이름이 아닌지 확인합니다. 아닌 경우 `const var`이 적합합니다.
- 전체 형식 이름 단순화

코드가 다소 많아 보이지만 그렇지 않습니다. `newLocal`을 선언 및 초기화하는 줄을 다음 코드로 바꿉니다. 코드는 `newModifiers` 초기화 바로 뒤에 옵니다.

[!code-csharp[Replace Var designations](~/samples/csharp/roslyn-sdk/Tutorials/MakeConst/MakeConst/MakeConstCodeFixProvider.cs#ReplaceVar "Replace a var designation with the explicit type")]

<xref:Microsoft.CodeAnalysis.Simplification.Simplifier> 형식을 사용하려면 하나의 `using` 문을 추가해야 합니다.

```csharp
using Microsoft.CodeAnalysis.Simplification;
```

테스트를 실행하면 모두 성공합니다. 완료된 분석기를 직접 실행할 수 있습니다. Ctrl+F5를 눌러 Roslyn 미리 보기 확장이 로드된 Visual Studio의 두 번째 인스턴스에서 분석기 프로젝트를 실행합니다.

- 두 번째 Visual Studio 인스턴스에서 새 C# 콘솔 애플리케이션 프로젝트를 만들고 `int x = "abc";`을 Main 메서드에 추가합니다. 첫 번째 버그 수정 덕분에 이 지역 변수 선언에 대한 경고가 보고되지 않습니다(컴파일러 오류는 예상대로 발생함).
- 그런 다음, `object s = "abc";`을 Main 메서드에 추가합니다. 두 번째 버그 수정으로 인해 경고가 보고되지 않습니다.
- 마지막으로 `var` 키워드를 사용하는 다른 지역 변수를 추가합니다. 경고가 보고되고 제안이 왼쪽 바로 아래에 표시됩니다.
- 편집기 캐럿을 물결선 위로 이동하고 Ctrl+.를 눌러 제안된 코드 수정 사항을 표시합니다. 코드 수정 사항을 선택하면 var' 키워드가 올바르게 처리됩니다.

마지막으로 다음 코드를 추가합니다.

```csharp
int i = 2;
int j = 32;
int k = i + j;
```

이러한 변경 후에는 처음 두 개의 변수에만 빨간색 물결선이 표시됩니다. `i` 및 `j`에 `const`를 추가합니다. `const`일 수 있으므로 `k`에 새 경고가 표시됩니다.

지금까지 신속한 코드 분석을 수행하여 문제를 검색하고 수정하기 위한 빠른 수정 사항을 제공하는 첫 번째 .NET Compiler Platform 확장을 만들었습니다. 또한 .NET Compiler Platform SDK(Roslyn API)의 일부인 많은 코드 API를 알아보았습니다. 샘플 GitHub 리포지토리의 [완료된 샘플](https://github.com/dotnet/samples/tree/master/csharp/roslyn-sdk/Tutorials/MakeConst)을 기준으로 작업을 검사할 수 있습니다. 또는 [완료된 프로젝트의 zip 파일](https://github.com/dotnet/samples/blob/master/csharp/roslyn-sdk/Tutorials/MakeConst.zip)을 다운로드할 수 있습니다.

## <a name="other-resources"></a>기타 리소스

- [구문 분석 시작](../get-started/syntax-analysis.md)
- [의미 체계 분석 시작](../get-started/semantic-analysis.md)
