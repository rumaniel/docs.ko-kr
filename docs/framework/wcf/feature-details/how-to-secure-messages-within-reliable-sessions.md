---
title: '방법: 신뢰할 수 있는 세션 내에서 메시지 보안'
ms.date: 03/30/2017
ms.assetid: aee33e50-936f-4486-9ca8-c1520c19a62d
ms.openlocfilehash: ee35f2a36ca08814423b5a3d0b1432bacd28c2e5
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61973006"
---
# <a name="how-to-secure-messages-within-reliable-sessions"></a>방법: 신뢰할 수 있는 세션 내에서 메시지 보안

이 항목에서는 기본적이지는 않지만 신뢰할 수 있는 세션을 지원하는 시스템 제공 바인딩 중 하나를 사용하여 이러한 세션 내에서 교환된 메시지의 메시지 수준 보안을 사용하도록 설정하는 데 필요한 단계에 대해 간략하게 설명합니다. 구성 파일에서 코드를 사용 하 여 명령적으로 또는 선언적으로 안전 하 고 신뢰할 수 있는 세션을 사용 하도록 설정 합니다. 이 절차에서는 클라이언트와 서비스 구성 파일을 사용하여 안전하고 신뢰할 수 있는 세션을 사용할 수 있습니다.

이 절차는 다음 세 가지 주요 작업으로 구성됩니다.

1. 클라이언트 및 서비스가 신뢰할 수 있는 세션 내에서 메시지를 교환하도록 지정합니다.

1. 신뢰할 수 있는 세션 내에서 메시지 수준 보안이 필요합니다.

1. 클라이언트가 서비스에서 인증받는 데 사용해야 하는 클라이언트 자격 증명 형식을 지정합니다.

끝점 구성 요소를 포함 하는 첫 번째 작업에서 중요 한 것을 `bindingConfiguration` (이 예제의) 이라는 바인딩 구성을 참조 하는 특성 `MessageSecurity`합니다. [  **\<바인딩 >** ](../../../../docs/framework/misc/binding.md) 구성 요소에는 다음을 설정 하 여 신뢰할 수 있는 세션을 사용 하도록 설정 하려면이 이름을 참조 합니다 `enabled` 특성을 [  **\<reliableSession >** ](https://docs.microsoft.com/previous-versions/ms731375(v=vs.90)) 요소를 `true`입니다. `ordered` 특성을 `true`로 설정하여 신뢰할 수 있는 세션 내에서 순서가 지정된 배달 보증을 사용하는 것이 필요할 수 있습니다.

이 구성 절차의 기반이 되는 예제의 소스 복사에 대 한 참조를 [WS 신뢰할 수 있는 세션](../../../../docs/framework/wcf/samples/ws-reliable-session.md)합니다.

두 번째 작업의 주요 항목은 설정 하 여 수행 합니다 `mode` 특성을  **\<보안 >** 요소에 포함 된를  **\<바인딩 >** 클라이언트와 서비스를 요소의 `Message`합니다.

세 번째 작업의 주요 항목은 설정 하 여 수행 합니다 `clientCredentialType` 특성을  **\<메시지 >** 요소에 포함 된를  **\<보안 >** 클라이언트와 서비스를 요소의 `Certificate`합니다.

> [!NOTE]
> 신뢰할 수 있는 세션을 사용 하 여 메시지 보안을 사용할 때 첫 번째 실패 시 예외를 throw 하는 대신 시간 초과가 발생할 때까지 인증 되지 않은 클라이언트를 인증 하려고 하는 신뢰할 수 있는 메시징 합니다.

### <a name="configure-the-service-with-a-wshttpbinding-to-use-a-reliable-session"></a>신뢰할 수 있는 세션을 사용 하도록 WSHttpBinding으로 서비스 구성

이 절차에 설명 되어 [방법: 신뢰할 수 있는 세션 내에서 메시지 교환](../../../../docs/framework/wcf/feature-details/how-to-exchange-messages-within-a-reliable-session.md)합니다.

### <a name="configure-the-client-with-a-wshttpbinding-to-use-a-reliable-session"></a>신뢰할 수 있는 세션을 사용 하도록 WSHttpBinding으로 클라이언트를 구성

이 절차에 설명 되어 [방법: 신뢰할 수 있는 세션 내에서 메시지 교환](../../../../docs/framework/wcf/feature-details/how-to-exchange-messages-within-a-reliable-session.md)합니다.

### <a name="set-the-mode-and-clientcredentialtype-in-configuration"></a>구성에서 모드 및 ClientCredentialType을 설정

1. 적절 한 바인딩 요소를 추가 합니다 [  **\<바인딩 >** ](../../../../docs/framework/configure-apps/file-schema/wcf/bindings.md) 구성 파일의 요소입니다. 다음 예제에서는 추가 된 [  **\<wsHttpBinding >** ](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md) 요소입니다.

1. 추가 된  **\<바인딩 >** 요소 집합과 해당 `name` 특성을 적절 한 값으로. 이 예제에서는 이름을 사용 하 여 `MessageSecurity`입니다.

1. 추가 된  **\<보안 >** 요소를 `mode` 특성을 `Message`.

1. 내에서  **\<보안 >** 요소를 추가  **\<메시지 >** 요소를 `clientCredentialType` 특성을 `Certificate`.

```xml
<wsHttpBinding>
  <binding name="MessageSecurity">
    <security mode="Message">
      <message clientCredentialType="Certificate" />
    </security>
  </binding>
</wsHttpBinding>
```
