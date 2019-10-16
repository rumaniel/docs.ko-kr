---
title: '엔드포인트: 주소, 바인딩 및 계약'
ms.date: 03/30/2017
helpviewer_keywords:
- endpoints [WCF]
- Windows Communication Foundation [WCF], endpoints
- WCF [WCF], endpoints
ms.assetid: 9ddc46ee-1883-4291-9926-28848c57e858
ms.openlocfilehash: 361ed623e50b409147387a0edec7f42c733f3d48
ms.sourcegitcommit: d6e27023aeaffc4b5a3cb4b88685018d6284ada4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67664117"
---
# <a name="endpoints-addresses-bindings-and-contracts"></a>엔드포인트: 주소, 바인딩 및 계약

Windows Communication Foundation (WCF) 서비스와 모든 통신을 통해 발생 합니다 *끝점* 서비스입니다. 끝점 클라이언트는 WCF 서비스에서 제공 하는 기능에 대 한 액세스를 제공 합니다.

각 엔드포인트는 다음 네 가지 속성으로 구성됩니다.

- 엔드포인트를 찾을 위치를 나타내는 주소

- 클라이언트가 엔드포인트와 통신할 수 있는 방법을 지정하는 바인딩

- 사용 가능한 작업을 식별하는 계약

- 엔드포인트의 로컬 구현 세부 정보를 지정하는 동작 집합

이 항목에서는이 끝점 구조에 설명 하 고 WCF 개체 모델에서 나타나는 방법에 대해 설명 합니다.

## <a name="the-structure-of-an-endpoint"></a>엔드포인트의 구조

각 엔드포인트는 다음으로 구성됩니다.

- 주소: 주소에서 고유 하 게 끝점을 식별 하 고 가능성을 알려 줍니다 위치한 서비스의 소비자입니다. WCF 개체 모델에서 표시 됩니다는 <xref:System.ServiceModel.EndpointAddress> 클래스입니다. <xref:System.ServiceModel.EndpointAddress> 클래스에는 다음이 포함됩니다.

  - 서비스의 주소를 나타내는 <xref:System.ServiceModel.EndpointAddress.Uri%2A> 속성.

  - 서비스의 보안 ID 및 선택적 메시지 헤더의 컬렉션을 나타내는 <xref:System.ServiceModel.EndpointAddress.Identity%2A> 속성. 선택적 메시지 헤더는 엔드포인트 확인 및 엔드포인트와의 상호 작용을 위해 자세한 추가 주소 지정 정보를 제공하는 데 사용합니다.

  자세한 내용은 [끝점 주소 지정](../../../../docs/framework/wcf/specifying-an-endpoint-address.md)합니다.

- 바인딩: 바인딩은 엔드포인트와 통신하는 방법을 지정합니다. 여기에는 다음이 포함됩니다.

  - 사용할 전송 프로토콜(예: TCP 또는 HTTP)

  - 메시지에 사용할 인코딩(예: 텍스트 또는 이진)

  - 필요한 보안 요구 사항(예: SSL 또는 SOAP 메시지 보안)

  자세한 내용은 [WCF 바인딩 개요](../../../../docs/framework/wcf/bindings-overview.md)합니다. 바인딩을 WCF 개체 모델 추상 기본 클래스에 의해 표현 됩니다 <xref:System.ServiceModel.Channels.Binding>합니다. 대부분의 시나리오의 경우 사용자는 시스템 제공 바인딩 중 하나를 사용할 수 있습니다. 자세한 내용은 [System-Provided Bindings](../../../../docs/framework/wcf/system-provided-bindings.md)합니다.

- 계약: 계약에서는 끝점이 클라이언트에 노출 하는 기능을 설명 합니다. 계약에서는 다음을 지정합니다.

  - 클라이언트가 호출할 수 있는 작업

  - 메시지 형식

  - 작업을 호출하는 데 필요한 입력 매개 변수 또는 데이터 형식

  - 클라이언트가 예상할 수 있는 처리 또는 응답 메시지 형식

  계약을 정의 하는 방법에 대 한 자세한 내용은 참조 하세요. [Designing Service Contracts](../../../../docs/framework/wcf/designing-service-contracts.md)합니다.

- 동작: 서비스 끝점의 로컬 동작을 사용자 지정 끝점 동작을 사용할 수 있습니다. 끝점 동작은 WCF 런타임 빌드 프로세스에 참여 하 여이 작업을 수행 합니다. 엔드포인트 동작의 예는 <xref:System.ServiceModel.Description.ServiceEndpoint.ListenUri%2A> 속성이며, 이 속성을 사용하여 SOAP 또는 WSDL(웹 서비스 기술 언어) 주소 이외의 다른 수신 대기 주소를 지정할 수 있습니다. 자세한 내용은 [ClientViaBehavior](../../../../docs/framework/wcf/diagnostics/wmi/clientviabehavior.md)합니다.

## <a name="defining-endpoints"></a>엔드포인트 정의

구성을 통해 코드를 명령적으로 또는 선언적으로 사용하여 서비스의 엔드포인트를 지정할 수 있습니다. 자세한 내용은 [방법: 구성에서 서비스 끝점을 만드는](../../../../docs/framework/wcf/feature-details/how-to-create-a-service-endpoint-in-configuration.md) 고 [방법: 코드에서 서비스 끝점을 만드는](../../../../docs/framework/wcf/feature-details/how-to-create-a-service-endpoint-in-code.md)합니다.

## <a name="in-this-section"></a>섹션 내용

이 단원에서는 바인딩, 엔드포인트 및 주소의 용도에 대해 설명하고 바인딩 및 엔드포인트를 구성하는 방법과 `ClientVia` 동작 및 `ListenUri` 속성을 사용하는 방법을 보여 줍니다.

[주소](../../../../docs/framework/wcf/feature-details/endpoint-addresses.md)\
WCF의 끝점 주소를 지정 하는 방법을 설명 합니다.

[Bindings](../../../../docs/framework/wcf/feature-details/bindings.md)\
바인딩을 사용하여 클라이언트와 서비스 간에 통신하는 데 필요한 전송, 인코딩 및 프로토콜 세부 정보를 지정하는 방법에 대해 설명합니다.

[계약](../../../../docs/framework/wcf/feature-details/contracts.md)\
계약이 서비스 메서드를 정의하는 방법에 대해 설명합니다.

[방법: 구성에서 서비스 끝점 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-service-endpoint-in-configuration.md)\
구성에서 서비스 엔드포인트를 만드는 방법에 대해 설명합니다.

[방법: 코드에서 서비스 끝점 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-service-endpoint-in-code.md)\
코드에서 서비스 엔드포인트를 만드는 방법에 대해 설명합니다.

[방법: Svcutil.exe를 사용 하 여 컴파일된 서비스 코드 유효성 검사](../../../../docs/framework/wcf/feature-details/how-to-use-svcutil-exe-to-validate-compiled-service-code.md)\
사용 하 여 서비스를 호스트 하지 않고 서비스 구현과 구성에서 오류를 검색 하는 방법에 설명 합니다 [ServiceModel Metadata 유틸리티 도구 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)합니다.

## <a name="see-also"></a>참고자료

- [서비스 구성](../../../../docs/framework/wcf/configuring-services.md)
- [바인딩 확장](../../../../docs/framework/wcf/extending/extending-bindings.md)
