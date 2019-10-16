---
title: ASP.NET 클라이언트에서 데이터 바인딩
ms.date: 03/30/2017
ms.assetid: 68b49fa6-94e7-4d4c-a34e-902a2b3770b6
ms.openlocfilehash: c5faeb99fa8fb153f1ab74f5f00786355af50016
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70045089"
---
# <a name="data-binding-in-an-aspnet-client"></a>ASP.NET 클라이언트에서 데이터 바인딩
이 샘플에서는 Web Forms 응용 프로그램에서 WCF (일반 Windows Communication Foundation) 서비스에 의해 반환 된 데이터를 바인딩하는 방법을 보여 줍니다.  
  
> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.  
  
 이 샘플에서는 요청-회신 통신 패턴을 정의하는 계약을 구현하는 서비스를 보여 줍니다. 이 샘플은 브라우저에서 액세스할 수 있는 클라이언트 Web Forms 응용 프로그램과 인터넷 정보 서비스 (IIS)에서 호스팅하는 WCF 서비스를 구성 합니다.  
  
 이 서비스는 요청-회신 통신 패턴을 정의하는 계약을 구현합니다. 계약은 `IWeatherService`라는 작업을 노출시키는 `GetWeatherData` 인터페이스에 의해 정의됩니다. 이 작업은 도시 배열을 사용하여 도시의 최고 및 최저 예상 기온을 나타내는 `WeatherData` 개체의 배열을 반환합니다.  
  
 ASP.NET 페이지에는 서비스에서 반환 하는 데이터의 그래픽 표현을 포함 하는 DataGrid 웹 컨트롤이 정의 되어 있습니다. .Aspx 페이지의 코드는 날씨 데이터에 대해 WCF 서비스를 호출 하 고 데이터를 개체의 `WeatherData` 배열에 반환 합니다. DataGrid는 `DataSource` 속성을 이 배열로 설정하여 데이터를 가져올 위치를 지정합니다. DataGrid의 `DataBind` 메서드를 호출함과 동시에 데이터 바인딩이 발생하며, 이 코드는 모두 내에 포함 되어 있습니다.`aspx` 페이지의 `Page_Load` 메서드를 사용 하 여 사용자가 브라우저 페이지를 새로 고칠 때마다 데이터가 DataGrid에서 업데이트 됩니다.  
  
### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.  
  
2. C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.  
  
3. 이 샘플의 클라이언트는 개발 웹 서버에서 실행되는 웹 사이트입니다. 개발 웹 서버를 시작 하려면 명령 프롬프트 `%SystemDrive%\Program Files\Common Files\Microsoft Shared\DevServer\9.0\WebDev.WebServer.EXE" /port:8000 /path:<WebFormsSamplePath>\CS\client /vpath:/client`에 다음을 입력 합니다. 그런 다음로 `http://localhost:8000/client`이동 합니다. 이 샘플을 여러 컴퓨터에서 실행하려면 클라이언트의 Web.config 파일에서 `localhost`에 대한 모든 참조를 서버의 컴퓨터 이름으로 바꿉니다.  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Scenario\DataBinding\WebForms`
