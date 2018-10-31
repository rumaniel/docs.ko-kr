---
title: XmlSchemaCollection 스키마 컴파일
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 76f28770-7126-428f-9ed5-7b5ae8bad5ee
author: mairaw
ms.author: mairaw
ms.openlocfilehash: d7b6ea782020dde83aa7d59be8ec3058a27075ad
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2018
ms.locfileid: "48030670"
---
# <a name="xmlschemacollection-schema-compilation"></a>XmlSchemaCollection 스키마 컴파일
**XmlSchemaCollection**은 XDR(XML 데이터 축소) 및 XSD(XML 스키마 정의 언어) 스키마를 저장하고 유효성 검사를 수행할 수 있는 캐시 또는 라이브러리입니다. **XmlSchemaCollection**에서는 파일이나 URL에서 스키마에 액세스하는 대신 메모리에 있는 스키마를 캐시하여 성능을 향상시킵니다.  
  
> [!NOTE]
>  **XmlSchemaCollection** 클래스에서 XDR 스키마와 XML 스키마를 모두 저장하더라도 **XmlSchema** 개체를 사용하거나 반환하는 메서드 및 속성에서는 XML 스키마만 지원합니다.  
  
> [!IMPORTANT]
>  이제 <xref:System.Xml.Schema.XmlSchemaCollection> 클래스는 사용되지 않으며 <xref:System.Xml.Schema.XmlSchemaSet> 클래스로 대체되었습니다. <xref:System.Xml.Schema.XmlSchemaSet> 클래스에 대한 자세한 내용은 [스키마 컴파일을 위한 XmlSchemaSet](../../../../docs/standard/data/xml/xmlschemaset-for-schema-compilation.md)을 참조하세요.  
  
## <a name="add-schemas-to-the-collection"></a>컬렉션에 스키마 추가  
 스키마가 네임스페이스 URI에 연결될 때 **XmlSchemaCollection**의 **Add** 메서드를 사용하여 스키마가 컬렉션에 로드됩니다. XML 스키마의 경우 네임스페이스 URI는 일반적으로 스키마의 대상 네임스페이스입니다. XDR 스키마의 경우 네임스페이스 URI는 스키마를 컬렉션에 추가할 때 지정한 네임스페이스입니다.  
  
## <a name="check-for-a-schema-in-the-collection"></a>컬렉션의 스키마 확인  
 **Contains** 메서드를 사용하여 스키마가 컬렉션에 있는지 확인할 수 있습니다. **Contains** 메서드에서는 **XmlSchema** 개체(XML 스키마에만 해당) 또는 스키마와 연결된 네임스페이스 URI를 나타내는 문자열(XML 스키마와 XDR 스키마의 경우)을 사용합니다.  
  
## <a name="retrieve-a-schema-from-the-collection"></a>컬렉션에서 스키마 검색  
 **Item** 속성을 사용하여 컬렉션에서 스키마를 검색할 수 있습니다. **Item** 속성은 스키마와 연결된 네임스페이스(일반적으로 해당 대상 네임스페이스) URI를 나타내는 문자열을 사용하여 **XmlSchema** 개체를 반환합니다. **Item** 속성은 XML 스키마에만 적용됩니다. XDR 스키마에는 사용할 수 있는 개체 모델이 없기 때문에 반환 값은 항상 XDR 스키마에 대한 null 참조입니다.  
  
## <a name="validate-xml-documents-using-xmlschemacollection"></a>XmlSchemaCollection을 사용하여 XML 문서의 유효성 검사  
 생성된 **XmlSchemaCollection**을 **XmlValidatingReader**에 할당하기 위해 **XmlSchemaCollection** 개체를 만들고, 스키마를 컬렉션에 추가하며, **XmlValidatingReader**의 **Schemas** 속성을 설정하여 **XmlSchemaCollection**을 사용하는 XML 인스턴스 문서의 유효성을 검사할 수 있습니다.  
  
### <a name="improved-performance"></a>향상된 성능  
 동일한 스키마에서 두 개 이상의 문서에 대한 유효성을 검사하는 경우 메모리의 스키마를 캐시하여 더 나은 성능을 제공하므로 **XmlSchemaCollection**을 사용하는 것이 좋습니다.  
  
 다음 코드 예제에서는 **XmlSchemaCollection** 개체를 만들고, 스키마를 컬렉션에 추가하며, **Schemas** 속성을 설정합니다.  
  
```vb  
Dim tr as XmlTextReader = new XmlTextReader("Books.xml")  
Dim vr as XmlValidatingReader = new XmlValidatingReader(tr)  
Dim xsc as XmlSchemaCollection = new XmlSchemaCollection  
xsc.Add("urn:bookstore-schema", "Books.xsd")  
vr.Schemas.Add(xsc)  
```  
  
```csharp  
XmlTextReader tr = new XmlTextReader("Books.xml");  
XmlValidatingReader vr = new XmlValidatingReader(tr);  
XmlSchemaCollection xsc = new XmlSchemaCollection();  
xsc.Add("urn:bookstore-schema", "Books.xsd");    
vr.Schemas.Add(xsc);  
```  
  
## <a name="see-also"></a>참고 항목

- [XmlSchemaCollection을 사용하여 XDR 유효성 검사](../../../../docs/standard/data/xml/xdr-validation-with-xmlschemacollection.md)  
- [XmlSchemaCollection을 사용하여 XSD(XML 스키마) 유효성 검사](../../../../docs/standard/data/xml/xml-schema-xsd-validation-with-xmlschemacollection.md)
