---
title: invalidCERCall MDA
ms.date: 03/30/2017
helpviewer_keywords:
- invalid CER calls
- InvalidCERCall MDA
- MDAs (managed debugging assistants), CER calls
- constrained execution regions
- CER calls
- managed debugging assistants (MDAs), CER calls
ms.assetid: c4577410-602e-44e5-9dab-fea7c55bcdfe
author: mairaw
ms.author: mairaw
ms.openlocfilehash: d508beb697e07f7d3b960b6627b9a07ffe25adf4
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052631"
---
# <a name="invalidcercall-mda"></a>invalidCERCall MDA
`invalidCERCall` MDA(관리 디버깅 도우미)는 안정성 계약 또는 지나치게 약한 계약이 없는 메서드에 대한 호출이 CER(제약이 있는 실행 영역) 그래프 내에 있으면 활성화됩니다. 약한 계약은 가장 나쁜 사례 상태 손상이 호출에 전달된 인스턴스보다 큰 범위에 관련됨을 선언하는 계약입니다. 즉, <xref:System.AppDomain> 또는 프로세스 상태가 손상될 수 있거나 CER 내에서 호출될 때 결과가 항상 결정적으로 계산 가능한 것은 아닙니다.  
  
## <a name="symptoms"></a>증상  
 CER에서 코드를 실행할 경우 예기치 않은 결과가 나타납니다. 증상은 구체적이지 않습니다. 불안정한 메서드에 대한 호출 시, 런타임이 해당 메서드를 미리 준비하거나 런타임에 <xref:System.Threading.ThreadAbortException> 예외로부터 보호하지 않았기 때문에 예기치 않은 <xref:System.OutOfMemoryException>, <xref:System.Threading.ThreadAbortException> 또는 기타 예외가 발생할 수 있습니다. 더 큰 위협은 CER의 목표와 다르게 런타임에 메서드에서 발생하는 예외로 인해 <xref:System.AppDomain> 또는 프로세스가 불안정한 상태가 될 수 있다는 것입니다. 이와 같은 상태 손상을 피하기 위해 CER을 만듭니다. 일관된 상태의 정보가 애플리케이션마다 다르기 때문에 손상된 상태의 증상은 애플리케이션별로 다릅니다.  
  
## <a name="cause"></a>원인  
 CER 내의 코드가 CER에서 실행할 수 없는 <xref:System.Runtime.ConstrainedExecution.ReliabilityContractAttribute>가 포함되지 않거나 약한 <xref:System.Runtime.ConstrainedExecution.ReliabilityContractAttribute>가 포함된 함수를 호출하고 있습니다.  
  
 안정성 계약 구문에서 약한 계약은 <xref:System.Runtime.ConstrainedExecution.Consistency> 열거형 값을 지정하지 않거나 <xref:System.Runtime.ConstrainedExecution.Consistency.MayCorruptProcess>, <xref:System.Runtime.ConstrainedExecution.Consistency.MayCorruptAppDomain> 또는 <xref:System.Runtime.ConstrainedExecution.Cer.None>의 <xref:System.Runtime.ConstrainedExecution.Consistency> 값을 지정하는 계약입니다. 이러한 조건은 호출되는 코드가 일관된 상태를 유지하기 위해 CER에서 다른 코드의 작업을 지연시킬 수 있음을 나타냅니다.  CER을 사용하면 코드가 매우 결정적인 방식으로 오류를 처리할 수 있으므로 애플리케이션에 중요한 내부 고정이 유지되고 메모리 부족 예외와 같은 일시적인 오류가 발생해도 코드가 계속 실행될 수 있습니다.  
  
 이 MDA가 활성화되는 것은 호출자가 예상하지 않았거나 <xref:System.AppDomain> 또는 프로세스가 손상되거나 복구할 수 없게 되는 방식으로 CER에서 호출 중인 메서드가 실패할 수 있는 가능성을 나타냅니다. 물론 호출된 코드는 제대로 실행될 수 있고 문제는 계약이 없다는 것입니다. 신뢰할 수 있는 코드 작성에 관련된 문제는 확인하기 힘들지만 계약이 없다는 것은 코드가 제대로 실행될 수 없음을 나타내는 좋은 표시기입니다. 계약은 프로그래머가 확실히 코딩했고 이러한 보장이 이후 코드 버전에서 변경되지 않을 것임을 약속함을 나타내는 표시기입니다.  즉, 계약은 단순한 구현 세부 정보가 아니라 의도적인 선언입니다.  
  
 약하거나 존재하지 않는 계약이 포함된 메서드는 예측할 수 없는 다양한 방식으로 실패할 수 있으므로 런타임은 지연 JIT 컴파일링, 제네릭 사전 채우기 또는 스레드 중단 등을 통해 도입된 메서드에서 예측할 수 없는 자체적인 오류를 제거하려고 시도하지 않습니다. 즉, 이 MDA가 활성화되면 이것은 런타임이 호출되는 메서드를 정의되는 CER에 포함하지 않았고 이 하위 트리를 계속 준비하면 잠재적인 오류를 마스킹할 수 있기 때문에 호출 그래프가 이 노드에서 종료되었음을 나타냅니다.  
  
## <a name="resolution"></a>해결  
 해당 함수 호출을 사용하지 않거나 유효한 안정성 계약을 함수에 추가합니다.  
  
## <a name="effect-on-the-runtime"></a>런타임에 대한 영향  
 CER에서 약한 계약을 호출하면 작업을 완료하기 위해 CER이 실패할 수 있습니다. 이로 인해 <xref:System.AppDomain> 프로세스 상태가 손상될 수 있습니다.  
  
## <a name="output"></a>출력  
 이 MDA의 샘플 출력은 다음과 같습니다.  
  
 `Method 'MethodWithCer', while executing within a constrained execution region, makes a call at IL offset 0x000C to 'MethodWithWeakContract', which does not have a sufficiently strong reliability contract and might cause non-deterministic results.`  
  
## <a name="configuration"></a>Configuration  
  
```xml  
<mdaConfig>  
  <assistants>  
    <invalidCERCall />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareMethod%2A>
- <xref:System.Runtime.ConstrainedExecution>
- [관리 디버깅 도우미를 사용하여 오류 진단](diagnosing-errors-with-managed-debugging-assistants.md)
