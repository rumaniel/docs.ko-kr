---
title: XPath 네임스페이스 탐색
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 06cc7abb-7416-415c-9dd6-67751b8cabd5
author: mairaw
ms.author: mairaw
ms.openlocfilehash: f6facc047d87c503313015eff4e869861cd6b301
ms.sourcegitcommit: 7bfe1682d9368cf88d43e895d1e80ba2d88c3a99
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71957008"
---
# <a name="xpath-namespace-navigation"></a>XPath 네임스페이스 탐색
XML 문서가 있는 XPath 쿼리를 사용하려면 네임스페이스에 포함된 XML 네임스페이스 및 요소를 올바르게 지정해야 합니다. 네임스페이스를 사용하면 이름이 둘 이상의 컨텍스트에 사용되는 경우 발생할 수 있는 모호성을 방지할 수 있습니다. 예를 들어 이름 `ID`는 XML 문서의 여러 다른 요소와 연결된 둘 이상의 ID를 참조할 수 있습니다. 네임스페이스 구문은 URI, 이름 및 XML 문서의 요소를 구분하는 접두사를 지정합니다.  
  
 이 항목의 예제는 <xref:System.Xml.XPath.XPathNavigator>로 XML 문서를 탐색하는 데 접두사를 사용하는 경우를 설명합니다. 네임스페이스 및 구문에 대한 자세한 내용은 [XML 파일: XML 네임스페이스 이해](https://docs.microsoft.com/previous-versions/dotnet/articles/bb986013(v=msdn.10))를 참조하세요.  
  
## <a name="namespace-declarations"></a>네임스페이스 선언  
 네임스페이스 선언은 <xref:System.Xml.XPath.XPathNavigator> 인스턴스를 사용하는 경우 XML 문서의 요소를 구분하고 지정할 수 있게 해 줍니다. 네임스페이스 접두사는 네임스페이스 지정에 사용되는 간단한 구문을 제공합니다.  
  
 접두사는 다음 양식으로 정의됩니다. `<e:Envelope xmlns:e=http://schemas.xmlsoap.org/soap/envelope/>.` 이 구문에서 "`e`" 접두사는 네임스페이스의 정식 URI에 대한 약어입니다. `Body` 구문을 사용하여 `Envelope` 요소를 `e:Body` 네임스페이스의 멤버로 식별할 수 있습니다.  
  
 다음 XML 문서는 다음 단원의 탐색 예제에서 `response.xml`로 참조됩니다.  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>  
<e:Envelope xmlns:e="http://schemas.xmlsoap.org/soap/envelope/">  
  <e:Body>  
    <s:Search xmlns:s="http://schemas.microsoft.com/v1/Search">  
      <r:request xmlns:r="http://schemas.microsoft.com/v1/Search/metadata"   
                 xmlns:i="http://www.w3.org/2001/XMLSchema-instance">  
      </r:request>  
    </s:Search>  
  </e:Body>  
</e:Envelope>  
```  
  
## <a name="navigation-by-namespace-prefix"></a>네임스페이스 접두사로 탐색  
 이 단원의 코드는 <xref:System.Xml.XPath.XPathNavigator> 및 <xref:System.Xml.XmlNamespaceManager> 개체를 사용하여 이전 단원의 XML 문서에서 `Search` 요소를 선택합니다. `xpath` 쿼리에는 경로의 각 요소에 대한 네임스페이스 접두사가 포함됩니다. 각 요소를 포함하는 네임스페이스의 ID를 정확히 지정하면 `Search` 메서드가 <xref:System.Xml.XPath.XPathNavigator.SelectSingleNode%2A> 요소에 대한 탐색을 올바르게 수행할 수 있습니다.  
  
```csharp  
using (XmlReader reader = XmlReader.Create("response.xml"))  
{  
    XPathDocument doc = new XPathDocument(reader);  
    XPathNavigator nav = doc.CreateNavigator();
  
    XmlNamespaceManager nsmgr = new XmlNamespaceManager(nav.NameTable);  
    nsmgr.AddNamespace("e", @"http://schemas.xmlsoap.org/soap/envelope/");  
    nsmgr.AddNamespace("s", @"http://schemas.microsoft.com/v1/Search");  
    nsmgr.AddNamespace("r", @"http://schemas.microsoft.com/v1/Search/metadata");  
    nsmgr.AddNamespace("i", @"http://www.w3.org/2001/XMLSchema-instance");  
  
    string xpath = "/e:Envelope/e:Body/s:Search";  
  
    XPathNavigator element = nav.SelectSingleNode(xpath, nsmgr);  
  
    Console.WriteLine("Element Prefix:" + element.Prefix +   
    " Local name:" + element.LocalName);  
    Console.WriteLine("Namespace URI: " + element.NamespaceURI);  
}  
```  
  
 정규화된 네임스페이스 및 이름의 정확한 사용은 단순히 편리한 것 이상의 이점이 있습니다. 이전 예제의 문서 정의 및 코드를 사용한 작은 실험을 통해 정규화된 요소 이름이 없는 탐색에서 예외를 throw한다는 사실을 확인한 바 있습니다. 예를 들어 요소 정의: `<Search xmlns="http://schemas.microsoft.com/v1/Search">` 및 쿼리: `xpath = "/s:Envelope/s:Body/Search";` 요소에 대한 네임스페이스 접두사가 없는 문자열 `Search`는 `null` 요소 대신 `Search`을 반환합니다.  
  
## <a name="see-also"></a>참조

- [XPathNavigator를 사용하여 XML 데이터 액세스](../../../../docs/standard/data/xml/accessing-xml-data-using-xpathnavigator.md)
- [XPathNavigator를 사용하여 XML 데이터 선택, 평가 및 일치시키기](../../../../docs/standard/data/xml/selecting-evaluating-and-matching-xml-data-using-xpathnavigator.md)
