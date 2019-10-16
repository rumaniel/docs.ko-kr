---
title: overlappedFreeError MDA
ms.date: 03/30/2017
helpviewer_keywords:
- OverlappedFreeError MDA
- overlapped free method call error
- managed debugging assistants (MDAs), overlapped structures
- overlapped structures
- MDAs (managed debugging assistants), overlapped structures
- freeing overlapped structures
ms.assetid: b6ab2d48-6eee-4bab-97a3-046b3b0a5470
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 70d31bc187cabe49351e86a20023e2ec65e87b94
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052395"
---
# <a name="overlappedfreeerror-mda"></a>overlappedFreeError MDA
`overlappedFreeError` MDA(관리 디버깅 도우미)는 겹치는 작업이 완료되기 전에 <xref:System.Threading.Overlapped.Free%28System.Threading.NativeOverlapped%2A%29?displayProperty=nameWithType> 메서드를 호출하면 활성화됩니다.  
  
## <a name="symptoms"></a>증상  
 액세스 위반 또는 가비지 수집된 힙의 손상입니다.  
  
## <a name="cause"></a>원인  
 작업이 완료되기 전에 겹친 구조체가 해제되었습니다. 겹친 포인터를 사용하는 함수는 나중에 해제된 후 구조체에 쓸 수 있습니다. 따라서 다른 개체가 현재 해당 지역을 사용하고 있을 수 있으므로 힙이 손상될 수 있습니다.  
  
 겹친 작업이 성공적으로 시작하지 않은 경우 이 MDA는 오류를 나타내지 않을 수 있습니다.  
  
## <a name="resolution"></a>해결 방법  
 <xref:System.Threading.Overlapped.Free%28System.Threading.NativeOverlapped%2A%29> 메서드를 호출하기 전에 겹친 구조체를 사용하는 I/O 작업이 완료되었는지 확인합니다.  
  
## <a name="effect-on-the-runtime"></a>런타임에 대한 영향  
 이 MDA는 CLR에 아무런 영향을 미치지 않습니다.  
  
## <a name="output"></a>출력  
 다음은 이 MDA의 샘플 출력입니다.  
  
 `An overlapped pointer (0x00ea3430) that was not allocated on the GC heap was passed via Pinvoke to the win32 function 'WriteFile' in module 'KERNEL32.DLL'. If the AppDomain is shut down, this can cause heap corruption when the async I/O completes. The best solution is to pass a NativeOverlappedStructure retrieved from a call to System.Threading.Overlapped.Pack(). If the AppDomain exits, the CLR will keep this structure alive and pinned until the I/O completes.`  
  
## <a name="configuration"></a>Configuration  
  
```xml  
<mdaConfig>  
  <assistants>  
    <overlappedFreeError/>  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [관리 디버깅 도우미를 사용하여 오류 진단](diagnosing-errors-with-managed-debugging-assistants.md)
- [interop 마샬링](../interop/interop-marshaling.md)
