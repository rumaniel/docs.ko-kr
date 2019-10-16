---
title: 열 유추
ms.date: 03/30/2017
ms.assetid: 0e022699-c922-454c-93e2-957dd7e7247a
ms.openlocfilehash: 2718cbcf29799f99c8648b129fdb6079a6f6d344
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70786183"
---
# <a name="inferring-columns"></a>열 유추
ADO.NET에서 XML 문서로부터 <xref:System.Data.DataSet>의 테이블로 유추할 요소를 결정한 후에는 해당 테이블의 열을 유추합니다. ADO.NET 2.0에는 각 **simpleType** 요소에 대해 강력한 형식의 데이터 형식을 유추 하는 새로운 스키마 유추 엔진이 도입 되었습니다. 이전 버전에서는 유추 된 **simpleType** 요소의 데이터 형식이 항상 **xsd: string**이었습니다.  
  
## <a name="migration-and-backward-compatibility"></a>마이그레이션 및 이전 버전과의 호환성  
 **ReadXml** 메서드는 **InferSchema**형식의 인수를 사용 합니다. 이 인수를 사용하면 이전 버전과 호환되는 유추 동작을 지정할 수 있습니다. **InferSchema** 열거에 사용할 수 있는 값은 다음 표에 나와 있습니다.  
  
 <xref:System.Data.XmlReadMode.InferSchema>  
 항상 단순 형식을 <xref:System.String>으로 유추하여 이전 버전과의 호환성을 제공합니다.  
  
 <xref:System.Data.XmlReadMode.InferTypedSchema>  
 강력한 형식의 데이터 형식을 유추합니다. <xref:System.Data.DataTable>과 함께 사용할 경우 예외가 throw됩니다.  
  
 <xref:System.Data.XmlReadMode.IgnoreSchema>  
 인라인 스키마를 무시하고 데이터를 기존 <xref:System.Data.DataSet> 스키마로 읽어옵니다.  
  
## <a name="attributes"></a>특성  
 [테이블 유추](inferring-tables.md)에 정의 된 대로 특성이 있는 요소는 테이블로 유추 됩니다. 그러면 해당 요소의 특성은 테이블의 열로 유추됩니다. 열의 **ColumnMapping** 속성은 스키마가 XML에 다시 기록 될 경우 열 이름이 특성으로 기록 되도록 mappingtype.attribute로 설정 됩니다 **.** 특성 값은 테이블의 행에 저장됩니다. 예를 들어, 다음과 같은 XML을 가정해 봅시다.  
  
```xml  
<DocumentElement>  
  <Element1 attr1="value1" attr2="value2"/>  
</DocumentElement>  
```  
  
 유추 프로세스는 **attr1** 및 **attr2**라는 두 개의 열이 있는 **Element1** 이라는 테이블을 생성 합니다. 두 열의 **ColumnMapping** 속성은 **mappingtype.attribute**로 설정 됩니다.  
  
 **DataSet:** DocumentElement  
  
 **테이블** Element1  
  
|attr1|attr2|  
|-----------|-----------|  
|value1|value2|  
  
## <a name="elements-without-attributes-or-child-elements"></a>특성이나 자식 요소가 없는 요소  
 요소에 자식 요소나 특성이 없으면 해당 요소는 열로 유추됩니다. 열의 **ColumnMapping** 속성은 **mappingtype.attribute**로 설정 됩니다. 자식 요소의 텍스트는 해당 테이블의 행에 저장됩니다. 예를 들어, 다음과 같은 XML을 가정해 봅시다.  
  
```xml  
<DocumentElement>  
  <Element1>  
    <ChildElement1>Text1</ChildElement1>  
    <ChildElement2>Text2</ChildElement2>  
  </Element1>  
</DocumentElement>  
```  
  
 유추 프로세스는 **ChildElement1** 및 **childelement2 라는**라는 두 개의 열이 있는 **Element1** 이라는 테이블을 생성 합니다. 두 열의 **ColumnMapping** 속성은 **mappingtype.attribute**로 설정 됩니다.  
  
 **DataSet:** DocumentElement  
  
 **테이블** Element1  
  
|ChildElement1|ChildElement2|  
|-------------------|-------------------|  
|Text1|Text2|  
  
## <a name="see-also"></a>참고자료

- [XML에서 데이터 세트 관계형 구조 유추](inferring-dataset-relational-structure-from-xml.md)
- [XML에서 데이터 세트 로드](loading-a-dataset-from-xml.md)
- [XML에서 데이터 세트 스키마 정보 로드](loading-dataset-schema-information-from-xml.md)
- [데이터 집합에서 XML 사용](using-xml-in-a-dataset.md)
- [DataSet, DataTable 및 DataView](index.md)
- [ADO.NET 개요](../ado-net-overview.md)
