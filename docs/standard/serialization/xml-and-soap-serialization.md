---
title: XML 및 SOAP Serialization
ms.date: 03/30/2017
helpviewer_keywords:
- SOAP, XML serialization
- XML serialization, SOAP
- serialization, SOAP
- serialization, about serialization
- XML serialization
- serialization
ms.assetid: 832ac524-21bc-419a-a27b-ca8bfc45840f
ms.openlocfilehash: d9dc68d8e7eced031af404aaec20784573c9930a
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62028241"
---
# <a name="xml-and-soap-serialization"></a>XML 및 SOAP Serialization

XML serialization은 개체의 public 필드와 속성 또는 메서드의 매개 변수와 반환 값을 특정 XSD(XML 스키마 정의 언어) 문서와 일치하는 XML 스트림으로 변환(serialize)합니다. XML serialization을 사용하면 스토리지이나 전송을 위해 직렬 형식(이 경우 XML)으로 변환되는 public 속성 및 필드가 있는 강력한 형식의 클래스가 만들어집니다.

XML은 공개 표준이기 때문에 XML 스트림은 플랫폼에 관계없이 필요에 따라 모든 애플리케이션에서 처리될 수 있습니다. 예를 들어 ASP.NET을 사용하여 만들어진 XML Web services는 <xref:System.Xml.Serialization.XmlSerializer> 클래스를 사용하여 데이터를 인터넷이나 인트라넷을 통해 XML Web services 애플리케이션 간에 전달하는 XML 스트림을 만듭니다. 이와 반대로 deserialization에서는 이러한 XML 스트림을 받아서 개체를 다시 만듭니다.

XML serialization은 SOAP 사양과 일치하는 XML 스트림으로 개체를 serialize하는 데 사용할 수도 있습니다. SOAP는 특히 XML을 사용하여 프로시저 호출을 전송하기 위해 디자인된 XML 기반 프로토콜입니다.

개체를 serialize하거나 deserialize하려면 <xref:System.Xml.Serialization.XmlSerializer> 클래스를 사용합니다. 클래스가 serialize되도록 하려면 XML 스키마 정의 도구를 사용합니다.

## <a name="in-this-section"></a>섹션 내용

[XML serialization 소개](introducing-xml-serialization.md)  
serialization, 특히 XML serialization에 대한 일반 정의를 제공합니다.

[방법: 개체 serialize](how-to-serialize-an-object.md)  
개체를 serialize하는 방법을 단계별로 설명합니다.

[방법: 개체 deserialize](how-to-deserialize-an-object.md)  
개체를 deserialize하는 방법을 단계별로 설명합니다.

[XML serialization 예제](examples-of-xml-serialization.md)  
XML serialization의 기본 사항을 보여 주는 예제를 제공합니다.

[XML 스키마 정의 도구 및 XML serialization](the-xml-schema-definition-tool-and-xml-serialization.md)  
XML 스키마 정의 도구를 사용하여 특정 XSD(XML 스키마 정의 언어) 스키마를 준수하거나 .dll 파일에서 XML 스키마를 생성하는 방법을 설명합니다.

[특성을 사용하여 XML serialization 제어](controlling-xml-serialization-using-attributes.md)  
특성을 사용하여 serialization을 제어하는 방법을 설명합니다.

[XML serialization을 제어하는 특성](attributes-that-control-xml-serialization.md)  
XML serialization의 제어에 사용되는 특성을 나열합니다.

[방법: XML Stream에 대 한 대체 요소 이름 지정](how-to-specify-an-alternate-element-name-for-an-xml-stream.md)  
serialization을 재정의하여 여러 XML 스트림을 생성하는 방법을 보여 주는 고급 시나리오를 소개합니다.

[방법: 파생된 클래스의 Serialization을 제어](how-to-control-serialization-of-derived-classes.md)  
파생 클래스의 serialization을 제어하는 방법을 보여 주는 예제를 제공합니다.

[방법: XML 요소 및 XML 특성 이름 한정](how-to-qualify-xml-element-and-xml-attribute-names.md)  
XML 네임스페이스가 XML 스트림에 사용되는 방법을 정의하고 제어하는 방법을 설명합니다.

[XML Web Services의 XML serialization](xml-serialization-with-xml-web-services.md)  
XML serialization이 XML Web services에 사용되는 방식을 설명합니다.

[방법: SOAP 인코딩된 XML Stream으로 개체를 serialize 합니다.](how-to-serialize-an-object-as-a-soap-encoded-xml-stream.md)  
사용 하는 방법에 설명 합니다 <xref:System.Xml.Serialization.XmlSerializer> World Wide Web Consortium (W3C) 문서의 5 단원을 준수 하는 인코딩된 SOAP XML 스트림을 만들 클래스 [단순 개체 액세스 프로토콜 (SOAP) 1.1](https://www.w3.org/TR/2000/NOTE-SOAP-20000508/)합니다.

[방법: 인코딩된 SOAP XML Serialization 재정의](how-to-override-encoded-soap-xml-serialization.md)  
개체의 XML serialization을 SOAP 메시지로 재정의하는 프로세스를 설명합니다.

[인코딩된 SOAP serialization을 제어하는 특성](attributes-that-control-encoded-soap-serialization.md)  
SOAP로 인코딩된 serialization의 제어에 사용되는 특성을 나열합니다.

[\<system.xml.serialization> 요소](system-xml-serialization-element.md)  
XML serialization을 제어하기 위한 최상위 구성 요소입니다.

[\<dateTimeSerialization> 요소](datetimeserialization-element.md)  
<xref:System.DateTime> 개체의 serialization 모드를 제어합니다.

[\<schemaImporterExtensions> 요소](schemaimporterextensions-element.md)  
<xref:System.Xml.Serialization.XmlSchemaImporter> 클래스에서 사용하는 형식을 포함합니다.

[\<추가 > 요소에 대 한 \<schemaImporterExtensions >](add-element-for-schemaimporterextensions.md)  
<xref:System.Xml.Serialization.XmlSchemaImporter> 클래스에서 사용하는 형식을 추가합니다.

## <a name="related-sections"></a>관련 단원

[ASP.NET 및 XML Web Service 클라이언트를 사용하여 만든 XML Web Services](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/7bkzywba(v=vs.100))  
ASP.NET을 사용하여 XML Web services를 프로그래밍하는 방법을 설명하는 항목을 제공합니다.

## <a name="see-also"></a>참고자료

- [이진 serialization](binary-serialization.md)
