---
title: XML에서 데이터 세트 관계형 구조 유추
ms.date: 03/30/2017
ms.assetid: cd2f41c6-6785-420e-aa43-3ceb0bdccdce
ms.openlocfilehash: 1c8325d7ed52fea7397a7b5aa8744bdfa90b2c6e
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70785323"
---
# <a name="inferring-dataset-relational-structure-from-xml"></a>XML에서 데이터 세트 관계형 구조 유추
<xref:System.Data.DataSet>의 관계형 구조 또는 스키마는 테이블, 열, 제약 조건 및 관계로 구성됩니다. XML에서 <xref:System.Data.DataSet>을 로드할 때 로드되는 XML에서 스키마를 명시적으로 또는 유추를 통해 미리 정의하거나 만들 수 있습니다. Xml <xref:System.Data.DataSet> 에서 스키마 및 콘텐츠를 로드 하는 방법에 대 한 자세한 내용은 xml [에서 데이터 집합 로드](loading-a-dataset-from-xml.md) 및 [xml에서 데이터 집합 스키마 정보 로드](loading-dataset-schema-information-from-xml.md)를 참조 하세요.  
  
 Xml에서의 <xref:System.Data.DataSet> 스키마를 만드는 경우 기본 방법은 xml [스키마 (xsd)에서 데이터 집합 관계형 구조 파생](deriving-dataset-relational-structure-from-xml-schema-xsd.md)에 설명 된 xsd (xml 스키마 정의 언어)를 사용 하 여 스키마를 명시적으로 지정 하는 것입니다. XML-데이터 축소 (XDR). XML에서 XML 스키마나 XDR 스키마를 사용할 수 없으면 <xref:System.Data.DataSet>의 스키마는 XML 요소 및 특성의 구조로부터 유추할 수 있습니다.  
  
 이 단원에서는 XML 요소와 특성 및 이들의 구조, 그리고 결과로서 유추된 <xref:System.Data.DataSet> 스키마를 보여 줌으로써 <xref:System.Data.DataSet> 스키마 유추 규칙을 설명합니다.  
  
 XML 문서에 나타난 모든 특성을 유추 과정에 포함시켜야 하는 것은 아닙니다. 네임스페이스로 한정된 특성에서는 XML 문서에는 중요하지만 <xref:System.Data.DataSet> 스키마에는 중요하지 않은 메타데이터를 포함할 수 있습니다. <xref:System.Data.DataSet.InferXmlSchema%2A>를 사용하면 유추 과정에서 네임스페이스를 무시하도록 지정할 수 있습니다. 자세한 내용은 [XML에서 데이터 집합 스키마 정보 로드](loading-dataset-schema-information-from-xml.md)를 참조 하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
 [데이터 세트 스키마 유추 프로세스 요약](summary-of-the-dataset-schema-inference-process.md)  
 XML로부터 <xref:System.Data.DataSet>의 스키마를 유추하는 규칙에 대한 고급 요약 정보를 제공합니다.  
  
 [테이블 유추](inferring-tables.md)  
 <xref:System.Data.DataSet>에서 테이블로 유추되는 XML 요소에 대해 설명합니다.  
  
 [열 유추](inferring-columns.md)  
 테이블 열로 유추되는 XML 요소 및 특성에 대해 설명합니다.  
  
 [관계 유추](inferring-relationships.md)  
 중첩된 유추 테이블에 사용하도록 만들어지는 <xref:System.Data.DataRelation> 및 <xref:System.Data.ForeignKeyConstraint> 개체에 대해 설명합니다.  
  
 [요소 텍스트 유추](inferring-element-text.md)  
 XML 요소의 텍스트에 사용하기 위해 만드는 열과 XML 요소 내의 텍스트가 무시되는 경우에 대해 설명합니다.  
  
 [유추 제한](inference-limitations.md)  
 스키마 유추의 제한 사항에 대해 설명합니다.  
  
## <a name="related-sections"></a>관련 단원  
 [데이터 집합에서 XML 사용](using-xml-in-a-dataset.md)  
 <xref:System.Data.DataSet> 개체가 XML 데이터와 상호 작용하는 방법을 설명합니다.  
  
 [XML 스키마에서 데이터 세트 관계형 구조 파생(XSD)](deriving-dataset-relational-structure-from-xml-schema-xsd.md)  
 XSD(XML 스키마 정의 언어) 스키마에서 만들어지는 <xref:System.Data.DataSet>의 관계 구조 또는 스키마에 대해 설명합니다.  
  
 [ADO.NET 개요](../ado-net-overview.md)  
 ADO.NET 아키텍처 및 구성 요소에 대해 설명하고, 이를 사용하여 기존 데이터 소스에 액세스하고 애플리케이션 데이터를 관리하는 방법을 설명합니다.  
  
## <a name="see-also"></a>참고자료

- [ADO.NET 개요](../ado-net-overview.md)
