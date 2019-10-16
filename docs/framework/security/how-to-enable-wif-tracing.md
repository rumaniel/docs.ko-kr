---
title: '방법: WIF 추적 사용'
ms.date: 03/30/2017
ms.assetid: 271b6889-3454-46ff-96ab-9feb15e742ee
author: BrucePerlerMS
ms.openlocfilehash: 40349c5aac7634a515b40a9cc1ab5e75492600c4
ms.sourcegitcommit: a97ecb94437362b21fffc5eb3c38b6c0b4368999
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2019
ms.locfileid: "68971513"
---
# <a name="how-to-enable-wif-tracing"></a>방법: WIF 추적 사용

## <a name="applies-to"></a>적용 대상

- Microsoft® Windows® Identity Foundation(WIF)

- ASP.NET® Web Forms

## <a name="summary"></a>요약

이 방법은 ASP.NET 애플리케이션에서 WIF 추적을 사용하도록 설정하기 위한 자세한 단계별 프로시저를 제공합니다. 또한 추적 수신기 및 로그가 제대로 작동하는지 확인하기 위해 애플리케이션을 테스트하는 방법에 대한 지침을 제공합니다. 이 방법 설명에 보안 토큰 서비스(STS)를 만들기 위한 자세한 지침은 없으며, 그 대신 ID 및 액세스 도구와 함께 제공되는 개발 STS를 사용합니다. 개발 STS가 실제 인증을 수행하는 것은 아니며, 테스트 목적으로만 사용됩니다. 이 방법을 완료하려면 ID 및 액세스 도구를 설치해야 합니다. 다음 위치에서 다운로드할 수 있습니다. [Id 및 액세스 도구](https://go.microsoft.com/fwlink/?LinkID=245849)

> [!IMPORTANT]
> WS-Federation 프로토콜을 사용하는 수동 애플리케이션에 WIF 추적을 사용하면 애플리케이션이 DoS(서비스 거부) 공격에 노출되거나 악의적인 주체에게 정보가 공개될 가능성이 있습니다. 여기에는 수동 RP 및 수동 STS가 둘 다 포함됩니다. 따라서 프로덕션 환경에서는 수동 RP 또는 STS에 WIF 추적을 사용하지 않는 것이 좋습니다.

## <a name="contents"></a>목차

- 목표

- 개요

- 단계 요약

- 1단계 – 간단한 ASP.NET Web Forms 애플리케이션 만들기 및 추적 사용

- 2단계 - 솔루션 테스트

## <a name="objectives"></a>목표

- ID 및 액세스 도구에서 WIF 및 개발 STS를 사용하는 간단한 ASP.NET 애플리케이션 만들기

- 추적 사용 및 작동하는지 확인

## <a name="overview"></a>개요

추적을 사용하면 토큰, 쿠키, 클레임, 프로토콜 메시지 등을 포함하여 WIF에 관련된 다양한 문제를 디버그 및 해결할 수 있습니다. WIF 추적은 WCF 추적과 비슷합니다. 예를 들어 추적의 자세한 정도를 선택하여 중요 메시지에서 모든 메시지까지 모든 것을 표시할 수 있습니다. WIF 추적은 Service Trace Viewer 도구를 사용하여 볼 수 있는 **.xml** 파일 또는 **.svclog** 파일에서 생성될 수 있습니다. 이 도구는 컴퓨터에서 Windows SDK 설치 경로의 **bin** 디렉터리에 있습니다. 예를 들면 다음과 같습니다. **C:\Program Files\Microsoft SDKs\Windows\v7.1\Bin\SvcTraceViewer.exe**.

## <a name="summary-of-steps"></a>단계 요약

- 1단계 – 간단한 ASP.NET Web Forms 애플리케이션 만들기 및 추적 사용

- 2단계 - 솔루션 테스트

## <a name="step-1--create-a-simple-aspnet-web-forms-application-and-enable-tracing"></a>1단계 – 간단한 ASP.NET Web Forms 애플리케이션 만들기 및 추적 사용

이 단계에서는 새 ASP.NET Web Forms 애플리케이션을 만들고 *Web.config* 파일을 수정하여 추적을 사용하도록 설정합니다.

### <a name="to-create-a-simple-aspnet-application"></a>간단한 ASP.NET 애플리케이션을 만들려면

1. Visual Studio를 시작하고 **파일**, **새로 만들기**, **프로젝트**를 차례로 클릭합니다.

2. **새 프로젝트** 창에서 **ASP.NET Web Forms 응용 프로그램**을 클릭합니다.

3. **이름**에서 `TestApp`을 입력하고 **확인**을 누릅니다.

4. **솔루션 탐색기**에서 **TestApp** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **ID 및 액세스**를 선택합니다.

5. **ID 및 액세스** 창이 나타납니다. **공급자**에서 **로컬 개발 STS로 응용 프로그램 테스트**를 선택한 다음 **적용**을 클릭합니다.

6. 다음과 같이 **C:** 드라이브의 루트에 명명 된 **로그** 에 새 폴더를 만듭니다. **C:\logs**

7. 다음 **\<system.diagnostics>** 요소를 *Web.config* 구성 파일의 닫는 **\</configSections>** 요소 바로 뒤에 추가합니다. 다음과 같이 표시됩니다.

    ```xml
    <configuration>
        <configSections>
            ...
        </configSections>
        <system.diagnostics>
            <sources>
                <source name="System.IdentityModel" switchValue="Verbose">
                    <listeners>
                        <add name="xml" type="System.Diagnostics.XmlWriterTraceListener" initializeData="C:\logs\WIF.xml" />
                    </listeners>
                </source>
            </sources>
            <trace autoflush="true" />
        </system.diagnostics>
    ```

    > [!NOTE]
    > **initializeData** 특성에 지정된 디렉터리 위치는 로깅을 시작하기 전에 이미 존재해야 합니다. 해당 위치가 없으면 로그가 만들어지지 않습니다.

     위의 구성 설정은 WIF에 대한 **동사** 추적을 사용하도록 설정하고 결과 로그를 **C:logsWIF.xml** 파일에 저장합니다.

## <a name="step-2--test-your-solution"></a>2단계 - 솔루션 테스트

이 단계에서는 WIF 사용 가능 ASP.NET 애플리케이션을 테스트하여 로그가 기록되고 있는지 확인합니다.

### <a name="to-test-your-wif-enabled-aspnet-application-for-successful-tracing"></a>성공적인 추적을 위해 WIF 사용 가능 ASP.NET 애플리케이션을 테스트하려면

1. **F5** 키를 눌러 솔루션을 실행합니다. 기본 ASP.NET 홈페이지가 표시되고 개발 STS에서 반환되는 기본 사용자인 사용자 이름 *Terry*로 자동으로 인증되어야 합니다.

2. 브라우저 창을 닫고 **C:\logs** 폴더로 이동합니다. 텍스트 편집기를 사용하여 **C:\logs\WIF.xml** 파일을 엽니다.

3. **WIF.xml** 파일을 검사하고 **\<E2ETraceEvent>** 로 시작하는 항목이 포함되어 있는지 확인합니다. 이러한 추적에는 **\<TraceRecord>** 요소와 추적된 작업에 대한 설명이 포함됩니다(예: **SecurityToken 유효성 검사**).
