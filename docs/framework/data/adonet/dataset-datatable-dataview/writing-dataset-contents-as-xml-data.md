---
title: 데이터 세트 콘텐츠를 XML 데이터로 작성
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: fd15f8a5-3b4c-46d0-a561-4559ab2a4705
ms.openlocfilehash: 9a63e79b2fce137ba9d21db861850a471cb42b9f
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71833961"
---
# <a name="writing-dataset-contents-as-xml-data"></a>데이터 세트 콘텐츠를 XML 데이터로 작성
ADO.NET에서는 해당 스키마의 사용 여부와 관계없이 <xref:System.Data.DataSet>을 XML 표현으로 작성할 수 있습니다. 스키마 정보가 XML과 함께 인라인에 포함된 경우에는 XSD(XML 스키마 정의 언어)를 사용하여 작성됩니다. 이 스키마에는 <xref:System.Data.DataSet>의 테이블 정의와 관계 및 제약 조건 정의가 포함됩니다.  
  
 <xref:System.Data.DataSet>이 XML 데이터로 작성되면 <xref:System.Data.DataSet>의 행은 자신의 현재 버전으로 작성됩니다. 그러나 <xref:System.Data.DataSet>은 DiffGram으로 작성될 수도 있으므로 행의 현재 및 원래 값이 모두 포함됩니다.  
  
 @No__t-0의 XML 표현은 파일, 스트림, **XmlWriter**또는 문자열에 쓸 수 있습니다. 이와 같이 다양한 작성이 가능하므로 <xref:System.Data.DataSet>의 XML 표현을 전송하는 방법은 매우 유연합니다. @No__t-0의 XML 표현을 문자열로 가져오려면 다음 예제와 같이 **GetXml** 메서드를 사용 합니다.  
  
```vb  
Dim xmlDS As String = custDS.GetXml()  
```  
  
```csharp  
string xmlDS = custDS.GetXml();  
```  
  
 **GetXml** 는 스키마 정보가 없는 <xref:System.Data.DataSet>의 XML 표현을 반환 합니다. @No__t-0 (XML 스키마)에서 문자열로 스키마 정보를 쓰려면 **Getxmlschema**를 사용 합니다.  
  
 파일, 스트림 또는 **XmlWriter**에 <xref:System.Data.DataSet>을 쓰려면 **WriteXml** 메서드를 사용 합니다. **WriteXml** 에 전달 하는 첫 번째 매개 변수는 XML 출력의 대상입니다. 예를 들어, 파일 이름, **시스템. i n i** . **XmlWriteMode** 의 선택적인 두 번째 매개 변수를 전달 하 여 XML 출력을 작성 하는 방법을 지정할 수 있습니다.  
  
 다음 표에서는 **XmlWriteMode**에 대 한 옵션을 보여 줍니다.  
  
|XmlWriteMode 옵션|설명|  
|-------------------------|-----------------|  
|**IgnoreSchema**|<xref:System.Data.DataSet>의 현재 내용을 XML 스키마 없이 XML 데이터로 작성합니다. 이 값이 기본값입니다.|  
|**WriteSchema**|<xref:System.Data.DataSet>의 현재 내용을 인라인 XML 스키마와 동일한 관계형 구조를 가진 XML 데이터로 작성합니다.|  
|**DiffGram**|원래 및 현재 값을 포함하여 전체 <xref:System.Data.DataSet>을 DiffGram으로 작성합니다. 자세한 내용은 [diffgram](diffgrams.md)를 참조 하세요.|  
  
 **DataRelation** 개체가 포함 된 <xref:System.Data.DataSet>의 XML 표현을 작성 하는 경우 결과 xml에서 각 관계의 자식 행을 관련 부모 요소 내에 중첩 시킬 수 있습니다. 이를 수행 하려면 <xref:System.Data.DataSet>에 **datarelation** 을 추가할 때 **datarelation** 의 **Nested** 속성을 **true** 로 설정 합니다. 자세한 내용은 [중첩 Datarelation](nesting-datarelations.md)합니다.  
  
 다음은 파일에 <xref:System.Data.DataSet>의 XML 표현을 작성 하는 방법에 대 한 두 가지 예입니다. 첫 번째 예에서는 결과 XML의 파일 이름을 **WriteXml**에 문자열로 전달 합니다. 두 번째 예제에서는 **system.object** 를 전달 합니다.
  
```vb  
custDS.WriteXml("Customers.xml", XmlWriteMode.WriteSchema)  
```  
  
```csharp  
custDS.WriteXml("Customers.xml", XmlWriteMode.WriteSchema);  
```  
  
```vb  
Dim xmlSW As System.IO.StreamWriter = New System.IO.StreamWriter("Customers.xml")  
custDS.WriteXml(xmlSW, XmlWriteMode.WriteSchema)  
xmlSW.Close()  
```  
  
```csharp  
System.IO.StreamWriter xmlSW = new System.IO.StreamWriter("Customers.xml");  
custDS.WriteXml(xmlSW, XmlWriteMode.WriteSchema);  
xmlSW.Close();  
```  
  
## <a name="mapping-columns-to-xml-elements-attributes-and-text"></a>열을 XML 요소, 특성 및 텍스트에 매핑  
 **DataColumn** 개체의 **ColumnMapping** 속성을 사용 하 여 XML에서 테이블의 열을 표현 하는 방법을 지정할 수 있습니다. 다음 표에서는 테이블 열의 **ColumnMapping** 속성과 결과 XML에 대 한 다양 한 **mappingtype.attribute** 값을 보여 줍니다.  
  
|MappingType 값|설명|  
|-----------------------|-----------------|  
|**요소**|이 값이 기본값입니다. 열이 XML 요소로 작성되며, 이 때 ColumnName이 요소의 이름이 되고 열의 내용은 요소의 텍스트로 작성됩니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.<br /><br /> `<ColumnName>Column Contents</ColumnName>`|  
|**특성**|열이 현재 행에 대한 XML 요소의 XML 특성으로 작성되며, 이 때 특성의 이름은 ColumnName이며 열의 내용은 특성의 값으로 작성됩니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.<br /><br /> `<RowElement ColumnName="Column Contents" />`|  
|**SimpleContent**|열의 내용이 현재 행에 대한 XML 요소의 텍스트로 작성됩니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.<br /><br /> `<RowElement>Column Contents</RowElement>`<br /><br /> **요소** 열 또는 중첩 관계가 있는 테이블의 열에는 **SimpleContent** 를 설정할 수 없습니다.|  
|**숨김**|열이 XML 출력으로 작성되지 않습니다.|  
  
## <a name="see-also"></a>참조

- [데이터 세트에서 XML 사용](using-xml-in-a-dataset.md)
- [DiffGram](diffgrams.md)
- [DataRelation 중첩](nesting-datarelations.md)
- [데이터 세트 스키마 정보를 XSD로 작성](writing-dataset-schema-information-as-xsd.md)
- [DataSets, DataTables 및 DataViews](index.md)
- [ADO.NET 개요](../ado-net-overview.md)
