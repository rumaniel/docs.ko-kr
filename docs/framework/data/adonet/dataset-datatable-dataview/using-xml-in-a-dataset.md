---
title: 데이터 세트에서 XML 사용
ms.date: 03/30/2017
ms.assetid: 35138159-e199-49ec-baf7-1ec6777e171e
ms.openlocfilehash: ca04f524685e080be6af12a4df6eda585a908683
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784261"
---
# <a name="using-xml-in-a-dataset"></a>데이터 세트에서 XML 사용
ADO.NET을 사용하면 XML 스트림이나 문서에서 <xref:System.Data.DataSet>을 채울 수 있습니다. XML 스트림이나 문서를 사용하여 데이터, 스키마 정보 또는 두 가지 모두를 <xref:System.Data.DataSet>에 제공할 수 있습니다. XML 스트림이나 문서에서 제공되는 정보를 <xref:System.Data.DataSet>에 있는 기존 데이터나 스키마 정보와 결합할 수 있습니다.  
  
 또한 ADO.NET을 사용하면 스키마 사용 여부에 관계없이 <xref:System.Data.DataSet>의 XML 표현을 만들어 다른 애플리케이션이나 XML 사용 플랫폼에서 사용할 수 있도록 HTTP를 통해 <xref:System.Data.DataSet>을 전송할 수 있습니다. <xref:System.Data.DataSet>의 XML 표현에서 데이터는 XML로 작성되며, 스키마는 XML 표현의 인라인에 포함되어 있는 경우 XSD(XML 스키마 정의 언어)를 사용하여 작성됩니다. XML 및 XML 스키마에서는 <xref:System.Data.DataSet>의 내용을 원격 클라이언트와 주고 받기에 알맞은 형식을 제공합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [DiffGram](diffgrams.md)  
 <xref:System.Data.DataSet>의 내용을 읽거나 쓰는 데 사용하는 XML 형식인 DiffGram에 대해 자세히 설명합니다.  
  
 [XML에서 데이터 세트 로드](loading-a-dataset-from-xml.md)  
 XML 문서에서 <xref:System.Data.DataSet>의 내용을 로드할 때 고려할 여러 가지 옵션에 대해 설명합니다.  
  
 [데이터 세트 콘텐츠를 XML 데이터로 작성](writing-dataset-contents-as-xml-data.md)  
 <xref:System.Data.DataSet>의 내용을 XML 데이터로 생성하는 방법과 사용할 수 있는 여러 XML 형식 옵션에 대해 설명합니다.  
  
 [XML에서 데이터 세트 스키마 정보 로드](loading-dataset-schema-information-from-xml.md)  
 XML에서 <xref:System.Data.DataSet>의 스키마를 로드하는 데 사용하는 <xref:System.Data.DataSet> 메서드에 대해 설명합니다.  
  
 [데이터 세트 스키마 정보를 XSD로 작성](writing-dataset-schema-information-as-xsd.md)  
 XML 스키마의 용도와 <xref:System.Data.DataSet>에서 XML 스키마를 생성하는 방법에 대해 설명합니다.  
  
 [데이터 세트 및 XmlDataDocument 동기화](dataset-and-xmldatadocument-synchronization.md)  
 단일 데이터 집합에 대한 관계형 뷰와 계층적 뷰에 동기적으로 액세스할 수 있는 .NET Framework의 기능과 <xref:System.Data.DataSet> 및 <xref:System.Xml.XmlDataDocument> 간에 동기적 관계를 만드는 방법에 대해 설명합니다.  
  
 [DataRelation 중첩](nesting-datarelations.md)  
 <xref:System.Data.DataRelation>의 내용을 XML 데이터로 표현할 경우 중첩된 <xref:System.Data.DataSet> 개체의 중요성과 이러한 개체를 만드는 방법에 대해 설명합니다.  
  
 [XML 스키마에서 데이터 세트 관계형 구조 파생(XSD)](deriving-dataset-relational-structure-from-xml-schema-xsd.md)  
 XML 스키마에서 만들어진 <xref:System.Data.DataSet>의 관계 구조 또는 스키마에 대해 설명합니다.  
  
 [XML에서 데이터 세트 관계형 구조 유추](inferring-dataset-relational-structure-from-xml.md)  
 XML 요소에서 유추할 때 만들어지는 <xref:System.Data.DataSet>의 관계형 구조 또는 스키마에 대해 설명합니다.  
  
## <a name="related-sections"></a>관련 단원  
 [ADO.NET 개요](../ado-net-overview.md)  
 ADO.NET 아키텍처 및 구성 요소에 대해 설명하고, 이를 사용하여 기존 데이터 소스에 액세스하고 애플리케이션 데이터를 관리하는 방법을 설명합니다.  
  
## <a name="see-also"></a>참고자료

- [DataSet, DataTable 및 DataView](index.md)
- [ADO.NET 개요](../ado-net-overview.md)
