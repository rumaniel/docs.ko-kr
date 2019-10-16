---
title: Visual Studio에서 Roslyn 구문 시각화 도우미를 사용하여 코드 탐색
description: 구문 시각화 도우미는 .NET Compiler Platform SDK에서 코드용으로 생성하는 모델을 탐색할 수 있는 시각적 도구를 제공합니다.
ms.date: 03/07/2018
ms.custom: mvc, vs-dotnet
ms.openlocfilehash: fa3b4fdbb8d573805119e13e8aa93f156c4111f9
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972010"
---
# <a name="explore-code-with-the-roslyn-syntax-visualizer-in-visual-studio"></a>Visual Studio에서 Roslyn 구문 시각화 도우미를 사용하여 코드 탐색

이 아티클에서는 .NET Compiler Platform("Roslyn") SDK의 일부로 제공되는 구문 시각화 도우미 도구에 대한 개요를 제공합니다. 구문 시각화 도우미는 구문 트리를 검사하고 탐색하는 데 도움이 되는 도구 창입니다. 분석하려는 코드의 모델을 이해하는 데 필수적인 도구입니다. 또한 .NET Compiler Platform("Roslyn") SDK를 사용하여 자체 애플리케이션을 개발할 때 도움이 되는 디버깅 도구이기도 합니다. 첫 번째 분석기를 만들 때 이 도구를 엽니다. 시각화 도우미는 API에서 사용되는 모델을 이해하는 데 도움이 됩니다. [SharpLab](https://sharplab.io) 또는 [LINQPad](https://www.linqpad.net/)와 같은 도구를 사용하여 코드를 검사하고 구문 트리를 이해할 수도 있습니다.

[!INCLUDE[interactive-note](~/includes/roslyn-installation.md)]

[개요](compiler-api-model.md) 아티클을 읽고 .NET Compiler Platform SDK에서 사용된 개념을 숙지하세요. 구문 트리, 노드, 토큰 및 퀴즈에 대한 소개를 제공합니다.

## <a name="syntax-visualizer"></a>구문 시각화 도우미

**구문 시각화 도우미**를 사용하면 Visual Studio IDE 내의 현재 활성 편집기 창에서 C# 또는 VB 코드 파일에 대한 구문 트리를 검사할 수 있습니다. 시각화 도우미는 **보기** > **다른 창** > **구문 시각화 도우미**를 클릭하여 시작할 수 있습니다.  오른쪽 위 모서리에 있는 **빠른 실행** 도구 모음을 사용할 수도 있습니다. "구문"을 입력하면 **구문 시각화 도우미**를 여는 명령이 나타납니다.

이 명령은 구문 시각화 도우미를 부동 도구 창으로 엽니다. 코드 편집기 창이 열려 있지 않은 경우 다음 그림과 같이 디스플레이가 비어 있습니다. 

![구문 시각화 도우미 도구 창](media/syntax-visualizer/syntax-visualizer.png)

이 도구 창을 Visual Studio 내에서 왼쪽과 같이 편리한 위치에 고정합니다. 시각화 도우미에서는 현재 코드 파일에 대한 정보를 표시합니다.

**파일** > **새 프로젝트** 명령을 사용하여 새 프로젝트를 만듭니다. VB 또는 C# 프로젝트를 만들 수 있습니다. Visual Studio에서 이 프로젝트의 주 코드 파일을 열면 시각화 도우미는 구문 트리를 표시합니다. Visual Studio 인스턴스에서 기존 C#/VB 파일을 열 수 있으며 시각화 도우미는 해당 파일의 구문 트리를 표시합니다. Visual Studio 내에서 여러 코드 파일을 열면 시각화 도우미는 현재 활성 코드 파일(키보드 포커스가 있는 코드 파일)에 대한 구문 트리를 표시합니다.

<!-- markdownlint-disable MD025 -->

# <a name="ctabcsharp"></a>[C#](#tab/csharp)
![C# 구문 트리 시각화](media/syntax-visualizer/visualize-csharp.png)
# <a name="visual-basictabvb"></a>[Visual Basic](#tab/vb)
![VB 구문 트리 시각화](media/syntax-visualizer/visualize-visual-basic.png)

---

위 이미지에서와 같이 시각화 도우미 도구 창에는 구문 트리가 위에 표시되고 속성 그리드가 아래에 표시됩니다. 속성 그리드는 항목의 .NET *형식* 및 *종류*(SyntaxKind)를 포함하여 트리에서 현재 선택된 항목의 속성을 표시합니다.

구문 트리는 *노드*, *토큰* 및 *퀴즈*라는 세 가지 유형의 항목으로 구성됩니다. [구문을 사용하여 작업](work-with-syntax.md) 아티클에서 이러한 형식에 대해 자세히 읽을 수 있습니다. 각 형식의 항목은 다른 색을 사용하여 표시됩니다. 사용된 색에 대한 개요를 보려면 '범례' 단추를 클릭하세요.

트리의 각 항목에는 자체 **범위**도 표시됩니다. **범위**는 텍스트 파일에서 해당 노드의 인덱스(시작 및 끝 위치)입니다.  앞의 C# 예에서 선택한 “UsingKeyword [0..5)” 토큰에는 5자 너비 [0..5)인 **범위**가 있습니다. "[..)" 표기법은 시작 인덱스는 범위의 일부이지만 끝 인덱스는 아님을 의미합니다.

트리를 탐색하는 방법은 두 가지가 있습니다.

* 트리에서 항목을 확장하거나 클릭합니다. 시각화 도우미는 코드 편집기에서 이 항목의 범위에 해당하는 텍스트를 자동으로 선택합니다.
* 코드 편집기에서 텍스트를 클릭하거나 선택합니다. 앞의 VB 예제에서 코드 편집기에 "모듈 Module1"이 포함된 줄을 선택하면 시각화 도우미가 트리의 해당 ModuleStatement 노드로 자동 이동합니다. 

시각화 도우미는 트리에서 편집기의 선택된 텍스트 범위와 가장 일치하는 항목을 강조 표시합니다.

시각화 도우미는 활성 코드 파일의 수정 내용과 일치하도록 트리를 새로 고칩니다. `Main()` 내의 `Console.WriteLine()`에 대한 호출을 추가합니다. 입력할 때 시각화 도우미는 트리를 새로 고칩니다.

`Console.`을 입력하면 입력을 일시 중지합니다. 트리에는 분홍색으로 채색된 일부 항목이 있습니다. 이때 입력된 코드에는 오류(‘진단’이라고도 함)가 있습니다. 이러한 오류는 구문 트리의 노드, 토큰 및 퀴즈에 첨부됩니다. 시각화 도우미에서는 분홍색으로 배경을 강조 표시하여 어떤 항목에 오류가 첨부되어 있는지 보여줍니다. 항목을 마우스로 가리키면 분홍색으로 표시된 항목의 오류를 검사할 수 있습니다. 시각화 도우미는 구문 오류(입력된 코드의 구문과 관련된 오류)만 표시하고, 의미 체계 오류는 표시하지 않습니다.
 
## <a name="syntax-graphs"></a>구문 그래프

트리에서 원하는 항목을 마우스 오른쪽 단추로 클릭하고 **직접 구문 그래프 보기**를 클릭합니다. 

# <a name="ctabcsharp"></a>[C#](#tab/csharp)

시각화 도우미는 선택한 항목을 루트로 하는 하위 트리의 그래픽 표현을 표시합니다. C# 예제에서 `Main()`메서드에 해당하는 **MethodDeclaration** 노드에 대해 이 단계를 시도합니다. 시각화 도우미는 다음과 같이 보이는 구문 그래프를 표시합니다.

![C# 구문 그래프 보기](media/syntax-visualizer/csharp-syntax-graph.png)
# <a name="visual-basictabvb"></a>[Visual Basic](#tab/vb)

위의 VB 예제에서 `Main()` 메서드에 해당하는 **SubBlock** 노드에 대해 동일하게 시도합니다. 시각화 도우미는 다음과 같이 보이는 구문 그래프를 표시합니다.

![VB 구문 그래프 보기](media/syntax-visualizer/visual-basic-syntax-graph.png)

---

구문 그래프 뷰어에는 범례를 색칠 체계로 표시하는 옵션이 있습니다. 또한 구문 그래프의 개별 항목을 마우스로 가리키면 해당 항목에 해당하는 속성을 볼 수 있습니다.

트리의 여러 항목에 대한 구문 그래프를 반복적으로 볼 수 있으며 그래프는 항상 Visual Studio 내의 동일한 창에 표시됩니다. Visual Studio 내 편리한 위치에 이 창을 고정할 수 있으므로 새 구문 그래프를 보기 위해 탭 사이를 전환할 필요가 없습니다. 대개는 코드 편집기 창 아래쪽이 보기 편리합니다.

시각화 도우미 도구 창 및 구문 그래프 창과 함께 사용할 도킹 레이아웃은 다음과 같습니다.

![시각화 도우미 및 구문 그래프 창에 대한 도킹 레이아웃](media/syntax-visualizer/docking-layout.png)

또 다른 옵션은 듀얼 모니터 환경에서 두 번째 모니터에 구문 그래프 창을 배치하는 것입니다.

## <a name="inspecting-semantics"></a>의미 체계 검사

구문 시각화 도우미는 기호 및 의미 체계 정보에 대한 기본 검사를 수행합니다. C# 예제에서는 Main() 안에 `double x = 1 + 1;`을 입력합니다. 그런 다음, 코드 편집기 창에서 식 `1 + 1`을 선택합니다. 시각화 도우미는 시각화 도우미에서 **AddExpression** 노드를 강조 표시합니다. 이 **AddExpression**을 마우스 오른쪽 단추로 클릭하고 **기호 보기(있는 경우)** 를 클릭합니다. 대부분의 메뉴 항목에는 "해당되는 경우" 한정자가 있습니다. 구문 시각화 도우미는 모든 노드에 대해 나타나지 않을 수 있는 속성을 포함한 노드의 속성을 검사합니다. 

시각화 도우미의 속성 그리드는 다음 그림과 같이 업데이트됩니다. 식의 기호는 **Kind = Method**인 **SynthesizedIntrinsicOperatorSymbol**입니다.

![기호 속성](media/syntax-visualizer/symbol-properties.png)

동일한 **AddExpression** 노드에 대해 **TypeSymbol 보기(있는 경우)** 를 시도합니다. 시각화 도우미의 속성 그리드가 다음 그림과 같이 업데이트되어 선택한 식의 형식이 `Int32`임을 나타냅니다.

![TypeSymbol 속성](media/syntax-visualizer/type-symbol-properties.png)

동일한 **AddExpression** 노드에 대해 **변환된 TypeSymbol 보기(있는 경우)** 를 시도합니다. 다음 그림과 같이 식 형식이 `Int32`이지만 변환된 식 형식이 `Double`임을 나타내도록 속성 그리드가 업데이트됩니다. `Int32` 식은 `Double`로 변환되어야 하는 컨텍스트에서 발생하므로 이 노드에는 변환된 형식 기호 정보가 포함됩니다. 이 변환은 대입 연산자의 왼쪽에 있는 변수 `x`에 대해 지정된 `Double` 형식을 충족시킵니다.

![변환된 TypeSymbol 속성](media/syntax-visualizer/converted-type-symbol-properties.png)

마지막으로 동일한 **AddExpression** 노드에 대해 **상수 값 보기(있는 경우)** 를 시도합니다. 속성 그리드에서는 식의 값이 값 `2`인 컴파일 시간 상수를 보여줍니다.

![상수 값](media/syntax-visualizer/constant-value.png)

앞의 예제는 VB에서 복제될 수도 있습니다. VB 파일에 `Dim x As Double = 1 + 1`을 입력합니다. 코드 편집기 창에서 식 `1 + 1`을 선택합니다. 시각화 도우미는 시각화 도우미의 해당 **AddExpression** 노드를 강조 표시합니다. 이 **AddExpression**에 대해 앞의 단계를 반복하면 동일한 결과가 나타납니다.

VB에서 더 많은 코드를 검사합니다. 주 VB 파일을 다음 코드로 업데이트합니다.

```vb
Imports C = System.Console

Module Program
    Sub Main(args As String())
        C.WriteLine()
    End Sub
End Module
```

이 코드에서는 파일 위에 있는 `System.Console` 형식에 매핑되는 `C`라는 별칭을 소개하고 `Main()` 내부에서 이 별칭을 사용합니다. `Main()` 메서드 내에서 이 별칭(`C.WriteLine()`의 `C`)의 사용을 선택합니다. 시각화 도우미는 시각화 도우미에서 해당 **IdentifierName** 노드를 선택합니다. 이 노드를 마우스 오른쪽 단추로 클릭하고 **기호 보기(있는 경우)** 를 클릭합니다. 속성 그리드는 다음 그림과 같이 이 식별자가 형식 `System.Console`에 바인딩되어 있음을 나타냅니다.

![기호 속성](media/syntax-visualizer/symbol-visual-basic.png)

동일한 **IdentifierName** 노드에 대해 **AliasSymbol 보기(있는 경우)** 를 시도합니다. 속성 그리드는 식별자가 `System.Console` 대상에 바인딩된 이름이 `C`인 별칭임을 나타냅니다. 즉, 속성 그리드는 식별자 `C`에 해당하는 **AliasSymbol**에 대한 정보를 제공합니다.

![AliasSymbol 속성](media/syntax-visualizer/alias-symbol.png)

선언된 형식, 메서드, 속성에 해당하는 기호를 검사합니다. 시각화 도우미에서 해당 노드를 선택하고 **기호 보기(있는 경우)** 를 클릭합니다. 메서드의 본문이 포함된 `Sub Main()` 메서드를 선택합니다. 시각화 도우미의 해당 **SubBlock** 노드에 대해 **기호 보기(있는 경우)** 를 클릭합니다. 속성 그리드는 이 **SubBlock**의 **MethodSymbol** 이름이 `Main`이고 반환 형식이 `Void`임을 보여줍니다.

![메서드 선언의 기호 보기](media/syntax-visualizer/method-symbol.png)

위의 VB 예제는 C#에서 쉽게 복제할 수 있습니다. 별칭에 대해 `Imports C = System.Console` 대신 `using C = System.Console;`을 입력합니다. C#의 앞 단계는 시각화 도우미 창에서 동일한 결과를 생성합니다.

의미 체계 검사 작업은 노드에서만 사용할 수 있습니다. 토큰 또는 퀴즈에는 사용할 수 없습니다. 모든 노드에 검사할 흥미있는 의미 체계 정보가 있는 것은 아닙니다. 노드에 흥미로운 의미 체계 정보가 없을 경우 **\* 기호 보기(있는 경우)** 를 클릭하면 빈 속성 그리드가 표시됩니다.

[의미 체계와 함께 작업](work-with-semantics.md) 개요 문서에서 의미 체계 분석을 수행하기 위한 API에 대해 자세히 읽을 수 있습니다.

## <a name="closing-the-syntax-visualizer"></a>구문 시각화 도우미 닫기

소스 코드 검사에 사용하고 있지 않을 때 시각화 도우미 창을 닫을 수 있습니다. 구문 시각화 도우미는 코드를 탐색하고 소스를 편집 및 변경하면서 해당 디스플레이를 업데이트합니다. 사용하지 않을 때 혼란을 가져올 수 있습니다. 
