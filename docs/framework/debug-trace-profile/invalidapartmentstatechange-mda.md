---
title: invalidApartmentStateChange MDA
ms.date: 03/30/2017
helpviewer_keywords:
- MDAs (managed debugging assistants), invalid apartment state
- managed debugging assistants (MDAs), invalid apartment state
- InvalidApartmentStateChange MDA
- invalid apartment state changes
- threading [.NET Framework], apartment states
- apartment states
- threading [.NET Framework], managed debugging assistants
- COM apartment states
ms.assetid: e56fb9df-5286-4be7-b313-540c4d876cd7
author: mairaw
ms.author: mairaw
ms.openlocfilehash: ed4933ae59223c0674d2e36428894cbc3a07933f
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052657"
---
# <a name="invalidapartmentstatechange-mda"></a>invalidApartmentStateChange MDA
`invalidApartmentStateChange` MDA(관리 디버깅 도우미)는 다음 두 문제 중 하나가 발생하면 활성화됩니다.  
  
- 이미 COM에서 초기화된 스레드의 COM 아파트 상태를 다른 아파트 상태로 변경하려고 시도했습니다.  
  
- 스레드의 COM 아파트 상태가 예기치 않게 변경됩니다.  
  
## <a name="symptoms"></a>증상  
  
- 스레드의 COM 아파트 상태가 요청된 상태가 아닙니다. 이로 인해 현재 모델과 다른 스레딩 모델이 포함된 COM 구성 요소에 프록시가 사용될 수 있습니다. 이 사용으로 인해 아파트 간 마샬링에 사용하도록 설정되지 않은 인터페이스를 통해 COM 개체를 호출할 때 <xref:System.InvalidCastException>이 throw될 수 있습니다.  
  
- 스레드의 COM 아파트 상태가 예상과 다릅니다. 이로 인해 RCW([런타임 호출 가능 래퍼](../../standard/native-interop/runtime-callable-wrapper.md))에서 호출할 경우 <xref:System.InvalidCastException> 및 RPC_E_WRONG_THREAD의 HRESULT에서 <xref:System.Runtime.InteropServices.COMException>이 발생할 수 있습니다. 또한 이로 인해 여러 스레드가 일부 단일 스레드 COM 구성 요소에 동시에 액세스할 수 있으므로 손상이나 데이터 손실이 발생할 수 있습니다.  
  
## <a name="cause"></a>원인  
  
- 스레드가 이전에 다른 COM 아파트 상태로 초기화되었습니다. 스레드의 아파트 상태는 명시적으로 또는 암시적으로 설정할 수 있습니다. 명시적 작업에는 <xref:System.Threading.Thread.ApartmentState%2A?displayProperty=nameWithType> 속성과 <xref:System.Threading.Thread.SetApartmentState%2A> 및 <xref:System.Threading.Thread.TrySetApartmentState%2A> 메서드가 포함됩니다. 스레드가 시작되기 전에 <xref:System.Threading.Thread.SetApartmentState%2A>가 호출되지 않을 경우 <xref:System.Threading.Thread.Start%2A> 메서드를 사용하여 만든 스레드는 암시적으로 <xref:System.Threading.ApartmentState.MTA>로 설정됩니다. 주 메서드에서 <xref:System.STAThreadAttribute> 특성이 지정되지 않은 경우 애플리케이션의 주 스레드는 <xref:System.Threading.ApartmentState.MTA>로 암시적으로 초기화됩니다.  
  
- 다른 동시성 모델이 포함된 `CoUninitialize` 메서드(또는 `CoInitializeEx` 메서드)는 스레드에서 호출됩니다.  
  
## <a name="resolution"></a>해결  
 실행이 시작되기 전에 스레드의 아파트 상태를 설정하거나 <xref:System.STAThreadAttribute> 특성이나 <xref:System.MTAThreadAttribute> 특성을 애플리케이션의 주 메서드에 적용합니다.  
  
 두 번째 원인의 경우 `CoUninitialize` 메서드를 호출하는 코드를 수정하여 스레드가 종료되려고 하고 스레드에서 사용 중인 RCW 및 기본 COM 구성 요소가 없을 때까지 호출을 연기하는 것이 가장 좋습니다. 그러나 `CoUninitialize` 메서드를 호출하는 코드를 수정할 수 없는 경우에는 이 방법으로 초기화되지 않은 스레드에서 RCW를 사용하면 안 됩니다.  
  
## <a name="effect-on-the-runtime"></a>런타임에 대한 영향  
 이 MDA는 CLR에 아무런 영향을 미치지 않습니다.  
  
## <a name="output"></a>출력  
 현재 스레드의 COM 아파트 상태 및 코드에서 적용하려고 시도한 상태.  
  
## <a name="configuration"></a>구성하기  
  
```xml  
<mdaConfig>  
  <assistants>  
    <invalidApartmentStateChange />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 이 MDA를 활성화할 수 있는 상황을 보여 줍니다.  
  
```csharp
using System.Threading;  
namespace ApartmentStateMDA  
{  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            Thread.CurrentThread.SetApartmentState(ApartmentState.STA);  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [관리 디버깅 도우미를 사용하여 오류 진단](diagnosing-errors-with-managed-debugging-assistants.md)
- [interop 마샬링](../interop/interop-marshaling.md)
