---
title: AJAX Service Using Complex Types 샘플
ms.date: 03/30/2017
ms.assetid: 88242b99-4811-4cbe-8201-52ddf48fb174
ms.openlocfilehash: dce3e89449a036de7c4936963cfa0b36f3f08451
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70045826"
---
# <a name="ajax-service-using-complex-types-sample"></a>AJAX Service Using Complex Types 샘플

이 샘플에서는 WCF (Windows Communication Foundation)를 사용 하 여 복합 형식의 인스턴스를 만들고이를 서비스와 클라이언트 (JSON) JavaScript Object Notation로 전송 하는 AJAX (ASP.NET 비동기 JavaScript and XML) 서비스를 만드는 방법을 보여 줍니다. 웹 브라우저 클라이언트에서 JavaScript 코드를 사용하여 AJAX 서비스에 액세스할 수 있습니다. 이 샘플은 [기본 AJAX 서비스](../../../../docs/framework/wcf/samples/basic-ajax-service.md) 샘플을 기반으로 합니다.

WCF의 ajax 지원은 컨트롤을 <xref:System.Web.UI.ScriptManager> 통해 ASP.NET ajax와 함께 사용 하도록 최적화 되어 있습니다. ASP.NET AJAX에서 WCF를 사용 하는 예제는 [Ajax 샘플](ajax.md)을 참조 하세요.

> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.

다음 샘플의 서비스는 AJAX 특정 코드가 없는 WCF 서비스입니다. <xref:System.ServiceModel.Web.WebGetAttribute> 특성이 적용되지 않으므로 기본 HTTP 동사("POST")가 사용됩니다. 서비스에는 `DoMath`라는 복합 형식을 반환하는 단일 작업인 `MathResult`가 있습니다. 복합 형식은 마찬가지로 AJAX 특정 코드가 없는 표준 데이터 계약 형식입니다.

```csharp
[DataContract]
public class MathResult
{
    [DataMember]
    public double sum;
    [DataMember]
    public double difference;
    [DataMember]
    public double product;
    [DataMember]
    public double quotient;
}
```

기본 AJAX 서비스 샘플에서와 마찬가지로, <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory>를 사용하여 서비스에 AJAX 엔드포인트를 만듭니다.

클라이언트 웹 페이지 Complextypeclientpage.aspx에는 사용자가 페이지에서 **계산 수행** 단추를 클릭할 때 서비스를 호출 하는 ASP.NET 및 JavaScript 코드가 포함 되어 있습니다. 서비스를 호출 하는 코드는 HTTP post 샘플을 [사용 하는 AJAX 서비스](../../../../docs/framework/wcf/samples/ajax-service-using-http-post.md) 와 유사 하 게 JSON 본문을 생성 하 고 http post를 사용 하 여 보냅니다.

서비스 호출에 성공한 후 결과 JavaScript 개체에서 개별 데이터 멤버(`sum`, `difference`, `product` 및 `quotient`)에 액세스할 수 있습니다.

```javascript
function onSuccess(mathResult){
     document.getElementById("sum").value = mathResult.sum;
     document.getElementById("difference").value = mathResult.difference;
     document.getElementById("product").value = mathResult.product;
     document.getElementById("quotient").value = mathResult.quotient;
}
```

### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면

1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.

2. [Windows Communication Foundation 샘플 빌드](../../../../docs/framework/wcf/samples/building-the-samples.md)에 설명 된 대로 ComplexTypeAjaxService 솔루션을 빌드합니다.

3. 로 `http://localhost/ServiceModelSamples/ComplexTypeClientPage.aspx` 이동 합니다 (프로젝트 디렉터리에서 브라우저에서 complextypeclientpage.aspx를 열지 마세요.).

> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Ajax\ComplexTypeAjaxService`

## <a name="see-also"></a>참고자료

- [기본 AJAX 서비스](../../../../docs/framework/wcf/samples/basic-ajax-service.md)
