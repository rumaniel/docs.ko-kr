---
title: DataTables
ms.date: 03/30/2017
ms.assetid: 52ff0e32-3e5a-41de-9a3b-7b04ea52b83e
ms.openlocfilehash: 12255f738dea0a4713389e599468d1a7fab67d23
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784698"
---
# <a name="datatables"></a>DataTables
<xref:System.Data.DataSet>은 테이블 컬렉션, 관계 및 제약 조건으로 구성되어 있습니다. ADO.NET <xref:System.Data.DataTable> 에서 개체는 **데이터 집합**의 테이블을 나타내는 데 사용 됩니다. **DataTable** 은 메모리 내 관계형 데이터의 한 테이블을 나타냅니다. 데이터는에 대해 로컬입니다. 이 파일이 상주 하지만 **dataadapter** 를 사용 하 여 Microsoft SQL Server와 같은 데이터 소스에서 채워질 수 있는 NET 기반 응용 프로그램 자세한 내용은 [Dataadapter에서 데이터 집합 채우기](../populating-a-dataset-from-a-dataadapter.md)를 참조 하세요.  
  
 **DataTable** 클래스는 .NET Framework 클래스 라이브러리 내에서 **system.xml 네임 스페이스** 의 멤버입니다. **Datatable** 은 독립적으로 만들거나 **데이터 집합**의 멤버로 사용할 수 있으며,를 <xref:System.Data.DataView>비롯 한 다른 .NET Framework 개체와 함께 **datatable** 개체를 사용할 수도 있습니다. **Dataset 개체의** **tables** 속성을 통해 **데이터 집합** 의 테이블 컬렉션에 액세스할 수 있습니다.  
  
 테이블의 스키마나 구조는 열이나 제약 조건에 의해 표시됩니다. <xref:System.Data.ForeignKeyConstraint> 및 <xref:System.Data.DataColumn> 개체뿐만아니라개체를사용하여DataTable의스키마를정의<xref:System.Data.UniqueConstraint> 합니다. 테이블 열은 데이터 소스 열에 매핑될 수 있습니다. 또한 이 열은 식에서 계산된 값을 포함하며 값을 자동으로 증가시키고 기본 키 값을 포함할 수 있습니다.  
  
 스키마 외에도 **DataTable** 에는 데이터를 포함 하 고 주문 하는 행이 있어야 합니다. <xref:System.Data.DataRow> 클래스는 테이블에 포함된 실제 데이터를 나타냅니다. **DataRow** 와 해당 속성 및 메서드를 사용 하 여 테이블의 데이터를 검색, 평가 및 조작할 수 있습니다. 행 내에서 데이터를 액세스 하 고 변경할 때 **DataRow** 개체는 현재 상태와 원래 상태를 유지 합니다.  
  
 테이블에서 하나 이상의 관련 열을 사용하면 테이블 간에 부모-자식 관계를 만들 수 있습니다. 을<xref:System.Data.DataRelation>사용 하 여 **DataTable** 개체 간의 관계를 만듭니다. 그런 다음 **DataRelation** 개체를 사용 하 여 특정 행의 관련 자식 또는 부모 행을 반환할 수 있습니다. 자세한 내용은 [DataRelations 추가](adding-datarelations.md)를 참조 하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
 [DataTable 만들기](creating-a-datatable.md)  
 **DataTable** 을 만들어 **데이터 집합**에 추가 하는 방법을 설명 합니다.  
  
 [DataTable 스키마 정의](datatable-schema-definition.md)  
 **DataColumn** 개체 및 제약 조건을 만들고 사용 하는 방법에 대 한 정보를 제공 합니다.  
  
 [DataTable에서 데이터 조작](manipulating-data-in-a-datatable.md)  
 테이블에서 데이터를 추가, 수정 및 삭제하는 방법에 대해 설명합니다. **DataTable** 이벤트를 사용 하 여 테이블의 데이터에 대 한 변경 내용을 검사 하는 방법을 설명 합니다.  
  
 [DataTable 이벤트 처리](handling-datatable-events.md)  
 열 값을 수정 하 고 행을 추가 하거나 삭제할 때 이벤트를 비롯 하 여 **DataTable**과 함께 사용할 수 있는 이벤트에 대 한 정보를 제공 합니다.  
  
## <a name="related-sections"></a>관련 단원  
 [ADO.NET](../index.md)  
 ADO.NET 아키텍처 및 구성 요소에 대해 설명하고, 이를 사용하여 기존 데이터 소스에 액세스하고 애플리케이션 데이터를 관리하는 방법을 설명합니다.  
  
 [DataSet, DataTable 및 DataView](index.md)  
 테이블 간의 관계를 만드는 방법을 포함 하 여 ADO.NET **데이터 집합** 에 대 한 정보를 제공 합니다.  
  
 <xref:System.Data.Constraint>  
 **제약 조건** 개체에 대 한 참조 정보를 제공 합니다.  
  
 <xref:System.Data.DataColumn>  
 **DataColumn** 개체에 대 한 참조 정보를 제공 합니다.  
  
 <xref:System.Data.DataSet>  
 **DataSet** 개체에 대 한 참조 정보를 제공 합니다.  
  
 <xref:System.Data.DataTable>  
 **DataTable** 개체에 대 한 참조 정보를 제공 합니다.  
  
 [클래스 라이브러리 개요](../../../../standard/class-library-overview.md)  
 **시스템** 네임 스페이스 뿐만 아니라 두 번째 수준 네임 스페이스인 **system.object**를 포함 하 여 .NET Framework 클래스 라이브러리에 대 한 개요를 제공 합니다.  
  
## <a name="see-also"></a>참고자료

- [ADO.NET 개요](../ado-net-overview.md)
