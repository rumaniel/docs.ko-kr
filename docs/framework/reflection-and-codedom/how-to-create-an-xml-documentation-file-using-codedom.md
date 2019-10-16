---
title: '방법: CodeDOM을 사용하여 XML 문서 파일 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- CodeDOM, generating XML documentation
- XML documentation, creating using CodeDOM
- Code Document Object Model, generating XML documentation
ms.assetid: e3b80484-36b9-41dd-9d21-a2f9a36381dc
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 283fc91762bc4065bd9bd09efaa2bc0061451ef9
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69962735"
---
# <a name="how-to-create-an-xml-documentation-file-using-codedom"></a>방법: CodeDOM을 사용하여 XML 문서 파일 만들기
CodeDOM을 사용하여 XML 문서를 생성하는 코드를 만들 수 있습니다. 이 프로세스에서는 XML 문서 주석이 포함된 CodeDOM 그래프를 생성하고, 코드를 생성하고, XML 문서 출력을 만드는 컴파일러 옵션을 사용하여 생성된 코드를 컴파일해야 합니다.  
  
### <a name="to-create-a-codedom-graph-that-contains-xml-documentation-comments"></a>XML 문서 주석을 포함하는 CodeDOM 그래프를 만들려면  
  
1. 애플리케이션 예제에 대한 CodeDOM 그래프를 포함하는 <xref:System.CodeDom.CodeCompileUnit>을 만듭니다.  
  
2. `docComment` 매개 변수를 `true`로 설정해서 <xref:System.CodeDom.CodeCommentStatement.%23ctor%2A> 생성자를 사용하여 XML 문서 주석 요소 및 텍스트를 만듭니다.  
  
     [!code-csharp[CodeDomHelloWorldSample#4](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomHelloWorldSample/cs/program.cs#4)]
     [!code-vb[CodeDomHelloWorldSample#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomHelloWorldSample/vb/program.vb#4)]  
  
### <a name="to-generate-the-code-from-the-codecompileunit"></a>CodeCompileUnit에서 코드를 생성하려면  
  
1. <xref:System.CodeDom.Compiler.CodeDomProvider.GenerateCodeFromCompileUnit%2A> 메서드를 사용하여 코드를 생성하고 컴파일할 소스 파일을 만듭니다.  
  
     [!code-csharp[CodeDomHelloWorldSample#5](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomHelloWorldSample/cs/program.cs#5)]
     [!code-vb[CodeDomHelloWorldSample#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomHelloWorldSample/vb/program.vb#5)]  
  
### <a name="to-compile-the-code-and-generate-the-documentation-file"></a>코드를 컴파일하고 문서 파일을 생성하려면  
  
1. <xref:System.CodeDom.Compiler.CompilerParameters> 개체의 <xref:System.CodeDom.Compiler.CompilerParameters.CompilerOptions%2A> 속성에 **/doc** 컴파일러 옵션을 추가하고, 코드를 컴파일할 때 <xref:System.CodeDom.Compiler.CodeDomProvider.CompileAssemblyFromFile%2A> 메서드에 이 개체를 전달하여 XML 문서 파일을 만듭니다.  
  
     [!code-csharp[CodeDomHelloWorldSample#6](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomHelloWorldSample/cs/program.cs#6)]
     [!code-vb[CodeDomHelloWorldSample#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomHelloWorldSample/vb/program.vb#6)]  
  
## <a name="example"></a>예  
 다음 코드 예제에서는 문서 주석이 포함된 CodeDOM 그래프를 만들고, 그래프에서 코드 파일을 생성한 다음 파일을 컴파일하고 연결된 XML 문서 파일을 만듭니다.  
  
 [!code-csharp[CodeDomHelloWorldSample#1](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeDomHelloWorldSample/cs/program.cs#1)]
 [!code-vb[CodeDomHelloWorldSample#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeDomHelloWorldSample/vb/program.vb#1)]  
  
 코드 예제에서는 HelloWorldDoc.xml 파일에 다음 XML 문서를 만듭니다.  
  
```xml  
<?xml version="1.0" ?>   
<doc>  
  <assembly>  
    <name>HelloWorld</name>   
  </assembly>  
  <members>  
    <member name="T:Samples.Class1">  
      <summary>  
        Create a Hello World application.   
        <seealso cref="M:Samples.Class1.Main" />   
      </summary>  
    </member>  
    <member name="M:Samples.Class1.Main">  
      <summary>  
        Main method for HelloWorld application.   
        <para>Add a new paragraph to the description.</para>   
      </summary>  
    </member>  
  </members>  
</doc>  
```  
  
## <a name="compiling-the-code"></a>코드 컴파일  
  
- 이 코드 예제를 성공적으로 실행하려면 `FullTrust` 권한이 설정되어 있어야 합니다.  
  
## <a name="see-also"></a>참고 항목

- [코드를 XML로 문서화](../../visual-basic/programming-guide/program-structure/documenting-your-code-with-xml.md)
- [XML 문서 주석](../../csharp/programming-guide/xmldoc/index.md)
- [XML 문서](/cpp/ide/xml-documentation-visual-cpp)
