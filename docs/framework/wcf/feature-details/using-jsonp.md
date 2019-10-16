---
title: JSONP 사용
ms.date: 03/30/2017
ms.assetid: f386718c-b4ba-4931-a610-40c27a46672a
ms.openlocfilehash: 622fbdbf2674aea552cfd57f528d7cc5168cfda8
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61932836"
---
# <a name="using-jsonp"></a>JSONP 사용

JSONP(JSON Padding)는 웹 브라우저에서 사이트 간 스크립팅을 지원할 수 있도록 하는 메커니즘입니다. JSONP는 현재 로드된 문서를 가져온 사이트가 아닌 다른 사이트에서 스크립트를 로드하는 웹 브라우저의 기능을 기반으로 설계되었습니다. 이 메커니즘은 다음 예제와 같이 JSON 페이로드를 사용자 정의 콜백 함수 이름으로 채우는 방식으로 작동합니다.

```javascript
callback({"a" = \\"b\\"});
```

위의 예제에서 `{"a" = \\"b\\"}` JSON 페이로드는 `callback` 함수 호출로 래핑됩니다. 콜백 함수는 현재 웹 페이지에 이미 정의되어 있어야 합니다. JSONP 응답의 콘텐츠 형식은 `application/javascript`합니다.

JSONP는 자동으로 사용되도록 설정되지 않습니다. JSONP를 사용하도록 설정하려면 다음 예제와 같이 HTTP 표준 엔드포인트(`javascriptCallbackEnabled` 또는 `true`) 중 하나에서 <xref:System.ServiceModel.Description.WebHttpEndpoint> 특성을 <xref:System.ServiceModel.Description.WebScriptEndpoint>로 설정합니다.

```xml
<system.serviceModel>
  <standardEndpoints>
    <webHttpEndpoint>
      <standardEndpoint name="" javascriptCallbackEnabled="true"/>
    </webHttpEndpoint>
  </standardEndpoints>
</system.serviceModel>
```

콜백 함수 이름은 다음 URL과 같이 callback이라는 쿼리 변수에 지정할 수 있습니다.

`http://baseaddress/Service/RestService?callback=functionName`

이 서비스는 호출되면 다음과 같은 응답을 보냅니다.

```javascript
functionName({"root":"Something"});
```  

또한 다음과 같이 서비스 클래스에 <xref:System.ServiceModel.Web.JavascriptCallbackBehaviorAttribute>를 적용하여 콜백 함수 이름을 지정할 수도 있습니다.

```csharp
[ServiceContract]
[JavascriptCallbackBehavior(ParameterName = "$callback")]
public class Service1
{
    [OperationContract]
    [WebGet(ResponseFormat=WebMessageFormat.Json)]
    public string GetData()
    {
    }
}
```

위에 나온 서비스는 다음을 사용하여 요청됩니다.

`http://baseaddress/Service/RestService?$callback=anotherFunction`

이 서비스는 호출되면 다음을 사용하여 응답합니다.

```javascript
anotherFunction ({"root":"Something"});
```

## <a name="http-status-codes"></a>HTTP 상태 코드

200 이외의 HTTP 상태 코드가 있는 JSONP 응답에는 다음 예제와 같이 HTTP 상태 코드의 숫자 표현이 있는 두 번째 매개 변수가 포함됩니다.

```javascript
anotherFunction ({"root":"Something"}, 201);
```

## <a name="validations"></a>유효성 검사

JSONP를 사용하도록 설정한 경우 다음 유효성 검사가 수행됩니다.

- `javascriptCallback`이 사용되도록 설정되어 있고, 콜백 쿼리 문자열 매개 변수가 요청에 있고, 응답 형식이 JSON으로 설정된 경우 WCF 인프라에서 예외가 throw됩니다.

- 요청에 콜백 쿼리 문자열 매개 변수가 포함되어 있지만 작업이 HTTP GET이 아닌 경우 콜백 매개 변수가 무시됩니다.

- 콜백 이름이 `null`이거나 빈 문자열이면 응답 형식이 JSONP로 지정되지 않습니다.

## <a name="see-also"></a>참고자료

- [WCF 웹 HTTP 프로그래밍 모델 개요](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model-overview.md)
