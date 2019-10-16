---
title: '방법: WIF를 사용하여 클레임 인식 ASP.NET Web Forms 애플리케이션 빌드'
ms.date: 03/30/2017
ms.assetid: efb264dd-f47b-49a9-85ee-9f45d4425765
author: BrucePerlerMS
ms.openlocfilehash: 45ad084013cbcafdf0d7c4ac3e0fd952305232c4
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70851553"
---
# <a name="how-to-build-claims-aware-aspnet-web-forms-application-using-wif"></a>방법: WIF를 사용하여 클레임 인식 ASP.NET Web Forms 애플리케이션 빌드
## <a name="applies-to"></a>적용 대상  
  
- Microsoft® Windows® Identity Foundation(WIF)  
  
- ASP.NET® Web Forms  
  
## <a name="summary"></a>요약  
 이 방법은 간단한 클레임 인식 ASP.NET Web Forms 애플리케이션을 만들기 위한 자세한 단계별 프로시저를 제공합니다. 또한 페더레이션 인증을 성공적으로 구현하기 위해 간단한 클레임 인식 ASP.NET Web Forms 애플리케이션을 테스트하는 방법에 대한 지침을 제공합니다. 이 방법에 STS(보안 토큰 서비스)를 만들기 위한 자세한 지침은 없으며, STS를 이미 구성했다고 가정합니다.  
  
## <a name="contents"></a>목차  
  
- 목표  
  
- 단계 요약  
  
- 1단계 – 간단한 ASP.NET Web Forms 애플리케이션 만들기  
  
- 2단계 – 클레임 기반 인증에 대한 ASP.NET Web Forms 애플리케이션 구성  
  
- 3단계 - 솔루션 테스트  
  
## <a name="objectives"></a>목표  
  
- 클레임 기반 인증에 대한 ASP.NET Web Forms 애플리케이션 구성  
  
- 성공적인 클레임 인식 ASP.NET Web Forms 애플리케이션 테스트  
  
## <a name="summary-of-steps"></a>단계 요약  
  
- 1단계 – 간단한 ASP.NET Web Forms 애플리케이션 만들기  
  
- 2단계 - 페더레이션 인증에 대한 ASP.NET Web Forms 애플리케이션 구성  
  
- 3단계 - 솔루션 테스트  
  
## <a name="step-1--create-a-simple-aspnet-web-forms-application"></a>1단계 – 간단한 ASP.NET Web Forms 애플리케이션 만들기  
 이 단계에서는 새로운 ASP.NET Web Forms 애플리케이션을 만듭니다.  
  
#### <a name="to-create-a-simple-aspnet-application"></a>간단한 ASP.NET 애플리케이션을 만들려면  
  
1. Visual Studio를 시작하고 **파일**, **새로 만들기**, **프로젝트**를 차례로 클릭합니다.  
  
2. **새 프로젝트** 창에서 **ASP.NET Web Forms 응용 프로그램**을 클릭합니다.  
  
3. **이름**에서 `TestApp`을 입력하고 **확인**을 누릅니다.  
  
## <a name="step-2--configure-aspnet-web-forms-application-for-claims-based-authentication"></a>2단계 – 클레임 기반 인증에 대한 ASP.NET Web Forms 애플리케이션 구성  
 이 단계에서는 ASP.NET Web Forms 애플리케이션의 *Web.config* 구성 파일에 구성 항목을 추가하여 클레임을 인식하도록 설정합니다.  
  
#### <a name="to-configure-aspnet-application-for-claims-based-authentication"></a>클레임 기반 인증에 대한 ASP.NET 애플리케이션을 구성하려면  
  
1. *Web.config* 구성 파일의 **\<configuration>** 여는 요소 바로 뒤에 다음 구성 섹션 항목을 추가합니다.  
  
    ```xml  
    <configSections>  
      <section name="system.identityModel" type="System.IdentityModel.Configuration.SystemIdentityModelSection, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089" />  
      <section name="system.identityModel.services" type="System.IdentityModel.Services.Configuration.SystemIdentityModelServicesSection, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089" />  
    </configSections>  
    ```  
  
2. 응용 프로그램의 페더레이션 메타데이터에 액세스할 수 있는 **\<location>** 요소를 추가합니다.  
  
    ```xml  
    <location path="FederationMetadata">  
      <system.web>  
        <authorization>  
          <allow users="*" />  
        </authorization>  
      </system.web>  
    </location>  
    ```  
  
3. **\<system.web>** 요소 내에 다음 구성 항목을 추가하여 사용자를 거부하고, 기본 인증을 사용하지 않도록 설정하고, WIF로 인증을 관리합니다.  
  
    ```xml  
    <authorization>  
      <deny users="?" />  
    </authorization>  
    <authentication mode="None" />  
    ```  
  
4. 페더레이션 인증에 대한 모듈을 정의하는 **\<system.webServer>** 요소를 추가합니다. *PublicKeyToken* 특성은 이전에 추가된 **\<configSections>** 항목에 대한 *PublicKeyToken* 특성과 동일해야 합니다.  
  
    ```xml  
    <system.webServer>  
      <modules>  
        <add name="WSFederationAuthenticationModule" type="System.IdentityModel.Services.WSFederationAuthenticationModule, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" preCondition="managedHandler" />  
        <add name="SessionAuthenticationModule" type="System.IdentityModel.Services.SessionAuthenticationModule, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" preCondition="managedHandler" />  
      </modules>  
    </system.webServer>  
    ```  
  
5. 다음 Windows Identity Foundation 관련 구성 항목을 추가하고 ASP.NET 응용 프로그램의 URL 및 포트 번호가 **\<audienceUris>** 항목, **\<wsFederation>** 요소의 **realm** 특성 및 **\<wsFederation>** 요소의 **reply** 특성 값과 일치하는지 확인합니다. 또한 **issuer** 값이 STS(보안 토큰 서비스) URL과 일치하는지 확인합니다.  
  
    ```xml  
    <system.identityModel>  
        <identityConfiguration>  
            <audienceUris>  
                <add value="http://localhost:28503/" />  
            </audienceUris>  
            <issuerNameRegistry type="System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">  
                <trustedIssuers>  
                    <add thumbprint="1234567890ABCDEFGHIJKLMNOPQRSTUVWXYZ1234" name="YourSTSName" />  
                </trustedIssuers>   
            </issuerNameRegistry>  
            <certificateValidation certificateValidationMode="None" />  
        </identityConfiguration>  
    </system.identityModel>  
    <system.identityModel.services>  
        <federationConfiguration>  
            <cookieHandler requireSsl="true" />  
            <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:13922/wsFederationSTS/Issue" realm="http://localhost:28503/" reply="http://localhost:28503/" requireHttps="true" />  
        </federationConfiguration>  
    </system.identityModel.services>  
    ```  
  
6. <xref:System.IdentityModel> 어셈블리에 대한 참조를 추가합니다.  
  
7. 솔루션을 컴파일하여 오류가 없는지 확인합니다.  
  
## <a name="step-3--test-your-solution"></a>3단계 - 솔루션 테스트  
 이 단계에서는 클레임 기반 인증에 대해 구성된 ASP.NET Web Forms 애플리케이션을 테스트합니다. 기본 테스트를 수행하려면 STS(보안 토큰 서비스)에서 발급된 토큰에 클레임을 표시하는 코드를 추가합니다.  
  
#### <a name="to-test-your-aspnet-web-form-application-for-claims-based-authentication"></a>클레임 기반 인증에 대한 ASP.NET Web Forms 애플리케이션을 테스트하려면  
  
1. **TestApp** 프로젝트 아래에서 **Default.aspx** 파일을 열고 기존 태그를 다음 태그로 바꿉니다.  
  
    ```aspx-csharp
    <%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>  
  
    <!DOCTYPE html>  
  
    <html>  
    <head id="Head1" runat="server">  
        <title></title>  
    </head>  
    <body>  
        <h1><asp:label ID="signedIn" runat="server" /></h1>  
        <asp:label ID="claimType" runat="server" />  
        <asp:label ID="claimValue" runat="server" />  
        <asp:label ID="claimValueType" runat="server" />  
        <asp:label ID="claimSubjectName" runat="server" />  
        <asp:label ID="claimIssuer" runat="server" />  
    </body>  
    </html>  
    ```  
  
2. **Default.aspx**를 저장하고 나서 **Default.aspx.cs**라는 코드 숨김 파일을 엽니다.  
  
    > [!NOTE]
    > **Default.aspx.cs**는 솔루션 탐색기에서 **Default.aspx** 아래에 숨겨질 수 있습니다. **Default.aspx.cs**가 표시되지 않으면 옆에 있는 삼각형을 클릭하여 **Default.aspx**를 확장합니다.  
  
3. **Default.aspx.cs**의 **Page_Load** 메서드에 있는 기존 코드를 다음 코드로 바꿉니다.  
  
    ```csharp  
    using System;  
    using System.IdentityModel;  
    using System.Security.Claims;  
    using System.Threading;  
    using System.Web.UI;  
  
    namespace TestApp  
    {  
        public partial class _Default : System.Web.UI.Page  
        {  
            protected void Page_Load(object sender, EventArgs e)  
            {  
                ClaimsPrincipal claimsPrincipal = Thread.CurrentPrincipal as ClaimsPrincipal;  
  
                if (claimsPrincipal != null)  
                {  
                    signedIn.Text = "You are signed in.";  
  
                    foreach (Claim claim in claimsPrincipal.Claims)  
                    {  
                        claimType.Text = claim.Type;  
                        claimValue.Text = claim.Value;  
                        claimValueType.Text = claim.ValueType;  
                        claimSubjectName.Text = claim.Subject.Name;  
                        claimIssuer.Text = claim.Issuer;  
                    }  
                }  
                else  
                {  
                    signedIn.Text = "You are not signed in.";  
                }  
            }  
        }  
    }  
    ```  
  
4. **Default.aspx.cs**를 저장하고 솔루션을 빌드합니다.  
  
5. **F5** 키를 눌러 솔루션을 실행합니다.  
  
6. STS(보안 토큰 서비스)에서 발급된 토큰에 클레임을 표시하는 페이지가 표시되어야 합니다.
