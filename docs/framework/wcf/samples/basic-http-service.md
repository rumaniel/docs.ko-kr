---
title: 기본 HTTP 서비스
ms.date: 03/30/2017
ms.assetid: 27048b43-8a54-4f2a-9952-594bbfab10ad
ms.openlocfilehash: ec716b41efb3dde6e5afdb386d797e402d924b56
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70045155"
---
# <a name="basic-http-service"></a>기본 HTTP 서비스

이 샘플에서는 WCF (Windows Communication Foundation) REST 프로그래밍 모델을 사용 하 여 "POX" (일반 이전 XML) 서비스 라고 하는 HTTP 기반의 RPC 기반 서비스 많이를 구현 하는 방법을 보여 줍니다. 이 샘플은 자체 호스팅되는 WCF HTTP 서비스 (Service.cs)와 서비스를 만들고 호출 하는 콘솔 응용 프로그램 (Program.cs)의 두 구성 요소로 구성 되어 있습니다.

## <a name="sample-details"></a>샘플 세부 정보

WCF 서비스는 입력으로 전달 된 `EchoWithGet` 문자열 `EchoWithPost`을 반환 하는 2 개의 작업 및를 노출 합니다.

`EchoWithGet` 작업에는 <xref:System.ServiceModel.Web.WebGetAttribute>를 주석을 달아 해당 작업이 HTTP `GET` 요청을 처리함을 나타냅니다. <xref:System.ServiceModel.Web.WebGetAttribute>는 <xref:System.UriTemplate>을 명시적으로 지정하지 않으므로 이 작업을 위해서는 이름이 `s`인 쿼리 문자열 매개 변수를 사용하여 입력 문자열을 전달해야 합니다. 서비스에 필요한 URI 형식은 <xref:System.ServiceModel.Web.WebGetAttribute.UriTemplate%2A> 속성을 사용하여 사용자 지정할 수 있습니다.

<xref:System.ServiceModel.Web.WebInvokeAttribute>로 주석을 달린 `EchoWithPost` 작업은 `GET` 작업이 아니며 의도하지 않은 결과가 발생함을 나타냅니다. <xref:System.ServiceModel.Web.WebInvokeAttribute>는 `Method`를 명시적으로 지정하지 않으므로 이 작업은 XML 형식과 같이 요청 본문에 문자열이 있는 HTTP `POST` 요청을 처리합니다. 요청에 대한 HTTP 메서드 및 URI 형식은 각각 <xref:System.ServiceModel.Web.WebInvokeAttribute.Method%2A> 및 <xref:System.ServiceModel.Web.WebInvokeAttribute.UriTemplate> 속성을 사용하여 사용자 지정할 수 있습니다.

App.config 파일은 <xref:System.ServiceModel.Description.WebHttpEndpoint> 속성이 <xref:System.ServiceModel.Description.WebHttpEndpoint.HelpEnabled%2A>로 설정된 기본 `true`로 WCF 서비스를 구성합니다. 결과적으로 WCF 인프라는에서 `http://localhost:8000/Customers/help` 서비스에 대 한 http 요청을 생성 하는 방법 및 서비스의 http 응답을 사용 하는 방법에 대 한 정보를 제공 하는 자동 HTML 기반 도움말 페이지를 만듭니다.

Program.cs는 WCF 채널 팩터리를 사용 하 여 서비스를 호출 하 고 응답을 처리할 수 있는 방법을 보여 줍니다. 이 방법은 WCF 서비스에 액세스하는 여러 방법 중 하나일 뿐입니다. <xref:System.Net.HttpWebRequest> 및 <xref:System.Net.WebClient> 같은 다른 .NET Framework 클래스를 사용하여 서비스에 액세스할 수도 있습니다.

이 샘플은 콘솔 애플리케이션 내에서 실행되는 자체 호스팅 서비스와 클라이언트로 구성되어 있습니다. 콘솔 애플리케이션이 실행되면 클라이언트에서는 서비스로 요청을 보내고 응답의 관련 정보를 콘솔 창에 씁니다.

#### <a name="to-use-this-sample"></a>이 샘플을 사용하려면

1. Basic Http Service 샘플의 솔루션을 엽니다. Visual Studio 2012을 시작할 때 샘플이 성공적으로 실행 되도록 관리자 권한으로를 실행 해야 합니다. 이렇게 하려면 Visual Studio 2012 아이콘을 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 **관리자 권한으로 실행** 을 선택 합니다.

2. Ctrl+Shift+B를 눌러 솔루션을 빌드한 다음 Ctrl+F5를 눌러 디버깅하지 않고 콘솔 애플리케이션을 실행합니다. 콘솔 창이 나타나고 실행 중인 서비스의 URI와 실행 중인 서비스에 대한 HTML 도움말 페이지의 URI가 제공됩니다. 언제든지 브라우저에서 HTML 도움말 페이지의 URI를 입력하면 해당 도움말 페이지를 볼 수 있습니다. 샘플이 실행되면 클라이언트에서는 현재 활동의 상태를 씁니다.

3. 아무 키나 눌러 샘플을 종료합니다.

> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Web\BasicHttpService`
