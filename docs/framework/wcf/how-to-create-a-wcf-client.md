---
title: '자습서: Windows Communication Foundation 클라이언트 만들기'
ms.date: 03/19/2019
helpviewer_keywords:
- clients [WCF], running
- WCF clients [WCF], running
ms.assetid: a67884cc-1c4b-416b-8c96-5c954099f19f
ms.openlocfilehash: ddb5167c7f71a263377fb465ec44ee21057fbf4a
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70928901"
---
# <a name="tutorial-create-a-windows-communication-foundation-client"></a>자습서: Windows Communication Foundation 클라이언트 만들기

이 자습서에서는 WCF (기본 Windows Communication Foundation) 응용 프로그램을 만드는 데 필요한 5 가지 작업 중 네 번째 작업에 대해 설명 합니다. 자습서에 대 한 개요를 보려면 [자습서: Windows Communication Foundation 응용 프로그램](getting-started-tutorial.md)을 시작 하세요.

WCF 응용 프로그램을 만들기 위한 다음 작업은 WCF 서비스에서 메타 데이터를 검색 하 여 클라이언트를 만드는 것입니다. Visual Studio를 사용 하 여 서비스의 MEX 끝점에서 메타 데이터를 가져오는 서비스 참조를 추가 합니다. 그러면 Visual Studio에서 사용자가 선택한 언어로 클라이언트 프록시에 대 한 관리 되는 소스 코드 파일을 생성 합니다. 또한 클라이언트 구성 파일 (*app.config*)을 만듭니다. 이 파일을 사용 하면 클라이언트 응용 프로그램이 끝점에서 서비스에 연결할 수 있습니다. 

> [!NOTE]
> Visual Studio의 클래스 라이브러리 프로젝트에서 WCF 서비스를 호출 하는 경우 **서비스 참조 추가** 기능을 사용 하 여 프록시 및 연결 된 구성 파일을 자동으로 생성 합니다. 그러나 클래스 라이브러리 프로젝트에서는이 구성 파일을 사용 하지 않으므로 생성 된 구성 파일의 설정을 클래스 라이브러리를 호출 하는 실행 파일에 대 한 *app.config* 파일에 추가 해야 합니다.

> [!NOTE]
> 대신, Visual Studio 대신 [ServiceModel Metadata 유틸리티 도구](#servicemodel-metadata-utility-tool) 를 사용 하 여 프록시 클래스와 구성 파일을 생성 합니다.

클라이언트 애플리케이션은 생성된 프록시 클래스를 사용하여 서비스와 통신합니다. 이 절차는 자습서에서 [설명 합니다. 클라이언트](how-to-use-a-wcf-client.md)를 사용 합니다.

이 자습서에서는 다음 작업을 수행하는 방법을 알아봅니다.
> [!div class="checklist"]
>
> - WCF 클라이언트용 콘솔 응용 프로그램 프로젝트를 만들고 구성 합니다.
> - WCF 서비스에 대 한 서비스 참조를 추가 하 여 프록시 클래스 및 구성 파일을 생성 합니다.

## <a name="create-a-windows-communication-foundation-client"></a>Windows Communication Foundation 클라이언트 만들기

1. Visual Studio에서 콘솔 응용 프로그램 프로젝트를 만듭니다. 

    1. **파일** 메뉴에서**프로젝트/솔루션** **열기** > 를 선택 하 고 이전에 만든 **get로 시작** 된 솔루션 (*gete r 시작 .sln*)로 이동 합니다. **열기**를 선택합니다.

    2. **보기** 메뉴에서 **솔루션 탐색기**를 선택 합니다.

    3. **솔루션 탐색기** 창에서 **get이상 시작** 된 솔루션 (최상위 노드)을 선택한 다음 바로 가기 메뉴에서**새 프로젝트** **추가** > 를 선택 합니다. 
    
    4. **새 프로젝트 추가** 창의 왼쪽에서  **C# 비주얼** 또는 **Visual Basic**아래에 있는 **Windows 바탕 화면** 범주를 선택 합니다. 

    5. **콘솔 앱 (.NET Framework)** 템플릿을 선택 하 고 **이름**에 *GettingStartedClient* 를 입력 합니다. **확인**을 선택합니다.

2. **GettingStartedClient** 프로젝트의 참조를 <xref:System.ServiceModel> 어셈블리에 추가 합니다. 

    1. **솔루션 탐색기** 창의 **GettingStartedClient** 프로젝트 아래에서 **참조** 폴더를 선택 하 고 바로 가기 메뉴에서 **참조 추가** 를 선택 합니다. 

    2. **참조 추가** 창의 창 왼쪽에 있는 **어셈블리** 에서 **프레임 워크**를 선택 합니다.
    
    3. **System.servicemodel**을 찾아 선택 하 고 **확인**을 선택 합니다. 

    4. **파일** > **모두 저장**을 선택 하 여 솔루션을 저장 합니다.

3. 계산기 서비스에 대 한 서비스 참조를 추가 합니다.

   1. **솔루션 탐색기** 창의 **GettingStartedClient** 프로젝트 아래에서 **참조** 폴더를 선택 하 고 바로 가기 메뉴에서 **서비스 참조 추가** 를 선택 합니다.

   2. **서비스 참조 추가** 창에서 **검색**을 선택 합니다.

      CalculatorService 서비스가 시작 되 고 Visual Studio가 **서비스** 상자에이를 표시 합니다.

   3. **CalculatorService** 를 선택 하 여 확장 하 고 서비스에서 구현 하는 서비스 계약을 표시 합니다. 기본 **네임 스페이스** 를 그대로 두고 **확인을**선택 합니다.

      **GettingStartedClient** 프로젝트의 **연결된 서비스** 폴더 아래에 새 항목이 추가 됩니다. 

### <a name="servicemodel-metadata-utility-tool"></a>ServiceModel Metadata 유틸리티 도구

다음 예제에서는 선택적으로 [ServiceModel Metadata 유틸리티 도구 (svcutil.exe)](servicemodel-metadata-utility-tool-svcutil-exe.md) 를 사용 하 여 프록시 클래스 파일을 생성 하는 방법을 보여 줍니다. 이 도구는 프록시 클래스 파일 및 *app.config* 파일을 생성 합니다. 다음 예에서는에서 C# 프록시를 생성 하 고 각각 Visual Basic 하는 방법을 보여 줍니다.

```shell
svcutil.exe /language:cs /out:generatedProxy.cs /config:app.config http://localhost:8000/GettingStarted/CalculatorService
```

```shell
svcutil.exe /language:vb /out:generatedProxy.vb /config:app.config http://localhost:8000/GettingStarted/CalculatorService
```

### <a name="client-configuration-file"></a>클라이언트 구성 파일

클라이언트를 만든 후 Visual Studio에서 **GettingStartedClient** 프로젝트에 app.config **구성 파일을 만듭니다 .이** 파일은 다음 예제와 유사 합니다.

```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <startup>
            <!-- specifies the version of WCF to use-->
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6.1" />
        </startup>
        <system.serviceModel>
            <bindings>
                <!-- Uses wsHttpBinding-->
                <wsHttpBinding>
                    <binding name="WSHttpBinding_ICalculator" />
                </wsHttpBinding>
            </bindings>
            <client>
                <!-- specifies the endpoint to use when calling the service -->
                <endpoint address="http://localhost:8000/GettingStarted/CalculatorService"
                    binding="wsHttpBinding" bindingConfiguration="WSHttpBinding_ICalculator"
                    contract="ServiceReference1.ICalculator" name="WSHttpBinding_ICalculator">
                    <identity>
                        <dns value="localhost" />
                    </identity>
                </endpoint>
            </client>
        </system.serviceModel>
    </configuration>
```

System.servicemodel > 섹션에서 끝점 > 요소를 확인 합니다 [ \<](../configure-apps/file-schema/wcf/endpoint-element.md) . [ \<](../configure-apps/file-schema/wcf/system-servicemodel.md) 끝점 요소는 **&lt;클라이언트에서 서비스에 액세스 하는 데 사용 하는 끝점을 다음과 같이 정의 합니다.&gt;**

- 주소: `http://localhost:8000/GettingStarted/CalculatorService`. 엔드포인트의 주소입니다.
- 서비스 계약: `ServiceReference1.ICalculator`. 서비스 계약은 WCF 클라이언트와 서비스 간의 통신을 처리 합니다. **서비스 참조 추가** 함수를 사용 하는 경우 Visual Studio에서이 계약을 생성 했습니다. 기본적으로 GettingStartedLib 프로젝트에 정의 된 계약의 복사본입니다. 
- 바인딩: <xref:System.ServiceModel.WSHttpBinding>. 바인딩은 HTTP를 전송, 상호 운용 가능한 보안 및 기타 구성 세부 사항으로 지정 합니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음 작업을 수행하는 방법을 알아보았습니다.
> [!div class="checklist"]
>
> - WCF 클라이언트용 콘솔 응용 프로그램 프로젝트를 만들고 구성 합니다.
> - WCF 서비스에 대 한 서비스 참조를 추가 하 여 클라이언트 응용 프로그램에 대 한 프록시 클래스 및 구성 파일을 생성 합니다.

다음 자습서로 이동 하 여 생성 된 클라이언트를 사용 하는 방법을 알아보세요.

> [!div class="nextstepaction"]
> [자습서: WCF 클라이언트 사용](how-to-use-a-wcf-client.md)
