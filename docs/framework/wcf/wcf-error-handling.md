---
title: WCF 오류 처리
ms.date: 03/30/2017
ms.assetid: 1e4b1e0f-9598-449d-9d73-90bda62305b8
ms.openlocfilehash: eba0894d6352bc1aea3596ee9d196b386e1eafef
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64645429"
---
# <a name="wcf-error-handling"></a>WCF 오류 처리
WCF 애플리케이션에서 발생하는 오류는 다음 세 그룹 중 하나에 속합니다.  
  
1. 통신 오류  
  
2. 프록시/채널 오류  
  
3. 애플리케이션 오류  
  
 네트워크를 사용할 수 없거나, 클라이언트가 잘못된 주소를 사용하거나, 서비스 호스트가 들어오는 메시지를 수신하고 있지 않은 경우 통신 오류가 발생합니다. 이러한 유형의 오류는 클라이언트에 <xref:System.ServiceModel.CommunicationException> 또는 <xref:System.ServiceModel.CommunicationException> 파생 클래스로 반환됩니다.  
  
 채널/프록시 오류는 채널 또는 프록시 자체 내에서 발생하는 오류입니다. 이러한 유형의 오류에는 닫힌 프록시 또는 채널 사용 시도, 클라이언트와 서비스 간의 계약 불일치, 클라이언트 자격 증명이 서비스에서 거부됨 등이 포함됩니다. 이 범주에는 여러 유형의 오류가 포함되며, 너무 많아서 여기에 모두 나열할 수는 없습니다. 이러한 유형의 오류는 클라이언트에 현재 상태대로 반환됩니다(예외 개체에서 변형이 수행되지 않음).  
  
 애플리케이션 오류는 서비스 작업을 실행하는 동안 발생합니다. 이러한 종류의 오류는 클라이언트에 <xref:System.ServiceModel.FaultException> 또는 <xref:System.ServiceModel.FaultException%601>으로 전송됩니다.  
  
 WCF의 오류 처리는 다음 방법 중 하나 이상을 통해 수행됩니다.  
  
- throw된 예외 직접 처리 이 방법은 통신 및 프록시/채널 오류에서만 수행됩니다.  
  
- 오류 계약 사용  
  
- <xref:System.ServiceModel.Dispatcher.IErrorHandler> 인터페이스 구현  
  
- <xref:System.ServiceModel.ServiceHost> 이벤트 처리  
  
## <a name="fault-contracts"></a>오류 계약  
 오류 계약을 사용하면 플랫폼에 독립적인 방법으로 서비스 작업 중에 발생할 수 있는 오류를 정의할 수 있습니다. 기본적으로 서비스 작업 내에서 throw된 모든 예외는 클라이언트에 <xref:System.ServiceModel.FaultException> 개체로 반환됩니다. <xref:System.ServiceModel.FaultException> 개체에는 정보가 거의 포함되어 있지 않습니다. 오류 계약을 정의하고 오류를 <xref:System.ServiceModel.FaultException%601>으로 반환하여 클라이언트에 전송되는 정보를 제어할 수 있습니다. 자세한 내용은 [지정 및 계약 및 서비스에서 오류 처리](../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md)합니다.  
  
## <a name="ierrorhandler"></a>IErrorHandler  
 <xref:System.ServiceModel.Dispatcher.IErrorHandler> 인터페이스를 사용하면 WCF 애플리케이션이 오류에 응답하는 방법을 보다 강력하게 제어할 수 있습니다.  클라이언트에 반환되는 오류 메시지를 완전히 제어하고 로깅 등의 사용자 지정 오류 처리를 수행할 수 있습니다.  에 대 한 자세한 내용은 <xref:System.ServiceModel.Dispatcher.IErrorHandler> 고 [확장 컨트롤을 통해 오류를 처리 하 고 보고](../../../docs/framework/wcf/samples/extending-control-over-error-handling-and-reporting.md)  
  
## <a name="servicehost-events"></a>ServiceHost 이벤트  
 <xref:System.ServiceModel.ServiceHost> 클래스는 서비스를 호스트하며 오류 처리에 필요할 수 있는 여러 이벤트를 정의합니다. 예를 들어:  
  
1. <xref:System.ServiceModel.Channels.CommunicationObject.Faulted>
  
2. <xref:System.ServiceModel.ServiceHostBase.UnknownMessageReceived>
  
 자세한 내용은 <xref:System.ServiceModel.ServiceHost>을 참조하세요.
