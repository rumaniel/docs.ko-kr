---
title: invalidVariant MDA
ms.date: 03/30/2017
helpviewer_keywords:
- MDAs (managed debugging assistants), invalid variant
- VARIANT type errors
- InvalidVariant MDA
- invalid VARIANT types
- managed debugging assistants (MDAs), invalid variant
ms.assetid: d273e070-d1b1-4a53-a9c7-7af837b04a3d
author: mairaw
ms.author: mairaw
ms.openlocfilehash: c34f160b643a0431168097d3832357b4ac6e4557
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052570"
---
# <a name="invalidvariant-mda"></a>invalidVariant MDA
`invalidVariant` MDA(관리 디버깅 도우미)는 네이티브 코드나 비관리 코드에서 관리 코드로 호출하는 동안 잘못된 `VARIANT` 구조가 발생할 때 활성화됩니다.  
  
## <a name="symptoms"></a>증상  
 `VARIANT`를 개체로 마샬링하는 작업과 관련해서 네이티브 코드와 관리 코드 간에 전환하는 동안 발생하는 예기치 않은 동작입니다.  
  
## <a name="cause"></a>원인  
 네이티브 코드는 형식이 잘못된 `VARIANT` 구조를 관리 코드로 전달합니다.  런타임에서는 이 `VARIANT`를 개체로 마샬링하려고 시도하고 `VARIANT`가 유효하지 않으면 MDA를 활성화합니다. 잘못된 `VARIANT`의 예로는 `VARIANT`와 `VARTYPE` VT_EMPTY &#124; VT_BYREF를 함께 사용하거나 `VARIANT`를 `VARTYPE` VT_VARIANT와 함께 사용하는 경우가 있습니다.  
  
## <a name="resolution"></a>해결 방법  
 `VARIANT`를 전달하는 네이티브 코드나 비관리 코드는 `VARIANT`가 제대로 서식 지정되고 초기화되었는지 확인해야 합니다.  
  
## <a name="effect-on-the-runtime"></a>런타임에 대한 영향  
 MDA는 런타임 동작에 영향을 미치지 않습니다.  
  
## <a name="output"></a>출력  
 런타임에서 비관리 모듈을 통해 관리 코드에 전달된 잘못된 `VARIANT`를 감지했음을 나타내는 MDA 메시지입니다.  
  
## <a name="configuration"></a>Configuration  
  
```xml  
<mdaConfig>  
  <assistants>  
    <invalidVariant />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [관리 디버깅 도우미를 사용하여 오류 진단](diagnosing-errors-with-managed-debugging-assistants.md)
- [interop 마샬링](../interop/interop-marshaling.md)
