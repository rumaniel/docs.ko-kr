---
title: EventWaitHandle
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- threading [.NET Framework], EventWaitHandle class
- EventWaitHandle class
- event wait handles [.NET Framework]
- threading [.NET Framework], cross-process synchronization
ms.assetid: 11ee0b38-d663-4617-b793-35eb6c64e9fc
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d9c90a3bd272b54d2884d013e62123dd67d836e3
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69960049"
---
# <a name="eventwaithandle"></a>EventWaitHandle
<xref:System.Threading.EventWaitHandle> 클래스를 사용하면 여러 스레드가 신호를 보내고 신호를 대기하여 서로 통신할 수 있습니다. 이벤트 대기 핸들(단순히 이벤트라고도 함)은 하나 이상의 대기 스레드를 해제하기 위해 신호를 보낼 수 있는 대기 핸들입니다. 신호를 받은 후 이벤트 대기 핸들은 수동으로 또는 자동으로 다시 설정됩니다. <xref:System.Threading.EventWaitHandle> 클래스는 로컬 이벤트 대기 핸들(로컬 이벤트) 또는 명명된 시스템 이벤트 대기 핸들(모든 프로세스에 표시되는 명명된 이벤트 또는 시스템 이벤트)을 나타낼 수 있습니다.  
  
> [!NOTE]
> 이벤트 대기 핸들은 .NET [이벤트](../events/index.md)가 아닙니다. 관련된 대리자 또는 이벤트 처리기가 없습니다. “이벤트”라는 단어는 기존에는 운영 체제 이벤트라고 했고 대기 핸들에 신호를 보내는 동작이 이벤트가 발생한 대기 스레드를 나타내기 때문에 이벤트를 설명하는 데 사용됩니다.  
  
 로컬 및 명명된 이벤트 대기 핸들은 모두 <xref:Microsoft.Win32.SafeHandles.SafeWaitHandle> 래퍼로 보호되는 시스템 동기화 개체를 사용하여 리소스가 해제되도록 합니다. <xref:System.Threading.WaitHandle.Dispose%2A> 메서드를 사용하여 개체 사용을 완료했을 때 즉시 리소스를 해제할 수 있습니다.  
  
## <a name="event-wait-handles-that-reset-automatically"></a>자동으로 다시 설정되는 이벤트 대기 핸들  
 <xref:System.Threading.EventWaitHandle> 개체를 만들 때 <xref:System.Threading.EventResetMode.AutoReset?displayProperty=nameWithType>을 지정하여 자동 재설정 이벤트를 만듭니다. 이름에서 알 수 있듯이 단일 대기 스레드를 해제한 후에 신호를 받으면 이 동기화 이벤트가 자동으로 다시 설정됩니다. <xref:System.Threading.EventWaitHandle.Set%2A> 메서드를 호출하여 이벤트에 신호를 보냅니다.  
  
 자동 재설정 이벤트는 일반적으로 한 번에 하나의 스레드에만 리소스에 대한 액세스를 제공하는 데 사용됩니다. 스레드는 <xref:System.Threading.WaitHandle.WaitOne%2A> 메서드를 호출하여 리소스를 요청합니다. 다른 스레드가 대기 핸들을 보유하고 있지 않으면 메서드는 `true`를 반환하고 호출 스레드가 리소스를 제어합니다.  
  
> [!IMPORTANT]
> 모든 동기화 메커니즘과 마찬가지로 보호된 리소스에 액세스하기 전에 모든 코드 경로가 적절한 대기 핸들에서 대기하도록 해야 합니다. 스레드 동기화는 협조적입니다.  
  
 대기 중인 스레드가 없을 때 신호를 받은 자동 재설정 이벤트는 스레드가 이 이벤트에서 대기를 시도할 때까지 신호를 받은 것으로 유지됩니다. 이벤트는 스레드를 해제하고 즉시 다시 설정되어 후속 스레드를 차단합니다.  
  
## <a name="event-wait-handles-that-reset-manually"></a>수동으로 다시 설정되는 이벤트 대기 핸들  
 <xref:System.Threading.EventWaitHandle> 개체를 만들 때 <xref:System.Threading.EventResetMode.ManualReset?displayProperty=nameWithType>을 지정하여 수동 재설정 이벤트를 만듭니다. 이름에서 알 수 있듯이 신호를 받은 후 이 동기화 이벤트를 수동으로 다시 설정해야 합니다. 이벤트가 다시 설정될 때까지는 <xref:System.Threading.EventWaitHandle.Reset%2A> 메서드를 호출하면 이벤트 핸들에서 대기하는 스레드가 차단 없이 즉시 진행됩니다.  
  
 수동 재설정 이벤트는 울타리 문처럼 작동합니다. 이벤트가 신호를 받지 않으면 울타리 안의 말처럼 이벤트에서 대기하는 스레드가 차단됩니다. 이벤트가 신호를 받은 경우 <xref:System.Threading.EventWaitHandle.Set%2A> 메서드를 호출하면 모든 대기 스레드가 해제되어 진행됩니다. 이 이벤트는 <xref:System.Threading.EventWaitHandle.Reset%2A> 메서드가 호출될 때까지 신호를 받은 것으로 유지됩니다. 이 덕분에 수동 재설정 이벤트는 한 스레드가 작업을 완료할 때까지 대기해야 하는 스레드를 지연시키는 적합한 방법입니다.  
  
 울타리를 떠나는 말들처럼 해제된 스레드가 운영 체제에 의해 예약되고 실행을 재개하는 데는 시간이 걸립니다. 모든 스레드가 실행을 재개하기 전에 <xref:System.Threading.EventWaitHandle.Reset%2A> 메서드가 호출되면 나머지 스레드가 다시 한번 차단됩니다. 재개되는 스레드와 차단되는 스레드는 시스템에 대한 로드, 스케줄러를 기다리는 스레드 수 등의 임의 요소에 따라 달라집니다. 이는 이벤트에 신호를 보내는 스레드가 신호를 보낸 후 종료될 경우의 문제가 아니라, 가장 일반적인 사용 패턴입니다. 이벤트에 신호를 보낸 스레드가 모든 대기 스레드가 재기된 후 새 작업을 시작하도록 하려면 해당 스레드를 모든 대기 스레드가 재개될 때까지 차단해야 합니다. 그렇지 않으면 경합 상태가 있어서 코드의 동작을 예측할 수 없습니다.  
  
## <a name="features-common-to-automatic-and-manual-events"></a>자동 및 수동 이벤트에 공통적인 기능  
 일반적으로 차단이 해제된 스레드가 대기 스레드 중 하나(자동 재설정 이벤트의 경우) 또는 모든 대기 스레드(수동 재설정 이벤트의 경우)를 해제하는 <xref:System.Threading.EventWaitHandle.Set%2A> 메서드를 호출할 때까지 하나 이상의 스레드가 <xref:System.Threading.EventWaitHandle>에서 차단됩니다. 스레드는 <xref:System.Threading.EventWaitHandle>에 신호를 보낸 다음, 정적 <xref:System.Threading.WaitHandle.SignalAndWait%2A?displayProperty=nameWithType> 메서드를 호출하여 이 개체에서 원자성 작업으로 차단될 수 있습니다.  
  
 <xref:System.Threading.EventWaitHandle> 개체는 정적 <xref:System.Threading.WaitHandle.WaitAll%2A?displayProperty=nameWithType> 및 <xref:System.Threading.WaitHandle.WaitAny%2A?displayProperty=nameWithType> 메서드와 함께 사용할 수 있습니다. <xref:System.Threading.EventWaitHandle> 및 <xref:System.Threading.Mutex> 클래스는 모두 <xref:System.Threading.WaitHandle>에서 파생되므로 두 클래스를 모두 이러한 방법으로 사용할 수 있습니다.  
  
### <a name="named-events"></a>명명된 이벤트  
 Windows 운영 체제에서는 이벤트 대기 핸들에 이름을 지정할 수 있습니다. 명명된 이벤트는 시스템 전체에서 사용됩니다. 즉, 명명된 이벤트가 만들어지면 모든 프로세스의 모든 스레드에 표시됩니다. 따라서 명명된 이벤트는 스레드뿐 아니라 프로세스의 활동을 동기화하는 데도 사용할 수 있습니다.  
  
 이벤트 이름을 지정하는 생성자 중 하나를 사용하여 명명된 시스템 이벤트를 나타내는 <xref:System.Threading.EventWaitHandle> 개체를 만들 수 있습니다.  
  
> [!NOTE]
> 명명된 이벤트는 시스템 전체 이벤트이므로 같은 명명된 이벤트를 나타내는 <xref:System.Threading.EventWaitHandle> 개체를 여러 개 사용할 수 있습니다. 생성자 또는 <xref:System.Threading.EventWaitHandle.OpenExisting%2A> 메서드를 호출할 때마다 새 <xref:System.Threading.EventWaitHandle> 개체가 만들어집니다. 같은 이름을 반복적으로 지정하면 같은 명명된 이벤트를 나타내는 개체가 여러 개 만들어집니다.  
  
 명명된 이벤트를 사용할 경우 주의하는 것이 좋습니다. 이러한 이벤트는 시스템 전체 이벤트이므로 같은 이름을 사용하는 다른 프로세스가 예기치 않게 스레드를 차단할 수 있습니다. 그러면 동일 컴퓨터에서 실행되는 악성 코드가 이를 악용해 서비스 거부 공격을 수행할 수 있습니다.  
  
 명명된 이벤트를 나타내는 <xref:System.Threading.EventWaitHandle> 개체를 보호하려면 액세스 제어 보안을 사용합니다. 이때 <xref:System.Security.AccessControl.EventWaitHandleSecurity> 개체를 지정하는 생성자를 사용하는 것이 좋습니다. <xref:System.Threading.EventWaitHandle.SetAccessControl%2A> 메서드를 사용하여 액세스 제어 보안을 적용할 수도 있지만 이렇게 하면 이벤트 작성 시간과 보호가 적용되는 시간 사이에 취약한 기간이 생기게 됩니다. 액세스 제어 보안을 통해 이벤트를 보호하면 악의적인 공격을 방지할 수는 있지만 의도하지 않은 이름 충돌 문제는 해결되지 않습니다.  
  
> [!NOTE]
> <xref:System.Threading.EventWaitHandle> 클래스와 달리 파생된 클래스 <xref:System.Threading.AutoResetEvent> 및 <xref:System.Threading.ManualResetEvent>는 로컬 대기 핸들만 나타낼 수 있습니다. 명명된 시스템 이벤트를 나타낼 수 없습니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Threading.EventWaitHandle>
- <xref:System.Threading.WaitHandle>
- <xref:System.Threading.AutoResetEvent>
- <xref:System.Threading.ManualResetEvent>
