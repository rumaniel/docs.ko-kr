---
title: WCF Web Service 참조 추가
description: .NET Framework 프로젝트용 서비스 참조 추가와 유사하게, .NET Core 및 ASP.NET Core 프로젝트 기능을 추가하는 Microsoft WCF Web Service Reference Provider 도구에 대한 개요입니다.
author: mlacouture
ms.date: 04/19/2018
ms.custom: mvc, seodec18
ms.openlocfilehash: 11a18161db0fde522442e2412c4522811c5dd40a
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70926455"
---
# <a name="use-the-wcf-web-service-reference-provider-tool"></a>WCF Web Service Reference Provider 도구 사용

지난 몇 년 동안, 많은 Visual Studio 개발자가 .NET Framework 프로젝트에서 웹 서비스에 액세스해야 할 때 제공된 [**서비스 참조 추가**](/visualstudio/data-tools/how-to-add-update-or-remove-a-wcf-data-service-reference) 도구를 통해 생산성을 향상시킬 수 있었습니다.  **WCF Web Service Reference** 도구는 .NET Core 및 ASP.NET Core 프로젝트에 대한 서비스 참조 추가 기능과 같은 환경을 제공하는 Visual Studio 연결된 서비스 확장입니다. 이 도구는 현재 솔루션, 네트워크 위치 또는 WSDL 파일의 웹 서비스에서 메타 데이터를 검색하고, 해당 웹 서비스를 액세스하는 데 사용할 수 있는 WCF(Windows Communication Foundation) 클라이언트 프록시 코드가 포함된 .NET Core 호환 소스 파일을 생성합니다.

> [!IMPORTANT]
> 신뢰할 수 있는 원본의 서비스만 참조해야 합니다. 신뢰할 수 없는 원본에서 참조를 추가하면 보안이 손상될 수 있습니다.

## <a name="prerequisites"></a>전제 조건

* [Visual Studio 2017 15.5](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs) 이상 버전

## <a name="how-to-use-the-extension"></a>확장을 사용하는 방법

> [!NOTE]
> **WCF Web Service Reference** 옵션은 다음과 같은 프로젝트 템플릿을 사용하여 만든 프로젝트에 적용할 수 있습니다.
>
> * **Visual C#**  >  **.NET Core**
> * **Visual C#**  >  **.NET Standard**
> * **Visual C#**  > **Web** > **ASP.NET Core Web Application**

이 문서에서는 **ASP.NET Core 웹 애플리케이션** 프로젝트 템플릿을 예로 사용하여 WCF 서비스 참조를 프로젝트에 추가하는 과정을 안내합니다.

1. 솔루션 탐색기에서 프로젝트의 **연결된 서비스** 노드를 두 번 클릭합니다(.NET Core 또는 .NET Standard 프로젝트의 경우 이 옵션은 솔루션 탐색기에서 프로젝트의 **종속성** 노드를 마우스 오른쪽 단추로 클릭할 때 사용 가능함).

    다음 이미지와 같이 **연결된 서비스** 페이지가 표시됩니다.

    ![.NET Core용 Visual Studio 연결된 서비스 탭](./media/wcf-web-service-reference-guide/wcfcs-ConnectedServicesPage.png)

2. **연결된 서비스** 페이지에서 **Microsoft WCF Web Service Reference Provider**를 클릭합니다. 그러면 **WCF Web Service Reference 구성** 마법사가 나타납니다.

    ![.NET Core용 Visual Studio 서비스 엔드포인트 탭](./media/wcf-web-service-reference-guide/wcfcs-ServiceEndpointPage.png)

3. 서비스를 선택합니다.

    3a. **WCF Web Service Reference 구성** 마법사 내에서 사용 가능한 여러 서비스 검색 옵션이 있습니다.

     * 현재 솔루션에 정의된 서비스를 검색하려면 **검색** 단추를 클릭합니다.
     * 지정된 주소에서 호스트되는 서비스를 검색하려면 **주소** 상자에 서비스 URL을 입력하고 **이동** 단추를 클릭합니다.
     * 웹 서비스 메타데이터 정보를 포함하는 WSDL 파일을 선택하려 **찾아보기** 단추를 클릭합니다.

    3b. **서비스** 상자의 검색 결과 목록에서 서비스를 선택합니다. 필요한 경우 해당 **네임스페이스** 입력란에 생성된 코드에 대한 네임스페이스를 입력합니다.

    3c. **다음** 단추를 클릭하면 **데이터 형식 옵션** 및 **클라이언트 옵션** 페이지가 열립니다. 또는 **마침** 단추를 클릭하고 기본 옵션을 사용합니다.

4. **데이터 형식 옵션** 양식을 사용하여 생성된 서비스 참조 구성 설정을 구체화할 수 있습니다.

    ![.NET Core용 Visual Studio 데이터 형식 옵션 탭](./media/wcf-web-service-reference-guide/wcfcs-DataTypesPage.png)

    > [!NOTE]
    > **참조된 어셈블리의 형식 재사용** 확인란 옵션은 서비스 참조 코드 생성에 필요한 데이터 형식이 프로젝트의 참조 어셈블리 중 하나에 정의될 때 유용합니다.  컴파일 시간 형식 충돌 또는 런타임 문제를 피하기 위해 기존 데이터 형식을 다시 사용하는 것이 중요합니다.

    프로젝트 종속성 및 기타 시스템 성능 요소의 수에 따라 형식 정보가 로드되는 동안 지연이 있을 수 있습니다. **참조된 어셈블리의 형식 재사용** 확인란을 선택 하면 로드 중에 **마침** 단추가 비활성화됩니다.

5. 완료했으면 **마침**을 클릭합니다.

진행률을 표시하면서 도구가 다음을 수행합니다.

* WCF 서비스에서 메타데이터를 다운로드합니다.
* *reference.cs*라는 파일에 서비스 참조 코드를 생성하고 **연결된 서비스** 노드 아래의 프로젝트에 추가합니다.
* 대상 플랫폼에서 컴파일 및 실행하는 데 필요한 NuGet 패키지 참조로 프로젝트 파일(.csproj)을 업데이트합니다.

![Visual Studio 진행률 창](./media/wcf-web-service-reference-guide/wcfcs-ProgressWindow.png)

이러한 과정을 완료하면 생성된 WCF 클라이언트 형식의 인스턴스를 만들고 서비스 작업을 호출할 수 있습니다.

## <a name="next-steps"></a>다음 단계

### <a name="feedback--questions"></a>사용자 의견 및 질문

질문이나 의견이 있는 경우 [GitHub에서 문제를 엽니다](https://github.com/dotnet/wcf/issues/new). 또한 [GitHub의 WCF 리포지토리에서](https://github.com/dotnet/wcf/issues?utf8=%E2%9C%93&q=is:issue%20label:tooling) 기존 질문이나 문제를 검토할 수 있습니다.

### <a name="release-notes"></a>릴리스 정보

* 알려진 문제를 비롯한 업데이트된 릴리스 정보는 [릴리스 정보](https://github.com/dotnet/wcf/blob/master/release-notes/WCF-Web-Service-Reference-notes.md)를 참조하세요.
