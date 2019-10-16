---
title: 지원 되는 배포 시나리오-WCF
ms.date: 03/30/2017
ms.assetid: 3399f208-3504-4c70-a22e-a7c02a8b94a6
ms.openlocfilehash: 2da55176cbfe618b332f2df210e3e1c0516b17ae
ms.sourcegitcommit: a8d3504f0eae1a40bda2b06bd441ba01f1631ef0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2019
ms.locfileid: "67170046"
---
# <a name="supported-deployment-scenarios"></a>지원 되는 배포 시나리오

부분적으로 신뢰할 수 있는 응용 프로그램에서 사용 하기 위해 지원 되는 Windows Communication Foundation (WCF) 기능의 하위 집합은 WCF를 사용 하 여 전부는 아니지만 일부 시나리오의 요구 사항을 충족 하도록 설계 되었습니다. 서버에서 WCF 보안을 위해 ASP.NET 2.0 보통 신뢰 권한에서 타사 응용 프로그램을 실행 하는 공유 호스팅 공급자를 설정 하는 인터넷 규모의 요구 사항을 충족 합니다. 와 같은 배포 기술의 요구 사항을 충족 하기 위해 클라이언트에서 WCF 부분 신뢰 지원이 디자인 되었습니다 [ClickOnce 배포](/visualstudio/deployment/clickonce-security-and-deployment) 또는 원활 하 고 안전한 배포를 허용 하는 WPF의 XAML 브라우저 응용 프로그램 기술 신뢰할 수 없는 사이트에서 데스크톱 응용 프로그램입니다.

## <a name="minimum-permission-requirements"></a>최소 권한 요구 사항

WCF는 다음 표준 명명 된 권한 집합 중 하나에서 실행 중인 응용 프로그램에서 기능의 하위 집합을 지원 합니다.

- 보통 신뢰 권한

- 인터넷 영역 권한

더 제한적인 권한 가진 부분적으로 신뢰할 수 있는 응용 프로그램에서 WCF를 사용 하는 동안 런타임에 보안 예외가 발생할 수 있습니다.

이러한 권한 집합에서 지원되는 기능에 대한 자세한 내용은 [Partial Trust Feature Compatibility](partial-trust-feature-compatibility.md)을 참조하십시오.

## <a name="partial-trust-on-the-server"></a>서버에서 부분 신뢰

ASP.NET 웹 응용 프로그램 호스팅 서비스의 상용 공급자는 대부분 ASP.NET 2.0 보통 신뢰 권한 집합에 해당 서버에서 실행 하는 응용 프로그램이 실행을 위임 합니다. WCF 서비스 사용 하는 경우 이러한 환경에서 실행할 수는 <xref:System.ServiceModel.BasicHttpBinding>는 <xref:System.ServiceModel.WebHttpBinding>, 또는 <xref:System.ServiceModel.WSHttpBinding> 전송 수준 보안을 사용 하 여 합니다.

보통 신뢰 호스팅 환경에서 실행 되는 WCF 서비스를 다른 서버에 클라이언트 요청에 응답 메시지를 전송 하 여 중간 계층 서비스로 사용할 수도 있습니다. 서버에서 중간 계층 시나리오는 호스팅 환경이 애플리케이션에 적합한 <xref:System.Net.WebPermission> 을 부여해서 원하는 서버로 아웃바운드 요청을 한 경우 지원됩니다.

WCF는 SOAP 메시징 지원 되는 SOAP 바인딩 중 하나를 사용 하는 것 외에도 다음을 지원 합니다.는 <xref:System.ServiceModel.WebHttpBinding> 부분적으로 신뢰할 수 있는 응용 프로그램에서 웹 스타일 서비스를 구축 하는 것에 대 한 합니다. 합니다 [WCF 웹 HTTP 프로그래밍 모델](wcf-web-http-programming-model.md)를 [WCF 배포](wcf-syndication.md), 및 [AJAX 통합 및 JSON 지원](ajax-integration-and-json-support.md) WCF 기능의 모든 부분 신뢰에서 지원 됩니다.

워크플로 서비스는 완전 신뢰 권한이 필요하며, 부분 신뢰 애플리케이션에서 사용할 수 없습니다.

자세한 내용은 [방법: Use Medium Trust in ASP.NET 2.0](https://go.microsoft.com/fwlink/?LinkId=84603)합니다.

## <a name="partial-trust-on-the-client"></a>클라이언트에서 부분 신뢰

신뢰할 수 없는 인터넷 사이트에서 코드를 다운로드하고 실행할 때 특정 보안 조치를 취해야 합니다. 둘 다 [ClickOnce 배포](/visualstudio/deployment/clickonce-security-and-deployment) WPF의 XAML 브라우저 응용 프로그램 (XBAP)이 기술을 확인를 사용 하 여 부분 신뢰의 제한 된 권한 (인터넷 영역)을 신뢰할 수 없는 코드에 부여 합니다.

WCF에서 배포한 부분 신뢰 응용 프로그램 내에서 원격 서버와 통신할 수 [ClickOnce 배포](/visualstudio/deployment/clickonce-security-and-deployment) 또는 XBAP 합니다. 인터넷 영역 권한 집합에 포함 됩니다 <xref:System.Net.WebPermission> 원래 호스트에 대 한 이러한 응용 프로그램에 설명 된 지원 되는 WCF 바인딩 중 하나를 사용 하 여 원본 서버와 통신할 수 있는 [Partial Trust Feature Compatibility ](partial-trust-feature-compatibility.md).

## <a name="see-also"></a>참고자료

- [코드 액세스 보안](../../misc/code-access-security.md)
- [Windows Presentation Foundation 브라우저에서 호스팅된 응용 프로그램 개요](../../wpf/app-development/wpf-xaml-browser-applications-overview.md)
- [부분 신뢰](partial-trust.md)
- [ASP.NET 신뢰 수준과 정책 파일](https://docs.microsoft.com/previous-versions/wyts434y(v=vs.140))
