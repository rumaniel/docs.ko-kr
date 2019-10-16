---
title: 유추 제한
ms.date: 03/30/2017
ms.assetid: 78517994-5d57-44f8-9d20-38812977de09
ms.openlocfilehash: 10347abc5b01edb4ec6fbf97221d44f4bfb88f54
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784584"
---
# <a name="inference-limitations"></a>유추 제한
XML에서 <xref:System.Data.DataSet> 스키마를 유추하는 과정을 통해 만들어지는 스키마는 각 문서의 XML 요소에 따라 다를 수 있습니다. 예를 들어, 다음과 같은 XML 문서를 가정해 봅시다.  
  
 Document1:  
  
```xml  
<DocumentElement>  
  <Element1>Text1</Element1>  
  <Element1>Text2</Element1>  
</DocumentElement>  
```  
  
 Document2:  
  
```xml  
<DocumentElement>  
  <Element1>Text1</Element1>  
</DocumentElement>  
```  
  
 "문서 1"의 경우 "Element1"가 반복 되는 요소 이므로 유추 프로세스에서 "DocumentElement" 라는 **데이터 집합과** "Element1" 라는 테이블을 생성 합니다.  
  
 **DataSet:** DocumentElement  
  
 **테이블** Element1  
  
|Element1_Text|  
|--------------------|  
|Text1|  
|Text2|  
  
 그러나 "Document2"의 경우 유추 프로세스는 "NewDataSet" 이라는 **데이터 집합과** "documentelement" 라는 테이블을 생성 합니다. "Element1"은 특성이나 자식 요소가 없으므로 열로 유추됩니다.  
  
 **DataSet:** NewDataSet  
  
 **테이블** DocumentElement  
  
|Element1|  
|--------------|  
|Text1|  
  
 이러한 두 XML 문서는 동일한 스키마를 생성하려는 의도로 만들어졌겠지만, 각 문서에 포함된 요소에 따라 유추 과정의 결과가 크게 달라졌습니다.  
  
 Xml 문서에서 스키마를 생성할 때 발생할 수 있는 불일치를 방지 하려면 xml에서 **데이터 집합** 을 로드할 때 XSD (xml 스키마 정의 언어) 또는 XDR (Xml 데이터 축소)를 사용 하 여 스키마를 명시적으로 지정 하는 것이 좋습니다. XML 스키마를 사용 하 여 **데이터 집합** 스키마를 명시적으로 지정 하는 방법에 대 한 자세한 내용은 [Xml 스키마에서 데이터 집합 관계형 구조 파생 (XSD)](deriving-dataset-relational-structure-from-xml-schema-xsd.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [XML에서 데이터 세트 관계형 구조 유추](inferring-dataset-relational-structure-from-xml.md)
- [XML에서 데이터 세트 로드](loading-a-dataset-from-xml.md)
- [XML에서 데이터 세트 스키마 정보 로드](loading-dataset-schema-information-from-xml.md)
- [데이터 집합에서 XML 사용](using-xml-in-a-dataset.md)
- [DataSet, DataTable 및 DataView](index.md)
- [ADO.NET 개요](../ado-net-overview.md)
