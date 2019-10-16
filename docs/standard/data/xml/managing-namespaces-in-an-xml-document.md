---
title: XML 문서의 네임스페이스 관리
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 682643fc-b848-4e42-8c0d-50deeaeb5f2a
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 83ea398f18ab02840ea811c74a6053dba11a3baa
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66490893"
---
# <a name="managing-namespaces-in-an-xml-document"></a>XML 문서의 네임스페이스 관리
XML 네임스페이스는 XML 문서의 요소 및 특성 이름을 사용자 지정 및 미리 정의된 URI와 연결합니다. 이러한 연결을 만들려면 네임스페이스 URI의 접두사를 정의하고 해당 접두사를 사용하여 XML 데이터의 요소 및 특성 이름을 한정합니다. 네임스페이스는 요소 및 특성 이름이 충돌하는 것을 막고 동일한 이름의 요소 및 특성이 처리 및 확인되도록 하는 역할을 합니다.  
  
<a name="declare"></a>   
## <a name="declaring-namespaces"></a>네임스페이스 선언  
 요소의 네임스페이스를 선언하려면 `xmlns:` 특성을 사용합니다.  
  
 `xmlns:<name>=<"uri">`  
  
 `<name>`이 네임스페이스 접두사이고 `<"uri">`는 네임스페이스를 식별하는 URI입니다. 접두사를 선언한 후에는 접두사를 사용하여 XML 문서의 요소 및 특성을 한정하고 네임스페이스 URI와 연결할 수 있습니다. 네임스페이스 접두사는 문서 전체에서 사용되므로 길이가 짧아야 합니다.  
  
 이 예제에서는 다음 두 개의 `BOOK` 요소를 정의합니다. 첫 번째 요소는 접두사 `mybook`에 의해 한정되고 두 번째 요소는 접두사 `bb`에 의해 한정됩니다. 각 접두사는 다른 네임스페이스 URI와 연관되어 있습니다.  
  
```xml  
<mybook:BOOK xmlns:mybook="http://www.contoso.com/books.dtd">  
<bb:BOOK xmlns:bb="urn:blueyonderairlines">  
```  
  
 요소가 특정 네임스페이스의 일부임을 나타내기 위해 네임스페이스 접두사를 추가합니다. 예를 들어 `Author` 요소가 `mybook` 네임스페이스에 속하는 경우에는 `<mybook:Author>`로 선언됩니다.  
  
<a name="scope"></a>   
## <a name="declaration-scope"></a>선언 범위  
 네임스페이스는 선언 지점부터 선언된 요소의 끝까지 유효합니다. 이 예에서 `BOOK` 요소에서 정의된 네임스페이스는 `BOOK` 요소와 같은 `Publisher` 요소 외부의 요소에는 적용되지 않습니다.  
  
```xml  
<Author>Joe Smith</Author>  
<BOOK xmlns:book="http://www.contoso.com">  
    <title>My Wonderful Day</title>  
      <price>$3.95</price>  
</BOOK>  
<Publisher>  
    <Name>MSPress</Name>  
</Publisher>  
```  
  
 네임스페이스는 사용되기 전에 선언되어야 하지만 XML 문서의 맨 처음에 나타나야 하는 것은 아닙니다.  
  
 XML 문서에서 여러 네임스페이스를 사용하는 경우 네임스페이스 하나를 기본 네임스페이스로 정의하여 더 간결한 문서를 만들 수 있습니다. 기본 네임스페이스는 루트 요소에서 정의되고 문서에서 정규화되지 않은 모든 요소에 적용됩니다. 기본 네임스페이스는 요소에만 적용되고 특성에는 적용되지 않습니다.  
  
 기본 네임스페이스를 사용하려면 요소의 선언에서 접두사와 콜론을 생략합니다.  
  
```xml  
<BOOK xmlns="http://www.contoso.com/books.dtd">  
```  
  
## <a name="managing-namespaces"></a>네임스페이스 관리  
 <xref:System.Xml.XmlNamespaceManager> 클래스는 네임스페이스 URI 및 해당 접두사의 컬렉션을 저장하고 이 컬렉션에서 네임스페이스를 조회, 추가 및 제거할 수 있도록 합니다. 특정 컨텍스트에서 향상된 XML 처리 성능을 위해 이 클래스가 필요합니다. 예를 들어, XPath 지원을 위해 <xref:System.Xml.Xsl.XsltContext> 클래스에서 <xref:System.Xml.XmlNamespaceManager>를 사용합니다.  
  
 네임스페이스 관리자는 네임스페이스에 대한 유효성 검사를 수행하지 않지만 접두사 및 네임스페이스가 이미 확인되었고 [W3C 네임스페이스](https://www.w3.org/TR/REC-xml-names/) 사양을 따르는 것으로 간주합니다.  
  
> [!NOTE]
> [C#](../../../csharp/programming-guide/concepts/linq/linq-to-xml-overview.md) 및 [Visual Basic](../../../visual-basic/programming-guide/concepts/linq/linq-to-xml.md)의 LINQ TO XML은 <xref:System.Xml.XmlNamespaceManager>를 사용하여 네임스페이스를 관리하지 않습니다. LINQ to XML을 사용할 때 네임스페이스를 관리하는 방법에 대한 내용은 LINQ 설명서에서 [XML 네임스페이스 작업](../../../csharp/programming-guide/concepts/linq/working-with-xml-namespaces.md) 및 [XML 네임스페이스 작업(Visual Basic)](../../../visual-basic/programming-guide/concepts/linq/working-with-xml-namespaces.md)을 참조하세요.  
  
 다음은 <xref:System.Xml.XmlNamespaceManager> 클래스로 수행할 수 있는 관리 및 조회 작업입니다. 자세한 내용 및 예제는 각 메서드 또는 속성의 참조 페이지에 대한 링크를 참조하세요.  
  
|대상|기능|  
|--------|---------|  
|네임스페이스 추가|<xref:System.Xml.XmlNamespaceManager.AddNamespace%2A> 메서드|  
|네임스페이스 제거|<xref:System.Xml.XmlNamespaceManager.RemoveNamespace%2A> 메서드|  
|기본 네임스페이스에 대한 URI 찾기|<xref:System.Xml.XmlNamespaceManager.DefaultNamespace%2A> 속성|  
|네임스페이스 접두사에 대한 URI 찾기|<xref:System.Xml.XmlNamespaceManager.LookupNamespace%2A> 메서드|  
|네임스페이스 URI에 대한 접두사 찾기|<xref:System.Xml.XmlNamespaceManager.LookupPrefix%2A> 메서드|  
|현재 노드의 네임스페이스 목록 가져오기|<xref:System.Xml.XmlNamespaceManager.GetNamespacesInScope%2A> 메서드|  
|네임스페이스 범위 지정|<xref:System.Xml.XmlNamespaceManager.PushScope%2A> 및 <xref:System.Xml.XmlNamespaceManager.PopScope%2A> 메서드|  
|접두사가 현재 범위에서 정의되어 있는지 확인|<xref:System.Xml.XmlNamespaceManager.HasNamespace%2A> 메서드|  
|접두사와 URI를 찾는 데 사용된 이름 테이블 가져오기|<xref:System.Xml.XmlNamespaceManager.NameTable%2A> 속성|  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Xml.XmlNamespaceManager>
- [XML 문서 및 데이터](../../../../docs/standard/data/xml/index.md)
