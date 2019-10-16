---
title: exceptionSwallowedOnCallFromCom MDA
ms.date: 03/30/2017
helpviewer_keywords:
- messages, informational
- informational messages
- managed debugging assistants (MDAs), exceptions
- exception handling, managed debugging assistants
- MDAs (managed debugging assistants), exceptions
- ExceptionSwallowedOnCallFromCOM MDA
ms.assetid: 55d6ab12-f251-4aab-aa64-aacbe9d9f974
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 3a49bdce78c1445cd25de8755ded0f27a4902937
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052813"
---
# <a name="exceptionswallowedoncallfromcom-mda"></a>exceptionSwallowedOnCallFromCom MDA
`exceptionSwallowedOnCallFromCOM` MDA(관리 디버깅 도우미)는 관리되지 않는 HRESULT 반환 형식이 없는 메서드를 통해 COM에서 호출된 CLR(공용 언어 런타임) 코드에서 예외가 throw되면 활성화됩니다.  
  
## <a name="symptoms"></a>증상  
 COM에서 관리되는 구성 요소에 대한 호출이 FALSE 또는 0 값으로 반환됩니다. 또는 메서드의 반환 형식이 void인 경우 메서드 실행 중에 예외가 throw되었음을 나타내는 표시가 없을 수 있습니다. 이 경우 예외가 자동으로 catch되고 실행이 COM 호출자에 반환됩니다.  
  
## <a name="cause"></a>원인  
 예외가 throw되었지만 해당 예외를 보고할 유효한 방법이 없습니다.  
  
## <a name="resolution"></a>해결 방법  
 정보 제공의 목적이며, 반드시 버그를 의미하는 것은 아닙니다.  
  
## <a name="effect-on-the-runtime"></a>런타임에 대한 영향  
 이 MDA는 CLR에 아무런 영향을 미치지 않습니다. 자동으로 catch된 예외에 대한 데이터를 보고할 뿐입니다.  
  
## <a name="output"></a>출력  
 메서드 이름, 형식 이름 및 예외 메시지를 포함하는 정보 메시지입니다.  
  
## <a name="configuration"></a>Configuration  
  
```xml  
<mdaConfig>  
  <assistants>  
    <exceptionSwallowedOnCallFromCom />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [관리 디버깅 도우미를 사용하여 오류 진단](diagnosing-errors-with-managed-debugging-assistants.md)
- [interop 마샬링](../interop/interop-marshaling.md)
