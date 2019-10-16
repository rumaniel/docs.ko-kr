---
title: JSONP
ms.date: 03/30/2017
ms.assetid: c13b4d7b-dac7-4ffd-9f84-765c903511e1
ms.openlocfilehash: 1fc85838d7491f94b8da1e0ab458d6d021cd2b32
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70989771"
---
# <a name="jsonp"></a>JSONP
이 샘플에서는 WCF REST 서비스에서 JSONP(JSON with Padding)를 지원하는 방법을 보여 줍니다. JSONP는 스크립트 태그를 현재 문서에서 생성함으로써 도메인의 제한 없이 스크립트를 호출하는 데 사용되는 규칙입니다. 결과는 지정된 콜백 함수를 통해 반환됩니다. JSONP은와 `<script src="http://..." >` 같은 태그가 모든 도메인의 스크립트를 평가할 수 있으며 이러한 태그로 검색 된 스크립트는 다른 기능이 이미 정의 되어 있을 수 있는 범위 내에서 평가 된다는 개념을 기반으로 합니다.

## <a name="demonstrates"></a>세부 항목
 JSONP를 사용한 도메인 간 스크립팅

## <a name="discussion"></a>토론
 이 샘플에는 브라우저에 렌더링된 후 스크립트 블록을 동적으로 추가하는 웹 페이지가 포함되어 있습니다. 이 스크립트 블록은 단일 작업 `GetCustomer`가 있는 WCF REST 서비스를 호출합니다. WCF REST 서비스는 고객의 이름 및 주소를 콜백 함수 이름으로 래핑하여 반환합니다. WCF REST 서비스가 응답하면 고객 데이터를 사용하여 웹 페이지에 대한 콜백 함수가 호출되며 이 콜백 함수는 웹 페이지에 데이터를 표시합니다. 스크립트 태그의 삽입과 콜백 함수의 실행은 ASP.NET AJAX ScriptManager 컨트롤에서 자동으로 처리됩니다. 이 사용 패턴은 모든 ASP.NET AJAX 프록시와 동일하지만 다음 코드와 같이 JSONP를 사용하도록 설정하기 위한 한 줄이 추가되었습니다.

```csharp
var proxy = new JsonpAjaxService.CustomerService();
proxy.set_enableJsonp(true);
proxy.GetCustomer(onSuccess, onFail, null);
```

 WCF REST 서비스에서는 <xref:System.ServiceModel.Description.WebScriptEndpoint>가 `crossDomainScriptAccessEnabled`로 설정된  `true`를 사용하므로 웹 페이지에서 이 서비스를 호출할 수 있습니다. 이러한 구성은 모두 system.servicemodel > 요소 아래의 \<web.config 파일에서 수행 됩니다.

```xml
<system.serviceModel>
  <serviceHostingEnvironment aspNetCompatibilityEnabled="true"/>
  <standardEndpoints>
    <webScriptEndpoint>
      <standardEndpoint name="" crossDomainScriptAccessEnabled="true"/>
    </webScriptEndpoint>
  </standardEndpoints>
</system.serviceModel>
```

 ScriptManager는 서비스와의 상호 작용을 관리하며 JSONP 액세스를 수동으로 구현하는 복잡한 과정을 단순하게 해 줍니다. 가 `crossDomainScriptAccessEnabled` 로`true` 설정 되 고 작업의 응답 형식이 JSON 인 경우 WCF 인프라는 콜백 쿼리 문자열 매개 변수에 대 한 요청의 URI를 검사 하 고 콜백 쿼리 문자열의 값으로 JSON 응답을 래핑합니다. 변수에. 샘플의 웹 페이지에서는 다음 URI를 사용하여 WCF REST 서비스를 호출합니다.

```http
http://localhost:33695/CustomerService/GetCustomer?callback=Sys._json0
```

 콜백 쿼리 문자열 매개 변수에는 `JsonPCallback` 값이 있으므로 WCF 서비스에서는 다음 예제와 같이 JSONP 응답을 반환합니다.

```json
Sys._json0({"__type":"Customer:#Microsoft.Samples.Jsonp","Address":"1 Example Way","Name":"Bob"});
```

 이 JSONP 응답에는 JSON으로 형식이 지정되고 웹 페이지에서 요청한 콜백 함수 이름으로 래핑된 고객 데이터가 포함됩니다. ScriptManager는 스크립트 태그를 사용하는 이 콜백을 실행하여 도메인 간 요청을 수행한 다음 ASP.NET AJAX 프록시의 GetCustomer 작업에 전달된 onSuccess 처리기에 결과를 전달합니다.

 이 샘플은 두 개의 ASP.NET 웹 응용 프로그램으로 구성 되어 있습니다. 하나는 WCF 서비스를 포함 하 고 다른 하나는 서비스를 호출 하는 .aspx 웹 페이지를 포함 합니다. 솔루션을 실행 하는 경우 Visual Studio 2012는 서로 다른 도메인에서 서비스와 클라이언트가 살고 있는 환경을 만드는 다른 포트에서 두 웹 사이트를 호스팅합니다.

> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\AJAX\JSONP`  
  
#### <a name="to-run-the-sample"></a>이 샘플을 실행하려면  
  
1. JSONP 샘플의 솔루션을 엽니다.  
  
2. F5 키를 눌러 `http://localhost:26648/JSONPClientPage.aspx` 브라우저에서 시작 합니다.  
  
3. 페이지가 로드 된 후에는 "Name" 및 "Address"에 대 한 텍스트 입력이 값으로 채워집니다.  이러한 값은 브라우저에서 페이지 렌더링을 마친 후 WCF 서비스 호출에서 제공 되었습니다.
