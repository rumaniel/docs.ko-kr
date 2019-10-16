---
title: IIS 및 WAS에서 구성 기반 활성화
ms.date: 03/30/2017
ms.assetid: 6a927e1f-b905-4ee5-ad0f-78265da38238
ms.openlocfilehash: 5b06f474d26b80f955b1508f01da83448a8708a3
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2019
ms.locfileid: "70928778"
---
# <a name="configuration-based-activation-in-iis-and-was"></a>IIS 및 WAS에서 구성 기반 활성화

일반적으로 인터넷 정보 서비스 (IIS) 또는 WAS (Windows Process Activation Service)에서 WCF (Windows Communication Foundation) 서비스를 호스팅하는 경우 .svc 파일을 제공 해야 합니다. .svc 파일에는 서비스 이름과 선택적 사용자 지정 서비스 호스트 팩터리가 포함되어 있습니다. 이 추가 파일을 사용하면 관리 효율성이 떨어지지만 구성 기반 활성화 기능을 사용하면 .svc 파일이 필요 없기 때문에 이로 인한 관리 효율성 저하도 발생하지 않습니다.

## <a name="configuration-based-activation"></a>구성 기반 활성화

구성 기반 활성화는 이전에 .svc 파일에 있던 메타데이터를 가져와서 Web.config 파일에 저장합니다. <`serviceHostingEnvironment`> 요소 내에는 <`serviceActivations`> 요소가 있습니다. <`serviceActivations`> 요소 내에는 호스팅된 각 서비스에`add`대 한 하나 이상의 < > 요소가 있습니다. <`add`> 요소에는 서비스의 상대 주소와 서비스 유형 또는 서비스 호스트 팩터리를 설정 하는 데 사용할 수 있는 특성이 포함 되어 있습니다. 다음 구성 예제 코드에서는 이 섹션을 사용하는 방법을 보여 줍니다.

> [!NOTE]
> 각 <`add`> 요소는 서비스 또는 팩터리 특성을 지정 해야 합니다. 서비스 특성과 팩터리 특성을 모두 지정할 수 있습니다.

```xml
<serviceHostingEnvironment>
  <serviceActivations>
    <add relativeAddress="MyServiceAddress" service="Service" factory="MyServiceHostFactory"/>
  </serviceActivations>
</serviceHostingEnvironment>
```

 Web.config 파일에 이 섹션이 있으면 애플리케이션의 App_Code 디렉터리에 서비스 소스 코드를 저장하거나 애플리케이션의 Bin 디렉터리에 컴파일된 어셈블리를 저장할 수 있습니다.

> [!NOTE]
>
> - 구성 기반 활성화를 사용하는 경우 .svc 파일의 인라인 코드는 지원되지 않습니다.
> - 특성 `relativeAddress` 은 "\<하위 디렉터리 >/service.svc" 또는 "~/\<sub-directory/service .svc"와 같은 상대 주소로 설정 해야 합니다.
> - WCF와 연결된 알려진 확장명이 없는 상대 주소를 등록하면 구성 예외가 throw됩니다.
> - 지정된 상대 주소는 가상 애플리케이션의 루트를 기준으로 합니다.
> - 구성의 계층적 모델로 인해 가상 애플리케이션은 컴퓨터 또는 사이트 수준에서 등록된 상대 주소를 상속합니다.
> - 구성 파일의 등록이 .svc, .xamlx, .xoml 또는 기타 파일의 설정보다 우선합니다.
> - IIS/WAS에 보내진 URI의 ‘\’(백슬래시)는 자동으로 ‘/’(슬래시)로 변환됩니다. ‘\’가 포함된 상대 주소가 추가된 경우 IIS에 이 상대 주소를 사용하는 URI를 보내면 백슬래시가 슬래시로 변환되기 때문에 IIS가 이 URI를 상대 주소와 일치시킬 수 없습니다. 따라서 IIS가 일치하는 항목을 찾을 수 없음을 나타내는 추적 정보를 보냅니다.

## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Configuration.ServiceHostingEnvironmentSection.ServiceActivations%2A>
- [서비스 호스팅](../../../../docs/framework/wcf/hosting-services.md)
- [워크플로 서비스 호스팅 개요](../../../../docs/framework/wcf/feature-details/hosting-workflow-services-overview.md)
- [\<serviceHostingEnvironment>](../../../../docs/framework/configure-apps/file-schema/wcf/servicehostingenvironment.md)
- [Windows Server App Fabric 호스팅 기능](https://go.microsoft.com/fwlink/?LinkId=201276)
