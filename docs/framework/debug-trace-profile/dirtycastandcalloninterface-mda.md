---
title: dirtyCastAndCallOnInterface MDA
ms.date: 03/30/2017
helpviewer_keywords:
- managed debugging assistants (MDAs), early bound calls AutoDispatch
- dispatch-only mode
- dirtyCastAndCallOnInterface
- early-bound managed classes
- early bound calls on AutoDispatch
- MDAs (managed debugging assistants), early bound calls AutoDispatch
- EarlyBoundCallOnAutorDispatchClassInteface MDA
ms.assetid: aa388ed3-7e3d-48ea-a0b5-c47ae19cec38
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 6ac43f6b92198fec03e722b6cf5e12b86df6f4b8
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052873"
---
# <a name="dirtycastandcalloninterface-mda"></a>dirtyCastAndCallOnInterface MDA
`dirtyCastAndCallOnInterface` MDA(관리 디버깅 도우미)는 런타임에만 바인딩됨으로 표시된 클래스 인터페이스에 대해 vtable을 통해 초기에 바인딩된 호출을 시도할 때 활성화됩니다.  
  
## <a name="symptoms"></a>증상  
 COM을 통해 초기에 바인딩된 호출을 CLR에 배치하는 경우 애플리케이션에서 액세스 위반이나 예기치 않은 동작이 발생합니다.  
  
## <a name="cause"></a>원인  
 코드에서 런타임에만 바인딩되는 클래스 인터페이스에 대해 vtable을 통해 초기에 바인딩된 호출을 시도 중입니다. 기본적으로 클래스 인터페이스는 런타임에만 바인딩됨으로 식별됩니다. <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> 특성에 <xref:System.Runtime.InteropServices.ClassInterfaceType.AutoDispatch> 값(`[ClassInterface(ClassInterfaceType.AutoDispatch)]`)을 사용하여 런타임에 바인딩됨으로 식별할 수도 있습니다.  
  
## <a name="resolution"></a>해결 방법  
 권장되는 해결 방법은 COM에서 사용할 명시적 인터페이스를 정의하고 자동으로 생성된 클래스 인터페이스 대신 이 인터페이스를 통해 COM 클라이언트가 호출하도록 하는 것입니다. 또는 `IDispatch`를 통해 COM 호출을 런타임에 바인딩된 호출로 변형할 수 있습니다.  
  
 끝으로, 클래스를 <xref:System.Runtime.InteropServices.ClassInterfaceType.AutoDual>(`[ClassInterface(ClassInterfaceType.AutoDual)]`)로 식별하여 COM에서 초기에 바인딩된 호출을 배치할 수 있도록 허용할 수 있습니다. 그러나 <xref:System.Runtime.InteropServices.ClassInterfaceAttribute>에 설명된 버전 관리 제한 사항 때문에 <xref:System.Runtime.InteropServices.ClassInterfaceType.AutoDual>은 사용하지 않는 것이 좋습니다.  
  
## <a name="effect-on-the-runtime"></a>런타임에 대한 영향  
 이 MDA는 CLR에 아무런 영향을 미치지 않습니다. 런타임에 바인딩된 인터페이스에 대한 초기에 바인딩된 호출 데이터만 보고합니다.  
  
## <a name="output"></a>출력  
 초기에 바인딩됨으로 액세스되는 필드 이름 또는 메서드 이름입니다.  
  
## <a name="configuration"></a>Configuration  
  
```xml  
<mdaConfig>  
  <assistants>  
    <dirtyCastAndCallOnInterface />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.InteropServices.ClassInterfaceAttribute>
- [관리 디버깅 도우미를 사용하여 오류 진단](diagnosing-errors-with-managed-debugging-assistants.md)
