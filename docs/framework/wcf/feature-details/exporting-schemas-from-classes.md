---
title: 클래스에서 스키마 내보내기
ms.date: 03/30/2017
helpviewer_keywords:
- WCF, schema import and export
- schemas [WCF], exporting from classes
- schemas [WCF]
- XsdDataContractExporter class
- XsdDataContractImporter class
ms.assetid: bb57b962-70c1-45a9-93d5-e721e340a13f
ms.openlocfilehash: 3db3cc1c529ab40bf775c06a5128e4dabf3c8a56
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69963646"
---
# <a name="exporting-schemas-from-classes"></a>클래스에서 스키마 내보내기
데이터 계약 모델에 사용되는 클래스에서 XSD(XML 스키마 정의 언어) 스키마를 생성하려면 <xref:System.Runtime.Serialization.XsdDataContractExporter> 클래스를 사용합니다. 이 항목에서는 스키마를 만드는 프로세스에 대해 설명합니다.  
  
## <a name="the-export-process"></a>내보내기 프로세스  
 스키마 내보내기 프로세스는 하나 이상의 형식으로 시작되고 해당 형식의 XML 프로젝션을 설명하는 <xref:System.Xml.Schema.XmlSchemaSet> 를 생성합니다.  
  
 는 `XmlSchemaSet` XSD 스키마 문서 집합을 나타내는 .NET Framework SOM (Schema Object Model)의 일부입니다. `XmlSchemaSet`에서 XSD 문서를 만들려면 <xref:System.Xml.Schema.XmlSchemaSet.Schemas%2A> 클래스의 `XmlSchemaSet` 속성에서 스키마 컬렉션을 사용합니다. 그런 다음 <xref:System.Xml.Schema.XmlSchema> 를 사용하여 각 <xref:System.Xml.Serialization.XmlSerializer>개체를 serialize합니다.  
  
#### <a name="to-export-schemas"></a>스키마를 내보내려면  
  
1. <xref:System.Runtime.Serialization.XsdDataContractExporter>의 인스턴스를 만듭니다.  
  
2. 선택 사항입니다. 생성자에 <xref:System.Xml.Schema.XmlSchemaSet> 를 포함하여 전달합니다. 이 경우 스키마를 내보내는 중 생성된 스키마는 빈 <xref:System.Xml.Schema.XmlSchemaSet> 로 시작하지 않고 이 <xref:System.Xml.Schema.XmlSchemaSet>인스턴스에 추가됩니다.  
  
3. 선택 사항입니다. <xref:System.Runtime.Serialization.XsdDataContractExporter.CanExport%2A> 메서드 중 하나를 호출합니다. 메서드에 따라 지정된 형식을 내보낼 수 있는지 여부가 결정됩니다. 이 메서드는 다음 단계의 `Export` 메서드와 동일한 오버로드를 갖습니다.  
  
4. <xref:System.Runtime.Serialization.XsdDataContractExporter.Export%2A> 메서드 중 하나를 호출합니다. <xref:System.Type>, <xref:System.Collections.Generic.List%601> 개체의 `Type` 또는 <xref:System.Collections.Generic.List%601> 개체의 <xref:System.Reflection.Assembly> 을 사용하는 세 가지 오버로드가 있습니다. 마지막 경우에서는 지정된 모든 어셈블리의 모든 형식을 내보냅니다.  
  
     `Export` 메서드를 여러 번 호출하면 동일한 `XmlSchemaSet`에 여러 항목이 추가됩니다. 형식이 이미 있으면 `XmlSchemaSet` 에 생성되지 않습니다. 따라서 `Export` 클래스의 여러 인스턴스를 만드는 경우 동일한 `XsdDataContractExporter` 에서 `XsdDataContractExporter` 를 여러 번 호출하는 것이 좋습니다. 이렇게 하면 중복 스키마 형식이 생성되지 않습니다.  
  
    > [!NOTE]
    > 내보내기 중 오류가 발생할 경우 `XmlSchemaSet` 상태를 예측할 수 없습니다.  
  
5. <xref:System.Xml.Schema.XmlSchemaSet> 속성을 통해 <xref:System.Runtime.Serialization.XsdDataContractExporter.Schemas%2A> 에 액세스합니다.  
  
## <a name="export-options"></a>내보내기 옵션  
 <xref:System.Runtime.Serialization.XsdDataContractExporter.Options%2A> 의 <xref:System.Runtime.Serialization.XsdDataContractExporter> 속성을 <xref:System.Runtime.Serialization.ExportOptions> 클래스로 설정하여 내보내기 프로세스의 다양한 측면을 제어할 수 있습니다. 특히 다음 옵션을 설정할 수 있습니다.  
  
- <xref:System.Runtime.Serialization.ExportOptions.KnownTypes%2A>. 이 `Type` 컬렉션은 내보내는 형식의 알려진 형식을 나타냅니다. 자세한 내용은 [데이터 계약 알려진 형식](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)을 참조 하세요. `Export` 메서드에 전달된 형식 외에도 이러한 알려진 형식이 모든 `Export` 호출 시 내보내집니다.  
  
- <xref:System.Runtime.Serialization.ExportOptions.DataContractSurrogate%2A>. 이 속성을 통해 내보내기 프로세스를 사용자 지정하는 <xref:System.Runtime.Serialization.IDataContractSurrogate> 를 제공할 수 있습니다. 자세한 내용은 [데이터 계약 서로게이트](../../../../docs/framework/wcf/extending/data-contract-surrogates.md)를 참조 하세요. 기본적으로 서로게이트는 사용되지 않습니다.  
  
## <a name="helper-methods"></a>도우미 메서드  
 스키마를 내보내는 기본 역할 외에도 `XsdDataContractExporter` 는 형식에 대한 정보를 제공하는 몇 가지 유용한 도우미 메서드를 제공합니다. 이러한 개체는 다음과 같습니다.  
  
- <xref:System.Runtime.Serialization.XsdDataContractExporter.GetRootElementName%2A> 메서드를 호출하여 생성됩니다. 이 메서드는 `Type` 을 받아서 이 형식이 루트 개체로 serialize된 경우에 사용되는 루트 요소 이름과 네임스페이스를 나타내는 <xref:System.Xml.XmlQualifiedName> 을 반환합니다.  
  
- <xref:System.Runtime.Serialization.XsdDataContractExporter.GetSchemaTypeName%2A> 메서드를 호출하여 생성됩니다. 이 메서드는 `Type` 을 받아서 이 형식을 스키마로 내보낸 경우에 사용되는 XSD 스키마 형식의 이름을 나타내는 <xref:System.Xml.XmlQualifiedName> 을 반환합니다. 스키마에 익명 형식으로 나타나는 <xref:System.Xml.Serialization.IXmlSerializable> 형식에 대해 이 메서드는 `null`을 반환합니다.  
  
- <xref:System.Runtime.Serialization.XsdDataContractExporter.GetSchemaType%2A> 메서드를 호출하여 생성됩니다. 이 메서드는 스키마에 익명 형식으로 나타나는 <xref:System.Xml.Serialization.IXmlSerializable> 형식에서만 작동하고 다른 모든 형식에 대해 `null` 을 반환합니다. 익명 형식의 경우 이 메서드는 지정된 <xref:System.Xml.Schema.XmlSchemaType> 을 나타내는 `Type`을 반환합니다.  
  
 내보내기 옵션은 이러한 모든 메서드에 영향을 줍니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.Serialization.DataContractSerializer>
- <xref:System.Runtime.Serialization.XsdDataContractImporter>
- <xref:System.Runtime.Serialization.XsdDataContractExporter>
- [스키마 가져오기 및 내보내기](../../../../docs/framework/wcf/feature-details/schema-import-and-export.md)
- [스키마를 가져와 클래스 생성](../../../../docs/framework/wcf/feature-details/importing-schema-to-generate-classes.md)
