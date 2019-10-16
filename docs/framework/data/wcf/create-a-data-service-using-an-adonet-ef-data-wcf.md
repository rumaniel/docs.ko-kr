---
title: '방법: ADO.NET Entity Framework 데이터 원본을 사용 하 여 데이터 서비스 만들기 (WCF Data Services)'
ms.date: 08/24/2018
helpviewer_keywords:
- WCF Data Services, providers
- WCF Data Services, Entity Framework
ms.assetid: 6d11fec8-0108-42f5-8719-2a7866d04428
ms.openlocfilehash: 8c597738d656b32e7b4c75246027b726f425c6ef
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053013"
---
# <a name="how-to-create-a-data-service-using-an-adonet-entity-framework-data-source-wcf-data-services"></a>방법: ADO.NET Entity Framework 데이터 원본을 사용 하 여 데이터 서비스 만들기 (WCF Data Services)

WCF Data Services 엔터티 데이터를 데이터 서비스로 노출 합니다. 이 엔터티 데이터는 데이터 원본이 관계형 데이터베이스인 경우에 ADO. NETEntity Framework에서 제공 됩니다. 이 항목에서는 기존 데이터베이스를 기반으로 하는 Visual Studio 웹 응용 프로그램에서 Entity Framework 기반 데이터 모델을 만들고 이 데이터 모델을 사용하여 새 데이터 서비스를 만드는 방법을 보여 줍니다.

Entity Framework는 Visual Studio 프로젝트 외부에서 Entity Framework 모델을 생성할 수 있는 명령줄 도구도 제공합니다. 자세한 내용은 [방법: Edmgen.exe를 사용 하 여 모델 및 매핑 파일](../adonet/ef/how-to-use-edmgen-exe-to-generate-the-model-and-mapping-files.md)을 생성 합니다.

## <a name="to-add-an-entity-framework-model-that-is-based-on-an-existing-database-to-an-existing-web-application"></a>기존 웹 애플리케이션에 기존 데이터베이스를 기반으로 하는 Entity Framework 모델을 추가하려면

1. **프로젝트** 메뉴에서**새 항목** **추가** > 를 클릭 합니다.

2. **템플릿** 창에서 **데이터** 범주를 클릭 한 다음 **ADO.NET 엔터티 데이터 모델**를 선택 합니다.

3. 모델 이름을 입력 한 다음 **추가**를 클릭 합니다.

     엔터티 데이터 모델 마법사 시작 페이지가 표시됩니다.

4. **Model 콘텐츠 선택** 대화 상자에서 **데이터베이스에서 생성**을 선택 합니다. 그리고 **다음**을 클릭합니다.

5. **새 연결** 단추를 클릭 합니다.

6. **연결 속성** 대화 상자에서 서버 이름을 입력 하 고 인증 방법을 선택한 다음 데이터베이스 이름을 입력 하 고 **확인**을 클릭 합니다.

     **데이터 연결 선택** 대화 상자가 데이터베이스 연결 설정으로 업데이트 됩니다.

7. **App.config의 엔터티 연결 설정 저장:** 확인란을 선택 했는지 확인 합니다. 그리고 **다음**을 클릭합니다.

8. **데이터베이스 개체 선택** 대화 상자에서 데이터 서비스에 노출할 데이터베이스 개체를 모두 선택 합니다.

    > [!NOTE]
    > 데이터 모델에 포함된 개체는 데이터 서비스에 의해 자동으로 노출되지 않습니다. 서비스 자체에서 해당 개체를 명시적으로 노출해야 합니다. 자세한 내용은 [데이터 서비스 구성](configuring-the-data-service-wcf-data-services.md)합니다.

9. **마침** 을 클릭 하 여 마법사를 완료 합니다.

     특정 데이터베이스를 기반으로 하는 기본 데이터 모델이 만들어집니다. Entity Framework에서 데이터 모델을 사용하도록 설정하여 사용자 지정합니다. 자세한 내용은 [엔터티 데이터 모델 도구 작업](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738480(v=vs.100))을 참조 하세요.

## <a name="to-create-the-data-service-by-using-the-new-data-model"></a>새 데이터 모델을 사용하여 데이터 서비스를 만들려면

1. Visual Studio에서 데이터 모델을 나타내는 .edmx 파일을 엽니다.

2. **모델 브라우저**에서 모델을 마우스 오른쪽 단추로 클릭 하 고 **속성**을 클릭 한 다음 엔터티 컨테이너의 이름을 확인 합니다.

3. **솔루션 탐색기**에서 ASP.NET 프로젝트의 이름을 마우스 오른쪽 단추로 클릭 한 다음**새 항목** **추가** > 를 클릭 합니다.

4. **새 항목 추가** 대화 상자의 **웹** 범주에서 **WCF 데이터 서비스** 템플릿을 선택 합니다.

   ![Visual Studio 2015의 WCF 데이터 서비스 항목 템플릿](./media/wcf-data-service-item-template.png)

   > [!NOTE]
   > **WCF 데이터 서비스** 템플릿은 visual studio 2015에서 사용할 수 있지만 visual studio 2017에서는 사용할 수 없습니다.

5. 서비스의 이름을 입력 하 고 **확인**을 클릭 합니다.

     Visual Studio에서 새 서비스의 XML 태그 및 코드 파일이 생성됩니다. 기본적으로 코드 편집기 창이 열립니다.

6. 데이터 서비스 코드에서 데이터 서비스를 정의하는 클래스 정의의 `/* TODO: put your data source class name here */` 주석을 <xref:System.Data.Objects.ObjectContext> 클래스에서 상속되고 2단계에서 적어 둔 데이터 모델의 엔터티 컨테이너인 형식으로 바꿉니다.

7. 데이터 서비스 코드에서 권한 있는 클라이언트가 데이터 서비스에서 노출하는 엔터티 집합에 액세스할 수 있도록 합니다. 자세한 내용은 [데이터 서비스 만들기](creating-the-data-service.md)를 참조 하세요.

8. 웹 브라우저를 사용 하 여 Northwind 데이터 서비스를 테스트 하려면 [웹 브라우저에서 서비스 액세스](accessing-the-service-from-a-web-browser-wcf-data-services-quickstart.md)항목의 지침을 따르세요.

## <a name="see-also"></a>참고자료

- [WCF Data Services 정의](defining-wcf-data-services.md)
- [Data Services 공급자](data-services-providers-wcf-data-services.md)
- [방법: 리플렉션 공급자를 사용 하 여 데이터 서비스 만들기](create-a-data-service-using-rp-wcf-data-services.md)
- [방법: LINQ to SQL 데이터 원본을 사용 하 여 데이터 서비스 만들기](create-a-data-service-using-linq-to-sql-wcf.md)
