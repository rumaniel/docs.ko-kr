---
title: 데이터 세트 및 XmlDataDocument 동기화
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 0ce3793d-54b2-47e4-8cf7-b0591cc4dd21
ms.openlocfilehash: e76e81153cb7d074fe975744c6b6041ee04be90f
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70785421"
---
# <a name="dataset-and-xmldatadocument-synchronization"></a>데이터 세트 및 XmlDataDocument 동기화
ADO.NET <xref:System.Data.DataSet>으로 데이터의 관계형 표현을 사용할 수 있습니다. 계층적으로 데이터에 액세스하기 위해 .NET Framework에서 사용 가능한 XML 클래스를 사용할 수 있습니다. 지금까지는 데이터의 이와 같은 두 가지 표현이 별도로 사용되어 왔습니다. 그러나 .NET Framework를 사용 하면 데이터 **집합** 개체와 <xref:System.Xml.XmlDataDocument> 개체를 통해 각각 관계형 및 계층적 데이터 표현에 대 한 실시간 동기 액세스를 사용할 수 있습니다.  
  
 **데이터 집합이** **XmlDataDocument**와 동기화 되 면 두 개체가 모두 단일 데이터 집합을 사용 합니다. 즉, **데이터 집합이**변경 되 면 변경 내용이 **XmlDataDocument**적용 되 고 그 반대의 경우도 마찬가지입니다. 데이터 집합과 **XmlDataDocument** 간의 관계는 단일 데이터 집합을 사용 하 여 단일 응용 프로그램에서 데이터 **집합** 을 기반으로 하는 전체 서비스 모음 (예: Web Forms 및 Windows Forms 컨트롤, Visual Studio .NET 디자이너) 뿐만 아니라 XSL (Extensible Stylesheet Language), XSLT (XSL 변환) 및 XPath (XML Path Language)를 비롯 한 XML 서비스 모음입니다. 두 서비스를 모두 사용할 수 있으므로 애플리케이션의 대상이 될 서비스 집합을 선택할 필요도 없습니다.  
  
 **데이터 집합** 을 **XmlDataDocument**와 동기화 하는 방법에는 여러 가지가 있습니다. 다음을 할 수 있습니다.  
  
- 스키마 (즉, 관계형 구조)와 데이터를 사용 하 여 데이터 **집합** 을 채운 다음 새 **XmlDataDocument**와 동기화 합니다. 이렇게 하면 기존 관계형 데이터를 계층적으로 표시할 수 있습니다. 예를 들어:  
  
    ```vb  
    Dim dataSet As DataSet = New DataSet  
  
    ' Add code here to populate the DataSet with schema and data.  
  
    Dim xmlDoc As XmlDataDocument = New XmlDataDocument(dataSet)  
    ```  
  
    ```csharp  
    DataSet dataSet = new DataSet();  
  
    // Add code here to populate the DataSet with schema and data.  
  
    XmlDataDocument xmlDoc = new XmlDataDocument(dataSet);  
    ```  
  
- 스키마만 포함 하는 **데이터 집합** (예: 강력한 형식의 **데이터 집합**)을 채운 다음 **XMLDATADOCUMENT**와 동기화 하 고 XML 문서에서 **XmlDataDocument** 을 로드 합니다. 이렇게 하면 기존 계층적 데이터를 관계형으로 표시할 수 있습니다. **데이터 집합** 스키마의 테이블 이름과 열 이름은 함께 동기화 할 XML 요소의 이름과 일치 해야 합니다. 이 때 대/소문자도 일치해야 합니다.  
  
     **데이터 집합** 의 스키마는 관계형 보기에 노출할 XML 요소와만 일치 해야 합니다. 이렇게 하면 XML 문서는 아주 크게, 이 문서의 관계형 "창"은 매우 작게 만들 수 있습니다. **XmlDataDocument** 는 **데이터 집합이** 작은 부분만 노출 하는 경우에도 전체 XML 문서를 유지 합니다. 이에 대 한 자세한 예제는 [데이터 집합을 XmlDataDocument와 동기화](synchronizing-a-dataset-with-an-xmldatadocument.md)를 참조 하세요.  
  
     다음 코드 예제에서는 **데이터 집합** 을 만들고 해당 스키마를 채운 다음 **XmlDataDocument**와 동기화 하는 단계를 보여 줍니다. **데이터 집합** 스키마는 **데이터 집합**을 사용 하 여 노출 하려는 **XmlDataDocument** 의 요소만 일치 해야 합니다.  
  
    ```vb  
    Dim dataSet As DataSet = New DataSet  
  
    ' Add code here to populate the DataSet with schema, but not data.  
  
    Dim xmlDoc As XmlDataDocument = New XmlDataDocument(dataSet)  
    xmlDoc.Load("XMLDocument.xml")  
    ```  
  
    ```csharp  
    DataSet dataSet = new DataSet();  
  
    // Add code here to populate the DataSet with schema, but not data.  
  
    XmlDataDocument xmlDoc = new XmlDataDocument(dataSet);  
    xmlDoc.Load("XMLDocument.xml");  
    ```  
  
     데이터가 포함 된 데이터 **집합과** 동기화 된 경우에는 **XmlDataDocument** 을 로드할 수 없습니다. 로드하는 경우에는 예외가 throw됩니다.  
  
- 새 **XmlDataDocument** 을 만들고 XML 문서에서 로드 한 다음 **XmlDataDocument**의 **DataSet** 속성을 사용 하 여 데이터의 관계형 뷰에 액세스 합니다. 데이터 **집합의** 스키마를 설정 해야 데이터 **집합**을 사용 하 여 **XmlDataDocument** 에서 데이터를 볼 수 있습니다. **데이터 집합** 스키마의 테이블 이름과 열 이름은 함께 동기화 할 XML 요소의 이름과 일치 해야 합니다. 이 때 대/소문자도 일치해야 합니다.  
  
     다음 코드 예제에서는 **XmlDataDocument**에서 데이터의 관계형 뷰에 액세스 하는 방법을 보여 줍니다.  
  
    ```vb  
    Dim xmlDoc As XmlDataDocument = New XmlDataDocument  
    Dim dataSet As DataSet = xmlDoc.DataSet  
  
    ' Add code here to create the schema of the DataSet to view the data.  
  
    xmlDoc.Load("XMLDocument.xml")  
    ```  
  
    ```csharp  
    XmlDataDocument xmlDoc = new XmlDataDocument();  
    DataSet dataSet = xmlDoc.DataSet;  
  
    // Add code here to create the schema of the DataSet to view the data.  
  
    xmlDoc.Load("XMLDocument.xml");  
    ```  
  
 **XmlDataDocument** 를 **DataSet** 과 동기화 하는 또 다른 이점은 XML 문서의 충실도가 유지 된다는 것입니다. 데이터 **집합이** **ReadXml**를 사용 하 여 xml 문서에서 채워지는 경우 **WriteXml** 을 사용 하 여 데이터를 XML 문서로 다시 쓸 때 원래 xml 문서와 크게 다를 수 있습니다. 이는 **데이터 집합이** XML 문서에서 공백 등의 서식 지정 이나 요소 순서와 같은 계층적 정보를 유지 하지 않기 때문입니다. 데이터 **집합은** **데이터 집합**의 스키마와 일치 하지 않기 때문에 무시 된 XML 문서의 요소도 포함 하지 않습니다. **XmlDataDocument** 를 **dataset** 과 동기화 하면 원래 XML 문서의 서식 지정 및 계층 구조 요소 구조가 **XmlDataDocument**에서 유지 되 고 데이터 **집합** 에는 데이터만 포함 됩니다. **데이터 집합**에 적합 한 스키마 정보입니다.  
  
 **데이터 집합** 을 **XmlDataDocument**와 동기화 하는 경우에는 <xref:System.Data.DataRelation> 개체가 중첩 되었는지 여부에 따라 결과가 다를 수 있습니다. 자세한 내용은 [중첩 Datarelation](nesting-datarelations.md)합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [XmlDataDocument로 데이터 세트 동기화](synchronizing-a-dataset-with-an-xmldatadocument.md)  
 **XmlDataDocument**를 사용 하 여 강력한 형식의 **데이터 집합**을 최소 스키마와 동기화 하는 방법을 보여 줍니다.  
  
 [데이터 세트에서 XPath 쿼리 수행](performing-an-xpath-query-on-a-dataset.md)  
 **데이터 집합**의 내용에 대해 XPath 쿼리를 수행 하는 방법을 보여 줍니다.  
  
 [XSLT 변형을 데이터 세트에 적용](applying-an-xslt-transform-to-a-dataset.md)  
 XSLT 변환을 **데이터 집합**의 내용에 적용 하는 방법을 보여 줍니다.  
  
## <a name="related-sections"></a>관련 단원  
 [데이터 집합에서 XML 사용](using-xml-in-a-dataset.md)  
 **Dataset의** 내용을 xml 데이터로 로드 하 고 유지 하는 것을 포함 하 여 데이터 **집합이** xml과 데이터 원본으로 상호 작용 하는 방법을 설명 합니다.  
  
 [DataRelation 중첩](nesting-datarelations.md)  
 **데이터 집합** 의 내용을 XML 데이터로 표현할 때 중첩 된 **DataRelation** 개체의 중요도를 설명 하 고 이러한 관계를 만드는 방법을 설명 합니다.  
  
 [DataSet, DataTable 및 DataView](index.md)  
 **데이터 집합** 및 데이터 집합을 사용 하 여 응용 프로그램 데이터를 관리 하 고 관계형 데이터베이스 및 XML을 비롯 한 데이터 원본과 상호 작용 하는 방법에 대해 설명 합니다.  
  
 <xref:System.Xml.XmlDataDocument>  
 **XmlDataDocument** 클래스에 대 한 참조 정보를 포함 합니다.  
  
## <a name="see-also"></a>참고자료

- [ADO.NET 개요](../ado-net-overview.md)
