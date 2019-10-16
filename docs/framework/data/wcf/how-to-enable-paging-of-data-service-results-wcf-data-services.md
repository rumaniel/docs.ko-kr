---
title: '방법: 데이터 서비스 결과의 페이징 사용 (WCF Data Services)'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- paging output [WCF Data Services]
ms.assetid: 9a316cbd-9612-4482-a541-a10bc78b2635
ms.openlocfilehash: 82b4d0fd3531778ab494d6526a56b092edf9481a
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70780046"
---
# <a name="how-to-enable-paging-of-data-service-results-wcf-data-services"></a>방법: 데이터 서비스 결과의 페이징 사용 (WCF Data Services)
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]를 사용하면 데이터 서비스 쿼리에서 반환되는 엔터티 수를 제한할 수 있습니다. 페이지 제한은 서비스가 초기화될 때 호출되는 메서드에서 정의되며 각 엔터티 집합에 대해 별도로 설정될 수 있습니다.  
  
 페이징을 사용하도록 설정하면 피드의 최종 항목에 다음 데이터 페이지에 대한 링크가 포함됩니다. 자세한 내용은 [데이터 서비스 구성](configuring-the-data-service-wcf-data-services.md)합니다.  
  
 이 항목에서는 데이터 서비스를 수정하여 반환된 `Customers` 및 `Orders` 엔터티 집합의 페이징을 사용하도록 설정하는 방법을 보여 줍니다. 이 항목의 예제에서는 Northwind 샘플 데이터 서비스를 사용합니다. 이 서비스는 [WCF Data Services 빠른](quickstart-wcf-data-services.md)시작을 완료 하면 생성 됩니다.  
  
### <a name="how-to-enable-paging-of-returned-customers-and-orders-entity-sets"></a>반환된 Customers 및 Orders 엔터티 집합의 페이징을 사용하도록 설정하는 방법  
  
- 데이터 서비스 코드에서 `InitializeService` 함수의 자리 표시자 코드를 다음 코드로 바꿉니다.  
  
     [!code-csharp[Astoria Northwind Service#DataServiceConfigPaging](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_service/cs/northwind.svc.cs#dataserviceconfigpaging)]
     [!code-vb[Astoria Northwind Service#DataServiceConfigPaging](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_service/vb/northwind.svc.vb#dataserviceconfigpaging)]  
  
## <a name="see-also"></a>참고자료

- [지연 콘텐츠 로드](loading-deferred-content-wcf-data-services.md)
- [방법: 페이지 단위 결과 로드](how-to-load-paged-results-wcf-data-services.md)
