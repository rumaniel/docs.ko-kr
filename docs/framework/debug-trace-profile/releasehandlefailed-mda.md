---
title: releaseHandleFailed MDA
ms.date: 03/30/2017
helpviewer_keywords:
- managed debugging assistants (MDAs), handles
- release handle failed
- CriticalHandle class, run-time errors
- releaseHandleFailed MDA
- ReleaseHandle method
- SafeHandle class, run-time errors
- MDAs (managed debugging assistants), handles
ms.assetid: 44cd98ba-95e5-40a1-874d-e8e163612c51
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 41f6b67ff63d096cc1fa2c599abb06c9c1129952
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052306"
---
# <a name="releasehandlefailed-mda"></a>releaseHandleFailed MDA
<xref:System.Runtime.InteropServices.SafeHandle> 또는 <xref:System.Runtime.InteropServices.CriticalHandle>에서 파생된 클래스의 <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A> 메서드가 `false`를 반환하면 `releaseHandleFailed` MDA(관리 디버깅 도우미)가 활성화되고 개발자에게 알립니다.  
  
## <a name="symptoms"></a>증상  
 리소스 또는 메모리 누수가 발생합니다.  <xref:System.Runtime.InteropServices.SafeHandle> 또는 <xref:System.Runtime.InteropServices.CriticalHandle>에서 파생된 클래스의 <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A> 메서드가 실패하는 경우 클래스에 캡슐화된 리소스가 해제 또는 정리되지 않았을 수 있습니다.  
  
## <a name="cause"></a>원인  
 사용자는 <xref:System.Runtime.InteropServices.SafeHandle> 또는 <xref:System.Runtime.InteropServices.CriticalHandle>에서 파생된 클래스를 만드는 경우 <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A> 메서드의 구현을 제공해야 합니다. 따라서 이 상황은 개별 리소스와 관련이 있습니다. 그러나 요구 사항은 다음과 같습니다.  
  
- <xref:System.Runtime.InteropServices.SafeHandle> 및 <xref:System.Runtime.InteropServices.CriticalHandle> 유형은 중요한 프로세스 리소스를 둘러싼 래퍼를 나타냅니다. 메모리 누수로 인해 시간이 지나면 프로세스를 사용할 수 없게 됩니다.  
  
- <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A> 메서드가 해당 기능을 수행해야 합니다. 프로세스에서 이러한 리소스를 획득한 후 해제하는 방법은 <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A>뿐입니다. 따라서 실패는 리소스 누수를 의미합니다.  
  
- <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A>을 실행하는 동안 발생하여 리소스 해제를 방해하는 모든 오류는 <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A> 메서드 자체 구현의 버그입니다. 코드가 해당 기능을 수행하기 위해 다른 사용자가 작성한 코드를 호출하는 경우에도 계약이 이행되도록 하는 것은 프로그래머의 책임입니다.  
  
## <a name="resolution"></a>해결 방법  
 MDA 알림을 발생시킨 특정 <xref:System.Runtime.InteropServices.SafeHandle>(또는 <xref:System.Runtime.InteropServices.CriticalHandle>)을 사용하는 코드를 검토하여 원시 핸들 값이 <xref:System.Runtime.InteropServices.SafeHandle>에서 추출되어 다른 곳에 복사되는 위치를 찾아야 합니다. 원시 핸들 값의 사용이 런타임에서 더 이상 추적되지 않으므로 이는 <xref:System.Runtime.InteropServices.SafeHandle> 또는 <xref:System.Runtime.InteropServices.CriticalHandle> 구현 내에서 일반적인 오류 원인입니다. 이후에 원시 핸들 복사를 닫을 경우 현재 유효하지 않은 핸들에 대해 닫기가 시도되기 때문에 이후 <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A> 호출이 실패할 수 있습니다.  
  
 잘못된 핸들 복제가 발생할 수 있는 여러 가지 방식이 있습니다.  
  
- <xref:System.Runtime.InteropServices.SafeHandle.DangerousGetHandle%2A> 메서드 호출을 찾습니다. 이 메서드 호출은 극히 드물어야 하며, 발견된 모든 호출은 <xref:System.Runtime.InteropServices.SafeHandle.DangerousAddRef%2A> 및 <xref:System.Runtime.InteropServices.SafeHandle.DangerousRelease%2A> 메서드 호출로 둘러싸여 있어야 합니다. 이러한 두 메서드는 원시 핸들 값을 안전하게 사용할 수 있는 코드 영역을 지정합니다. 이 영역 외부에서 또는 참조 횟수가 증가하지 않는 경우 언제든지 다른 스레드에서 <xref:System.Runtime.InteropServices.SafeHandle.Dispose%2A> 또는 <xref:System.Runtime.InteropServices.SafeHandle.Close%2A>를 호출하여 핸들 값을 무효화할 수 있습니다. <xref:System.Runtime.InteropServices.SafeHandle.DangerousGetHandle%2A>의 모든 사용이 추적되고 나면 원시 핸들의 경로를 따라 결국 `CloseHandle` 또는 핸들을 해제할 다른 하위 수준 네이티브 메서드를 호출하는 일부 구성 요소에 전달되지 않는지 확인해야 합니다.  
  
- <xref:System.Runtime.InteropServices.SafeHandle>을 유효한 원시 핸들 값으로 초기화하는 데 사용되는 코드가 핸들을 소유하고 있는지 확인합니다. 기본 생성자에서 `ownsHandle` 매개 변수를 `false`로 설정하지 않고 코드가 소유하지 않는 핸들을 중심으로 <xref:System.Runtime.InteropServices.SafeHandle>을 형성하는 경우 <xref:System.Runtime.InteropServices.SafeHandle> 및 실제 핸들 소유자 모두 핸들을 닫으려고 하여 <xref:System.Runtime.InteropServices.SafeHandle>이 경합에서 지면 <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A>에서 오류가 발생합니다.  
  
- <xref:System.Runtime.InteropServices.SafeHandle>이 애플리케이션 도메인 간에 마샬링되는 경우 사용 중인 <xref:System.Runtime.InteropServices.SafeHandle> 파생이 직렬화 가능으로 표시되었는지 확인합니다. 드물기는 하지만 <xref:System.Runtime.InteropServices.SafeHandle>에서 파생된 클래스가 deserialization 가능으로 설정된 경우 <xref:System.Runtime.Serialization.ISerializable> 인터페이스를 구현하거나 deserialization 프로세스를 수동으로 제어하는 다른 기술 중 하나를 사용해야 합니다. 이 작업은 기본 직렬화 작업이 묶인 원시 핸들 값의 비트 복제본을 만들어 두 개의 <xref:System.Runtime.InteropServices.SafeHandle> 인스턴스가 동일한 핸들을 소유하고 있다고 생각하게 만들기 때문에 필요합니다. 일부 지점에서 둘 다 동일한 핸들에 대해 <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A>을 호출하려고 합니다. 두 번째 <xref:System.Runtime.InteropServices.SafeHandle>이 실패합니다. <xref:System.Runtime.InteropServices.SafeHandle>을 직렬화할 때의 올바른 작업 과정은 네이티브 핸들 형식에 대해 `DuplicateHandle` 함수나 비슷한 함수를 호출하여 별개의 올바른 핸들 복사본을 만드는 것입니다. 핸들 형식이 이 작업을 지원하지 않는 경우 래핑하는 <xref:System.Runtime.InteropServices.SafeHandle> 형식을 직렬화 가능으로 설정할 수 없습니다.  
  
- 핸들을 해제하는 데 사용된 네이티브 루틴(예: `CloseHandle` 함수)에 디버거 중단점을 배치하면 핸들이 일찍 닫혀 <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A> 메서드를 최종 호출할 때 오류가 발생하는 위치를 추적할 수 있습니다. 이 작업은 이러한 루틴이 종종 처리하는 많은 트래픽으로 인해 스트레스 시나리오나 중간 규모의 기능 테스트에서도 불가능할 수 있습니다. 호출자 ID 또는 전체 스택 추적과 해제되는 핸들의 값을 캡처하기 위해 네이티브 해제 메서드를 호출하는 코드를 계측하면 도움이 될 수도 있습니다.  핸들 값을 이 MDA에서 보고한 값과 비교할 수 있습니다.  
  
- `CloseHandle` 함수를 통해 해제할 수 있는 모든 Win32 핸들과 같은 일부 네이티브 핸들 형식은 동일한 핸들 네임스페이스를 공유합니다. 하나의 핸들 형식을 잘못 해제하면 다른 핸들에서 문제가 발생할 수 있습니다. 예를 들어 실수로 Win32 이벤트 핸들을 두 번 닫을 경우 관련이 없어 보이는 파일 핸들이 조기에 닫힐 수 있습니다. 이 문제는 핸들이 해제되고 다른 형식의 다른 리소스를 추적하는 데 핸들 값을 사용할 수 있게 될 때 발생합니다. 이 경우 잘못된 두 번째 해제가 이어서 발생하면 관련 없는 스레드의 핸들이 무효화될 수 있습니다.  
  
## <a name="effect-on-the-runtime"></a>런타임에 대한 영향  
 이 MDA는 CLR에 아무런 영향을 미치지 않습니다.  
  
## <a name="output"></a>출력  
 <xref:System.Runtime.InteropServices.SafeHandle> 또는 <xref:System.Runtime.InteropServices.CriticalHandle>이 핸들을 제대로 해제하지 못했음을 나타내는 메시지입니다. 예를 들어:  
  
```output
"A SafeHandle or CriticalHandle of type 'MyBrokenSafeHandle'   
failed to properly release the handle with value 0x0000BEEF. This   
usually indicates that the handle was released incorrectly via   
another means (such as extracting the handle using DangerousGetHandle   
and closing it directly or building another SafeHandle around it."  
```  
  
## <a name="configuration"></a>Configuration  
  
```xml  
<mdaConfig>  
  <assistants>  
    <releaseHandleFailed/>  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="example"></a>예제  
 다음은 `releaseHandleFailed` MDA를 활성화할 수 있는 코드 예제입니다.  
  
```csharp
bool ReleaseHandle()  
{  
    // Calling the Win32 CloseHandle function to release the   
    // native handle wrapped by this SafeHandle. This method returns   
    // false on failure, but should only fail if the input is invalid   
    // (which should not happen here). The method specifically must not   
    // fail simply because of lack of resources or other transient   
    // failures beyond the user’s control. That would make it unacceptable   
    // to call CloseHandle as part of the implementation of this method.  
    return CloseHandle(handle);  
}  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [관리 디버깅 도우미를 사용하여 오류 진단](diagnosing-errors-with-managed-debugging-assistants.md)
- [interop 마샬링](../interop/interop-marshaling.md)
