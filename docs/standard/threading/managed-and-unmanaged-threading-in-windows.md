---
title: Windows에서 관리되는 스레딩 및 관리되지 않는 스레딩
ms.date: 10/24/2018
ms.technology: dotnet-standard
helpviewer_keywords:
- threading [.NET Framework], unmanaged
- threading [.NET Framework], managed
- threading [.NET], managed
- threads and fibers [.NET]
- managed threading
ms.assetid: 4fb6452f-c071-420d-9e71-da16dee7a1eb
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: da32d514b19424487cebc1d113388cfa9a2dbdf0
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69913237"
---
# <a name="managed-and-unmanaged-threading-in-windows"></a>Windows에서 관리되는 스레딩 및 관리되지 않는 스레딩

공용 언어 런타임에 의해 만들어진 스레드 및 런타임 외부에서 만들어져 코드를 실행하기 위해 관리되는 환경에 들어가는 스레드를 비롯한 모든 스레드는 <xref:System.Threading.Thread> 클래스를 통해 관리됩니다. 런타임은 해당 프로세스에서 관리되는 실행 환경 내에서 코드를 실행한 적이 있는 모든 스레드를 모니터링하며, 다른 모든 스레드는 추적하지 않습니다. 스레드는 COM interop(런타임이 관리되는 개체를 관리되지 않는 환경에 COM 개체로 노출하므로), COM [DllGetClassObject](/windows/desktop/api/combaseapi/nf-combaseapi-dllgetclassobject) 함수 및 플랫폼 호출을 통해 관리되는 실행 환경에 들어갈 수 있습니다.  
  
 관리되지 않는 스레드가 COM 호출 가능 래퍼를 통해 런타임에 들어가면 시스템에서는 해당 스레드의 스레드 로컬 저장소를 확인하여 내부의 관리되는 <xref:System.Threading.Thread> 개체를 찾습니다. 이 개체를 찾은 경우 런타임이 이미 이 스레드에 대해 알고 있는 것입니다. 그러나 이 개체를 찾을 수 없으면 런타임은 새 <xref:System.Threading.Thread> 개체를 빌드하여 해당 스레드의 스레드 로컬 저장소에 설치합니다.  
  
 관리되는 스레딩에서 <xref:System.Threading.Thread.GetHashCode%2A?displayProperty=nameWithType> 는 안정적인 관리되는 스레드 ID입니다. 이는 이 값을 가져온 애플리케이션 도메인과 관계없이 스레드 수명 동안 다른 모든 스레드의 값과 충돌하지 않습니다.  
  
> [!NOTE]
> 관리되지 않는 호스트가 관리되는 스레드와 관리되지 않는 스레드 간의 관계를 제어할 수 있으므로 운영 체제 **ThreadId** 는 관리되는 스레드에 대한 고정 관계를 포함하지 않습니다. 특히, 정교한 호스트는 파이버 API를 사용하여 동일한 운영 체제 스레드에 대해 관리되는 여러 스레드를 예약하거나 다양한 운영 체제 스레드 간에 관리되는 스레드를 이동할 수 있습니다.  
  
## <a name="mapping-from-win32-threading-to-managed-threading"></a>Win32 스레딩에서 관리되는 스레딩으로 매핑

 다음 테이블에는 Win32 스레딩 요소가 대략적으로 동일한 런타임 요소에 매핑되어 있습니다. 이 매핑은 동일한 기능을 나타내지 않습니다. 예를 들어, **TerminateThread** 는 **finally** 절을 실행하거나 리소스를 해제하지 않고 방지될 수 없습니다. 그러나 <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> 는 모든 롤백 코드를 실행하고 모든 리소스를 회수하며 <xref:System.Threading.Thread.ResetAbort%2A>를 사용하여 거부될 수 있습니다. 기능에 대해 가정하기 전에 설명서를 주의해서 읽어야 합니다.  
  
|Win32|공용 언어 런타임|  
|--------------|------------------------------------|  
|**CreateThread**|**Thread** 와 <xref:System.Threading.ThreadStart>의 조합|  
|**TerminateThread**|<xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType>|  
|**SuspendThread**|<xref:System.Threading.Thread.Suspend%2A?displayProperty=nameWithType>|  
|**ResumeThread**|<xref:System.Threading.Thread.Resume%2A?displayProperty=nameWithType>|  
|**Sleep**|<xref:System.Threading.Thread.Sleep%2A?displayProperty=nameWithType>|  
|스레드 핸들의**WaitForSingleObject**|<xref:System.Threading.Thread.Join%2A?displayProperty=nameWithType>|  
|**ExitThread**|동일한 요소 없음|  
|**GetCurrentThread**|<xref:System.Threading.Thread.CurrentThread%2A?displayProperty=nameWithType>|  
|**SetThreadPriority**|<xref:System.Threading.Thread.Priority%2A?displayProperty=nameWithType>|  
|동일한 요소 없음|<xref:System.Threading.Thread.Name%2A?displayProperty=nameWithType>|  
|동일한 요소 없음|<xref:System.Threading.Thread.IsBackground%2A?displayProperty=nameWithType>|  
|**CoInitializeEx** (OLE32.DLL)와 비슷함|<xref:System.Threading.Thread.ApartmentState%2A?displayProperty=nameWithType>|  
  
## <a name="managed-threads-and-com-apartments"></a>관리되는 스레드 및 COM 아파트

관리되는 스레드는 [단일 스레드](/windows/desktop/com/single-threaded-apartments) 또는 [다중 스레드](/windows/desktop/com/multithreaded-apartments) 아파트를 호스트할 것임을 나타내기 위해 표시될 수 있습니다. (COM 스레딩 아키텍처에 대한 자세한 내용은 [프로세스, 스레드 및 아파트](/windows/desktop/com/processes--threads--and-apartments)를 참조하세요.) <xref:System.Threading.Thread.GetApartmentState%2A> 클래스의 <xref:System.Threading.Thread.SetApartmentState%2A>, <xref:System.Threading.Thread.TrySetApartmentState%2A> 및 <xref:System.Threading.Thread> 메서드는 스레드의 아파트 상태를 반환하고 할당합니다. 상태가 설정되지 않은 경우 <xref:System.Threading.Thread.GetApartmentState%2A>는 <xref:System.Threading.ApartmentState.Unknown?displayProperty=nameWithType>을 반환합니다.  
  
 이 속성은 스레드가 <xref:System.Threading.ThreadState.Unstarted?displayProperty=nameWithType> 상태일 때만 설정될 수 있으며, 한 스레드에 대해 한 번만 설정될 수 있습니다.  
  
 스레드가 시작되기 전에 아파트 상태가 설정되지 않은 경우 스레드가 MTA(다중 스레드 아파트)로 초기화됩니다. 종료자 스레드 및 <xref:System.Threading.ThreadPool> 에 의해 제어되는 모든 스레드는 MTA입니다.  
  
> [!IMPORTANT]
> 애플리케이션 시작 코드의 경우 아파트 상태를 제어하는 유일한 방법은 <xref:System.MTAThreadAttribute> 또는 <xref:System.STAThreadAttribute> 를 진입점 프로시저에 적용하는 것입니다. .NET Framework 1.0 및 1.1에서는 <xref:System.Threading.Thread.ApartmentState%2A> 속성을 코드의 첫 번째 줄로 설정할 수 있습니다. .NET Framework 2.0에서는 이러한 설정이 허용되지 않습니다.  
  
 COM에 노출된 관리되는 개체는 자유 스레드된 마샬러를 집계한 것처럼 동작합니다. 즉, 모든 COM 아파트에서 자유 스레드 방식으로 이러한 개체를 호출할 수 있습니다. 이 자유 스레드 동작을 노출하지 않는 관리되는 개체만이 <xref:System.EnterpriseServices.ServicedComponent> 또는 <xref:System.Runtime.InteropServices.StandardOleMarshalObject>에서 파생되는 개체입니다.  
  
 관리되는 세계에는 컨텍스트 및 컨텍스트 바인딩된 관리되는 인스턴스를 사용하지 않는 한 <xref:System.Runtime.Remoting.Contexts.SynchronizationAttribute>에 대한 지원이 없습니다. 엔터프라이즈 서비스를 사용 중인 경우 개체는 <xref:System.EnterpriseServices.ServicedComponent>(이 자체는 <xref:System.ContextBoundObject>에서 파생됨)에서 파생되어야 합니다.  
  
 관리 코드가 COM 개체를 호출할 때는 항상 COM 규칙을 따릅니다. 즉, 관리 코드는 OLE32에서 지시하는 대로 COM 아파트 프록시 및 COM+ 1.0 컨텍스트 래퍼를 통해 호출합니다.  
  
## <a name="blocking-issues"></a>차단 문제  

스레드가 비관리 코드에서 스레드를 차단한 운영 체제에 대해 관리되지 않는 호출을 수행할 경우 런타임이 <xref:System.Threading.Thread.Interrupt%2A?displayProperty=nameWithType> 또는 <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType>에 대해 스레드를 제어하지 못합니다. <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType>의 경우 런타임은 스레드에 **Abort** 를 표시하고 스레드가 관리 코드에 다시 들어가면 스레드를 제어합니다. 관리되지 않는 차단이 아니라 관리되는 차단을 사용하는 것이 좋습니다. <xref:System.Threading.WaitHandle.WaitOne%2A?displayProperty=nameWithType>,<xref:System.Threading.WaitHandle.WaitAny%2A?displayProperty=nameWithType>, <xref:System.Threading.WaitHandle.WaitAll%2A?displayProperty=nameWithType>, <xref:System.Threading.Monitor.Enter%2A?displayProperty=nameWithType>, <xref:System.Threading.Monitor.TryEnter%2A?displayProperty=nameWithType>, <xref:System.Threading.Thread.Join%2A?displayProperty=nameWithType>, <xref:System.GC.WaitForPendingFinalizers%2A?displayProperty=nameWithType>등은 모두 <xref:System.Threading.Thread.Interrupt%2A?displayProperty=nameWithType> 및 <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType>에 응답합니다. 또한 스레드가 단일 스레드 아파트에 있는 경우 이러한 모든 관리되는 차단 작업은 스레드가 차단되어 있는 동안 올바르게 아파트에 메시지를 펌핑합니다.  

## <a name="threads-and-fibers"></a>스레드 및 파이버

.NET 스레딩 모델은 [파이버](/windows/desktop/procthread/fibers)를 지원하지 않습니다. 파이버를 사용하여 구현된 관리되지 않는 함수를 호출하면 안 됩니다. 이러한 호출로 인해 .NET 런타임에서 크래시가 발생할 수 있습니다.

## <a name="see-also"></a>참고 항목

- <xref:System.Threading.Thread.ApartmentState%2A?displayProperty=nameWithType>
- <xref:System.Threading.ThreadState>
- <xref:System.EnterpriseServices.ServicedComponent>
- <xref:System.Threading.Thread>
- <xref:System.Threading.Monitor>
