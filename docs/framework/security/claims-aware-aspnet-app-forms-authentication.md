---
title: '방법: 양식 기반 인증을 사용하여 클레임 인식 ASP.NET 애플리케이션 빌드'
ms.date: 03/30/2017
ms.assetid: 98a3e029-1a9b-4e0c-b5d0-29d3f23f5b15
author: BrucePerlerMS
ms.openlocfilehash: 75db96a621d7863ef445efb24814111b34da6960
ms.sourcegitcommit: a97ecb94437362b21fffc5eb3c38b6c0b4368999
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2019
ms.locfileid: "68971844"
---
# <a name="how-to-build-claims-aware-aspnet-application-using-forms-based-authentication"></a>방법: 양식 기반 인증을 사용하여 클레임 인식 ASP.NET 애플리케이션 빌드

## <a name="applies-to"></a>적용 대상

- Microsoft® Windows® Identity Foundation(WIF)

- ASP.NET® Web Forms

## <a name="summary"></a>요약

이 방법은 Forms 인증을 사용하는 간단한 클레임 인식 ASP.NET Web Forms 애플리케이션을 만들기 위한 자세한 단계별 절차를 제공합니다. 또한 애플리케이션을 테스트하여 사용자가 Forms 인증으로 로그인할 때 클레임이 제공되는지 확인하는 방법에 대한 지침을 제공합니다.

## <a name="contents"></a>목차

- 목표

- 개요

- 단계 요약

- 1단계 – 간단한 ASP.NET Web Forms 애플리케이션 만들기

- 2단계 – Forms 인증을 사용하여 클레임에 대한 ASP.NET Web Forms 애플리케이션 구성

- 3단계 - 솔루션 테스트

## <a name="objectives"></a>목표

- Forms 인증을 사용하여 클레임에 대한 ASP.NET Web Forms 애플리케이션 구성

- ASP.NET Web Forms 애플리케이션 테스트하여 제대로 작동하는지 확인

## <a name="overview"></a>개요

.NET 4.5에서 WIF 및 해당 클레임 기반 권한 부여는 프레임워크의 필수적인 부분으로 포함되었습니다. 이전에는 ASP.NET 사용자의 클레임을 원할 경우 WIF를 설치하고 나서 인터페이스를 주체 개체(예: `Thread.CurrentPrincipal` 또는 `HttpContext.Current.User`)로 캐스팅해야 했습니다. 이제 클레임은 이러한 주체 개체를 통해 자동으로 제공됩니다.

Forms로 인증된 모든 사용자는 클레임이 자동으로 연결되므로 .NET 4.5에 포함된 WIF를 Forms 인증에 활용할 수 있습니다. 이 방법에서 설명하는 것처럼 Forms 인증을 사용하는 ASP.NET 애플리케이션에서 즉시 이러한 클레임을 사용하기 시작할 수 있습니다.

## <a name="summary-of-steps"></a>단계 요약

- 1단계 – 간단한 ASP.NET Web Forms 애플리케이션 만들기

- 2단계 – Forms 인증을 사용하여 클레임에 대한 ASP.NET Web Forms 애플리케이션 구성

- 3단계 - 솔루션 테스트

## <a name="step-1--create-a-simple-aspnet-web-forms-application"></a>1단계 – 간단한 ASP.NET Web Forms 애플리케이션 만들기

이 단계에서는 새로운 ASP.NET Web Forms 애플리케이션을 만듭니다.

### <a name="to-create-a-simple-aspnet-application"></a>간단한 ASP.NET 애플리케이션을 만들려면

1. Visual Studio를 시작하고 **파일**, **새로 만들기**, **프로젝트**를 차례로 클릭합니다.

2. **새 프로젝트** 창에서 **ASP.NET Web Forms 응용 프로그램**을 클릭합니다.

3. **이름**에서 `TestApp`을 입력하고 **확인**을 누릅니다.

## <a name="step-2--configure-aspnet-web-forms-application-for-claims-using-forms-authentication"></a>2단계 – Forms 인증을 사용하여 클레임에 대한 ASP.NET Web Forms 애플리케이션 구성

이 단계에서는 *Web.config* 구성 파일에 구성 항목을 추가하고 *Default.aspx* 파일을 편집하여 계정에 대한 클레임 정보를 표시합니다.

### <a name="to-configure-aspnet-application-for-claims-using-forms-authentication"></a>Forms 인증을 사용하여 클레임에 대한 ASP.NET 애플리케이션을 구성하려면

1. *Default.aspx* 파일에서 기존 태그를 다음과 같이 바꿉니다.

    ```aspx
    <%@ Page Title="Home Page" Language="C#" MasterPageFile="~/Site.Master" AutoEventWireup="true" CodeBehind="Default.aspx.cs" Inherits="TestApp._Default" %>

    <asp:Content runat="server" ID="BodyContent" ContentPlaceHolderID="MainContent">
        <p>
            This page displays the claims associated with a Forms authenticated user.
        </p>
        <h3>Your Claims</h3>
        <p>
            <asp:GridView ID="ClaimsGridView" runat="server" CellPadding="3">
                <AlternatingRowStyle BackColor="White" />
                <HeaderStyle BackColor="#7AC0DA" ForeColor="White" />
            </asp:GridView>
        </p>
    </asp:Content>
    ```

    이 단계에서는 Forms 인증에서 검색된 클레임으로 채워질 *Default.aspx* 페이지에 GridView 컨트롤을 추가합니다.

2. *Default.aspx* 파일을 저장하고 나서 *Default.aspx.cs*라는 코드 숨김 파일을 엽니다. 기존 코드를 다음으로 바꿉니다.

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

                if (claimsPrincipal != null)
                {
                    this.ClaimsGridView.DataSource = claimsPrincipal.Claims;
                    this.ClaimsGridView.DataBind();
                }
            }
        }
    }
    ```

    위의 코드는 Forms 인증으로 식별된 사용자를 포함하여 인증된 사용자에 대한 클레임을 표시합니다.

## <a name="step-3--test-your-solution"></a>3단계 - 솔루션 테스트

이 단계에서는 ASP.NET Web Forms 애플리케이션을 테스트하고 사용자가 Forms 인증으로 로그인할 때 클레임이 제공되는지 확인합니다.

### <a name="to-test-your-aspnet-web-forms-application-for-claims-using-forms-authentication"></a>Forms 인증을 사용하여 클레임에 대한 ASP.NET Web Forms 애플리케이션을 테스트하려면

1. **F5** 키를 눌러 응용 프로그램을 빌드하고 실행합니다. 페이지의 오른쪽 위에 **등록** 및 **로그인** 링크가 있는 *Default.aspx*가 제공되어야 합니다. **등록**을 클릭합니다.

2. **등록** 페이지에서 사용자 계정을 만든 다음 **등록**을 클릭합니다. Forms 인증을 사용하여 계정이 만들어지며, 자동으로 로그인됩니다.

3. 홈페이지로 리디렉션된 후 계정에 대한 **Issuer**, **OriginalIssuer**, **Type**, **Value** 및 **ValueType** 클레임 정보를 포함하는 표가 **클레임** 제목 아래에 표시됩니다.
