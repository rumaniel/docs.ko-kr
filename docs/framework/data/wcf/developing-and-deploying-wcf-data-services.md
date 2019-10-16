---
title: WCF Data Services 개발 및 배포
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, developing
- WCF Data Services, deploying
- deploying [WCF Data Services
- developing applications [WCF Data Services]
ms.assetid: 6557c0e3-5aea-4f6e-bc14-77ad317a168b
ms.openlocfilehash: d7ddae58874c69468eb6ff1762db9083897b1acd
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854077"
---
# <a name="develop-and-deploy-wcf-data-services"></a>WCF Data Services 개발 및 배포

이 항목에서는 WCF Data Services 개발 및 배포에 대 한 정보를 제공 합니다. WCF Data Services에 대 한 자세한 기본 정보는 [시작](getting-started-with-wcf-data-services.md) 및 [개요](wcf-data-services-overview.md)를 참조 하세요.

## <a name="develop-wcf-data-services"></a>WCF Data Services 개발

WCF Data Services를 사용 하 여를 지 원하는 [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)]데이터 서비스를 만들 때는 개발 과정에서 다음과 같은 기본 작업을 수행 해야 합니다.

1. **데이터 모델 정의**

     WCF Data Services은 다양 한 데이터 원본의 데이터를 기반으로 하는 데이터 모델을 관계형 데이터베이스에서 런타임에 바인딩된 데이터 형식으로 정의할 수 있도록 하는 다양 한 데이터 서비스 공급자를 지원 합니다. 자세한 내용은 [데이터 서비스 공급자](data-services-providers-wcf-data-services.md)합니다.

2. **데이터 서비스 만들기**

     가장 기본적인 데이터 서비스는 <xref:System.Data.Services.DataService%601> 클래스에서 상속하는 클래스를 엔터티 컨테이너의 네임스페이스로 정규화된 이름인 `T` 형식으로 노출합니다. 자세한 내용은 [Defining WCF Data Services](defining-wcf-data-services.md)의 개발 및 배포에 대한 정보를 제공합니다.

3. **데이터 서비스 구성**

     기본적으로 WCF Data Services는 엔터티 컨테이너에 의해 노출 되는 리소스에 대 한 액세스를 사용 하지 않도록 설정 합니다. <xref:System.Data.Services.DataServiceConfiguration> 인터페이스를 사용 하면 리소스 및 서비스 작업에 대 한 액세스를 구성 하 고, 지원 되는 버전의 OData를 지정 하 고, 일괄 처리 동작 또는 반환할 수 있는 최대 엔터티 수와 같은 다른 서비스 전체 동작을 정의할 수 있습니다. 단일 응답 피드에 제공 됩니다. 자세한 내용은 [데이터 서비스 구성](configuring-the-data-service-wcf-data-services.md)합니다.

이 항목에서는 Visual Studio를 사용 하 여 데이터 서비스를 개발 하 고 배포 하는 방법을 주로 다룹니다. 데이터를 OData 피드로 노출 하는 WCF Data Services에서 제공 하는 유연성에 대 한 자세한 내용은 [WCF Data Services 정의](defining-wcf-data-services.md)를 참조 하세요.

### <a name="choose-a-development-web-server"></a>개발 웹 서버 선택

Visual Studio 2015을 사용 하 여 WCF 데이터 서비스를 ASP.NET 응용 프로그램 또는 ASP.NET 웹 사이트로 개발 하는 경우 개발 하는 동안 데이터 서비스를 실행할 웹 서버를 선택할 수 있습니다. 다음 웹 서버를 Visual Studio와 통합 하 여 로컬 컴퓨터에서 데이터 서비스를 쉽게 테스트 하 고 디버그할 수 있습니다.

1. **로컬 IIS 서버**

     인터넷 정보 서비스 (IIS)에서 실행 되는 ASP.NET 응용 프로그램 또는 ASP.NET 웹 사이트인 데이터 서비스를 만들 때 로컬 컴퓨터에서 IIS를 사용 하 여 데이터 서비스를 개발 하 고 테스트 하는 것이 좋습니다. IIS에서 데이터 서비스를 실행하면 디버깅하는 동안 HTTP 요청을 쉽게 추적할 수 있습니다. 또한 IIS에서 데이터 서비스에 필요한 파일, 데이터베이스 및 기타 리소스에 액세스하는 데 필요한 권한을 미리 결정할 수도 있습니다. IIS에서 데이터 서비스를 실행 하려면 IIS와 Windows Communication Foundation (WCF)를 모두 올바르게 설치 및 구성 하 고 파일 시스템 및 데이터베이스에 있는 IIS 계정에 액세스 권한을 부여 해야 합니다. 자세한 내용은 [방법: IIS](how-to-develop-a-wcf-data-service-running-on-iis.md)에서 실행 되는 WCF Data Service를 개발 합니다.

    > [!NOTE]
    > 개발 환경을 사용 하 여 로컬 IIS 서버를 구성 하려면 관리자 권한으로 Visual Studio를 실행 해야 합니다.

2. **Visual Studio 개발 서버**

     Visual Studio에는 기본 제공 웹 서버 ASP.NET 프로젝트의 기본 웹 서버인 Visual Studio 개발 서버이 포함 되어 있습니다. 이 웹 서버는 개발 중에 로컬 컴퓨터에서 ASP.NET 프로젝트를 실행 하도록 설계 되었습니다. [WCF Data Services 빠른](quickstart-wcf-data-services.md) 시작에서는 Visual Studio 개발 서버에서 실행 되는 데이터 서비스를 만드는 방법을 보여 줍니다.

     Visual Studio 개발 서버를 사용 하 여 데이터 서비스를 개발 하는 경우 다음과 같은 제한 사항을 알고 있어야 합니다.

    - 이 서버는 로컬 컴퓨터에서만 액세스할 수 있습니다.

    - 이 서버는 HTTP 메시지의 기본 포트인 특정 포트(포트 80 제외)와 `localhost` 에서 수신 대기합니다. 자세한 내용은 [Visual Studio의 ASP.NET 웹 프로젝트에 대한 웹 서버](https://docs.microsoft.com/previous-versions/aspnet/58wxa9w5(v=vs.120))를 참조하세요.

    - 이 서버는 현재 사용자 계정의 컨텍스트에서 데이터 서비스를 실행합니다. 예를 들어 관리자 수준의 사용자로를 실행 하는 경우 Visual Studio 개발 서버에서 실행 되는 데이터 서비스에는 관리자 수준의 권한이 있습니다. 따라서 데이터 서비스가 IIS 서버에 배포된 리소스 중 액세스 권한이 없는 리소스에도 액세스할 수 있습니다.

    - 이 서버에는 인증과 같은 IIS의 추가 기능이 포함되어 있지 않습니다.

    - 이 서버는 데이터 서비스에서 많은 이진 데이터에 액세스할 때 WCF Data Services 클라이언트가 기본적으로 전송 하는 청크 분할 HTTP 스트림을 처리할 수 없습니다. 자세한 내용은 [스트리밍 공급자](streaming-provider-wcf-data-services.md)합니다.

    - 키 값의 WCF Data Services에서이 문자를 지`.`원하는 경우에도이 서버는 URL에서 마침표 () 문자를 처리 하는 문제가 있습니다.

    > [!TIP]
    > Visual Studio 개발 서버를 사용 하 여 개발 중에 데이터 서비스를 테스트할 수 있지만 IIS를 실행 하는 웹 서버에 배포한 후 다시 테스트 해야 합니다.

3. **Microsoft Azure 개발 환경**

     Microsoft Azure Tools for Visual Studio에는 Visual Studio에서 Windows Azure 서비스를 개발 하기 위한 통합 된 도구 집합이 포함 되어 있습니다. 이 도구를 사용하면 Microsoft Azure에 배포할 수 있는 데이터 서비스를 개발하고, 배포하기 전에 로컬 컴퓨터에서 데이터 서비스를 테스트할 수 있습니다. Visual Studio를 사용 하 여 Microsoft Azure 플랫폼에서 실행 되는 데이터 서비스를 개발할 때 이러한 도구를 사용 합니다. [Microsoft 다운로드 센터](https://go.microsoft.com/fwlink/?LinkID=201848)에서 Visual Studio 용 Windows Azure 도구를 다운로드할 수 있습니다. Windows Azure에서 실행 되는 데이터 서비스를 개발 하는 방법에 대 한 자세한 내용은 [Windows azure에서 OData 서비스 배포](https://go.microsoft.com/fwlink/?LinkId=201847)게시물을 참조 하십시오.

### <a name="development-tips"></a>개발 팁

데이터 서비스를 개발할 때 다음 사항을 고려해야 합니다.

- 사용자를 인증하거나 특정 사용자의 액세스를 제한하려는 경우 데이터 서비스의 보안 요구 사항을 확인해야 합니다. 자세한 내용은 [Securing WCF Data Services](securing-wcf-data-services.md)을 참조하세요.

- HTTP 검사 프로그램은 요청 및 응답 메시지의 내용을 검사할 수 있도록 하여 데이터 서비스를 디버깅할 때 아주 유용할 수 있습니다. 원시 패킷을 표시할 수 있는 네트워크 패킷 분석기를 사용하여 데이터 서비스와 주고받는 HTTP 요청 및 응답을 검사할 수 있습니다.

- 데이터 서비스를 디버깅할 때 일반 작업을 수행 하는 것 보다 데이터 서비스에서 오류에 대 한 자세한 정보를 얻을 수 있습니다. <xref:System.Data.Services.DataServiceConfiguration.UseVerboseErrors%2A> 에서 <xref:System.Data.Services.DataServiceConfiguration> 속성을 `true` 로 설정하고 데이터 서비스 클래스에서 <xref:System.ServiceModel.Description.ServiceDebugBehavior.IncludeExceptionDetailInFaults%2A> 특성의 <xref:System.ServiceModel.Description.ServiceDebugBehavior> 속성을 `true`로 설정하여 데이터 서비스에서 추가 오류 정보를 가져올 수 있습니다. 자세한 내용은 [디버깅 후 WCF Data Services](https://go.microsoft.com/fwlink/?LinkId=201868)를 참조 하세요. WCF에서 추적을 사용 하도록 설정 하 여 HTTP 메시징 계층에서 발생 하는 예외를 볼 수도 있습니다. 자세한 내용은 [Configuring Tracing](../../wcf/diagnostics/tracing/configuring-tracing.md)을 참조하세요.

- 데이터 서비스는 일반적으로 ASP.NET 응용 프로그램 프로젝트로 개발 되지만 Visual Studio에서 ASP.NET 웹 사이트 프로젝트로 데이터 서비스를 만들 수도 있습니다. 두 프로젝트 형식 간의 차이점에 대 한 자세한 내용은 [웹 응용 프로그램 프로젝트와 Visual Studio의 웹 사이트 프로젝트](https://docs.microsoft.com/previous-versions/aspnet/dd547590(v=vs.110))를 참조 하세요.

- Visual Studio에서 **새 항목 추가** 대화 상자를 사용 하 여 데이터 서비스를 만들면 데이터 서비스는 IIS의 ASP.NET에서 호스팅됩니다. ASP.NET 및 IIS는 데이터 서비스의 기본 호스트 이지만 다른 호스팅 옵션도 지원 됩니다. 자세한 내용은 [데이터 서비스 호스팅](hosting-the-data-service-wcf-data-services.md)합니다.

## <a name="deploy-wcf-data-services"></a>WCF Data Services 배포

WCF Data Services에서는 데이터 서비스를 호스트하는 프로세스를 유연성 있게 선택할 수 있도록 합니다. Visual Studio를 사용 하 여 데이터 서비스를 다음 플랫폼에 배포할 수 있습니다.

- **IIS에서 호스트되는 웹 서버**

    데이터 서비스를 ASP.NET 프로젝트로 개발 하는 경우 표준 ASP.NET 배포 프로세스를 사용 하 여 IIS 웹 서버에 배포할 수 있습니다.  Visual Studio는 배포 중인 데이터 서비스를 호스팅하는 ASP.NET 프로젝트의 종류에 따라 ASP.NET에 대해 다음과 같은 배포 기술을 제공 합니다.

  - **ASP.NET 웹 응용 프로그램을 위한 배포 기술**

    - [방법: Visual Studio에서 웹 배포 패키지 만들기](https://docs.microsoft.com/previous-versions/aspnet/dd465323(v=vs.110))

    - [방법: Visual Studio에서 한 번 클릭으로 게시를 사용 하 여 웹 프로젝트 배포](https://docs.microsoft.com/previous-versions/aspnet/dd465337(v=vs.110))

  - **ASP.NET 웹 사이트를 위한 배포 기술**

    - [방법: 웹 사이트 복사 도구를 사용 하 여 웹 사이트 파일 복사](https://docs.microsoft.com/previous-versions/aspnet/c95809c0(v=vs.100))

    - [방법: 웹 사이트 게시](https://docs.microsoft.com/previous-versions/aspnet/20yh9f1b(v=vs.100))

    - [연습: XCOPY를 사용 하 여 ASP.NET 웹 응용 프로그램 배포](https://docs.microsoft.com/previous-versions/aspnet/f735abw9(v=vs.100))

     ASP.NET 응용 프로그램의 배포 옵션에 대 한 자세한 내용은 [Visual Studio 및 ASP.NET에 대 한 웹 배포 개요](https://docs.microsoft.com/previous-versions/aspnet/dd394698(v=vs.110))를 참조 하세요.

    > [!TIP]
    > 데이터 서비스를 IIS에 배포하기 전에 IIS가 실행 중인 웹 서버로의 배포를 테스트했는지 확인해야 합니다. 자세한 내용은 [방법: IIS](how-to-develop-a-wcf-data-service-running-on-iis.md)에서 실행 되는 WCF Data Service를 개발 합니다.

- **Windows Azure**

     Microsoft Azure Tools for Visual Studio를 사용 하 여 Windows Azure에 데이터 서비스를 배포할 수 있습니다. [Microsoft 다운로드 센터](https://go.microsoft.com/fwlink/?LinkID=201848)에서 Visual Studio 용 Windows Azure 도구를 다운로드할 수 있습니다. Windows Azure에 데이터 서비스를 배포 하는 방법에 대 한 자세한 내용은 [Windows azure에서 OData 서비스 배포](https://go.microsoft.com/fwlink/?LinkId=201847)게시물을 참조 하십시오.

### <a name="deployment-considerations"></a>배포 고려 사항

데이터 서비스를 배포할 때 다음 사항을 고려해야 합니다.

- Entity Framework 공급자를 사용 하는 데이터 서비스를 배포 하 여 SQL Server 데이터베이스에 액세스 하는 경우 데이터 서비스 배포와 함께 데이터 구조, 데이터 또는 둘 다를 전파 해야 할 수도 있습니다. Visual Studio는 대상 데이터베이스에서이 작업을 수행 하기 위해 스크립트 (.sql 파일)를 자동으로 만들 수 있으며, 이러한 스크립트를 ASP.NET 응용 프로그램의 웹 배포 패키지에 포함할 수 있습니다. 자세한 내용은 [방법: 웹 응용 프로그램 프로젝트](https://docs.microsoft.com/previous-versions/dd465343(v=vs.100))를 사용 하 여 데이터베이스를 배포 합니다. ASP.NET 웹 사이트의 경우 Visual Studio에서 **데이터베이스 게시 마법사** 를 사용 하 여이 작업을 수행할 수 있습니다. 자세한 내용은 [SQL Database 게시](https://docs.microsoft.com/previous-versions/aspnet/bb907585(v=vs.100))를 참조 하십시오.

- WCF Data Services에는 기본 WCF 구현이 포함 되어 있기 때문에 windows Server AppFabric을 사용 하 여 Windows Server에서 실행 되는 IIS에 배포 된 데이터 서비스를 모니터링할 수 있습니다. Windows Server AppFabric을 사용 하 여 데이터 서비스를 모니터링 하는 방법에 대 한 자세한 내용은 [Windows Server appfabric을 사용 하 여 WCF Data Services 추적](https://go.microsoft.com/fwlink/?LinkID=202005)게시물을 참조 하세요.

## <a name="see-also"></a>참고자료

- [데이터 서비스 호스팅](hosting-the-data-service-wcf-data-services.md)
- [WCF Data Services 보안](securing-wcf-data-services.md)
- [WCF Data Services 정의](defining-wcf-data-services.md)
