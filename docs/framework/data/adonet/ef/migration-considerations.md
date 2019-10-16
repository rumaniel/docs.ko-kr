---
title: 마이그레이션 고려 사항(Entity Framework)
ms.date: 03/30/2017
ms.assetid: c85b6fe8-cc32-4642-8f0a-dc0e5a695936
ms.openlocfilehash: e3e4caf79c1e75708e266e625a4271bc0c90747b
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854427"
---
# <a name="migration-considerations-entity-framework"></a>마이그레이션 고려 사항(Entity Framework)
ADO.NET Entity Framework는 기존 응용 프로그램에 몇 가지 이점을 제공 합니다. 가장 중요한 이점 중 하나는 개념적 모델을 사용하여 응용 프로그램에서 사용되는 데이터 구조를 데이터 소스의 스키마와 구분할 수 있다는 것입니다. 이렇게 하면 응용 프로그램을 적절하게 변경하지 않아도 나중에 저장소 모델이나 데이터 소스 자체를 쉽게 변경할 수 있습니다. Entity Framework 사용의 이점에 대 한 자세한 내용은 [Entity Framework 개요](overview.md) 및 [엔터티 데이터 모델](../entity-data-model.md)를 참조 하세요.  
  
 Entity Framework의 이점을 활용 하기 위해 기존 응용 프로그램을 Entity Framework로 마이그레이션할 수 있습니다. 일부 작업은 마이그레이션되는 모든 응용 프로그램에 공통됩니다. 이러한 일반적인 작업에는 버전 3.5 SP1 (서비스 팩 1)부터 .NET Framework 사용 하도록 응용 프로그램을 업그레이드 하 고, 모델 및 매핑을 정의 하 고, Entity Framework를 구성 하는 작업이 포함 됩니다. 응용 프로그램을 Entity Framework로 마이그레이션하면 적용 되는 추가 고려 사항이 있습니다. 이러한 고려 사항은 마이그레이션되는 응용 프로그램의 종류와 응용 프로그램의 특정 기능에 따라 달라집니다. 이 항목에서는 기존 응용 프로그램을 업그레이드할 때 사용할 최상의 방법을 선택하는 데 유용한 정보를 제공합니다.  
  
## <a name="general-migration-considerations"></a>일반적인 마이그레이션 고려 사항  
 응용 프로그램을 Entity Framework로 마이그레이션할 때는 다음 사항을 고려해 야 합니다.  
  
- 응용 프로그램에서 사용 하는 데이터 원본에 대 한 데이터 공급자가 Entity Framework를 지 원하는 경우 버전 3.5 s p 1부터 .NET Framework를 사용 하는 모든 응용 프로그램을 Entity Framework로 마이그레이션할 수 있습니다.  
  
- 공급자가 Entity Framework를 지원하지만 Entity Framework에서 데이터 소스 공급자의 모든 기능을 지원하지 않을 수도 있습니다.  
  
- 크거나 복잡한 응용 프로그램의 경우 한 번에 전체 응용 프로그램을 Entity Framework로 마이그레이션할 필요는 없습니다. 그러나 데이터 소스가 변경될 경우 Entity Framework를 사용하지 않는 응용 프로그램의 모든 부분을 변경해야 합니다.  
  
- Entity Framework에서 사용 하는 데이터 공급자 연결은 Entity Framework ADO.NET 데이터 공급자를 사용 하 여 데이터 원본에 액세스 하기 때문에 응용 프로그램의 다른 부분과 공유할 수 있습니다. 예를 들어, Entity Framework는 SqlClient 공급자를 사용하여 SQL Server 데이터베이스에 액세스합니다. 자세한 내용은 [Entity Framework에 대 한 EntityClient 공급자](entityclient-provider-for-the-entity-framework.md)를 참조 하세요.  
  
## <a name="common-migration-tasks"></a>일반적인 마이그레이션 작업  
 기존 응용 프로그램을 Entity Framework로 마이그레이션하기 위한 경로는 응용 프로그램 유형과 기존 데이터 액세스 전략 모두에 따라 달라 집니다. 그러나 기존 응용 프로그램을 Entity Framework으로 마이그레이션하는 경우에는 항상 다음 작업을 수행 해야 합니다.  
  
> [!NOTE]
> 이러한 모든 작업은 Visual Studio 2008부터 시작 하는 엔터티 데이터 모델 도구를 사용 하는 경우 자동으로 수행 됩니다. 자세한 내용은 [방법: 엔터티 데이터 모델 마법사](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738677(v=vs.100))를 사용 합니다.  
  
1. 응용 프로그램을 업그레이드합니다.  
  
     이전 버전의 Visual Studio 및 .NET Framework를 사용 하 여 만든 프로젝트는 Visual Studio 2008 s p 1을 사용 하 고 .NET Framework 버전 3.5 s p 1 부터는 업그레이드 해야 합니다.  
  
2. 모델 및 매핑을 정의합니다.  
  
     모델 및 매핑 파일은 개념적 모델의 엔터티, 데이터 소스의 구조(예: 테이블, 저장 프로시저 및 뷰), 엔터티와 데이터 소스 구조 간의 매핑을 정의합니다. 자세한 내용은 [방법: 모델 및 매핑 파일](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb399785(v=vs.100))을 수동으로 정의 합니다.  
  
     저장소 모델에 정의된 형식은 데이터 소스의 개체 이름과 일치해야 합니다. 기존 응용 프로그램에서 데이터를 개체로 노출하는 경우 개념적 모델에 정의된 엔터티 및 속성이 이러한 기존 데이터 클래스 및 속성의 이름과 일치하는지 확인해야 합니다. 자세한 내용은 [방법: 사용자 지정 개체](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738625(v=vs.100))를 사용할 수 있도록 모델링 및 매핑 파일을 사용자 지정 합니다.  
  
    > [!NOTE]
    > 엔터티 데이터 모델 디자이너를 사용하여 개념적 모델의 엔터티 이름을 기존 개체와 일치하도록 바꿀 수 있습니다. 자세한 내용은 [엔터티 데이터 모델 Designer](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/cc716685(v=vs.100))를 참조 하세요.  
  
3. 연결 문자열을 정의합니다.  
  
     Entity Framework는 개념적 모델에 대해 쿼리를 실행할 때 특별 한 형식의 연결 문자열을 사용 합니다. 이 연결 문자열은 모델과 매핑 파일 및 데이터 소스에 대한 연결 정보를 캡슐화합니다. 자세한 내용은 [방법: 연결 문자열](how-to-define-the-connection-string.md)을 정의 합니다.  
  
4. Visual Studio 프로젝트를 구성 합니다.  
  
     Entity Framework 어셈블리와 모델 및 매핑 파일에 대 한 참조는 Visual Studio 프로젝트에 추가 해야 합니다. 이러한 매핑 파일을 프로젝트에 추가하여 연결 문자열에 표시된 위치에 응용 프로그램과 함께 배포되도록 할 수 있습니다. 자세한 내용은 [방법: Entity Framework 프로젝트](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738546(v=vs.100))를 수동으로 구성 합니다.  
  
## <a name="considerations-for-applications-with-existing-objects"></a>기존 개체가 있는 응용 프로그램에 대한 고려 사항  
 .NET Framework 4부터 Entity Framework은 지 속성 무시 개체 라고도 하는 "일반 이전" CLR 개체 (POCO)를 지원 합니다. 대부분의 경우 기존 개체는 사소한 변경을 수행 하 여 Entity Framework 사용할 수 있습니다. 자세한 내용은 [POCO 엔터티 작업](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dd456853(v=vs.100))을 참조 하세요. 응용 프로그램을 Entity Framework로 마이그레이션하고 Entity Framework 도구에서 생성 된 데이터 클래스를 사용할 수도 있습니다. 자세한 내용은 [방법: 엔터티 데이터 모델 마법사](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738677(v=vs.100))를 사용 합니다.  
  
## <a name="considerations-for-applications-that-use-adonet-providers"></a>ADO.NET 공급자를 사용하는 응용 프로그램에 대한 고려 사항  
 SqlClient와 같은 ADO.NET 공급자를 사용 하 여 데이터 원본을 쿼리하여 테이블 형식 데이터를 반환할 수 있습니다. 데이터를 ADO.NET 데이터 집합으로 로드할 수도 있습니다. 다음 목록에서는 기존 ADO.NET 공급자를 사용 하는 응용 프로그램을 업그레이드 하기 위한 고려 사항을 설명 합니다.  
  
- 데이터 판독기를 사용하여 표 형식 데이터 표시  

  EntityClient 공급자를 사용 하 [!INCLUDE[esql](../../../../../includes/esql-md.md)] 여 쿼리를 실행 하 고 반환 <xref:System.Data.EntityClient.EntityDataReader> 된 개체를 열거 하는 것을 고려할 수 있습니다. 응용 프로그램이 데이터 판독기를 사용 하 여 테이블 형식 데이터를 표시 하며 데이터를 개체로 구체화 하 고 변경 내용을 추적 하 고 업데이트 하는 데 Entity Framework에서 제공 하는 기능이 필요 하지 않은 경우에만이 작업을 수행 합니다. 데이터 소스를 업데이트하는 기존 데이터 액세스 코드를 계속 사용할 수 있지만 <xref:System.Data.EntityClient.EntityConnection.StoreConnection%2A>의 <xref:System.Data.EntityClient.EntityConnection> 속성에서 액세스된 기존 연결을 사용할 수도 있습니다. 자세한 내용은 [Entity Framework에 대 한 EntityClient 공급자](entityclient-provider-for-the-entity-framework.md)를 참조 하세요.  
  
- DataSets 사용  

  Entity Framework는 메모리 내 지 속성, 변경 내용 추적, 데이터 바인딩 및 XML 데이터로 개체 serialize를 비롯 하 여 데이터 집합에서 제공 하는 것과 동일한 많은 기능을 제공 합니다. 자세한 내용은 [개체 작업](working-with-objects.md)을 참조 하세요.  
  
  Entity Framework 응용 프로그램에 필요한 데이터 집합의 기능을 제공 하지 않는 경우에도 LINQ to DataSet를 사용 하 여 LINQ 쿼리의 이점을 활용할 수 있습니다. 자세한 내용은 [LINQ to DataSet](../linq-to-dataset.md)을 참조하세요.  
  
## <a name="considerations-for-applications-that-bind-data-to-controls"></a>데이터를 컨트롤에 바인딩하는 응용 프로그램에 대한 고려 사항  
 .NET Framework를 사용 하면 데이터 집합 또는 ASP.NET 데이터 소스 컨트롤과 같은 데이터 원본의 데이터를 캡슐화 한 다음 사용자 인터페이스 요소를 해당 데이터 컨트롤에 바인딩할 수 있습니다. 다음 목록에서는 컨트롤을 Entity Framework 데이터에 바인딩할 때 고려할 사항에 대해 설명합니다.  
  
- 컨트롤에 데이터 바인딩  

  개념적 모델을 쿼리하면 Entity Framework는 데이터를 엔터티 형식의 인스턴스인 개체로 반환 합니다. 이러한 개체는 컨트롤에 직접 바인딩할 수 있으며,이 바인딩은 업데이트를 지원 합니다. 이는 <xref:System.Windows.Forms.DataGridView> <xref:System.Data.Objects.ObjectContext.SaveChanges%2A> 메서드가 호출 될 때의 행과 같은 컨트롤의 데이터 변경 내용이 자동으로 데이터베이스에 저장 됨을 의미 합니다.  
  
  응용 프로그램에서 쿼리 결과를 열거하여 <xref:System.Windows.Forms.DataGridView> 또는 데이터 바인딩을 지원하는 다른 형식의 컨트롤에 데이터를 표시하는 경우 응용 프로그램을 수정하여 컨트롤을 <xref:System.Data.Objects.ObjectQuery%601>의 결과에 바인딩할 수 있습니다.  
  
  자세한 내용은 [컨트롤에 개체 바인딩](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738469(v=vs.100))합니다.  
  
- ASP.NET 데이터 소스 컨트롤입니다.  

  Entity Framework에는 ASP.NET 웹 응용 프로그램에서 데이터 바인딩을 간소화 하도록 디자인 된 데이터 소스 컨트롤이 포함 되어 있습니다. 자세한 내용은 [EntityDataSource 웹 서버 컨트롤 개요](https://docs.microsoft.com/previous-versions/aspnet/cc488502(v=vs.100))합니다.  
  
## <a name="other-considerations"></a>기타 고려 사항  
 특정 종류의 응용 프로그램을 Entity Framework로 마이그레이션할 때 다음 사항을 고려해야 할 수도 있습니다.  
  
- 데이터 서비스를 노출하는 응용 프로그램  

  WCF(Windows Communication Foundation)를 기반으로 하는 웹 서비스와 응용 프로그램은 XML 요청/응답 메시징 형식을 사용하여 기본 데이터 소스의 데이터를 노출합니다. Entity Framework는 이진, XML 또는 WCF 데이터 계약 serialization을 사용 하 여 엔터티 개체의 serialization을 지원 합니다. 이진 및 WCF serialization은 모두 개체 그래프의 전체 serialization을 지원합니다. 자세한 내용은 [N 계층 애플리케이션 빌드](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896304(v=vs.100))합니다.  
  
- XML 데이터를 사용하는 응용 프로그램  

  개체 serialization을 사용 하면 Entity Framework 데이터 서비스를 만들 수 있습니다. 이러한 서비스는 AJAX 기반 인터넷 응용 프로그램과 같이 XML 데이터를 사용하는 응용 프로그램에 데이터를 제공합니다. 이런 경우 [!INCLUDE[ssAstoria](../../../../../includes/ssastoria-md.md)]를 사용하는 것이 좋습니다. 이러한 데이터 서비스는 엔터티 데이터 모델을 기반으로 하며 GET, PUT, POST와 같은 표준 REST (Representational State Transfer) HTTP 동작을 사용 하 여 엔터티 데이터에 대 한 동적 액세스를 제공 합니다. 자세한 내용은 [WCF Data Services 4.5](../../wcf/index.md)를 참조하세요.  
  
  Entity Framework는 기본 XML 데이터 형식을 지원 하지 않습니다. 즉, XML 열이 있는 테이블에 엔터티를 매핑할 때 XML 열에 해당하는 엔터티 속성은 문자열입니다. 개체의 연결을 끊고 XML로 serialize할 수 있습니다. 자세한 내용은 [개체 직렬화](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738446(v=vs.100))합니다.  
  
  응용 프로그램에 XML 데이터 쿼리 기능이 필요한 경우에도 LINQ to XML을 사용하여 LINQ 쿼리의 이점을 활용할 수 있습니다. 자세한 내용은 [LINQ to XMLC#()](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-overview.md) 또는 [LINQ to XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml.md)를 참조 하세요.  
  
- 상태를 유지하는 응용 프로그램  

  ASP.NET 웹 응용 프로그램은 웹 페이지 또는 사용자 세션의 상태를 유지 해야 하는 경우가 많습니다. <xref:System.Data.Objects.ObjectContext> 인스턴스의 개체를 클라이언트 뷰 상태나 서버의 세션 상태에 저장 한 다음 나중에 검색 하 여 새 개체 컨텍스트에 다시 연결할 수 있습니다. 자세한 내용은 [연결 및 분리 개체](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896271(v=vs.100))합니다.  
  
## <a name="see-also"></a>참고자료

- [배포 고려 사항](deployment-considerations.md)
- [Entity Framework 용어](terminology.md)
