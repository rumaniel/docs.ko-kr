---
title: 메시지 필터
ms.date: 03/30/2017
helpviewer_keywords:
- routing [WCF], message filters
ms.assetid: cb33ba49-8b1f-4099-8acb-240404a46d9a
ms.openlocfilehash: b8de58b6935ee59fc8c787dfcf7445afcd0774b9
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69912695"
---
# <a name="message-filters"></a>메시지 필터
라우팅 서비스는 내용 기반 라우팅을 구현하기 위해 주소, 엔드포인트 이름 또는 특정 XPath 문과 같은 메시지의 특정 섹션을 검사하는 <xref:System.ServiceModel.Dispatcher.MessageFilter> 구현을 사용합니다. [!INCLUDE[netfx_current_short](../../../../includes/netfx-current-short-md.md)]에 제공되는 메시지 필터 중 요구 사항을 충족하는 필터가 없는 경우 기본 <xref:System.ServiceModel.Dispatcher.MessageFilter> 클래스의 새 구현을 만드는 방법으로 사용자 지정 필터를 만들 수 있습니다.  
  
 라우팅 서비스를 구성할 때 메시지 내에서 검색할 특정 문자열 값<xref:System.ServiceModel.Routing.Configuration.FilterElement> 과 같이 필터를 만드는 데 필요한 지원 데이터 및 **messagefilter** 의 형식을 설명 하는 필터 요소 (개체)를 정의 해야 합니다. . 필터 요소를 만들 경우 개별 메시지 필터만 정의됩니다. 필터를 사용하여 메시지를 평가 및 라우트하려면 필터 테이블(<xref:System.ServiceModel.Routing.Configuration.FilterTableEntryCollection>)도 만들어야 합니다.  
  
 필터 테이블의 각 항목은 필터 요소를 참조하며 메시지가 필터와 일치할 경우 메시지가 라우트될 클라이언트 엔드포인트를 지정합니다. 또한 필터 테이블 항목을 통해 백업 엔드포인트 컬렉션(<xref:System.ServiceModel.Routing.Configuration.BackupEndpointCollection>)을 지정할 수 있습니다. 여기에는 기본 엔드포인트로 보내는 중 전송 오류가 발생할 경우 메시지를 전송할 엔드포인트 목록이 정의됩니다. 전송이 성공하는 엔드포인트가 나올 때까지 여기에 지정된 엔드포인트에 대해 순서대로 전송이 시도됩니다.  
  
## <a name="message-filters"></a>메시지 필터  
 라우팅 서비스에 사용되는 메시지 필터는 SOAP 동작, 메시지가 전송된 주소나 주소 접두사 또는 메시지를 보내는 엔드포인트 이름 평가와 같은 일반적인 메시지 선택 기능을 제공합니다. 또한 필터를 `AND` 조건과 결합하면 메시지가 두 필터에 모두 일치하는 경우에만 엔드포인트에 라우트되도록 할 수 있습니다. 사용자 고유의 <xref:System.ServiceModel.Dispatcher.MessageFilter> 구현을 만들어 사용자 지정 필터를 만들 수도 있습니다.  
  
 다음 표에서는 라우팅 서비스에 사용되는 <xref:System.ServiceModel.Routing.Configuration.FilterType>, 특정 메시지 필터를 구현하는 클래스 및 필수 <xref:System.ServiceModel.Routing.Configuration.FilterElement.FilterData%2A> 매개 변수를 보여 줍니다.  
  
|필터 형식|설명|필터 데이터 의미|예제 필터|  
|------------------|-----------------|-------------------------|--------------------|  
|동작|<xref:System.ServiceModel.Dispatcher.ActionMessageFilter> 클래스를 사용하여 특정 작업이 포함된 메시지를 일치시킵니다.|필터링할 작업입니다.|\<filter name="action1" filterType="Action" filterData="http://namespace/contract/operation" />|  
|EndpointAddress|<xref:System.ServiceModel.Dispatcher.EndpointAddressMessageFilter> 는 클래스 <xref:System.ServiceModel.Dispatcher.EndpointAddressMessageFilter.IncludeHostNameInComparison%2A> 를사용하여특정주소를포함하는메시지를일치시킵니다. ==  `true`|To 헤더의 필터링할 주소입니다.|\<filter name="address1" filterType="EndpointAddress" filterData="http://host/vdir/s.svc/b"  />|  
|EndpointAddressPrefix|<xref:System.ServiceModel.Dispatcher.PrefixEndpointAddressMessageFilter> 는 클래스 <xref:System.ServiceModel.Dispatcher.PrefixEndpointAddressMessageFilter.IncludeHostNameInComparison%2A> 를사용하여특정주소접두사를포함하는메시지를일치시킵니다. ==  `true`|가장 긴 접두사 일치를 사용하여 필터링을 적용할 주소입니다.|\<filter name="prefix1" filterType="EndpointAddressPrefix" filterData="http://host/" />|  
|And|반환 전에 항상 두 조건을 모두 평가하는 <xref:System.ServiceModel.Dispatcher.StrictAndMessageFilter> 클래스를 사용합니다.|filterData는 사용 되지 않습니다. 대신 filter1 및 filter2에는 해당 메시지 필터의 이름 (테이블에도 포함)이 포함 되어 **있고**함께 사용할 수 있습니다.|\<filter name="and1" filterType="And" filter1="address1" filter2="action1" />|  
|사용자 지정|<xref:System.ServiceModel.Dispatcher.MessageFilter> 클래스를 확장하고 문자열을 사용하는 생성자를 포함하는 사용자 정의 형식입니다.|customType 특성은 만들 클래스의 정규화된 형식 이름입니다. filterData는 필터를 만들 때 생성자에 전달할 문자열입니다.|\<filter name="custom1" filterType="Custom" customType="CustomAssembly.CustomMsgFilter, CustomAssembly" filterData="Custom Data" />|  
|EndpointName|<xref:System.ServiceModel.Dispatcher.EndpointNameMessageFilter> 클래스를 사용하여 메시지가 도착하는 서비스 엔드포인트의 이름을 기반으로 메시지를 일치시킵니다.|서비스 끝점의 이름 예: "serviceEndpoint1"입니다.  이는 라우팅 서비스에서 노출되는 엔드포인트 중 하나여야 합니다.|\<filter name="stock1" filterType="Endpoint" filterData="SvcEndpoint" />|  
|MatchAll|<xref:System.ServiceModel.Dispatcher.MatchAllMessageFilter> 클래스를 사용합니다. 이 필터는 도착하는 메시지를 모두 일치시킵니다.|filterData는 사용되지 않습니다. 이 필터는 항상 모든 메시지를 일치시킵니다.|\<filter name="matchAll1" filterType="MatchAll" />|  
|XPath|<xref:System.ServiceModel.Dispatcher.XPathMessageFilter> 클래스를 사용하여 메시지 내의 특정 XPath 쿼리를 일치시킵니다.|메시지를 대조할 때 사용하는 XPath 쿼리입니다.|\<필터 이름 = "XPath1" filterType "XPath" filterData = = "//ns:element" / >|  
  
 다음 예제에서는 XPath, EndpointName 및 PrefixEndpointAddress 메시지 필터를 사용하는 필터 항목을 정의합니다. 이 예제에서는 RoundRobinFilter1 및 RoundRobinFilter2 항목에 대해 사용자 지정 필터를 사용하는 방법도 보여 줍니다.  
  
```xml  
<filters>  
     <filter name="XPathFilter" filterType="XPath"   
             filterData="/s12:Envelope/s12:Header/custom:RoundingCalculator = 1"/>  
     <filter name="EndpointNameFilter" filterType="EndpointName"   
             filterData="calculatorEndpoint"/>  
     <filter name="PrefixAddressFilter" filterType="PrefixEndpointAddress"   
             filterData="http://localhost/routingservice/router/rounding/"/>  
     <filter name="RoundRobinFilter1" filterType="Custom"   
             customType="RoutingServiceFilters.RoundRobinMessageFilter,   
             RoutingService" filterData="group1"/>  
     <filter name="RoundRobinFilter2" filterType="Custom"   
             customType="RoutingServiceFilters.RoundRobinMessageFilter,   
             RoutingService" filterData="group1"/>  
</filters>  
```  
  
> [!NOTE]
> 단순히 필터를 정의하는 것만으로는 메시지에 필터가 적용되지 않습니다. 필터는 필터 테이블에 추가되어야 하며, 그러면 필터 테이블은 라우팅 서비스에 의해 노출되는 서비스 엔드포인트와 연결됩니다.  
  
### <a name="namespace-table"></a>네임스페이스 테이블  
 XPath 필터를 사용할 때 XPath 쿼리가 포함된 필터 데이터는 네임스페이스 사용으로 인해 그 크기가 상당히 커질 수 있습니다. 이 문제를 완화하기 위해 라우팅 서비스는 네임스페이스 테이블을 사용하여 사용자 고유의 네임스페이스 접두사를 정의할 수 있는 기능을 제공합니다.  
  
 네임스페이스 테이블은 XPath에 사용 가능한 공통 네임스페이스를 위한 네임스페이스 접두사를 정의하는 <xref:System.ServiceModel.Routing.Configuration.NamespaceElement> 개체 컬렉션입니다. 다음은 네임스페이스 테이블에 포함된 기본 네임스페이스 및 네임스페이스 접두사입니다.  
  
|접두사|네임스페이스|  
|------------|---------------|  
|s11|`http://schemas.xmlsoap.org/soap/envelope`|  
|s12|`http://www.w3.org/2003/05/soap-envelope`|  
|wsaAugust2004|`http://schemas.xmlsoap.org/ws/2004/08/addressing`|  
|wsa10|`http://www.w3.org/2005/08/addressing`|  
|sm|`http://schemas.microsoft.com/serviceModel/2004/05/xpathfunctions`|  
|tempuri|`http://tempuri.org`|  
|ser|`http://schemas.microsoft.com/2003/10/Serialization`|  
  
 XPath 쿼리에서 특정 네임스페이스를 사용할 예정인 경우 이를 고유한 네임스페이스 접두사와 함께 네임스페이스 테이블에 추가하면 모든 XPath 쿼리에서 전체 네임스페이스 대신 이 접두사를 사용할 수 있습니다. 다음 예에서는 네임 스페이스 `"http://my.custom.namespace"`에 대 한 "custom" 접두사를 정의 합니다 .이 접두사는 filterdata에 포함 된 XPath 쿼리에서 사용 됩니다.  
  
```xml  
<namespaceTable>  
     <add prefix="custom" namespace="http://my.custom.namespace/"/>  
</namespaceTable>  
<filters>  
     <filter name="XPathFilter" filterType="XPath" filterData="/s12:Envelope/s12:Header/custom:RoundingCalculator = 1"/>  
</filters>  
```  
  
## <a name="filter-tables"></a>필터 테이블  
 각 필터 요소는 메시지에 적용할 수 있는 논리 비교를 정의하며 필터 테이블은 필터 요소와 대상 클라이언트 엔드포인트 간의 연결을 제공합니다. 필터 테이블은 필터, 기본 대상 엔드포인트 및 대체 백업 엔드포인트 목록 간의 연결을 정의하는 명명된 <xref:System.ServiceModel.Routing.Configuration.FilterTableEntryElement> 개체 컬렉션입니다. 또한 필터 테이블 항목을 통해 각 필터 조건에 대해 선택적인 우선 순위를 지정할 수 있습니다. 다음 예제에서는 두 가지 필터를 정의한 다음 각 필터를 대상 엔드포인트와 연결하는 필터 테이블을 정의합니다.  
  
```xml  
<routing>  
     <filters>  
       <filter name="AddAction" filterType="Action" filterData="Add" />  
       <filter name="SubtractAction" filterType="Action" filterData="Subtract" />  
     </filters>  
     <filterTables>  
       <table name="routingTable1">  
         <filters>  
           <add filterName="AddAction" endpointName="Addition" />  
           <add filterName="SubtractAction" endpointName="Subtraction" />  
         </filters>  
       </table>  
     </filterTables>      
</routing>  
```  
  
### <a name="filter-evaluation-priority"></a>필터 평가 우선 순위  
 기본적으로 필터 테이블의 모든 항목은 동시에 평가되며, 평가되는 메시지는 일치하는 각 필터 항목에 연결된 엔드포인트로 라우트됩니다. 여러 필터가 `true`를 반환하고 메시지가 단방향 또는 이중인 경우 메시지는 일치하는 모든 필터에 대한 엔드포인트로 멀티캐스트됩니다. 요청-회신 메시지의 경우 클라이언트에 하나의 회신만 반환할 수 있으므로 멀티캐스트될 수 없습니다.  
  
 각 필터에 우선 순위를 지정하면 더 복잡한 라우팅 논리를 구현할 수 있습니다. 라우팅 서비스는 가장 우선 순위가 높은 필터부터 시작하여 모든 필터를 평가합니다. 메시지가 이 수준의 필터와 일치할 경우 우선 순위가 더 아래인 필터는 처리되지 않습니다. 예를 들어 들어오는 단방향 메시지는 먼저 우선 순위가 2인 모든 필터를 기준으로 평가됩니다. 이 우선 순위에서 메시지와 일치하는 필터가 없으므로 그 다음으로 우선 순위가 1인 필터와 메시지가 비교됩니다. 두 개의 우선 순위 1 필터가 메시지와 일치하며, 메시지가 단방향 메시지이므로 두 대상 엔드포인트 모두로 라우트됩니다.  우선 순위 1 필터 중에서 일치가 발견되었으므로 우선 순위가 0인 필터는 평가되지 않습니다.  
  
> [!NOTE]
> 우선 순위가 지정되지 않으면 기본 우선 순위인 0이 사용됩니다.  
  
 다음 예제에서는 테이블에서 참조되는 필터에 대해 우선 순위 2, 1 및 0을 지정하는 필터 테이블을 정의합니다.  
  
```xml  
<filterTables>  
     <filterTable name="filterTable1">  
          <add filterName="XPathFilter" endpointName="roundingCalcEndpoint"   
               priority="2"/>  
          <add filterName="EndpointNameFilter" endpointName="regularCalcEndpoint"   
               priority="1"/>  
          <add filterName="PrefixAddressFilter" endpointName="roundingCalcEndpoint"   
               priority="1"/>  
          <add filterName="MatchAllMessageFilter" endpointName="defaultCalcEndpoint"   
               priority="0"/>  
     </filterTable>  
</filterTables>  
```  
  
 앞의 예제에서 메시지가 XPathFilter와 일치할 경우 roundingCalcEndpoint로 라우트되며, 테이블의 다른 모든 필터는 우선 순위가 더 낮으므로 더 이상 평가되지 않습니다. 그러나 메시지가 XPathFilter와 일치하지 않는 경우 그 다음 우선 순위의 모든 필터(EndpointNameFilter 및 PrefixAddressFilter)를 기준으로 평가됩니다.  
  
> [!NOTE]
> 우선 순위 평가로 인해 성능이 저하될 수 있으므로 가능한 경우 우선 순위를 지정하는 대신 단독 필터를 사용하세요.  
  
### <a name="backup-lists"></a>백업 목록  
 필터 테이블의 각 필터는 선택적으로 백업 목록을 지정할 수 있습니다. 백업 목록은 명명된 엔드포인트 컬렉션입니다(<xref:System.ServiceModel.Routing.Configuration.BackupEndpointCollection>). 이 컬렉션에는 <xref:System.ServiceModel.CommunicationException>에 지정된 기본 엔드포인트로 보낼 때 <xref:System.ServiceModel.Routing.Configuration.FilterTableEntryElement.EndpointName%2A>이 발생하는 경우 메시지를 전송할 엔드포인트가 순서대로 나열된 목록이 포함됩니다. 다음 예에서는 두 개의 끝점이 포함 된 "backupServiceEndpoints" 라는 백업 목록을 정의 합니다.  
  
```xml  
<filterTables>  
     <filterTable name="filterTable1">  
          <add filterName="MatchAllFilter1" endpointName="Destination" backupList="backupEndpointList"/>  
     </filterTable>  
</filterTables>  
<backupLists>  
     <backupList name="backupEndpointList">  
          <add endpointName="backupServiceQueue" />  
          <add endpointName="alternateServiceQueue" />  
     </backupList>  
</backupLists>  
```  
  
 앞의 예제에서 기본 끝점 "대상"에 대 한 송신이 실패 하면 라우팅 서비스는 나열 된 시퀀스에서 각 끝점에 대 한 전송을 시도 하 고, 먼저 backupServiceQueue로 보낸 다음, alternateServiceQueue에 게 보냅니다. backupServiceQueue에 보내기가 실패 합니다. 모든 백업 엔드포인트가 실패할 경우 오류가 반환됩니다.
