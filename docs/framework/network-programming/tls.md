---
title: .NET Framework를 사용한 TLS(전송 계층 보안) 모범 사례
description: .NET Framework와 함께 TLS(전송 계층 보안)를 사용한 모범 사례를 설명합니다.
ms.date: 10/22/2018
helpviewer_keywords:
- sending data, Internet security
- protocols, Internet security
- Network security
- network resources, Internet security
- receiving data, Internet security
- authentication [.NET Framework], Internet security
- Internet, security
- security [.NET Framework], Internet
- permissions [.NET Framework], Internet
ms.openlocfilehash: ad15c0d4bd69417fffd8bcad0805a3b78321e05b
ms.sourcegitcommit: 5ae5a1a9520b8b8b6164ad728d396717f30edafc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/11/2019
ms.locfileid: "70894949"
---
# <a name="transport-layer-security-tls-best-practices-with-the-net-framework"></a>.NET Framework를 사용한 TLS(전송 계층 보안) 모범 사례

TLS(전송 계층 보안) 프로토콜은 인터넷을 통해 전달되는 개인 정보를 보호하는 데 도움이 되도록 설계된 업계 표준입니다. [TLS 1.2](https://tools.ietf.org/html/rfc5246)는 이전 버전보다 향상된 보안을 제공하는 표준입니다. TLS 1.2는 더 빠르고 보안이 향상된 가장 최근 릴리스된 표준 [TLS 1.3](https://tools.ietf.org/html/rfc8446)으로 대체됩니다. 이 문서에서는 TLS 프로토콜을 사용하는 .NET Framework 애플리케이션을 보호하기 위한 권장 사항을 제공합니다.

.NET Framework 애플리케이션이 안전하게 유지되도록 하려면 TLS 버전을 하드 코드하면 **안 됩니다**. .NET Framework 애플리케이션에서는 OS(운영 체제)가 지원하는 TLS 버전을 사용해야 합니다.

이 문서는 다음과 같은 개발자를 대상으로 합니다.

- <xref:System.Net> API(예: <xref:System.Net.Http.HttpClient?displayProperty=nameWithType> 및 <xref:System.Net.Security.SslStream?displayProperty=nameWithType>)를 직접 사용하는 개발자.
- <xref:System.ServiceModel?displayProperty=nameWithType> 네임스페이스를 통해 WCF 클라이언트 및 서비스를 직접 사용하는 개발자.
- [Azure Cloud Services](https://azure.microsoft.com/services/cloud-services/) 웹 및 작업자 역할을 사용하여 애플리케이션을 호스트 및 실행하는 개발자. [Azure Cloud Services](#azure-cloud-services) 섹션을 참조하세요.

다음을 권장합니다.

- 앱에서 .NET Framework 4.7 이상 버전을 대상으로 지정합니다. WCF 앱에서 .NET Framework 4.7.1 이상 버전을 대상으로 지정합니다.
- TLS 버전을 지정하지 마세요. OS에서 TLS 버전을 결정하도록 코드를 구성합니다.
- 철저한 코드 감사를 수행하여 TLS 또는 SSL 버전을 지정하지 않았는지 확인합니다.

앱에서 OS가 TLS 버전을 선택하도록 하는 경우:

- OS가 향후 추가되는 새 프로토콜(예: TLS 1.3)을 자동으로 활용합니다.
- OS는 검색되지 않는 OS 프로토콜을 차단합니다.

[코드 감사 및 변경](#audit-your-code-and-make-code-changes) 섹션에서는 코드를 감사하고 업데이트하는 방법을 설명합니다.

이 문서에서는 앱이 대상으로 하고 실행되는 버전의 .NET Framework에 대해 사용 가능한 가장 강력한 보안을 구현하는 방법을 설명합니다. 명시적으로 보안 프로토콜 및 버전을 설정하는 앱은 다른 대체 방법을 옵트아웃(opt out)하고 .NET Framework 및 OS 기본 동작을 옵트아웃(opt out)합니다. 앱이 TLS 1.2 연결을 협상할 수 있도록 하려는 경우 명시적으로 더 낮은 TLS 버전으로 설정하면 TLS 1.2 연결이 차단됩니다.

프로토콜 버전의 하드 코드를 피할 수 없는 경우에는 TLS 1.2를 지정하는 것이 좋습니다. TLS 1.0 종속성을 식별하고 제거하는 방법에 대한 지침은 [TLS 1.0 문제 해결](https://www.microsoft.com/download/details.aspx?id=55266) 백서를 다운로드합니다.

WCF는 .NET Framework 4.7의 기본값으로 TLS 1.0, 1.1 및 1.2를 지원합니다. .NET Framework 4.7.1부터 WCF 기본값은 운영 체제에 구성된 버전으로 설정됩니다. 애플리케이션이 명시적으로 `SslProtocols.None`으로 구성된 경우 WCF는 NetTcp 전송을 사용할 때 운영 체제 기본 설정을 사용합니다.

GitHub 문제 [.NET Framework를 사용한 TLS(전송 계층 보안) 모범 사례](https://github.com/dotnet/docs/issues/4675)에서 이 문서에 대한 질문을 할 수 있습니다.

## <a name="audit-your-code-and-make-code-changes"></a>코드 감사 및 변경

ASP.NET 애플리케이션의 경우 _web.config_의 `<system.web><httpRuntime targetFramework>` 요소를 검사하여 의도한 .NET Framework 버전을 사용하고 있는지 확인합니다.

Windows Forms 및 기타 애플리케이션의 경우 [방법: 한 버전의 .NET Framework를 대상으로 지정](/visualstudio/ide/how-to-target-a-version-of-the-dotnet-framework).

다음 섹션을 사용하여 특정 TLS 또는 SSL 버전을 사용하지 않는지 확인합니다.

## <a name="if-your-app-targets-net-framework-47-or-later-versions"></a>앱이 .NET Framework 4.7 이상 버전을 대상으로 하는 경우

다음 섹션에서는 특정 TLS 또는 SSL 버전을 사용하지 않는지 확인하는 방법을 보여줍니다.

### <a name="for-http-networking"></a>HTTP 네트워킹의 경우

.NET Framework 4.7 이상 버전을 사용하는 <xref:System.Net.ServicePointManager>는 OS에 구성된 기본 보안 프로토콜을 사용합니다. 기본 OS가 최적의 선택을 하도록 하려면(가능한 경우) <xref:System.Net.ServicePointManager.SecurityProtocol?displayProperty=nameWithType> 속성의 값(기본값은 <xref:System.Net.SecurityProtocolType.SystemDefault?displayProperty=nameWithType>)을 설정하지 마세요.

<xref:System.Net.SecurityProtocolType.SystemDefault?displayProperty=nameWithType> 설정으로 인해 <xref:System.Net.ServicePointManager>가 운영 체제에서 구성한 기본 보안 프로토콜을 사용하므로 애플리케이션이 실행되는 OS에 따라 다르게 실행될 수 있습니다. 예를 들어 Windows 7 SP1은 TLS 1.0을 사용하고 Windows 8 및 Windows 10은 TLS 1.2를 사용합니다.

.NET Framework 4.7 이상 버전의 HTTP 네트워킹을 대상으로 하는 경우에는 이 문서의 나머지 부분은 관련이 없습니다.

### <a name="for-tcp-sockets-networking"></a>TCP 소켓 네트워킹의 경우

.NET Framework 4.7 이상 버전을 사용하는 <xref:System.Net.Security.SslStream>는 가장 적합한 보안 프로토콜 및 버전을 선택하는 OS로 기본 설정됩니다. 기본 OS가 최적의 선택을 하도록 하려면(가능한 경우) 명시적 <xref:System.Security.Authentication.SslProtocols> 매개 변수를 사용하는 <xref:System.Net.Security.SslStream>의 메서드 오버로드를 사용하지 마세요. 그렇지 않으면 <xref:System.Security.Authentication.SslProtocols.None?displayProperty=nameWithType>을 전달합니다. <xref:System.Security.Authentication.SslProtocols.Default>를 사용하지 않는 것이 좋습니다. `SslProtocols.Default`를 설정하면 SSL 3.0/TLS 1.0이 강제로 사용되고 TLS 1.2가 차단됩니다.

<xref:System.Net.ServicePointManager.SecurityProtocol> 속성의 값을 설정하지 마세요(HTTP 네트워킹의 경우).

명시적 <xref:System.Security.Authentication.SslProtocols> 매개 변수를 사용하는 <xref:System.Net.Security.SslStream>의 메서드 오버로드를 사용하지 마세요(TCP 소켓 네트워킹의 경우). 앱의 대상을 .NET Framework 4.7 이상 버전으로 변경하면 모범 사례 권장 사항을 따르게 됩니다.

TCP 소켓 네트워킹에 대해 .NET Framework 4.7 이상 버전을 대상으로 하는 경우에는 이 항목의 나머지 부분은 관련이 없습니다.

<a name="wcf-tcp-cert"></a>

### <a name="for-wcf-tcp-transport-using-transport-security-with-certificate-credentials"></a>인증서 자격 증명과 함께 전송 보안을 사용하는 WCF TCP 전송의 경우

WCF는 .NET Framework의 나머지와 동일한 네트워킹 스택을 사용합니다.

4\.7.1을 대상으로 지정하면 다음 위치에 명시적으로 구성되지 않은 경우에 한해 WCF는 OS에서 기본적으로 가장 적합한 보안 프로토콜을 선택할 수 있도록 구성됩니다.

- 애플리케이션 구성 파일.
- **또는**소스 코드의 애플리케이션.

기본적으로 .NET Framework 4.7 이상 버전은 TLS 1.2를 사용하도록 구성되고 TLS 1.1 또는 TLS 1.0을 사용하는 연결을 허용합니다. <xref:System.Security.Authentication.SslProtocols.None?displayProperty=nameWithType>을 사용하도록 바인딩을 구성하여 OS가 가장 적합한 보안 프로토콜을 선택할 수 있도록 WCF를 구성하세요. 이 구성은 <xref:System.ServiceModel.TcpTransportSecurity.SslProtocols>에서 설정할 수 있습니다. `SslProtocols.None`은 <xref:System.ServiceModel.NetTcpSecurity.Transport>에서 액세스할 수 있습니다. `NetTcpSecurity.Transport`는 <xref:System.ServiceModel.NetTcpBinding.Security>에서 액세스할 수 있습니다.

사용자 지정 바인딩을 사용하는 경우:

- <xref:System.Security.Authentication.SslProtocols.None?displayProperty=nameWithType>을 사용하도록 <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement.SslProtocols>를 설정하여 OS가 가장 적합한 보안 프로토콜을 선택할 수 있도록 WCF를 구성합니다.
- **또는** 구성 경로 `system.serviceModel/bindings/customBinding/binding/sslStreamSecurity:sslProtocols`와 함께 사용되는 프로토콜을 구성합니다.

사용자 지정 바인딩을 사용하지 **않고**, **또한** 구성을 통해 WCF 바인딩을 설정하는 경우 구성 경로 `system.serviceModel/bindings/netTcpBinding/binding/security/transport:sslProtocols`와 함께 사용되는 프로토콜을 설정합니다.

### <a name="for-wcf-message-security-with-certificate-credentials"></a>인증서 자격 증명을 사용하는 WCF 메시지 보안의 경우

.NET Framework 4.7 이상 버전에서는 기본적으로 <xref:System.Net.ServicePointManager.SecurityProtocol> 속성에 지정된 프로토콜을 사용합니다. [AppContextSwitch](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) `Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols`가 `true`로 설정된 경우 WCF는 TLS 1.0까지 가장 적합한 프로토콜을 선택합니다.

## <a name="if-your-app-targets-a-net-framework-version-earlier-than-47"></a>앱이 4.7 이전의 .NET Framework 버전을 대상으로 하는 경우

다음 섹션을 통해 코드를 감사하여 특정 TLS 또는 SSL 버전을 설정하지 않는지 확인합니다.

### <a name="for-net-framework-46---462-and-not-wcf"></a>WCF가 아니고 .NET Framework 4.6~4.6.2인 경우

`DontEnableSystemDefaultTlsVersions` `AppContext` 스위치를 `false`로 설정합니다. [AppContext 스위치를 통해 보안 구성](#configuring-security-via-appcontext-switches)을 참조하세요.

### <a name="for-wcf-using-net-framework-46---462-using-tcp-transport-security-with-certificate-credentials"></a>인증서 자격 증명과 함께 TCP 전송 보안을 사용하고 .NET Framework 4.6~4.6.2를 사용하는 WCF의 경우

최신 OS 패치를 설치해야 합니다. [보안 업데이트](#security-updates)를 참조하세요.

WCF 프레임워크는 프로토콜 버전을 명시적으로 구성하지 않는 한 TLS 1.2까지 사용 가능한 가장 높은 프로토콜을 자동으로 선택합니다. 자세한 내용은 이전 섹션 [인증서 자격 증명과 함께 전송 보안을 사용하는 WCF TCP 전송의 경우](#wcf-tcp-cert)를 참조하세요.

### <a name="for-net-framework-35---452-and-not-wcf"></a>WCF가 아니고 .NET Framework 3.5~4.5.2인 경우

앱을 .NET Framework 4.7 이상 버전으로 업그레이드하는 것이 좋습니다. 업그레이드할 수 없는 경우에는 다음 단계를 수행합니다. 향후 특정 시점에 .NET Framework 4.7 이상 버전으로 업그레이드할 때까지 애플리케이션이 작동하지 않을 수 있습니다.

[SchUseStrongCrypto](#schusestrongcrypto) 및 [SystemDefaultTlsVersions](#systemdefaulttlsversions) 레지스트리 키를 1로 설정합니다. [Windows 레지스트리를 통해 보안 구성](#configuring-security-via-the-windows-registry)을 참조하세요. .NET Framework 버전 3.5는 명시적 TLS 값이 전달되는 경우에만 `SchUseStrongCrypto` 플래그를 지원합니다.

.NET Framework 3.5에서 실행 중인 경우 프로그램에서 TLS 1.2를 지정할 수 있도록 핫 패치를 설치해야 합니다.

| [KB3154518](https://support.microsoft.com/kb/3154518) | 안정성 롤업 HR-1605 - Windows 7 SP1 및 Server 2008 R2 SP1 기반 .NET Framework 3.5.1에 포함된 TLS 시스템 기본 버전에 대한 지원 |
| --- | --- |
| [KB3154519](https://support.microsoft.com/kb/3154519) | 안정성 롤업 HR-1605 - Windows Server 2012 기반 .NET Framework 3.5에 포함된 TLS 시스템 기본 버전에 대한 지원 |
| [KB3154520](https://support.microsoft.com/kb/3154520) | 안정성 롤업 HR-1605 - Windows 8.1 및 Windows Server 2012 R2 기반 .NET Framework 3.5에 포함된 TLS 시스템 기본 버전에 대한 지원 |
| [KB3156421](https://support.microsoft.com/kb/3156421) | Windows 기반 .NET Framework 4.5.2 및 4.5.1에 대한 1605 핫픽스 롤업 3154521 |

### <a name="for-wcf-using-net-framework-35---452-using-tcp-transport-security-with-certificate-credentials"></a>인증서 자격 증명과 함께 TCP 전송 보안을 사용하고 .NET Framework 3.5~4.5.2를 사용하는 WCF의 경우

이러한 WCF 프레임워크 버전은 SSL 3.0 및 TLS 1.0 값을 사용하도록 하드 코드됩니다. 이러한 값은 변경할 수 없습니다. TLS 1.1 및 1.2를 사용하려면 .NET Framework 4.6 이상 버전으로 업데이트하고 대상을 변경해야 합니다.

## <a name="if-your-app-targets-net-framework-35"></a>앱이 .NET Framework 3.5를 대상으로 하는 경우

.NET Framework 또는 OS에서 보안 프로토콜을 선택하도록 허용하는 대신 보안 프로토콜을 명시적으로 설정해야 하는 경우에는 코드에 `SecurityProtocolTypeExtensions` 및 `SslProtocolsExtension` 열거형을 추가합니다. `SecurityProtocolTypeExtensions` 및 `SslProtocolsExtension`에는 `Tls12`, `Tls11` 및 `SystemDefault` 값이 포함됩니다. [Windows 8.1 및 Windows Server 2012 R2 기반 .NET Framework 3.5에 포함된 TLS 시스템 기본 버전에 대한 지원](https://support.microsoft.com/help/3154520/support-for-tls-system-default-versions-included-in-the--net-framework)을 참조하세요.

<a name="configuring-security-via-appcontext-switches"></a>

## <a name="configuring-security-via-appcontext-switches-for-net-framework-46-or-later-versions"></a>AppContext 스위치를 통해 보안 구성(.NET Framework 4.6 이상 버전의 경우)

앱이 .NET Framework 4.6 이상 버전을 대상으로 하거나 이 버전에서 실행되는 경우 이 섹션에 설명된 [AppContext](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) 스위치는 관련이 있습니다. 기본적으로 또는 명시적으로 설정하는지 여부에 관계없이 스위치는 `false`여야 합니다(가능할 경우). 하나 또는 두 스위치를 통해 보안을 구성하려는 경우 코드에서 보안 프로토콜 값을 지정하지 마세요. 지정할 경우 스위치가 재정의됩니다.

HTTP 네트워킹(<xref:System.Net.ServicePointManager>) 또는 TCP 소켓 네트워킹(<xref:System.Net.Security.SslStream>)을 수행하는지에 관계없이 스위치의 효과는 동일합니다.

### <a name="switchsystemnetdontenableschusestrongcrypto"></a>Switch.System.Net.DontEnableSchUseStrongCrypto

`Switch.System.Net.DontEnableSchUseStrongCrypto`가 `false` 값이면 앱에서 강력한 암호화가 사용됩니다. `DontEnableSchUseStrongCrypto`가 `false` 값이면 더 안전한 네트워크 프로토콜(TLS 1.2, TLS 1.1 및 TLS 1.0)이 사용되고 보안되지 않은 프로토콜은 차단됩니다. 자세한 내용은 [SCH_USE_STRONG_CRYPTO 플래그](#the-sch_use_strong_crypto-flag)를 참조하세요. `true` 값은 앱에 대해 강력한 암호화를 사용하지 않도록 설정합니다.

앱이 .NET Framework 4.6 이상 버전을 대상으로 하는 경우 이 스위치는 기본적으로 `false`로 설정됩니다. 이 값이 권장되는 안전한 기본값입니다. 앱이 .NET Framework 4.6에서 실행되지만 이전 버전을 대상으로 하는 경우 스위치는 기본적으로 `true`로 설정됩니다. 이 경우 스위치를 명시적으로 `false`로 설정해야 합니다.

`DontEnableSchUseStrongCrypto`는 강력한 암호화를 지원하지 않고 업그레이드할 수 없는 레거시 서비스에 연결해야 하는 경우에만 `true` 값으로 설정되어야 합니다.

### <a name="switchsystemnetdontenablesystemdefaulttlsversions"></a>Switch.System.Net.DontEnableSystemDefaultTlsVersions

`Switch.System.Net.DontEnableSystemDefaultTlsVersions`가 `false` 값이면 앱에서 운영 체제가 프로토콜을 선택하도록 허용됩니다. `true` 값이면 앱이 .NET Framework에서 선택된 프로토콜을 사용합니다.

앱이 .NET Framework 4.7 이상 버전을 대상으로 하는 경우 이 스위치는 기본적으로 `false`로 설정됩니다. 이 값이 권장되는 안전한 기본값입니다. 앱이 .NET Framework 4.7 이상 버전에서 실행되지만 이전 버전을 대상으로 하는 경우 스위치는 기본적으로 `true`로 설정됩니다. 이 경우 스위치를 명시적으로 `false`로 설정해야 합니다.

### <a name="switchsystemservicemodeldisableusingservicepointmanagersecurityprotocols"></a>Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols

`Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols`가 `false` 값이면 애플리케이션에는 인증서 자격 증명을 사용하는 메시지 보안을 위해 `ServicePointManager.SecurityProtocols`에 정의된 값이 사용됩니다. `true` 값이면 TLS1.0까지 사용 가능한 최고 버전의 프로토콜이 사용됩니다.

.NET Framework 4.7 이상 버전을 대상으로 하는 애플리케이션의 경우 이 값은 기본적으로 `false`로 설정됩니다. .NET Framework 4.6.2 이하를 대상으로 하는 애플리케이션의 경우 이 값은 기본적으로 `true`로 설정됩니다.

### <a name="switchsystemservicemodeldontenablesystemdefaulttlsversions"></a>Switch.System.ServiceModel.DontEnableSystemDefaultTlsVersions

`Switch.System.ServiceModel.DontEnableSystemDefaultTlsVersions`가 `false` 값이면 운영 체제가 프로토콜을 선택할 수 있도록 기본 구성이 설정됩니다. `true` 값이면 TLS1.2까지 사용 가능한 최고 버전의 프로토콜로 기본값이 설정됩니다.

.NET Framework 4.7.1 이상 버전을 대상으로 하는 애플리케이션의 경우 이 값은 기본적으로 `false`로 설정됩니다. .NET Framework 4.7 이하를 대상으로 하는 애플리케이션의 경우 이 값은 기본적으로 `true`로 설정됩니다.

TLS 프로토콜에 대한 자세한 내용은 [완화: TLS 프로토콜](../migration-guide/mitigation-tls-protocols.md)을 참조하세요. `AppContext` 스위치에 대한 자세한 내용은 [ `<AppContextSwitchOverrides> Element` ](../configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md)를 참조하세요.

## <a name="configuring-security-via-the-windows-registry"></a>Windows 레지스트리를 통해 보안 구성

> [!WARNING]
> 레지스트리 키를 설정하면 시스템의 모든 애플리케이션에 영향을 줍니다. 머신에 대한 모든 권한이 있고 레지스트리의 변경 내용을 제거할 수 있는 경우에만 이 옵션을 사용합니다.

하나 또는 두 `AppContext` 스위치를 모두 설정할 수 없는 경우에는 이 섹션에 설명된 Windows 레지스트리 키와 함께 앱에서 사용하는 보안 프로토콜을 제어할 수 있습니다. 앱이 .NET Framework 4.5.2 이하 버전에서 실행되거나 구성 파일을 편집할 수 없는 경우에는 `AppContext` 스위치 중 하나 또는 모두를 사용할 수 없습니다. 레지스트리를 사용하여 보안을 구성하려면 코드에서 보안 프로토콜 값을 지정하지 마세요. 지정할 경우 레지스트리 설정이 재정의됩니다.

레지스트리 키의 이름은 해당 `AppContext` 스위치의 이름과 유사하지만 이름 앞에 `DontEnable`이 추가되지 않습니다. 예를 들어 `AppContext` 스위치 `DontEnableSchUseStrongCrypto`는 [SchUseStrongCrypto](#schusestrongcrypto)라는 레지스트리 키입니다.

이러한 키는 최신 보안 패치가 있는 모든 .NET Framework 버전에서 사용할 수 있습니다. [보안 업데이트](#security-updates)를 참조하세요.

HTTP 네트워킹(<xref:System.Net.ServicePointManager>) 또는 TCP 소켓 네트워킹(<xref:System.Net.Security.SslStream>)을 수행하는지에 관계없이 아래 설명된 모든 레지스트리 키의 효과는 동일합니다.

### <a name="schusestrongcrypto"></a>SchUseStrongCrypto

`HKEY_LOCAL_MACHINE\SOFTWARE\[Wow6432Node\]Microsoft\.NETFramework\<VERSION>: SchUseStrongCrypto` 레지스트리 키의 값은 DWORD 형식입니다. 값이 1이면 앱에서 강력한 암호화가 사용됩니다. 강력한 암호화의 경우 더 안전한 네트워크 프로토콜(TLS 1.2, TLS 1.1 및 TLS 1.0)이 사용되고 보안되지 않은 프로토콜은 차단됩니다. 0 값은 강력한 암호화를 사용하지 않도록 설정합니다. 자세한 내용은 [SCH_USE_STRONG_CRYPTO 플래그](#the-sch_use_strong_crypto-flag)를 참조하세요.

앱이 .NET Framework 4.6 이상 버전을 대상으로 하는 경우 이 키는 기본적으로 1 값으로 설정됩니다. 이 값이 권장되는 안전한 기본값입니다. 앱이 .NET Framework 4.6에서 실행되지만 이전 버전을 대상으로 하는 경우 키는 기본적으로 0으로 설정됩니다. 이 경우 키 값을 명시적으로 1로 설정해야 합니다.

이 키는 강력한 암호화를 지원하지 않고 업그레이드할 수 없는 레거시 서비스에 연결해야 하는 경우에만 0 값으로 설정되어야 합니다.

### <a name="systemdefaulttlsversions"></a>SystemDefaultTlsVersions

`HKEY_LOCAL_MACHINE\SOFTWARE\[Wow6432Node\]Microsoft\.NETFramework\<VERSION>: SystemDefaultTlsVersions` 레지스트리 키의 값은 DWORD 형식입니다. 값이 1이면 앱에서 운영 체제가 프로토콜을 선택하도록 허용됩니다. 값이 0이면 앱이 .NET Framework에서 선택된 프로토콜을 사용합니다.

`<VERSION>`은 v4.0.30319(.NET Framework 4 이상의 경우) 또는 v2.0.50727(.NET Framework 3.5의 경우)이어야 합니다.

앱이 .NET Framework 4.7 이상 버전을 대상으로 하는 경우 이 키는 기본적으로 1 값으로 설정됩니다. 이 값이 권장되는 안전한 기본값입니다. 앱이 .NET Framework 4.7 이상 버전에서 실행되지만 이전 버전을 대상으로 하는 경우 키는 기본적으로 0으로 설정됩니다. 이 경우 키 값을 명시적으로 1로 설정해야 합니다.

자세한 내용은 [Windows 10 버전 1511 및 Windows Server 2016 Technical Preview 4용 누적 업데이트: 2016년 5월 10일](https://support.microsoft.com/help/3156421/cumulative-update-for-windows-10-version-1511-and-windows-server-2016)을 참조하세요.

.NET Framework 3.5.1 사용에 대한 자세한 내용은 [Windows 7 SP1 및 Server 2008 R2 SP1 기반 .NET Framework 3.5.1에 포함된 TLS 시스템 기본 버전에 대한 지원](https://support.microsoft.com/help/3154518/support-for-tls-system-default-versions-included-in-the--net-framework)을 참조하세요.

다음 _.REG_ 파일은 레지스트리 키와 해당 변형을 가장 안전한 값으로 설정합니다.

```text
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v2.0.50727]
"SystemDefaultTlsVersions"=dword:00000001
"SchUseStrongCrypto"=dword:00000001

[HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319]
"SystemDefaultTlsVersions"=dword:00000001
"SchUseStrongCrypto"=dword:00000001

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v2.0.50727]
"SystemDefaultTlsVersions"=dword:00000001
"SchUseStrongCrypto"=dword:00000001

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]
"SystemDefaultTlsVersions"=dword:00000001
"SchUseStrongCrypto"=dword:00000001
```

## <a name="configuring-schannel-protocols-in-the-windows-registry"></a>Windows 레지스트리에서 Schannel 프로토콜 구성

클라이언트 및/또는 서버 앱이 협상하는 프로토콜에 대한 세분화된 제어에 레지스트리를 사용할 수 있습니다. 앱의 네트워킹이 Schannel( [보안 채널](/windows/desktop/SecAuthN/secure-channel)의 다른 이름)을 거칩니다. `Schannel`을 구성하여 앱 동작을 구성할 수 있습니다.

`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols` 레지스트리 키로 시작합니다. `SSL 2.0`, `SSL 3.0`, `TLS 1.0`, `TLS 1.1` 및 `TLS 1.2` 집합에서 해당 키 아래에 하위 키를 만들 수 있습니다. 각 하위 키 아래에 하위 키 `Client` 및/또는 `Server`를 만들 수 있습니다. `Client` 및 `Server` 아래에 DWORD 값 `DisabledByDefault`(0 또는 1) 및 `Enabled`(0 또는 0xFFFFFFFF)를 만들 수 있습니다.

## <a name="the-sch_use_strong_crypto-flag"></a>SCH_USE_STRONG_CRYPTO 플래그

사용으로 설정된 경우(기본적으로, `AppContext` 스위치 또는 Windows 레지스트리에서) .NET Framework는 앱이 TLS 보안 프로토콜을 요청할 때 `SCH_USE_STRONG_CRYPTO` 플래그를 사용합니다. `SCH_USE_STRONG_CRYPTO` 플래그는 기본적으로 `AppContext` 스위치 또는 레지스트리와 함께 사용할 수 있습니다. OS는 플래그를 `Schannel`에 전달하여 상호 운용성 향상을 위해 사용하도록 설정될 수 있는, 알려진 약한 암호화 알고리즘, 암호 도구 모음 및 TLS/SSL 프로토콜 버전을 사용하지 않도록 설정하도록 지시합니다. 자세한 내용은 다음을 참조하세요.

- [보안 채널](/windows/desktop/SecAuthN/secure-channel)
- [SCHANNEL_CRED 구조체](/windows/win32/api/schannel/ns-schannel-schannel_cred)

<xref:System.Net.SecurityProtocolType> 또는 <xref:System.Security.Authentication.SslProtocols>의 `Tls`(TLS 1.0), `Tls11` 또는 `Tls12` 열거 값을 명시적으로 사용할 경우 `SCH_USE_STRONG_CRYPTO` 플래그가 `Schannel`에도 전달됩니다.

## <a name="security-updates"></a>보안 업데이트

이 문서의 모범 사례는 설치 중인 최신 보안 업데이트에 따라 달라집니다. 이러한 업데이트에는 고급 .NET Framework 4.7 이상 기능을 사용하는 기능이 포함됩니다. 앱이 .NET Framework 4.7 이상 버전에서 실행되는 경우(이전 버전을 대상으로 하더라도) 최신 보안 업데이트가 중요합니다.

운영 체제에서 사용할 가장 적합한 TLS 버전을 선택할 수 있도록 .NET Framework를 업데이트하려면 최소한 다음을 설치해야 합니다.

- [품질 롤업의 .NET Framework 2017년 8월 Preview](https://devblogs.microsoft.com/dotnet/net-framework-august-2017-preview-of-quality-rollup/).
- **또는** [.NET Framework 2017년 9월 보안 및 품질 롤업](https://devblogs.microsoft.com/dotnet/net-framework-september-2017-security-and-quality-rollup/).

참고 항목:

- [.NET Framework 버전 및 종속성](../migration-guide/versions-and-dependencies.md)
- [방법: 설치된 .NET Framework 버전 확인](../migration-guide/how-to-determine-which-versions-are-installed.md)을 참조하세요.

## <a name="support-for-tls-12"></a>TLS 1.2에 대한 지원

앱이 TLS 1.2를 협상하려면 OS 및 .NET Framework 버전이 모두 TLS 1.2를 지원해야 합니다.

**TLS 1.2를 지원하기 위한 운영 체제 요구 사항**

TLS 1.2 및/또는 TLS 1.1을 지원하는 시스템에서 이를 사용하도록 설정하거나 다시 사용하도록 설정하려면 [TLS(전송 계층 보안) 레지스트리 설정](/windows-server/security/tls/tls-registry-settings)을 참조하세요.

| **OS** | **TLS 1.2 지원** |
| --- | --- |
| Windows 10<br>Windows Server 2016 | 지원되며 기본적으로 사용하도록 설정됩니다. |
| Windows 8.1<br>Windows Server 2012 R2 | 지원되며 기본적으로 사용하도록 설정됩니다. |
| Windows 8.0<br>Windows Server 2012 | 지원되며 기본적으로 사용하도록 설정됩니다. |
| Windows 7 SP1<br>Windows Server 2008 R2 SP1 | 지원되지만 기본적으로 사용하도록 설정되지 않습니다. TLS 1.2를 사용하도록 설정하는 방법에 대한 자세한 내용은 [TLS(전송 계층 보안) 레지스트리 설정](/windows-server/security/tls/tls-registry-settings) 웹 페이지를 참조하세요. |
| Windows Server 2008 | TLS 1.2 및 TLS 1.1 지원에는 업데이트가 필요합니다. [Windows Server 2008 SP2에서 TLS 1.1 및 TLS 1.2에 대한 지원을 추가하는 업데이트](https://support.microsoft.com/help/4019276/update-to-add-support-for-tls-1-1-and-tls-1-2-in-windows-server-2008-s)를 참조하세요. |
| Windows Vista | 지원되지 않습니다. |

Windows의 각 버전에서 기본적으로 사용하도록 설정되는 TLS/SSL 프로토콜에 대한 자세한 내용은 [Protocols in TLS/SSL (Schannel SSP)](/windows/desktop/SecAuthN/protocols-in-tls-ssl--schannel-ssp-)(TLS/SSL의 프로토콜(Schannel SSP))을 참조하세요.

**.NET Framework 3.5에서 TLS 1.2를 지원하는 요구 사항**

이 표에서는 .NET Framework 3.5에서 TLS 1.2를 지원하는 데 필요한 OS 업데이트를 보여줍니다. 모든 OS 업데이트를 적용하는 것이 좋습니다.

| **OS** | **.NET Framework 3.5에서 TLS 1.2를 지원하는 데 필요한 최소 업데이트** |
| --- | --- |
| Windows 10<br>Windows Server 2016 | [Windows 10 버전 1511 및 Windows Server 2016 Technical Preview 4용 누적 업데이트: 2016년 5월 10일](https://support.microsoft.com/help/3156421/cumulative-update-for-windows-10-version-1511-and-windows-server-2016) |
| Windows 8.1<br>Windows Server 2012 R2 | [Windows 8.1 및 Windows Server 2012 R2 기반 .NET Framework 3.5에 포함된 TLS 시스템 기본 버전에 대한 지원](https://support.microsoft.com/help/3154520/support-for-tls-system-default-versions-included-in-the--net-framework) |
| Windows 8.0<br>Windows Server 2012 | [Windows Server 2012 기반 .NET Framework 3.5에 포함된 TLS 시스템 기본 버전에 대한 지원](https://support.microsoft.com/help/3154519/support-for-tls-system-default-versions-included-in-the--net-framework) |
| Windows 7 SP1<br>Windows Server 2008 R2 SP1 | [Windows 7 SP1 및 Server 2008 R2 SP1 기반 .NET Framework 3.5.1에 포함된 TLS 시스템 기본 버전에 대한 지원](https://support.microsoft.com/help/3154518/support-for-tls-system-default-versions-included-in-the--net-framework) |
| Windows Server 2008 | [Windows Vista SP2 및 Server 2008 SP2 기반 .NET Framework 2.0 SP2에 포함된 TLS 시스템 기본 버전에 대한 지원](https://support.microsoft.com/help/3154517/support-for-tls-system-default-versions-included-in-the--net-framework) |
| Windows Vista | 지원 안 함 |

## <a name="azure-cloud-services"></a>Azure Cloud Services

[Azure Cloud Services](https://azure.microsoft.com/services/cloud-services/) 웹 및 작업자 역할을 사용하여 애플리케이션을 호스트하고 실행하는 경우에는 TLS 1.2를 지원하기 위해 몇 가지 고려할 사항이 있습니다.

### <a name="net-framework-47-is-not-installed-on-azure-guest-os-by-default"></a>.NET Framework 4.7은 기본적으로 Azure 게스트 OS에 설치되지 않습니다.

최신 Azure 게스트 OS 제품군 5 릴리스(Windows Server 2016)에 설치된 최신 버전은 4.6.2입니다. 각 Azure 게스트 OS에 설치된 .NET Framework 버전을 확인하려면 [Azure 게스트 OS 릴리스 및 SDK 호환성 매트릭스](https://docs.microsoft.com/azure/cloud-services/cloud-services-guestos-update-matrix)를 참조하세요.

앱이 Azure 게스트 OS 버전에서 사용할 수 없는 .NET Framework 버전을 대상으로 하는 경우 이를 직접 설치해야 합니다. [Azure 클라우드 서비스 역할에 .NET 설치](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-install-dotnet)를 참조하세요. 프레임워크 설치 시 다시 시작해야 하는 경우 서비스 역할은 준비 상태로 들어가기 전에 다시 시작될 수도 있습니다.

### <a name="azure-guest-os-registry-settings"></a>Azure 게스트 OS 레지스트리 설정

[Azure Cloud Services](https://azure.microsoft.com/services/cloud-services/)의 Azure 게스트 OS 제품군 5 이미지에는 이미 `SchUseStrongCrypto` 레지스트리 키가 1로 설정되어 있습니다. 자세한 내용은 [SchUseStrongCrypto](#schusestrongcrypto)를 참조하세요.

[SystemDefaultTlsVersions](#systemdefaulttlsversions) 레지스트리 키를 1로 설정합니다. [Windows 레지스트리를 통해 보안 구성](#configuring-security-via-the-windows-registry)을 참조하세요.
