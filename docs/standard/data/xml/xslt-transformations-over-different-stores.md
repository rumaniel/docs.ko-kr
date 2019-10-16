---
title: 여러 저장소에서의 XSLT 변환
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 369850e9-004a-45d2-b5c3-5060d9135adb
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 6a967ffe5db0b8b08adacff9085c7573867f21a4
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69910359"
---
# <a name="xslt-transformations-over-different-stores"></a>여러 저장소에서의 XSLT 변환
> [!NOTE]
> <xref:System.Xml.Xsl.XslTransform> 클래스는 .NET Framework 2.0에서 사용되지 않습니다. <xref:System.Xml.Xsl.XslCompiledTransform> 클래스를 사용하여 XSLT(Extensible Stylesheet Language for Transformations) 변환을 수행할 수 있습니다. 자세한 내용은 [XslCompiledTransform 클래스 사용](../../../../docs/standard/data/xml/using-the-xslcompiledtransform-class.md) 및 [XslTransform 클래스에서 마이그레이션](../../../../docs/standard/data/xml/migrating-from-the-xsltransform-class.md)을 참조하세요.  
  
 .NET Framework에서 ADO.NET 및 XML 클래스는 데이터에 액세스하는 통합된 프로그래밍 모델을 제공합니다. 이러한 데이터는 태그로 구분된 텍스트인 XML 데이터와 행 및 열로 구성된 테이블인 관계형 데이터 모두로 표현됩니다. .NET Framework에서 XML은 모든 데이터 스트림의 XML 데이터를 프로그래밍 방식으로 데이터에 액세스할 수 있는 XML DOM(문서 개체 모델) 노드 트리에 읽어오지만, ADO.NET은 <xref:System.Data.DataSet> 개체 내에서 관계형 데이터에 액세스하고 조작하는 수단을 제공합니다.  
  
 XML DOM은 XML 문서에 있는 데이터에 대한 액세스를 제공하며 XML 문서를 읽고, 쓰고, 탐색하는 추가 클래스를 제공합니다. 이러한 클래스는 ADO.NET으로 제공되는 데이터 액세스 서비스와 XML DOM을 통합하는 <xref:System.Xml> 네임스페이스에서 지원됩니다. <xref:System.Xml.XmlDataDocument>는 데이터에 대한 관계형 액세스를 제공합니다. <xref:System.Xml.XmlDataDocument>는 XML을 ADO.NET <xref:System.Data.DataSet>의 관계형 데이터에 매핑합니다. 모든 .NET Framework 기반 애플리케이션은 <xref:System.Xml> 네임스페이스의 클래스를 사용하여 XML 문서와 <xref:System.Xml.XmlDataDocument>의 관계형 데이터 모두에 액세스하고 이를 조작할 수 있습니다. 이러한 구현은 데이터를 수집하고 배포하는 n 계층 아키텍처를 지원합니다. 자세한 내용은 [XML과 관계형 데이터 및 ADO.NET의 통합](../../../../docs/standard/data/xml/xml-integration-with-relational-data-and-adonet.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- [XslTransform 클래스의 XSLT 프로세서 구현](../../../../docs/standard/data/xml/xsltransform-class-implements-the-xslt-processor.md)
