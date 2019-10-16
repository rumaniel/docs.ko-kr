---
title: 범위 샘플을 사용한 검색
ms.date: 03/30/2017
ms.assetid: 6a37a754-6b8c-4ebe-bdf2-d4f0520271d5
ms.openlocfilehash: 9b65a348c943b07e813e3fe690f1364b77a94890
ms.sourcegitcommit: a97ecb94437362b21fffc5eb3c38b6c0b4368999
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2019
ms.locfileid: "68972012"
---
# <a name="discovery-with-scopes-sample"></a>범위 샘플을 사용한 검색

이 샘플에서는 범위를 사용하여 검색 가능한 엔드포인트를 분류하는 방법과 <xref:System.ServiceModel.Discovery.DiscoveryClient>를 사용하여 엔드포인트에 대한 비동기 검색을 수행하는 방법을 보여 줍니다. 이 샘플의 서비스에서는 엔드포인트 검색 동작을 추가하고 이를 사용하여 엔드포인트에 범위를 추가하고 엔드포인트의 검색 기능을 제어하여 각 엔드포인트에 대한 검색을 사용자 지정하는 방법을 보여 줍니다. 이 샘플의 클라이언트에서는 <xref:System.ServiceModel.Discovery.DiscoveryClient>를 만들고 <xref:System.ServiceModel.Discovery.FindCriteria>에 범위를 추가하는 방식으로 검색 매개 변수를 세부적으로 조정하여 범위를 포함하는 방법을 보여 줍니다. 이 샘플에서는 클라이언트가 종료 조건을 추가하여 응답을 제한하는 방법도 보여 줍니다.

## <a name="service-features"></a>Service Features

이 프로젝트에서는 <xref:System.ServiceModel.ServiceHost>에 추가되는 두 개의 서비스 엔드포인트를 보여 줍니다. 각 엔드포인트에는 <xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior>가 연결되어 있습니다. 이 동작은 두 엔드포인트 모두에 대한 URI 범위를 추가하는 데 사용됩니다. 범위는 클라이언트가 검색을 세부적으로 조정할 수 있도록 이러한 각 엔드포인트를 구별하는 데 사용됩니다. 두 번째 엔드포인트의 경우 <xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior.Enabled%2A> 속성을 `false`로 설정하여 검색 기능을 사용하지 않도록 설정할 수 있습니다. 이렇게 하면 이 엔드포인트와 연결된 검색 메타데이터가 검색 메시지의 일부로 보내지지 않습니다.

## <a name="client-features"></a>Client Features

`FindCalculatorServiceAddress()` 메서드는 <xref:System.ServiceModel.Discovery.DiscoveryClient>를 사용하고 두 가지 제한으로 <xref:System.ServiceModel.Discovery.FindCriteria>를 전달하는 방법을 보여 줍니다. 범위가 조건에 추가되고 <xref:System.ServiceModel.Discovery.FindCriteria.MaxResults%2A> 속성은 1로 설정됩니다. 범위는 동일한 범위를 게시하는 서비스만으로 결과를 제한합니다. <xref:System.ServiceModel.Discovery.FindCriteria.MaxResults%2A>를 1로 설정하면 <xref:System.ServiceModel.Discovery.DiscoveryClient>에서 기다리는 응답이 최대 1개의 엔드포인트로 제한됩니다. <xref:System.ServiceModel.Discovery.DiscoveryClient.Find%2A> 호출은 제한 시간에 도달하거나 하나의 엔드포인트가 발견될 때까지 스레드를 차단하는 동기 작업입니다.

### <a name="to-use-this-sample"></a>이 샘플을 사용하려면

1. 이 샘플에서는 HTTP 엔드포인트를 사용하며 이 샘플을 실행하려면 적절한 URL ACL을 추가해야 합니다. 자세한 내용은 [HTTP 및 HTTPS 구성](https://go.microsoft.com/fwlink/?LinkId=70353) 을 참조 하세요. 높은 권한으로 다음 명령을 실행하면 적절한 ACL이 추가됩니다. 명령이 지정한 대로 작동하지 않는 경우 `netsh http add urlacl url=http://+:8000/ user=%DOMAIN%\%UserName%` 인수 대신 도메인과 사용자 이름을 사용할 수 있습니다.

2. 솔루션을 빌드합니다.

3. 빌드 디렉터리에서 서비스 실행 파일을 실행합니다.

4. 클라이언트 실행 파일을 실행합니다. 클라이언트에서 서비스를 찾을 수 있는지 확인합니다.

> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Discovery\DiscoveryWithScopes`
