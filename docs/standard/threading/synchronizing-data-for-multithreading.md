---
title: 다중 스레딩을 위한 데이터 동기화
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- synchronization, threads
- threading [.NET Framework], synchronizing threads
- managed threading
ms.assetid: b980eb4c-71d5-4860-864a-6dfe3692430a
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1a7561a09b1b47827b3476b5525863503765064f
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2018
ms.locfileid: "48842660"
---
# <a name="synchronizing-data-for-multithreading"></a>다중 스레딩을 위한 데이터 동기화
다중 스레드가 단일 개체의 속성 및 메서드에 대한 호출을 할 수 있는 경우 해당 호출을 동기화하는 것은 중요합니다. 그렇지 않으면 하나의 스레드는 다른 스레드가 수행하는 작업을 중단시킬 수 있으며 개체는 잘못된 상태로 남을 수 있습니다. 멤버가 그러한 중단으로부터 보호되는 클래스를 스레드로부터 안전하다고 합니다.  
  
 공용 언어 인프라는 인스턴스 및 정적 멤버에 대한 액세스를 동기화하는 여러 전략을 제공합니다.  
  
-   동기화된 코드 영역. <xref:System.Threading.Monitor> 클래스 또는 이 클래스에 대한 컴파일러 지원을 사용하여 성능을 향상시키는 필요한 코드 블록만을 동기화할 수 있습니다.  
  
-   수동 동기화. .NET Framework 클래스 라이브러리에서 제공하는 동기화 개체를 사용할 수 있습니다. <xref:System.Threading.Monitor> 클래스에 대한 설명을 포함하는 [동기화 기본 형식 개요](../../../docs/standard/threading/overview-of-synchronization-primitives.md)를 참조하세요.  
  
-   동기화된 컨텍스트. <xref:System.Runtime.Remoting.Contexts.SynchronizationAttribute>를 사용하여 <xref:System.ContextBoundObject> 개체에 대한 간단한 자동 동기화를 사용하도록 설정할 수 있습니다.  
  
-   <xref:System.Collections.Concurrent?displayProperty=nameWithType> 네임스페이스의 컬렉션 클래스. 이러한 클래스는 기본 제공 동기화된 추가 및 제거 작업을 제공합니다. 자세한 내용은 [스레드로부터 안전한 컬렉션](../../../docs/standard/collections/thread-safe/index.md)을 참조하세요.  
  
 공용 언어 런타임은 클래스가 요구 사항에 따라 다양한 서로 다른 방식으로 동기화될 수 있는 범주의 수로 나뉘는 스레드 모델을 제공합니다. 다음 표는 지정된 동기화 범주로 필드 및 메서드에 대해 제공되는 동기화 지원을 보여 줍니다.  
  
|범주|전역 필드|정적 필드|정적 메서드|인스턴스 필드|인스턴스 메서드|특정 코드 블록|  
|--------------|-------------------|-------------------|--------------------|---------------------|----------------------|--------------------------|  
|동기화 없음|아니요|아니요|아니요|아니요|아니요|아니요|  
|동기화된 컨텍스트|아니요|아니요|아니요|예|예|아니요|  
|동기화된 코드 영역|아니요|아니요|표시된 경우에만|아니요|표시된 경우에만|표시된 경우에만|  
|수동 동기화|수동|수동|수동|수동|수동|수동|  
  
## <a name="no-synchronization"></a>동기화 없음  
 이것은 개체의 기본값입니다. 모든 스레드는 언제든지 모든 메서드 또는 필드에 액세스할 수 있습니다. 한 번에 하나의 스레드만 이러한 개체에 액세스해야 합니다.  
  
## <a name="manual-synchronization"></a>수동 동기화  
 .NET Framework 클래스 라이브러리는 스레드 동기화에 대한 다양한 클래스를 제공합니다. [동기화 기본 형식 개요](../../../docs/standard/threading/overview-of-synchronization-primitives.md)를 참조하세요.  
  
## <a name="synchronized-code-regions"></a>동기화된 코드 영역  
 <xref:System.Threading.Monitor> 클래스 또는 컴파일러 키워드를 사용하여 코드 블록, 인스턴스 메서드 및 정적 메서드를 동기화할 수 있습니다. 동기화된 정적 필드에 대한 지원은 없습니다.  
  
 Visual Basic 및 C#은 특정 언어 키워드를 사용하여 코드 블록의 표시를 지원합니다(C#에서 `lock` 문 또는 Visual Basic에서 `SyncLock` 문). 스레드에 의해 코드가 실행되면 잠금을 얻으려는 시도가 이루어집니다. 다른 스레드가 잠금을 이미 획득한 경우 잠금을 사용할 수 있게 될 때까지 해당 스레드는 차단됩니다. 스레드가 동기화된 코드 블록을 종료하면 스레드가 블록을 종료하는 방법에 관계 없이 잠금이 해제됩니다.  
  
> [!NOTE]
>  동기화된 영역 내에서 <xref:System.Threading.Monitor>의 다른 메서드와 함께 사용할 수 있도록 <xref:System.Threading.Monitor.Enter%2A?displayProperty=nameWithType> 및 <xref:System.Threading.Monitor.Exit%2A?displayProperty=nameWithType>을 사용하여 `lock` 및 `SyncLock` 문이 구현됩니다.  
  
 **Monitor** 또는 컴파일러 키워드 중 하나를 사용하여 전체 메서드의 본문을 잠그는 것과 동일한 효과를 가지는 **MethodImplAttribute** 및 **MethodImplOptions.Synchronized**를 사용하여 메서드를 데코레이팅할 수도 있습니다.  
  
 <xref:System.Threading.Thread.Interrupt%2A?displayProperty=nameWithType>를 사용하여 동기화된 코드 영역에 대한 액세스를 기다리는 것과 같은 차단 작업에서 스레드를 중단시킬 수 있습니다. <xref:System.Threading.Thread.Sleep%2A?displayProperty=nameWithType>과 같은 작업에서 스레드를 중단시키는 데도 **Thread.Interrupt**가 사용됩니다.  
  
> [!IMPORTANT]
>  `static` 메서드(Visual Basic에서 `Shared` 메서드)를 보호하기 위해 형식(C#에서 `typeof(MyType)`, Visual Basic에서 `GetType(MyType)` 또는 C++에서 `MyType::typeid`)을 잠그지 마세요. 전용 정적 개체를 대신 사용합니다. 마찬가지로 인스턴스 메서드를 잠그는 데 C#에서 `this`(Visual Basic에서 `Me`)를 사용하지 마세요. 전용 개체를 대신 사용합니다. 잠재적으로 교착 상태 또는 성능 문제를 발생시키는 사용자 고유의 것 이외의 코드에서 클래스 또는 인스턴스를 잠글 수 있습니다.  
  
### <a name="compiler-support"></a>컴파일러 지원  
 Visual Basic 및 C#은 <xref:System.Threading.Monitor.Enter%2A?displayProperty=nameWithType> 및 <xref:System.Threading.Monitor.Exit%2A?displayProperty=nameWithType>를 사용하여 개체를 잠그는 언어 키워드를 지원합니다. Visual Basic은 [SyncLock](~/docs/visual-basic/language-reference/statements/synclock-statement.md) 문을 지원하고 C#은 [lock](~/docs/csharp/language-reference/keywords/lock-statement.md) 문을 지원합니다.  
  
 두 경우 모두 코드 블록에서 예외가 throw되는 경우 **lock** 또는 **SyncLock**으로 획득된 잠금이 자동으로 해제됩니다. C# 및 Visual Basic 컴파일러는 시도의 초반에 **Monitor.Enter**로 **try**/**finally** 블록을 내보내고 **finally** 블록에서 **Monitor.Exit**을 내보냅니다. **lock** 또는 **SyncLock** 블록 내에서 예외가 throw되는 경우 **finally** 처리기가 정리 작업을 수행할 수 있도록 실행됩니다.  
  
## <a name="synchronized-context"></a>동기화된 컨텍스트  
 모든 **ContextBoundObject**에서 **SynchronizationAttribute**를 사용하여 모든 인스턴스 메서드와 필드를 동기화할 수 있습니다. 동일한 컨텍스트 도메인에 있는 모든 개체는 동일한 잠금을 공유합니다. 여러 스레드가 메서드 및 필드에 액세스할 수 있지만 한 번에 하나의 스레드만 허용됩니다.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Runtime.Remoting.Contexts.SynchronizationAttribute>  
- [스레드 및 스레딩](../../../docs/standard/threading/threads-and-threading.md)  
- [동기화 기본 형식 개요](../../../docs/standard/threading/overview-of-synchronization-primitives.md)  
- [SyncLock 문](~/docs/visual-basic/language-reference/statements/synclock-statement.md)  
- [lock 문](~/docs/csharp/language-reference/keywords/lock-statement.md)
