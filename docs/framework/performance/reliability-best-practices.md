---
title: 최선의 안정성 구현 방법
ms.date: 03/30/2017
helpviewer_keywords:
- marking locks
- rebooting databases
- denial of service attacks
- back-out code
- SQL Server [.NET Framework], reliability
- synchronization, reliability
- single-threaded COM components
- slow leaks
- suspending threads
- asynchronous exception handling
- leaked resources [.NET Framework]
- unmanaged memory
- memory, reliability
- threading [.NET Framework], reliability
- process-wide domain shared states
- shared states
- SafeHandle class, reliability
- reliability contracts [.NET Framework]
- cleanup operations
- constrained execution regions
- CERs
- finalizers, reliability
- reliability [.NET Framework]
- blocks, reliability
- finally clauses
- cross-application domain shared states
- catch blocks
- identifying locks
- writing reliable code
- impersonation
- GC.KeepAlive method
- managed threading
- locks, reliability
- STA-dependent features
- fibers
ms.assetid: cf624c1f-c160-46a1-bb2b-213587688da7
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 40c1b98f82fe53819edc437bbac575c1df206496
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834534"
---
# <a name="reliability-best-practices"></a>최선의 안정성 구현 방법

다음 안정성 규칙은 SQL Server 중심이지만, 호스트 기반 서버 애플리케이션에도 적용됩니다. SQL Server와 같은 서버에서 리소스가 누출되지 않고 중단되지 않는 것이 매우 중요합니다.  그러나 이 작업은 개체의 상태를 변경하는 모든 메서드에 대해 취소 코드를 작성하여 수행할 수 없습니다.  취소 코드를 사용하여 모든 위치에서 모든 오류로부터 복구되는 100% 신뢰할 수 있는 관리 코드를 작성하는 것이 목표가 아닙니다.  성공 가능성이 희박한 매우 까다로운 작업입니다.  CLR(공용 언어 런타임)에서는 완벽한 코드를 작성할 수 있는 관리 코드가 제공된다고 확실히 보장할 수 없습니다.  ASP.NET과 달리 SQL Server에서는 허용할 수 없을 정도로 오랜 기간 동안 데이터베이스를 작동 중지하지 않고는 재활용할 수 없는 단 하나의 프로세스만 사용합니다.

이와 같이 희박하게 보장되며 단일 프로세스에서 실행되는 조건에서, 필요할 때 스레드를 종료하거나 애플리케이션을 재활용하며 핸들이나 메모리와 같은 운영 체제 리소스가 누출되지 않도록 주의하는 것만이 안정성을 보장합니다.  이와 같이 안정성 제약 조건은 단순해도 안정성 요구 사항은 여전히 상당합니다.

- 운영 체제 리소스가 누출되지 않습니다.

- 모든 형식의 관리되는 잠금을 CLR에 모두 식별합니다.

- 애플리케이션 간 도메인 공유 상태를 중단시키지 않으므로 <xref:System.AppDomain> 재활용이 원활하게 작동할 수 있습니다.

<xref:System.Threading.ThreadAbortException>, <xref:System.StackOverflowException> 및 <xref:System.OutOfMemoryException> 예외를 처리하기 위한 관리 코드를 작성하는 것은 이론상으로는 가능하지만, 개발자가 애플리케이션 전체에서 이와 같이 강력한 코드를 작성하는 것을 기대하는 것은 합리적이지 않습니다.  따라서 대역 외 예외가 발생하여 스레드 실행이 종료됩니다. 종료된 스레드가 공유 상태를 편집 중이었으면(스레드에서 잠금을 보유하는지에 따라 판별 가능) <xref:System.AppDomain>이 언로드됩니다.  공유 상태를 편집 중인 메서드가 종료되면 공유 상태로 업데이트하는 안정된 취소 코드를 작성할 수 없으므로 상태가 손상됩니다.

.NET Framework 버전 2.0에서 안정성이 필요한 호스트는 SQL Server뿐입니다.  어셈블리가 SQL Server에서 실행되는 경우 데이터베이스에서 실행 중일 때 사용하지 않게 설정된 특정 기능이 있어도 해당 어셈블리의 모든 부분에서 안정성이 작동해야 합니다.  코드 분석 엔진은 어셈블리 수준에서 코드를 검사하고 비활성화된 코드를 구분할 수 없으므로 이와 같은 안정성이 필요합니다. 또 다른 SQL Server 프로그래밍 고려 사항은 SQL Server가 한 프로세스에서 모든 작업을 실행하며 <xref:System.AppDomain> 재활용을 사용하여 메모리 및 운영 체제 핸들과 같은 모든 리소스를 정리한다는 것입니다.

종료자, 소멸자 또는 `try/finally` 블록에 의존하여 취소 코드를 작성할 수 없습니다. 이러한 항목은 중단되거나 호출되지 않을 수 있습니다.

모든 컴퓨터 명령의 예기치 않은 위치에서 비동기 예외가 발생할 수 있습니다(<xref:System.Threading.ThreadAbortException>, <xref:System.StackOverflowException> 및 <xref:System.OutOfMemoryException>).

관리되는 스레드는 SQL의 Win32 스레드가 아니어도 되며, 파이버일 수도 있습니다.

프로세스 전체 또는 애플리케이션 간 도메인 변경 가능 공유 상태는 안전하게 변경하기가 극도로 어려우므로 가능하면 피해야 합니다.

메모리 부족 조건은 SQL Server에서 자주 발생합니다.

SQL Server에서 호스팅되는 라이브러리가 공유 상태를 올바르게 업데이트하지 않아도 데이터베이스를 다시 시작할 때까지 코드가 복구되지 않을 가능성이 높습니다.  또한 극단적인 경우에는 SQL Server 프로세스가 실패되는 원인이 되므로 데이터베이스를 다시 부팅해야 할 수도 있습니다.  데이터베이스를 다시 부팅하면 웹 사이트를 종료시키거나 회사 업무에 영향을 미쳐 가용성이 손상될 수 있습니다.  메모리 또는 핸들과 같은 운영 체제 리소스가 서서히 누출되면 서버에서 복구 가능성이 없이 핸들을 할당하는 데 실패하거나 서버의 성능이 서서히 저하되거나 고객의 애플리케이션 가용성이 줄어듭니다.  이러한 시나리오는 확실히 방지해야 합니다.

## <a name="best-practice-rules"></a>모범 사례 규칙

이 소개에서는 프레임워크의 안정성과 신뢰성을 높이기 위해 서버에서 실행되는 관리 코드의 코드 검토에서 파악해야 하는 사항에 중점을 둡니다. 이러한 검사를 수행하는 것은 일반적으로 좋은 방법이며 서버에서는 절대적으로 수행되어야 합니다.

교착 상태나 리소스 제약 조건이 발생하는 경우 SQL Server에서 스레드를 중단하거나 <xref:System.AppDomain>을 손상시킵니다.  이 경우 제약이 있는 실행 지역(CER)의 취소 코드만 확실히 실행됩니다.

### <a name="use-safehandle-to-avoid-resource-leaks"></a>리소스 누수를 방지 하기 위해 SafeHandle 사용

<xref:System.AppDomain> 언로드 시, 실행 중인 `finally` 블록 또는 종료자에 의존할 수 없으므로 <xref:System.IntPtr>, <xref:System.Runtime.InteropServices.HandleRef> 또는 비슷한 클래스가 아니라 <xref:System.Runtime.InteropServices.SafeHandle> 클래스를 통해 모든 운영 체제 리소스 액세스를 추상화하는 것이 중요합니다. 그러면 CLR이 <xref:System.AppDomain>이 손상되는 경우에도 사용하는 핸들을 닫고 추적할 수 있습니다.  <xref:System.Runtime.InteropServices.SafeHandle>에서는 CLR이 항상 실행하는 중요한 종료자를 사용합니다.

운영 체제 핸들은 생성된 순간부터 해제되는 순간까지 안전한 핸들에 저장됩니다.  핸들이 누출되도록 <xref:System.Threading.ThreadAbortException>이 발생할 수 있는 기간이 없습니다.  또한 플랫폼 호출에서 핸들을 참조-카운트합니다. 그러면 핸들의 수명을 면밀하게 추적할 수 있으므로, `Dispose`와 현재 핸들을 사용 중인 메서드 사이의 경합 상태에서 보안 문제가 발생하는 것을 방지할 수 있습니다.

현재 운영 체제 핸들을 정리만 하는 종료자가 있는 대부분의 클래스에는 더 이상 종료자가 필요하지 않습니다. 대신 종료자는 <xref:System.Runtime.InteropServices.SafeHandle> 파생 클래스에 있습니다.

<xref:System.Runtime.InteropServices.SafeHandle>은 <xref:System.IDisposable.Dispose%2A?displayProperty=nameWithType>의 대안이 아닙니다.  운영 체제 리소스를 명시적으로 삭제하면 여전히 리소스 경합과 성능 이점을 얻을 수 있습니다.  리소스를 명시적으로 삭제하지 않는 `finally` 블록은 완료될 때까지 실행되지 않을 수 있다는 점에 유의하세요.

<xref:System.Runtime.InteropServices.SafeHandle>을 사용하면 운영 체제 핸들에 상태 전달, 루틴 해제 또는 루프에서 핸들 집합 해제와 같은 핸들 해제 작업을 수행하는 고유 <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A> 메서드를 구현할 수 있습니다.  CLR에서는 이 메서드가 확실히 실행됩니다.  작성자는 모든 상황에서 핸들이 해제되도록 <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A>을 구현해야 합니다. 그러지 않으면 핸들이 누출되므로, 핸들과 연결된 네이티브 리소스가 누출되는 결과가 자주 초래됩니다. 따라서 <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A> 구현에서 호출 시 사용 가능하지 않은 리소스를 할당할 필요가 없도록 <xref:System.Runtime.InteropServices.SafeHandle> 파생 클래스를 구성하는 것이 중요합니다. 코드에서 이러한 실패를 처리하고 네이티브 핸들을 해제하는 계약을 완료할 수 있는 경우, <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A>의 구현에서 실패할 수 있는 메서드를 호출할 수 있습니다. <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A>에는 디버깅 용도의 <xref:System.Boolean> 반환 값이 있습니다. 리소스를 해제하지 못하게 하는 치명적인 오류가 발생하는 경우 이 값은 `false`로 설정될 수 있습니다. 그러면 [releaseHandleFailed](../debug-trace-profile/releasehandlefailed-mda.md) MDA가 활성화되어(사용된 경우) 문제를 파악하는 데 도움이 됩니다. 다른 방식으로 런타임에 영향을 주지 않습니다. <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A>는 동일한 리소스에 대해 다시 호출되지 않으므로 핸들이 누출됩니다.

<xref:System.Runtime.InteropServices.SafeHandle>은 특정 컨텍스트에서는 적절하지 않습니다.  <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A> 메서드는 <xref:System.GC> 종료자 스레드에서 실행될 수 있으므로, 특정 스레드에서 해제해야 하는 모든 핸들은 <xref:System.Runtime.InteropServices.SafeHandle>로 래핑하지 않아야 합니다.

런타임 호출 가능 래퍼(RCW)는 추가 코드 없이 CLR에서 정리할 수 있습니다.  플랫폼 호출을 사용하고 COM 개체를 `IUnknown*` 또는 <xref:System.IntPtr>로 처리하므로, RCW를 사용하도록 코드를 다시 작성해야 합니다.  <xref:System.Runtime.InteropServices.SafeHandle>은 관리되지 않는 릴리스 메서드가 관리 코드로 다시 호출될 수 있으므로 이 시나리오에는 적합하지 않을 수 있습니다.

#### <a name="code-analysis-rule"></a>코드 분석 규칙

<xref:System.Runtime.InteropServices.SafeHandle>을 사용하여 운영 체제 리소스를 캡슐화합니다. <xref:System.Runtime.InteropServices.HandleRef> 또는 <xref:System.IntPtr> 형식의 필드를 사용하지 마세요.

### <a name="ensure-finalizers-do-not-have-to-run-to-prevent-leaking-operating-system-resources"></a>운영 체제 리소스 누수를 방지 하기 위해 종료자를 실행 하지 않아도 되는지 확인 합니다.

종료자를 실행하지 않아도 중요한 운영 체제 리소스가 누출되지 않게 종료자를 신중하게 검토합니다.  애플리케이션이 안정된 상태로 실행되거나 SQL Server와 같은 서버가 종료될 때 수행되는 정상 <xref:System.AppDomain> 언로드와 달리, 갑작스러운 <xref:System.AppDomain> 언로드 중에는 개체가 종료되지 않습니다.  애플리케이션의 정확도는 보장할 수 없지만, 서버의 무결성은 누출되지 않는 리소스를 통해 유지 관리해야 하므로, 갑작스러운 언로드 시 리소스가 누출되지 않게 해야 합니다.  <xref:System.Runtime.InteropServices.SafeHandle>을 사용하여 운영 체제 리소스를 해제합니다.

### <a name="ensure-that-finally-clauses-do-not-have-to-run-to-prevent-leaking-operating-system-resources"></a>Finally 절을 실행 하 여 운영 체제 리소스 누수가 발생 하지 않도록 해야 합니다.

`finally` 절은 CER 외부에서는 실행되지 않을 수도 있으므로, 라이브러리 개발자가 관리되지 않는 리소스를 해제하는 데 `finally` 블록 내의 코드에 의존하지 않아야 합니다.  <xref:System.Runtime.InteropServices.SafeHandle>을 사용하는 것이 좋은 솔루션입니다.

#### <a name="code-analysis-rule"></a>코드 분석 규칙

운영 체제 리소스를 정리하는 데 `Finalize`가 아니라 <xref:System.Runtime.InteropServices.SafeHandle>을 사용합니다. <xref:System.IntPtr>을 사용하지 않습니다. <xref:System.Runtime.InteropServices.SafeHandle>을 사용하여 리소스를 캡슐화합니다. finally 절을 실행해야 하는 경우 CER에 둡니다.

### <a name="all-locks-should-go-through-existing-managed-locking-code"></a>모든 잠금은 기존 관리 되는 잠금 코드를 통과 해야 합니다.

스레드를 단지 중단하는 것이 아니라 <xref:System.AppDomain>을 손상시키는 경우를 파악하기 위해 CLR에서는 코드가 언제 잠금 상태인지를 알아야 합니다.  스레드를 중단하면 해당 스레드에서 조작하는 데이터가 일관되지 않은 상태가 될 수 있으므로 위험해질 수 있습니다. 따라서 전체 <xref:System.AppDomain>을 재활용해야 합니다.  잠금 상태를 파악하지 못하면 교착 상태나 잘못된 결과가 초래될 수 있습니다. <xref:System.Threading.Thread.BeginCriticalRegion%2A> 및 <xref:System.Threading.Thread.EndCriticalRegion%2A> 메서드를 사용하여 잠금 영역을 식별합니다.  이 메서드는 현재 스레드에만 적용되는 <xref:System.Threading.Thread> 클래스의 정적 메서드이므로, 한 스레드가 다른 스레드의 잠금 카운트를 편집하지 못하게 할 수 있습니다.

<xref:System.Threading.Monitor.Enter%2A> 및 <xref:System.Threading.Monitor.Exit%2A>에는 이 CLR 알림이 기본으로 제공되므로, 이러한 메서드를 사용하는 [lock 문](../../csharp/language-reference/keywords/lock-statement.md)뿐 아니라 이 알림을 사용하는 것이 좋습니다.

스핀 잠금 및 <xref:System.Threading.AutoResetEvent>와 같은 기타 잠금 메커니즘에서는 이러한 메서드를 호출하여 임계 영역으로 전환하고 있음을 CLR에 알려야 합니다.  이러한 메서드는 잠금을 사용하지 않습니다. 임계 영역에서 코드가 실행 중이며, 스레드를 중단하면 공유 상태가 일관되지 않게 될 수 있음을 CLR에 알립니다.  사용자 지정 <xref:System.Threading.ReaderWriterLock> 클래스와 같은 고유 잠금 형식을 정의한 경우 이러한 잠금 카운트 메서드를 사용합니다.

#### <a name="code-analysis-rule"></a>코드 분석 규칙

<xref:System.Threading.Thread.BeginCriticalRegion%2A> 및 <xref:System.Threading.Thread.EndCriticalRegion%2A>을 사용하여 모든 잠금을 표시하고 식별합니다. 루프에서 <xref:System.Threading.Interlocked.CompareExchange%2A>, <xref:System.Threading.Interlocked.Increment%2A> 및 <xref:System.Threading.Interlocked.Decrement%2A>를 사용하지 마세요.  이러한 메서드의 Win32 변형에 대한 플랫폼 호출을 수행하지 마세요.  루프에서 <xref:System.Threading.Thread.Sleep%2A>을 사용하지 마세요.  Volatile 필드를 사용하지 마세요.

### <a name="cleanup-code-must-be-in-a-finally-or-a-catch-block-not-following-a-catch"></a>정리 코드는 catch를 수행 하는 것이 아니라 finally 또는 catch 블록에 있어야 합니다.

정리 코드는 `catch` 블록을 수행하지 않아야 합니다. `finally` 또는 `catch` 블록 자체에 있어야 합니다. 이 방법은 정상적인 모범 사례여야 합니다. `finally` 블록은 예외가 throw되고 `try` 블록이 정상적으로 종료될 때 모두 동일한 코드를 실행하므로 일반적으로 사용이 선호됩니다.  예기치 않은 예외가 throw되는 경우(예: <xref:System.Threading.ThreadAbortException>) 정리 코드가 실행되지 않습니다.  누출을 방지하기 위해 `finally`에서 정리할 관리되지 않는 리소스는 <xref:System.Runtime.InteropServices.SafeHandle>로 래핑하는 것이 좋습니다.  C# `using` 키워드는 핸들 등의 개체를 삭제하는 데 효과적으로 사용할 수 있습니다.

<xref:System.AppDomain> 재활용을 통해 종료자 스레드에서 리소스를 정리할 수 있지만 정리 코드를 올바른 위치에 두는 것이 여전히 중요합니다. 스레드에서 잠금을 보유하지 않고 비동기 예외를 받는 경우 CLR에서 <xref:System.AppDomain>을 재활용할 필요 없이 스레드를 종료하려고 합니다.  리소스를 늦게 정리하는 것보다 빨리 정리하면 더 많은 리소스가 사용 가능하게 되므로 수명 관리가 향상됩니다. 일부 오류 코드 경로에 있는 파일의 핸들을 명시적으로 종료하는 경우가 아니면 <xref:System.Runtime.InteropServices.SafeHandle> 종료자가 정리할 때까지 기다립니다. 다음번에 코드를 실행할 때 종료자가 아직 실행되지 않았으면 똑같은 파일에 액세스하지 못할 수 있습니다.  따라서 정리 코드가 있고 제대로 작동하는지 확인하면 실패에서 더 깔끔하고 신속하게 복구할 수 있습니다. 그러나 필수는 아닙니다.

#### <a name="code-analysis-rule"></a>코드 분석 규칙

`catch` 다음에 있는 정리 코드는 `finally` 블록에 있어야 합니다. 삭제할 호출을 finally 블록에 둡니다. `catch` 블록은 throw 또는 rethrow로 종료되어야 합니다. 네트워크 연결 설정 여부를 감지하며 다수의 예외가 발생할 수 있는 코드에서와 같이 예외가 발생할 수 있지만, 정상 상황에서 다수의 예외를 catch해야 하는 코드에서는 성공 여부를 확인하기 위해 코드를 테스트해야 한다고 표시해야 합니다.

### <a name="process-wide-mutable-shared-state-between-application-domains-should-be-eliminated-or-use-a-constrained-execution-region"></a>응용 프로그램 도메인 간의 프로세스 차원의 변경 가능 공유 상태는 제거 하거나 제약이 있는 실행 영역을 사용 해야 합니다.

소개에 설명된 것처럼 애플리케이션 도메인 간에 프로세스 전체 공유 상태를 안정되게 모니터하는 관리 코드를 작성하기는 매우 어려울 수 있습니다.  프로세스 전체 공유 상태는 Win32 코드, CLR 내부 또는 원격을 사용하여 관리 코드 내에서 애플리케이션 도메인 간에 공유하는 일종의 데이터 구조체입니다.  변경할 수 있는 공유 상태는 관리 코드에서 올바르게 작성하기가 매우 어려우며, 정적 공유 상태를 작성할 때는 상당한 주의를 기울여야 합니다.  프로세스 전체 또는 컴퓨터 전체 공유 상태가 있으면 제거 방법을 찾거나 제약이 있는 실행 지역(CER)을 사용하여 공유 상태를 보호합니다.  공유 상태의 라이브러리를 식별하여 정정하지 않으면 정리 <xref:System.AppDomain> 언로드가 필요한 호스트(예: SQL Server)를 중단시킬 수 있습니다.

코드에서 COM 개체를 사용하는 경우 애플리케이션 도메인 간에 COM 개체를 공유하지 않게 하세요.

### <a name="locks-do-not-work-process-wide-or-between-application-domains"></a>잠금은 프로세스 전체 또는 응용 프로그램 도메인 간에 작동 하지 않습니다.

이전에는 <xref:System.Threading.Monitor.Enter%2A> 및 [lock 문](../../csharp/language-reference/keywords/lock-statement.md)을 사용하여 전역 프로세스 잠금을 만들었습니다.  예를 들어, 이 동작은 <xref:System.AppDomain> agile 클래스에서 잠글 때 발생합니다(예: 비공유 어셈블리의 <xref:System.Type> 인스턴스, <xref:System.Threading.Thread> 개체, 인턴 지정 문자열 및 원격을 사용하여 애플리케이션 도메인 간에 공유하는 문자열).  이러한 잠금은 더 이상 프로세스 전체에 적용되지 않습니다.  프로세스 전체 애플리케이션 도메인 간 잠금의 현재 상태를 파악하려면 잠금 내의 코드에서 디스크의 파일 또는 데이터베이스와 같은 외부 영구 리소스를 사용하는지 확인합니다.

<xref:System.AppDomain>에서 잠금을 사용하면 보호된 코드에서 외부 리소스를 사용하는 경우 문제가 발생할 수 있습니다. 해당 코드가 여러 애플리케이션 도메인에서 동시에 실행될 수 있기 때문입니다.  그러면 한 로그 파일에 쓰거나 전체 프로세스를 위해 소켓에 바인딩할 때 문제가 될 수 있습니다.  이러한 변경은 명명된 <xref:System.Threading.Mutex> 또는 <xref:System.Threading.Semaphore> 인스턴스를 사용하는 방법 외에 관리 코드를 사용하여 프로세스-전역 잠금을 얻기가 쉽지 않다는 것을 나타냅니다.  두 애플리케이션 도메인에서 동시에 실행되지 않는 코드를 만들거나 <xref:System.Threading.Mutex> 또는 <xref:System.Threading.Semaphore> 클래스를 사용합니다.  기존 코드를 변경할 수 없으면 이 동기화를 달성하는 데 Win32 명명된 뮤텍스를 사용하지 마세요. 파이버 모드에서 실행하면 동일한 운영 체제 스레드가 뮤텍스를 확보하고 해제하지 못할 수도 있기 때문입니다.  비관리 코드를 사용하여 잠금을 동기화하는 대신 CLR에서 알고 있는 방식으로 코드 잠금을 동기화하려면 관리되는 <xref:System.Threading.Mutex> 클래스 또는 명명된 <xref:System.Threading.ManualResetEvent>, <xref:System.Threading.AutoResetEvent> 또는 <xref:System.Threading.Semaphore>를 사용해야 합니다.

#### <a name="avoid-locktypeofmytype"></a>lock(typeof(MyType)) 방지

모든 애플리케이션 도메인 간에 공유되는 코드 복사본이 하나뿐인 공유 어셈블리의 개인 및 공용 <xref:System.Type> 개체도 문제를 초래합니다.  공유 어셈블리의 경우 <xref:System.Type> 인스턴스는 프로세스당 하나뿐입니다. 즉, 여러 애플리케이션 도메인에서 똑같은 <xref:System.Type> 인스턴스를 공유합니다.  <xref:System.Type> 인스턴스에서 잠금을 사용하면 단지 <xref:System.AppDomain>만이 아니라 전체 프로세스에 영향을 미치는 잠금을 사용합니다.  하나의 <xref:System.AppDomain>이 <xref:System.Type> 개체에서 잠금을 사용하면 해당 스레드가 갑자기 중단되고 잠금을 릴리스하지 않습니다.  그러면 이 잠금으로 인해 다른 애플리케이션 도메인이 교착 상태가 될 수 있습니다.

정적 메서드에서 잠금을 사용하려면 정적 내부 동기화 개체를 코드에 추가하는 것이 좋은 방법입니다.  개체가 하나 있으면 클래스 생성자에서 초기화할 수 있지만, 없으면 다음과 같이 초기화할 수 있습니다.

```csharp
private static Object s_InternalSyncObject;
private static Object InternalSyncObject
{
    get
    {
        if (s_InternalSyncObject == null)
        {
            Object o = new Object();
            Interlocked.CompareExchange(
                ref s_InternalSyncObject, o, null);
        }
        return s_InternalSyncObject;
    }
}
```

잠금을 사용할 때 `InternalSyncObject` 속성을 사용하여 잠글 개체를 가져옵니다.  클래스 생성자에서 내부 동기화 개체를 초기화한 경우 이 속성을 사용하지 않아도 됩니다.  이중 검사 잠금 초기화 코드는 다음 예와 같아야 합니다.

```csharp
public static MyClass SingletonProperty
{
    get
    {
        if (s_SingletonProperty == null)
        {
            lock(InternalSyncObject)
            {
                // Do not use lock(typeof(MyClass))
                if (s_SingletonProperty == null)
                {
                    MyClass tmp = new MyClass(…);
                    // Do all initialization before publishing
                    s_SingletonProperty = tmp;
                }
            }
        }
        return s_SingletonProperty;
    }
}
```

#### <a name="a-note-about-lockthis"></a>잠금에 대 한 참고 사항 (this)

공개적으로 액세스할 수 있는 개별 개체에서는 일반적으로 잠금을 사용할 수 있습니다.  그러나 개체가 전체 하위 시스템에서 교착 상태를 초래할 수 있는 단일 개체인 경우에는 추가로 위의 디자인 패턴을 사용해 보세요.  예를 들어, 한 <xref:System.Security.SecurityManager> 개체의 잠금으로 인해 <xref:System.AppDomain>에 교착 상태가 발생할 수 있으므로, 전체 <xref:System.AppDomain>을 사용할 수 없게 됩니다. 공개적으로 액세스할 수 있는 이 형식의 개체에서 잠금을 사용하지 않는 것이 좋은 방법입니다.  그러나 개별 컬렉션 또는 배열의 잠금은 일반적으로 문제를 초래하지 않아야 합니다.

#### <a name="code-analysis-rule"></a>코드 분석 규칙

애플리케이션 도메인 간에 사용할 수 있거나 엄격한 ID 규칙이 없는 형식에서는 잠금을 사용하지 마세요. <xref:System.Type>, <xref:System.Reflection.MethodInfo>, <xref:System.Reflection.PropertyInfo>, <xref:System.String>, <xref:System.ValueType>, <xref:System.Threading.Thread> 또는 <xref:System.MarshalByRefObject>에서 파생된 개체에서는 <xref:System.Threading.Monitor.Enter%2A>를 호출하지 마세요.

### <a name="remove-gckeepalive-calls"></a>GC를 제거 합니다. KeepAlive 호출

상당한 양의 기존 코드에서<xref:System.GC.KeepAlive%2A>를 사용해야 하지만 그렇지 않거나, 사용이 적절하지 않을 때 사용합니다.  <xref:System.Runtime.InteropServices.SafeHandle>로 변환한 후에는 클래스에서 <xref:System.GC.KeepAlive%2A>를 호출하지 않아도 되며, 종료자가 없지만 <xref:System.Runtime.InteropServices.SafeHandle>을 사용하여 운영 체제 핸들을 종료한다고 가정합니다.  <xref:System.GC.KeepAlive%2A>에 대한 호출을 유지하는 데 따른 성능 저하는 무시할 수 있지만, <xref:System.GC.KeepAlive%2A>에 대한 호출이 필요하거나 더 이상 존재하지 않는 수명 문제를 해결하는 데 충분하다는 인식 때문에 코드를 유지하기가 더 어려워집니다.  그러나 COM interop CLR 호출 가능 래퍼(RCW)를 사용할 때 <xref:System.GC.KeepAlive%2A>가 여전히 코드에 필요합니다.

#### <a name="code-analysis-rule"></a>코드 분석 규칙

<xref:System.GC.KeepAlive%2A>를 제거합니다.

### <a name="use-the-hostprotection-attribute"></a>HostProtection 특성 사용

<xref:System.Security.Permissions.HostProtectionAttribute>(HPA)에서는 호스트 보호 요구 사항을 판별하기 위해 선언적 보호 작업 사용을 제공하므로, 호스트가 완전히 신뢰할 수 있는 코드에서도 SQL Server용 <xref:System.Environment.Exit%2A> 또는 <xref:System.Windows.Forms.MessageBox.Show%2A>와 같이 지정된 호스트에 적합하지 않은 특정 호스트를 호출하지 못하게 방지할 수 있습니다.

HPA는 공용 언어 런타임을 호스트하고 SQL Server와 같은 호스트 보호를 구현하는 관리되지 않는 애플리케이션에서만 적용됩니다. 적용되면 보안 작업에서 클래스 또는 메서드가 노출하는 호스트 리소스를 기반으로 링크 요구 사항을 만듭니다. 호스트에서 보호되지 않는 서버나 클라이언트 애플리케이션에서 코드가 실행되면 “evaporates” 특성이 감지되지 않으므로 적용되지 않습니다.

> [!IMPORTANT]
> 이 특성은 보안 동작이 아니라 호스트별 프로그래밍 모델 지침을 적용하는 데 사용합니다.  링크 요구 사항을 사용하여 프로그래밍 모델 요구 사항을 만족하는지 확인하지만 <xref:System.Security.Permissions.HostProtectionAttribute>는 보안 권한이 아닙니다.

호스트에 프로그래밍 모델 요구 사항이 없으면 링크 요구가 발생하지 않습니다.

이 특성을 사용하여 다음을 식별합니다.

- 호스트 프로그래밍 모델에 적합하지 않지만 달리 유해하지 않은 메서드 또는 클래스.

- 호스트 프로그래밍 모델에 적합하지 않으며 서버 관리 사용자 코드를 불안정하게 만드는 메서드 또는 클래스.

- 호스트 프로그래밍 모델에 적합하지 않으며 서버 프로세스 자체를 불안정하게 만드는 메서드 또는 클래스.

> [!NOTE]
> 호스트 보호 환경에서 실행할 수 있는 응용 프로그램에서 호출할 클래스 라이브러리를 만드는 경우 <xref:System.Security.Permissions.HostProtectionResource> 리소스 범주를 노출하는 멤버에 이 특성을 적용해야 합니다. 이 특성과 함께 .NET Framework 클래스 라이브러리 멤버를 사용하면 즉각적인 호출자만 검사하게 됩니다.  사용자의 라이브러리 멤버도 이와 동일한 방식으로 즉각적인 호출자 검사만 수행해야 합니다.

<xref:System.Security.Permissions.HostProtectionAttribute>에 HPA에 대한 자세한 내용이 있습니다.

#### <a name="code-analysis-rule"></a>코드 분석 규칙

SQL Server의 경우 동기화 또는 스레딩을 소개하는 데 사용한 모든 메서드는 HPA를 사용하여 식별해야 합니다. 여기에는 상태를 공유하거나 동기화되거나 외부 프로세스를 관리하는 메서드가 포함됩니다. SQL Server에 영향을 주는 <xref:System.Security.Permissions.HostProtectionResource> 값은 <xref:System.Security.Permissions.HostProtectionResource.SharedState>, <xref:System.Security.Permissions.HostProtectionResource.Synchronization> 및 <xref:System.Security.Permissions.HostProtectionResource.ExternalProcessMgmt>입니다. 그러나 SQL에 영향을 미치는 리소스를 사용하는 메서드뿐 아니라 <xref:System.Security.Permissions.HostProtectionResource>를 노출하는 모든 메서드를 HPA를 통해 식별해야 합니다.

### <a name="do-not-block-indefinitely-in-unmanaged-code"></a>비관리 코드에서 무기한 차단 안 함

관리 코드가 아니라 비관리 코드에서 차단하면 CLR에서 스레드를 중단할 수 없으므로 서비스 거부 공격이 발생할 수 있습니다.  스레드가 차단되면 극도로 안전하지 않은 작업을 수행하지 않고 CLR에서 <xref:System.AppDomain>을 언로드하는 것을 방지할 수 있습니다.  Windows 동기화 기본 형식을 사용 하 여 차단 하는 것은 허용 되지 않는 항목의 명확한 예입니다.  가능한 경우 소켓 `ReadFile` 에서 호출을 차단 하는 것은 피해 야 합니다. 즉, Windows API가 시간 초과와 같은 작업에 대 한 메커니즘을 제공 해야 합니다.

네이티브를 호출하는 모든 메서드는 적절한 시간 제한 내에 Win32 호출을 사용해야 합니다.  사용자가 시간 제한을 지정할 수 있으면 특정 보안 권한이 없이는 무한 시간을 지정할 수 없어야 합니다.  참고로 메서드를 10초가 넘게 차단할 경우 시간 제한을 지원하는 버전을 사용하거나 추가 CLR 지원이 필요합니다.

다음은 문제가 있는 Api의 몇 가지 예입니다.  파이프(익명 파이프 및 명명된 파이프 모두)는 시간 제한을 지정하여 만들 수 있지만, 코드에서 NMPWAIT_WAIT_FOREVER를 사용하여 `CreateNamedPipe`와 `WaitNamedPipe`를 호출하지 않게 지정해야 합니다.  또한 시간 제한이 지정된 경우에도 예기치 않은 차단이 발생할 수 있습니다.  익명 파이프에서 수행되는 `WriteFile` 호출은 모든 바이트를 작성할 때까지 차단됩니다. 즉, 버퍼에 읽지 않은 데이터가 있으면 판독기에서 파이프 버퍼의 공간을 확보할 때까지 `WriteFile` 호출이 차단됩니다.  소켓에서는 시간 제한 메커니즘을 준수하는 API를 항상 사용해야 합니다.

#### <a name="code-analysis-rule"></a>코드 분석 규칙

비관리 코드에서 시간 제한 없이 차단하는 것은 서비스 거부 공격입니다. `WaitForSingleObject`, `WaitForSingleObjectEx`, `WaitForMultipleObjects`, `MsgWaitForMultipleObjects` 및 `MsgWaitForMultipleObjectsEx`에 대한 플랫폼 호출을 수행하지 마세요.  NMPWAIT_WAIT_FOREVER를 사용하지 마세요.

### <a name="identify-any-sta-dependent-features"></a>모든 STA 종속 기능 식별

COM STA(단일 스레드 아파트)를 사용하는 코드를 식별합니다.  STA는 SQL Server 프로세스에서 비활성화됩니다.  성능 카운터 또는 클립보드와 같이 `CoInitialize`를 사용하는 기능은 SQL Server에서 비활성화되어야 합니다.

### <a name="ensure-finalizers-are-free-of-synchronization-problems"></a>종료 자가 동기화 문제가 없는지 확인

향후 버전의 .NET Framework에 여러 종료자 스레드가 있을 수 있습니다. 즉, 동일한 형식의 여러 다른 인스턴스에 대해 종료자가 동시에 실행됩니다.  스레드로부터 완전히 안전하지 않아도 됩니다. 가비지 수집기에서는 하나의 스레드만 지정된 개체 인스턴스에 대해 종료자를 실행하도록 보장합니다.  그러나 여러 다른 개체 인스턴스에서 동시에 실행될 때 경합 상태와 교착 상태를 방지하도록 종료자를 코딩해야 합니다.  종료자에서 로그 파일에 쓰기와 같이 외부 상태를 사용하는 경우 스레딩 문제를 처리해야 합니다.  종료에서 스레드 보안을 제공할 것으로 의존하지 마세요. 스레드 로컬 스토리지, 관리 또는 네이티브를 사용하여 종료자 스레드에 상태를 저장하지 마세요.

#### <a name="code-analysis-rule"></a>코드 분석 규칙

종료자에 동기화 문제가 없어야 합니다. 종료자에서 정적 변경 가능 상태를 사용하지 마세요.

### <a name="avoid-unmanaged-memory-if-possible"></a>가능 하면 관리 되지 않는 메모리 방지

운영 체제 핸들과 마찬가지로 관리되지 않는 메모리는 누출될 수 있습니다. 가능하면 [stackalloc](../../csharp/language-reference/operators/stackalloc.md)를 사용하는 스택의 메모리, 고정된 관리 개체(예: [fixed 문](../../csharp/language-reference/keywords/fixed-statement.md)) 또는 byte[]를 사용하는 <xref:System.Runtime.InteropServices.GCHandle>를 사용합니다. 결국 <xref:System.GC>에서 정리합니다. 그러나 관리되지 않는 메모리를 할당해야 하는 경우 <xref:System.Runtime.InteropServices.SafeHandle>에서 파생되는 클래스를 사용하여 메모리 할당을 래핑합니다.

<xref:System.Runtime.InteropServices.SafeHandle>이 적합하지 않은 경우가 하나 이상 있습니다. 메모리를 할당하거나 해제하는 COM 메서드 호출의 경우 한 DLL에서 `CoTaskMemAlloc`를 통해 메모리를 할당한 다음 다른 DLL에서 `CoTaskMemFree`로 메모리를 해제하는 것이 일반적입니다.  이러한 위치에서 <xref:System.Runtime.InteropServices.SafeHandle>을 사용하면 다른 DLL에서 메모리의 수명을 제어하도록 허용하지 않고 관리되지 않는 메모리의 수명을 <xref:System.Runtime.InteropServices.SafeHandle>의 수명과 연결하려고 하므로 적합하지 않습니다.

### <a name="review-all-uses-of-catchexception"></a>Catch의 모든 사용 검토 (예외)

하나의 특정 예외가 아니라 모든 예외를 catch하는 Catch 블록은 이제 비동기 예외도 catch합니다. 모든 catch(Exception) 블록을 검사하여 건너뛸 수 있는 중요한 리소스 해제 또는 취소 코드가 없으며, <xref:System.Threading.ThreadAbortException>, <xref:System.StackOverflowException> 또는 <xref:System.OutOfMemoryException>을 처리하는 catch 블록 자체에 잘못된 동작이 없는지 확인합니다.  이 코드에서는 특정 예외만 볼 수 있거나 예외가 발생할 때마다 단 하나의 특정 이유로 인해 실패한다고 가정하거나 로깅 중일 수 있습니다.  <xref:System.Threading.ThreadAbortException>을 포함하도록 이러한 가정을 업데이트해야 합니다.

문자열 형식 메서드의 <xref:System.FormatException>과 같이 예외가 throw될 것으로 예상하는 특정 형식의 예외를 catch하도록 모든 예외를 catch하는 위치를 모두 변경합니다.  그러면 catch 블록이 예기치 않은 예외에 대해 실행되지 않으며 예기치 않은 예외를 catch하여 코드에서 버그를 숨기지 않게 할 수 있습니다.  일반적으로 규칙은 라이브러리 코드의 예외를 처리하지 않습니다(예외를 catch해야 하는 코드가 호출하는 코드의 디자인 결함을 나타낼 수 있음).  경우에 따라 더 많은 데이터를 제공하기 위해 예외를 catch하여 여러 다른 예외 형식을 throw할 수 있습니다.  이 경우 중첩 예외를 사용하면 새로운 예외의 <xref:System.Exception.InnerException%2A> 속성에 실패의 실제 이유를 저장할 수 있습니다.

#### <a name="code-analysis-rule"></a>코드 분석 규칙

관리 코드에서 모든 개체를 catch하거나 모든 예외를 catch하는 모든 catch 블록을 검토합니다.  에서 C#이 `catch` 는 {} 및 의플래그를{}나타냅니다. `catch(Exception)`  예외 형식을 매우 구체적으로 만들거나 코드를 검토하여 예기치 않은 예외 형식을 catch하는 경우 잘못된 방식으로 작동하지 않게 합니다.

### <a name="do-not-assume-a-managed-thread-is-a-win32-thread--it-is-a-fiber"></a>관리 되는 스레드가 Win32 스레드 라고 가정 하지 않음-파이버입니다.

관리되는 스레드 로컬 스토리지를 사용하는 것은 가능하지만, 관리되지 않는 스레드 로컬 스토리지를 사용하지 않거나 코드가 현재 운영 체제 스레드에서 다시 실행된다고 가정할 수 있습니다. 스레드 로캘과 같은 설정은 변경하지 않습니다. 플랫폼 호출을 통해 `InitializeCriticalSection` 또는 `CreateMutex`를 호출하지 마세요. 잠금을 시작하는 운영 체제 스레드가 잠금을 종료해야 하기 때문입니다. 파이버를 사용할 때는 해당되지 않으므로, Win32 중요 섹션과 뮤텍스를 SQL에서 직접 사용할 수 없습니다.  관리되는 <xref:System.Threading.Mutex> 클래스에서는 이러한 스레드 선호도 문제를 처리하지 않습니다.

관리되는 스레드 로컬 스토리지 및 스레드의 현재 UI 문화권을 포함하여 대부분의 상태를 관리되는 <xref:System.Threading.Thread> 개체에서 안전하게 사용할 수 있습니다. <xref:System.ThreadStaticAttribute>도 사용할 수 있습니다. 그러면 현재 관리되는 스레드에서만 기존 정적 변수의 값에 액세스할 수 있습니다(이는 CLR에서 파이버 로컬 스토리지를 수행하는 또 다른 방법임). 프로그래밍 모델 때문에 SQL에서 실행할 때 현재 스레드의 문화권을 변경할 수 없습니다.

#### <a name="code-analysis-rule"></a>코드 분석 규칙

SQL Server는 파이버 모드로 실행됩니다. 스레드 로컬 스토리지를 사용하지 마세요. `TlsAlloc`, `TlsFree`, `TlsGetValue` 및 `TlsSetValue.`에 대한 플랫폼 호출을 수행하지 마세요.

### <a name="let-sql-server-handle-impersonation"></a>SQL Server 가장을 처리할 수 있습니다.

가장은 스레드 수준에서 작동하고 SQL은 파이버 모드에서 실행될 수 있으므로 관리 코드에서는 사용자를 가장하지 않아야 하며 `RevertToSelf`를 호출하지 않아야 합니다.

#### <a name="code-analysis-rule"></a>코드 분석 규칙

SQL Server 핸들 가장 허용 `RevertToSelf`, `ImpersonateAnonymousToken`, `DdeImpersonateClient`, `ImpersonateDdeClientWindow`, `ImpersonateLoggedOnUser`, `ImpersonateNamedPipeClient`, `ImpersonateSelf`, `RpcImpersonateClient`, `RpcRevertToSelf`, `RpcRevertToSelfEx` 또는 `SetThreadToken`을 사용하지 마세요.

### <a name="do-not-call-threadsuspend"></a>Thread:: Suspend를 호출 하지 마십시오.

스레드를 일시 중단하는 기능은 간단한 작업처럼 보일 수 있지만 교착 상태를 초래할 수 있습니다.  두 번째 스레드가 잠금을 보유하는 스레드를 일시 중단한 다음 동일한 잠금을 사용하려고 하면 교착 상태가 발생합니다.  <xref:System.Threading.Thread.Suspend%2A>는 현재 보안, 클래스 로드, 원격 및 리플렉션을 방해할 수 있습니다.

#### <a name="code-analysis-rule"></a>코드 분석 규칙

<xref:System.Threading.Thread.Suspend%2A>를 호출하지 마세요. 대신 <xref:System.Threading.Semaphore> 또는 <xref:System.Threading.ManualResetEvent>와 같은 실제 동기화 기본 형식을 사용합니다.

### <a name="protect-critical-operations-with-constrained-execution-regions-and-reliability-contracts"></a>제약이 있는 실행 영역 및 안정성 계약을 사용 하 여 중요 한 작업 보호

공유 상태를 업데이트하거나 완벽한 성공 또는 실패 여부를 판별해야 하는 복잡한 작업을 수행할 때 제약이 있는 실행 영역(CER)으로 보호합니다. 그러면 갑작스러운 스레드 중단 또는 갑작스러운 <xref:System.AppDomain> 언로드 시에도 코드가 항상 실행됩니다.

CER은 <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions%2A>에 대한 호출 바로 다음에 오는 특정 `try/finally` 블록입니다.

그러면 `try` 블록을 실행하기 전에 finally 블록의 모든 코드를 준비하도록 Just-In-Time 컴파일러에 지시합니다. 그러면 finally 블록의 코드가 빌드되고 경우에 상관없이 실행될 수 있습니다. CER에서 `try` 블록이 비어 있는 경우가 드물지 않습니다. CER을 사용하여 비동기 스레드 중단 및 메모리 부족 예외로부터 보호합니다. 매우 복잡한(deep) 코드의 스택 오버플로를 추가로 처리하는 CER 양식은 <xref:System.Runtime.CompilerServices.RuntimeHelpers.ExecuteCodeWithGuaranteedCleanup%2A>을 참조하세요.

## <a name="see-also"></a>참조

- <xref:System.Runtime.ConstrainedExecution>
- [SQL Server 프로그래밍 및 호스트 보호 특성](sql-server-programming-and-host-protection-attributes.md)
