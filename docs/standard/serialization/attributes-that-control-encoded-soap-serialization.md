---
title: 인코딩된 SOAP Serialization을 제어하는 특성
ms.date: 03/30/2017
helpviewer_keywords:
- SOAP, XML serialization
- XML serialization, SOAP
- XML serialization, attributes
- attributes [.NET Framework], XML serialization
- serialization, attributes
ms.assetid: 93ee258c-9c0f-4a08-897c-c10db7a00f91
ms.openlocfilehash: 2961d9abc6c32e78b5a61e8f2bbea5cfcf6677bd
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61794942"
---
# <a name="attributes-that-control-encoded-soap-serialization"></a>인코딩된 SOAP Serialization을 제어하는 특성

이라는 World Wide Web Consortium (W3C) 문서 [단순 개체 액세스 프로토콜 (SOAP) 1.1](https://www.w3.org/TR/2000/NOTE-SOAP-20000508/) SOAP 매개 변수를 인코딩할 수 있는 방법을 설명 하는 선택적 단원 (5 단원)를 포함 합니다. 사양의 5단원을 따르려면 <xref:System.Xml.Serialization> 네임스페이스에 속한 특별한 특성 집합을 사용해야 합니다. 이러한 특성을 클래스 및 클래스 멤버에 적절하게 적용한 다음 <xref:System.Xml.Serialization.XmlSerializer>를 사용하여 클래스의 인스턴스를 serialize합니다.

다음 표에서는 특성, 해당 특성을 적용할 수 있는 위치 및 해당 특성이 수행하는 작업을 보여 줍니다. 이러한 특성이 XML serialization 제어를 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [방법: SOAP 인코딩된 XML Stream 개체 직렬화](how-to-serialize-an-object-as-a-soap-encoded-xml-stream.md) 고 [방법: 인코딩된 SOAP XML Serialization 재정의](how-to-override-encoded-soap-xml-serialization.md)합니다.

특성에 대한 자세한 내용은 [특성](../../../docs/standard/attributes/index.md)을 참조하세요.

|특성|적용 대상|설명|
|---------------|----------------|---------------|
|<xref:System.Xml.Serialization.SoapAttributeAttribute>|public 필드, 속성, 매개 변수 또는 반환 값입니다.|클래스 멤버는 XML 특성으로 serialize됩니다.|
|<xref:System.Xml.Serialization.SoapElementAttribute>|public 필드, 속성, 매개 변수 또는 반환 값입니다.|클래스는 XML 요소로 serialize됩니다.|
|<xref:System.Xml.Serialization.SoapEnumAttribute>|열거형 식별자인 public 필드입니다.|열거형 멤버의 요소 이름입니다.|
|<xref:System.Xml.Serialization.SoapIgnoreAttribute>|public 속성 및 필드입니다.|속성 또는 필드는 포함 클래스가 serialize될 때 무시되어야 합니다.|
|<xref:System.Xml.Serialization.SoapIncludeAttribute>|WSDL(웹 서비스 설명 언어) 문서에 대한 공용 파생 클래스 선언 및 공용 메서드입니다.|스키마를 생성할 때 형식을 포함해야 합니다(serialize될 때 인식되도록).|
|<xref:System.Xml.Serialization.SoapTypeAttribute>|public 클래스 선언입니다.|클래스는 XML 형식으로 serialize되어야 합니다.|

## <a name="see-also"></a>참고자료

- [XML 및 SOAP serialization](xml-and-soap-serialization.md)
- [방법: SOAP 인코딩된 XML Stream으로 개체를 serialize 합니다.](how-to-serialize-an-object-as-a-soap-encoded-xml-stream.md)
- [방법: 인코딩된 SOAP XML Serialization 재정의](how-to-override-encoded-soap-xml-serialization.md)
- [특성](../../../docs/standard/attributes/index.md)
- <xref:System.Xml.Serialization.XmlSerializer>
- [방법: 개체 serialize](how-to-serialize-an-object.md)
- [방법: 개체 deserialize](how-to-deserialize-an-object.md)
