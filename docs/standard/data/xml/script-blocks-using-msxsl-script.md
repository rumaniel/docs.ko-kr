---
title: msxsl:script를 사용하는 스크립트 블록
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: fde6f43f-c594-486f-abcb-2211197fae20
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 1488fb6b7671acd86286bcac6fbfce8bee9429ad
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69939584"
---
# <a name="script-blocks-using-msxslscript"></a>msxsl:script를 사용하는 스크립트 블록
<xref:System.Xml.Xsl.XslCompiledTransform> 클래스는 `msxsl:script` 요소를 사용하여 포함 스크립트를 지원합니다. 스타일시트가 로드될 때 정의된 모든 함수는 CodeDOM(코드 문서 개체 모델)에 의해 MSIL(Microsoft Intermediate Language)로 컴파일되며 런타임 동안 실행됩니다. 포함된 스크립트 블록에서 생성된 어셈블리는 스타일시트에 대해 생성된 어셈블리와는 다릅니다.  
  
## <a name="enable-xslt-script"></a>XSLT 스크립트 사용  
 포함된 스크립트 지원은 <xref:System.Xml.Xsl.XslCompiledTransform> 클래스에서 선택적 XSLT 설정입니다. 스크립트 지원은 기본적으로 사용되지 않습니다. 스크립트 지원을 사용하려면 <xref:System.Xml.Xsl.XsltSettings> 속성을 <xref:System.Xml.Xsl.XsltSettings.EnableScript%2A>로 설정하여 `true` 개체를 만들고 이 개체를 <xref:System.Xml.Xsl.XslCompiledTransform.Load%2A> 메서드에 전달합니다.  
  
> [!NOTE]
> XSLT 스크립트는 스크립트 지원이 필요하거나 완전히 신뢰할 수 있는 환경에서 작업하는 경우에만 활성화해야 합니다.  
  
## <a name="msxslscript-element-definition"></a>msxsl:script 요소 정의  
 `msxsl:script` 요소는 XSLT 1.0 권장 사항에 대한 Microsoft 확장으로, 다음 정의를 가집니다.  
  
```xml  
<msxsl:script language = "language-name" implements-prefix = "prefix of user namespace"> </msxsl:script>  
```  
  
 `msxsl` 접두사는 `urn:schemas-microsoft-com:xslt` 네임스페이스 URI에 바인딩됩니다. 스타일시트는 `xmlns:msxsl=urn:schemas-microsoft-com:xslt` 네임스페이스 선언을 포함해야 합니다.  
  
 `language` 특성은 선택 사항입니다. 해당 값은 포함된 코드 블록의 코드 언어입니다. 이 언어는 <xref:System.CodeDom.Compiler.CodeDomProvider.CreateProvider%2A?displayProperty=nameWithType> 메서드를 사용하여 적합한 CodeDOM 컴파일러에 매핑됩니다. <xref:System.Xml.Xsl.XslCompiledTransform> 클래스는 모든 Microsoft .NET 언어를 지원할 수 있습니다. 이때 적합한 공급자가 컴퓨터에 설치되어 있으며 machine.config 파일의 system.codedom 섹션에 등록되어 있다고 가정합니다. `language` 특성을 지정하지 않을 경우 언어 기본값은 JScript입니다. 언어 이름은 대/소문자를 구분하지 않으므로 'JavaScript'와 'javascript'는 같습니다.  
  
 `implements-prefix` 특성은 필수 항목입니다. 이 특성은 네임스페이스를 선언하고 스크립트 블록에 연결하는 데 사용됩니다. 이 특성 값은 네임스페이스를 나타내는 접두사입니다. 이 접두사는 스타일시트에서 정의할 수 있습니다.  
  
> [!NOTE]
> `msxsl:script` 요소를 사용하는 경우에는 언어에 관계없이 스크립트를 CDATA 섹션에 배치하는 것이 좋습니다. 스크립트에는 지정된 언어에 대한 연산자, 식별자 또는 구분자가 포함될 수 있으므로 스크립트를 CDATA 섹션에 포함하지 않으면 XML로 잘못 해석될 수 있습니다. 다음 XML에서는 코드를 배치할 수 있는 CDATA 섹션 템플릿을 보여 줍니다.  
  
```xml  
<msxsl:script implements-prefix='your-prefix' language='CSharp'>  
<![CDATA[  
// Code block.  
]]>  
</msxsl:script>  
```  
  
## <a name="script-functions"></a>스크립트 함수  
 함수는 `msxsl:script` 요소 내에서 선언할 수 있습니다. 함수를 선언하면 해당 함수는 스크립트 블록 내에 포함됩니다. 스타일시트에는 여러 스크립트 블록이 포함될 수 있으며 각 블록은 서로 독립적으로 작동합니다. 즉, 스크립트 블록 내부에서 실행할 경우 같은 네임스페이스와 같은 스크립트 언어를 사용하도록 선언된 경우에만 다른 스크립트 블록에 정의된 함수를 호출할 수 있습니다. 각 스크립트 블록에서는 서로 다른 언어를 사용할 수 있고, 블록은 해당 언어 파서의 문법 규칙에 따라 구문 분석되기 때문에 사용하는 언어의 올바른 구문을 사용해야 합니다. 예를 들어, Microsoft C# 스크립트 블록에서는 C# 주석 구문을 사용합니다.  
  
 함수에 제공된 인수 및 반환 값에는 어떤 형식도 사용할 수 있습니다. W3C XPath 형식은 CLR(공용 언어 런타임) 형식의 하위 집합이므로 XPath 형식으로 간주되지 않는 형식에서 형식 변환이 발생합니다. 다음 표에서는 해당 W3C 형식 및 CLR 형식을 보여 줍니다.  
  
|W3C 형식|CLR 형식|  
|--------------|--------------|  
|`String`|<xref:System.String>|  
|`Boolean`|<xref:System.Boolean>|  
|`Number`|<xref:System.Double>|  
|`Result Tree Fragment`|<xref:System.Xml.XPath.XPathNavigator>|  
|`Node Set`|<xref:System.Xml.XPath.XPathNodeIterator>|  
  
 CLR 숫자 형식은 <xref:System.Double>로 변환됩니다. <xref:System.DateTime> 형식은 <xref:System.String>으로 변환되고, <xref:System.Xml.XPath.IXPathNavigable> 형식은 <xref:System.Xml.XPath.XPathNavigator>로 변환됩니다. **XPathNavigator[]** 는 <xref:System.Xml.XPath.XPathNodeIterator>로 변환됩니다.  
  
 다른 모든 형식은 오류를 throw합니다.  
  
### <a name="importing-namespaces-and-assemblies"></a>네임스페이스 및 어셈블리 가져오기  
 <xref:System.Xml.Xsl.XslCompiledTransform> 클래스는 `msxsl:script` 요소에서 기본적으로 지원하는 어셈블리 및 네임스페이스 집합을 미리 정의합니다. 그러나 `msxsl:script` 블록에 어셈블리 및 네임스페이스를 가져오면 미리 정의된 목록에 없는 네임스페이스에 속한 클래스 및 멤버를 사용할 수 있습니다.  
  
#### <a name="assemblies"></a>어셈블리  
 기본적으로 다음 두 어셈블리가 참조됩니다.  
  
- System.dll  
  
- System.Xml.dll  
  
- Microsoft.VisualBasic.dll(스크립트 언어가 VB인 경우)  
  
 `msxsl:assembly` 요소를 사용하여 추가 어셈블리를 가져올 수 있습니다. 여기에는 스타일시트를 컴파일할 때 어셈블리가 포함됩니다. `msxsl:assembly` 요소에는 다음 정의가 있습니다.  
  
```xml  
<msxsl:script>  
  <msxsl:assembly name="system.assemblyName" />  
  <msxsl:assembly href="path-name" />  
    <![CDATA[  
    // User code  
    ]]>  
</msxsl:script>  
```  
  
 `name` 특성에는 어셈블리 이름이 포함되며 `href` 특성에는 어셈블리 경로가 포함됩니다. 어셈블리 이름은 "System.Data, Version=2.0.3600.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" 등의 전체 이름이거나 "System.Web"과 같은 약식 이름일 수 있습니다.  
  
#### <a name="namespaces"></a>네임스페이스  
 기본적으로 다음 네임스페이스가 포함됩니다.  
  
- 시스템  
  
- System.Collection  
  
- System.Text  
  
- System.Text.RegularExpressions  
  
- System.Xml  
  
- System.Xml.Xsl  
  
- System.Xml.XPath  
  
- Microsoft.VisualBasic(스크립트 언어가 VB인 경우)  
  
 `namespace` 특성을 사용하여 추가 네임스페이스에 대한 지원을 추가할 수 있습니다. 특성 값은 네임스페이스 이름입니다.  
  
```xml  
<msxsl:script>  
  <msxsl:using namespace="system.namespaceName" />  
    <![CDATA[  
    // User code  
    ]]>  
</msxsl:script>  
```  
  
## <a name="example"></a>예  
 다음 예제에서는 포함 스크립트를 사용하여 주어진 반지름으로 원의 원주를 계산합니다.  
  
 [!code-csharp[XSLT_Script#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XSLT_Script/CS/xslt_script.cs#1)]
 [!code-vb[XSLT_Script#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XSLT_Script/VB/xslt_script.vb#1)]  
  
#### <a name="numberxml"></a>number.xml  
 [!code-xml[XSLT_Script#2](../../../../samples/snippets/xml/VS_Snippets_Data/XSLT_Script/XML/number.xml#2)]  
  
#### <a name="calcxsl"></a>calc.xsl  
 [!code-xml[XSLT_Script#3](../../../../samples/snippets/xml/VS_Snippets_Data/XSLT_Script/XML/calc.xsl#3)]  
  
### <a name="output"></a>출력  
  
```xml  
<circles xmlns:msxsl="urn:schemas-microsoft-com:xslt" xmlns:user="urn:my-scripts">  
  <circle>  
    <radius>12</radius>  
    <circumference>75.36</circumference>  
  </circle>  
  <circle>  
    <radius>37.5</radius>  
    <circumference>235.5</circumference>  
  </circle>  
</circles>  
```  
  
## <a name="see-also"></a>참고 항목

- [XSLT 변환](../../../../docs/standard/data/xml/xslt-transformations.md)
- [동적 소스 코드 생성 및 컴파일](../../../../docs/framework/reflection-and-codedom/dynamic-source-code-generation-and-compilation.md)
