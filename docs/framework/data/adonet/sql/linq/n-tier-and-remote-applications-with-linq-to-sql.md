---
title: LINQ to SQL을 사용한 N 계층 및 원격 애플리케이션
ms.date: 03/30/2017
ms.assetid: 854a1cdd-53cb-45f5-83ca-63962a9b3598
ms.openlocfilehash: 94ca057da10c3570e85e17b5caec2d86154d8a3f
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781411"
---
# <a name="n-tier-and-remote-applications-with-linq-to-sql"></a>LINQ to SQL을 사용한 N 계층 및 원격 애플리케이션
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]을 사용하는 n 계층 또는 다계층 애플리케이션을 만들 수 있습니다. 일반적으로 데이터 컨텍스트, 엔터티 클래스 및 쿼리 생성 논리는 중간 계층에서 DAL (데이터 액세스 계층)로 배치 됩니다. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 비즈니스 논리와 모든 비지속적 데이터는 엔터티와 데이터 컨텍스트의 부분 클래스와 메서드에 완전하게 구현되거나 별도의 클래스에 구현될 수 있습니다.

 클라이언트 또는 프레젠테이션 계층에서 중간 계층의 원격 인터페이스에 있는 메서드를 호출하면 중간 계층의 DAL에서는 <xref:System.Data.Linq.DataContext> 메서드에 매핑된 쿼리나 저장 프로시저를 실행합니다. 중간 계층에서는 일반적으로 프록시 개체 또는 엔터티의 XML 표현으로 클라이언트에 데이터를 반환합니다.

 중간 계층에서 엔터티는 엔터티의 상태를 추적하는 데이터 컨텍스트에 의해 만들어지며, 데이터베이스로부터의 지연된 로드 및 데이터베이스로의 변경 내용 전송을 관리합니다. 이러한 엔터티는 `DataContext`에 "연결"됩니다. 그러나 serialization을 통해 엔터티를 다른 계층으로 보내면 엔터티가 분리되어 `DataContext`에서 해당 엔터티의 상태를 더 이상 추적하지 않습니다. 업데이트를 위해 클라이언트에서 다시 보내는 엔터티는 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]에서 변경 내용을 데이터베이스에 전송하기 전에 데이터 컨텍스트에 다시 연결되어야 합니다. 낙관적 동시성 검사에 원래 값 및/또는 타임스탬프가 필요한 경우 클라이언트에서는 이러한 정보를 중간 계층에 다시 제공해야 합니다.

 ASP.NET 애플리케이션에서는 이러한 복잡한 작업을 <xref:System.Web.UI.WebControls.LinqDataSource>에서 대부분 처리합니다. 자세한 내용은 [LinqDataSource 웹 서버 컨트롤 개요](https://docs.microsoft.com/previous-versions/aspnet/bb547113(v=vs.100))를 참조 하세요.

## <a name="additional-resources"></a>추가 리소스
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]을 사용하는 n 계층 애플리케이션을 구현하는 방법에 대한 자세한 내용은 다음 항목을 참조하세요.

- [ASP.NET을 사용하는 LINQ to SQL N 계층](linq-to-sql-n-tier-with-aspnet.md)

- [웹 서비스를 사용하는 LINQ to SQL N 계층](linq-to-sql-n-tier-with-web-services.md) 

- [N 계층 비즈니스 논리 구현](implementing-business-logic-linq-to-sql.md)

- [N 계층 애플리케이션에서 데이터 검색 및 CUD 작업(LINQ to SQL)](data-retrieval-and-cud-operations-in-n-tier-applications.md)

 ADO.NET 데이터 집합을 사용 하는 n 계층 응용 프로그램에 대 한 자세한 내용은 [n 계층 응용 프로그램에서 데이터 집합 작업](/visualstudio/data-tools/work-with-datasets-in-n-tier-applications)을 참조 하세요.

## <a name="see-also"></a>참고자료

- [배경 정보](background-information.md)
