---
title: '방법: WIF를 사용하여 로그인 상태 표시'
ms.date: 03/30/2017
ms.assetid: 4d1174e4-5397-4962-9a5f-3b1ad7b3fc14
author: BrucePerlerMS
ms.openlocfilehash: d2500c6ded485fca76715425b9a52258e07be08d
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70851546"
---
# <a name="how-to-display-signed-in-status-using-wif"></a>방법: WIF를 사용하여 로그인 상태 표시
## <a name="applies-to"></a>적용 대상  
  
- Microsoft® Windows® Identity Foundation(WIF) 4.5  
  
- ASP.NET® Web Forms  
  
## <a name="summary"></a>요약  
 이 항목에서는 WIF 사용 가능 ASP.NET 애플리케이션에서 로그인 상태를 표시하는 방법을 설명합니다. WIF는 애플리케이션이 클레임을 인식하도록 설정하고 애플리케이션 리소스에 대한 인증 및 권한 부여를 관리하기 위한 메커니즘을 제공합니다.  
  
## <a name="contents"></a>목차  
  
- 개요  
  
- 단계 요약  
  
- 1단계 – ID 및 액세스 도구 확장 설치  
  
- 2단계 – 신뢰 당사자 ASP.NET 애플리케이션 만들기  
  
- 3단계 – 로컬 개발 STS를 사용하여 사용자 인증  
  
- 4단계 – ASP.NET 애플리케이션을 수정하여 로그인 상태 표시  
  
- 5단계 – WIF 및 ASP.NET 애플리케이션 간 통합 테스트  
  
## <a name="overview"></a>개요  
 이 항목에서는 WIF를 사용하여 간단한 클레임 인식 애플리케이션을 만드는 방법 및 사용자가 로그인되어 있는지 여부를 쉽게 표시하는 방법을 보여 줍니다. 다음 단계에서는 ID 및 액세스 Visual Studio 확장과 함께 제공되는 로컬 개발 STS를 사용합니다. 로컬 개발 STS는 클레임을 애플리케이션에 통합하는 간단한 메서드를 제공하기 위해 테스트 및 개발 환경에서 사용되어야 합니다. 실제 인증을 수행하지 않고 자격 증명이 필요하지 않으므로 프로덕션 환경에서 사용하면 안 됩니다. 그러나 실제 인증을 사용하는 프로덕션 준비 애플리케이션의 경우 다음 단계의 명령형 코드가 동일합니다.  
  
## <a name="summary-of-steps"></a>단계 요약  
  
- 1단계 – ID 및 액세스 도구 확장 설치  
  
- 2단계 – 신뢰 당사자 ASP.NET 애플리케이션 만들기  
  
- 3단계 – 로컬 개발 STS를 사용하여 사용자 인증  
  
- 4단계 – ASP.NET 애플리케이션을 수정하여 로그인 상태 표시  
  
- 5단계 – WIF 및 ASP.NET 애플리케이션 간 통합 테스트  
  
## <a name="step-1--install-the-identity-and-access-extension"></a>1단계 – ID 및 액세스 도구 확장 설치  
 이 단계에서는 Visual Studio 2012에 대한 ID 및 액세스 확장을 구성하는 방법을 설명합니다. 이 확장은 STS 엔드포인트와 통신하도록 애플리케이션을 구성하는 프로세스를 자동화합니다.  
  
### <a name="to-install-the-identity-and-access-extension"></a>ID 및 액세스 확장을 설치하려면  
  
1. 관리자로 승격된 모드에서 Visual Studio를 시작합니다.  
  
2. Visual Studio에서 **도구**, **확장 관리자**를 차례로 클릭합니다. **확장 관리자** 창이 표시됩니다.  
  
3. **확장 관리자**의 왼쪽 메뉴에서 **온라인 확장**을 클릭하고 **Visual Studio 갤러리**를 선택합니다.  
  
4. **확장 관리자**의 오른쪽 위에서 *ID 및 액세스*를 검색합니다.  
  
5. **ID 및 액세스** 항목이 검색 결과에 나타납니다. 해당 항목을 클릭하고 **다운로드**를 클릭합니다.  
  
6. **다운로드 및 설치** 대화 상자가 나타납니다. 사용 약관에 동의하면 **설치**를 클릭합니다.  
  
7. **ID 및 액세스** 확장이 설치를 완료하면 관리자 모드에서 Visual Studio를 다시 시작합니다.  
  
## <a name="step-2--create-a-relying-party-aspnet-application"></a>2단계 – 신뢰 당사자 ASP.NET 애플리케이션 만들기  
 이 단계에서는 WIF와 통합될 신뢰 당사자 ASP.NET Web Forms 애플리케이션을 만드는 방법을 설명합니다.  
  
### <a name="to-create-a-simple-aspnet-application"></a>간단한 ASP.NET 애플리케이션을 만들려면  
  
1. Visual Studio를 시작하고 **파일**, **새로 만들기**, **프로젝트**를 차례로 클릭합니다.  
  
2. **새 프로젝트** 창에서 **ASP.NET Web Forms 응용 프로그램**을 클릭합니다.  
  
3. **이름**에서 `TestApp`을 입력하고 **확인**을 누릅니다.  
  
## <a name="step-3--enable-local-development-sts-to-authenticate-users"></a>3단계 – 로컬 개발 STS를 사용하여 사용자 인증  
 이 단계에서는 애플리케이션에서 로컬 개발 STS를 사용하도록 설정하는 방법을 설명합니다. 로컬 개발 STS는 Visual Studio용 ID 및 액세스 확장을 통해 사용하도록 설정합니다.  
  
### <a name="to-enable-local-development-sts-in-your-aspnet-application"></a>ASP.NET 애플리케이션에서 로컬 개발 STS를 사용하도록 설정하려면  
  
1. Visual Studio의 **솔루션 탐색기**에서 **TestApp** 프로젝트를 마우스 오른쪽 단추로 클릭하고 **ID 및 액세스**를 선택합니다.  
  
2. **ID 및 액세스** 창이 나타납니다. **공급자**에서 **로컬 개발 STS로 응용 프로그램 테스트**를 선택한 다음 **적용**을 클릭합니다.  
  
## <a name="step-4--modify-your-aspnet-application-to-display-sign-in-status"></a>4단계 – ASP.NET 애플리케이션을 수정하여 로그인 상태 표시  
 이 단계에서는 ASP.NET 애플리케이션을 수정하여 현재 사용자가 로그인되어 있는지 여부를 동적으로 표시하는 방법을 설명합니다. STS 공급자가 구성되면 WIF가 들어오는 클레임을 처리합니다. 이제 인증 결과를 표시하도록 애플리케이션 코드를 구성해야 합니다.  
  
### <a name="to-display-sign-in-status"></a>로그인 상태를 표시하려면  
  
1. Visual Studio의 **TestApp** 프로젝트에서 **Default.aspx** 파일을 엽니다.  
  
2. **Default.aspx** 파일의 기존 태그를 다음 태그로 바꿉니다.  
  
    ```aspx-csharp  
    <%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>  
  
    <!DOCTYPE html>  
  
    <html>  
    <head runat="server">  
        <title>Logged In Status</title>  
    </head>  
    <body>  
        <asp:label ID="myLabel" runat="server" />  
    </body>  
    </html>  
    ```  
  
3. **Default.aspx**를 저장하고 나서 **Default.aspx.cs**라는 코드 숨김 파일을 엽니다.  
  
    > [!NOTE]
    > **Default.aspx.cs**는 솔루션 탐색기에서 **Default.aspx** 아래에 숨겨질 수 있습니다. **Default.aspx.cs**가 표시되지 않으면 옆에 있는 삼각형을 클릭하여 **Default.aspx**를 확장합니다.  
  
4. **Default.aspx.cs**의 기존 코드를 다음 코드로 바꿉니다.  
  
    ```csharp  
    using System;  
    using System.Web.UI;  
    using System.Security.Claims;  
  
    namespace TestApp  
    {  
        protected void Page_Load(object sender, EventArgs e)  
        {  
            ClaimsPrincipal claimsPrincipal = Thread.CurrentPrincipal as ClaimsPrincipal;  
  
            if (claimsPrincipal != null)  
            {  
                myLabel.Text = "You are signed in.";  
            }  
            else  
            {  
                myLabel.Text = "You are not signed in.";  
            }  
        }  
    }  
    ```  
  
5. **Default.aspx.cs**를 저장하고 응용 프로그램을 빌드합니다.  
  
## <a name="step-5--test-the-integration-between-wif-and-your-aspnet-application"></a>5단계 – WIF 및 ASP.NET 애플리케이션 간 통합 테스트  
 이 단계에서는 WIF 및 ASP.NET 애플리케이션 간 통합을 테스트하는 방법을 설명합니다.  
  
### <a name="to-test-the-integration-between-wif-and-aspnet"></a>WIF 및 ASP.NET 응용 프로그램 간 통합을 테스트하려면  
  
1. Visual Studio에서 **F5** 키를 눌러 애플리케이션 디버깅을 시작합니다. 오류가 발견되지 않으면 새 브라우저 창이 열립니다.  
  
2. 브라우저가 요청을 STS로 자동으로 리디렉션하고 나서 Default.aspx 페이지를 엽니다. WIF이 제대로 구성 된 경우 사이트에 다음 텍스트가 표시 됩니다. **"사용자가 로그인**했습니다."
