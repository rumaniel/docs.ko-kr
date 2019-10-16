---
title: loaderLock MDA
ms.date: 03/30/2017
helpviewer_keywords:
- deadlocks [.NET Framework]
- LoaderLock MDA
- MDAs (managed debugging assistants), loader locks
- managed debugging assistants (MDAs), loader locks
- operating system loader locks
- loader locks
- locks, threads
ms.assetid: 8c10fa02-1b9c-4be5-ab03-451d943ac1ee
author: mairaw
ms.author: mairaw
ms.openlocfilehash: c3e8769ec972ec76d04d2f22368fdde99de9c6de
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052540"
---
# <a name="loaderlock-mda"></a>loaderLock MDA
`loaderLock` MDA(관리 디버깅 도우미)는 Microsoft Windows 운영 체제 로더 잠금을 보유하는 스레드에서 관리 코드를 실행하려는 시도를 감지합니다.  이와 같은 실행은 운영 체제의 로더에서 초기화하기 전에 DLL을 사용하고 교착 상태를 일으킬 수 있으므로 유효하지 않습니다.  
  
## <a name="symptoms"></a>증상  
 운영 체제의 로더 잠금에서 코드를 실행할 때 가장 많이 발생하는 오류는 마찬가지로 로더 잠금이 필요한 다른 Win32 함수를 호출하려고 할 때 스레드가 교착 상태가 된다는 것입니다.  이러한 함수의 예는 `LoadLibrary`, `GetProcAddress`, `FreeLibrary` 및 `GetModuleHandle`입니다.  애플리케이션에서 이러한 함수를 직접 호출하지 않을 수 있습니다. CLR(공용 언어 런타임)에서는 <xref:System.Reflection.Assembly.Load%2A>와 같은 상위 레벨 호출 또는 플랫폼 호출 메서드를 처음 호출한 결과로 이러한 함수를 호출할 수 있습니다.  
  
 교착 상태는 한 스레드에서 다른 스레드가 시작하거나 완료되기를 기다리는 경우에도 발생할 수 있습니다.  스레드가 실행을 시작하거나 완료하면 영향받은 DLL에 이벤트를 제공하도록 운영 체제의 로더 잠금을 획득해야 합니다.  
  
 마지막으로 운영 체제의 로더에서 DLL을 제대로 초기화하기 전에 DLL을 호출할 수 있는 경우가 있습니다.  교착 상태와 관련된 모든 스레드의 스택을 검사하여 진단할 수 있는 교착 상태 오류와 달리 초기화되지 않은 DLL 사용은 이 MDA를 사용하지 않으면 진단하기가 매우 어렵습니다.  
  
## <a name="cause"></a>원인  
 .NET Framework 버전 1.0 또는 1.1용으로 빌드된 혼합 관리/관리되지 않는 C++ 어셈블리에서는 특별하게 주의를 기울이는 경우가 아니면(예: **/NOENTRY**와 링크) 일반적으로 로더 잠금 내의 관리 코드를 실행하려고 시도합니다.
  
 .NET Framework 버전 2.0용으로 빌드된 혼합된 관리/관리되지 않는 C++ 어셈블리에서는 이러한 문제점이 발생할 가능성이 적으며, 운영 체제의 규칙을 위반하는 관리되지 않는 DLL을 사용하는 애플리케이션과 마찬가지로 위험이 줄어듭니다.  예를 들어, 관리되지 않는 DLL의 `DllMain` 진입점에서 `CoCreateInstance`를 호출하여 COM에 노출된 관리되는 오브젝트를 확보하는 경우 결과적으로 로더 잠금 내에서 관리 코드를 실행하려고 시도합니다. .NET Framework 버전 2.0 이상의 로더 잠금 문제점에 대한 자세한 내용은 [혼합 어셈블리 초기화](/cpp/dotnet/initialization-of-mixed-assemblies)를 참조하세요.  
  
## <a name="resolution"></a>해결  
 Visual C++ .NET 2002 및 Visual C++ NET 2003에서 `/clr` 컴파일러 옵션을 사용하여 컴파일한 DLL을 로드할 때 명확하지 않은 교착 상태에 빠질 수 있습니다. 이 문제를 혼합 DLL 로드 또는 로더 잠금 문제라고 합니다. Visual C++ 2005 이상에서 혼합 DLL 로드 프로세스의 불명확한 요소가 대부분 제거되었습니다. 그러나 일부 시나리오에서는 명확한 로더 잠금 문제가 발생할 수 있습니다. 나머지 로더 잠금 문제의 원인과 해결 방법에 대한 자세한 내용은 [혼합 어셈블리 초기화](/cpp/dotnet/initialization-of-mixed-assemblies)를 참조하세요. 해당 항목에서 로더 잠금 문제를 식별하지 못하는 경우 스레드 스택을 검사하여 로더 잠금이 발생하는 이유와 문제를 정정하는 방법을 판별해야 합니다. 이 MDA가 활성화된 스레드의 스택 추적을 확인합니다.  스레드에서 운영 체제의 로더 잠금을 보유하는 동안 관리 코드를 잘못 호출하려고 합니다.  DLL의 `DllMain` 또는 스택의 해당 진입점이 표시됩니다.  이러한 진입점에서 올바르게 수행할 수 있는 사항에 대한 운영 체제 규칙은 상당히 제한되어 있습니다.  이러한 규칙은 관리되는 모든 실행을 차단합니다.  
  
## <a name="effect-on-the-runtime"></a>런타임에 대한 영향  
 일반적으로 프로세스 내의 여러 스레드가 교착 상태가 됩니다.  이러한 스레드 중 하나는 가비지 수집을 수행하는 스레드이므로 이 교착 상태가 전체 프로세스에 주된 영향을 미칠 수 있습니다.  또한 운영 체제의 로더 잠금이 필요한 추가 작업(예: 어셈블리 또는 DLL 로드 및 로드 해제, 스레드 시작 또는 중지)도 수행하지 못하게 합니다.  
  
 드문 경우지만 액세스 위반이나 이와 비슷한 문제점이 DLL에서 트리거되어 초기화되기 전에 호출되는 문제도 발생할 수 있습니다.  
  
## <a name="output"></a>출력  
 이 MDA는 잘못된 관리 실행이 시도되고 있음을 보고합니다.  스레드 스택을 검사하여 로더 잠금이 발생하는 이유와 문제를 정정하는 방법을 판별해야 합니다.  
  
## <a name="configuration"></a>Configuration  
  
```xml  
<mdaConfig>  
  <assistants>  
    <loaderLock/>  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>참고자료

- [관리 디버깅 도우미를 사용하여 오류 진단](diagnosing-errors-with-managed-debugging-assistants.md)
