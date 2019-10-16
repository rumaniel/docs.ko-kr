---
title: CodeDOM 그래프에서 소스 코드 생성 및 컴파일
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- code compilers
- CodeDOM, generating source code
- Code Document Object Model, graphs
- templated code generation
- source code, generating
- dynamically representing source code
- generating CodeDOM graphs
- Code Document Object Model, generating source code
- translating language to language
- compiling assemblies
- generating source code in multiple languages
- graphing with CodeDOM
- dynamic compilation
- assemblies [.NET Framework], CodeDOM
- source code generation
- outputting source code by CodeDOM
- code generators
- compiling source code, multiple languages
- CodeDOM, graphs
ms.assetid: 6c864c8e-6dd3-4a65-ace0-36879d9a9c42
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 4f2576aa0d1cf6a4938c8b1c8ee7883251cc192d
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71046073"
---
# <a name="generating-and-compiling-source-code-from-a-codedom-graph"></a>CodeDOM 그래프에서 소스 코드 생성 및 컴파일
<xref:System.CodeDom.Compiler> 네임스페이스는 CodeDOM 개체 그래프에서 소스 코드를 생성하고 지원되는 컴파일러를 통한 컴파일을 관리하기 위한 인터페이스를 제공합니다. 코드 공급자는 CodeDOM 그래프에 따라 특정 프로그래밍 언어로 소스 코드를 생성할 수 있습니다. <xref:System.CodeDom.Compiler.CodeDomProvider>에서 파생되는 클래스는 일반적으로 공급자가 지원하는 언어의 코드를 생성 및 컴파일하기 위한 메서드를 제공할 수 있습니다.  
  
## <a name="using-a-codedom-code-provider-to-generate-source-code"></a>CodeDOM 코드 공급자를 사용하여 소스 코드 생성  
 특정 언어로 소스 코드를 생성하려면 생성할 소스 코드의 구조를 나타내는 CodeDOM 그래프가 필요합니다.  
  
 다음 예제에서는 <xref:Microsoft.CSharp.CSharpCodeProvider> 인스턴스를 만드는 방법을 보여 줍니다.  
  
 [!code-cpp[CodeDomExample#21](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source3.cpp#21)]
 [!code-csharp[CodeDomExample#21](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source3.cs#21)]
 [!code-vb[CodeDomExample#21](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source3.vb#21)]  
  
 코드 생성 그래프는 일반적으로 <xref:System.CodeDom.CodeCompileUnit>에 포함되어 있습니다. CodeDOM 그래프를 포함하는 **CodeCompileUnit**에 대한 코드를 생성하려면 코드 공급자의 <xref:System.CodeDom.Compiler.CodeDomProvider.GenerateCodeFromCompileUnit%2A> 메서드를 호출합니다. 이 메서드에는 소스 코드를 생성하는 데 사용하는 <xref:System.IO.TextWriter>에 대한 매개 변수가 있으므로 먼저 쓸 수 있는 **TextWriter**를 만들어야 하는 경우도 있습니다. 다음 예제에서는 **CodeCompileUnit**에서 코드를 생성하고 생성된 소스 코드를 HelloWorld.cs라는 파일에 쓰는 방법을 보여 줍니다.  
  
 [!code-cpp[CodeDomExample#22](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source3.cpp#22)]
 [!code-csharp[CodeDomExample#22](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source3.cs#22)]
 [!code-vb[CodeDomExample#22](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source3.vb#22)]  
  
## <a name="using-a-codedom-code-provider-to-compile-assemblies"></a>CodeDOM 코드 공급자를 사용하여 어셈블리 컴파일  
 **컴파일 호출**  
  
 CodeDom 공급자를 사용하여 어셈블리를 컴파일하려면 컴파일러가 있는 언어로 컴파일할 소스 코드나 컴파일할 소스 코드를 생성할 수 있는 CodeDOM 그래프가 있어야 합니다.  
  
 CodeDOM 그래프에서 컴파일하는 경우 그래프를 포함하는 <xref:System.CodeDom.CodeCompileUnit>을 코드 공급자의 <xref:System.CodeDom.Compiler.CodeDomProvider.CompileAssemblyFromDom%2A> 메서드에 전달합니다. 컴파일러가 이해할 수 있는 언어의 소스 코드 파일이 있는 경우 소스 코드를 포함하는 파일의 이름을 CodeDom 공급자의 <xref:System.CodeDom.Compiler.CodeDomProvider.CompileAssemblyFromFile%2A> 메서드에 전달합니다. 컴파일러가 이해할 수 있는 언어의 소스 코드를 포함하는 문자열을 CodeDom 공급자의 <xref:System.CodeDom.Compiler.CodeDomProvider.CompileAssemblyFromSource%2A> 메서드에 전달할 수도 있습니다.  
  
 **컴파일 매개 변수 구성**  
  
 CodeDom 공급자의 모든 표준 컴파일 호출 메서드에는 컴파일에 사용할 옵션을 나타내는 <xref:System.CodeDom.Compiler.CompilerParameters> 형식의 매개 변수가 있습니다.  
  
 **CompilerParameters**의 <xref:System.CodeDom.Compiler.CompilerParameters.OutputAssembly%2A> 속성에 출력 어셈블리에 대한 파일 이름을 지정할 수 있습니다. 지정하지 않으면 기본 출력 파일 이름이 사용됩니다.  
  
 기본적으로 새 **CompilerParameters**는 <xref:System.CodeDom.Compiler.CompilerParameters.GenerateExecutable%2A> 속성을 **false**로 설정하여 초기화됩니다. 실행 프로그램을 컴파일하는 경우 **GenerateExecutable** 속성을 **true**로 설정해야 합니다. **GenerateExecutable**이 **false**로 설정된 경우 컴파일러에서 클래스 라이브러리를 생성합니다.  
  
 CodeDOM 그래프에서 실행 파일을 컴파일하는 경우 <xref:System.CodeDom.CodeEntryPointMethod>가 그래프에 정의되어 있어야 합니다. 코드 진입점이 여러 개 있을 경우 사용할 진입점을 정의하는 클래스의 이름으로 **CompilerParameters**의 <xref:System.CodeDom.Compiler.CompilerParameters.MainClass%2A> 속성을 설정해야 할 수도 있습니다.  
  
 생성된 실행 파일에 디버그 정보를 포함하려면 <xref:System.CodeDom.Compiler.CompilerParameters.IncludeDebugInformation%2A> 속성을 **true**로 설정합니다.  
  
 프로젝트가 어셈블리를 참조하는 경우 컴파일을 호출할 때 사용하는 **CompilerParameters**의 <xref:System.CodeDom.Compiler.CompilerParameters.ReferencedAssemblies%2A> 속성으로 <xref:System.Collections.Specialized.StringCollection>의 항목인 어셈블리 이름을 지정해야 합니다.  
  
 <xref:System.CodeDom.Compiler.CompilerParameters.GenerateInMemory%2A> 속성을 **true**로 설정하면 디스크가 아니라 메모리에 기록되는 어셈블리를 컴파일할 수 있습니다. 어셈블리가 메모리에 생성되면 코드에서 <xref:System.CodeDom.Compiler.CompilerResults>의 <xref:System.CodeDom.Compiler.CompilerResults.CompiledAssembly%2A> 속성을 통해 생성된 어셈블리에 대한 참조를 가져올 수 있습니다. 어셈블리가 디스크에 기록되는 경우 **CompilerResults**의 <xref:System.CodeDom.Compiler.CompilerResults.PathToAssembly%2A> 속성에서 생성된 어셈블리의 경로를 가져올 수 있습니다.  
  
 컴파일 프로세스를 호출할 때 사용할 사용자 지정 명령줄 인수 문자열을 지정하려면 <xref:System.CodeDom.Compiler.CompilerParameters.CompilerOptions%2A> 속성에 문자열을 설정합니다.  
  
 컴파일러 프로세스를 호출하는 데 Win32 보안 토큰이 필요한 경우 <xref:System.CodeDom.Compiler.CompilerParameters.UserToken%2A> 속성에 토큰을 지정합니다.  
  
 Win32 리소스 파일을 컴파일된 어셈블리에 연결하려면 <xref:System.CodeDom.Compiler.CompilerParameters.Win32Resource%2A> 속성에서 Win32 리소스 파일의 이름을 지정합니다.  
  
 컴파일을 중단할 경고 수준을 지정하려면 컴파일을 중단할 경고 수준을 나타내는 정수로 <xref:System.CodeDom.Compiler.CompilerParameters.WarningLevel%2A> 속성을 설정합니다. <xref:System.CodeDom.Compiler.CompilerParameters.TreatWarningsAsErrors%2A> 속성을 **true**로 설정하여 경고가 발생할 경우 컴파일을 중단하도록 컴파일러를 구성할 수도 있습니다.  
  
 다음 코드 예제에서는 <xref:System.CodeDom.Compiler.CodeDomProvider> 클래스에서 파생된 CodeDom 공급자를 사용하여 소스 파일을 컴파일하는 방법을 보여 줍니다.  
  
 [!code-cpp[CodeDomExample#23](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeDomExample/CPP/source3.cpp#23)]
 [!code-csharp[CodeDomExample#23](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomExample/CS/source3.cs#23)]
 [!code-vb[CodeDomExample#23](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomExample/VB/source3.vb#23)]  
  
## <a name="languages-with-initial-support"></a>초기 지원 상태의 언어  
 .NET Framework는 다음 언어에 대한 코드 컴파일러 및 코드 생성기를 제공합니다. C#, Visual Basic, C++ 및 JScript. 언어별 코드 생성기 및 코드 컴파일러를 구현하면 CodeDOM 지원을 다른 언어로 확장할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.CodeDom>
- <xref:System.CodeDom.Compiler>
- [동적 소스 코드 생성 및 컴파일](dynamic-source-code-generation-and-compilation.md)
- [CodeDOM 빠른 참조](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/f1dfsbhc(v=vs.100))
