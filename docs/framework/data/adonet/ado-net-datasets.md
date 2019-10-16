---
title: ADO.NET 데이터 집합
ms.date: 03/30/2017
ms.assetid: 82b641bb-6001-4512-bf1a-2830acdd92ab
ms.openlocfilehash: acbe5a549539a77d63332687486cbe8744592f8b
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70786981"
---
# <a name="adonet-datasets"></a>ADO.NET 데이터 집합
이 <xref:System.Data.DataSet> 개체는 ADO.NET를 사용 하 여 연결이 끊어진 분산 데이터 시나리오를 지 원하는 데 중요 합니다. 데이터 **집합** 은 데이터 원본에 관계 없이 일관 된 관계형 프로그래밍 모델을 제공 하는 데이터의 메모리 상주 표현입니다. 이 개체는 다양한 여러 데이터 소스에 사용하거나 XML 데이터에 사용할 수 있을 뿐 아니라 이 개체를 사용하여 응용 프로그램의 로컬 데이터를 관리할 수도 있습니다. 데이터 **집합** 은 관련 테이블, 제약 조건 및 테이블 간의 관계를 포함 하 여 전체 데이터 집합을 나타냅니다. 다음 그림에서는 **데이터 집합** 개체 모델을 보여 줍니다.  
  
 ![ADO.Net graphic](./media/ado-1-bpuedev11.png "ado_1_bpuedev11")  
DataSet 개체 모델  
  
 **데이터 집합** 의 메서드와 개체는 관계형 데이터베이스 모델의 메서드와 일치 합니다.  
  
 **데이터 집합** 은 해당 콘텐츠를 xml로 유지 하 고 해당 스키마를 XSD (xml 스키마 정의 언어) 스키마로 다시 로드할 수도 있습니다. 자세한 내용은 [데이터 세트에서 XML 사용](./dataset-datatable-dataview/using-xml-in-a-dataset.md)을 참조하세요.  
  
## <a name="the-datatablecollection"></a>DataTableCollection  
 ADO.NET **데이터 집합** 은 <xref:System.Data.DataTable> 개체가 나타내는 0 개 이상의 테이블 컬렉션을 포함 합니다. 에 <xref:System.Data.DataTableCollection> 는 **데이터 집합**의 모든 **DataTable** 개체가 포함 되어 있습니다.  
  
 **DataTable** 은 <xref:System.Data> 네임 스페이스에 정의 되며 메모리 상주 데이터의 단일 테이블을 나타냅니다. 여기에는 <xref:System.Data.DataColumnCollection>에 의해 표현되는 열의 컬렉션과 <xref:System.Data.ConstraintCollection>에 의해 표현되는 제약 조건의 컬렉션이 포함됩니다. 이 두 컬렉션은 테이블의 스키마를 정의합니다. **DataTable** 에는 <xref:System.Data.DataRowCollection>테이블의 데이터를 포함 하는가 나타내는 행의 컬렉션도 포함 됩니다. 이와 함께 <xref:System.Data.DataRow>는 현재 버전과 원래 버전을 모두 보유하므로 행에 저장된 값에 대한 변경 사항을 식별할 수 있습니다.  
  
## <a name="the-dataview-class"></a>DataView 클래스  
 <xref:System.Data.DataView>는 데이터 바인딩 응용 프로그램에서 자주 사용되는 기능으로, 이 기능을 사용하면 <xref:System.Data.DataTable>에 저장되어 있는 데이터에 대해 서로 다른 뷰를 만들 수 있습니다. <xref:System.Data.DataView>를 사용하면 테이블의 데이터를 여러 정렬 순서로 노출시킬 수 있으며 행 상태에 따라 또는 필터 식을 기준으로 데이터를 필터링할 수 있습니다. 자세한 내용은 [Dataview](./dataset-datatable-dataview/dataviews.md)합니다.  
  
## <a name="the-datarelationcollection"></a>DataRelationCollection  
 **데이터 집합** 은 해당 <xref:System.Data.DataRelationCollection> 개체의 관계를 포함 합니다. <xref:System.Data.DataRelation> 개체로 표시 되는 관계는 한 **datatable** 의 행을 다른 **datatable**의 행과 연결 합니다. 이 관계는 관계형 데이터베이스의 기본 키 열과 외래 키 열 간에 존재하는 조인 경로와 유사합니다. **DataRelation** 은 **데이터 집합**의 두 테이블에서 일치 하는 열을 식별 합니다.  
  
 관계는 **데이터 집합**의 한 테이블에서 다른 테이블로의 탐색을 가능 하 게 합니다. **DataRelation** 의 필수 요소는 관계의 이름, 관련 되는 테이블의 이름 및 각 테이블에 있는 관련 열입니다. <xref:System.Data.DataColumn> 개체의 배열을 키 열로 지정하면 테이블당 두 개 이상의 열에 대한 관계를 빌드할 수 있습니다. 에 <xref:System.Data.DataRelationCollection>관계를 추가 하는 경우 필요에 따라 **UniqueKeyConstraint** 및 **ForeignKeyConstraint** 를 추가 하 여 관련 열 값이 변경 될 때 무결성 제약 조건을 적용할 수 있습니다.  
  
 자세한 내용은 [DataRelations 추가](./dataset-datatable-dataview/adding-datarelations.md)를 참조 하세요.  
  
## <a name="xml"></a>XML  
 XML 스트림 또는 문서에서 **데이터 집합** 을 채울 수 있습니다. XML 스트림이나 문서를 사용 하 여 데이터, 스키마 정보 또는 두 가지 모두를 데이터 **집합** 에 제공할 수 있습니다. XML 스트림이나 문서에서 제공 되는 정보를 데이터 **집합**에 이미 있는 기존 데이터 나 스키마 정보와 결합할 수 있습니다. 자세한 내용은 [데이터 세트에서 XML 사용](./dataset-datatable-dataview/using-xml-in-a-dataset.md)을 참조하세요.  
  
## <a name="extendedproperties"></a>ExtendedProperties  
 **DataSet**, **DataTable**및 **DataColumn** 은 모두 **extendedproperties** 속성을 가집니다. **Extendedproperties** 는 결과 집합을 생성 하는 데 사용 된 SELECT 문 또는 데이터가 생성 된 시간 등의 사용자 지정 정보를 저장할 수 있는 **PropertyCollection** 입니다. **Extendedproperties** 컬렉션은 **데이터 집합**에 대 한 스키마 정보와 함께 유지 됩니다.  
  
## <a name="linq-to-dataset"></a>LINQ to DataSet  
 LINQ to DataSet는 데이터 집합에 저장 된 연결 되지 않은 데이터에 대 한 언어 통합 쿼리 기능을 제공 합니다. LINQ to DataSet는 표준 [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] 구문을 사용 하 고 Visual Studio IDE를 사용 하는 경우 컴파일 시간 구문 검사, 정적 입력 및 IntelliSense 지원을 제공 합니다.  
  
 자세한 내용은 [LINQ to DataSet](linq-to-dataset.md)을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- [ADO.NET 개요](ado-net-overview.md)
- [DataSet, DataTable 및 DataView](./dataset-datatable-dataview/index.md)
- [ADO.NET에서 데이터 검색 및 수정](retrieving-and-modifying-data.md)
