---
title: 추적 및 디버그 설정 스키마
ms.date: 03/30/2017
helpviewer_keywords:
- tracing [.NET Framework], trace and debug settings schema
- configuration schema [.NET Framework], trace and debug settings
- configuration settings [.NET Framework], tracing
- schema configuration settings
- configuration settings [.NET Framework], debugging
- trace listeners, trace and debug settings schema
- configuration sections [.NET Framework]
- elements [.NET Framework], trace and debug settings
ms.assetid: 277ca5f6-e1c4-41b6-a47f-3a67ce5b94ac
ms.openlocfilehash: 037d08b33e9aa6a64d236b36ebcf821b604b03df
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69927128"
---
# <a name="trace-and-debug-settings-schema"></a>추적 및 디버그 설정 스키마
추적 및 디버그 설정은 메시지를 수집하고 저장하고 라우팅하는 추적 수신기를 지정하며, 추적 스위치가 설정되는 수준을 지정합니다.  
  
 다음 표는 각 추적 및 디버그 설정 요소의 기능을 설명합니다.  
  
|요소|설명|  
|-------------|-----------------|  
|[\<add>](add-element-for-listeners-for-source.md)|추적 소스의 `Listeners` 컬렉션에 수신기를 추가합니다.|  
|[\<add>](add-element-for-listeners-for-trace.md)|`Listeners` 컬렉션에 수신기를 추가합니다.|  
|[\<add>](add-element-for-sharedlisteners.md)|`sharedListeners` 컬렉션에 수신기를 추가합니다.|  
|[\<add>](add-element-for-switches.md)|추적 스위치를 설정하는 수준을 지정합니다.|  
|[\<assert>](assert-element.md)|<xref:System.Diagnostics.Debug.Assert%2A?displayProperty=nameWithType> 메서드를 호출할 때 메시지 상자를 표시할지 여부를 지정합니다. 또한 메시지를 작성할 파일의 이름도 지정합니다.|  
|[\<clear>](clear-element-for-listeners-for-source.md)|추적 소스의 `Listeners` 컬렉션을 지웁니다.|  
|[\<clear>](clear-element-for-listeners-for-trace.md)|추적의 `Listeners` 컬렉션을 지웁니다.|  
|[\<filter>](filter-element-for-add-for-listeners-for-source.md)|추적 소스의 `Listeners` 컬렉션에 있는 수신기에 필터를 추가합니다.|  
|[\<filter>](filter-element-for-add-for-listeners-for-trace.md)|추적의 `Listeners` 컬렉션에 있는 수신기에 필터를 추가합니다.|  
|[\<filter>](filter-element-for-add-for-sharedlisteners.md)|`sharedListeners` 컬렉션에 있는 수신기에 필터를 추가합니다.|  
|[\<listeners>](listeners-element-for-source.md)|추적 소스의 `Listeners` 컬렉션에 대한 수신기를 지정합니다.|  
|[\<listeners>](listeners-element-for-trace.md)|추적의 `Listeners` 컬렉션에 대한 수신기를 지정합니다.|  
|[\<performanceCounters>](performancecounters-element.md)|성능 카운터에서 공유하는 전역 메모리의 크기를 지정합니다.|  
|[\<remove>](remove-element-for-listeners-for-trace.md)|추적의 `Listeners` 컬렉션에서 수신기를 제거합니다.|  
|[\<remove>](remove-element-for-listeners-for-source.md)|추적 소스의 `Listeners` 컬렉션에서 수신기를 제거합니다.|  
|[\<sharedListeners>](sharedlisteners-element.md)|소스 또는 추적 요소가 참조할 수 있는 수신기가 포함되어 있습니다.|  
|[\<sources>](sources-element.md)|추적 메시지를 시작하는 추적 소스가 포함되어 있습니다.|  
|[\<source>](source-element.md)|추적 메시지를 시작하는 추적 소스를 지정합니다.|  
|[\<switches>](switches-element.md)|추적 스위치 및 추적 스위치가 설정된 수준이 포함되어 있습니다.|  
|[\<system.diagnostics>](system-diagnostics-element.md)|메시지를 수집하고 저장하고 라우팅하는 추적 수신기를 지정하며, 추적 스위치가 설정되는 수준을 지정합니다.|  
|[\<trace>](trace-element.md)|추적 메시지를 수집하고 저장하고 라우팅하는 수신기가 포함되어 있습니다.|  
  
## <a name="see-also"></a>참고자료

- <xref:System.Diagnostics.Trace>
- <xref:System.Diagnostics.TraceSource>
- <xref:System.Diagnostics.Debug>
- [구성 파일 스키마](../index.md)
