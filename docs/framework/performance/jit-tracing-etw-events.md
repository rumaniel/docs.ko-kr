---
title: JIT 추적 ETW 이벤트
ms.date: 03/30/2017
helpviewer_keywords:
- JIT tracing events [.NET Framework]
- ETW, JIT tracing events (CLR)
ms.assetid: 926adde2-c123-452e-bf4f-4b977bf06ffb
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 145a53363c9d7aca622ee0b1ccb2700e5984397d
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71046422"
---
# <a name="jit-tracing-etw-events"></a>JIT 추적 ETW 이벤트
<a name="top"></a> 이들 이벤트는 JIT(Just-In-Time) 인라인 처리 및 JIT 마무리 호출의 성공 또는 실패와 관련된 정보를 수집합니다.  
  
 JIT 추적 이벤트는 다음 두 범주로 구성됩니다.  
  
- [JIT 인라인 처리 이벤트](#jit_inlining_events)  
  
- [JIT 마무리 호출 이벤트](#jit_tail_call_events)  
  
<a name="jit_inlining_events"></a>   
## <a name="jit-inlining-events"></a>JIT 인라인 처리 이벤트  
  
### <a name="methodjitinliningfailed-event"></a>MethodJitInliningFailed 이벤트  
 다음 표에서는 키워드와 수준을 보여 줍니다. 자세한 내용은 [CLR ETW Keywords and Levels](clr-etw-keywords-and-levels.md)을 참조하세요.  
  
|이벤트를 발생시키기 위한 키워드|Level|  
|-----------------------------------|-----------|  
|`JITTracingKeyword` (0x10)|자세한 정보 표시(5)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|발생 시기|  
|-----------|--------------|-----------------|  
|`MethodJitInliningFailed`|186|JIT 인라인 처리에 실패했습니다.|  
  
 다음 표에서는 이벤트 데이터를 보여 줍니다.  
  
|필드 이름|데이터 형식|Description|  
|----------------|---------------|-----------------|  
|MethodBeingCompiledNameSpace|win:UnicodeString|컴파일되는 메서드의 네임스페이스입니다.|  
|MethodBeingCompiledName|win:UnicodeString|컴파일되는 메서드의 이름입니다.|  
|MethodBeingCompiledNameSignature|win:UnicodeString|컴파일되는 메서드의 서명입니다.|  
|InlinerNamespace|win:UnicodeString|JIT 컴파일러가 코드를 생성할 메서드의 네임스페이스입니다.|  
|InlinerName|win:UnicodeString|컴파일러가 코드를 생성할 메서드의 이름입니다. 컴파일러가 `MethodBeingCompiledName` 에 대한 호출을 생성하는 대신 코드를 `MethodBeingCompiledName` 으로 인라인 처리하려고 하면 이름이 `InlinerName`과 같지 않을 수 있습니다.|  
|InlinerNameSignature|win:UnicodeString|인라인 처리자에 대한 서명입니다.|  
|InlineeNamespace|win:UnicodeString|인라인 대상의 네임스페이스입니다.|  
|InlineeName|win:UnicodeString|컴파일러가 인라인 처리하려고 하는 메서드입니다(호출을 생성하지 않음).|  
|InlineeNameSignature|win:UnicodeString|인라인 대상에 대한 서명입니다.|  
|FailAlways|win:Boolean|인라인 대상에 대한 인라인 처리가 항상 실패함을 JIT 컴파일러에 알리는 힌트입니다.|  
|FailReason|win:UnicodeString|INLINE_NEVER는 어떤 다른 이유로 인라인 처리가 실패할 것으로 확인된 이전 인라인 처리 시도를 의미합니다. 이외의 경우는 자유 형식 텍스트입니다.|  
|ClrInstanceID|win:UnicodeString|CLR 또는 CoreCLR 인스턴스에 대한 고유 ID입니다.|  
  
### <a name="methodjitinliningsucceeded-event"></a>MethodJitInliningSucceeded 이벤트  
 다음 표에서는 키워드와 수준을 보여 줍니다.  
  
|이벤트를 발생시키기 위한 키워드|Level|  
|-----------------------------------|-----------|  
|`JITTracingKeyword` (0x10)|자세한 정보 표시(5)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|발생 시기|  
|-----------|--------------|-----------------|  
|`MethodJitInliningSucceeded`|185|메서드 인라인 처리에 성공했습니다.|  
  
 다음 표에서는 이벤트 데이터를 보여 줍니다.  
  
|필드 이름|데이터 형식|Description|  
|----------------|---------------|-----------------|  
|MethodBeingCompiledNameSpace|win:UnicodeString|컴파일되는 메서드의 네임스페이스입니다.|  
|MethodBeingCompiledName|win:UnicodeString|컴파일되는 메서드의 이름입니다.|  
|MethodBeingCompiledNameSignature|win:UnicodeString|컴파일되는 메서드의 서명입니다.|  
|InlinerNamespace|win:UnicodeString|JIT 컴파일러가 코드를 생성할 메서드의 네임스페이스입니다.|  
|InlinerName|win:UnicodeString|컴파일러가 코드를 생성할 메서드의 이름입니다. 컴파일러가 `MethodBeingCompiledName` 에 대한 호출을 생성하는 대신 코드를 `MethodBeingCompiledName` 으로 인라인 처리하려고 하면 이름이 `InlinerName`과 같지 않을 수 있습니다.|  
|InlinerNameSignature|win:UnicodeString|인라인 처리자에 대한 서명입니다.|  
|InlineeNamespace|win:UnicodeString|인라인 대상의 네임스페이스입니다.|  
|InlineeName|win:UnicodeString|컴파일러가 인라인 처리하려고 하는 메서드입니다(호출을 생성하지 않음).|  
|InlineeNameSignature|win:UnicodeString|인라인 대상에 대한 서명입니다.|  
|ClrInstanceID|win:UInt16|CLR 또는 CoreCLR 인스턴스에 대한 고유 ID입니다.|  
  
 [맨 위로 이동](#top)  
  
<a name="jit_tail_call_events"></a>   
## <a name="jit-tail-call-events"></a>JIT 마무리 호출 이벤트  
  
### <a name="methodjittailcallfailed-event"></a>MethodJITTailCallFailed 이벤트  
 다음 표에서는 키워드와 수준을 보여 줍니다.  
  
|이벤트를 발생시키기 위한 키워드|Level|  
|-----------------------------------|-----------|  
|`JITTracingKeyword` (0x10)|자세한 정보 표시(5)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|발생 시기|  
|-----------|--------------|-----------------|  
|`MethodJitTailCallFailed`|189|메서드 마무리 호출에 실패했습니다.|  
  
 다음 표에서는 이벤트 데이터를 보여 줍니다.  
  
|필드 이름|데이터 형식|설명|  
|----------------|---------------|-----------------|  
|MethodBeingCompiledNameSpace|win:UnicodeString|컴파일되는 메서드의 네임스페이스입니다.|  
|MethodBeingCompiledName|win:UnicodeString|컴파일되는 메서드의 이름입니다.|  
|MethodBeingCompiledNameSignature|win:UnicodeString|컴파일되는 메서드의 서명입니다.|  
|CallerNamespace|win:UnicodeString|JIT 컴파일러가 코드를 생성할 메서드의 네임스페이스입니다.|  
|CallerName|win:UnicodeString|컴파일러가 코드를 생성할 메서드의 이름입니다.|  
|CallerNameSignature|win:UnicodeString|호출자에 대한 서명입니다.|  
|CalleeNamespace|win:UnicodeString|호출 수신자의 네임스페이스입니다.|  
|CalleeName|win:UnicodeString|컴파일러가 마무리 호출하려고 하는 메서드입니다(호출을 생성하지 않음).|  
|CalleeNameSignature|win:UnicodeString|호출자 수신자에 대한 서명입니다.|  
|TailPrefix|win:Boolean|마무리 호출에 대한 접두사입니다.|  
|FailReason|win:UnicodeString|마무리 호출이 실패한 이유입니다.|  
|ClrInstanceID|win:UInt16|CLR 또는 CoreCLR 인스턴스에 대한 고유 ID입니다.|  
  
### <a name="methodjittailcallsucceeded-event"></a>MethodJITTailCallSucceeded 이벤트  
 다음 표에서는 키워드와 수준을 보여 줍니다.  
  
|이벤트를 발생시키기 위한 키워드|Level|  
|-----------------------------------|-----------|  
|`JITTracingKeyword` (0x10)|자세한 정보 표시(5)|  
  
 다음 표에서는 이벤트 정보를 보여 줍니다.  
  
|이벤트|이벤트 ID|발생 시기|  
|-----------|--------------|-----------------|  
|`MethodJitTailCallSucceeded`|188|메서드 마무리 호출에 성공했습니다.|  
  
 다음 표에서는 이벤트 데이터를 보여 줍니다.  
  
|필드 이름|데이터 형식|Description|  
|----------------|---------------|-----------------|  
|MethodBeingCompiledNameSpace|win:UnicodeString|컴파일되는 메서드의 네임스페이스입니다.|  
|MethodBeingCompiledName|win:UnicodeString|컴파일되는 메서드의 이름입니다.|  
|MethodBeingCompiledNameSignature|win:UnicodeString|컴파일되는 메서드의 서명입니다.|  
|CallerNamespace|win:UnicodeString|JIT 컴파일러가 코드를 생성할 메서드의 네임스페이스입니다.|  
|CallerName|win:UnicodeString|컴파일러가 코드를 생성할 메서드의 이름입니다.|  
|CallerNameSignature|win:UnicodeString|호출자에 대한 서명입니다.|  
|CalleeNamespace|win:UnicodeString|호출 수신자의 네임스페이스입니다.|  
|CalleeName|win:UnicodeString|컴파일러가 마무리 호출하려고 하는 메서드입니다(호출을 생성하지 않음).|  
|CalleeNameSignature|win:UnicodeString|호출자 수신자에 대한 서명입니다.|  
|TailPrefix|win:Boolean|마무리 호출에 대한 접두사입니다.|  
|TailCallType|win:UnicodeString|마무리 호출의 형식입니다.|  
|ClrInstanceID|win:UInt16|CLR 또는 CoreCLR 인스턴스에 대한 고유 ID입니다.|  
  
## <a name="see-also"></a>참고자료

- [CLR ETW 이벤트](clr-etw-events.md)
