---
title: nonComVisibleBaseClass MDA
ms.date: 03/30/2017
helpviewer_keywords:
- visible classes
- managed debugging assistants (MDAs), COM visible classes
- nonComVisibleBaseClass MDA
- COM visible classes
- QueryInterface call failures
- MDAs (managed debugging assistants), COM visible classes
ms.assetid: 9ec1af27-604b-477e-9ee2-e833eb10d3ce
author: mairaw
ms.author: mairaw
ms.openlocfilehash: e4340dd75e24ddeb01428159d5532b86e76fd8b4
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052436"
---
# <a name="noncomvisiblebaseclass-mda"></a>nonComVisibleBaseClass MDA
`nonComVisibleBaseClass` MDA(관리 디버깅 도우미)는 COM 노출이 아닌 기본 클래스에서 파생된 COM 노출 관리되는 클래스의 COM CCW(호출 가능 래퍼)에서 네이티브 코드 또는 비관리 코드에 의해 `QueryInterface` 호출이 수행될 때 활성화됩니다.  `QueryInterface` 호출은 호출에서 클래스 인터페이스 또는 COM 노출 관리되는 클래스의 기본 `IDispatch`를 요청하는 경우에만 MDA가 활성화되게 합니다.  <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> 특성이 적용되고 COM 노출 클래스에 의해 명시적으로 구현된 명시적 인터페이스에 대한 `QueryInterface`인 경우에는 MDA가 활성화되지 않습니다.  
  
## <a name="symptoms"></a>증상  
 COR_E_INVALIDOPERATION HRESULT로 인해 실패하는 네이티브 코드에서 `QueryInterface` 호출이 수행됩니다.  HRESULT는 런타임에서 `QueryInterface` 호출을 허용하지 않아 이 MDA의 활성화가 발생하기 때문일 수 있습니다.  
  
## <a name="cause"></a>원인  
 런타임에서 잠재적 버전 관리 문제 때문에 COM 노출이 아닌 클래스에서 파생된 COM 노출 클래스의 클래스 인터페이스 또는 기본 `IDispatch` 인터페이스에 대해 `QueryInterface` 호출을 허용하지 않습니다.  예를 들어 public 멤버가 COM 노출이 아닌 기본 클래스에 추가된 경우 기본 클래스 멤버를 포함하는 파생 클래스의 vtable이 이러한 변경 내용으로 인해 변경되기 때문에 파생 클래스를 사용하는 기존 COM 클라이언트가 손상될 수 있습니다.  COM에 노출되는 명시적 인터페이스는 vtable에 인터페이스의 기본 멤버가 포함되지 않으므로 이 문제가 없습니다.  
  
## <a name="resolution"></a>해결 방법  
 클래스 인터페이스를 노출하지 마세요. 명시적 인터페이스를 정의하고 <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> 특성을 적용합니다.  
  
## <a name="effect-on-the-runtime"></a>런타임에 대한 영향  
 이 MDA는 CLR에 아무런 영향을 미치지 않습니다.  
  
## <a name="output"></a>출력  
 다음은 COM 노출이 아닌 클래스 `Base`에서 파생된 COM 노출 클래스 `Derived`에 대한 `QueryInterface` 호출의 예제 메시지입니다.  
  
```output
A QueryInterface call was made requesting the class interface of COM   
visible managed class 'Derived'. However since this class derives from   
non COM visible class 'Base', the QueryInterface call will fail. This   
is done to prevent the non COM visible base class from being   
constrained by the COM versioning rules.   
```  
  
## <a name="configuration"></a>Configuration  
  
```xml  
<mdaConfig>  
  <assistants>  
    <nonComVisibleBaseClass />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [관리 디버깅 도우미를 사용하여 오류 진단](diagnosing-errors-with-managed-debugging-assistants.md)
- [interop 마샬링](../interop/interop-marshaling.md)
