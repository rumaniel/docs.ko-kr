---
title: 확장성 소개
ms.date: 03/30/2017
helpviewer_keywords:
- WCF [WCF], extensibility
- Windows Communication Foundation [WCF], extensibility
- extensibility [WCF]
ms.assetid: ef56c251-d63c-4b3f-944f-b0c67bfb0f68
ms.openlocfilehash: 8ac605b562531329333b5f05e081d89de55d8cd2
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64645433"
---
# <a name="introduction-to-extensibility"></a>확장성 소개
Windows Communication Foundation (WCF) 응용 프로그램 모델은 대부분의 분산된 응용 프로그램의 통신 요구 사항 해결 하도록 설계 되었습니다. 그러나 기본 애플리케이션 모델과 시스템 제공 구현이 지원되지 않습니다. WCF 확장성 모델의 전체 응용 프로그램 모델을 대체 지점에도 모든 수준에서 시스템 동작을 수정할 수 있도록 하 여 사용자 지정 시나리오를 지원 됩니다. 이 항목에서는 다양한 확장명 영역에 대해 간략하게 설명하고 각 영역에 대한 자세한 내용을 제공합니다.  
  
## <a name="areas-to-extend"></a>확장할 영역  
 확장 가능 영역:  
  
- 애플리케이션 런타임. 이 영역에서는 애플리케이션에 대한 메시지 처리 및 디스패치를 확장합니다. 또한 이 영역은 보안 시스템, 메타데이터 시스템, serialization 시스템 확장을 비롯하여 애플리케이션을 기본 채널 시스템에 연결하는 바인딩 및 바인딩 요소 확장을 포함합니다.  
  
- 채널 및 채널 런타임. 이 영역에서는 프로토콜, 전송 및 인코딩 지원을 제공하여 메시지 수준에서 작동하는 시스템을 확장합니다.  
  
- 호스트 런타임. 이 영역에서는 호스트 애플리케이션 도메인과 채널 및 애플리케이션 런타임의 관계를 확장합니다.  
  
### <a name="extending-the-application-runtime"></a>애플리케이션 런타임 확장  
 WCF 응용 프로그램에서 응용 프로그램 자체에 대 한 보내는 메시지의 대상이 해당 채널인 메시지 사이의 구분이 됩니다. 채널 메시지는 보안 대화 설정, 신뢰할 수 있는 세션 설정과 같은 일부 채널 관련 기능을 지원합니다. 이러한 메시지는 애플리케이션 런타임에 사용할 수 없으며, 애플리케이션 계층이 포함되기 이전에 처리됩니다.  
  
 애플리케이션 메시지는 사용자 또는 사용자의 고객이 만든 클라이언트 또는 서비스 작업을 대상으로 하는 데이터를 포함합니다. 이러한 메시지는 애플리케이션 수준 확장 시스템에서 필요에 따라 메시지 또는 개체 형태로 사용할 수 있습니다.  
  
 모든 메시지는 채널 시스템을 통해 전달되고, 애플리케이션 메시지만 채널 시스템에서 애플리케이션으로 전달됩니다. 새 채널 수준 기능을 만들려면 채널 시스템을 확장해야 합니다. 새 애플리케이션 수준 기능을 만들려면 서비스 또는 클라이언트 런타임(각각 디스패처 및 채널 팩터리)을 확장해야 합니다. 응용 프로그램 런타임 확장 하는 방법에 대 한 자세한 내용은 참조 하세요. [Extending ServiceHost 및 서비스 모델 계층](../../../docs/framework/wcf/extending/extending-servicehost-and-the-service-model-layer.md)합니다.  
  
#### <a name="extending-security"></a>보안 확장  
 토큰 및 자격 증명과 같은 사용자 지정 보안 메커니즘을 빌드하려면 보안 시스템을 확장해야 합니다. 자세한 내용은 [보안 확장](../../../docs/framework/wcf/extending/extending-security.md)합니다.  
  
#### <a name="extending-metadata"></a>메타데이터 확장  
 메타데이터를 기본값과 다르게 노출하려면 메타데이터 시스템을 확장해야 합니다. 자세한 내용은 [메타 데이터 시스템 확장](../../../docs/framework/wcf/extending/extending-the-metadata-system.md)합니다.  
  
#### <a name="extending-serialization"></a>Serialization 확장  
 사용자 지정 인코더를 빌드하거나, 데이터 서로게이트를 제공하거나, 전송된 데이터에 대한 사용자 지정과 관련된 다른 작업을 수행하려면 serialization 시스템을 확장해야 합니다. 자세한 내용은 [확장 인코더 및 Serializer](../../../docs/framework/wcf/extending/extending-encoders-and-serializers.md)합니다.  
  
#### <a name="extending-bindings"></a>바인딩 확장명  
 전송 또는 프로토콜 채널을 애플리케이션 계층에 연결하려면 바인딩 시스템을 확장해야 합니다. 자세한 내용은 [바인딩 확장](../../../docs/framework/wcf/extending/extending-bindings.md)합니다.  
  
### <a name="extending-the-channel-system"></a>채널 시스템 확장  
 채널 지원 사용자 지정 전송 또는 프로토콜 기능을 참조 하세요 [채널 계층 확장](../../../docs/framework/wcf/extending/extending-the-channel-layer.md)합니다.  
  
### <a name="extending-the-service-hosting-system"></a>서비스 호스팅 시스템 확장  
 서비스 차원 애플리케이션 모델을 수정하려면 <xref:System.ServiceModel.ServiceHostBase?displayProperty=nameWithType> 클래스를 확장해야 합니다. 자세한 내용은 [Extending ServiceHost 및 서비스 모델 계층](../../../docs/framework/wcf/extending/extending-servicehost-and-the-service-model-layer.md)합니다.  
  
 호스팅 애플리케이션 도메인과 서비스 호스트 간의 관계를 수정하려면 <xref:System.ServiceModel.Activation.ServiceHostFactory?displayProperty=nameWithType> 클래스를 확장해야 합니다. 자세한 내용은 [호스트를 사용 하 여 ServiceHostFactory 확장](../../../docs/framework/wcf/extending/extending-hosting-using-servicehostfactory.md)합니다.  
  
## <a name="see-also"></a>참고자료

- [WCF 확장](../../../docs/framework/wcf/extending/index.md)
