---
title: disconnectedContext MDA
ms.date: 03/30/2017
helpviewer_keywords:
- DisconnectedContext MDA
- MDAs (managed debugging assistants), disconnected context
- dead context
- transitioning disconnected apartment or context
- context disconnections
- managed debugging assistants (MDAs), disconnected context
ms.assetid: 1887d31d-7006-4491-93b3-68fd5b05f71d
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 670a32b4d198d2762e0bb51e41297836e471e05b
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052837"
---
# <a name="disconnectedcontext-mda"></a>disconnectedContext MDA
`disconnectedContext` MDA(관리 디버깅 도우미)는 CLR이 COM 개체 관련 요청을 서비스하는 동안 연결이 끊어진 아파트 또는 컨텍스트로 전환하려고 하면 활성화됩니다.  
  
## <a name="symptoms"></a>증상  
 RCW([런타임 호출 가능 래퍼](../../standard/native-interop/runtime-callable-wrapper.md))에 대한 호출이 해당 호출이 존재하는 아파트 또는 컨텍스트 대신 현재 아파트 또는 컨텍스트의 기본 COM 구성 요소에 전달됩니다. 따라서 COM 구성 요소가 다중 스레드가 아닌 경우 STA(단일 스레드 아파트) 구성 요소의 경우처럼 손상 및/또는 데이터 손실이 발생할 수 있습니다. 또는 RCW 자체가 프록시인 경우 호출로 인해 RPC_E_WRONG_THREAD의 HRESULT로 <xref:System.Runtime.InteropServices.COMException>이 throw될 수 있습니다.  
  
## <a name="cause"></a>원인  
 CLR이 OLE 아파트 또는 컨텍스트로 전환하려고 할 때 이러한 아파트 또는 컨텍스트가 종료되었습니다. 이 문제는 대개 아파트가 소유한 모든 COM 구성 요소가 완전히 해제되기 전에 STA 아파트가 종료되기 때문에 발생합니다. 이는 사용자 코드의 RCW에 대한 명시적 호출의 결과로 발생하거나, CLR 자체가 COM 구성 요소를 조작(예: 연결된 RCW가 가비지 수집되었을 때 CLR이 COM 구성 요소를 해제하는 경우)하는 동안 발생할 수 있습니다.  
  
## <a name="resolution"></a>해결 방법  
 이 문제를 방지하려면 STA를 소유한 스레드가 애플리케이션이 아파트에 존재하는 모든 개체에서 종료되기 전에 종료되지 않도록 합니다. 동일한 내용이 컨텍스트에도 적용됩니다. 컨텍스트가 애플리케이션이 컨텍스트 내에 존재하는 모든 COM 구성 요소에서 완전히 종료되기 전에 종료되지 않도록 합니다.  
  
## <a name="effect-on-the-runtime"></a>런타임에 대한 영향  
 이 MDA는 CLR에 아무런 영향을 미치지 않습니다. 연결이 끊어진 컨텍스트에 대한 데이터를 보고할 뿐입니다.  
  
## <a name="output"></a>출력  
 연결이 끊어진 아파트 또는 컨텍스트의 컨텍스트 쿠키를 보고합니다.  
  
## <a name="configuration"></a>Configuration  
  
```xml  
<mdaConfig>  
  <assistants>  
    <disconnectedContext />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [관리 디버깅 도우미를 사용하여 오류 진단](diagnosing-errors-with-managed-debugging-assistants.md)
- [interop 마샬링](../interop/interop-marshaling.md)
