---
title: 보호 수준 이해
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF, security
- ProtectionLevel property
ms.assetid: 0c034608-a1ac-4007-8287-b1382eaa8bf2
ms.openlocfilehash: 4ebb93d3ed325c115dcf311c821b014532dffc11
ms.sourcegitcommit: d6e27023aeaffc4b5a3cb4b88685018d6284ada4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67663946"
---
# <a name="understanding-protection-level"></a>보호 수준 이해

`ProtectionLevel` 및 <xref:System.ServiceModel.ServiceContractAttribute> 클래스와 같은 여러 클래스에서 볼 수 있는 <xref:System.ServiceModel.OperationContractAttribute> 속성은 메시지의 전체나 일부를 보호하는 방법을 제어합니다. 이 항목에서는 Windows Communication Foundation (WCF) 기능 및 작동 원리를 설명 합니다.

보호 수준 설정에 대 한 지침을 참조 하세요. [방법: ProtectionLevel 속성 설정](../../../docs/framework/wcf/how-to-set-the-protectionlevel-property.md)합니다.

> [!NOTE]
> 구성이 아닌 코드에서만 보호 수준을 설정할 수 있습니다.

## <a name="basics"></a>기본 사항

다음과 같은 기본 문을 적용하여 보호 수준 기능을 이해할 수 있습니다.

- 메시지에 대해 세 가지 기본 보호 수준이 있습니다. 수준 속성은 <xref:System.Net.Security.ProtectionLevel> 열거형 값 중 하나로 설정됩니다. 다음은 낮은 보호 수준에서 높은 보호 수준의 순서로 나열된 열거형 값입니다.

  - `None`.

  - `Sign`. 보호되는 부분이 디지털 방식으로 서명됩니다. 이를 통해 보호된 메시지 부분에 대한 변조를 탐지할 수 있습니다.

  - `EncryptAndSign`. 메시지 부분이 서명되기 전에 암호화되어 기밀성을 보장합니다.

- 보호 요구 사항에 대해서만 설정할 수 있습니다 *응용 프로그램 데이터* 이 기능을 사용 하 여 합니다. 예를 들어 WS-Addressing 헤더는 인프라 데이터이므로 `ProtectionLevel`의 영향을 받지 않습니다.

- 보안 모드가 `Transport`로 설정되면 전체 메시지가 전송 메커니즘의 보호를 받습니다. 따라서 메시지의 각 부분에 별도의 보호 수준을 설정하는 것은 효과가 없습니다.

- `ProtectionLevel` 는 개발자가 설정할 수는 *최소 수준* 바인딩을 준수 해야 하는 합니다. 서비스가 배포되면 구성에 지정된 실제 바인딩은 최소 수준을 지원하거나 지원하지 않을 수 있습니다. 예를 들어 <xref:System.ServiceModel.BasicHttpBinding> 클래스는 보안을 활성화할 수 있더라도 기본적으로 보안을 제공하지 않습니다. 따라서 `None` 이외의 값으로 설정된 계약에 이 클래스를 사용하면 예외가 throw됩니다.

- 서비스는 필요한 경우 최소한 `ProtectionLevel` 모든 메시지는 `Sign`, 클라이언트 (WCF 이외의 기술로 만든 경우 등)를 암호화 하 고 수 모든 메시지에 서명 (되는 데 필요한 최소 수준 이상의). 이 경우 WCF 클라이언트는 최소값 보다 좀 더 수행 되기 때문에 예외를 throw 하지 됩니다. 그러나 WCF 응용 프로그램 (서비스 또는 클라이언트) 하지 과도 하 게 보호 하는 메시지 파트를 가능한 경우는 최소 수준 준수할 note 합니다. 또한 `Transport`를 보안 모드로 사용하면, 전송에서 메시지 스트림을 과보호할 수 있는데, 이는 보다 세부적인 수준으로 보호하는 것이 기본적으로 불가능하기 때문입니다.

- `ProtectionLevel`을 명시적으로 `Sign` 또는 `EncryptAndSign`으로 설정하면 보안이 활성화된 상태에서 바인딩을 사용해야 합니다. 그렇지 않으면 예외가 throw됩니다.

- 보안이 활성화된 바인딩을 선택하고 계약의 어떤 위치에서도 `ProtectionLevel` 속성을 설정하지 않으면, 모든 애플리케이션 데이터가 암호화되거나 서명됩니다.

- 보안이 활성화되지 않은 바인딩(예: `BasicHttpBinding` 클래스에서는 기본적으로 보안이 비활성화됨)을 선택하고 `ProtectionLevel`이 명시적으로 설정되지 않은 경우 애플리케이션 데이터가 보호되지 않습니다.

- 전송 수준에서 보안을 적용하는 바인딩을 사용하면 모든 애플리케이션 데이터가 전송 기능에 따라 보안되며,

- 메시지 수준에서 보안을 적용하는 바인딩을 사용하면 애플리케이션 데이터는 계약에 설정된 보호 수준에 따라 보안됩니다. 보호 수준을 지정하지 않는다면 메시지의 모든 애플리케이션 데이터는 암호화되고 서명됩니다.

- `ProtectionLevel`은 다양한 범위 지정 수준에서 설정할 수 있습니다. 범위 지정과 관련된 계층 구조에 대해서는 다음 단원에서 설명합니다.

## <a name="scoping"></a>범위 지정

맨 위 API에 `ProtectionLevel`을 설정하면 그 아래의 모든 단계에 해당 수준이 설정됩니다. 그러나 보다 하위 단계에서 `ProtectionLevel`을 다른 값으로 설정하면, 계층 구조에서 해당 단계 아래에 있는 모든 API가 새 수준으로 다시 설정됩니다. 하지만 그 단계 위에 있는 API에는 맨 위 단계의 영향을 계속해서 받게 됩니다. 계층 구조는 다음과 같습니다. 동일한 단계에 있는 특성은 피어라고 합니다.

- <xref:System.ServiceModel.ServiceContractAttribute>

- <xref:System.ServiceModel.OperationContractAttribute>

- <xref:System.ServiceModel.FaultContractAttribute>

- <xref:System.ServiceModel.MessageContractAttribute>

- <xref:System.ServiceModel.MessageHeaderAttribute>

- <xref:System.ServiceModel.MessageBodyMemberAttribute>

## <a name="programming-protectionlevel"></a>ProtectionLevel 프로그래밍

계층 구조 내 임의의 지점에서 `ProtectionLevel`을 프로그래밍하려면 특성을 적용할 때 속성에 적절한 값을 설정하면 됩니다. 예제는 [방법: ProtectionLevel 속성 설정](../../../docs/framework/wcf/how-to-set-the-protectionlevel-property.md)합니다.

> [!NOTE]
> 기본적인 속성과 메시지 계약을 설정하려면 이러한 기능의 작동 방법에 대해 이해해야 합니다. 자세한 내용은 [방법: ProtectionLevel 속성 설정](../../../docs/framework/wcf/how-to-set-the-protectionlevel-property.md) 하 고 [메시지 계약을 사용 하 여](../../../docs/framework/wcf/feature-details/using-message-contracts.md)입니다.

## <a name="ws-addressing-dependency"></a>WS-Addressing 종속성

사용 하 여 대부분의 경우에는 [ServiceModel Metadata 유틸리티 도구 (Svcutil.exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 클라이언트를 생성 하는 클라이언트와 서비스 계약이 동일 하면 합니다. 그러나 표면상 동일한 계약으로 인해 클라이언트에서 예외를 throw할 수 있습니다. 이러한 현상은 바인딩이 WS-Addressing 사양을 지원하지 않고 계약에 여러 수준의 보호가 지정된 경우에 발생합니다. 예를 들어 <xref:System.ServiceModel.BasicHttpBinding> 클래스가 사양을 지원하지 않거나, WS-Addressing을 지원하지 않는 사용자 지정 바인딩을 만드는 경우 등이 있습니다. `ProtectionLevel` 기능에서는 하나의 계약에 여러 개의 보호 수준을 사용할 수 있도록 WS-Addressing 사양을 사용합니다. 바인딩이 WS-Addressing 사양을 지원하지 않으면 모든 단계가 동일한 보호 수준으로 설정됩니다. 계약의 모든 범위에 대해 유효한 보호 수준은 계약에 사용되는 가장 강력한 보호 수준으로 설정됩니다.

이로 인해 디버깅 작업이 어려울 것처럼 느껴질 수 있습니다. 둘 이상의 서비스에 대한 메서드를 포함하는 클라이언트 계약(인터페이스)을 만들 수 있습니다. 즉, 여러 서비스와 통신하는 클라이언트를 만드는 데 동일한 인터페이스를 사용할 수 있습니다. 이 단일 인터페이스에는 여러 서비스에 대한 메서드가 포함됩니다. 이러한 시나리오는 드물지만, 개발자가 각각의 특정 서비스에 적용 가능한 메서드만 호출하려면 더욱 주의를 해야 합니다. 바인딩이 <xref:System.ServiceModel.BasicHttpBinding> 클래스이면 여러 보호 수준이 지원되지 않습니다. 하지만 클라이언트에 응답하는 서비스는 요구된 보호 수준보다 낮은 수준으로 클라이언트에 응답합니다. 이 경우 클라이언트에서는 더 높은 보호 수준을 필요로 하기 때문에 예외를 throw합니다.

이러한 문제는 코드 예제에서 설명하고, 다음은 서비스 및 클라이언트 계약을 보여 주는 예제입니다. 바인딩이 있다고 가정 합니다 [ \<basicHttpBinding >](../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md) 요소입니다. 계약에 대한 모든 작업은 동일한 보호 수준을 갖습니다. 이 일관된 보호 수준은 모든 작업에 대한 최대 보호 수준으로 결정됩니다.

서비스 계약은 다음과 같습니다.

[!code-csharp[c_ProtectionLevel#7](../../../samples/snippets/csharp/VS_Snippets_CFX/c_protectionlevel/cs/source.cs#7)]
[!code-vb[c_ProtectionLevel#7](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_protectionlevel/vb/source.vb#7)]

다음 코드에서는 클라이언트 계약 인터페이스를 보여 줍니다. 여기에는 다른 서비스에 사용되는 `Tax` 메서드가 포함되어 있습니다.

[!code-csharp[c_ProtectionLevel#8](../../../samples/snippets/csharp/VS_Snippets_CFX/c_protectionlevel/cs/source.cs#8)]
[!code-vb[c_ProtectionLevel#8](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_protectionlevel/vb/source.vb#8)]

클라이언트가 `Price` 메서드를 호출할 경우 서비스로부터 회신을 받으면 예외를 throw합니다. 이는 클라이언트가 `ProtectionLevel`에 `ServiceContractAttribute`을 지정하지 않아 <xref:System.Net.Security.ProtectionLevel.EncryptAndSign> 메서드를 포함한 모든 메서드에 기본값(`Price`)을 사용하기 때문입니다. 하지만 서비스 계약에서는 보호 수준이 <xref:System.Net.Security.ProtectionLevel.Sign>으로 설정된 하나의 메서드를 정의하므로, 서비스에서 <xref:System.Net.Security.ProtectionLevel.Sign> 수준을 사용하여 값을 반환합니다. 이 경우 클라이언트에서는 서비스 응답에 대한 유효성 검사를 할 때 오류를 throw합니다.

## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.ServiceContractAttribute>
- <xref:System.ServiceModel.OperationContractAttribute>
- <xref:System.ServiceModel.FaultContractAttribute>
- <xref:System.ServiceModel.MessageContractAttribute>
- <xref:System.ServiceModel.MessageHeaderAttribute>
- <xref:System.ServiceModel.MessageBodyMemberAttribute>
- <xref:System.Net.Security.ProtectionLevel>
- [서비스에 보안 설정](../../../docs/framework/wcf/securing-services.md)
- [방법: ProtectionLevel 속성 설정](../../../docs/framework/wcf/how-to-set-the-protectionlevel-property.md)
- [계약 및 서비스에서 오류 지정 및 처리](../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md)
- [메시지 계약 사용](../../../docs/framework/wcf/feature-details/using-message-contracts.md)
