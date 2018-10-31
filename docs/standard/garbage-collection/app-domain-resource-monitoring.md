---
title: 응용 프로그램 도메인 리소스 모니터링
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- monitoring managed memory use by application domain
- application domains, memory use
- memory use, monitoring
- application domains, resource monitoring
ms.assetid: 318bedf8-7f35-4f00-b34a-2b7b8e3fa315
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 50d601d711579bce2e2651a1efc65d824a50d47a
ms.sourcegitcommit: 8c28ab17c26bf08abbd004cc37651985c68841b8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/08/2018
ms.locfileid: "48266652"
---
# <a name="application-domain-resource-monitoring"></a>응용 프로그램 도메인 리소스 모니터링
ARM(응용 프로그램 도메인 리소스 모니터링)을 통해 호스트가 응용 프로그램 도메인별로 CPU 및 메모리 사용량을 모니터링할 수 있습니다. 이는 장기 실행 프로세스에서 많은 응용 프로그램 도메인을 사용하는 ASP.NET과 같은 호스트에 유용합니다. 호스트가 전체 프로세스의 성능에 부정적인 영향을 주는 응용 프로그램의 응용 프로그램 도메인을 언로드할 수 있지만, 이는 문제가 있는 응용 프로그램을 식별할 수 있는 경우에만 가능합니다. ARM은 이러한 결정을 지원하는 데 사용할 수 있는 정보를 제공합니다.  
  
 예를 들어 호스팅 서비스에는 ASP.NET 서버에서 실행 중인 여러 응용 프로그램이 있을 수 있습니다. 프로세스의 한 응용 프로그램이 너무 많은 메모리를 사용하거나 프로세서 시간을 과도하게 사용하기 시작하는 경우 호스팅 서비스는 ARM을 사용하여 문제의 원인이 되는 응용 프로그램 도메인을 식별할 수 있습니다.  
  
 ARM은 라이브 응용 프로그램에서 사용할 수 있을 만큼 충분히 간단합니다. ETW(Windows용 이벤트 추적)를 사용하거나 관리되는 API 또는 네이티브 API를 통해 직접 정보에 액세스할 수 있습니다.  
  
## <a name="enabling-resource-monitoring"></a>리소스 모니터링 사용  
 ARM은 CLR(공용 언어 런타임)이 시작될 때 구성 파일을 제공하거나, 관리되지 않는 호스팅 API를 사용하거나, 관리 코드를 사용하거나, ARM ETW 이벤트를 수신하는 등 네 가지 방법으로 활성화할 수 있습니다.  
  
 ARM이 사용되도록 설정되는 즉시 프로세스의 모든 응용 프로그램 도메인에 대한 데이터 수집이 시작됩니다. ARM을 사용하도록 설정하기 전에 응용 프로그램 도메인을 만든 경우 응용 프로그램 도메인을 만든 때가 아니라 ARM을 사용하도록 설정한 때부터 데이터 누적이 시작됩니다. 사용하도록 설정한 ARM은 사용 중지할 수 없습니다.  
  
-   구성 파일에 [\<appDomainResourceMonitoring>](../../../docs/framework/configure-apps/file-schema/runtime/appdomainresourcemonitoring-element.md) 요소를 추가하고 `enabled` 특성을 `true`로 설정하여 CLR 시작 시 ARM을 사용하도록 설정할 수 있습니다. `false` 값(기본값)은 단지 시작할 때 ARM이 사용하도록 설정되지 않았다는 것을 의미합니다. 다른 활성화 메커니즘 중 하나를 사용하여 나중에 활성화할 수 있습니다.  
  
-   호스트가 [ICLRAppDomainResourceMonitor](../../../docs/framework/unmanaged-api/hosting/iclrappdomainresourcemonitor-interface.md) 호스팅 인터페이스를 요청하여 ARM을 사용하도록 설정할 수 있습니다. 이 인터페이스를 성공적으로 가져오면 ARM이 사용하도록 설정됩니다.  
  
-   관리 코드에서 static(Visual Basic의 경우 `Shared`) <xref:System.AppDomain.MonitoringIsEnabled%2A?displayProperty=nameWithType> 속성을 `true`로 설정하여 ARM을 사용하도록 설정할 수 있습니다. 속성을 설정하는 즉시 ARM이 사용하도록 설정됩니다.  
  
-   ETW 이벤트를 수신함으로써 시작 후 ARM을 사용하도록 설정할 수 있습니다. `AppDomainResourceManagementKeyword` 키워드를 사용하여 공용 공급자 `Microsoft-Windows-DotNETRuntime`을 사용하도록 설정하면 ARM이 사용하도록 설정되어 모든 응용 프로그램 도메인에 대해 이벤트를 발생시키기 시작합니다. 데이터를 응용 프로그램 도메인 및 스레드와 상호 연결하려면 `ThreadingKeyword` 키워드를 사용하여 `Microsoft-Windows-DotNETRuntimeRundown` 공급자도 사용하도록 설정해야 합니다.  
  
## <a name="using-arm"></a>ARM 사용  
 ARM은 응용 프로그램 도메인에서 사용하는 총 프로세서 시간 및 메모리 사용에 대한 세 종류의 정보를 제공합니다.  
  
-   **응용 프로그램 도메인의 총 프로세서 시간(초)**: 이 값은 해당 수명 동안 응용 프로그램 도메인의 실행 시간을 사용한 모든 스레드에 대해 운영 체제에서 보고한 스레드 시간을 더하여 계산됩니다. 차단되거나 중지 중인 스레드는 프로세서 시간을 사용하지 않습니다. 스레드가 네이티브 코드를 호출할 때 스레드가 네이티브 코드에 사용하는 시간은 호출이 수행된 응용 프로그램 도메인의 계산에 포함됩니다.  
  
    -   관리되는 API: <xref:System.AppDomain.MonitoringTotalProcessorTime%2A?displayProperty=nameWithType> 속성입니다.  
  
    -   호스팅 API: [ICLRAppDomainResourceMonitor::GetCurrentCpuTime](../../../docs/framework/unmanaged-api/hosting/iclrappdomainresourcemonitor-getcurrentcputime-method.md) 메서드입니다.  
  
    -   ETW 이벤트: `ThreadCreated`, `ThreadAppDomainEnter` 및 `ThreadTerminated` 이벤트입니다. 공급자 및 키워드에 대한 자세한 내용은 [CLR ETW 이벤트](../../../docs/framework/performance/clr-etw-events.md)의 “AppDomain 리소스 모니터링 이벤트”를 참조하세요.  
  
-   **해당 수명 동안 응용 프로그램 도메인에서 수행한 관리되는 총 할당(바이트)**: 할당된 개체의 수명이 짧을 수 있기 때문에 총 할당이 응용 프로그램 도메인의 메모리 사용을 항상 반영하는 것은 아닙니다. 그러나 응용 프로그램이 엄청난 수의 개체를 할당하고 해제하는 경우 할당 비용이 상당할 수 있습니다.  
  
    -   관리되는 API: <xref:System.AppDomain.MonitoringTotalAllocatedMemorySize%2A?displayProperty=nameWithType> 속성입니다.  
  
    -   호스팅 API: [ICLRAppDomainResourceMonitor::GetCurrentAllocated](../../../docs/framework/unmanaged-api/hosting/iclrappdomainresourcemonitor-getcurrentallocated-method.md) 메서드입니다.  
  
    -   ETW 이벤트: `AppDomainMemAllocated` 이벤트, `Allocated` 필드입니다.  
  
-   **응용 프로그램 도메인에 의해 참조되고 가장 최근의 전체 차단 컬렉션 후에도 유지된 관리되는 메모리(바이트)**: 이 바이트 수는 전체 차단 컬렉션 이후에만 정확합니다. 이는 백그라운드에서 발생하며 응용 프로그램을 차단하지 않는 동시 컬렉션과는 대조적입니다. 예를 들어 <xref:System.GC.Collect?displayProperty=nameWithType> 메서드 오버로드로 인해 전체 차단 컬렉션이 발생합니다.  
  
    -   관리되는 API: <xref:System.AppDomain.MonitoringSurvivedMemorySize%2A?displayProperty=nameWithType> 속성입니다.  
  
    -   호스팅 API: [ICLRAppDomainResourceMonitor::GetCurrentSurvived](../../../docs/framework/unmanaged-api/hosting/iclrappdomainresourcemonitor-getcurrentsurvived-method.md) 메서드, `pAppDomainBytesSurvived` 매개 변수입니다.  
  
    -   ETW 이벤트: `AppDomainMemSurvived` 이벤트, `Survived` 필드입니다.  
  
-   **프로세스에 의해 참조되고 가장 최근의 전체 차단 컬렉션 후에도 유지된 관리되는 총 메모리(바이트)**: 개별 응용 프로그램 도메인의 유지된 메모리를 이 바이트 수와 비교할 수 있습니다.  
  
    -   관리되는 API: <xref:System.AppDomain.MonitoringSurvivedProcessMemorySize%2A?displayProperty=nameWithType> 속성입니다.  
  
    -   호스팅 API: [ICLRAppDomainResourceMonitor::GetCurrentSurvived](../../../docs/framework/unmanaged-api/hosting/iclrappdomainresourcemonitor-getcurrentsurvived-method.md) 메서드, `pTotalBytesSurvived` 매개 변수입니다.  
  
    -   ETW 이벤트: `AppDomainMemSurvived` 이벤트, `ProcessSurvived` 필드입니다.  
  
### <a name="determining-when-a-full-blocking-collection-occurs"></a>전체 차단 컬렉션 발생 시기 확인  
 유지된 메모리의 수가 정확한 시기를 확인하려면 전체 차단 컬렉션이 발생한 바로 그때를 알아야 합니다. 이를 수행하는 방법은 ARM 통계를 조사하는 데 사용하는 API에 따라 다릅니다.  
  
#### <a name="managed-api"></a>관리되는 API  
 <xref:System.AppDomain> 클래스의 속성을 사용하는 경우 <xref:System.GC.RegisterForFullGCNotification%2A?displayProperty=nameWithType> 메서드를 사용하여 전체 컬렉션 알림에 등록할 수 있습니다. 컬렉션의 접근이 아닌 컬렉션의 완료를 기다리고 있기 때문에 사용하는 임계값은 중요하지 않습니다. 그런 다음, 전체 컬렉션이 완료될 때까지 차단하는 <xref:System.GC.WaitForFullGCComplete%2A?displayProperty=nameWithType> 메서드를 호출할 수 있습니다. 루프로 메서드를 호출하고 메서드가 반환할 때마다 필요한 모든 분석을 수행하는 스레드를 만들 수 있습니다.  
  
 또는 <xref:System.GC.CollectionCount%2A?displayProperty=nameWithType> 메서드를 주기적으로 호출하여 세대 2 컬렉션 수가 증가했는지 확인할 수 있습니다. 폴링 빈도에 따라 이 기술은 전체 컬렉션의 발생을 정확하게 표시하지 못할 수도 있습니다.  
  
#### <a name="hosting-api"></a>호스팅 API  
 관리되지 않는 호스팅 API를 사용하는 경우 호스트는 [IHostGCManager](../../../docs/framework/unmanaged-api/hosting/ihostgcmanager-interface.md) 인터페이스의 구현을 CLR에 전달해야 합니다. CLR은 컬렉션이 발생하는 동안 일시 중단된 스레드의 실행을 다시 시작할 때 [IHostGCManager::SuspensionEnding](../../../docs/framework/unmanaged-api/hosting/ihostgcmanager-suspensionending-method.md) 메서드를 호출합니다. CLR이 완료된 컬렉션의 생성을 메서드의 매개 변수로 전달하므로 호스트는 컬렉션이 전체인지 또는 부분인지 확인할 수 있습니다. [IHostGCManager::SuspensionEnding](../../../docs/framework/unmanaged-api/hosting/ihostgcmanager-suspensionending-method.md) 메서드를 구현하면 유지된 메모리를 쿼리하여 수가 업데이트되는 즉시 수를 검색하도록 할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.AppDomain.MonitoringIsEnabled%2A?displayProperty=nameWithType>  
- [ICLRAppDomainResourceMonitor 인터페이스](../../../docs/framework/unmanaged-api/hosting/iclrappdomainresourcemonitor-interface.md)  
- [\<appDomainResourceMonitoring>](../../../docs/framework/configure-apps/file-schema/runtime/appdomainresourcemonitoring-element.md)  
- [CLR ETW 이벤트](../../../docs/framework/performance/clr-etw-events.md)
