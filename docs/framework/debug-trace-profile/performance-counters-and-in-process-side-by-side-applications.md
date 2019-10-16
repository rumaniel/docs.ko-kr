---
title: 성능 카운터 및 In-Process Side-By-Side 응용 프로그램
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- performance counters
- performance counters,and in-process side-by-side applications
- performance,.NET Framework applications
- performance monitoring,counters
ms.assetid: 6888f9be-c65b-4b03-a07b-df7ebdee2436
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 3c583e9568a55b994f0516af2dcdf29f0d0f21fb
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69967271"
---
# <a name="performance-counters-and-in-process-side-by-side-applications"></a>성능 카운터 및 In-Process Side-By-Side 응용 프로그램
성능 모니터(Perfmon.exe)를 사용하면 런타임별로 성능 카운터를 구분할 수 있습니다. 이 항목에서는 이 기능을 사용하는 데 필요한 레지스트리 변경 사항에 대해 설명합니다.  
  
## <a name="the-default-behavior"></a>기본 동작  
 기본적으로 성능 모니터는 응용 프로그램별로 성능 카운터를 표시합니다. 그러나 이 동작이 문제가 될 수 있는 두 가지 시나리오가 있습니다.  
  
- 이름이 동일한 두 개의 애플리케이션을 모니터링하는 경우. 예를 들어 두 애플리케이션의 이름을 모두 myapp.exe로 지정하면 **인스턴스** 열에 하나는 **myapp**으로 표시되고 다른 하나는 **myapp#1**오 표시됩니다. 이 경우 성능 카운터를 특정 애플리케이션과 일치시키는 것은 어렵습니다. **myapp#1**용으로 수집한 데이터가 첫 번째 myapp.exe를 참조하는지 아니면 두 번째 myapp.exe를 참조하는지 명확하지 않습니다.  
  
- 애플리케이션에서 공용 언어 런타임의 인스턴스를 여러 개 사용하는 경우. .NET Framework 4는 in-process side-by-side 호스팅 시나리오를 지원 합니다. 즉, 단일 프로세스나 응용 프로그램에서 공용 언어 런타임의 인스턴스를 여러 개 로드할 수 있습니다. myapp.exe라는 단일 애플리케이션에서 두 개의 런타임 인스턴스를 로드하는 경우 기본적으로 **Instance** 열이 **myapp** 및 **myapp#1**로 지정됩니다. 이 경우 **myapp** 및 **myapp#1**이 이름이 같은 두 애플리케이션을 나타내는지 아니면 런타임이 두 개인 동일한 애플리케이션을 나타내는지 명확하지 않습니다. 이름이 같은 여러 애플리케이션에서 여러 런타임을 로드하는 경우 모호성은 더 커집니다.  
  
 이 모호성을 제거하기 위해 레지스트리 키를 설정할 수 있습니다. .NET Framework 4를 사용 하 여 개발 된 응용 프로그램의 경우이 레지스트리 변경 내용에 따라 **인스턴스** 열의 응용 프로그램 이름에 프로세스 식별자와 런타임 인스턴스 식별자가 차례로 추가 됩니다. *application* 또는 *application*#1 대신 이제 **Instance** 열에서 응용 프로그램은 *application*_`p`*processID*\_`r`*runtimeID*로 식별됩니다. 응용 프로그램이 이전 버전의 공용 언어 런타임을 사용 하 여 개발 된 경우 해당 인스턴스는 .NET Framework 4가 설치 된 경우 *\_응용 프로그램*`p`*processID* 로 표시 됩니다.  
  
## <a name="performance-counters-for-in-process-side-by-side-applications"></a>In-Process Side-by-Side 애플리케이션의 성능 카운터  
 단일 애플리케이션에서 호스팅되는 여러 공용 언어 런타임 버전의 성능 카운터를 처리하려면 다음 표에 표시된 대로 단일 레지스트리 키 설정을 변경해야 합니다.  
  
|||  
|-|-|  
|키 이름|HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\\.NETFramework\Performance|  
|값 이름|ProcessNameFormat|  
|값 형식|REG_DWORD|  
|값|1 (0x00000001)|  
  
 `ProcessNameFormat`의 값이 0이면 기본 동작이 사용되는 것을 나타냅니다. 즉, Perfmon.exe에서 응용 프로그램별로 성능 카운터를 표시합니다. 이 값을 1로 설정하면 Perfmon.exe에서 여러 버전의 애플리케이션을 명확하게 구분하고 런타임별로 성능 카운터를 제공합니다. `ProcessNameFormat` 레지스트리 키 설정의 다른 값은 지원되지 않으며 나중에 사용하도록 예약됩니다.  
  
 새로운 인스턴스 이름 지정 기능이 제대로 작동하도록 `ProcessNameFormat` 레지스트리 키 설정을 업데이트한 다음 Perfmon.exe 또는 성능 카운터의 다른 소비자를 다시 시작해야 합니다.  
  
 다음 예제에서는 프로그래밍 방식으로 `ProcessNameFormat` 값을 변경하는 방법을 보여 줍니다.  
  
 [!code-csharp[Conceptual.PerfCounters.InProSxS#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.perfcounters.inprosxs/cs/regsetting1.cs#1)]
 [!code-vb[Conceptual.PerfCounters.InProSxS#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.perfcounters.inprosxs/vb/regsetting1.vb#1)]  
  
 레지스트리를 변경 하면 .NET Framework 4를 대상으로 하는 응용 프로그램의 이름이 응용 프로그램 _`p`*processID*\_`r`*runtimeID*로 표시 됩니다. 는 응용 프로그램의 이름이 고, *processID* 는 응용 프로그램의 프로세스 식별자 이며, *runtimeID* 는 공용 언어 런타임 식별자입니다. 예를 들어 myapp.exe라는 애플리케이션에서 공용 언어 런타임의 인스턴스를 두 개 로드하는 경우 Perfmon.exe에서는 하나의 인스턴스를 myapp_p1416_r10으로 식별하고 두 번째는 myapp_p3160_r10으로 식별합니다. 런타임 ID는 프로세스에 있는 런타임만 구분합니다. 런타임에 대한 다른 정보는 제공하지 않습니다. (예를 들어, 런타임 ID는 버전이나 런타임의 SKU와 아무 관계가 없습니다.)  
  
 .NET Framework 4가 설치 되어 있는 경우 레지스트리 변경 내용은 이전 버전의 .NET Framework를 사용 하 여 개발 된 응용 프로그램에도 영향을 줍니다. 이러한 애플리케이션은 Perfmon.exe에 *application_* `p`*processID*로 표시됩니다. 여기서 *application*은 애플리케이션 이름이고 *processID*는 프로세스 식별자입니다. 예를 들어, myapp.exe라는 두 애플리케이션의 성능 카운터를 모니터하는 경우 하나는 myapp_p23900으로 표시되고 다른 하나는 myapp_p24908로 표시될 수 있습니다.  
  
> [!NOTE]
> 프로세스 식별자를 사용하면 이전 버전의 런타임을 사용하는 이름이 동일한 두 애플리케이션을 확인할 때 모호성이 제거됩니다. 이전 버전의 공용 언어 런타임에서는 병렬 시나리오를 지원하지 않으므로 이전 버전에는 런타임 ID가 필요하지 않습니다.  
  
 .NET Framework 4가 없거나 제거 된 경우 레지스트리 키를 설정 해도 아무런 영향을 주지 않습니다. 즉, 이름이 같은 두 개의 애플리케이션이 Perfmon.exe에 계속 *application* 및 *application#1*(예: **myapp** 및 **myapp#1**)로 표시됩니다.
