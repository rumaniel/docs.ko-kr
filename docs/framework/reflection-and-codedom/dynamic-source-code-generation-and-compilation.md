---
title: 동적 소스 코드 생성 및 컴파일
ms.date: 03/30/2017
helpviewer_keywords:
- Code Document Object Model
- System.CodeDom namespace
- language-independent source code modeling
- CodeDOM
- multiple languages supported by CodeDOM
- source code in multiple languages
- languages, multiple language support by CodeDOM
ms.assetid: d077a3e8-bd81-4bdf-b6a3-323857ea30fb
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a90b4214e244bc1f9c5f8e71782e604bd6c7b619
ms.sourcegitcommit: 69229651598b427c550223d3c58aba82e47b3f82
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48582595"
---
# <a name="dynamic-source-code-generation-and-compilation"></a>동적 소스 코드 생성 및 컴파일
.NET Framework에는 소스 코드를 내보내는 프로그램 개발자가 렌더링할 코드를 나타내는 단일 모델을 기반으로 런타임에 여러 가지 프로그래밍 언어로 소스 코드를 생성할 수 있는 CodeDOM(코드 문서 개체 모델) 메커니즘이 포함됩니다.  
  
 소스 코드를 나타내기 위해 CodeDOM 요소는 서로 연결되어 일부 소스 코드의 구조를 모델링하는 CodeDOM 그래프라는 데이터 구조를 형성합니다.  
  
 `System.CodeDom` 네임스페이스는 특정 프로그래밍 언어에 관계없이 소스 코드의 논리 구조를 나타낼 수 있는 형식을 정의합니다. `System.CodeDom.Compiler` 네임스페이스는 CodeDOM 그래프에서 소스 코드를 생성하고 지원되는 언어로 소스 코드의 컴파일을 관리하기 위한 형식을 정의합니다. 컴파일러 공급업체나 개발자는 지원되는 언어 집합을 확장할 수 있습니다.  
  
 프로그램이 프로그램 모델에 대한 소스 코드를 여러 언어로 또는 확실하지 않은 대상 언어로 생성해야 하는 경우 언어 독립적 소스 코드 모델링이 중요할 수 있습니다. 예를 들어 CodeDOM이 해당 언어를 지원하는 경우 일부 디자이너는 CodeDOM을 언어 추상 인터페이스로 사용하여 소스 코드를 올바른 프로그래밍 언어로 생성합니다.  
  
 .NET Framework에는 <xref:Microsoft.CSharp.CSharpCodeProvider>, <xref:Microsoft.JScript.JScriptCodeProvider> 및 <xref:Microsoft.VisualBasic.VBCodeProvider>에 대한 코드 생성기 및 코드 컴파일러가 포함됩니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [CodeDOM 사용](../../../docs/framework/reflection-and-codedom/using-the-codedom.md)  
 일반적인 용도를 설명하고 CodeDOM을 사용하여 간단한 개체 그래프를 빌드하는 방법을 보여 줍니다.  
  
 [CodeDOM 그래프에서 소스 코드 생성 및 프로그램 컴파일](../../../docs/framework/reflection-and-codedom/generating-and-compiling-source-code-from-a-codedom-graph.md)  
 소스 코드를 생성하고 `System.CodeDom.Compiler` 네임스페이스에 설명된 클래스를 사용하여 외부 컴파일러를 통해 생성된 코드를 컴파일하는 방법을 설명합니다.  
  
 [방법: CodeDOM을 사용하여 XML 문서 파일 만들기](../../../docs/framework/reflection-and-codedom/how-to-create-an-xml-documentation-file-using-codedom.md)  
 CodeDOM을 사용하여 XML 문서 주석이 포함된 코드를 생성하고 XML 문서 출력을 만들도록 생성된 코드를 컴파일하는 방법을 설명합니다.  
  
 [방법: CodeDOM을 사용하여 클래스 만들기](../../../docs/framework/reflection-and-codedom/how-to-create-a-class-using-codedom.md)  
 CodeDOM을 사용하여 필드, 속성, 메서드, 생성자, 진입점이 포함된 클래스를 생성하는 방법을 설명합니다.  
  
## <a name="reference"></a>참조  
 <xref:System.CodeDom>  
 공용 언어 런타임을 대상으로 하는 프로그래밍 언어로 코드 요소를 나타내는 요소를 정의합니다.  
  
 <xref:System.CodeDom.Compiler>  
 런타임에 코드를 생성 및 컴파일하기 위한 인터페이스를 정의합니다.  
  
## <a name="related-sections"></a>관련 단원  
 [CodeDOM 빠른 참조](https://msdn.microsoft.com/library/c77b8bfd-0a32-4e36-b59a-4f687f32c524)  
 개발자가 소스 코드 요소를 나타내는 CodeDOM 요소를 빠르게 찾을 수 있는 방법을 제공합니다.
