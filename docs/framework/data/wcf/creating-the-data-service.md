---
title: Visual Studio에서 WCF 데이터 서비스 만들기
ms.date: 08/24/2018
dev_langs:
- csharp
- vb
ms.assetid: 34d1d971-5e18-4c22-9bf6-d3612e27ea59
ms.openlocfilehash: 582f5f2d6d82613736ed795eebe5129284cdac6e
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052991"
---
# <a name="create-the-data-service"></a>데이터 서비스 만들기

이 항목에서는 WCF Data Services를 사용 하 여 Northwind 샘플 데이터베이스를 기반으로 하는 [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] 피드를 노출 하는 샘플 데이터 서비스를 만듭니다. 작업에 필요한 기본 단계는 다음과 같습니다.

1. ASP.NET 웹 애플리케이션을 만듭니다.

2. 엔터티 데이터 모델 도구를 사용하여 데이터 모델을 정의합니다.

3. 웹 애플리케이션에 데이터 서비스를 추가합니다.

4. 데이터 서비스에 액세스할 수 있도록 설정합니다.

## <a name="create-the-aspnet-web-app"></a>ASP.NET 웹 앱 만들기

1. Visual Studio의 **파일** 메뉴에서 **새** > **프로젝트**를 선택 합니다.

1. **새 프로젝트** 대화 상자의 Visual Basic 또는 시각적 개체 C# 에서 **웹** 범주를 선택 하 고 **ASP.NET 웹 응용 프로그램**을 선택 합니다.

1. 프로젝트 `NorthwindService` 의 이름으로를 입력 한 다음 **확인을**선택 합니다.

1. **새 ASP.NET 웹 응용 프로그램** 대화 상자에서 **비어 있음** 을 선택 하 고 **확인**을 선택 합니다.

1. (선택 사항) 웹 애플리케이션의 특정 포트 번호를 지정합니다. 참고: 포트 번호 `12345` 는이 일련의 빠른 시작 항목에서 사용 됩니다.

    1. **솔루션 탐색기**에서 방금 만든 ASP.NET 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 선택 합니다.

    2. **웹** 탭을 선택 하 고 **특정 포트** 텍스트 상자의 값을로 `12345`설정 합니다.

## <a name="define-the-data-model"></a>데이터 모델 정의

1. **솔루션 탐색기**에서 ASP.NET 프로젝트의 이름을 마우스 오른쪽 단추로 클릭 한 다음**새 항목** **추가** > 를 클릭 합니다.

2. **새 항목 추가** 대화 상자에서 **데이터** 범주를 선택 하 고 **ADO.NET 엔터티 데이터 모델**를 선택 합니다.

3. 데이터 모델의 이름에을 입력 `Northwind.edmx`합니다.

4. **엔터티 데이터 모델 마법사**에서 **데이터베이스에서 EF Designer**를 선택 하 고 **다음**을 클릭 합니다.

5. 다음 단계 중 하나를 수행 하 여 데이터 모델을 데이터베이스에 연결한 **후 다음을 클릭 합니다**.

    - 데이터베이스 연결이 이미 구성 되어 있지 않은 경우 **새 연결** 을 클릭 하 고 새 연결을 만듭니다. 자세한 내용은 [방법: SQL Server 데이터베이스](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/s4yys16a(v=vs.90))에 대 한 연결을 만듭니다. 이 SQL Server 인스턴스에는 Northwind 샘플 데이터베이스가 연결되어 있어야 합니다.

         \- 또는 -

    - Northwind 데이터베이스에 연결할 수 있도록 데이터베이스 연결이 이미 구성되어 있는 경우 연결 목록에서 해당 연결을 선택합니다.

6. 마법사의 마지막 페이지에서 데이터베이스의 모든 테이블에 대한 확인란을 선택하고 뷰 및 저장 프로시저에 대한 확인란의 선택을 취소합니다.

7. **마침** 을 클릭하여 마법사를 닫습니다.

## <a name="create-the-wcf-data-service"></a>WCF 데이터 서비스 만들기

1. **솔루션 탐색기**에서 ASP.NET 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음**새 항목** **추가** > 를 선택 합니다.

2. **새 항목 추가** 대화 상자의 **웹** 범주에서 **WCF 데이터 서비스** 항목 템플릿을 선택 합니다.

   ![Visual Studio 2015의 WCF 데이터 서비스 항목 템플릿](./media/wcf-data-service-item-template.png)

   > [!NOTE]
   > **WCF 데이터 서비스** 템플릿은 visual studio 2015에서 사용할 수 있지만 visual studio 2017에서는 사용할 수 없습니다.

3. 서비스의 이름에을 입력 `Northwind`합니다.

     Visual Studio에서 새 서비스의 XML 태그 및 코드 파일이 생성됩니다. 기본적으로 코드 편집기 창이 열립니다. **솔루션 탐색기**서비스에는 이름이 *svc.cs* 또는. n a n *.vb*인 Northwind 이름이 있습니다.

4. 데이터 서비스 코드에서 데이터 서비스를 정의하는 클래스 정의의 `/* TODO: put your data source class name here */` 주석을 데이터 모델의 엔터티 컨테이너인 형식(이 경우 `NorthwindEntities`)으로 바꿉니다. 클래스 정의는 다음과 같이 나타납니다.

     [!code-csharp[Astoria Quickstart Service#ServiceDefinition](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_quickstart_service/cs/northwind.svc.cs#servicedefinition)]
     [!code-vb[Astoria Quickstart Service#ServiceDefinition](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_quickstart_service/vb/northwind.svc.vb#servicedefinition)]

## <a name="enable-access-to-data-service-resources"></a>데이터 서비스 리소스에 대 한 액세스 사용

1. 데이터 서비스 코드에서 `InitializeService` 함수의 자리 표시자 코드를 다음 코드로 바꿉니다.

     [!code-csharp[Astoria Quickstart Service#AllReadConfig](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_quickstart_service/cs/northwind.svc.cs#allreadconfig)]
     [!code-vb[Astoria Quickstart Service#AllReadConfig](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_quickstart_service/vb/northwind.svc.vb#allreadconfig)]

     이렇게 하면 권한 있는 클라이언트가 지정된 엔터티 집합의 리소스에 대한 읽기 및 쓰기 액세스 권한을 가질 수 있습니다.

    > [!NOTE]
    > ASP.NET 애플리케이션에 액세스할 수 있는 클라이언트는 데이터 서비스에 의해 노출되는 리소스에도 액세스할 수 있습니다. 리소스에 무단으로 액세스할 수 없도록 하려면 프로덕션 데이터 서비스에서 애플리케이션 자체에도 보안을 설정해야 합니다. 자세한 내용은 [Securing WCF Data Services](securing-wcf-data-services.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계

Northwind 샘플 데이터베이스를 기반으로 하는 OData 피드를 노출 하는 새 데이터 서비스를 성공적으로 만들었으며 ASP.NET 웹 응용 프로그램에 대 한 사용 권한이 있는 클라이언트의 피드에 대 한 액세스를 사용 하도록 설정 했습니다. 다음으로, Visual Studio에서 데이터 서비스를 시작 하 고 웹 브라우저를 통해 HTTP GET 요청을 제출 하 여 OData 피드에 액세스 합니다.

> [!div class="nextstepaction"]
> [웹 브라우저에서 서비스 액세스](accessing-the-service-from-a-web-browser-wcf-data-services-quickstart.md)

## <a name="see-also"></a>참고자료

- [ADO.NET 엔터티 데이터 모델 도구](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb399249(v=vs.100))
