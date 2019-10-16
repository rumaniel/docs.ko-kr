---
title: 웹 브라우저에서 서비스 액세스(WCF Data Services 빠른 시작)
ms.date: 03/30/2017
ms.assetid: 5a6fa180-3094-4e6e-ba2b-8c80975d18d1
ms.openlocfilehash: d89f84cd3ea4f56bbae34cbefe0c3891df96fa8b
ms.sourcegitcommit: 5ae5a1a9520b8b8b6164ad728d396717f30edafc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/11/2019
ms.locfileid: "70894342"
---
# <a name="accessing-the-service-from-a-web-browser-wcf-data-services-quickstart"></a>웹 브라우저에서 서비스 액세스(WCF Data Services 빠른 시작)

WCF Data Services 빠른 시작의 두 번째 작업입니다. 이 작업에서는 Visual Studio에서 WCF Data Services를 시작 하 고 웹 브라우저에서 선택적으로 피드 읽기를 사용 하지 않도록 설정 합니다. 그런 다음 웹 브라우저를 통해 HTTP GET 요청을 노출 된 리소스로 전송 하 여 서비스 정의 문서를 검색 하 고 데이터 서비스 리소스에 액세스 합니다.

> [!NOTE]
> 기본적으로 Visual Studio에서는 사용자 컴퓨터에서 `localhost` URI에 포트 번호를 자동으로 할당합니다. 이 작업에서는 URI 예제에서 포트 번호 `12345`를 사용합니다. Visual Studio 프로젝트에서 특정 포트 번호를 설정 하는 방법에 대 한 자세한 내용은 [데이터 서비스 만들기](creating-the-data-service.md)를 참조 하세요.

## <a name="to-request-the-default-service-document-by-using-internet-explorer"></a>Internet Explorer를 사용하여 기본 서비스 문서를 요청하려면

1. Internet Explorer의 **도구** 메뉴에서 **인터넷 옵션**을 선택 하 고 **콘텐츠** 탭을 클릭 한 다음 **설정**을 클릭 하 고 **피드 보기 켜기**를 선택 취소 합니다.

     이렇게 하면 피드 읽기가 사용되지 않습니다. 이 기능을 사용하지 않도록 설정하지 않으면 웹 브라우저에서 원시 XML 데이터를 표시하지 않고 반환된 AtomPub 인코딩 문서를 XML 피드로 처리합니다.

    > [!NOTE]
    > 브라우저에서 피드를 원시 XML 데이터로 표시할 수 없는 경우 피드를 페이지의 소스 코드로 볼 수 있어야 합니다.

2. Visual Studio에서 **f5** 키를 눌러 응용 프로그램 디버깅을 시작 합니다.

3. 로컬 컴퓨터에서 웹 브라우저를 엽니다. 주소 표시줄에 다음 URI를 입력합니다.

    ```http
    http://localhost:12345/northwind.svc
    ```

     이 데이터 서비스에서 노출하는 엔터티 집합 목록을 포함하는 기본 서비스 문서가 반환됩니다.

## <a name="to-access-entity-set-resources-from-a-web-browser"></a>웹 브라우저에서 엔터티 집합 리소스에 액세스하려면

1. 웹 브라우저의 주소 표시줄에 다음 URI를 입력합니다.

    ```http
    http://localhost:12345/northwind.svc/Customers
    ```

     Northwind 샘플 데이터베이스의 모든 고객 집합이 반환됩니다.

2. 웹 브라우저의 주소 표시줄에 다음 URI를 입력합니다.

    ```http
    http://localhost:12345/northwind.svc/Customers('ALFKI')
    ```

     특정 고객 `ALFKI`의 엔터티 인스턴스가 반환됩니다.

3. 웹 브라우저의 주소 표시줄에 다음 URI를 입력합니다.

    ```http
    http://localhost:12345/northwind.svc/Customers('ALFKI')/Orders
    ```

     고객과 주문 간의 관계가 이동되어 특정 고객 `ALFKI`에 대한 모든 주문 집합이 반환됩니다.

4. 웹 브라우저의 주소 표시줄에 다음 URI를 입력합니다.

    ```http
    http://localhost:12345/northwind.svc/Customers('ALFKI')/Orders?$filter=OrderID eq 10643
    ```

     제공한 `ALFKI` 값을 기반으로 특정 주문만 반환되도록 특정 고객 `OrderID`에 속하는 주문이 필터링됩니다.

## <a name="next-steps"></a>다음 단계

브라우저에서 지정 된 리소스에 대 한 HTTP GET 요청을 실행 하 여 웹 브라우저에서 WCF Data Services에 성공적으로 액세스 했습니다. 웹 브라우저를 사용하면 간편하게 요청의 주소 지정 구문을 실행해 보고 그 결과를 볼 수 있습니다. 그러나 프로덕션 데이터 서비스는 대개 이 방법으로 액세스되지 않습니다. 애플리케이션은 일반적으로 애플리케이션 코드나 스크립트 언어를 통해 데이터 서비스와 상호 작용합니다. 다음에는 클라이언트 라이브러리를 사용하여 CLR(공용 언어 런타임) 개체인 것처럼 데이터 서비스 리소스에 액세스하는 클라이언트 애플리케이션을 만듭니다.

> [!div class="nextstepaction"]
> [.NET Framework 클라이언트 애플리케이션 만들기](creating-the-dotnet-client-application-wcf-data-services-quickstart.md)

## <a name="see-also"></a>참고자료

- [데이터 서비스 리소스에 액세스](accessing-data-service-resources-wcf-data-services.md)
