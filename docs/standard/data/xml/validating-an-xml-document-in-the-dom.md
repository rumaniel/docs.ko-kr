---
title: DOM에서의 XML 문서 유효성 검사
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
ms.assetid: 2c61c920-d0f8-4c72-bfcc-6524570f3060
author: mairaw
ms.author: mairaw
ms.openlocfilehash: d0f5ae64eb1017570a56efab59a4bf1a66d5e02b
ms.sourcegitcommit: 8c28ab17c26bf08abbd004cc37651985c68841b8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2018
ms.locfileid: "48846242"
---
# <a name="validating-an-xml-document-in-the-dom"></a>DOM에서의 XML 문서 유효성 검사
기본적으로 <xref:System.Xml.XmlDocument> 클래스는 기본적으로 DOM(문서 개체 모델)에서 XSD(XML 스키마 정의 언어) 스키마 또는 DTD(문서 종류 정의)에 대해 XML의 유효성을 검사하지 않으며 XML이 제대로 구성되었는지만 확인합니다.  
  
 DOM에서 XML의 유효성을 검사하려면 스키마의 유효성을 검사하는 <xref:System.Xml.XmlReader>를 <xref:System.Xml.XmlDocument.Load%2A> 클래스의 <xref:System.Xml.XmlDocument> 메서드에 전달하여 DOM에 XML을 로드할 때 유효성을 검사하거나 <xref:System.Xml.XmlDocument.Validate%2A> 클래스의 <xref:System.Xml.XmlDocument> 메서드를 사용하여 DOM에서 이전에 유효성을 검사하지 않은 XML 문서의 유효성을 검사합니다.  
  
## <a name="validating-an-xml-document-as-it-is-loaded-into-the-dom"></a>XML 문서를 DOM에 로드할 때 유효성 검사  
 유효성을 검사하는 <xref:System.Xml.XmlDocument>가 <xref:System.Xml.XmlReader> 클래스의 <xref:System.Xml.XmlDocument.Load%2A> 메서드에 전달되면 <xref:System.Xml.XmlDocument> 클래스는 XML 데이터를 DOM에 로드할 때 유효성을 검사합니다.  
  
 유효성 검사를 수행한 후에는 스키마 기본값이 적용되고 필요한 경우 텍스트 값이 atomic 값으로 변환되며 형식 정보는 유효성이 검사된 정보 항목과 연결됩니다. 그 결과, 형식화된 XML 데이터가 이전에 형식화되지 않은 XML 데이터를 대체합니다.  
  
### <a name="creating-an-xml-schema-validating-xmlreader"></a>XML 스키마의 유효성을 검사하는 XmlReader 만들기  
 XML 스키마의 유효성을 검사하는 <xref:System.Xml.XmlReader>를 만들려면 다음 단계를 수행합니다.  
  
1.  새 <xref:System.Xml.XmlReaderSettings> 인스턴스를 생성합니다.  
  
2.  XML 스키마를 <xref:System.Xml.XmlReaderSettings.Schemas%2A> 인스턴스의 <xref:System.Xml.XmlReaderSettings> 속성에 추가합니다.  
  
3.  `Schema`를 <xref:System.Xml.XmlReaderSettings.ValidationType%2A>으로 지정합니다.  
  
4.  필요에 따라 유효성 검사 중에 발생하는 스키마 유효성 검사 오류 및 경고를 처리하는 <xref:System.Xml.XmlReaderSettings.ValidationFlags%2A> 및 <xref:System.Xml.XmlReaderSettings.ValidationEventHandler>를 지정할 수도 있습니다.  
  
5.  마지막으로 XML 문서와 함께 <xref:System.Xml.XmlReaderSettings> 개체를 <xref:System.Xml.XmlReader.Create%2A> 클래스의 <xref:System.Xml.XmlReader> 메서드에 전달하여 스키마의 유효성을 검사하는 <xref:System.Xml.XmlReader>를 만듭니다.  
  
### <a name="example"></a>예  
 다음 코드 예제에서는 스키마의 유효성을 검사하는 <xref:System.Xml.XmlReader>가 DOM에 로드된 XML 데이터의 유효성을 검사합니다. 또한 XML 문서를 잘못 수정하고 이 문서의 유효성을 다시 검사하므로 스키마 유효성 검사 오류가 발생합니다. 마지막으로 오류 중 하나를 수정한 다음 XML 문서의 일부에 대한 유효성을 부분적으로 검사합니다.  
  
 [!code-cpp[XmlDocumentValidation.Load#1](../../../../samples/snippets/cpp/VS_Snippets_Data/XmlDocumentValidation.Load/CPP/XmlDocumentValidationExample.cpp#1)]
 [!code-csharp[XmlDocumentValidation.Load#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlDocumentValidation.Load/CS/XmlDocumentValidationExample.cs#1)]
 [!code-vb[XmlDocumentValidation.Load#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlDocumentValidation.Load/VB/XmlDocumentValidationExample.vb#1)]  
  
 이 예제에서는 `contosoBooks.xml` 파일을 입력으로 사용합니다.  
  
 [!code-xml[XPathXMLExamples#2](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xml#2)]  
  
 이 예제에서는 `contosoBooks.xsd` 파일을 입력으로 사용합니다.  
  
 [!code-xml[XPathXMLExamples#3](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/contosoBooks.xsd#3)]  
  
 XML 데이터를 DOM에 로드할 때 유효성을 검사하는 경우 다음을 고려해야 합니다.  
  
-   위 예제에서 잘못된 형식이 발견될 때마다 <xref:System.Xml.XmlReaderSettings.ValidationEventHandler>가 호출됩니다. <xref:System.Xml.XmlReaderSettings.ValidationEventHandler>가 유효성을 검사하는 <xref:System.Xml.XmlReader>에 대해 설정되어 있지 않으면 특성 또는 요소 형식이 유효성 검사 스키마에 지정된 해당 형식과 일치하지 않은 경우 <xref:System.Xml.Schema.XmlSchemaValidationException>가 호출될 때 <xref:System.Xml.XmlDocument.Load%2A>이 throw됩니다.  
  
-   기본값을 정의하는 스키마가 연결되어 있는 XML 문서를 <xref:System.Xml.XmlDocument> 개체에 로드하면 <xref:System.Xml.XmlDocument>는 이 기본값이 XML 문서에 나타난 것처럼 처리합니다. 그러므로 <xref:System.Xml.XmlReader.IsEmptyElement%2A> 속성은 항상 스키마의 기본값으로 설정된 요소에 대해 `false`를 반환합니다. XML 문서에서도 빈 요소로 작성됩니다.  
  
## <a name="validating-an-xml-document-in-the-dom"></a>DOM에서의 XML 문서 유효성 검사  
 <xref:System.Xml.XmlDocument.Validate%2A> 클래스의 <xref:System.Xml.XmlDocument> 메서드는 <xref:System.Xml.XmlDocument> 개체의 <xref:System.Xml.XmlDocument.Schemas%2A> 속성에 있는 스키마에 대해 DOM에 로드된 XML 데이터의 유효성을 검사합니다. 유효성 검사를 수행한 후에는 스키마 기본값이 적용되고 필요한 경우 텍스트 값이 atomic 값으로 변환되며 형식 정보는 유효성이 검사된 정보 항목과 연결됩니다. 그 결과, 형식화된 XML 데이터가 이전에 형식화되지 않은 XML 데이터를 대체합니다.  
  
 아래 예제는 위의 "XML 문서를 DOM에 로드할 때 유효성 검사"의 예제와 비슷합니다. 이 예제에서는 XML 문서를 DOM에 로드할 때 유효성을 검사하지 않고 DOM에 로드한 후 <xref:System.Xml.XmlDocument.Validate%2A> 클래스의 <xref:System.Xml.XmlDocument> 메서드를 사용하여 검사합니다. <xref:System.Xml.XmlDocument.Validate%2A> 메서드는 <xref:System.Xml.XmlDocument.Schemas%2A>의 <xref:System.Xml.XmlDocument> 속성에 포함된 XML 스키마에 대해 XML 문서의 유효성을 검사합니다. 또한 XML 문서를 잘못 수정하고 이 문서의 유효성을 다시 검사하므로 스키마 유효성 검사 오류가 발생합니다. 마지막으로 오류 중 하나를 수정한 다음 XML 문서의 일부에 대한 유효성을 부분적으로 검사합니다.  
  
 [!code-csharp[XmlDocumentValidation.Validate#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XmlDocumentValidation.Validate/CS/XmlDocumentValidationExample.cs#1)]
 [!code-vb[XmlDocumentValidation.Validate#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XmlDocumentValidation.Validate/VB/XmlDocumentValidationExample.vb#1)]  
  
 이 예제에서는 위의 "XML 문서를 DOM에 로드할 때 유효성 검사"에 참조된 `contosoBooks.xml` 및 `contosoBooks.xsd` 파일을 입력으로 사용합니다.  
  
## <a name="handling-validation-errors-and-warnings"></a>유효성 검사 오류 및 경고 처리  
 DOM에 로드된 XML 데이터의 유효성을 검사하면 XML 스키마 유효성 검사 오류가 보고됩니다. XML 데이터를 로드할 때 수행한 유효성 검사 또는 이전에 유효성을 검사하지 않은 XML 문서의 유효성 검사에서 발견된 모든 스키마 유효성 검사 오류에 대해 알림을 받습니다.  
  
 유효성 검사 오류는 <xref:System.Xml.Schema.ValidationEventHandler>에서 처리합니다. <xref:System.Xml.Schema.ValidationEventHandler>를 <xref:System.Xml.XmlReaderSettings> 인스턴스에 지정하거나 <xref:System.Xml.XmlDocument.Validate%2A> 클래스의 <xref:System.Xml.XmlDocument> 메서드에 전달한 경우 <xref:System.Xml.Schema.ValidationEventHandler>는 스키마 유효성 검사 오류를 처리하며 그렇지 않은 경우에는 스키마 유효성 검사 오류가 발생할 때 <xref:System.Xml.Schema.XmlSchemaValidationException>이 일어납니다.  
  
> [!NOTE]
>  <xref:System.Xml.Schema.ValidationEventHandler>에 의해 예외가 발생하여 프로세스가 중지되지 않은 경우에는 스키마 유효성 검사 오류가 발생해도 XML 데이터가 DOM에 로드됩니다.  
>   
>  <xref:System.Xml.Schema.XmlSchemaValidationFlags.ReportValidationWarnings> 플래그를 <xref:System.Xml.XmlReaderSettings> 개체에 지정하지 않으면 스키마 유효성 검사 경고가 보고되지 않습니다.  
  
 <xref:System.Xml.Schema.ValidationEventHandler>를 설명하는 예제는 위의 "XML 문서를 DOM에 로드할 때 유효성 검사" 및 "DOM에서의 XML 문서 유효성 검사"를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Xml.XmlDocument>  
- <xref:System.Xml.XmlReader>  
- <xref:System.Xml.Schema.ValidationEventHandler>  
- <xref:System.Xml.XmlReaderSettings>  
- [DOM 모델을 사용하여 XML 데이터 처리](../../../../docs/standard/data/xml/process-xml-data-using-the-dom-model.md)  
- [XML 스키마 사용](../../../../docs/standard/data/xml/working-with-xml-schemas.md)
