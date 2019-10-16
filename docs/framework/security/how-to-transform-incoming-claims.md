---
title: '방법: 들어오는 클레임 변환'
ms.date: 03/30/2017
ms.assetid: 2831d514-d9d8-4200-9192-954bb6da1126
author: BrucePerlerMS
ms.openlocfilehash: ce99b97007bf7608856345d6da87cd9e422d2266
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70041473"
---
# <a name="how-to-transform-incoming-claims"></a>방법: 들어오는 클레임 변환

## <a name="applies-to"></a>적용 대상

- Microsoft® Windows® Identity Foundation(WIF)

- ASP.NET® Web Forms

## <a name="summary"></a>요약

이 방법은 간단한 클레임 인식 ASP.NET Web Forms 애플리케이션을 만들고 들어오는 클레임을 변환하기 위한 자세한 단계별 프로시저를 제공합니다. 또한, 애플리케이션이 실행될 때 변환된 클레임이 제공되는지 확인하기 위해 애플리케이션을 테스트하는 방법에 대한 지침을 제공합니다.

## <a name="contents"></a>목차

- 목표

- 개요

- 단계 요약

- 1단계 – 간단한 ASP.NET Web Forms 애플리케이션 만들기

- 2단계 – 사용자 지정 ClaimsAuthenticationManager를 사용하여 클레임 변환 구현

- 3단계 - 솔루션 테스트

## <a name="objectives"></a>목표

- 클레임 기반 인증에 대한 ASP.NET Web Forms 애플리케이션 구성

- 관리자 역할 클레임을 추가하여 들어오는 클레임 변환

- ASP.NET Web Forms 애플리케이션 테스트하여 제대로 작동하는지 확인

## <a name="overview"></a>개요

WIF는 RP(신뢰 당사자) 애플리케이션에 제공되기 전에 사용자가 클레임을 수정할 수 있는 <xref:System.Security.Claims.ClaimsAuthenticationManager>라는 클래스를 노출합니다. <xref:System.Security.Claims.ClaimsAuthenticationManager>는 인증 및 기본 응용 프로그램 코드 간에 문제를 분리하는 데 유용합니다. 아래 예제에서는 RP에 필요할 수 있는 들어오는 <xref:System.Security.Claims.ClaimsPrincipal>의 클레임에 역할을 추가하는 방법을 보여 줍니다.

## <a name="summary-of-steps"></a>단계 요약

- 1단계 – 간단한 ASP.NET Web Forms 애플리케이션 만들기

- 2단계 – 사용자 지정 ClaimsAuthenticationManager를 사용하여 클레임 변환 구현

- 3단계 - 솔루션 테스트

## <a name="step-1--create-a-simple-aspnet-web-forms-application"></a>1단계 – 간단한 ASP.NET Web Forms 애플리케이션 만들기

이 단계에서는 새로운 ASP.NET Web Forms 애플리케이션을 만듭니다.

#### <a name="to-create-a-simple-aspnet-application"></a>간단한 ASP.NET 애플리케이션을 만들려면

1. 관리자로 승격된 모드에서 Visual Studio를 시작합니다.

2. Visual Studio에서 **파일**, **새로 만들기**, **프로젝트**를 차례로 클릭합니다.

3. **새 프로젝트** 창에서 **ASP.NET Web Forms 응용 프로그램**을 클릭합니다.

4. **이름**에서 `TestApp`을 입력하고 **확인**을 누릅니다.

5. **솔루션 탐색기**에서 **TestApp** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **ID 및 액세스**를 선택합니다.

6. **ID 및 액세스** 창이 나타납니다. **공급자**에서 **로컬 개발 STS로 응용 프로그램 테스트**를 선택한 다음 **적용**을 클릭합니다.

7. *Default.aspx* 파일에서 기존 태그를 다음 태그로 바꾸고 파일을 저장합니다.

    ```aspx-csharp
    <%@ Page Title="Home Page" Language="C#" MasterPageFile="~/Site.Master" AutoEventWireup="true"
        CodeBehind="Default.aspx.cs" Inherits="TestApp._Default" %>

    <asp:Content runat="server" ID="BodyContent" ContentPlaceHolderID="MainContent">
          <h3>Your Claims</h3>
        <p>
            <asp:GridView ID="ClaimsGridView" runat="server" CellPadding="3">
                <AlternatingRowStyle BackColor="White" />
                <HeaderStyle BackColor="#7AC0DA" ForeColor="White" />
            </asp:GridView>
        </p>
    </asp:Content>
    ```

8. *Default.aspx.cs*라는 코드 숨김 파일을 엽니다. 기존 코드를 다음으로 바꾸고 파일을 저장합니다.

    ```csharp
    using System;
    using System.Web.UI;
    using System.Security.Claims;

    namespace TestApp
    {
        public partial class _Default : Page
        {
            protected void Page_Load(object sender, EventArgs e)
            {
                ClaimsPrincipal claimsPrincipal = Page.User as ClaimsPrincipal;
                this.ClaimsGridView.DataSource = claimsPrincipal.Claims;
                this.ClaimsGridView.DataBind();
            }
        }
    }
    ```

## <a name="step-2--implement-claims-transformation-using-a-custom-claimsauthenticationmanager"></a>2단계 – 사용자 지정 ClaimsAuthenticationManager를 사용하여 클레임 변환 구현

이 단계에서는 <xref:System.Security.Claims.ClaimsAuthenticationManager> 클래스에서 기본 기능을 재정의하여 들어오는 주체에 관리자 역할을 추가합니다.

#### <a name="to-implement-claims-transformation-using-a-custom-claimsauthenticationmanager"></a>사용자 지정 ClaimsAuthenticationManager를 사용하여 클레임 변환을 구현하려면

1. Visual Studio에서 솔루션을 마우스 오른쪽 단추로 클릭하고, **추가**를 클릭한 다음, **새 프로젝트**를 클릭합니다.

2. **새 프로젝트 추가** 창의 **Visual C#** 템플릿 목록에서 **클래스 라이브러리**를 선택하고, `ClaimsTransformation`을 입력한 다음, **확인**을 누릅니다. 새 프로젝트가 솔루션 폴더에 생성됩니다.

3. **ClaimsTransformation** 프로젝트에서 **참조**를 마우스 오른쪽 단추로 클릭한 다음 **참조 추가**를 클릭합니다.

4. **참조 관리자** 창에서 **System.IdentityModel**을 선택하고 **확인**을 클릭합니다.

5. **Class1.cs**를 열거나 이 파일이 없는 경우 **ClaimsTransformation**을 마우스 오른쪽 단추로 클릭하고 **추가**, **클래스…** 를 차례로 클릭합니다.

6. 지시문을 사용하여 다음을 코드 파일에 추가합니다.

    ```csharp
    using System.Security.Claims;
    using System.Security.Principal;
    ```

7. 다음 클래스 및 메서드를 코드 파일에 추가합니다.

    > [!WARNING]
    > 다음 코드는 데모용으로만 제공됩니다. 프로덕션 코드에서 필요한 권한이 있는지 확인해야 합니다.

    ```csharp
    public class ClaimsTransformationModule : ClaimsAuthenticationManager
    {
        public override ClaimsPrincipal Authenticate(string resourceName, ClaimsPrincipal incomingPrincipal)
        {
            if (incomingPrincipal != null && incomingPrincipal.Identity.IsAuthenticated == true)
            {
               ((ClaimsIdentity)incomingPrincipal.Identity).AddClaim(new Claim(ClaimTypes.Role, "Admin"));
            }

            return incomingPrincipal;
        }
    }
    ```

8. 파일을 저장하고 **ClaimsTransformation** 프로젝트를 빌드합니다.

9. **TestApp** ASP.NET 프로젝트에서 참조를 마우스 오른쪽 단추로 클릭하고 **참조 추가**를 클릭합니다.

10. **참조 관리자** 창의 왼쪽 메뉴에서 **솔루션**을 선택하고, 채워진 옵션에서 **ClaimsTransformation**을 선택하고 나서, **확인**을 클릭합니다.

11. 루트 **Web.config** 파일에서 **\<system.identityModel>** 항목으로 이동합니다. **\<identityConfiguration>** 요소 내에 다음 줄을 추가하고 파일을 저장합니다.

    ```xml
    <claimsAuthenticationManager type="ClaimsTransformation.ClaimsTransformationModule, ClaimsTransformation" />
    ```

## <a name="step-3--test-your-solution"></a>3단계 - 솔루션 테스트

이 단계에서는 ASP.NET Web Forms 애플리케이션을 테스트하고 사용자가 Forms 인증으로 로그인할 때 클레임이 제공되는지 확인합니다.

#### <a name="to-test-your-aspnet-web-forms-application-for-claims-using-forms-authentication"></a>Forms 인증을 사용하여 클레임에 대한 ASP.NET Web Forms 애플리케이션을 테스트하려면

1. **F5** 키를 눌러 응용 프로그램을 빌드하고 실행합니다. *Default.aspx*가 표시됩니다.

2. *Default.aspx* 페이지에서 계정에 대한 **Issuer**, **OriginalIssuer**, **Type**, **Value** 및 **ValueType** 클레임 정보를 포함하는 표가 **클레임** 제목 아래에 표시됩니다. 마지막 행은 다음 방식으로 제공됩니다.

    ||||||
    |-|-|-|-|-|
    |LOCAL AUTHORITY|LOCAL AUTHORITY|`http://schemas.microsoft.com/ws/2008/06/identity/claims/role`|관리|<https://www.w3.org/2001/XMLSchema#string>|
