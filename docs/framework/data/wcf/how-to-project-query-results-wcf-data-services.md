---
title: '방법: 프로젝트 쿼리 결과 (WCF Data Services)'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- projection [WCF Data Services]
- WCF Data Services, projection
- query projection [WCF Data Services]
- WCF Data Services, querying
ms.assetid: 474ac625-8770-43ba-8320-d3315ea9530f
ms.openlocfilehash: 758bb01764fcfe195d4f940705316e7579be95ff
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70780014"
---
# <a name="how-to-project-query-results-wcf-data-services"></a>방법: 프로젝트 쿼리 결과 (WCF Data Services)
프로젝션은 엔터티의 특정 속성만 응답에서 반환되도록 지정하여 쿼리에서 반환되는 데이터의 양을 줄이는 메커니즘을 제공합니다. 쿼리 옵션을 `$select` 사용 하거나 LINQ 쿼리에서 [select](../../../csharp/language-reference/keywords/select-clause.md) 절 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] (Visual Basic에서[선택](../../../visual-basic/language-reference/queries/select-clause.md) )을 사용 하 여 쿼리 결과에 대해 프로젝션을 수행할 수 있습니다. 자세한 내용은 [데이터 서비스 쿼리](querying-the-data-service-wcf-data-services.md)를 참조 하세요.  
  
 이 항목의 예제에서는 Northwind 샘플 데이터 서비스 및 자동 생성된 클라이언트 데이터 서비스 클래스를 사용합니다. 이 서비스 및 클라이언트 데이터 클래스는 [WCF Data Services 빠른](quickstart-wcf-data-services.md)시작을 완료 하면 생성 됩니다.  
  
## <a name="example"></a>예제  
 다음 예제에서는 Customers 엔터티를 새로운 CustomerAddress 형식으로 프로젝션하는 LINQ 쿼리를 보여 줍니다. 이 형식에는 주소 관련 속성과 ID 속성만 포함됩니다. 이 `CustomerAddress` 클래스는 클라이언트에서 정의되며 클라이언트 라이브러리가 엔터티 형식으로 인식할 수 있도록 특성이 지정됩니다.  
  
 [!code-csharp[Astoria Northwind Client#SelectCustomerAddress](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#selectcustomeraddress)]
 [!code-vb[Astoria Northwind Client#SelectCustomerAddress](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#selectcustomeraddress)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 반환된 Customers 엔터티를 새로운 CustomerAddressNonEntity 형식으로 프로젝션하는 LINQ 쿼리를 보여 줍니다. 이 형식에는 주소 관련 속성만 포함되고 ID 속성은 포함되지 않습니다. 이 `CustomerAddressNonEntity` 클래스는 클라이언트에서 정의되며 엔터티 형식으로 특성이 지정되지 않습니다.  
  
 [!code-csharp[Astoria Northwind Client#SelectCustomerAddressNonEntity](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#selectcustomeraddressnonentity)]
 [!code-vb[Astoria Northwind Client#SelectCustomerAddressNonEntity](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#selectcustomeraddressnonentity)]  
  
## <a name="example"></a>예제  
 다음 예제에서는 이전 예제에서 사용 되 `CustomerAddress` 는 `CustomerAddressNonEntity` 및 형식의 정의를 보여 줍니다.  
  
 [!code-csharp[Astoria Northwind Client#CustomerAddressDefinition](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/customeraddress.cs#customeraddressdefinition)]
 [!code-vb[Astoria Northwind Client#CustomerAddressDefinition](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/customeraddress.vb#customeraddressdefinition)]
