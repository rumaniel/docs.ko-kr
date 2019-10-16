---
title: '방법: WCF 웹 서비스 애플리케이션에 WIF 사용'
ms.date: 03/30/2017
ms.assetid: bfc64b3d-64e9-4093-a6a4-72e933917af7
author: BrucePerlerMS
ms.openlocfilehash: 809009642caf743f4f067591adfa63ccb154a577
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70851538"
---
# <a name="how-to-enable-wif-for-a-wcf-web-service-application"></a>방법: WCF 웹 서비스 애플리케이션에 WIF 사용
## <a name="applies-to"></a>적용 대상

- Microsoft® Windows® Identity Foundation(WIF)

- Microsoft® Windows® Communication Foundation(WCF)

## <a name="summary"></a>요약

이 방법 설명에서는 WCF 웹 서비스에서 WIF를 사용하기 위한 자세한 단계별 절차를 소개합니다. 또한, 응용 프로그램이 실행될 때 웹 서비스가 클레임을 올바로 표시하는지 확인하기 위해 응용 프로그램을 테스트하는 방법에 대한 지침을 제공합니다. 이 방법 설명에 보안 토큰 서비스(STS)를 만들기 위한 자세한 지침은 없으며, 그 대신 ID 및 액세스 도구와 함께 제공되는 개발 STS를 사용합니다. 개발 STS가 실제 인증을 수행하는 것은 아니며, 테스트 목적으로만 사용됩니다. 이 방법을 완료하려면 ID 및 액세스 도구를 설치해야 합니다. 다음 위치에서 다운로드할 수 있습니다. [Id 및 액세스 도구](https://go.microsoft.com/fwlink/?LinkID=245849)

## <a name="contents"></a>목차

- 목표

- 개요

- 단계 요약

- 1단계 - 간단한 WCF 서비스 만들기

- 2단계 - WCF 서비스용 클라이언트 응용 프로그램 만들기

- 3단계 - 솔루션 테스트

## <a name="objectives"></a>목표

- 발행된 토큰을 요구하는 WCF 서비스 만들기

- STS로부터 토큰을 요청하고 WCF 서비스로 토큰을 전달하는 WCF 클라이언트 만들기

## <a name="overview"></a>개요

이 방법은 WCF 서비스를 개발할 때 개발자가 페더레이션 인증을 사용할 수 있는 방법을 보여주기 위한 것입니다. WCF 서비스에서 페더레이션을 사용할 때의 이점은 다음과 같습니다.

1. WCF 서비스 코드에서 인증 논리 제외

2. 기존 ID 관리 솔루션 재사용

3. 다른 ID 솔루션과의 상호 운용성

4. 미래 변화에 대한 유연성과 탄력성

WIF와 관련 ID 및 액세스 도구는 다음 단계에서 설명하는 바와 같이 페더레이션된 인증을 사용하여 WCF 서비스를 더욱 쉽게 개발하고 테스트할 수 있게 해줍니다.

## <a name="summary-of-steps"></a>단계 요약

- 1단계 - 간단한 WCF 서비스 만들기

- 2단계 - WCF 서비스용 클라이언트 응용 프로그램 만들기

- 3단계 - 솔루션 테스트

## <a name="step-1--create-a-simple-wcf-service"></a>1단계 - 간단한 WCF 서비스 만들기

이 단계에서는 ID 및 액세스 도구에 포함되어 있는 개발 STS를 사용하는 새 WCF 서비스를 만듭니다.

#### <a name="to-create-a-simple-wcf-service"></a>간단한 WCF 서비스를 만들려면

1. 관리자로 승격된 모드에서 Visual Studio를 시작합니다.

2. Visual Studio에서 **파일**, **새로 만들기**, **프로젝트**를 차례로 클릭합니다.

3. **새 프로젝트** 창에서 **WCF 서비스 응용 프로그램**을 클릭합니다.

4. **이름**에서 `TestService`를 입력하고 **확인**을 누릅니다.

5. **솔루션 탐색기**에서 **TestService** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **ID 및 액세스**를 선택합니다.

6. **ID 및 액세스** 창이 나타납니다. **공급자**에서 **로컬 개발 STS로 응용 프로그램 테스트**를 선택한 다음 **적용**을 클릭합니다. ID 및 액세스 도구는 *Web.config* 파일에 구성 요소를 추가하여 WIF를 사용하고 로컬 개발 STS(**LocalSTS**)로 인증을 아웃소싱하도록 서비스를 구성합니다.

7. *Service1.svc.cs* 파일에서 **System.Security.Claims** 네임스페이스에 대한 `using` 지시문을 추가하고 기존 코드를 다음으로 바꾼 다음 파일을 저장합니다.

    ```csharp
    public class Service1 : IService1
    {
        public string ComputeResponse(string input)
        {
            // Get the caller's identity from ClaimsPrincipal.Current
            ClaimsPrincipal claimsPrincipal = OperationContext.Current.ClaimsPrincipal;

            // Start generating the output
            StringBuilder builder = new StringBuilder();
            builder.AppendLine("Computed by ClaimsAwareWebService");
            builder.AppendLine("Input received from client:" + input);

            if (claimsPrincipal != null)
            {
                // Display the claims from the caller. Do not use this code in a production application.
                ClaimsIdentity identity = claimsPrincipal.Identity as ClaimsIdentity;
                builder.AppendLine("Client Name:" + identity.Name);
                builder.AppendLine("IsAuthenticated:" + identity.IsAuthenticated);
                builder.AppendLine("The service received the following issued claims of the client:");

                // Iterate over the caller’s claims and append to the output
                foreach (Claim claim in claimsPrincipal.Claims)
                {
                    builder.AppendLine("ClaimType :" + claim.Type + "   ClaimValue:" + claim.Value);
                }
            }

            return builder.ToString();
        }
    }
    ```

    `ComputeResponse` 메서드는 **LocalSTS**가 발행하는 다양한 클레임의 속성을 표시합니다.

8. *IService1.cs* 파일에서 기존 코드를 다음으로 바꾼 다음 파일을 저장합니다.

    ```csharp
    [ServiceContract]
    public interface IService1
    {
        [OperationContract]
        string ComputeResponse(string input);
    }
    ```

9. 프로젝트를 빌드합니다.

10. **Ctrl-F5** 키를 눌러 디버거를 시작하지 않고 서비스를 실행합니다. 서비스를 위한 웹 페이지가 열려야 하고 알림 영역(시스템 트레이)을 보고 **LocalSTS**가 실행 중인지 확인할 수 있습니다.

    > [!IMPORTANT]
    > 다음 단계에서 클라이언트 애플리케이션에 서비스 참조를 추가할 때 **TestService**와 **LocalSTS**가 모두 실행 중이어야 합니다.

## <a name="step-2--create-a-client-application-for-the-wcf-service"></a>2단계 - WCF 서비스용 클라이언트 응용 프로그램 만들기

이 단계에서는 개발 STS를 사용하여 이전 단계에서 만든 WCF 서비스로 인증하는 콘솔 응용 프로그램을 만듭니다.

#### <a name="to-create-a-client-application"></a>클라이언트 응용 프로그램을 만들려면

1. Visual Studio에서 솔루션을 마우스 오른쪽 단추로 클릭하고, **추가**, **새 프로젝트**를 차례로 클릭합니다.

2. **새 프로젝트 추가** 창의 **Visual C#** 템플릿 목록에서 **콘솔 응용 프로그램**을 선택하고, `Client`를 입력한 다음, **확인**을 누릅니다. 새 프로젝트가 솔루션 폴더에 생성됩니다.

3. **클라이언트** 프로젝트에서 **참조**를 마우스 오른쪽 단추로 클릭한 다음 **서비스 참조 추가**를 클릭합니다.

4. **서비스 참조 추가** 창에서 **검색** 단추의 드롭다운 화살표를 클릭하고 **솔루션의 서비스**를 클릭합니다. **주소**에는 앞서 만든 WCF 서비스가 자동으로 채워지고 **네임스페이스**는 **ServiceReference1**로 설정됩니다. **확인**을 클릭합니다.

    > [!IMPORTANT]
    > 클라이언트에 서비스 참조를 추가할 때 **TestService**와 **LocalSTS**가 모두 실행 중이어야 합니다.

5. Visual Studio는 WCF 서비스를 위한 프록시 클래스를 생성하고 필요한 참조 정보를 모두 추가합니다. 또한, *App.config* 파일에 요소를 추가하여 클라이언트가 STS에서 토큰을 받아 서비스에 인증하도록 구성합니다. 이 프로세스가 완료되면 **Program.cs** 파일이 열립니다. **System.ServiceModel**에 대한 `using` 지시문과 **Client.ServiceReference1**에 대한 다른 지시문을 추가하고, **Main** 메서드를 다음 코드로 바꾼 다음, 파일을 저장합니다.

    ```csharp
    static void Main(string[] args)
    {
        // Create the client for the service
        Service1Client client = new Service1Client();
        Console.WriteLine("-------------WCF Client Application--------------\n");

        while (!ShouldQuitApplication())
        {
            try
            {
                Console.WriteLine(client.ComputeResponse("Hello World"));
            }
            catch (CommunicationException e)
            {
                Console.WriteLine(e.Message);
                Console.WriteLine(e.StackTrace);
                Exception ex = e.InnerException;
                while (ex != null)
                {
                    Console.WriteLine("===========================");
                    Console.WriteLine(ex.Message);
                    Console.WriteLine(ex.StackTrace);
                    ex = ex.InnerException;
                }
            }
            catch (TimeoutException)
            {
                Console.WriteLine("Timed out...");
            }
            catch (Exception e)
            {
                Console.WriteLine("An unexpected exception occurred.");
                Console.WriteLine(e.StackTrace);
            }
        }

        client.Close();

        if (client != null)
        {
            client.Abort();
        }
    }

    static bool ShouldQuitApplication()
    {
        Console.WriteLine("---------------------------------------------------------------------");
        Console.WriteLine("Press Enter key to invoke service, any other key to quit application:");
        Console.WriteLine("----------------------------------------------------------------------");

        ConsoleKeyInfo keyInfo = Console.ReadKey();
        if (keyInfo.Key == ConsoleKey.Enter)
            return false;
        return true;
    }
    ```

6. *App.config* 파일을 열고, 다음 XML을 `<system.serviceModel>` 요소 아래의 첫 번째 자식 요소로 추가한 다음, 파일을 저장합니다.

    ```xml
    <behaviors>
       <endpointBehaviors>
         <behavior>
           <clientCredentials>
             <serviceCertificate>
               <authentication certificateValidationMode="None"/>
             </serviceCertificate>
           </clientCredentials>
         </behavior>
       </endpointBehaviors>
     </behaviors>
    ```

    이렇게 하면 인증서 유효성 검사를 사용하지 않습니다.

7. **TestService** 솔루션을 마우스 오른쪽 단추로 클릭하고 **시작 프로젝트 설정**을 클릭합니다. **시작 프로젝트** 속성 페이지가 열립니다. **시작 프로젝트** 속성 페이지에서 **여러 개의 시작 프로젝트**를 선택한 다음, 각 프로젝트에 대한 **작업** 필드를 클릭하고, 드롭다운 메뉴에서 **시작**을 선택합니다. **확인**을 클릭하여 설정을 저장합니다.

8. 솔루션을 빌드합니다.

## <a name="step-3--test-your-solution"></a>3단계 - 솔루션 테스트

이 단계에서 WIF를 사용하는 WCF 응용 프로그램을 테스트하고 클레임이 표시되는지 확인합니다.

#### <a name="to-test-your-wif-enabled-wcf-application-for-claims"></a>클레임에 대해 WIF를 사용하는 WCF 응용 프로그램을 테스트하려면

1. **F5** 키를 눌러 응용 프로그램을 빌드하고 실행합니다. 콘솔 창과 다음 텍스트가 표시 됩니다. **Enter 키를 눌러 서비스를 호출 하 고 다른 모든 키를 눌러 응용 프로그램을 종료 합니다.**

2. **Enter** 키를 누르면 콘솔에 다음 클레임 정보가 나타납니다.

    ```output
    Computed by Service1
    Input received from client: Hello World
    Client Name: Terry
    IsAuthenticated: True
    The service received the following issued claims of the client:
    ClaimType :http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name    ClaimValue:Terry
    ClaimType :http://schema.xmlsoap.org/ws/2005/05/identity/claims/surname    ClaimValue:Adams
    ClaimType :http://schemas.microsoft.com/ws/2008/06/identity/claims/role    ClaimValue:developer
    ClaimType :http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress    ClaimValue:terry@contoso.com
    ```

    > [!IMPORTANT]
    > **Enter** 키를 누르기 전에 **TestService**와 **LocalSTS**가 모두 실행 중이어야 합니다. 서비스를 위한 웹 페이지가 열려야 하고 알림 영역(시스템 트레이)을 보고 **LocalSTS**가 실행 중인지 확인할 수 있습니다.

3. 이러한 클레임이 콘솔에 나타나는 경우, WCF 서비스에서 클레임을 표시하도록 STS 인증에 성공한 것입니다.
