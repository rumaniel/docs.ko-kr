---
title: Windows Communication Foundation 정의
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Communication Foundation [WCF], technology overview
- technology overview [WCF]
- WCF [WCF], technology overview
ms.assetid: 40e1009d-ef15-450b-9848-62eabe5e5738
ms.openlocfilehash: 21a01c5d59d30ac89f6baa19dbcdcf718a1b7d88
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834844"
---
# <a name="what-is-windows-communication-foundation"></a>Windows Communication Foundation 정의
WCF (Windows Communication Foundation)는 서비스 지향 응용 프로그램을 빌드하기 위한 프레임 워크입니다. WCF를 사용 하면 한 서비스 끝점에서 다른 서비스 끝점으로 데이터를 비동기 메시지로 보낼 수 있습니다. 서비스 엔드포인트는 IIS에서 호스팅하는 계속 사용 가능한 서비스의 일부분일 수도 있고 애플리케이션에서 호스팅되는 서비스일 수도 있습니다. 또한 엔드포인트는 서비스 엔드포인트에서 데이터를 요청하는 서비스의 클라이언트일 수 있습니다. 메시지는 XML로 전송되는 한 문자나 단어처럼 간단할 수도 있고 이진 데이터 스트림처럼 복잡할 수도 있습니다. 다음은 몇 가지 샘플 시나리오입니다.

- 비즈니스 트랜잭션을 처리하는 보안 서비스

- 트래픽 보고서 또는 기타 모니터링 서비스와 같은 최신 데이터를 다른 서비스에 제공하는 서비스

- 두 사람이 실시간으로 통신하거나 데이터를 교환할 수 있도록 하는 채팅 서비스

- 하나 이상의 서비스를 폴링해 데이터를 가져와서 논리적 프레젠테이션으로 표시하는 대시보드 애플리케이션

- Windows Workflow Foundation을 사용하여 구현되는 워크플로를 WCF 서비스로 노출

- 서비스를 폴링해 최신 데이터 피드를 가져오는 Silverlight 애플리케이션

Wcf를 사용 하기 전에 이러한 응용 프로그램을 만드는 것이 가능 했지만, WCF를 사용 하면 끝점을 보다 쉽게 개발할 수 있습니다. 요약 하자면, WCF는 웹 서비스와 웹 서비스 클라이언트를 만들 수 있는 관리 가능한 방법을 제공 하도록 설계 되었습니다.

## <a name="features-of-wcf"></a>WCF의 기능

WCF에는 다음과 같은 기능 집합이 포함 되어 있습니다. 자세한 내용은 [WCF 기능 정보](../../../docs/framework/wcf/feature-details/index.md)를 참조 하세요.

- **서비스 지향성**

     WS 표준을 사용 하는 경우 WCF를 사용 하면 *서비스 지향* 응용 프로그램을 만들 수 있습니다. SOA(서비스 지향 아키텍처) 방식에서는 웹 서비스를 사용하여 데이터를 보내고 받습니다. 이러한 서비스에서는 애플리케이션이 서로 하드 코드되지 않고 느슨하게 결합된다는 장점이 있습니다. 느슨하게 결합된 관계란 필수 계약이 충족되는 한 모든 플랫폼에서 만들어지는 모든 클라이언트가 어떤 서비스에나 연결할 수 있는 관계입니다.

- **상호 운용성**

     WCF는 웹 서비스 상호 운용성을 위한 최신 업계 표준을 구현 합니다. 지원 되는 표준에 대 한 자세한 내용은 [상호 운용성 및 통합](../../../docs/framework/wcf/feature-details/interoperability-and-integration.md)을 참조 하세요.

- **다양한 메시지 패턴**

     메시지가 교환되는 패턴에는 여러 가지가 있습니다. 그 중에서 가장 일반적인 패턴인 요청/회신 패턴에서는 한 엔드포인트에서 두 번째 엔드포인트의 데이터를 요청합니다. 그러면 두 번째 엔드포인트에서 회신을 합니다. 또한 단일 엔드포인트에서 회신을 기대하지 않고 메시지를 보내는 단방향 메시지와 같은 패턴도 있습니다. 보다 복잡한 패턴인 이중 교환 패턴은 두 엔드포인트가 하나의 연결을 설정하여 데이터를 주고 받는 것으로, 인스턴트 메시징 프로그램과 유사합니다. WCF를 사용 하 여 다양 한 메시지 교환 패턴을 구현 하는 방법에 대 한 자세한 내용은 [계약](../../../docs/framework/wcf/feature-details/contracts.md)을 참조 하세요.

- **서비스 메타데이터**

     WCF에서는 WSDL, XML 스키마 및 WS-POLICY와 같은 산업 표준에 지정 된 형식을 사용 하 여 서비스 메타 데이터를 게시할 수 있습니다. 이 메타 데이터를 사용 하 여 WCF 서비스에 액세스 하기 위한 클라이언트를 자동으로 생성 하 고 구성할 수 있습니다. 메타데이터는 HTTP 및 HTTPS를 통해 게시하거나 웹 서비스 메타데이터 교환 표준을 사용하여 게시할 수 있습니다. 자세한 내용은 [메타 데이터](../../../docs/framework/wcf/feature-details/metadata.md)를 참조 하세요.

- **데이터 계약**

     WCF는 .NET Framework를 사용 하 여 빌드 되므로 적용 하려는 계약을 제공 하는 코드에 친숙 한 메서드도 포함 합니다. 널리 사용되는 계약 유형 중 하나는 데이터 계약입니다. 기본적으로 Visual C# 또는 Visual Basic을 사용하여 서비스 코드를 작성할 때 데이터를 가장 쉽게 처리하는 방법은 데이터 엔터티에 속하는 속성을 사용하여 해당 데이터 엔터티를 나타내는 클래스를 만드는 것입니다. WCF에는이 간편한 방식으로 데이터를 사용 하기 위한 포괄적인 시스템이 포함 되어 있습니다. 데이터를 나타내는 클래스를 만들면 서비스에서 메타데이터를 자동으로 생성하며, 이 메타데이터는 클라이언트가 사용자가 디자인한 데이터 형식을 준수할 수 있도록 합니다. 자세한 내용은 [데이터 계약 사용](../../../docs/framework/wcf/feature-details/using-data-contracts.md)을 참조 하세요.

- **보안**

     개인 정보를 보호하기 위해 메시지를 암호화할 수 있으며, 사용자가 인증을 해야 메시지를 받을 수 있도록 지정할 수 있습니다. SSL 또는 WS-SecureConversation 등의 널리 알려진 표준을 사용하여 보안을 구현할 수 있습니다. 자세한 내용은 [보안](../../../docs/framework/wcf/feature-details/security.md)을 참조하세요.

- **다양한 전송 및 인코딩**

     기본 제공되는 여러 전송 프로토콜 및 인코딩 중 원하는 항목을 사용하여 메시지를 전송할 수 있습니다. 가장 일반적인 프로토콜 및 인코딩은 World Wide Web에서 사용 하기 위해 HTTP (하이퍼텍스트 전송 프로토콜)를 사용 하 여 텍스트 인코딩된 SOAP 메시지를 보내는 것입니다. 또는 WCF를 사용 하 여 TCP, 명명 된 파이프 또는 MSMQ를 통해 메시지를 보낼 수 있습니다. 이러한 메시지는 텍스트로 인코딩할 수도 있고 최적화된 이진 형식을 사용하여 인코딩할 수도 있습니다.  이진 데이터는 MTOM 표준을 사용하여 보내는 것이 효율적입니다. 제공되는 전송 또는 인코딩 중에서 요구 사항에 적합한 항목이 없는 경우에는 사용자 지정 전송 또는 인코딩을 직접 만들 수 있습니다. WCF에서 지 원하는 전송 및 인코딩에 대 한 자세한 내용은 [전송](../../../docs/framework/wcf/feature-details/transports.md)을 참조 하세요.

- **신뢰할 수 있는 메시지 및 대기 중인 메시지**

     WCF는 신뢰할 수 있는 메시징 및 MSMQ 사용을 통해 구현 된 신뢰할 수 있는 세션을 사용 하 여 신뢰할 수 있는 메시지 교환을 지원 합니다 WCF의 신뢰할 수 있는 메시징 및 대기 중인 메시징 지원에 대 한 자세한 내용은 [큐 및 신뢰할](../../../docs/framework/wcf/feature-details/queues-and-reliable-sessions.md)수 있는 세션을 참조 하세요.

- **지속적 메시지**

     지속적 메시지는 통신이 중단되어도 손실되지 않는 메시지입니다. 지속적 메시지 패턴의 메시지는 항상 데이터베이스에 저장됩니다. 통신이 중단되는 경우 연결이 복원되면 데이터베이스가 메시지 교환을 다시 시작할 수 있도록 해 줍니다. WF (Windows Workflow Foundation)를 사용 하 여 지 속성 메시지를 만들 수도 있습니다. 자세한 내용은 [워크플로 서비스](../../../docs/framework/wcf/feature-details/workflow-services.md)를 참조 하세요.

- **트랜잭션**

     또한 WCF는 세 가지 트랜잭션 모델 중 하나를 사용 하 여 트랜잭션을 지원 합니다. AtomicTransactions, <xref:System.Transactions> 네임 스페이스의 Api 및 Microsoft DTC(Distributed Transaction Coordinator). WCF의 트랜잭션 지원에 대 한 자세한 내용은 [트랜잭션](../../../docs/framework/wcf/feature-details/transactions-in-wcf.md)을 참조 하십시오.

- **AJAX 및 REST 지원**

     REST는 Web 2.0 기술 발전에 대한 한 가지 예일 뿐입니다. WCF는 SOAP 봉투에 래핑되지 않은 "일반" XML 데이터를 처리 하도록 구성할 수 있습니다. 또한 WCF는 ATOM (인기 RSS 표준)과 같은 특정 XML 형식 뿐만 아니라 JavaScript Object Notation (JSON)와 같은 비 XML 형식도 지원 하도록 확장할 수 있습니다.

- **확장성**

     WCF 아키텍처에는 다양 한 확장성 지점이 있습니다. 추가적인 기능이 필요한 경우에는 여러 진입점을 통해 서비스 동작을 사용자 지정할 수 있습니다. 사용 가능한 확장 요소에 대 한 자세한 내용은 [WCF 확장](../../../docs/framework/wcf/extending/index.md)을 참조 하세요.

## <a name="wcf-integration-with-other-microsoft-technologies"></a>WCF와 다른 Microsoft 기술의 통합

WCF는 유연한 플랫폼입니다. 이러한 극단적인 유연성으로 인해 WCF는 다른 여러 Microsoft 제품 에서도 사용 됩니다. WCF의 기본 사항을 이해 하면 이러한 제품을 사용 하는 경우에도 즉시 활용할 수 있습니다.

WCF와 함께 사용 하는 첫 번째 기술은 WF (Windows Workflow Foundation) 였습니다. 워크플로는 워크플로의 단계를 "활동"으로 캡슐화 하 여 응용 프로그램 개발을 간소화 합니다. Windows Workflow Foundation의 첫 번째 버전에서 개발자는 워크플로에 대 한 호스트를 만들어야 했습니다. Windows Workflow Foundation의 다음 버전은 WCF와 통합 되었습니다. 이렇게 하면 모든 워크플로를 WCF 서비스에서 쉽게 호스팅할 수 있습니다. Visual Studio 2012 이상에서 WF/WCF 프로젝트 형식을 자동으로 선택 하 여이 작업을 수행할 수 있습니다.

Microsoft BizTalk Server R2는 또한 WCF를 통신 기술로 활용 합니다. BizTalk는 표준화된 형식 간에 데이터를 전송 및 수신하도록 디자인되었습니다. 메시지는 중앙의 메시지 상자로 배달되어야 하며, 여기서 엄격한 매핑을 사용하거나 워크플로 엔진과 같은 BizTalk 기능 중 하나를 사용하여 메시지를 변환할 수 있습니다. 이제 BizTalk에서 WCF LOB (기간 업무) 어댑터를 사용 하 여 메시지를 메시지 상자에 배달할 수 있습니다.

Microsoft Silverlight는 상호 운용 가능하며 다양한 기능을 제공하는 웹 애플리케이션을 만들기 위한 플랫폼입니다. 개발자는 이러한 웹 애플리케이션을 통해 스트리밍 비디오 등의 다양한 미디어를 사용하는 웹 사이트를 만들 수 있습니다. 버전 2부터 Silverlight는 Silverlight 응용 프로그램을 WCF 끝점에 연결 하기 위한 통신 기술로 WCF를 통합 했습니다.

Windows Server AppFabric 응용 프로그램 서버의 호스팅 기능은 특별히 통신을 위해 WCF를 사용 하는 응용 프로그램을 배포 하 고 관리 하기 위해 특별히 설계 되었습니다. 호스팅 기능에는 WCF 지원 응용 프로그램을 위해 특별히 설계 된 다양 한 도구 및 구성 옵션이 포함 되어 있습니다.

## <a name="see-also"></a>참조

- <xref:System.ServiceModel>
- [기본적인 Windows Communication Foundation 개념](../../../docs/framework/wcf/fundamental-concepts.md)
- [Windows Communication Foundation 아키텍처](../../../docs/framework/wcf/architecture.md)
- [지침 및 모범 사례](../../../docs/framework/wcf/guidelines-and-best-practices.md)
- [초보자를 위한 자습서](../../../docs/framework/wcf/getting-started-tutorial.md)
- [설명서에 대한 안내](../../../docs/framework/wcf/guide-to-the-documentation.md)
- [기본 WCF 프로그래밍](../../../docs/framework/wcf/basic-wcf-programming.md)
- [Windows Communication Foundation 샘플](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751514%28v=vs.90%29)
