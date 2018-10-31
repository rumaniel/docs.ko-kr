---
title: LINQ to XML 보안(C#)
ms.date: 07/20/2015
ms.assetid: ef2c0dc9-ecf9-4c17-b24e-144184ab725f
ms.openlocfilehash: 0c4ee8df85d6e5c6f84947dcaaeb6875bbd687de
ms.sourcegitcommit: 69229651598b427c550223d3c58aba82e47b3f82
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48584366"
---
# <a name="linq-to-xml-security-c"></a>LINQ to XML 보안(C#)
이 항목에서는 LINQ to XML과 관련된 보안 문제에 대해 설명합니다. 또한 보안 노출을 경감하는 몇 가지 지침을 제공합니다.  
  
## <a name="linq-to-xml-security-overview"></a>LINQ to XML 보안 개요  
 LINQ to XML은 보안 요구 사항이 엄격한 서버측 응용 프로그램보다 간편하게 프로그래밍하는 데 중점을 두어 디자인되었습니다. 대부분의 XML 시나리오는 서버에 업로드된 신뢰할 수 없는 XML 문서의 처리가 아니라 신뢰할 수 있는 XML 문서의 처리로 이루어져 있습니다. LINQ to XML은 이러한 시나리오에 맞게 최적화되었습니다.  
  
 알 수 없는 소스에서 신뢰할 수 없는 데이터를 처리해야 하는 경우 알려진 XML DoS(서비스 거부) 공격을 필터링하도록 구성된 <xref:System.Xml.XmlReader> 클래스의 인스턴스를 사용하는 것이 좋습니다.  
  
 서비스 거부 공격을 완화하도록 <xref:System.Xml.XmlReader>를 구성한 경우 해당 판독기를 사용하여 LINQ to XML 트리를 채우고 LINQ to XML의 프로그래머 생산성 향상 기능에서 혜택을 얻을 수 있습니다. 많은 완화 기법에는 보안 문제를 완화하도록 구성된 판독기를 만들고 구성된 판독기를 통해 XML 트리를 인스턴스화하는 작업이 포함됩니다.  
  
 XML은 문서의 크기, 깊이, 요소 이름 크기 등이 제한되어 있지 않기 때문에 서비스 거부 공격에 기본적으로 취약합니다. XML 처리에 사용하는 구성 요소에 관계없이 과도한 리소스를 사용하는 경우 응용 프로그램 도메인을 재활용할 준비가 항상 되어 있어야 합니다.  
  
## <a name="mitigation-of-xml-xsd-xpath-and-xslt-attacks"></a>XML, XSD, XPath 및 XSLT 공격의 완화  
 LINQ to XML은 <xref:System.Xml.XmlReader> 및 <xref:System.Xml.XmlWriter>를 기반으로 빌드되었습니다. LINQ to XML에서는 <xref:System.Xml.Schema?displayProperty=nameWithType> 및 <xref:System.Xml.XPath?displayProperty=nameWithType> 네임스페이스의 확장 메서드를 통해 XSD와 XPath를 지원합니다. LINQ to XML과 함께 <xref:System.Xml.XmlReader>, <xref:System.Xml.XPath.XPathNavigator> 및 <xref:System.Xml.XmlWriter> 클래스를 사용하는 경우 XSLT를 호출하여 XML 트리를 변환할 수 있습니다.  
  
 보안 수준이 낮은 운영 환경에서는 XML 및 <xref:System.Xml?displayProperty=nameWithType>, <xref:System.Xml.Schema?displayProperty=nameWithType>, <xref:System.Xml.XPath?displayProperty=nameWithType> 및 <xref:System.Xml.Xsl?displayProperty=nameWithType>의 클래스 사용과 관련된 많은 보안 문제가 있습니다. 이러한 문제는 다음과 같지만 다음 문제로만 제한되지는 않습니다.  
  
-   XSD, XPath 및 XSLT는 많은 시간이나 메모리를 사용하는 작업을 지정할 수 있는 문자열 기반 언어입니다. 문자열이 악성이 아닌지 확인하거나 이러한 문자열을 확인할 때 시스템 리소스를 과도하게 사용하게 될 가능성을 모니터링하고 완화하는 것은 신뢰할 수 없는 소스에서 XSD, XPath 또는 XSLT 문자열을 가져오는 응용 프로그램 프로그래머의 책임입니다.  
  
-   인라인 스키마를 비롯한 XSD 스키마는 기본적으로 서비스 거부 공격에 취약하므로 신뢰할 수 없는 소스에서 스키마를 받아들이지 않아야 합니다.  
  
-   XSD와 XSLT에는 다른 파일에 대한 참조가 포함될 수 있으며 이러한 참조로 인해 영역 간 공격과 도메인 간 공격이 발생할 수 있습니다.  
  
-   DTD의 외부 엔터티로 인해 영역 간 공격과 도메인 간 공격이 발생할 수 있습니다.  
  
-   DTD는 서비스 거부 공격에 취약합니다.  
  
-   매우 깊은 XML 문서는 서비스 거부 문제를 일으킬 수 있으므로 XML 문서의 깊이를 제한할 수 있습니다.  
  
-   신뢰할 수 없는 어셈블리에서 <xref:System.Xml.NameTable>, <xref:System.Xml.XmlNamespaceManager> 및 <xref:System.Xml.XmlResolver> 개체와 같은 지원 구성 요소를 받아들이지 않습니다.  
  
-   큰 문서 공격을 완화하기 위해 데이터를 청크로 읽습니다.  
  
-   XSLT 스타일시트의 스크립트 블록은 많은 공격에 노출될 수 있습니다.  
  
-   동적 XPath 식을 생성하기 전에 신중하게 유효성을 검사합니다.  
  
## <a name="linq-to-xml-security-issues"></a>LINQ to XML 보안 문제  
 이 항목의 보안 문제는 특정 순서로 제공되지 않습니다. 모든 문제는 중요하며 적절하게 처리되어야 합니다.  
  
 권한 상승 공격이 성공하면 악의적인 어셈블리가 환경을 더 많이 제어할 수 있습니다. 또한 데이터 공개, 서비스 거부 등이 발생할 수 있습니다.  
  
 응용 프로그램에서는 데이터를 볼 권한이 없는 사용자에게 데이터를 공개해서는 안 됩니다.  
  
 서비스 거부 공격이 발생하면 XML 파서나 LINQ to XML에서 메모리나 CPU 시간을 지나치게 많이 사용합니다. 서비스 거부 공격은 권한 상승 공격이나 데이터 공개 공격보다 심각하지 않은 것으로 간주됩니다. 그러나 서버에서 신뢰할 수 없는 소스의 XML 문서를 처리해야 하는 경우에는 서비스 거부 공격이 중요합니다.  
  
### <a name="exceptions-and-error-messages-might-reveal-data"></a>예외 및 오류 메시지에서 데이터를 드러낼 수 있음  
 오류에 대한 설명에서 변환 중인 데이터, 파일 이름 또는 구현 정보와 같은 데이터를 드러낼 수 있습니다. 오류 메시지는 신뢰할 수 없는 호출자에게 노출되지 않아야 합니다. 사용자 지정 오류 메시지를 사용하여 모든 오류와 보고서 오류를 catch해야 합니다.  
  
### <a name="do-not-call-codeaccesspermissionsassert-in-an-event-handler"></a>이벤트 처리기에서 CodeAccessPermissions.Assert를 호출하지 않아야 함  
 어셈블리는 적은 권한이나 많은 권한을 가질 수 있습니다. 많은 권한을 가진 어셈블리는 컴퓨터와 환경을 더 많이 제어합니다.  
  
 많은 권한을 가진 어셈블리의 코드가 이벤트 처리기에서 <xref:System.Security.CodeAccessPermission.Assert%2A?displayProperty=nameWithType>를 호출한 후 제한된 권한을 가진 악의적인 어셈블리에 XML 트리가 전달되면 악의적인 어셈블리로 인해 이벤트가 발생할 수 있습니다. 이벤트에서 많은 권한을 가진 어셈블리에 있는 코드를 실행하기 때문에 악의적인 어셈블리가 상승된 권한으로 작동합니다.  
  
 이벤트 처리기에서 <xref:System.Security.CodeAccessPermission.Assert%2A?displayProperty=nameWithType>를 절대로 호출하지 않는 것이 좋습니다.  
  
### <a name="dtds-are-not-secure"></a>DTD에 보안이 설정되지 않음  
 DTD의 엔터티에는 기본적으로 보안이 설정되지 않습니다. DTD가 포함된 악의적인 XML 문서로 인해 파서에서 모든 메모리와 CPU 시간을 사용하여 서비스 거부 공격을 일으킬 수 있습니다. 따라서 LINQ to XML에서 DTD 처리는 기본적으로 해제되어 있습니다. 신뢰할 수 없는 소스에서는 DTD를 받아들이지 않아야 합니다.  
  
 신뢰할 수 없는 소스에서 DTD를 받아들이는 한 가지 예는 웹 사용자가 DTD와 DTD 파일을 참조하는 XML 파일을 업로드할 수 있도록 하는 웹 응용 프로그램입니다. 파일의 유효성을 검사할 때 악의적인 DTD는 서버에서 서비스 거부 공격을 실행할 수 있습니다. 신뢰할 수 없는 소스에서 DTD를 받아들이는 또 다른 예는 익명 FTP 액세스도 허용하는 네트워크 공유에서 DTD를 참조하는 경우입니다.  
  
### <a name="avoid-excessive-buffer-allocation"></a>과도한 버퍼 할당 방지  
 응용 프로그램 개발자는 데이터 소스가 매우 크면 리소스가 고갈되고 서비스 거부 공격이 발생할 수 있음을 명심해야 합니다.  
  
 악의적인 사용자가 매우 큰 XML 문서를 제출하거나 업로드하면 LINQ to XML에서 시스템 리소스를 지나치게 많이 사용할 수 있으며, 이로 인해 서비스 거부 공격이 발생할 수 있습니다. 이를 방지하기 위해 <xref:System.Xml.XmlReaderSettings.MaxCharactersInDocument%2A?displayProperty=nameWithType> 속성을 설정하고 로드할 수 있는 문서 크기로 제한된 판독기를 만들 수 있습니다. 그런 다음 판독기를 사용하여 XML 트리를 만듭니다.  
  
 예를 들어, 신뢰할 수 없는 소스에서 제공되는 XML 문서의 최대 예상 크기가 50K바이트보다 작을 것으로 예상되면 <xref:System.Xml.XmlReaderSettings.MaxCharactersInDocument%2A?displayProperty=nameWithType>를 100,000으로 설정합니다. 이렇게 하는 경우 XML 문서의 처리가 방해를 받지 않으며 이와 동시에 많은 메모리를 사용할 문서가 업로드될 수 있는 서비스 거부 위협이 완화됩니다.  
  
### <a name="avoid-excess-entity-expansion"></a>지나친 엔터티 확장 방지  
 DTD를 사용하는 경우 알려진 서비스 거부 공격 중 하나는 지나친 엔터티 확장을 발생시키는 문서입니다. 이를 방지하기 위해 <xref:System.Xml.XmlReaderSettings.MaxCharactersFromEntities%2A?displayProperty=nameWithType> 속성을 설정하고 엔터티 확장으로 발생하는 문자 수로 제한된 판독기를 만들 수 있습니다. 그런 다음 판독기를 사용하여 XML 트리를 만듭니다.  
  
### <a name="limit-the-depth-of-the-xml-hierarchy"></a>XML 계층 구조의 깊이 제한  
 한 가지 가능한 서비스 거부 공격은 계층 구조의 깊이가 매우 큰 문서가 제출되는 경우입니다. 이를 방지하기 위해 <xref:System.Xml.XmlReader>를 요소의 깊이를 세는 자체 클래스에 래핑할 수 있습니다. 깊이가 미리 결정된 적절한 수준을 초과하면 악의적인 문서의 처리를 종료할 수 있습니다.  
  
### <a name="protect-against-untrusted-xmlreader-or-xmlwriter-implementations"></a>신뢰할 수 없는 XmlReader 또는 XmlWriter 구현으로부터 보호  
 관리자는 외부에서 제공된 <xref:System.Xml.XmlReader> 또는 <xref:System.Xml.XmlWriter> 구현이 강력한 이름을 갖고 있고 컴퓨터 구성에 등록되어 있는지 확인해야 합니다. 이렇게 하면 판독기 또는 작성기로 가장한 악의적인 코드가 로드되는 것이 방지됩니다.  
  
### <a name="periodically-free-objects-that-reference-xname"></a>XName을 참조하는 개체의 주기적 해제  
 특정 유형의 공격으로부터 보호하기 위해 응용 프로그램 프로그래머는 응용 프로그램 도메인에서 <xref:System.Xml.Linq.XName> 개체를 참조하는 모든 개체를 주기적으로 해제해야 합니다.  
  
### <a name="protect-against-random-xml-names"></a>임의의 XML 이름으로부터 보호  
 신뢰할 수 없는 소스에서 데이터를 가져오는 응용 프로그램은 임의의 XML 이름 및 네임스페이스의 가능성을 검사하기 위해 사용자 지정 코드에 래핑된 <xref:System.Xml.XmlReader>를 사용하는 것을 고려해야 합니다. 이러한 임의의 XML 이름 및 네임스페이스가 검색되면 응용 프로그램에서 악의적인 문서의 처리를 종료할 수 있습니다.  
  
 네임스페이스에 없는 이름을 비롯하여 지정된 네임스페이스에서 이름의 수를 적합한 한도까지 제한할 수 있습니다.  
  
### <a name="annotations-are-accessible-by-software-components-that-share-a-linq-to-xml-tree"></a>LINQ to XML 트리를 공유하는 소프트웨어 구성 요소에서 주석에 액세스할 수 있음  
 LINQ to XML을 사용하여 여러 응용 프로그램 구성 요소가 구성 요소 간에 전달되는 XML 데이터의 로드, 유효성 검사, 쿼리, 변환, 업데이트 및 XML 트리로의 저장을 수행하는 처리 파이프라인을 만들 수 있습니다. 이렇게 하면 개체를 로드하고 XML 텍스트로 serialize하는 오버헤드가 파이프라인 끝에서만 발생하므로 성능을 최적화하는 데 도움이 될 수 있습니다. 그러나 개발자는 한 구성 요소에서 만든 모든 주석과 이벤트 처리기를 다른 구성 요소에서 액세스할 수 있음을 명심해야 합니다. 이 때문에 구성 요소의 신뢰 수준이 서로 다른 경우 많은 취약점이 생길 수 있습니다. 신뢰 수준이 낮은 구성 요소 간에 보안 파이프라인을 만들려면 신뢰할 수 없는 구성 요소에 데이터를 전달하기 전에 LINQ to XML 개체를 XML 텍스트로 serialize해야 합니다.  
  
 일부 보안은 CLR(공용 언어 런타임)을 통해 제공됩니다. 예를 들어, private 클래스가 포함되지 않은 구성 요소는 해당 클래스에서 입력한 주석에 액세스할 수 없습니다. 그러나 주석을 읽을 수 없는 구성 요소에서 주석을 삭제할 수 있으며, 이것이 변조 공격으로 사용될 수 있습니다.  
  
## <a name="see-also"></a>참고 항목

- [프로그래밍 가이드(LINQ to XML)(C#)](../../../../csharp/programming-guide/concepts/linq/programming-guide-linq-to-xml.md)
