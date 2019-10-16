---
title: 빠른 시작(WCF Data Services)
ms.date: 08/24/2018
helpviewer_keywords:
- WCF Data Services, quick-start example
- WCF Data Services, Entity Data Model (EDM) service
ms.assetid: 7b18ca1e-d4d6-4c7a-afb9-ce3cebb98a8d
ms.openlocfilehash: df6806cd77e7ff109d79f7ba61866763de4c7fc1
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70790370"
---
# <a name="quickstart-wcf-data-services"></a>빠른 시작(WCF Data Services)

이 빠른 시작을 사용 하면 [시작](getting-started-with-wcf-data-services.md)의 항목을 [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] 지 원하는 일련의 작업을 통해 WCF Data Services 및에 익숙해질 수 있습니다.

## <a name="what-youll-learn"></a>학습 내용

이 빠른 시작의 첫 번째 작업에서는 Northwind 샘플 데이터베이스에서 OData 피드를 노출 하는 데이터 서비스를 만드는 방법을 보여 줍니다. 이후 항목에서는 웹 브라우저를 사용 하 여 OData 피드에 액세스 하 고 클라이언트 라이브러리를 사용 하 여 OData 피드를 사용 하는 Windows Presentation Foundation (WPF) 클라이언트 응용 프로그램도 만듭니다.

## <a name="prerequisites"></a>필수 구성 요소

이 퀵 스타트를 수행하려면 다음 구성 요소를 설치해야 합니다.

- Visual Studio

- SQL Server 인스턴스입니다. 여기에는 visual studio 2015의 기본 설치에 포함 되거나 Visual Studio 2017의 **데이터 저장 및 처리** 워크 로드의 일부로 포함 되는 SQL Server Express 포함 됩니다.

- Northwind 샘플 데이터베이스 이 샘플 데이터베이스를 다운로드하려면 [SQL Server용 샘플 데이터베이스](https://go.microsoft.com/fwlink/?linkid=24758)다운로드 페이지를 참조하세요.

## <a name="wcf-data-services-quickstart-tasks"></a>WCF data services 빠른 시작 작업

 [데이터 서비스 만들기](creating-the-data-service.md)

 ASP.NET 응용 프로그램과 데이터 모델을 정의하고, 데이터 서비스를 만들고, 리소스에 액세스할 수 있도록 합니다.

 [웹 브라우저에서 서비스 액세스](accessing-the-service-from-a-web-browser-wcf-data-services-quickstart.md)

 Visual Studio에서 서비스를 시작하고 웹 브라우저를 통해 HTTP GET 요청을 노출된 피드로 전송하여 서비스에 액세스합니다.

 [.NET Framework 클라이언트 응용 프로그램 만들기](creating-the-dotnet-client-application-wcf-data-services-quickstart.md)

 OData 피드를 사용 하 고, 데이터를 Windows 컨트롤에 바인딩하고, 바인딩된 컨트롤의 데이터를 변경 하 고, 변경 내용을 데이터 서비스로 다시 전송 하는 WPF 앱을 만듭니다.

> [!NOTE]
> 완성된 퀵 스타트 버전의 프로젝트 파일은 [WCF Data Services Documentation Samples](https://go.microsoft.com/fwlink/?LinkId=179994) 페이지에서 다운로드할 수 있습니다.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [빠른 시작 시작](creating-the-data-service.md)

## <a name="see-also"></a>참고자료

- [ADO.NET Entity Framework](../adonet/ef/index.md)
