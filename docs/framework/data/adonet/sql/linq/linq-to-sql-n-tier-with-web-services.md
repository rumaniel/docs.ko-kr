---
title: 웹 서비스를 사용하는 LINQ to SQL N 계층
ms.date: 03/30/2017
ms.assetid: 9cb10eb8-957f-4beb-a271-5f682016fed2
ms.openlocfilehash: 279907aeaaa83d6901621c03231068d61045ec5c
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781334"
---
# <a name="linq-to-sql-n-tier-with-web-services"></a>웹 서비스를 사용하는 LINQ to SQL N 계층
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]는 웹 서비스와 같이 느슨하게 결합 된 DAL (데이터 액세스 계층)의 중간 계층에서 사용 하기 위해 특별히 설계 되었습니다. 프레젠테이션 계층이 ASP.NET 웹 페이지인 경우에는 <xref:System.Web.UI.WebControls.LinqDataSource> 웹 서버 컨트롤을 사용하여 사용자 인터페이스와 중간 계층의 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 사이에 데이터 전송을 관리합니다. 그러나 프레젠테이션 계층이 ASP.NET 페이지가 아닌 경우에는 중간 계층과 프레젠테이션 계층 모두에서 데이터 serialization 및 deserialization을 관리하기 위해 추가적인 작업을 수행해야 합니다.  
  
## <a name="setting-up-linq-to-sql-on-the-middle-tier"></a>중간 계층에서 LINQ to SQL 설정  
 웹 서비스 또는 n 계층 응용 프로그램의 중간 계층에는 데이터 컨텍스트와 엔터티 클래스가 들어 있습니다. 설명서의 다른 부분에서 설명한 대로 이러한 클래스를 수동으로 만들거나 SQLMetal 또는 개체 관계형 디자이너를 사용 하 여 만들 수 있습니다. 디자인 타임에 엔터티 클래스를 serialize할 수 있습니다. 자세한 내용은 [방법: 엔터티를 Serialize](how-to-make-entities-serializable.md)가능 하 게 만듭니다. 또는 serialize할 데이터를 캡슐화하는 별도의 클래스 집합을 만든 다음 [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)] 쿼리에 데이터를 반환할 때 serialize 가능한 이러한 형식을 사용할 수도 있습니다.  
  
 그런 다음 클라이언트에서 데이터를 검색, 삽입 및 업데이트할 때 호출할 메서드를 사용하여 인터페이스를 정의합니다. 이 인터페이스 메서드는 [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)] 쿼리를 래핑합니다. 원격 메서드 호출 및 데이터 serialization은 모든 종류의 serialization 메커니즘을 사용하여 처리할 수 있습니다. 단, 표준 Northwind 개체 모델의 Customers와 Orders의 관계와 같이 개체 모델에 순환 또는 양방향 관계가 있는 경우에는 이를 지원하는 serializer를 반드시 사용해야 합니다. WCF(Windows Communication Foundation) <xref:System.Runtime.Serialization.DataContractSerializer>는 양방향 관계를 지원하지만 WCF가 아닌 웹 서비스에 사용되는 XmlSerializer는 양방향 관계를 지원하지 않습니다. 따라서 XmlSerializer를 사용하도록 선택한 경우에는 개체 모델에 순환 관계가 없는지 반드시 확인해야 합니다.  
  
 Windows Communication Foundation에 대 한 자세한 내용은 [Visual Studio의 Windows Communication Foundation Services 및 WCF Data Services](/visualstudio/data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio)를 참조 하세요.  
  
 <xref:System.Data.Linq.DataContext> 및 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 런타임 이벤트에 후크할 엔터티 클래스에 부분 클래스 및 메서드를 사용하여 비즈니스 규칙 또는 다른 도메인별 논리를 구현합니다. 자세한 내용은 [N 계층 비즈니스 논리 구현](implementing-business-logic-linq-to-sql.md)을 참조 하세요.  
  
## <a name="defining-the-serializable-types"></a>Serializable 형식 정의  
 클라이언트나 프레젠테이션 계층에는 중간 계층으로부터 수신할 클래스의 형식 정의가 있어야 합니다. 이러한 형식은 엔터티 클래스 자체이거나 원격 작업을 위해 엔터티 클래스의 특정 필드만 래핑하는 특수 클래스일 수 있습니다. 어떤 경우든 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]은 프레젠테이션 계층이 이러한 형식 정의를 어떤 방법으로 가져오는지 전혀 고려하지 않습니다. 예를 들어 프레젠테이션 계층에서는 WCF를 사용하여 형식을 자동으로 생성하거나, 이러한 형식이 정의되어 있는 DLL의 복사본을 가지고 있거나, 형식에 대한 고유한 버전을 직접 정의할 수 있습니다.  
  
## <a name="retrieving-and-inserting-data"></a>데이터 검색 및 삽입  
 중간 계층에서는 프레젠테이션 계층에서 데이터에 액세스하는 방법을 지정하는 인터페이스를 정의합니다. 예를 들면 `GetProductByID(int productID)` 또는 `GetCustomers()`와 같은 인터페이스를 정의할 수 있습니다. 중간 계층에서 메서드 본문은 일반적으로 <xref:System.Data.Linq.DataContext>의 새 인스턴스를 만들고 하나 이상의 테이블에 대해 쿼리를 실행합니다. 그런 다음 중간 계층에서는 결과를 <xref:System.Collections.Generic.IEnumerable%601>로 반환합니다. 여기에서 `T`는 엔터티 클래스이거나 serialization에 사용되는 다른 형식입니다. 프레젠테이션 계층에서는 중간 계층을 대상으로 쿼리 변수를 직접 보내거나 받지 않습니다. 이 두 계층은 구체적인 데이터의 값, 개체 및 컬렉션을 교환합니다. 프레젠테이션 계층에서는 컬렉션을 수신한 후 필요한 경우 [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)] to Objects를 사용하여 쿼리할 수 있습니다.  
  
 데이터를 삽입할 경우 프레젠테이션 계층에서는 새 개체를 만든 후 중간 계층에 보내거나, 중간 계층에서 개체를 만드는 데 사용할 기준 값을 제공할 수 있습니다. 일반적으로 n 계층 응용 프로그램에서의 데이터 검색 및 삽입은 2계층 응용 프로그램에서의 해당 프로세스와 크게 다르지 않습니다. 자세한 내용은 [데이터베이스 쿼리](querying-the-database.md) 및 [데이터 변경 내용 작성 및 전송](making-and-submitting-data-changes.md)을 참조 하세요.  
  
## <a name="tracking-changes-for-updates-and-deletes"></a>업데이트 및 삭제 변경 사항 추적  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]은 RowVersions라고도 하는 타임스탬프 및 원래 값을 기반으로 하는 낙관적 동시성을 지원합니다. 데이터베이스 테이블에 타임스탬프가 있는 경우에는 업데이트 및 삭제 시 중간 계층 또는 프레젠테이션 계층에서 약간의 추가 작업이 필요할 수 있습니다. 그러나 낙관적 동시성 검사에 원래 값을 사용해야 하는 경우에는 업데이트 시 이러한 값을 추적하고 다시 보내는 작업을 프레젠테이션 계층에서 담당합니다. 그 이유는 프레젠테이션 계층에서 발생한 엔터티 변경 사항을 중간 계층에서 추적하지 않기 때문입니다. 실제로 엔터티에 대한 최초 검색과 엔터티에 대한 이후 업데이트는 일반적으로 <xref:System.Data.Linq.DataContext>의 완전하게 다른 두 개별 인스턴스를 통해 수행됩니다.  
  
 프레젠테이션 계층에서 변경하는 내용이 많을수록 변경 사항을 추적하고 패키지화하여 중간 계층에 다시 보내기가 복잡해 집니다. 변경 사항 통신 메커니즘은 응용 프로그램에 따라 다르게 구현되지만 낙관적 동시성 검사에 필요한 원래 값을 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에 반드시 제공해야 한다는 점은 동일합니다.  
  
 자세한 내용은 [데이터 검색 및 CUD 작업에서 N 계층 애플리케이션 (LINQ to SQL)](data-retrieval-and-cud-operations-in-n-tier-applications.md)합니다.  
  
## <a name="see-also"></a>참고자료

- [LINQ to SQL을 사용한 N 계층 및 원격 응용 프로그램](n-tier-and-remote-applications-with-linq-to-sql.md)
- [LinqDataSource 웹 서버 컨트롤 개요](https://docs.microsoft.com/previous-versions/aspnet/bb547113(v=vs.100))
