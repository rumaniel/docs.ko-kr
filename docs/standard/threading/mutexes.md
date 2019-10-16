---
title: 뮤텍스
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- wait handles
- threading [.NET Framework], Mutex class
- Mutex class, about Mutex class
- threading [.NET Framework], cross-process synchronization
ms.assetid: 9dd06e25-12c0-4a9e-855a-452dc83803e2
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 8b2edf1f06873796bd63fceaca9a4bb99e509589
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69910339"
---
# <a name="mutexes"></a>뮤텍스
<xref:System.Threading.Mutex> 개체를 사용하여 리소스에 대한 전용 액세스를 제공할 수 있습니다. <xref:System.Threading.Mutex> 클래스는 <xref:System.Threading.Monitor> 클래스보다 많은 시스템 리소스를 사용하지만 애플리케이션 도메인 경계를 넘어 마샬링될 수 있으며 여러 대기와 함께 사용될 수 있고 서로 다른 프로세스에서 스레드를 동기화하는 데 사용될 수 있습니다. 관리되는 동기화 메커니즘의 비교는 [동기화 기본 형식 개요](../../../docs/standard/threading/overview-of-synchronization-primitives.md)를 참조하세요.  
  
 코드 예제는 <xref:System.Threading.Mutex.%23ctor%2A> 생성자에 대한 참조 설명서를 참조하세요.  
  
## <a name="using-mutexes"></a>뮤텍스 사용  
 스레드는 소유권을 요청하는 뮤텍스의 <xref:System.Threading.WaitHandle.WaitOne%2A> 메서드를 호출합니다. 호출은 뮤텍스를 사용할 수 있거나 선택적 시간 제한 간격이 경과할 때까지 차단합니다. 뮤텍스의 상태는 스레드가 소유하지 않는 경우 신호를 받습니다.  
  
 스레드는 해당 <xref:System.Threading.Mutex.ReleaseMutex%2A> 메서드를 호출하여 뮤텍스를 해제합니다. 뮤텍스에는 스레드 선호도가 있습니다. 즉, 뮤텍스를 소유하는 스레드에 의해서만 해제될 수 있습니다. 스레드가 소유하지 않는 뮤텍스를 해제하는 경우 스레드에서 <xref:System.ApplicationException>이 throw됩니다.  
  
 <xref:System.Threading.Mutex> 클래스는 <xref:System.Threading.WaitHandle>에서 파생되므로 <xref:System.Threading.WaitHandle>의 정적 <xref:System.Threading.WaitHandle.WaitAll%2A> 또는 <xref:System.Threading.WaitHandle.WaitAny%2A> 메서드를 호출하여 다른 대기 핸들과 결합하여 <xref:System.Threading.Mutex>의 소유권을 요청할 수도 있습니다.  
  
 스레드가 <xref:System.Threading.Mutex>를 소유하는 경우 해당 스레드는 해당 실행을 차단하지 않고 반복되는 대기 요청 호출에서 동일한 <xref:System.Threading.Mutex>를 지정할 수 있지만 소유권을 해제하는 횟수만큼 <xref:System.Threading.Mutex>를 해제해야 합니다.  
  
## <a name="abandoned-mutexes"></a>중단된 뮤텍스  
 스레드가 <xref:System.Threading.Mutex>를 해제하지 않고 종료하는 경우 뮤텍스는 중단되도록 명령됩니다. 뮤텍스가 보호하는 리소스가 일관성 없는 상태로 남을 수도 있으므로 이는 종종 심각한 프로그래밍 오류를 나타냅니다. .NET Framework 버전 2.0에서 <xref:System.Threading.AbandonedMutexException>은 뮤텍스를 획득하는 다음 스레드에서 throw됩니다.  
  
> [!NOTE]
> .NET Framework 버전 1.0 및 1.1에서 중단된 <xref:System.Threading.Mutex>는 신호 받음 상태로 설정되고 다음 대기 스레드는 소유권을 가져옵니다. 대기 중인 스레드가 없는 경우 <xref:System.Threading.Mutex>는 신호 받음 상태로 유지됩니다. 예외가 throw되지 않습니다.  
  
 시스템 차원 뮤텍스의 경우 중단된 뮤텍스는 애플리케이션이 갑자기 종료되었음을 나타낼 수 있습니다(예: Windows 작업 관리자를 사용하여).  
  
## <a name="local-and-system-mutexes"></a>로컬 및 시스템 뮤텍스  
 뮤텍스는 로컬 뮤텍스 및 명명된 시스템 뮤텍스로 두 가지 유형입니다. 이름을 허용하는 생성자를 사용하여 <xref:System.Threading.Mutex> 개체를 만드는 경우 해당 이름의 운영 체제 개체에 연결됩니다. 명명된 시스템 뮤텍스는 운영 체제 전체에서 볼 수 있으며 프로세스 작업을 동기화하는 데 사용될 수 있습니다. 동일한 명명된 시스템 뮤텍스를 나타내는 여러 <xref:System.Threading.Mutex> 개체를 만들 수 있으며 <xref:System.Threading.Mutex.OpenExisting%2A> 메서드를 사용하여 기존 명명된 시스템 뮤텍스를 열 수 있습니다.  
  
 로컬 뮤텍스는 프로세스 내에만 존재합니다. 로컬 <xref:System.Threading.Mutex> 개체에 대한 참조가 있는 프로세스의 모든 스레드에서 사용할 수 있습니다. 각 <xref:System.Threading.Mutex> 개체는 별도 로컬 뮤텍스입니다.  
  
### <a name="access-control-security-for-system-mutexes"></a>시스템 뮤텍스에 대한 액세스 제어 보안  
 .NET Framework 버전 2.0은 명명된 시스템 개체에 대해 Windows 액세스 제어 보안을 쿼리 및 설정하는 기능을 제공합니다. 시스템 개체는 전역적이며 따라서 코드에서 잠글 수 있으므로 생성 순간부터 시스템 뮤텍스를 보호하는 것이 좋습니다.  
  
 뮤텍스의 액세스 제어 보안에 대한 자세한 내용은 <xref:System.Security.AccessControl.MutexSecurity> 및 <xref:System.Security.AccessControl.MutexAccessRule> 클래스, <xref:System.Security.AccessControl.MutexRights> 열거형, <xref:System.Threading.Mutex> 클래스의 <xref:System.Threading.Mutex.GetAccessControl%2A>, <xref:System.Threading.Mutex.SetAccessControl%2A> 및 <xref:System.Threading.Mutex.OpenExisting%2A> 메서드, <xref:System.Threading.Mutex.%23ctor%28System.Boolean%2CSystem.String%2CSystem.Boolean%40%2CSystem.Security.AccessControl.MutexSecurity%29> 생성자를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

- <xref:System.Threading.Mutex?displayProperty=nameWithType>
- <xref:System.Threading.Mutex.%23ctor%2A?displayProperty=nameWithType>
- <xref:System.Security.AccessControl.MutexSecurity?displayProperty=nameWithType>
- <xref:System.Security.AccessControl.MutexAccessRule?displayProperty=nameWithType>
- <xref:System.Threading.Monitor?displayProperty=nameWithType>
- [스레딩 개체 및 기능](threading-objects-and-features.md)
- [스레드 및 스레딩](threads-and-threading.md)
- [스레딩](index.md)
