---
title: 리소스 사용 제어 및 성능 향상
ms.date: 03/30/2017
ms.assetid: 9a829669-5f76-4c88-80ec-92d0c62c0660
ms.openlocfilehash: 11d1333ed0ae8b46f8f87fa6f4643d4b31fac3ff
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61785062"
---
# <a name="controlling-resource-consumption-and-improving-performance"></a>리소스 사용 제어 및 성능 향상
이 항목에서는 리소스 소모를 작동 및 성능 메트릭에 영향을 주는 Windows Communication Foundation (WCF) 아키텍처의 다른 영역에서 다양 한 속성을 설명 합니다.

## <a name="properties-that-constrain-resource-consumption-in-wcf"></a>WCF에서 리소스 사용을 제한하는 속성
 Windows Communication Foundation (WCF)에 특정 유형의 보안 또는 성능 목적에 대 한 프로세스에는 제한이 적용 됩니다. 이러한 제약 조건은 할당량이나 스로틀 같은 두 가지 기본 형태로 나타납니다. *할당량* 도달 또는 초과 시 시스템에서 일부 지점에서 즉각적인 예외를 트리거하는 제한 됩니다. *제한* 예외가 throw 될 즉시 발생 하지 않는 제한 됩니다. 대신 스로틀 한계에 도달하면 프로세스는 해당 스로틀 값으로 설정된 한계 내에서만 계속 수행됩니다. 이러한 제한된 처리로 다른 위치에 예외가 트리거될 수 있지만, 애플리케이션에 따라 다릅니다.

 할당량과 스로틀 간의 차이 외에도 제약 속성 중 일부는 serialization 수준에, 일부는 전송 수준에, 일부는 애플리케이션 수준에 있는 등 차이가 있습니다. 예를 들어, 모든 시스템 제공 전송 바인딩 요소에 의해 구현되는 할당량인 <xref:System.ServiceModel.Channels.TransportBindingElement.MaxReceivedMessageSize%2A?displayProperty=nameWithType>는 악의적인 클라이언트가 메모리를 과도하게 사용하여 서비스에 대한 서비스 거부 공격을 하지 못하도록 기본적으로 65,536바이트로 설정됩니다. 일반적으로 이 값을 낮추면 성능이 향상됩니다.

 serialization 할당량의 예로는 <xref:System.Runtime.Serialization.DataContractSerializer.MaxItemsInObjectGraph%2A?displayProperty=nameWithType> 속성이 있으며, 이 속성은 serializer가 단일 <xref:System.Runtime.Serialization.DataContractSerializer.ReadObject%2A> 메서드 호출에서 serialize하거나 deserialize하는 최대 개체 수를 지정합니다. 애플리케이션 수준 스로틀의 예로는 <xref:System.ServiceModel.Dispatcher.ServiceThrottle.MaxConcurrentSessions%2A?displayProperty=nameWithType> 속성이 있으며, 기본적으로 이 속성은 동시 세션 채널 연결의 수를 10으로 제한합니다. 할당량과 달리 스로틀 값에 도달하면 애플리케이션에서는 처리를 계속 수행하지만 새 세션 채널을 허용하지는 않습니다. 따라서 다른 세션 채널 중 하나가 종료될 때까지 새 클라이언트에 연결되지 않습니다.

 이러한 제어는 특정 유형의 공격에 대해 즉각적인 완화를 제공하거나 메모리 사용 공간, 시작 시간 등과 같은 성능 메트릭을 향상하기 위해 디자인되었습니다. 그러나 애플리케이션에 따라 이러한 제어로 인해 서비스 애플리케이션 성능이 저하되거나 애플리케이션이 전혀 작동하지 않을 수 있습니다. 예를 들어, 비디오 스트리밍을 위해 개발된 애플리케이션은 기본 <xref:System.ServiceModel.Channels.TransportBindingElement.MaxReceivedMessageSize%2A?displayProperty=nameWithType> 속성을 쉽게 초과할 수 있습니다. 이 항목에서는 다양 한 컨트롤 개요 WCF의 모든 수준에서 응용 프로그램에 적용, 설정을 응용 프로그램을 방해 하는 여부에 대 한 자세한 정보를 가져오는 다양 한 방법에 설명 합니다. 다양 한 문제를 해결 하는 방법에 설명 합니다. 기본 속성이 serialization이나 전송 제약 조건이더라도 애플리케이션 수준에서 대부분의 스로틀 및 일부 할당량을 사용할 수 있습니다. 예를 들어, 서비스 클래스의 <xref:System.Runtime.Serialization.DataContractSerializer.MaxItemsInObjectGraph%2A?displayProperty=nameWithType> 속성을 사용하여 <xref:System.ServiceModel.ServiceBehaviorAttribute.MaxItemsInObjectGraph%2A?displayProperty=nameWithType> 속성을 설정할 수 있습니다.

> [!NOTE]
> 먼저 읽어야 하는 경우 특정 문제를가 합니다 [WCF 문제 해결 퀵 스타트](../../../docs/framework/wcf/wcf-troubleshooting-quickstart.md) 문제 (및 솔루션)을 있습니다 나열 되어 있는지 여부를 확인 합니다.

 Serialization 프로세스를 제한 하는 속성에 나와 [데이터에 대 한 보안 고려 사항](../../../docs/framework/wcf/feature-details/security-considerations-for-data.md)합니다. 전송과 관련 된 리소스의 소비를 제한 하는 속성에 나와 [전송 할당량](../../../docs/framework/wcf/feature-details/transport-quotas.md)합니다. 애플리케이션 계층에서 리소스 사용을 제한하는 속성은 <xref:System.ServiceModel.Dispatcher.ServiceThrottle> 클래스의 멤버입니다.

## <a name="detecting-application-and-performance-issues-related-to-quota-settings"></a>할당량 설정과 관련된 애플리케이션 및 성능 문제 검색
 일반적인 보안 문제에 대해 기본 보호를 제공하면서 다양한 종류의 애플리케이션에서 기본 애플리케이션 기능을 사용할 수 있도록 이전 기본값이 선택되어 있습니다. 그러나 애플리케이션이 안전하고 개발된 대로 작동하더라도 다른 애플리케이션 디자인에서 하나 이상의 스로틀 설정을 초과할 수 있습니다. 이러한 경우 어떤 수준에서 어떤 스로틀 값이 초과되었는지 식별하여 애플리케이션 처리량을 늘리기 위해 수행할 적합한 작업을 결정해야 합니다.

 일반적으로 애플리케이션을 작성하고 이를 디버깅할 때 구성 파일에서 또는 프로그래밍 방식으로 <xref:System.ServiceModel.Description.ServiceDebugBehavior.IncludeExceptionDetailInFaults%2A?displayProperty=nameWithType> 속성을 `true`로 설정합니다. 이렇게 하면 WCF 서비스 예외 스택 추적 보기에 대 한 클라이언트 응용 프로그램에 반환 합니다. 이 기능은 관련이 있을 수 있는 할당량 설정을 표시하는 방식으로(이 설정이 문제인 경우) 대부분의 애플리케이션 수준 예외를 보고합니다.

 일부 예외는 런타임에 애플리케이션 계층의 표시 범위 아래에서 발생하고, 이 메커니즘을 사용하여 반환되지 않으며, 사용자 지정 <xref:System.ServiceModel.Dispatcher.IErrorHandler?displayProperty=nameWithType> 구현에 의해 처리될 수 없습니다. Microsoft Visual Studio와 같은 개발 환경을 사용하는 경우 이러한 예외의 대부분이 자동으로 표시됩니다. 그러나와 같은 개발 환경 설정에 따라 몇 가지 예외를 마스크 될 수 있습니다 [Just My Code](/visualstudio/debugger/just-my-code) Visual Studio입니다.

 개발 환경의 기능에 관계 없이 모든 예외를 디버깅 및 응용 프로그램의 성능 튜닝에 WCF 추적 및 메시지 로깅 기능을 사용할 수 있습니다. 자세한 내용은 [추적 응용 프로그램 문제 해결을 사용 하 여](../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)입니다.

## <a name="performance-issues-and-xmlserializer"></a>성능 문제 및 XmlSerializer
 <xref:System.Xml.Serialization.XmlSerializer>를 사용하여 serialize할 수 있는 데이터 형식을 사용하는 서비스 및 클라이언트 애플리케이션은 런타임에 해당 데이터 형식에 대한 serialization 코드를 생성하고 컴파일합니다. 이로 인해 시작 시 성능이 저하될 수 있습니다.

> [!NOTE]
> 미리 생성된 serialization 코드는 서비스가 아닌 클라이언트 애플리케이션에서만 사용될 수 있습니다.

 합니다 [ServiceModel Metadata 유틸리티 도구 (Svcutil.exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 응용 프로그램에 대 한 컴파일된 어셈블리 로부터 필요한 serialization 코드를 생성 하 여 이러한 응용 프로그램의 시작 성능을 향상 시킬 수 있습니다. 자세한 내용은 [방법: 시작 시간의 WCF 클라이언트 응용 프로그램 개선 XmlSerializer를 사용 하 여](../../../docs/framework/wcf/feature-details/startup-time-of-wcf-client-applications-using-the-xmlserializer.md)입니다.

## <a name="performance-issues-when-hosting-wcf-services-under-aspnet"></a>WCF 서비스를 ASP.NET 호스팅할 때의 성능 문제
 WCF 서비스를 IIS 및 ASP.NET에 호스팅하는 경우 IIS 및 ASP.NET의 구성 설정이 WCF 서비스의 처리량 및 메모리 사용 공간에 영향을 줄 수 있습니다.  ASP.NET 성능에 대 한 자세한 내용은 참조 하세요. [ASP.NET 성능 향상](https://go.microsoft.com/fwlink/?LinkId=186462)합니다.  예상치 않은 결과를 일으킬 수 있는 설정 중 하나는 <xref:System.Web.Configuration.ProcessModelSection.MinWorkerThreads%2A>의 속성인 <xref:System.Web.Configuration.ProcessModelSection>입니다. 애플리케이션의 클라이언트 수가 고정되어 있거나 적은 경우 <xref:System.Web.Configuration.ProcessModelSection.MinWorkerThreads%2A>를 2로 설정하면 다중 프로세서 컴퓨터에서 처리량이 크게 높아져 CPU 사용률이 100%에 가깝게 됩니다. 이러한 성능 증가는 비용을 초래합니다. 또한 메모리 사용량도 증가하여 확장성이 저하됩니다.

## <a name="see-also"></a>참고자료

- [관리 및 진단](../../../docs/framework/wcf/diagnostics/index.md)
- [큰 데이터 및 스트리밍](../../../docs/framework/wcf/feature-details/large-data-and-streaming.md)
