---
title: CodeDOM 사용
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- code compilers
- Code Document Object Model
- Code Document Object Model, graphs
- types, CodeDOM
- namespaces [.NET Framework], CodeDOM
- templated code generation
- dynamically representing source code
- source code models
- CodeDOM
- graphing with CodeDOM
- dynamic compilation
- code generators
- CodeDOM, graphs
ms.assetid: 0444ddf3-c3f6-44ed-a999-f710d9c3e0cf
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 56b0b76e8dc137cbb9346f97604c2d53435c1fe6
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71045737"
---
# <a name="using-the-codedom"></a>CodeDOM 사용
CodeDOM은 소스 코드 요소의 다양한 일반적인 형식을 나타내는 형식을 제공합니다. 개체 그래프를 어셈블하는 데 CodeDOM 요소를 사용하는 소스 코드 모델을 빌드하는 프로그램을 디자인할 수 있습니다. 이 개체 그래프는 CodeDOM 코드 생성기를 사용하여 지원되는 프로그래밍 언어에 대한 소스 코드로 렌더링할 수 있습니다. CodeDOM은 소스 코드를 이진 어셈블리로 컴파일하는 데도 사용할 수 있습니다.  
  
 CodeDOM의 몇 가지 일반적인 용도는 다음과 같습니다.  
  
- 템플릿 기반 코드 생성: ASP.NET, XML Web services 클라이언트 프록시, 코드 마법사, 디자이너 또는 기타 코드 내보내기 메커니즘에 대한 코드를 생성합니다.  
  
- 동적 컴파일: 단일 또는 여러 언어로 코드 컴파일을 지원합니다.  
  
## <a name="building-a-codedom-graph"></a>CodeDOM 그래프 빌드  
 <xref:System.CodeDom> 네임스페이스는 언어 구문에 관계없이 소스 코드의 논리 구조를 나타내기 위한 클래스를 제공합니다.  
  
### <a name="the-structure-of-a-codedom-graph"></a>CodeDOM 그래프 구조  
 CodeDOM 그래프 구조는 컨테이너 트리와 비슷합니다. 각 호환 가능한 CodeDOM 그래프의 최상위 또는 루트 컨테이너는 <xref:System.CodeDom.CodeCompileUnit>입니다. 소스 코드 모델의 모든 요소는 그래프의 <xref:System.CodeDom.CodeObject> 속성을 통해 그래프에 연결되어야 합니다.  
  
### <a name="building-a-source-code-model-for-a-sample-hello-world-program"></a>샘플 Hello World 프로그램에 대한 소스 코드 모델 빌드  
 다음 연습에서는 간단한 Hello World 애플리케이션의 코드를 나타내는 CodeDOM 개체 그래프를 빌드하는 방법의 예제를 제공합니다. 이 코드 예제의 전체 소스 코드를 보려면 <xref:System.CodeDom.Compiler.CodeDomProvider?displayProperty=nameWithType> 항목을 참조하세요.  
  
#### <a name="creating-a-compile-unit"></a>컴파일 단위 만들기  
 CodeDOM은 컴파일할 소스 코드를 모델링하는 CodeDOM 개체 그래프를 참조할 수 있는 <xref:System.CodeDom.CodeCompileUnit>라는 개체를 정의합니다. **CodeCompileUnit**에는 특성, 네임스페이스 및 어셈블리에 대한 참조를 저장하기 위한 속성이 있습니다.  
  
 <xref:System.CodeDom.Compiler.CodeDomProvider> 클래스에서 파생되는 CodeDom 공급자에는 **CodeCompileUnit**에서 참조되는 개체 그래프를 처리하는 메서드가 포함됩니다.  
  
 간단한 애플리케이션용 개체 그래프를 만들려면 소스 코드 모델을 어셈블하고 **CodeCompileUnit**에서 해당 모델을 참조해야 합니다.  
  
 이 예제에서 보여 주는 구문을 사용하여 새 컴파일 단위를 만들 수 있습니다.  
  
 [!code-cpp[CodeDomExample#12](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#12)]
 [!code-csharp[CodeDomExample#12](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#12)]
 [!code-vb[CodeDomExample#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#12)]  
  
 <xref:System.CodeDom.CodeSnippetCompileUnit>에는 이미 대상 언어에 있는 소스 코드 섹션이 포함되지만 이 클래스는 다른 언어로 렌더링될 수 없습니다.  
  
#### <a name="defining-a-namespace"></a>네임스페이스 정의  
 네임스페이스를 정의하려면 <xref:System.CodeDom.CodeNamespace>를 만들고 적절한 생성자를 사용하거나 **Name** 속성을 설정하여 이름을 지정합니다.  
  
 [!code-cpp[CodeDomExample#13](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#13)]
 [!code-csharp[CodeDomExample#13](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#13)]
 [!code-vb[CodeDomExample#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#13)]  
  
#### <a name="importing-a-namespace"></a>네임스페이스 가져오기  
 네임스페이스 가져오기 지시문을 네임스페이스에 추가하려면 가져올 네임스페이스를 나타내는 <xref:System.CodeDom.CodeNamespaceImport>를 **CodeNamespace.Imports** 컬렉션에 추가합니다.  
  
 다음 코드는 **System** 네임스페이스의 가져오기를 `samples`라는 **CodeNamespace**의 **Imports** 컬렉션에 추가합니다.  
  
 [!code-cpp[CodeDomExample#14](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#14)]
 [!code-csharp[CodeDomExample#14](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#14)]
 [!code-vb[CodeDomExample#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#14)]  
  
#### <a name="linking-code-elements-into-the-object-graph"></a>개체 그래프에 코드 요소 연결  
 CodeDOM 그래프를 형성하는 모든 코드 요소는 그래프의 루트 개체에 대한 속성에서 직접 참조되는 요소 간 일련의 참조를 통해 트리의 루트 요소인 <xref:System.CodeDom.CodeCompileUnit>에 연결되어야 합니다. 개체를 컨테이너 개체의 속성으로 설정하여 컨테이너 개체에서 참조를 설정합니다.  
  
 다음 문은 `samples` **CodeNamespace**를 루트 **CodeCompileUnit**의 **Namespaces** 컬렉션 속성에 추가합니다.  
  
 [!code-cpp[CodeDomExample#15](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#15)]
 [!code-csharp[CodeDomExample#15](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#15)]
 [!code-vb[CodeDomExample#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#15)]  
  
#### <a name="defining-a-type"></a>형식 정의  
 CodeDOM을 사용하여 클래스, 구조체, 인터페이스 또는 열거형을 선언하려면 새 <xref:System.CodeDom.CodeTypeDeclaration>을 만들고 이름을 지정합니다. 다음 예제에서는 생성자 오버로드를 사용하여 **Name** 속성을 설정하는 방식으로 이 방법을 보여 줍니다.  
  
 [!code-cpp[CodeDomExample#16](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#16)]
 [!code-csharp[CodeDomExample#16](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#16)]
 [!code-vb[CodeDomExample#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#16)]  
  
 형식을 네임스페이스에 추가하려면 네임스페이스에 추가할 형식을 나타내는 <xref:System.CodeDom.CodeTypeDeclaration>을 **CodeNamespace**의 **Types** 컬렉션에 추가합니다.  
  
 다음 예제에서는 `class1` 클래스를 `samples`라는 **CodeNamespace**에 추가하는 방법을 보여 줍니다.  
  
 [!code-cpp[CodeDomExample#17](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#17)]
 [!code-csharp[CodeDomExample#17](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#17)]
 [!code-vb[CodeDomExample#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#17)]  
  
#### <a name="adding-class-members-to-a-class"></a>클래스에 클래스 멤버 추가  
 <xref:System.CodeDom> 네임스페이스는 클래스 멤버를 나타내는 데 사용될 수 있는 다양한 요소를 제공합니다. 각 클래스 멤버를 <xref:System.CodeDom.CodeTypeDeclaration>의 **Members** 컬렉션에 추가할 수 있습니다.  
  
#### <a name="defining-a-code-entry-point-method-for-an-executable"></a>실행 파일에 대한 코드 진입점 메서드 정의  
 실행 가능한 프로그램에 대한 코드를 빌드할 경우 프로그램 실행이 시작되어야 하는 메서드를 나타내기 위한 <xref:System.CodeDom.CodeEntryPointMethod>를 만들어 프로그램의 진입점을 지정해야 합니다.  
  
 다음 예제에서는 "Hello World!"를 인쇄하기 위해 **System.Console.WriteLine**을 호출하는 <xref:System.CodeDom.CodeMethodInvokeExpression>이 포함된 진입점 메서드를 정의하는 방법을 보여 줍니다.  
  
 [!code-cpp[CodeDomExample#18](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#18)]
 [!code-csharp[CodeDomExample#18](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#18)]
 [!code-vb[CodeDomExample#18](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#18)]  
  
 다음 문은 `Start`라는 진입점 메서드를 `class1`의 **Members** 컬렉션에 추가합니다.  
  
 [!code-cpp[CodeDomExample#19](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source2.cpp#19)]
 [!code-csharp[CodeDomExample#19](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source2.cs#19)]
 [!code-vb[CodeDomExample#19](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source2.vb#19)]  
  
 이제 `compileUnit`라는 <xref:System.CodeDom.CodeCompileUnit>에는 간단한 Hello World 프로그램에 대한 CodeDOM 그래프가 포함됩니다. CodeDOM 그래프에서 코드를 생성 및 컴파일하는 방법에 대한 자세한 내용은 [CodeDOM 그래프에서 소스 코드 생성 및 프로그램 컴파일](generating-and-compiling-source-code-from-a-codedom-graph.md)을 참조하세요.  
  
### <a name="more-information-on-building-a-codedom-graph"></a>CodeDOM 그래프 빌드에 대한 자세한 정보  
 CodeDOM은 공용 언어 런타임을 지원하는 프로그래밍 언어에 있는 코드 요소의 다양한 일반적인 형식을 지원합니다. CodeDOM이 모든 가능한 프로그래밍 언어 기능을 나타내는 요소를 제공하도록 디자인된 것은 아닙니다. CodeDOM 요소로 쉽게 나타낼 수 없는 코드는 <xref:System.CodeDom.CodeSnippetExpression>, <xref:System.CodeDom.CodeSnippetStatement>, <xref:System.CodeDom.CodeSnippetTypeMember> 또는 <xref:System.CodeDom.CodeSnippetCompileUnit>로 캡슐화할 수 있습니다. 하지만 코드 조각은 CodeDOM을 통해 자동으로 다른 언어로 변환할 수 없습니다.  
  
 각 CodeDOM 형식에 대한 문서는 <xref:System.CodeDom> 네임스페이스에 대한 참조 문서를 참조하세요.  
  
 코드 요소의 특정 형식을 나타내는 CodeDOM 요소를 찾기 위한 빠른 차트는 [CodeDOM 빠른 참조](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/f1dfsbhc(v=vs.100))를 참조하세요.
