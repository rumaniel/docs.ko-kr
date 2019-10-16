---
title: 서비스 디자인 및 구현
ms.date: 03/30/2017
helpviewer_keywords:
- defining service contracts [WCF]
ms.assetid: 036fae20-7c55-4002-b71d-ac4466e167a3
ms.openlocfilehash: 5cbf7c16988d8b8858aa75f4e7a956fa371238dd
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64652042"
---
# <a name="designing-and-implementing-services"></a>서비스 디자인 및 구현
이 섹션에서는 정의 하 고 WCF 계약을 구현 하는 방법을 보여 줍니다. 서비스 계약에서는 엔드포인트가 외부와 통신하는 내용을 지정합니다. 더 구체적으로 말하면, 단방향 및 이중 request/reply와 같은 기본 메시지 교환 패턴에 구성된 특정 메시지 집합에 대한 문입니다. 서비스 계약이 논리적으로 관련된 메시지 교환 집합인 경우 서비스 작업은 단일 메시지 교환이 됩니다. 예를 들어 `Hello` 작업에서는 호출자가 인사말을 알릴 수 있도록 단일 메시지를 수락해야 하며 작업 의례에 따라 메시지를 반환하거나 반환하지 않을 수 있습니다.  
  
 계약 및 다른 핵심 Windows Communication Foundation (WCF) 개념에 대 한 자세한 내용은 참조 하세요. [기본적인 Windows Communication Foundation 개념](../../../docs/framework/wcf/fundamental-concepts.md)합니다. 이 항목에서는 서비스 계약을 이해하는 데 중점을 둡니다. 서비스에 연결 하려면 서비스 계약을 사용 하는 클라이언트를 빌드하는 방법에 대 한 자세한 내용은 참조 하세요. [WCF Client Overview](../../../docs/framework/wcf/wcf-client-overview.md)합니다.  
  
## <a name="overview"></a>개요  
 이 항목에서는 WCF 서비스 디자인 및 구현에 높은 수준의 개념 방향을 제시 합니다. 특정 디자인 및 구현에 대한 자세한 내용은 하위 항목에서 제공됩니다. 것이 좋습니다를 디자인 하 고 WCF 응용 프로그램을 구현 하기 전에:  
  
- 서비스 계약에 대한 정의, 작동 방식 및 생성 방법  
  
- 런타임 구성 또는 호스팅 환경에서 지원되지 않을 수 있는 계약 상태 최소 요구 사항  
  
## <a name="service-contracts"></a>서비스 계약  
 서비스 계약은 다음을 지정합니다.  
  
- 계약이 노출하는 작업  
  
- 교환되는 메시지와 관련된 작업 서명  
  
- 이러한 메시지의 데이터 형식  
  
- 작업의 위치  
  
- 서비스와의 통신을 지원하는 데 사용되는 특정 프로토콜 및 serialization 형식  
  
 예를 들어 구매 주문 계약에는 주문 정보 유형에 대한 입력을 수락하고 주문 식별자를 비롯한 성공 또는 실패 정보를 반환하는 `CreateOrder` 작업이 포함될 수 있습니다. 또한 주문 식별자를 수락하고 주문 상태 정보를 반환하는 `GetOrderStatus` 작업이 포함될 수 있습니다. 이러한 종류의 서비스 계약에서는 다음을 지정합니다.  
  
1. `CreateOrder` 및 `GetOrderStatus` 작업으로 구성된 구매 주문 계약  
  
2. 입력 메시지와 출력 메시지를 지정한 작업  
  
3. 이러한 메시지에서 전달할 수 있는 데이터  
  
4. 메시지를 처리하는 데 필요한 통신 인프라에 대한 범주별 문 (예: 통신을 위해 보안이 필요한지 여부 및 필요한 보안 양식 등에 대한 세부 사항)  
  
 이러한 종류의 다양 한 플랫폼 (포함 하 여 Microsoft 이외의 플랫폼)에서 다른 응용 프로그램에 대 한 정보를 전달 하기 위해 XML 서비스 계약은 공개적으로에서 표현 되는 표준 XML 형식으로와 같은 [Web Services Description Language](https://go.microsoft.com/fwlink/?LinkId=94952) ( WSDL) 및 [XML 스키마](https://go.microsoft.com/fwlink/?LinkId=94953) (XSD) 중 일부입니다. 여러 플랫폼의 개발자의 경우 언어 사양에 대해 이해하고 있고 이러한 언어는 서비스에서 지원하는 공용 양식, 형식 및 프로토콜에 대해 기술함으로써 상호 운용이 가능하도록 디자인되어 있으므로, 개발자는 이러한 공개 계약 정보를 사용하여 서비스와 통신할 수 있는 애플리케이션을 만들 수 있습니다. WCF에서 이러한 종류의 정보를 처리 하는 방법에 대 한 자세한 내용은 참조 하세요. [메타 데이터](../../../docs/framework/wcf/feature-details/metadata.md)입니다.  
  
 계약은 여러 방식으로 표현할 수 있습니다. WSDL 및 XSD는 액세스 가능한 방식으로 서비스를 기술하는 뛰어난 언어인 반면 직접 사용하기에 어렵고 서비스 계약 구현이 아닌 서비스에 대해서만 기술하는 언어입니다. 따라서 WCF 응용 프로그램 사용 하 여 관리 되는 특성, 인터페이스 및 클래스 모두 서비스의 구조를 정의 하 고 구현 합니다.  
  
 관리 되는 형식으로 정의 되어 만들어진 계약은 수 *내보낸* 메타 데이터로, WSDL 및 XSD-클라이언트나 다른 서비스 구현자에서 필요한 경우. 이를 통해 모든 클라이언트 애플리케이션에 대해 공용 메타데이터를 사용하여 기술할 수 있는 간단한 프로그래밍 모델이 만들어집니다. Wcf의 필요한 변환이 서비스 계약 형식 시스템에서 XML 형식 시스템에 자동으로 수행 하는 기본 SOAP 메시지, 전송 및 보안 관련 정보 및 등의 세부 정보를 유지할 수 있습니다.  
  
 계약을 디자인 하는 방법에 대 한 자세한 내용은 참조 하세요. [Designing Service Contracts](../../../docs/framework/wcf/designing-service-contracts.md)합니다. 계약을 구현 하는 방법에 대 한 자세한 내용은 참조 하세요. [Implementing Service Contracts](../../../docs/framework/wcf/implementing-service-contracts.md)합니다.  
  
### <a name="messages-up-front-and-center"></a>중심적 역할의 메시지  
 RPC(원격 프로시저 호출) 스타일의 메서드 서명에 익숙한 경우에는 관리되는 인터페이스, 클래스 및 메서드를 사용하여 서비스 작업을 모델링하는 것이 수월합니다. 이러한 서명에서는 매개 변수를 메서드에 전달하고 반환 값을 받는 것이 개체나 다른 형식의 코드로부터 기능을 요청하는 일반적인 방법입니다. 사용 하 여 프로그래머에 게 Visual Basic과 같은 언어를 관리 하는 예를 들어, 및 C++ COM에 적용할 수는 RPC 스타일의 방법에 대 한 지식을 (개체 또는 인터페이스를 사용 하 여) 여부 WCF 서비스 계약의 생성 문제를 경험 하지 않고 RPC 스타일의 분산 개체 시스템입니다. 서비스 지향은 RPC 프로그래밍 경험의 친숙함과 편리함은 유지하면서 느슨하게 결합된 메시지 기반 프로그래밍의 이점을 제공합니다.  
  
 대부분의 프로그래머는 Microsoft MSMQ와 같은 메시지 큐, .NET Framework의 <xref:System.Messaging> 네임스페이스 또는 HTTP 요청 시의 비구조적 XML 전송과 같은 메시지 기반 애플리케이션의 프로그래밍 인터페이스에 더 친숙합니다. 메시지 수준의 프로그래밍에 대 한 자세한 내용은 참조 하세요. [Using Message Contracts](../../../docs/framework/wcf/feature-details/using-message-contracts.md)하십시오 [서비스 채널 수준 프로그래밍](../../../docs/framework/wcf/extending/service-channel-level-programming.md), 및 [POX응용프로그램과상호운용성](../../../docs/framework/wcf/feature-details/interoperability-with-pox-applications.md).  
  
### <a name="understanding-the-hierarchy-of-requirements"></a>요구 사항 계층 구조 이해  
 서비스 계약에서는 작업을 그룹화하고 메시지 교환 패턴, 메시지 유형 및 메시지에서 전달하는 데이터 형식을 지정합니다. 또한 계약을 지원하기 위해 구현에 포함되어야 하는 런타임 동작의 범주를 나타냅니다(예: 메시지 암호화 및 서명을 요구할 수 있음). 서비스 계약 자체에서는 이러한 요구 사항이 어떻게 부합되는지 자세히 지정하지 않고 부합되어야 한다는 점만 지정합니다. 암호화 유형이나 메시지 서명 방법은 규격 서비스의 구현 및 구성에 따라 결정됩니다.  
  
 동작을 추가하기 위해 계약에서 런타임 구성 및 서비스 계약 구현의 특정 부분을 요구하는 방식에 유의해야 합니다. 사용할 서비스 노출을 위해 부합해야 하는 요구 사항은 이전의 요구 사항을 바탕으로 합니다. 계약에서 구현에 대한 요구 사항을 정하는 경우에는, 구현에서 서비스 실행을 위한 바인딩 및 구성을 더욱 많이 요구할 수 있습니다. 또한 호스트 애플리케이션에서도 서비스 구성 및 바인딩을 통해 추가된 모든 요구 사항을 지원해야 합니다.  
  
 이러한 추가 요구 사항 프로세스는 디자인, 구현, 구성 및 Windows Communication Foundation (WCF) 서비스 응용 프로그램을 호스트 하는 동안 주의 해야 합니다. 예를 들어 세션 지원이 필요함을 계약에서 지정할 수 있습니다. 이 경우, 해당 계약 요구 사항을 지원하도록 바인딩을 구성해야 하며 그렇지 않으면 서비스 구현이 이루어지지 않습니다. 또는 Windows 통합 인증을 요구하는 서비스가 IIS(인터넷 정보 서비스)에서 호스팅되는 경우 해당 서비스가 있는 웹 애플리케이션에는 Windows 통합 인증을 사용하도록 설정되고 익명 지원은 해제되어야 합니다. 다른 유형의 서비스 호스트 응용 프로그램에 미치는 영향에 대 한 자세한 내용은 참조 하세요. [호스팅 서비스](../../../docs/framework/wcf/hosting-services.md)합니다.  
  
## <a name="see-also"></a>참고자료

- [서비스 계약 디자인](../../../docs/framework/wcf/designing-service-contracts.md)
- [서비스 계약 구현](../../../docs/framework/wcf/implementing-service-contracts.md)
