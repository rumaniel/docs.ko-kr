---
title: 관리되는 스레드의 예외
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- unhandled exceptions,in managed threads
- threading [.NET Framework],unhandled exceptions
- threading [.NET Framework],exceptions in managed threads
- managed threading
ms.assetid: 11294769-2e89-43cb-890e-ad4ad79cfbee
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 689ee44980a4a41b6d46ed9b68306c1b08c49586
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69960070"
---
# <a name="exceptions-in-managed-threads"></a>관리되는 스레드의 예외
NET Framework 버전 2.0부터 공용 언어 런타임을 통해 스레드에 있는 대부분의 처리되지 않은 예외가 정상적으로 진행됩니다. 즉, 대부분의 경우에서 처리되지 않은 예외는 애플리케이션을 종료시킵니다.  
  
> [!NOTE]
> 이 내용은 .NET Framework 버전 1.0 및 1.1과 비교하여 크게 달라진 것으로, 여러 처리되지 않은 예외(예: 스레드 풀 스레드의 처리되지 않은 예외)에 백업을 제공합니다. 이 항목의 뒷부분에 나오는 [이전 버전의 변경 내용](#ChangeFromPreviousVersions)을 참조하세요.  
  
 공용 언어 런타임은 프로그램 흐름을 제어하는 데 사용되는 처리되지 않은 예외에 백업을 제공합니다.  
  
- <xref:System.Threading.Thread.Abort%2A>가 호출되었으므로 스레드에서 <xref:System.Threading.ThreadAbortException>이 throw됩니다.  
  
- 스레드가 실행 중인 애플리케이션 도메인이 언로드되는 중이므로 스레드에서 <xref:System.AppDomainUnloadedException>이 throw됩니다.  
  
- 공용 언어 런타임 또는 호스트 프로세스에서 내부 예외를 throw하여 스레드를 종료합니다.  
  
 이러한 예외가 공용 언어 런타임에서 만든 스레드에서 처리되지 않는 경우 해당 예외는 스레드를 종료시키지만, 공용 언어 런타임에서 해당 예외가 계속 진행되도록 허용하지 않습니다.  
  
 이러한 예외가 주 스레드나 비관리 코드에서 런타임으로 들어간 스레드에서 처리되지 않는 경우 해당 예외는 정상적으로 진행되고 애플리케이션이 종료됩니다.  
  
> [!NOTE]
> 관리 코드가 예외 처리기를 설치하기 전에 런타임은 처리되지 않은 예외를 throw할 수 있습니다. 관리 코드가 이러한 예외를 처리하지 못하더라도 예외는 정상적으로 진행될 수 있습니다.  
  
## <a name="exposing-threading-problems-during-development"></a>개발하는 동안 스레딩 문제 노출  
 애플리케이션이 종료되지 않고 스레드에 오류가 발생할 수 있는 경우 심각한 프로그래밍 문제를 발견하지 못할 수 있습니다. 이것은 확장된 기간 동안 실행되는 서비스와 기타 애플리케이션에 특정된 문제입니다. 스레드에 오류가 발생하면 프로그램 상태가 서서히 손상됩니다. 애플리케이션 성능이 저하되거나 애플리케이션이 응답하지 않을 수 있습니다.  
  
 운영 체제가 응용 프로그램을 종료시킬 때까지 스레드의 처리되지 않은 예외가 정상적으로 진행되도록 허용하면 개발이나 테스트하는 동안 이러한 문제에 노출됩니다. 프로그램 종료에 대한 오류 보고서는 디버깅을 지원합니다.  
  
<a name="ChangeFromPreviousVersions"></a>   
## <a name="change-from-previous-versions"></a>이전 버전의 변경 내용  
 가장 중대한 변경은 관리되는 스레드와 관련됩니다. NET Framework 버전 1.0 및 1.1에서는 공용 언어 런타임이 다음과 같은 상황에서 처리되지 않은 예외에 백업을 제공합니다.  
  
- 스레드 풀 스레드에 처리되지 않은 예외가 없습니다. 작업이 처리하지 않는 예외를 throw하는 경우 런타임은 해당 예외의 스택 추적을 콘솔에 출력한 다음 해당 스레드를 스레드 풀에 반환합니다.  
  
- <xref:System.Threading.Thread> 클래스의 <xref:System.Threading.Thread.Start%2A> 메서드를 사용하여 만들어진 스레드에는 처리되지 않은 예외가 없습니다. 해당 스레드에서 실행되는 코드가 처리하지 않는 예외를 throw하는 경우 런타임은 해당 예외의 스택 추적을 콘솔에 출력한 다음 해당 스레드를 종료합니다.  
  
- 종료자 스레드에 처리되지 않은 예외가 없습니다. 종료자가 처리하지 않는 예외를 throw하는 경우 런타임은 해당 예외의 스택 추적을 콘솔에 출력한 다음 해당 종료자 스레드가 종료자 실행을 다시 시작하도록 합니다.  
  
 관리되는 스레드의 포그라운드 또는 백그라운드 상태가 이 동작에 영향을 주지 않습니다.  
  
 비관리 코드에서 발생되는 스레드의 처리되지 않은 예외의 경우 이 차이점은 더 미묘합니다. 네이티브 코드를 통해 전달된 스레드의 관리되는 예외 또는 네이티브 예외에 대해 런타임 JIT 연결 대화 상자가 운영 체제 대화 상자를 선점합니다. 모든 경우에 프로세스가 종료됩니다.  
  
### <a name="migrating-code"></a>코드 마이그레이션  
 일반적으로 변경이 되면 이전에 인식할 수 없었던 프로그래밍 문제가 노출되므로 이러한 문제를 해결할 수 있습니다. 그러나 경우에 따라 프로그래머는 스레드를 종료하기 위한 목적 등으로 런타임 백업을 활용할 수도 있습니다. 상황에 따라 프로그래머는 다음 마이그레이션 전략 중 하나를 고려해 보는 것이 좋습니다.  
  
- 코드를 재구성하여 신호를 받으면 스레드가 정상적으로 종료되도록 합니다.  
  
- <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> 메서드를 사용하여 스레드를 중단합니다.  
  
- 프로세스 종료가 진행될 수 있도록 스레드가 중단되어야 하는 경우 해당 스레드를 백그라운드 스레드로 만들어 프로세스가 종료되면 자동으로 종료되도록 합니다.  
  
 모든 경우에서 전략은 예외에 대한 다음 디자인 지침을 따라야 합니다. [예외 디자인 지침](../../../docs/standard/design-guidelines/exceptions.md)을 참조하세요.  
  
### <a name="application-compatibility-flag"></a>애플리케이션 호환 플래그  
 임시 호환을 위해 관리자는 애플리케이션 구성 파일의 `<runtime>` 섹션에 호환 플래그를 배치할 수 있습니다. 이렇게 하면 공용 언어 런타임이 버전 1.0 및 1.1의 동작으로 다시 돌아옵니다.  
  
```xml  
<legacyUnhandledExceptionPolicy enabled="1"/>  
```  
  
## <a name="host-override"></a>호스트 재정의  
 .NET Framework 버전 2.0에서는 관리되지 않는 호스트가 호스팅 API의 [ICLRPolicyManager](../../../docs/framework/unmanaged-api/hosting/iclrpolicymanager-interface.md) 인터페이스를 사용하여 공용 언어 런타임의 기본 처리되지 않은 예외를 재정의할 수 있습니다. [ICLRPolicyManager::SetUnhandledExceptionPolicy](../../../docs/framework/unmanaged-api/hosting/iclrpolicymanager-setunhandledexceptionpolicy-method.md) 함수를 사용하여 처리되지 않은 예외에 대한 정책을 설정합니다.  
  
## <a name="see-also"></a>참고 항목

- [관리되는 스레딩 기본 사항](../../../docs/standard/threading/managed-threading-basics.md)
