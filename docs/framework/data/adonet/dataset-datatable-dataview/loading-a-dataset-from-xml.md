---
title: XML에서 데이터 세트 로드
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 49c083b7-a5ed-41cf-aabc-5aaba96f00e6
ms.openlocfilehash: 4c8b26651a1f4050145b6d43e03f9d4cc3d68202
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70785284"
---
# <a name="loading-a-dataset-from-xml"></a>XML에서 데이터 세트 로드
ADO.NET <xref:System.Data.DataSet>의 내용은 XML 스트림이나 문서로부터 만들 수 있습니다. 또한, .NET Framework를 사용하면 XML로부터 로드할 정보와 <xref:System.Data.DataSet>의 스키마나 관계형 구조를 만드는 방법을 매우 융통성 있게 선택할 수 있습니다.  
  
 XML의 데이터로 <xref:System.Data.DataSet> 를 채우려면 <xref:System.Data.DataSet> 개체의 **ReadXml** 메서드를 사용 합니다. **ReadXml** 메서드는 파일, 스트림 또는 **XMLREADER**에서 읽고 XML 소스와 선택적 **XmlReadMode** 인수를 인수로 사용 합니다. **XmlReader**에 대 한 자세한 내용은 [XmlTextReader를 사용 하 여 XML 데이터 읽기](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/tfz3cz6w(v=vs.100))를 참조 하세요. **ReadXml** 메서드는 XML 스트림이나 문서의 내용을 읽고를 <xref:System.Data.DataSet> 사용 하 여 데이터를 로드 합니다. 또한 관계형 스키마가 이미 있는지 여부에 <xref:System.Data.DataSet> 따라 지정 된 **XmlReadMode** 에 따라의 관계형 스키마를 만듭니다.  
  
 다음 표에서는 **XmlReadMode** 인수에 대 한 옵션을 설명 합니다.  
  
|옵션|설명|  
|------------|-----------------|  
|**자동**|기본값입니다. XML을 검사하고 다음 순서에 따라 가장 적합한 옵션을 선택합니다.<br /><br /> -XML이 DiffGram 인 경우 **diffgram** 이 사용 됩니다.<br />-에 <xref:System.Data.DataSet> 스키마가 포함 되어 있거나 XML에 인라인 스키마가 포함 되어 있으면 **readschema** 가 사용 됩니다.<br />-에 <xref:System.Data.DataSet> 스키마가 없고 XML에 인라인 스키마가 포함 되어 있지 않으면 **InferSchema** 가 사용 됩니다.<br /><br /> 읽을 XML의 형식을 알고 있는 경우 최상의 성능을 위해 **자동** 기본값을 허용 하는 대신 명시적 **XmlReadMode**를 설정 하는 것이 좋습니다.|  
|**ReadSchema**|모든 인라인 스키마를 읽은 다음 데이터와 스키마를 로드합니다.<br /><br /> <xref:System.Data.DataSet>에 이미 스키마가 있으면 인라인 스키마의 새 테이블이 <xref:System.Data.DataSet>에 있는 기존 스키마에 추가됩니다. 인라인 스키마의 모든 테이블이 <xref:System.Data.DataSet>에 이미 있으면 예외가 throw됩니다. **XmlReadMode 스키마**를 사용 하 여 기존 테이블의 스키마를 수정할 수 없습니다.<br /><br /> <xref:System.Data.DataSet>에 스키마도 없고 인라인 스키마도 없으면 데이터를 읽지 않습니다.<br /><br /> 인라인 스키마는 XSD(XML 스키마 정의 언어) 스키마를 사용하여 정의할 수 있습니다. 인라인 스키마를 XML 스키마로 작성 하는 방법에 대 한 자세한 내용은 [Xml 스키마에서 데이터 집합 관계형 구조 파생 (XSD)](deriving-dataset-relational-structure-from-xml-schema-xsd.md)을 참조 하세요.|  
|**IgnoreSchema**|모든 인라인 스키마를 무시하고 데이터를 기존 <xref:System.Data.DataSet> 스키마로 로드합니다. 기존 스키마와 일치하지 않는 모든 데이터는 삭제됩니다. <xref:System.Data.DataSet>에 스키마가 없으면 데이터를 로드하지 않습니다.<br /><br /> 데이터가 DiffGram 인 경우 **IgnoreSchema** 는 **diffgram** 과 동일한 기능을 갖습니다 *.*|  
|**InferSchema**|모든 인라인 스키마를 무시하며 XML 데이터의 구조마다 스키마를 유추한 다음 데이터를 로드합니다.<br /><br /> <xref:System.Data.DataSet>에 이미 스키마가 있으면 기존 테이블에 열을 추가하여 현재 스키마를 확장합니다. 기존 테이블이 없으면 테이블이 추가되지 않습니다. 유추된 테이블이 다른 네임스페이스로 이미 존재하거나 유추된 열이 기존 열과 충돌하면 예외가 throw됩니다.<br /><br /> **Readxmlschema** 에서 xml 문서의 스키마를 유추 하는 방법에 대 한 자세한 내용은 [Xml에서 데이터 집합 관계형 구조 유추](inferring-dataset-relational-structure-from-xml.md)를 참조 하세요.|  
|**DiffGram**|DiffGram을 읽은 다음 해당 데이터를 현재 스키마에 추가합니다. **DiffGram** 은 고유 식별자 값이 일치 하는 기존 행과 새 행을 병합 합니다. 이 항목의 맨 뒤에 나오는 "XML로부터 데이터 병합"을 참조하세요. Diffgram에 대 한 자세한 내용은 [diffgram](diffgrams.md)를 참조 하세요.|  
|**Don't**|스트림의 끝에 도달할 때까지 여러 개의 XML 조각을 계속 읽습니다. <xref:System.Data.DataSet> 스키마에 일치하는 조각이 해당 테이블의 뒤에 추가됩니다. <xref:System.Data.DataSet> 스키마에 일치하지 않는 조각은 삭제됩니다.|  
  
> [!NOTE]
> XML 문서로 배치 된 **ReadXml** 에 **XmlReader** 를 전달 하는 경우 **ReadXml** 는 다음 요소 노드를 읽고이를 루트 요소로 처리 하 여 요소 노드 끝 까지만 읽습니다. **XmlReadMode**를 지정 하는 경우에는 적용 되지 않습니다.  
  
## <a name="dtd-entities"></a>DTD 엔터티  
 XML이 DTD (문서 종류 정의) 스키마에 정의 된 엔터티를 포함 하는 경우 파일 이름, 스트림 또는 유효성 검사를 수행 <xref:System.Data.DataSet> 하지 않는 **XmlReader** 를 **ReadXml**에 전달 하 여를 로드 하려고 하면 예외가 throw 됩니다. 대신 **Entityhandling** 을 **entityhandling.expandentities**로 설정 하 여 **XmlValidatingReader**를 만들고 **XmlValidatingReader** 를 **ReadXml**에 전달 해야 합니다. **XmlValidatingReader** 는에서 읽기 <xref:System.Data.DataSet>전에 엔터티를 확장 합니다.  
  
 다음 코드 예제에서는 XML 스트림으로부터 <xref:System.Data.DataSet>을 로드하는 방법을 보여 줍니다. 첫 번째 예제에서는 **ReadXml** 메서드에 전달 되는 파일 이름을 보여 줍니다. 두 번째 예제에서는 <xref:System.IO.StringReader>를 사용하여 로드될 XML이 포함된 문자열을 보여 줍니다.  
  
```vb  
Dim dataSet As DataSet = New DataSet  
dataSet.ReadXml("input.xml", XmlReadMode.ReadSchema)  
```  
  
```csharp  
DataSet dataSet = new DataSet();  
dataSet.ReadXml("input.xml", XmlReadMode.ReadSchema);  
```  
  
```vb  
Dim dataSet As DataSet = New DataSet  
Dim dataTable As DataTable = New DataTable("table1")  
dataTable.Columns.Add("col1", Type.GetType("System.String"))  
dataSet.Tables.Add(dataTable)  
  
Dim xmlData As String = "<XmlDS><table1><col1>Value1</col1></table1><table1><col1>Value2</col1></table1></XmlDS>"  
  
Dim xmlSR As System.IO.StringReader = New System.IO.StringReader(xmlData)  
  
dataSet.ReadXml(xmlSR, XmlReadMode.IgnoreSchema)  
```  
  
```csharp  
DataSet dataSet = new DataSet();  
DataTable dataTable = new DataTable("table1");  
dataTable.Columns.Add("col1", typeof(string));  
dataSet.Tables.Add(dataTable);  
  
string xmlData = "<XmlDS><table1><col1>Value1</col1></table1><table1><col1>Value2</col1></table1></XmlDS>";  
  
System.IO.StringReader xmlSR = new System.IO.StringReader(xmlData);  
  
dataSet.ReadXml(xmlSR, XmlReadMode.IgnoreSchema);  
```  
  
> [!NOTE]
> **ReadXml** 를 호출 하 여 매우 큰 파일을 로드 하는 경우 성능이 저하 될 수 있습니다. **ReadXml**에 대 한 최상의 성능을 보장 하려면의 <xref:System.Data.DataTable.BeginLoadData%2A> <xref:System.Data.DataSet>각 테이블에 대해 메서드를 호출한 다음 **ReadXml**를 호출 합니다. 마지막으로 다음 예제와 같이 <xref:System.Data.DataTable.EndLoadData%2A>의 각 테이블에 대해 <xref:System.Data.DataSet>를 호출합니다.  
  
```vb  
Dim dataTable As DataTable  
  
For Each dataTable In dataSet.Tables  
   dataTable.BeginLoadData()  
Next  
  
dataSet.ReadXml("file.xml")  
  
For Each dataTable in dataSet.Tables  
   dataTable.EndLoadData()  
Next  
```  
  
```csharp  
foreach (DataTable dataTable in dataSet.Tables)  
   dataTable.BeginLoadData();  
  
dataSet.ReadXml("file.xml");   
  
foreach (DataTable dataTable in dataSet.Tables)  
   dataTable.EndLoadData();  
```  
  
> [!NOTE]
> 의 <xref:System.Data.DataSet> XSD 스키마에 **targetNamespace**가 포함 된 경우 데이터를 읽을 수 없으며 **ReadXml** 를 호출 하 여 정규화 된 네임 스페이스가 없는 요소가 포함 된 XML <xref:System.Data.DataSet> 로를 로드 하는 경우 예외가 발생할 수 있습니다. 이 경우 정규화 되지 않은 요소를 읽으려면 XSD 스키마에서 **Elementformdefault** 를 "정규화 된"로 설정 합니다. 예:  
  
```xml  
<xsd:schema id="customDataSet"   
  elementFormDefault="qualified"  
  targetNamespace="http://www.tempuri.org/customDataSet.xsd"   
  xmlns="http://www.tempuri.org/customDataSet.xsd"   
  xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
  xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
</xsd:schema>  
```  
  
## <a name="merging-data-from-xml"></a>XML로부터 데이터 병합  
 <xref:System.Data.DataSet>에 데이터가 이미 있으면 XML의 새 데이터는 <xref:System.Data.DataSet>에 이미 있는 데이터에 추가됩니다. **ReadXml** 는 XML에서 기본 키가 일치 하 <xref:System.Data.DataSet> 는 행 정보로 병합 되지 않습니다. 기존 행 정보를 XML의 새 정보로 덮어쓰려면 **ReadXml** 를 사용 <xref:System.Data.DataSet>하 여 새를 만든 다음 <xref:System.Data.DataSet.Merge%2A> 새 <xref:System.Data.DataSet> 를 기존 <xref:System.Data.DataSet>에 만듭니다. **Diffgram** **XmlReadMode** 를 사용 하 여 **ReadXML** 를 사용 하 여 diffgram을 로드 하면 동일한 고유 식별자를 가진 행이 병합 됩니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Data.DataSet.Merge%2A?displayProperty=nameWithType>
- [데이터 집합에서 XML 사용](using-xml-in-a-dataset.md)
- [DiffGram](diffgrams.md)
- [XML 스키마에서 데이터 세트 관계형 구조 파생(XSD)](deriving-dataset-relational-structure-from-xml-schema-xsd.md)
- [XML에서 데이터 세트 관계형 구조 유추](inferring-dataset-relational-structure-from-xml.md)
- [XML에서 데이터 세트 스키마 정보 로드](loading-dataset-schema-information-from-xml.md)
- [DataSet, DataTable 및 DataView](index.md)
- [ADO.NET 개요](../ado-net-overview.md)
