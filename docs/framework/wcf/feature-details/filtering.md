---
title: 필터링
ms.date: 03/30/2017
ms.assetid: 4002946c-e34a-4356-8cfb-e25912a4be63
ms.openlocfilehash: 46716d1a96da6ddc729992b546be56c2aec0bf5d
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64593498"
---
# <a name="filtering"></a>필터링
Windows Communication Foundation (WCF) 필터링 시스템 선언적 필터를 사용 메시지를 일치 시키고 운영 결정을 내릴 수 있습니다. 필터를 사용하여 메시지 일부를 검사하고 메시지를 통해 수행할 작업을 결정할 수 있습니다. 예를 들어, 큐 프로세스에서는 XPath 1.0 쿼리를 사용하여 알려진 헤더의 우선 순위 요소를 검사함으로써 메시지를 큐의 앞으로 이동할지 여부를 결정할 수 있습니다.  
  
 필터링 시스템은 효율적으로 수행할 수 있는 클래스의 집합으로 구성 되는 필터 집합을 결정 `true` 특정 WCF 메시지에 대 한 합니다.  
  
 필터링 시스템은 WCF 메시징;의 핵심 구성 요소 초고속 되도록 설계 되었습니다. 각 필터 구현은 특정 종류의 일치 하는 WCF 메시지에 대해 최적화 되었습니다.  
  
 필터링 시스템은 스레드로부터 안전하지 않습니다. 애플리케이션은 모든 잠금 의미 체계를 처리해야 합니다. 그러나 다중 판독기, 단일 작성기를 지원합니다.  
  
## <a name="where-filtering-fits"></a>필터링이 적용되는 위치  
 메시지를 수신하고 메시지를 적절한 애플리케이션 구성 요소에 발송하는 프로세스의 일부인 경우 필터링이 수행됩니다. 필터링 시스템의 디자인에는 메시징, 라우팅, 보안, 이벤트 처리 및 시스템 관리를 포함 하 여, 여러 WCF 하위 시스템의 요구 사항을 해결 합니다.  
  
## <a name="filters"></a>필터  
 필터 엔진에는 두 가지 기본 구성 요소 즉, 필터와 필터 테이블이 있습니다. 필터는 사용자 지정 논리 조건에 기반한 메시지에 대해 부울을 결정합니다. 필터는 <xref:System.ServiceModel.Dispatcher.MessageFilter> 클래스를 구현합니다.  
  
 <xref:System.ServiceModel.Dispatcher.MessageFilter.Match%2A> 메서드는 메시지가 필터를 충족하는지 확인하는 데 사용됩니다. 메서드 중 하나가 메시지의 헤더를 테스트하지만 메시지 본문은 검사할 수 없습니다. 다른 메서드를 *메시지 버퍼* 입력된 매개 변수로 및 메시지 본문을 검사할 수 있습니다.  
  
 필터는 보통 개별적으로 테스트되지 않고, <xref:System.ServiceModel.Dispatcher.MessageFilterTable%601.CreateFilterTable%2A> 메서드가 만드는 제네릭 클래스인 필터 테이블의 일부로 테스트됩니다.  
  
 여러 종류의 필터마다 특정 유형의 부울 조건에 대해 일치하도록 특수화됩니다. 필터를 일단 생성하고 나면 필터가 사용하는 기준을 변경할 수 없습니다. 필터 기준을 수정하려면 새 필터를 생성하고 기존 필터를 삭제합니다.  
  
### <a name="action-filters"></a>작업 필터  
 <xref:System.ServiceModel.Dispatcher.ActionMessageFilter>에는 작업 문자열 목록이 포함되어 있습니다. 필터 목록의 작업이 메시지 또는 메시지 버퍼의 작업 헤더와 일치하는 경우 `Match` 메서드는 `true`를 반환합니다. 목록이 비어 있는 경우 필터는 모두 일치하는 필터로 간주되고 모든 메시지 또는 메시지 버퍼가 일치하며 `Match`는 `true`를 반환합니다. 필터 목록의 작업이 메시지 또는 메시지 버퍼의 작업 헤더와 일치하지 않는 경우 `Match`는 `false`를 반환합니다. 메시지에 작업이 없고 필터 목록이 비어 있지 않은 경우 `Match`는 `false`를 반환합니다.  
  
### <a name="endpoint-address-filters"></a>엔드포인트 주소 필터  
 <xref:System.ServiceModel.Dispatcher.EndpointAddressMessageFilter>는 헤더 컬렉션에 표시된 대로 엔드포인트 주소를 기준으로 메시지 및 메시지 버퍼를 필터링합니다. 메시지가 이러한 필터를 통과하려면 다음 조건을 충족해야 합니다.  
  
- 필터 주소 URI(Uniform Resource Identifier)가 메시지 받는 사람 헤더의 URI와 동일해야 합니다.  
  
- 필터 주소의 각 엔드포인트 매개 변수(`address.Headers` 컬렉션)가 매핑할 메시지에서 헤더를 찾아야 합니다. 메시지 또는 메시지 버퍼의 추가 헤더는 `true`를 유지하기 위해 일치에 사용할 수 있습니다.  
  
### <a name="prefix-endpoint-address-filters"></a>접두사 엔드포인트 주소 필터  
  
1. <xref:System.ServiceModel.Dispatcher.PrefixEndpointAddressMessageFilter>는 메시지 URI의 접두사에 위치할 수 있는 일치를 제외하고 <xref:System.ServiceModel.Dispatcher.EndpointAddressMessageFilter> 필터와 동일하게 작동합니다. 예를 들어 주소를 지정 하는 필터 `http://www.adatum.com` 주소가 지정 된 메시지를 일치 `http://www.adatum.com/userA`합니다.  
  
### <a name="xpath-message-filters"></a>XPath 메시지 필터  
 <xref:System.ServiceModel.Dispatcher.XPathMessageFilter>는 XPath 식을 사용하여 XML 문서에 특정 요소, 특성, 텍스트 또는 기타 XML 구문을 포함할지 여부를 결정합니다. 필터는 엄격한 XPath의 하위 집합에 대해 매우 효율적으로 최적화됩니다. XML 경로 언어에 설명 되어는 [W3C XML Path Language 1.0 사양](https://go.microsoft.com/fwlink/?LinkId=94779)합니다.  
  
 일반적으로 애플리케이션은 엔드포인트에서 <xref:System.ServiceModel.Dispatcher.XPathMessageFilter>를 사용하여 SOAP 메시지의 내용을 퀴리한 다음 해당 쿼리의 결과를 기준으로 적절한 작업을 수행합니다. 예를 들어, 큐 프로세스에서는 XPath 쿼리를 사용하여 알려진 헤더의 우선 순위 요소를 검사함으로써 메시지를 큐 앞으로 이동할지 여부를 결정할 수 있습니다.  
  
## <a name="filter-tables"></a>필터 테이블  
 필터 테이블은 키-값 쌍을 저장하는 데 사용되며 여기서 필터는 키이고 일부 관련 데이터가 값입니다. 필터 데이터는 메시지가 필터와 일치하고 필터 데이터의 유형이 필터 테이블 클래스의 일반 매개 변수인 경우 수행할 작업을 표시하는 데 사용할 수 있습니다. 필터 데이터는 라우팅 규칙, 세션 보안 상태, 채널 상의 수신기 등으로 구성할 수 있습니다. 데이터는 데이터 흐름 제어가 필요한 경우 사용할 수 있습니다.  
  
 필터 테이블은 제네릭 인터페이스 <xref:System.ServiceModel.Dispatcher.IMessageFilterTable%601>을 구현합니다.  
  
 필터 테이블에는 테이블의 모든 필터에 대한 메시지와 일치하고 일치하는 필터 또는 데이터의 순서 지정이 없는 컬렉션을 반환하는 여러 메서드가 있습니다. 일부 일치 메서드는 다중 일치이며 일치하는 모든 항목을 반환합니다. 다른 메서드는 하나의 항목만 반환하는 단일 일치이며 필터가 두 개 이상 일치할 경우 <xref:System.ServiceModel.Dispatcher.MultipleFilterMatchesException>을 throw합니다.  
  
### <a name="message-filter-table"></a>메시지 필터 테이블  
 <xref:System.ServiceModel.Dispatcher.MessageFilterTable%601>은 <xref:System.ServiceModel.Dispatcher.IMessageFilterTable%601>의 가장 일반적인 구현입니다. 테이블에 모든 형식의 필터를 저장할 수 있습니다.  
  
 숫자로 된 우선 순위를 필터에 할당할 수 있으며 가장 큰 숫자가 제일 높은 우선 순위입니다. 여러 형식의 필터가 동일한 우선 순위를 가질 수 있습니다. 특정 형식의 필터가 둘 이상의 우선 순위 수준으로 표시될 수 있습니다.  
  
 일치는 제일 높은 우선 순위부터 시작하여 수행되며 제공된 우선 순위와 일치하는 필터를 찾으면 하위 우선 순위를 가진 필터는 검사하지 않습니다. 따라서 단일 필터 일치 메서드를 사용하고 둘 이상의 필터가 메시지와 일치하지만 일치하는 각 필터의 우선 순위가 서로 다른 경우, 예외가 throw되지 않고 가장 높은 순위를 가진 필터가 반환됩니다. 마찬가지로 다중 필터 일치 메서드는 가장 높은 순위를 가진 필터와 일치하는 필터만 반환합니다.  
  
### <a name="xpath-message-filter-table"></a>XPath 메시지 필터 테이블  
 <xref:System.ServiceModel.Dispatcher.XPathMessageFilterTable%601>은 선언적 XPath 필터에 대해서 최적화되기 때문에 테이블 키가 <xref:System.ServiceModel.Dispatcher.XPathMessageFilter>입니다.  
  
 <xref:System.ServiceModel.Dispatcher.XPathMessageFilterTable%601> 클래스는 메시징 시나리오 대부분을 포함하는 XPath의 하위 집합에 대한 일치를 최적화하고, 전체 XPath 1.0 문법도 지원합니다. 효율적인 병렬 일치를 위한 알고리즘을 최적화합니다.  
  
 이 테이블에는 `Match` 및 <xref:System.Xml.XPath.XPathNavigator>를 통해 수행되는 여러 특수화된 <xref:System.ServiceModel.Dispatcher.SeekableXPathNavigator> 메서드가 있습니다. <xref:System.ServiceModel.Dispatcher.SeekableXPathNavigator>는 <xref:System.Xml.XPath.XPathNavigator> 속성을 추가하여 <xref:System.ServiceModel.Dispatcher.SeekableXPathNavigator.CurrentPosition%2A> 클래스를 확장합니다. 이 속성을 사용하면 XML 문서 내의 위치를 저장해 놓은 후 탐색기를 복제하지 않고 신속하게 로드할 수 있습니다. 이 작업을 <xref:System.Xml.XPath.XPathNavigator>에서 수행하려면 비용이 많이 드는 메모리 할당이 필요합니다. WCF XPath 엔진은 XML 문서에 대해 쿼리를 실행 하는 과정에서 커서의 위치를 자주 기록해 야 하므로 <xref:System.ServiceModel.Dispatcher.SeekableXPathNavigator> 메시지 처리에 대 한 중요 한 최적화를 제공 합니다.  
  
## <a name="customer-scenarios"></a>고객 시나리오  
 메시지에 포함된 데이터에 따라 메시지를 다른 프로세싱 모듈에 전송하려는 경우 언제든지 필터링을 사용할 수 있습니다. 두 가지 일반적인 시나리오는 동작 코드에 기반한 메시지 라우팅과 메시지 엔드포인트 주소에 기반한 메시지 스트림의 역 멀티플렉싱입니다.  
  
### <a name="routing"></a>라우팅  
 엔드포인트의 수신기는 메시지 SOAP 헤더에서 하나 이상의 동작 코드가 있는 메시지를 수신 대기합니다. 동작 코드가 들어 있는 배열을 생성자에게 전달하고 <xref:System.ServiceModel.Dispatcher.ActionMessageFilter>를 만들어 이를 구현합니다. 해당 필터를 사용하여 `ListenerFactory`에 등록하기 때문에 동작이 필터의 동작과 일치하는 메시지만 해당 특정 엔드포인트에 도달합니다.  
  
### <a name="de-multiplexing"></a>역 멀티플렉싱  
 여러 개의 엔드포인트가 동일한 `ServiceListener`에서 분리되어 연결이 끊어진 경우 메시지를 역 멀티플렉싱하고 특정 엔드포인트 주소에 속하는지 여부를 확인하는 유일한 방법은 <xref:System.ServiceModel.Dispatcher.EndpointAddressMessageFilter>를 사용하는 것입니다. 여기서 헤더에 저장된 정보를 조회하여 등록된 엔드포인트 쪽에 있는 메시지를 선택합니다. 이러한 필터의 경우 전달된 메시지에만 다음 두 가지 모두에 해당하는 필요한 모든 헤더가 포함됩니다.  
  
- `EndpointAddress`의 URI.  
  
- `EndpointAddress`에 지정된 대로 <xref:System.ServiceModel.Dispatcher.EndpointAddressMessageFilter>의 나머지 엔드포인트 매개 변수.  
  
## <a name="see-also"></a>참고자료

- [데이터 전송 및 Serialization](../../../../docs/framework/wcf/feature-details/data-transfer-and-serialization.md)
