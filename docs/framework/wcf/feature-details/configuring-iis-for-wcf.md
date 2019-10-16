---
title: Windows Communication Foundation에 대해 Internet Information Services 7.0 구성
ms.date: 03/30/2017
ms.assetid: 1050d395-092e-44d3-b4ba-66be3b039ffb
ms.openlocfilehash: 6962ed1dccca6db2e55554459742adab210585ef
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64654987"
---
# <a name="configuring-internet-information-services-70-for-windows-communication-foundation"></a>Windows Communication Foundation에 대해 Internet Information Services 7.0 구성

IIS(인터넷 정보 서비스) 7.0은 필요한 구성 요소를 선택적으로 설치할 수 있는 모듈형 디자인입니다. 이러한 디자인은 [!INCLUDE[wv](../../../../includes/wv-md.md)]에 도입된 새로운 매니페스트 기반의 컴포넌트화 기술을 바탕으로 합니다. 독립적으로 설치 될 수 있는 IIS 7.0의 40 개 이상의 독립 실행형 기능 구성 요소가 있습니다. 따라서 IT 전문가는 필요에 따라 편리하게 설치를 사용자 지정할 수 있습니다. 이 항목에서는 IIS 7.0을 사용 하 여 Windows Communication Foundation (WCF)를 사용 하 여에 대 한 구성 필수 구성 요소를 결정 하는 방법을 설명 합니다.

## <a name="minimal-installation-installing-was"></a>최소 설치: WAS를 설치합니다.
 전체 IIS 7.0 패키지의 최소 설치는 Windows 프로세스 활성화 서비스 (WAS)를 설치 하는 것입니다. 가 독립 실행형 기능 이며 모두에 사용할 수 있는 IIS 7.0에서 기능만 [!INCLUDE[wv](../../../../includes/wv-md.md)] 운영 체제 (Home Basic, Home Premium, Business 및 Ultimate 및 Enterprise).

 제어판에서 클릭 **프로그램** 클릭 하 고 **설정할 Windows 기능 사용 / 해제** 아래에 나열 된 **프로그램 및 기능**, WAS 구성 요소에 표시 됩니다는 다음 그림과 같이 목록입니다.

 ![기능 켜기 / 끄기 대화](../../../../docs/framework/wcf/feature-details/media/wcfc-turnfeaturesonoroffs.gif "wcfc_TurnFeaturesOnOrOffs")

 이 기능에는 다음과 같은 하위 구성 요소가 있습니다.

- .NET 환경

- 구성 API

- 프로세스 모델

 만 WAS의 루트 노드를 선택 하는 경우는 **프로세스 모델** 하위 노드는 기본적으로 선택 됩니다. 이 설치에서는 웹 서버에 대한 지원이 없으므로 WAS만 설치됩니다.

 WCF 또는 ASP.NET 응용 프로그램 작업을 하려면 다음을 확인 합니다 **.NET 환경** 확인란을 선택 합니다. 즉, WCF 및 ASP.NET 잘 작동 해야 하는 모든 WAS 구성 요소입니다. 이러한 구성 요소는 일단 설치되면 자동으로 선택됩니다.

## <a name="iis-70-default-installation"></a>IIS 7.0: 기본 설치
 확인 하 여 합니다 **인터넷 정보 서비스** 하위 노드 중 일부 기능에는 다음 그림에 나와 있는 것 처럼 자동으로 선택 됩니다.

 ![기본 IIS 7.0 기능에 대 한 설정](../../../../docs/framework/wcf/feature-details/media/wcfc-turningfeaturesonoroff2.gif "wcfc_TurningFeaturesOnOrOff2")

 IIS 7.0의 기본 설치입니다. 이 설치를 사용 하 여 서비스 정적 콘텐츠 (예: HTML 페이지 및 기타 콘텐츠)를 IIS 7.0을 사용할 수 있습니다. 그러나 ASP.NET 또는 CGI 응용 프로그램 또는 WCF 서비스를 호스팅하는 실행할 수 없습니다.

## <a name="iis-70-installation-with-aspnet-support"></a>IIS 7.0: ASP.NET 지원과 함께 설치
 ASP.NET IIS 7.0에서 작동 하도록 ASP.NET을 설치 해야 합니다. 확인 한 후 **ASP.NET**, 화면이 다음 그림과 같이 표시 됩니다.

 ![Asp.NET 필수 설정](../../../../docs/framework/wcf/feature-details/media/wcfc-trunfeaturesonoroff3s.gif "wcfc_TrunFeaturesOnOrOFf3s")

 이 IIS 7.0에서 작동 하도록 WCF와 ASP.NET 응용 프로그램에 대 한 최소 환경입니다.

## <a name="iis-70-installation-with-iis-60-compatibility-components"></a>IIS 7.0: IIS 6.0 호환성 구성 요소를 사용 하 여 설치
 Visual Studio 2005 또는 일부 기타 자동화 스크립트나 도구 (예: Adsutil.vbs) IIS 6.0 메타 베이스 API를 사용 하는 가상 응용 프로그램을 구성 하는 시스템에 IIS 7.0을 설치 하는 경우 IIS 6.0를 확인 하는 확인 **스크립팅 도구**. IIS 6.0의 다른 하위 노드에 자동으로 검사 **관리 호환성**합니다. 다음 그림에서는이 작업이 완료 되 면 화면을 보여 줍니다.

 ![IIS 6.0 관리 호환성 설정을](../../../../docs/framework/wcf/feature-details/media/scfc-turnfeaturesonoroff5s.gif "scfc_TurnFeaturesOnOrOff5s")

 이 설치 된 경우 웹에서 IIS 7.0, ASP.NET 및 WCF 기능과 사용할 수 있는 샘플을 사용 하는 데 필요한 모든 것

## <a name="request-limits"></a>요청 제한
 IIS 7이 설치된 [!INCLUDE[wv](../../../../includes/wv-md.md)]에서 `maxUri` 및 `maxQueryStringSize` 설정의 기본값이 변경되었습니다. 기본적으로 IIS 7.0의 요청 필터링은 URL 길이로 4096자를 허용하며 쿼리 문자열 길이로 2048자를 허용합니다. 이러한 기본값을 변경하려면 다음 XML을 App.config 파일에 추가합니다.

```xml
 <system.webServer>
    <security>
        <requestFiltering>
            <requestLimits maxUrl="8192" maxQueryString="8192" />
        </requestFiltering>
    </security>
 </system.webServer>
 ```

## <a name="see-also"></a>참고자료

- [WAS Activation 아키텍처](../../../../docs/framework/wcf/feature-details/was-activation-architecture.md)
- [WCF와 함께 사용하도록 WAS 구성](../../../../docs/framework/wcf/feature-details/configuring-the-wpa--service-for-use-with-wcf.md)
- [방법: 설치 하 고 WCF Activation 구성 요소를 구성 합니다.](../../../../docs/framework/wcf/feature-details/how-to-install-and-configure-wcf-activation-components.md)
- [Windows Server App Fabric 호스팅 기능](https://go.microsoft.com/fwlink/?LinkId=201276)
