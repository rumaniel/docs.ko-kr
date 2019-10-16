---
title: callbackOnCollectedDelegate MDA
ms.date: 03/30/2017
dev_langs:
- cpp
helpviewer_keywords:
- MDAs (managed debugging assistants), garbage collection
- managed debugging assistants (MDAs), callback on collected delegates
- MDAs (managed debugging assistants), callback on collected delegates
- callback on delegate after garbage collection
- callbackOnCollectedDelegate MDA
- managed debugging assistants (MDAs), garbage collection
- call back collected delegates
- garbage collection, run-time errors
- delegates [.NET Framework], garbage collection
ms.assetid: 398b0ce0-5cc9-4518-978d-b8263aa21e5b
author: mairaw
ms.author: mairaw
ms.openlocfilehash: f7f5a6ef2d4e8d4a987ed74a6a04e31f87cc46f3
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052931"
---
# <a name="callbackoncollecteddelegate-mda"></a>callbackOnCollectedDelegate MDA
대리자가 함수 포인터로 관리 코드에서 비관리 코드로 마샬링되고 대리자가 가비지 수집된 후 콜백이 해당 함수 포인터에 배치된 경우 `callbackOnCollectedDelegate` MDA(관리 디버깅 도우미)가 활성화됩니다.  
  
## <a name="symptoms"></a>증상  
 관리되는 대리자에서 가져온 함수 포인터를 통해 관리 코드를 호출하려고 하면 액세스 위반이 발생합니다. 이러한 오류는 CLR(공용 언어 런타임) 버그가 아니지만 CLR 코드에서 액세스 위반이 발생하기 때문에 버그처럼 보일 수도 있습니다.  
  
 오류는 일관성이 없습니다. 함수 포인터에 대한 호출이 성공하는 경우도 있고 실패하는 경우도 있습니다. 부하가 높은 상태에서 또는 임의의 시도 횟수에서만 오류가 발생할 수도 있습니다.  
  
## <a name="cause"></a>원인  
 함수 포인터가 생성되고 비관리 코드에 노출된 대리자가 가비지 수집되었습니다. 관리되지 않는 구성 요소가 함수 포인터를 호출하려고 하면 액세스 위반이 생성됩니다.  
  
 가비지 수집이 발생하는 시기에 따라 달라지므로 오류는 무작위인 것처럼 보입니다. 대리자가 컬렉션에 적합한 경우 콜백 후에 가비지 수집이 발생할 수 있으며 호출이 성공합니다. 그러지 않은 경우에는 콜백 전에 가비지 컬렉션이 발생하며, 콜백에서 액세스 위반을 생성하고 프로그램이 중지됩니다.  
  
 오류 가능성은 대리자 마샬링과 함수 포인터에 대한 콜백 사이의 시간 및 가비지 수집 빈도에 따라 달라집니다. 대리자 마샬링과 이후 콜백 사이의 시간이 짧으면 오류가 드물게 발생합니다. 이는 일반적으로 함수 포인터를 받는 관리되지 않는 메서드가 나중에 사용하기 위해 함수 포인터를 저장하지 않고 함수 포인터에 대해 즉시 콜백하여 반환하기 전에 해당 작업을 완료하는 경우에 나타납니다. 마찬가지로, 시스템의 부하가 높은 상태에서는 가비지 수집이 더 많이 발생하므로 콜백 전에 가비지 수집이 발생할 가능성이 커집니다.  
  
## <a name="resolution"></a>해결 방법  
 대리자가 관리되지 않는 함수 포인터로 마샬링된 경우 가비지 수집기가 수명을 추적할 수 없습니다. 대신, 코드에서 관리되지 않는 함수 포인터의 수명 동안 대리자에 대한 참조를 유지해야 합니다. 그러나 이렇게 하려면 먼저 수집된 대리자를 식별해야 합니다. MDA가 활성화되면 대리자의 형식 이름을 제공합니다. 이 이름을 사용하여 해당 대리자를 비관리 코드에 전달하는 COM 서명이나 플랫폼 호출을 코드에서 검색할 수 있습니다. 위반 대리자는 이러한 호출 사이트 중 하나를 통해 전달됩니다. `gcUnmanagedToManaged` MDA에서 각 런타임 콜백 전에 가비지 컬렉션을 강제할 수 있게 할 수도 있습니다. 그러면 항상 콜백 전에 가비지 수집이 발생하므로 가비지 수집에 의한 불확실성이 제거됩니다. 수집된 대리자를 확인했으면 마샬링된 관리되지 않는 함수 포인터의 수명 동안 관리되는 쪽에서 해당 대리자에 대한 참조를 유지하도록 코드를 변경합니다.  
  
## <a name="effect-on-the-runtime"></a>런타임에 대한 영향  
 대리자가 함수 포인터로 마샬링되는 경우 런타임은 비관리에서 관리로 전환을 수행하는 썽크를 할당합니다. 이 썽크는 관리되는 대리자가 최종 호출되기 전에 비관리 코드에서 실제로 호출하는 대상입니다. `callbackOnCollectedDelegate` MDA를 사용할 수 없는 경우 대리자가 수집되면 관리되지 않는 마샬링 코드가 삭제됩니다. `callbackOnCollectedDelegate` MDA를 사용할 수 있는 경우 대리자가 수집되어도 관리되지 않는 마샬링 코드가 즉시 삭제되지 않습니다. 대신, 마지막 1,000개 인스턴스가 기본적으로 활성 상태로 유지되고 호출 시 MDA를 활성화하도록 변경됩니다. 썽크는 1,001개 이상의 마샬링된 대리자가 수집된 후에 삭제됩니다.  
  
## <a name="output"></a>출력  
 MDA는 관리되지 않는 함수 포인터에서 콜백이 시도되기 전에 수집된 대리자의 형식 이름을 보고합니다.  
  
## <a name="configuration"></a>Configuration  
 다음 예제에서는 애플리케이션 구성 옵션을 보여 줍니다. MDA에서 활성 상태로 유지하는 썽크 수를 1,500개로 설정합니다. 기본 `listSize` 값은 1,000이고, 최소값은 50이고, 최대값은 2,000입니다.  
  
```xml  
<mdaConfig>  
  <assistants>  
    <callbackOnCollectedDelegate listSize="1500" />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="example"></a>예제  
 다음 예제에서는 이 MDA를 활성화할 수 있는 상황을 보여 줍니다.  
  
```cpp
// Library.cpp : Defines the unmanaged entry point for the DLL application.  
#include "windows.h"  
#include "stdio.h"  
  
void (__stdcall *g_pfTarget)();  
  
void __stdcall Initialize(void __stdcall pfTarget())  
{  
    g_pfTarget = pfTarget;  
}  
  
void __stdcall Callback()  
{  
    g_pfTarget();  
}
```

```csharp
// C# Client  
using System;  
using System.Runtime.InteropServices;  
  
public class Entry  
{  
    public delegate void DCallback();  
  
    public static void Main()  
    {  
        new Entry();  
        Initialize(Target);  
        GC.Collect();  
        GC.WaitForPendingFinalizers();  
        Callback();  
    }  
  
    public static void Target()  
    {          
    }  
  
    [DllImport("Library", CallingConvention = CallingConvention.StdCall)]  
    public static extern void Initialize(DCallback pfDelegate);  
  
    [DllImport ("Library", CallingConvention = CallingConvention.StdCall)]  
    public static extern void Callback();  
  
    ~Entry() { Console.Error.WriteLine("Entry Collected"); }  
}  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [관리 디버깅 도우미를 사용하여 오류 진단](diagnosing-errors-with-managed-debugging-assistants.md)
- [interop 마샬링](../interop/interop-marshaling.md)
- [gcUnmanagedToManaged](gcunmanagedtomanaged-mda.md)
