---
title: WCF 서비스 및 ASP.NET
ms.date: 03/30/2017
ms.assetid: b980496a-f0b0-4319-8e55-a0f0fa32da70
ms.openlocfilehash: d42787492b00b8e0a5a732d641947fec61b5ff96
ms.sourcegitcommit: d6e27023aeaffc4b5a3cb4b88685018d6284ada4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67663676"
---
# <a name="wcf-services-and-aspnet"></a>WCF 서비스 및 ASP.NET

이 항목에서는 호스팅 Windows Communication Foundation (WCF) 서비스-side-by-side ASP.NET 및 ASP.NET 호환 모드에서 호스트 하를 사용 하 여 설명 합니다.

## <a name="hosting-wcf-side-by-side-with-aspnet"></a>WCF-side-by-side asp.net 호스팅

인터넷 정보 서비스 (IIS)에서 호스팅되는 WCF 서비스를 사용 하 여 찾을 수 있습니다. ASPX 페이지 및 단일의 공통 응용 프로그램 도메인 내에서 ASMX 웹 서비스입니다. ASP.NET은 AppDomain 관리 및 WCF 및 ASP.NET HTTP 런타임 모두에 대 한 동적 컴파일과 같은 공통 인프라 서비스를 제공합니다. WCF에 대 한 기본 구성은 side-by-side-ASP.NET을 사용 하 여 합니다.

![WCF 서비스와 ASP.NET을 보여 주는 스크린 샷: 상태를 공유 합니다.](./media/wcf-services-and-aspnet/windows-communication-foundation-services-asp-dotnet-configuration.gif)

ASP.NET HTTP 런타임은 ASP.NET 요청을 처리 하지만 이러한 서비스는 ASP.NET 콘텐츠는 동일한 AppDomain에서 호스트 하는 경우에 WCF 서비스에 대 한 요청 처리에 참여 하지 않습니다. 대신 WCF 서비스 모델을 WCF 서비스에 주소가 지정 된 메시지를 차단 하 고 WCF 전송/채널 스택을 통해 라우트 합니다.

동시 모델의 결과는 다음과 같습니다.

- ASP.NET 및 WCF 서비스는 AppDomain 상태를 공유할 수 있습니다. 두 프레임 워크 동일한 AppDomain에서 공존할 수 있으므로 WCF는 (정적 변수, 이벤트 및 등 포함)는 ASP.NET과 AppDomain 상태를 공유할 수도 있습니다.

- WCF 서비스 호스팅 환경 및 전송과 독립적으로 일관성 있게 동작 합니다. ASP.NET HTTP 런타임은 IIS/ASP.NET 호스팅 환경 및 HTTP 통신에 의도적으로 연결됩니다. 반대로, WCF는 호스팅 환경에서 일관성 있게 동작 하도록 (WCF 모두 일관성 있게 동작 내에서 IIS 내부 및 외부) 및 전송을 통해 (이상 및 IIS 7.0에서 호스팅되는 서비스를 노출 하는 모든 끝점에 걸쳐 일관 된 동작에 경우에 일부 끝점이 사용 하 여 HTTP 이외의 프로토콜).

- AppDomain 내에서 HTTP 런타임에 의해 구현 된 기능에는 ASP.NET 콘텐츠 아니라 WCF 적용 됩니다. ASP.NET 응용 프로그램 플랫폼의 많은 HTTP 관련 기능은 ASP.NET 내용이 포함 된 AppDomain의 내부에서 호스팅되는 WCF 서비스에 적용 되지 않습니다. 이러한 기능의 예는 다음과 같습니다.

  - HttpContext: <xref:System.Web.HttpContext.Current%2A> 항상 `null` WCF 서비스 내에서 액세스 하는 경우. 대신 <xref:System.ServiceModel.Channels.RequestContext>를 사용하세요.

  - 파일 기반 권한 부여: WCF 보안 모델에서는 서비스 요청 권한이 있는지 결정 하는 경우 서비스의.svc 파일에 적용할 액세스 제어 목록 (ACL)에 대 한 수 없습니다.

  - 구성 기반 URL 권한 부여: 마찬가지로, WCF 보안 모델을 따르지 않으면 System.Web의에서 지정 된 URL 기반 권한 부여 규칙 \<권한 부여 > 구성 요소입니다. WCF 요청은 ASP로 보호 되는 URL 공간에 상주 하는 경우 이러한 설정은 무시 됩니다. NET의 URL 권한 부여 규칙입니다.

  - HttpModule 확장성: WCF 호스팅 인프라 가로채 WCF 요청 하는 경우는 <xref:System.Web.HttpApplication.PostAuthenticateRequest> 이벤트가 발생 하 고 ASP.NET HTTP 파이프라인에 처리를 반환 하지 않습니다. 코딩 된 모듈은 파이프라인의 이후 단계에서 요청을 가로채도록 WCF 요청 가로채지 않습니다.

  - ASP.NET 가장: 기본적으로 WCF 요청 항상 실행 되는 IIS 프로세스 id로 ASP.NET이 System.Web의를 사용 하는 가장을 사용 하도록 설정 하려면 설정 되어 있어도 \<impersonate = "true" / > 구성 옵션입니다.

이러한 제한 사항은 IIS 응용 프로그램에서 호스팅되는 WCF 서비스에만 적용 됩니다. ASP.NET 내용의 동작은 WCF의 현재 상태를 받지 않습니다.

일반적으로 HTTP 파이프라인에서 제공 하는 기능을 필요로 하는 WCF 응용 프로그램 호스트 및 전송 독립적인는 WCF 관련 정보를 사용 하 여 고려해 야 합니다.

- <xref:System.ServiceModel.OperationContext> 대신 <xref:System.Web.HttpContext> 사용

- ASP.NET의 File/URL 권한 부여 대신 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior> 사용

- HTTP 모듈 대신 <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector> 또는 사용자 지정 계층화된 채널 사용

- System.Web 가장 대신 WCF를 사용 하 여 각 작업에 대 한 가장 합니다.

또는 WCF의 ASP.NET 호환 모드에서 서비스를 실행할 수도 있습니다.

## <a name="hosting-wcf-services-in-aspnet-compatibility-mode"></a>ASP.NET 호환 모드에서 WCF 서비스 호스팅

WCF 모델 호스팅 환경 및 전송에서 일관성 있게 동작 하도록 디자인 되었지만, 시나리오가 종종 응용 프로그램이이 수준의 유연성 필요 하지 않습니다. WCF의 ASP.NET 호환 모드 호스트 IIS 외부에서 또는 HTTP 이외의 프로토콜을 통해 통신 하는 기능이 필요 하지는 않지만 모든 ASP.NET 웹 응용 프로그램 플랫폼의 기능을 사용 하는 시나리오에 적합 합니다.

WCF 호스팅 인프라 WCF 메시지를 가로채서 않았고 하 고 HTTP 파이프라인에서 경로 기본 side-by-side-구성에서는 달리 ASP.NET 호환 모드에서 실행 되는 WCF 서비스 ASP.NET HTTP 요청 수명에 완전히 참여 합니다. 호환성 모드에서 WCF 서비스 사용을 통해 HTTP 파이프라인은 <xref:System.Web.IHttpHandler> 구현에서 ASPX 페이지 및 ASMX 웹 서비스의 처리에 대 한 방식으로 요청와 비슷합니다. 결과적으로, WCF 동일 하 게 동작 ASMX는 다음 ASP.NET 기능과 관련 하 여:

- <xref:System.Web.HttpContext>: ASP.NET 호환 모드에서 실행 되는 WCF 서비스에 액세스할 수 <xref:System.Web.HttpContext.Current%2A> 및 연결 된 상태입니다.

- 파일 기반 권한 부여: 파일 시스템 액세스 제어 목록 (Acl) 서비스의.svc 파일에 연결 하 여 ASP.NET 호환 모드에서 실행 되는 WCF 서비스 보안 될 수 있습니다.

- URL 권한 부여를 구성할 수 있습니다. ASP 합니다. WCF 서비스가 ASP.NET 호환 모드에서 실행 중인 경우 WCF 요청에 대 한 NET의 URL 권한 부여 규칙이 적용 됩니다.

- <xref:System.Web.HttpModuleCollection> 확장성: ASP.NET 호환 모드에서 실행 되는 WCF 서비스는 ASP.NET HTTP 요청 수명에 완전히 참여, 때문에 HTTP 파이프라인에 구성 된 모든 HTTP 모듈은 서비스 호출 전후 WCF 요청에서 작동할 수 있습니다.

- ASP.NET 가장: ASP.NET의 현재 id를 사용 하 여 실행 하는 WCF 서비스 응용 프로그램에 대 한 ASP.NET 가장을 사용 하도록 설정 된 경우 IIS 프로세스 id를 다 수 있는 스레드를 가장 합니다. ASP.NET 가장 및 WCF 가장 모두 특정 서비스 작업을 사용 하는 경우 서비스 구현을 궁극적으로 WCF에서 가져온 id를 사용 하 여 실행 합니다.

WCF의 ASP.NET 호환 모드 (응용 프로그램의 Web.config 파일에 있음) 다음 구성을 통해 응용 프로그램 수준에서 사용 하도록 설정 됩니다.

```xml
<system.serviceModel>
    <serviceHostingEnvironment aspNetCompatibilityEnabled="true" />
</system.serviceModel>
```

기본값은 "`true`" 지정 되지 않은 경우. 이 값을 설정 "`false`" 응용 프로그램에서 실행 중인 모든 WCF 서비스가 ASP.NET 호환 모드에서 실행 되지 것입니다 나타냅니다.

개별 서비스 구현 asp.net 응용 프로그램 내에서 실행할지 여부를 제어할 수 있는 ASP.NET 호환 모드는 근본적으로 다른 WCF 기본 요청 처리 의미 체계 의미 하기 때문에 호환성 모드가 설정 되었습니다. 서비스는 <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsAttribute>를 사용하여 ASP.NET 호환 모드를 지원할지 여부를 나타낼 수 있습니다. 이 특성의 기본값은 <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode.Allowed>입니다.

```csharp
[AspNetCompatibilityRequirements(RequirementsMode = AspNetCompatibilityRequirementsMode.Allowed)]
public class CalculatorService : ICalculatorSession
{//Implement calculator service methods.}
```

다음 표에서는 애플리케이션 수준의 호환 모드 설정이 개별 서비스에 명시된 지원 수준과 상호 작용하는 방법을 보여 줍니다.

|애플리케이션 수준의 호환 모드 설정|[AspNetCompatibilityRequirementsMode]<br /><br /> 설정|확인된 결과|
|--------------------------------------------------|---------------------------------------------------------|---------------------|
|aspNetCompatibilityEnabled = "`true`"|<xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode.Required>|서비스가 활성화됩니다.|
|aspNetCompatibilityEnabled = "`true`"|<xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode.Allowed>|서비스가 활성화됩니다.|
|aspNetCompatibilityEnabled = "`true`"|<xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode.NotAllowed>|서비스가 메시지를 수신할 때 활성화 오류가 발생합니다.|
|aspNetCompatibilityEnabled = "`false`"|<xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode.Required>|서비스가 메시지를 수신할 때 활성화 오류가 발생합니다.|
|aspNetCompatibilityEnabled = "`false`"|<xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode.Allowed>|서비스가 활성화됩니다.|
|aspNetCompatibilityEnabled = "`false`"|<xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode.NotAllowed>|서비스가 활성화됩니다.|

> [!NOTE]
> IIS 7.0과 WAS에 WCF 서비스를에서 HTTP 이외의 프로토콜을 통해 통신할 수 있습니다. 그러나 ASP.NET 호환 모드 사용 하도록 설정 하는 응용 프로그램에서 실행 되는 WCF 서비스 HTTP가 아닌 끝점을 노출할 허용 되지 않습니다. 이러한 구성은 서비스에서 첫 번째 메시지를 수신할 때 활성화 예외를 생성합니다.

WCF 서비스에 대 한 ASP.NET 호환 모드를 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 참조 하세요. <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode> 하며 [ASP.NET 호환성](../samples/aspnet-compatibility.md) 샘플입니다.

## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsAttribute>
- [Windows Server App Fabric 호스팅 기능](https://docs.microsoft.com/previous-versions/appfabric/ee677189(v=azure.10))
