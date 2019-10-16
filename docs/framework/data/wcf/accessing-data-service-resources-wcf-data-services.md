---
title: 데이터 서비스 리소스에 액세스(WCF Data Services)
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, querying
- getting started, WCF Data Services
- querying the data service [WCF Data Service]
- WCF Data Services, getting started
- WCF Data Services, accessing data
ms.assetid: 9665ff5b-3e3a-495d-bf83-d531d5d060ed
ms.openlocfilehash: d18ec4fd57f2437ca936074e8dcf70f17f09b877
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991114"
---
# <a name="accessing-data-service-resources-wcf-data-services"></a>데이터 서비스 리소스에 액세스(WCF Data Services)
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]는 uri [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] 로 주소를 지정할 수 있는 리소스로 데이터를 피드로 노출 하는를 지원 합니다. 이러한 리소스는 [엔터티 데이터 모델](../adonet/entity-data-model.md)의 엔터티-관계 규칙에 따라 표시 됩니다. 이 모델에서 엔터티는 고객, 주문, 항목 및 제품과 같이 애플리케이션 도메인의 데이터 형식인 데이터 운영 단위를 나타냅니다. REST(Representational State Transfer)의 의미 체계, 특히 GET, PUT, POST, DELETE 등의 표준 HTTP 동사를 사용하여 엔터티 데이터에 액세스하고 변경합니다.  
  
## <a name="addressing-resources"></a>리소스 처리  
 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]에서는 URI를 사용하여 데이터 모델에서 노출하는 모든 데이터에 주소를 지정합니다. 예를 들어, 다음 URI는 Customer 엔터티 형식의 모든 인스턴스에 대 한 항목을 포함 하는 Customers 엔터티 집합인 피드를 반환 합니다.  
  
<https://services.odata.org/Northwind/Northwind.svc/Customers>
  
 엔터티에는 엔터티 키라는 특수 속성이 있습니다. 엔터티 키는 엔터티 집합 내에서 단일 엔터티를 고유하게 식별하는 데 사용됩니다. 엔터티 키를 사용하면 엔터티 집합에 속한 특정 엔터티 형식 인스턴스의 주소를 지정할 수 있습니다. 예를 들어, 다음 URI는 키 값이 `ALFKI`인 Customer 엔터티 형식의 특정 인스턴스에 대한 항목을 반환합니다.  
  
<https://services.odata.org/Northwind/Northwind.svc/Customers('ALFKI')>
  
 엔터티 인스턴스의 기본 및 복합 속성에도 개별적으로 주소를 지정할 수 있습니다. 예를 들어, 다음 URI는 특정 고객의 `ContactName` 속성 값이 포함된 XML 요소를 반환합니다.  
  
<https://services.odata.org/Northwind/Northwind.svc/Customers('ALFKI')/ContactName>
  
 이전 URI에 `$value` 엔드포인트를 포함하는 경우 기본 속성의 값만 응답 메시지에 반환됩니다. 다음 예제에서는 XML 요소 없이 "Maria Anders" 문자열만 반환합니다.  
  
<https://services.odata.org/Northwind/Northwind.svc/Customers('ALFKI')/ContactName/$value>
  
 엔터티 간의 관계는 데이터 모델에서 연결에 의해 정의됩니다. 이러한 연결을 사용하면 엔터티 인스턴스의 탐색 속성을 사용하여 관련 엔터티의 주소를 지정할 수 있습니다. 탐색 속성은 다대일 관계의 경우 단일 관련 엔터티를 반환하고 일대다 관계의 경우 관련 엔터티의 집합을 반환할 수 있습니다. 예를 들어, 다음 URI는 특정 고객과 관련된 모든 주문의 집합인 피드를 반환합니다.  
  
<https://services.odata.org/Northwind/Northwind.svc/Customers('ALFKI')/Orders>
  
 대개 양방향인 관계는 탐색 속성 쌍으로 표현됩니다. 이전 예제에서 보여 준 관계와 반대로, 다음 URI는 특정 Order 엔터티가 속한 Customer 엔터티에 대한 참조를 반환합니다.  
  
<https://services.odata.org/Northwind/Northwind.svc/Orders(10643)/Customer>
  
 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]를 사용 하면 쿼리 식의 결과를 기반으로 리소스를 처리할 수도 있습니다. 이렇게 하면 계산 된 식을 기반으로 리소스 집합을 필터링 할 수 있습니다. 예를 들어, 다음 URI는 1997년 9월 22일 이후에 운송된 특정 고객의 주문만 반환하도록 리소스를 필터링합니다.  
  
<https://services.odata.org/Northwind/Northwind.svc/Customers( ' ALFKI ')/Orders? $filter = ShippedDate gt datetime ' 1997-09-22T00:00:00 ' >
  
 자세한 내용은 [OData: URI 규칙](https://www.odata.org/documentation/odata-version-2-0/uri-conventions/).
  
## <a name="system-query-options"></a>시스템 쿼리 옵션  
 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]필터링, 정렬 및 페이징과 같은 리소스에 대해 기존 쿼리 작업을 수행 하는 데 사용할 수 있는 시스템 쿼리 옵션 집합을 정의 합니다. 예를 들어, 다음 URI는 관련 `Order` `Order_Detail` 된 엔터티와 함께 모든 엔터티 집합을 반환 합니다 .이의 우편 번호는에서 `100`끝나지 않습니다.  
  
<https://services.odata.org/Northwind/Northwind.svc/Orders? $filter = endswith (Order_Details; ' 100 ') & $expand = & $orderby = ShipCity >
  
 또한 반환된 피드의 항목은 주문의 ShipCity 속성 값을 기준으로 정렬됩니다.  
  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]에서 지 원하는 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 시스템 쿼리 옵션은 다음과 같습니다.  
  
|쿼리 옵션|설명|  
|------------------|-----------------|  
|`$orderby`|반환된 피드의 엔터티에 대한 기본 정렬 순서를 정의합니다. 다음 쿼리는 반환된 고객 피드를 국가 및 도시를 기준으로 정렬합니다.<br /><br /> <https://services.odata.org/Northwind/Northwind.svc/Customers?$orderby=Country,City>|  
|`$top`|반환된 피드에 포함할 엔터티의 수를 지정합니다. 다음 예제에서는 처음 10명의 고객을 건너뛰고 다음 10명의 고객을 반환합니다.<br /><br /> <https://services.odata.org/Northwind/Northwind.svc/Customers?$skip=10&$top=10>|  
|`$skip`|피드의 엔터티 반환을 시작하기 전에 건너뛸 엔터티의 수를 지정합니다. 다음 예제에서는 처음 10명의 고객을 건너뛰고 다음 10명의 고객을 반환합니다.<br /><br /> <https://services.odata.org/Northwind/Northwind.svc/Customers?$skip=10&$top=10>|  
|`$filter`|특정 조건에 따라 피드에서 반환되는 엔터티를 필터링하는 식을 정의합니다. 이 쿼리 옵션은 필터 식을 계산하는 데 사용되는 미리 정의된 쿼리 함수, 논리 비교 연산자 및 산술 연산자의 집합을 지원합니다. 다음 예제에서는 우편 번호가 100으로 끝나지 않는 모든 주문을 반환합니다.<br /><br /> <https://services.odata.org/Northwind/Northwind.svc/Orders? $filter = endswith (고, ' 100 ') >|  
|`$expand`|쿼리 결과로 반환되는 관련 엔터티를 지정합니다. 관련 엔터티는 쿼리 결과로 반환되는 엔터티와 함께 항목이나 피드로 포함됩니다. 다음 예제에서는 'ALFKI' 고객의 주문을 각 주문에 대한 항목 정보와 함께 반환합니다.<br /><br /> <https://services.odata.org/Northwind/Northwind.svc/Customers('ALFKI')/Orders?$expand=Order_Details>|  
|`$select`|엔터티의 속성이 해당 프로젝션에 반환되도록 정의하는 프로젝션을 지정합니다. 기본적으로 엔터티의 모든 속성은 피드에 반환됩니다. 다음 쿼리는 `Customer` 엔터티의 세 속성만 반환합니다.<br /><br /> <https://services.odata.org/Northwind/Northwind.svc/Customers?$select=CustomerID,CompanyName,City>|  
|`$inlinecount`|피드에 반환되는 엔터티 수가 피드와 함께 포함되도록 요청합니다.|  
  
## <a name="addressing-relationships"></a>관계 주소 지정  
 엔터티 집합과 엔터티 인스턴스의 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 주소를 지정 하는 것 외에도 엔터티 간의 관계를 나타내는 연결의 주소를 지정할 수 있습니다. 이 기능은 Northwind 샘플 데이터베이스의 지정된 주문과 관련된 운송업체와 같이 두 엔터티 인스턴스 간의 관계를 만들거나 변경하는 데 필요합니다. [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]는 엔터티 `$link` 간의 연결을 구체적으로 처리 하는 연산자를 지원 합니다. 예를 들어, 다음 URI는 HTTP PUT 요청 메시지에 지정되어 지정한 주문의 운송업체를 새 운송업체로 변경합니다.  
  
<https://services.odata.org/Northwind/Northwind.svc/Orders(10643)/$links/Shipper>
  
 자세한 내용은 OData에서 `3.2. Addressing Links between Entries` [섹션을 참조 하세요. URI 규칙](https://www.odata.org/documentation/odata-version-2-0/uri-conventions/).
  
## <a name="consuming-the-returned-feed"></a>반환된 피드 사용  
 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 리소스의 URI를 사용 하면 서비스에서 노출 하는 엔터티 데이터의 주소를 지정할 수 있습니다. 웹 브라우저 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 의 주소 필드에 URI를 입력 하면 요청 된 리소스의 피드 표현이 반환 됩니다. 자세한 내용은 [WCF Data Services 빠른](quickstart-wcf-data-services.md)시작을 참조 하세요. 웹 브라우저가 데이터 서비스 리소스가 필요한 데이터를 반환 하는지 테스트 하는 데 유용할 수 있지만, 데이터를 만들고 업데이트 하 고 삭제할 수 있는 프로덕션 데이터 서비스는 일반적으로 웹 페이지의 응용 프로그램 코드나 스크립팅 언어를 통해 액세스 됩니다. 자세한 내용은 [클라이언트 응용 프로그램에서 데이터 서비스 사용](using-a-data-service-in-a-client-application-wcf-data-services.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [Open Data Protocol 웹 사이트](https://www.odata.org/)
