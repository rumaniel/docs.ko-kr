---
title: 사용자 지정 찾기 조건
ms.date: 03/30/2017
ms.assetid: b2723929-8829-424d-8015-a37ba2ab4f68
ms.openlocfilehash: 236cce194d89409ab19732c239459418cddd251b
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70039936"
---
# <a name="custom-find-criteria"></a>사용자 지정 찾기 조건
이 샘플에서는 논리를 사용하여 사용자 지정 범위 일치를 만드는 방법과 사용자 지정 검색 서비스를 구현하는 방법을 보여 줍니다. 클라이언트에서는 사용자 지정 범위 일치 기능을 사용하여 WCF 검색의 시스템 제공 찾기 기능을 구체화하고 보다 세부적으로 빌드합니다. 이 샘플에서 다루는 시나리오는 다음과 같습니다.  
  
1. 클라이언트에서 계산기 서비스를 찾습니다.  
  
2. 검색을 구체화하기 위해 클라이언트는 사용자 지정 범위 일치 규칙을 사용해야 합니다.  
  
3. 이 규칙에 따라 엔드포인트가 클라이언트에서 지정한 범위와 일치하면 서비스에서는 클라이언트에 다시 응답합니다.  
  
## <a name="demonstrates"></a>세부 항목  
  
- 사용자 지정 검색 서비스 만들기  
  
- 알고리즘에 따른 사용자 지정 범위 일치 구현  
  
## <a name="discussion"></a>토론  
 클라이언트에서 "OR" 형식 일치 조건을 찾고 있습니다. 엔드포인트의 범위가 클라이언트에서 제공한 범위와 일치하면 서비스가 다시 응답합니다. 이 경우 클라이언트는 다음 목록의 범위가 있는 계산기 서비스를 찾습니다.  
  
1. `net.tcp://Microsoft.Samples.Discovery/RedmondLocation`  
  
2. `net.tcp://Microsoft.Samples.Discovery/SeattleLocation`  
  
3. `net.tcp://Microsoft.Samples.Discovery/PortlandLocation`  
  
 이 작업을 수행하기 위해 클라이언트에서는 URI에 따른 사용자 지정 범위 일치를 전달하여 서비스에서 사용자 지정 범위 일치 규칙을 사용하도록 지정합니다. 사용자 지정 범위 일치에 도움이 되도록 서비스에서는 사용자 지정 범위 규칙을 인식하고 관련 일치 논리를 구현하는 사용자 지정 검색 서비스를 사용해야 합니다.  
  
 클라이언트 프로젝트에서 Program.cs 파일을 엽니다. `ScopeMatchBy` 개체의 `FindCriteria` 필드는 특정 URI로 설정되어 있습니다. 이 식별자는 서비스로 보내집니다. 서비스에서는 이 규칙을 인식하지 못하는 경우 클라이언트의 찾기 요청을 무시합니다.  
  
 서비스 프로젝트를 엽니다. 다음 세 개의 파일은 사용자 지정 검색 서비스를 구현하는 데 사용됩니다.  
  
1. **AsyncResult.cs**: 검색 방법에 필요한의 `AsyncResult` 구현입니다.  
  
2. **CustomDiscoveryService.cs**: 이 파일은 사용자 지정 검색 서비스를 구현 합니다. 이 구현에서는 <xref:System.ServiceModel.Discovery.DiscoveryService> 클래스를 확장하고 필요한 메서드를 재정의합니다. <xref:System.ServiceModel.Discovery.DiscoveryService.OnBeginFind%2A> 메서드의 구현에 주의하십시오. 이 메서드는 클라이언트에서 규칙에 따른 사용자 지정 범위 일치를 지정했는지 여부를 확인합니다. 이는 클라이언트에서 이전에 지정한 사용자 지정 URI와 동일합니다. 사용자 지정 규칙을 지정 하는 경우 "OR" 일치 논리를 구현 하는 코드 경로를 따릅니다.  
  
     이 사용자 지정 논리는 서비스에 있는 각 엔드포인트의 모든 범위에 적용됩니다. 엔드포인트의 범위가 클라이언트에서 제공한 범위와 일치하면 검색 서비스에서는 클라이언트로 다시 보내는 응답에 해당 엔드포인트를 추가합니다.  
  
3. **CustomDiscoveryExtension.cs**: 검색 서비스를 구현 하는 마지막 단계는이 사용자 지정 검색 서비스의 구현을 서비스 호스트에 연결 하는 것입니다. 여기에 사용되는 도우미 클래스는 `CustomDiscoveryExtension` 클래스입니다. 이 클래스는 <xref:System.ServiceModel.Discovery.DiscoveryServiceExtension> 클래스를 확장합니다. 사용자는 <xref:System.ServiceModel.Discovery.DiscoveryServiceExtension.GetDiscoveryService%2A> 메서드를 재정의해야 합니다. 이 경우 메서드는 이전에 생성된 사용자 지정 검색 서비스의 인스턴스를 반환합니다. `PublishedEndpoints`는 <xref:System.Collections.ObjectModel.ReadOnlyCollection%601>에 추가된 모든 애플리케이션 엔드포인트를 포함하는 <xref:System.ServiceModel.ServiceHost>입니다. 사용자 지정 검색 서비스에서는 이를 사용하여 해당 내부 목록을 채웁니다. 사용자가 다른 엔드포인트 메타데이터를 추가할 수도 있습니다.  
  
 마지막으로 Program.cs를 엽니다. <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior>와 `CustomDiscoveryExtension`이 모두 호스트에 추가되어 있습니다. 이 작업이 수행되고 호스트에 검색 메시지를 받는 데 사용할 엔드포인트가 있으면 애플리케이션에서 사용자 지정 검색 서비스를 사용할 수 있습니다.  
  
 클라이언트에서 주소를 모르고도 서비스를 찾을 수 있는지 확인합니다.  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. 프로젝트가 포함된 솔루션을 엽니다.  
  
2. 프로젝트를 빌드합니다.  
  
3. 서비스 애플리케이션을 실행합니다.  
  
4. 클라이언트 애플리케이션을 실행합니다.  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Discovery\CustomFindCriteria`
