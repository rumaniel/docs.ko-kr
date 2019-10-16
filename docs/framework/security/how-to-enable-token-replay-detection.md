---
title: '방법: 토큰 재생을 검색하도록 설정'
ms.date: 03/30/2017
ms.assetid: 5a9f5771-f5f6-4100-8501-406aa20d731a
author: BrucePerlerMS
ms.openlocfilehash: 0149bf424751a0c95337743b02465629826d9686
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64625857"
---
# <a name="how-to-enable-token-replay-detection"></a>방법: 토큰 재생을 검색하도록 설정
## <a name="applies-to"></a>적용 대상  
  
- Microsoft® Windows® Identity Foundation(WIF)  
  
- ASP.NET® Web Forms  
  
## <a name="summary"></a>요약  
 이 방법은 WIF를 사용하는 ASP.NET 애플리케이션에서 토큰 재생 검색을 사용하도록 설정하기 위한 자세한 단계별 프로시저를 제공합니다. 또한 토큰 재생 검색이 사용되는지 확인하기 위해 애플리케이션을 테스트하는 방법에 대한 지침을 제공합니다. 이 방법 설명에 보안 토큰 서비스(STS)를 만들기 위한 자세한 지침은 없으며, 그 대신 ID 및 액세스 도구와 함께 제공되는 개발 STS를 사용합니다. 개발 STS가 실제 인증을 수행하는 것은 아니며, 테스트 목적으로만 사용됩니다. 이 방법을 완료하려면 ID 및 액세스 도구를 설치해야 합니다. 다음 위치에서 다운로드할 수 있습니다. [Id 및 액세스 도구](https://go.microsoft.com/fwlink/?LinkID=245849)  
  
## <a name="contents"></a>목차  
  
- 목표  
  
- 개요  
  
- 단계 요약  
  
- 1단계 – 간단한 ASP.NET Web Forms 애플리케이션 만들기 및 재생 검색 사용  
  
- 2단계 - 솔루션 테스트  
  
## <a name="objectives"></a>목표  
  
- ID 및 액세스 도구에서 WIF 및 개발 STS를 사용하는 간단한 ASP.NET 애플리케이션 만들기  
  
- 토큰 재생 검색 사용 및 작동하는지 확인  
  
## <a name="overview"></a>개요  
 클라이언트에서 이미 사용한 STS 토큰을 사용하여 신뢰 당사자에 대해 인증을 시도할 경우 재생 공격이 발생합니다. 이 공격을 방지하기 위해 WIF에는 이전에 사용된 STS 토큰의 재생 검색 캐시가 포함됩니다. 사용하도록 설정된 재생 검색은 들어오는 요청의 토큰을 확인하고 토큰이 이전에 사용되었는지 여부를 확인합니다. 토큰이 이미 사용된 경우 요청이 거부되고 <xref:System.IdentityModel.Tokens.SecurityTokenReplayDetectedException> 예외가 throw됩니다.  
  
 다음 단계에서는 재생 검색을 사용하는 데 필요한 구성 변경 내용을 보여 줍니다.  
  
## <a name="summary-of-steps"></a>단계 요약  
  
- 1단계 – 간단한 ASP.NET Web Forms 애플리케이션 만들기 및 재생 검색 사용  
  
- 2단계 - 솔루션 테스트  
  
## <a name="step-1--create-a-simple-aspnet-web-forms-application-and-enable-replay-detection"></a>1단계 – 간단한 ASP.NET Web Forms 애플리케이션 만들기 및 재생 검색 사용  
 이 단계에서는 새 ASP.NET Web Forms 애플리케이션을 만들고 *Web.config* 파일을 수정하여 재생 검색을 사용하도록 설정합니다.  
  
#### <a name="to-create-a-simple-aspnet-application"></a>간단한 ASP.NET 애플리케이션을 만들려면  
  
1. Visual Studio를 시작하고 **파일**, **새로 만들기**, **프로젝트**를 차례로 클릭합니다.  
  
2. **새 프로젝트** 창에서 **ASP.NET Web Forms 응용 프로그램**을 클릭합니다.  
  
3. **이름**에서 `TestApp`을 입력하고 **확인**을 누릅니다.  
  
4. **솔루션 탐색기**에서 **TestApp** 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **ID 및 액세스**를 선택합니다.  
  
5. **ID 및 액세스** 창이 나타납니다. **공급자**에서 **로컬 개발 STS로 응용 프로그램 테스트**를 선택한 다음 **적용**을 클릭합니다.  
  
6. 표시된 것처럼 다음 **\<tokenReplayDetection>** 요소를 *Web.config* 구성 파일의 **\<system.identityModel>** 및 **\<identityConfiguration>** 요소 바로 뒤에 추가합니다.  
  
    ```xml  
    <system.identityModel>  
        <identityConfiguration>  
            <tokenReplayDetection enabled="true"/>  
    ```  
  
## <a name="step-2--test-your-solution"></a>2단계 - 솔루션 테스트  
 이 단계에서는 WIF 사용 가능 ASP.NET 애플리케이션을 테스트하여 재생 검색이 사용하도록 설정되었는지 확인합니다.  
  
#### <a name="to-test-your-wif-enabled-aspnet-application-for-replay-detection"></a>재생 검색에 대한 WIF 사용 가능 ASP.NET 애플리케이션을 테스트하려면  
  
1. **F5** 키를 눌러 솔루션을 실행합니다. 기본 ASP.NET 홈페이지가 표시되고 개발 STS에서 반환되는 기본 사용자인 사용자 이름 *Terry*로 자동으로 인증되어야 합니다.  
  
2. 브라우저의 **뒤로** 단추를 누릅니다. 사용 하 여 표시 되어야 합니다는 **'/' 응용 프로그램에서 서버 오류** 함께 다음 설명이 페이지: *ID1062: 재생 검색 되었습니다. 토큰: '있는 System.IdentityModel.Tokens.SamlSecurityToken'* 고 뒤에 *AssertionId* 와 *발급자*합니다.  
  
     토큰 재생이 검색될 때 <xref:System.IdentityModel.Tokens.SecurityTokenReplayDetectedException> 형식의 예외가 throw되었으므로 이 오류 페이지가 표시됩니다. 토큰이 먼저 제공된 경우 초기 POST 요청을 다시 보내려고 하므로 이 오류가 발생합니다. **뒤로** 단추를 선택해도 서버에 대한 후속 요청에서 이 동작이 수행되지 않습니다.
