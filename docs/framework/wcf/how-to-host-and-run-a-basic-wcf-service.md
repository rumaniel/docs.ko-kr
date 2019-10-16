---
title: '자습서: 기본 Windows Communication Foundation 서비스 호스팅 및 실행'
ms.date: 03/19/2019
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF services [WCF]
- WCF services [WCF], running
ms.assetid: 31774d36-923b-4e2d-812e-aa190127266f
ms.openlocfilehash: 984c5e73a8efc4e9c2d487485267868ffa2f60f3
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70928721"
---
# <a name="tutorial-host-and-run-a-basic-windows-communication-foundation-service"></a>자습서: 기본 Windows Communication Foundation 서비스 호스팅 및 실행

이 자습서에서는 WCF (기본 Windows Communication Foundation) 응용 프로그램을 만드는 데 필요한 5 가지 작업 중 세 번째 작업에 대해 설명 합니다. 자습서에 대 한 개요를 보려면 [자습서: Windows Communication Foundation 응용 프로그램](getting-started-tutorial.md)을 시작 하세요.

WCF 응용 프로그램을 만들기 위한 다음 작업은 콘솔 응용 프로그램에서 WCF 서비스를 호스트 하는 것입니다. WCF 서비스는 하나 이상의 끝점을 노출 하 고, 각 *끝점*은 하나 이상의 서비스 작업을 노출 합니다. 서비스 끝점은 다음 정보를 지정 합니다.

- 서비스를 찾을 수 있는 주소입니다.
- 클라이언트가 서비스와 통신 해야 하는 방법을 설명 하는 정보를 포함 하는 바인딩입니다. 
- 서비스에서 클라이언트에 제공 하는 기능을 정의 하는 계약입니다.

이 자습서에서는 다음 작업을 수행하는 방법을 알아봅니다.
> [!div class="checklist"]
>
> - WCF 서비스를 호스팅하기 위한 콘솔 응용 프로그램 프로젝트를 만들고 구성 합니다.
> - WCF 서비스를 호스트 하는 코드를 추가 합니다.
> - 구성 파일을 업데이트 합니다.
> - WCF 서비스를 시작 하 고 실행 중인지 확인 합니다.

## <a name="create-and-configure-a-console-app-project-for-hosting-the-service"></a>서비스를 호스팅하기 위한 콘솔 앱 프로젝트 만들기 및 구성

1. Visual Studio에서 콘솔 응용 프로그램 프로젝트를 만듭니다. 
 
    1. **파일** 메뉴에서**프로젝트/솔루션** **열기** > 를 선택 하 고 이전에 만든 **get로 시작** 된 솔루션 (*gete r 시작 .sln*)로 이동 합니다. **열기**를 선택합니다.

    2. **보기** 메뉴에서 **솔루션 탐색기**를 선택 합니다.
    
    3. **솔루션 탐색기** 창에서 **get이상 시작** 된 솔루션 (최상위 노드)을 선택한 다음 바로 가기 메뉴에서**새 프로젝트** **추가** > 를 선택 합니다. 

    4. **새 프로젝트 추가** 창의 왼쪽에서  **C# 비주얼** 또는 **Visual Basic**아래에 있는 **Windows 바탕 화면** 범주를 선택 합니다. 

    5. **콘솔 앱 (.NET Framework)** 템플릿을 선택 하 고 **이름**에 *GettingStartedHost* 를 입력 합니다. **확인**을 선택합니다.

2. **GettingStartedLib** 프로젝트에 **GettingStartedHost** 프로젝트에 대 한 참조를 추가 합니다. 

    1. **솔루션 탐색기** 창의 **GettingStartedHost** 프로젝트 아래에서 **참조** 폴더를 선택 하 고 바로 가기 메뉴에서 **참조 추가** 를 선택 합니다. 

    2. **참조 추가** 대화 상자의 창 왼쪽에 있는 **프로젝트** 에서 **솔루션**을 선택 합니다. 
 
    3. 창의 가운데 섹션에서 **GettingStartedLib** 를 선택 하 고 **확인**을 선택 합니다. 

       이 작업을 수행 하면 **GettingStartedLib** 프로젝트에 정의 된 형식을 **GettingStartedHost** 프로젝트에서 사용할 수 있습니다.

3. **GettingStartedHost** 프로젝트의 참조를 <xref:System.ServiceModel> 어셈블리에 추가 합니다. 

    1. **솔루션 탐색기** 창의 **GettingStartedHost** 프로젝트 아래에서 **참조** 폴더를 선택 하 고 바로 가기 메뉴에서 **참조 추가** 를 선택 합니다.
    
    2. **참조 추가** 창의 창 왼쪽에 있는 **어셈블리** 에서 **프레임 워크**를 선택 합니다. 

    3. **System.servicemodel**을 선택 하 고 **확인**을 선택 합니다. 
    
    4. **파일** > **모두 저장**을 선택 하 여 솔루션을 저장 합니다.

## <a name="add-code-to-host-the-service"></a>서비스를 호스트 하는 코드 추가

서비스를 호스팅하려면 다음 단계를 수행 하는 코드를 추가 합니다. 

1. 기본 주소에 대 한 URI를 만듭니다.
2. 서비스를 호스팅하기 위한 클래스 인스턴스를 만듭니다.
3. 서비스 끝점을 만듭니다.
4. 메타데이터 교환을 사용하도록 설정합니다.
5. 들어오는 메시지를 수신 대기 하는 서비스 호스트를 엽니다.
  
코드를 다음과 같이 변경 합니다.

1. **GettingStartedHost** 프로젝트에서 **Program.cs** 또는 module1.vb 파일을 열고 해당 코드를 다음 코드로 **바꿉니다.**

    ```csharp
    using System;
    using System.ServiceModel;
    using System.ServiceModel.Description;
    using GettingStartedLib;

    namespace GettingStartedHost
    {
        class Program
        {
            static void Main(string[] args)
            {
                // Step 1: Create a URI to serve as the base address.
                Uri baseAddress = new Uri("http://localhost:8000/GettingStarted/");

                // Step 2: Create a ServiceHost instance.
                ServiceHost selfHost = new ServiceHost(typeof(CalculatorService), baseAddress);

                try
                {
                    // Step 3: Add a service endpoint.
                    selfHost.AddServiceEndpoint(typeof(ICalculator), new WSHttpBinding(), "CalculatorService");

                    // Step 4: Enable metadata exchange.
                    ServiceMetadataBehavior smb = new ServiceMetadataBehavior();
                    smb.HttpGetEnabled = true;
                    selfHost.Description.Behaviors.Add(smb)    ;

                    // Step 5: Start the service.
                    selfHost.Open();
                    Console.WriteLine("The service is ready.");

                    // Close the ServiceHost to stop the service.
                    Console.WriteLine("Press <Enter> to terminate the service.");
                    Console.WriteLine();
                    Console.ReadLine();
                    selfHost.Close();
                }
                catch (CommunicationException ce)
                {
                    Console.WriteLine("An exception occurred: {0}", ce.Message);
                    selfHost.Abort();
                }
            }
        }
    }
    ```

    ```vb
    Imports System.ServiceModel
    Imports System.ServiceModel.Description
    Imports GettingStartedLib.GettingStartedLib

    Module Service

        Class Program
            Shared Sub Main()
                ' Step 1: Create a URI to serve as the base address.
                Dim baseAddress As New Uri("http://localhost:8000/GettingStarted/")

                ' Step 2: Create a ServiceHost instance.
                Dim selfHost As New ServiceHost(GetType(CalculatorService), baseAddress)
               Try

                    ' Step 3: Add a service endpoint.
                    selfHost.AddServiceEndpoint( _
                        GetType(ICalculator), _
                        New WSHttpBinding(), _
                        "CalculatorService")

                    ' Step 4: Enable metadata exchange.
                    Dim smb As New ServiceMetadataBehavior()
                    smb.HttpGetEnabled = True
                    selfHost.Description.Behaviors.Add(smb)

                    ' Step 5: Start the service.
                    selfHost.Open()
                    Console.WriteLine("The service is ready.")

                    ' Close the ServiceHost to stop the service.
                    Console.WriteLine("Press <Enter> to terminate the service.")
                    Console.WriteLine()
                    Console.ReadLine()
                    selfHost.Close()

                Catch ce As CommunicationException
                    Console.WriteLine("An exception occurred: {0}", ce.Message)
                    selfHost.Abort()
                End Try
            End Sub
        End Class

    End Module
    ```
    
    이 코드가 작동 하는 방식에 대 한 자세한 내용은 [서비스 호스팅 프로그램 단계](#service-hosting-program-steps)를 참조 하세요.

2. 프로젝트 속성을 업데이트 합니다.

   1. **솔루션 탐색기** 창에서 **GettingStartedHost** 폴더를 선택 하 고 바로 가기 메뉴에서 **속성** 을 선택 합니다.

   2. **GettingStartedHost** 속성 페이지에서 **응용 프로그램** 탭을 선택 합니다.

      - 프로젝트 C# 의 경우 **시작 개체** 목록에서 **GettingStartedHost** 를 선택 합니다.

      - Visual Basic 프로젝트의 경우 **시작 개체** 목록에서 **서비스 프로그램** 을 선택 합니다.

   3. **파일** 메뉴에서 **모두 저장**을 선택 합니다.

## <a name="verify-the-service-is-working"></a>서비스가 작동 하는지 확인

1. 솔루션을 빌드한 다음, Visual Studio 내에서 **GettingStartedHost** 콘솔 응용 프로그램을 실행 합니다. 

    관리자 권한으로 서비스를 실행 해야 합니다. 관리자 권한으로 Visual Studio를 열었지만 Visual Studio에서 **GettingStartedHost** 를 실행 하면 응용 프로그램도 관리자 권한으로 실행 됩니다. 또는 관리자 권한으로 새 명령 프롬프트를 열고 (바로 가기 메뉴에서**관리자 권한으로 실행** **을 선택** > 하는 경우), 그 안에서 **GettingStartedHost** 을 실행할 수 있습니다.

2. 웹 브라우저를 열고에서 `http://localhost:8000/GettingStarted/CalculatorService`서비스 페이지로 이동 합니다.
   
   > [!NOTE]
   > 이러한 서비스에는 수신 대기를 위해 컴퓨터에서 HTTP 주소를 등록할 수 있는 적절 한 권한이 필요 합니다. 관리자 계정에는 이 권한이 있지만, 관리자 이외의 계정에는 HTTP 네임스페이스에 대한 권한을 부여해야 합니다. 네임스페이스 예약을 구성하는 방법에 대한 자세한 내용은 [HTTP 및 HTTPS 구성](feature-details/configuring-http-and-https.md)을 참조하세요. 

## <a name="service-hosting-program-steps"></a>서비스 호스팅 프로그램 단계

서비스를 호스트 하기 위해 추가한 코드의 단계는 다음과 같이 설명 됩니다.

- **1 단계**: 서비스의 기본 주소를 `Uri` 보유할 클래스의 인스턴스를 만듭니다. 기본 주소를 포함 하는 URL에는 서비스를 식별 하는 선택적 URI가 있습니다. 기본 주소는 다음과 `<transport>://<machine-name or domain><:optional port #>/<optional URI segment>`같이 형식이 지정 됩니다. 계산기 서비스에 대 한 기본 주소는 HTTP 전송, localhost, 포트 8000 및 URI 세그먼트 Get% 시작을 사용 합니다.

- **2단계**: 서비스를 호스트 하는 <xref:System.ServiceModel.ServiceHost> 데 사용 하는 클래스의 인스턴스를 만듭니다. 생성자는 서비스 계약을 구현 하는 클래스의 형식 및 서비스의 기본 주소 라는 두 개의 매개 변수를 사용 합니다.

- **3단계**: <xref:System.ServiceModel.Description.ServiceEndpoint> 인스턴스를 만듭니다. 서비스 엔드포인트는 주소, 바인딩 및 서비스 계약으로 구성되어 있습니다. 생성자 <xref:System.ServiceModel.Description.ServiceEndpoint> 는 서비스 계약 인터페이스 형식, 바인딩 및 주소로 구성 됩니다. 서비스 계약은 사용자가 정의한 `ICalculator`이며 서비스 형식에 구현합니다. 이 샘플에 대 한 바인딩은 <xref:System.ServiceModel.WSHttpBinding>기본 제공 바인딩으로, WS-* 사양을 준수 하는 끝점에 연결 하는입니다. WCF 바인딩에 대 한 자세한 내용은 [wcf 바인딩 개요](bindings-overview.md)를 참조 하세요. 주소를 기본 주소에 추가 하 여 끝점을 식별 합니다. 이 코드는 CalculatorService로 주소를 지정 하 고 끝점의 정규화 된 주소를 `http://localhost:8000/GettingStarted/CalculatorService`로 지정 합니다.

    > [!IMPORTANT]
    > .NET Framework 버전 4 이상에서는 서비스 끝점을 추가 하는 것이 선택 사항입니다. 이러한 버전의 경우, 코드 또는 구성을 추가 하지 않으면 WCF는 서비스에 의해 구현 된 기본 주소 및 계약의 각 조합에 대해 기본 끝점을 하나씩 추가 합니다. 기본 끝점에 대 한 자세한 내용은 [끝점 주소 지정](specifying-an-endpoint-address.md)을 참조 하세요. 기본 끝점, 바인딩 및 동작에 대 한 자세한 내용은 [WCF 서비스에 대 한](samples/simplified-configuration-for-wcf-services.md) [간소화 된 구성](simplified-configuration.md) 및 단순화 된 구성을 참조 하세요.

- **4단계**: 메타데이터 교환을 사용하도록 설정합니다. 클라이언트는 메타 데이터 교환을 사용 하 여 서비스 작업을 호출 하는 프록시를 생성 합니다. 메타 데이터 교환을 사용 하도록 설정 하려면 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 인스턴스를 만들고 해당 <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpGetEnabled> 속성을 `true`로 설정 하 고 `ServiceMetadataBehavior` 개체를 <xref:System.ServiceModel.ServiceHost> 인스턴스의 <xref:System.ServiceModel.Description.ServiceDescription.Behaviors%2A> 컬렉션에 추가 합니다.

- **5 단계**: 를 <xref:System.ServiceModel.ServiceHost> 열어 들어오는 메시지를 수신 합니다. 응용 프로그램에서 **enter**키를 누를 때까지 기다립니다. 응용 프로그램을 인스턴스화한 <xref:System.ServiceModel.ServiceHost>후에는 try/catch 블록을 실행 합니다. 에서 throw 되는 <xref:System.ServiceModel.ServiceHost>예외를 안전 하 게 catch 하는 방법에 대 한 자세한 내용은 [Close 및 Abort를 사용 하 여 WCF 클라이언트 리소스 해제](samples/use-close-abort-release-wcf-client-resources.md)

> [!IMPORTANT]
> WCF 서비스 라이브러리를 추가 하는 경우 서비스 호스트를 시작 하 여 디버깅 하는 경우 Visual Studio에서 해당 라이브러리를 호스팅합니다. 충돌을 방지 하기 위해 Visual Studio에서 WCF 서비스 라이브러리를 호스팅하지 못하도록 방지할 수 있습니다. 
>
> 1. **솔루션 탐색기** 에서 **GettingStartedLib** 프로젝트를 선택 하 고 바로 가기 메뉴에서 **속성** 을 선택 합니다.
> 2. **동일한 솔루션에서 다른 프로젝트를 디버깅할 때** **wcf 옵션** 을 선택 하 고 wcf 서비스 호스트 시작을 선택 취소 합니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음 작업을 수행하는 방법을 알아보았습니다.
> [!div class="checklist"]
>
> - WCF 서비스를 호스팅하기 위한 콘솔 응용 프로그램 프로젝트를 만들고 구성 합니다.
> - WCF 서비스를 호스트 하는 코드를 추가 합니다.
> - 구성 파일을 업데이트 합니다.
> - WCF 서비스를 시작 하 고 실행 중인지 확인 합니다.

WCF 클라이언트를 만드는 방법에 대해 알아보려면 다음 자습서로 이동 합니다.

> [!div class="nextstepaction"]
> [자습서: WCF 클라이언트 만들기](how-to-create-a-wcf-client.md)
