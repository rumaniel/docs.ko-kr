---
title: '방법: 개체를 SOAP 인코딩된 XML 스트림으로 직렬화'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- SOAP, XML serialization
- XML serialization, SOAP
- serialization, SOAP
ms.assetid: af406e0a-fa3a-46dd-a7ba-c80731eba3a0
ms.openlocfilehash: bfbdda0861a6f2867a2e7003dd7054129fd343b8
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62018023"
---
# <a name="how-to-serialize-an-object-as-a-soap-encoded-xml-stream"></a>방법: 개체를 SOAP 인코딩된 XML 스트림으로 직렬화
  
 SOAP 메시지는 XML을 사용하여 생성되므로 <xref:System.Xml.Serialization.XmlSerializer> 클래스를 사용하여 클래스를 직렬화하고 인코딩된 SOAP 메시지를 생성할 수 있습니다. 결과 XML은 [World Wide Web 컨소시엄 문서의 5단원 “SOAP(Simple Object Access Protocol) 1.1”](https://www.w3.org/TR/2000/NOTE-SOAP-20000508/#_Toc478383512)을 따릅니다. SOAP 메시지를 통해 통신하는 XML Web services를 만들 때는 특별한 SOAP 특성 집합을 클래스와 클래스 멤버에 적용하여 XML 스트림을 사용자 지정할 수 있습니다. 특성 목록을 보려면 [인코딩된 SOAP serialization을 제어하는 특성](../../../docs/standard/serialization/attributes-that-control-encoded-soap-serialization.md)을 참조하세요.  
  
### <a name="to-serialize-an-object-as-a-soap-encoded-xml-stream"></a>개체를 SOAP 인코딩된 XML 스트림으로 serialize하려면  
  
1. [XML 스키마 정의 도구(Xsd.exe)](../../../docs/standard/serialization/xml-schema-definition-tool-xsd-exe.md)를 사용하여 클래스를 만듭니다.  
  
2. `System.Xml.Serialization`에 있는 하나 이상의 특수 특성을 적용합니다. "인코딩된 SOAP serialization을 제어하는 특성"의 목록을 참조하십시오.  
  
3. 새 `XmlTypeMapping`를 만들고 serialize된 클래스의 형식으로 `SoapReflectionImporter` 메서드를 호출하여 `ImportTypeMapping`을 만듭니다.  
  
     다음 코드 예제에서는 `SoapReflectionImporter` 클래스의 `ImportTypeMapping` 메서드를 호출하여 `XmlTypeMapping`을 만듭니다.  
  
    ```vb  
    ' Serializes a class named Group as a SOAP message.  
    Dim myTypeMapping As XmlTypeMapping =
        New SoapReflectionImporter().ImportTypeMapping(GetType(Group))  
    ```  
  
    ```csharp  
    // Serializes a class named Group as a SOAP message.  
    XmlTypeMapping myTypeMapping =
        new SoapReflectionImporter().ImportTypeMapping(typeof(Group));
    ```  
  
4. `XmlSerializer`을 `XmlTypeMapping` 생성자로 전달하여 <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Xml.Serialization.XmlTypeMapping%29> 클래스의 인스턴스를 만듭니다.  
  
    ```vb  
    Dim mySerializer As XmlSerializer = New XmlSerializer(myTypeMapping)  
    ```  
  
    ```csharp  
    XmlSerializer mySerializer = new XmlSerializer(myTypeMapping);  
    ```  
  
5. `Serialize` 또는 `Deserialize` 메서드를 호출합니다.  
  
## <a name="example"></a>예제  
  
```vb  
' Serializes a class named Group as a SOAP message.  
Dim myTypeMapping As XmlTypeMapping =
    New SoapReflectionImporter().ImportTypeMapping(GetType(Group))
Dim mySerializer As XmlSerializer = New XmlSerializer(myTypeMapping)  
```  
  
```csharp  
// Serializes a class named Group as a SOAP message.  
XmlTypeMapping myTypeMapping =
    new SoapReflectionImporter().ImportTypeMapping(typeof(Group));
XmlSerializer mySerializer = new XmlSerializer(myTypeMapping);  
```  
  
## <a name="see-also"></a>참고자료

- [XML 및 SOAP serialization](../../../docs/standard/serialization/xml-and-soap-serialization.md)
- [인코딩된 SOAP serialization을 제어하는 특성](../../../docs/standard/serialization/attributes-that-control-encoded-soap-serialization.md)
- [XML Web Services의 XML serialization](../../../docs/standard/serialization/xml-serialization-with-xml-web-services.md)
- [방법: 개체 serialize](../../../docs/standard/serialization/how-to-serialize-an-object.md)
- [방법: 개체 deserialize](../../../docs/standard/serialization/how-to-deserialize-an-object.md)
- [방법: 인코딩된 SOAP XML Serialization 재정의](../../../docs/standard/serialization/how-to-override-encoded-soap-xml-serialization.md)
