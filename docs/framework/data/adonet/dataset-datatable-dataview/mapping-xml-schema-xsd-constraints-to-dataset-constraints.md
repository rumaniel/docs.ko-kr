---
title: 데이터 세트 제약 조건에 XSD(XML 스키마) 제약 조건 매핑
ms.date: 03/30/2017
ms.assetid: 3d0d1a4b-9104-434f-ac04-6c01ab5716b5
ms.openlocfilehash: b44c3193e1b9e2e52e086111eab0ab0b0cae5c97
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70786080"
---
# <a name="mapping-xml-schema-xsd-constraints-to-dataset-constraints"></a>데이터 세트 제약 조건에 XSD(XML 스키마) 제약 조건 매핑
XSD(XML 스키마 정의 언어)를 사용하여 요소와 특성에서 제약 조건을 지정할 수 있습니다. Xml 스키마를의 <xref:System.Data.DataSet>관계형 스키마에 매핑할 때 xml 스키마 제약 조건은 **데이터 집합**내의 테이블 및 열에 대 한 적절 한 관계형 제약 조건에 매핑됩니다.  
  
 이 단원에서는 다음 XML 스키마 제약 조건의 매핑에 대해 설명합니다.  
  
- **Unique** 요소를 사용 하 여 지정 된 고유성 제약 조건입니다.  
  
- **Key** 요소를 사용 하 여 지정 된 키 제약 조건입니다.  
  
- **Keyref** 요소를 사용 하 여 지정 된 keyref 제약 조건입니다.  
  
 요소나 특성에서 제약 조건을 사용하여 문서의 모든 인스턴스에서 요소의 값에 특정 제한 사항을 지정할 수 있습니다. 예를 들어 스키마에 있는 **Customer** 요소의 **customerid** 자식 요소에 대 한 key 제약 조건은 **customerid** 자식 요소의 값이 모든 문서 인스턴스에서 고유 해야 하며 null 값이 허용 되지 않음을 나타냅니다.  
  
 또한 문서 내에서 관계를 설정하도록 문서의 요소와 특성 사이에 제약 조건을 지정할 수 있습니다. KEY 및 KEYREF 제약 조건은 스키마에서 사용되어 문서 내에서의 제약 조건을 지정함으로써 결과적으로 문서 요소와 특성 간의 관계를 설정합니다.  
  
 매핑 프로세스에서는 이러한 스키마 제약 조건을 **데이터 집합**내에서 생성 된 테이블에 대 한 적절 한 제약 조건으로 변환 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [데이터 세트 제약 조건에 고유 XSD(XML 스키마) 제약 조건 매핑](map-unique-xml-schema-xsd-constraints-to-dataset-constraints.md)  
 **데이터 집합**에서 unique 제약 조건을 만드는 데 사용 되는 XML 스키마 요소에 대해 설명 합니다.  
  
 [데이터 세트 제약 조건에 키 XSD(XML 스키마) 제약 조건 매핑](map-key-xml-schema-xsd-constraints-to-dataset-constraints.md)  
 **데이터 집합**에서 키 제약 조건 (null 값이 허용 되지 않는 unique 제약 조건)을 만드는 데 사용 되는 XML 스키마 요소에 대해 설명 합니다.  
  
 [데이터 세트 제약 조건에 keyref XSD(XML 스키마) 제약 조건 매핑](map-keyref-xml-schema-xsd-constraints-to-dataset-constraints.md)  
 **데이터 집합**에서 keyref (외래 키) 제약 조건을 만드는 데 사용 되는 XML 스키마 요소에 대해 설명 합니다.  
  
## <a name="related-sections"></a>관련 단원  
 [XML 스키마에서 데이터 세트 관계형 구조 파생(XSD)](deriving-dataset-relational-structure-from-xml-schema-xsd.md)  
 XSD 스키마에서 생성 되는 **데이터 집합** 의 관계형 구조 또는 스키마에 대해 설명 합니다.  
  
 [XSD(XML 스키마)에서 데이터 세트 관계 생성](generating-dataset-relations-from-xml-schema-xsd.md)  
 **데이터 집합**에 있는 테이블 열 간의 관계를 만드는 데 사용 되는 XML 스키마 요소에 대해 설명 합니다.  
  
## <a name="see-also"></a>참고자료

- [ADO.NET 개요](../ado-net-overview.md)
