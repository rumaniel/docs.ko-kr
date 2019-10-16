---
title: <diagnostics>
ms.date: 03/30/2017
ms.assetid: 0c2f95c4-cc12-4fb5-a70c-7fc6fa95db58
ms.openlocfilehash: 2749bc6c66d491a8a160d98b508fb43aa027b806
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70398047"
---
# <a name="diagnostics"></a>\<diagnostics>
`diagnostics` 요소는 관리자가 런타임 검사 및 제어에 사용할 수 있는 설정을 정의합니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.servicemodel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<진단 >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<system.serviceModel>
  <diagnostics etwProviderId="String"
               performanceCounters="Off/ServiceOnly/All/Default"
               wmiProviderEnabled="Boolean">
    <endToEndTracing activityTracing="Boolean"
                     messageFlowTracing="Boolean"
                     propagateActivity="Boolean" />
    <messageLogging logEntireMessage="Boolean"
                    logMalformedMessages="Boolean"
                    logMessagesAtServiceLevel="Boolean"
                    logMessagesAtTransportLevel="Boolean"
                    maxMessagesToLog="Integer"
                    maxSizeOfMessageToLog="Integer">
      <filters>
        <clear />
      </filters>
    </messageLogging>
  </diagnostics>
</system.serviceModel>
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|etwProviderId|ETW 세션에 이벤트를 기록하는 이벤트 추적 공급자에 대한 식별자를 지정하는 문자열입니다.|  
|performanceCounters|어셈블리에 대해 성능 카운터를 사용할 수 있는지 여부를 지정합니다. 유효한 값은 다음과 같습니다.<br /><br /> 해제 성능 카운터를 사용하지 않습니다.<br />ServiceOnly 이 서비스와 관련된 성능 카운터만 사용합니다.<br />모두가 성능 카운터를 런타임에 볼 수 있습니다.<br />기본 단일 성능 카운터 인스턴스 _WCF_Admin이 만들어집니다. 이 인스턴스는 인프라에서 사용되는 SQM 데이터 컬렉션을 설정하는 데 사용됩니다. 이 인스턴스의 어떤 카운터 값도 업데이트되지 않으므로 0으로 남게 됩니다. 이것은 WCF에 대한 구성이 없을 경우 기본값입니다.|  
|wmiProviderEnabled|어셈블리에 대해 WMI 공급자를 사용할 수 있는지 여부를 지정하는 부울 값입니다. 사용자가 WCF(Windows Communication Foundation)의 검사 및 제어 기능에 대해 런타임 액세스 권한을 얻으려면 WMI 공급자가 필요합니다. 기본값은 `false`입니다.|  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<endToEndTracing>](endtoendtracing.md)|서비스 애플리케이션 실행 중에 엔드투엔드 추적의 다양한 측면을 사용하거나 사용하지 않도록 설정할 수 있는 구성 요소입니다.|  
|[\<messageLogging>](messagelogging.md)|WCF 메시지 로깅의 설정을 설명합니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|serviceModel|모든 WCF 구성 요소의 루트 요소입니다.|  
  
## <a name="remarks"></a>설명  
 `diagnostics` 섹션에서는 어셈블리에 있는 모든 서비스의 진단 설정을 정의합니다. 어셈블리에 서비스가 하나만 있는 경우가 아니라면 서비스 수준에서 별도의 진단 설정을 정의할 수 없습니다. 해당 섹션의 요구 사항에 따라 특성이 설정됩니다.  
  
## <a name="example"></a>예제  
  
```xml  
<diagnostics wmiProviderEnabled="false"
             performanceCounters="all">
  <messageLogging logEntireMessage="true"
                  logMalformedMessages="true"
                  logMessagesAtServiceLevel="true"
                  logMessagesAtTransportLevel="true"
                  maxMessagesToLog="42"
                  maxSizeOfMessageToLog="42">
    <filters>
      <clear />
    </filters>
  </messageLogging>
</diagnostics>
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Configuration.DiagnosticSection>
- <xref:System.ServiceModel.Diagnostics>
