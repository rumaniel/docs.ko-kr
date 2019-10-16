---
title: 제약이 있는 실행 영역
ms.date: 03/30/2017
helpviewer_keywords:
- constrained execution regions
- CERs
ms.assetid: 99354547-39c1-4b0b-8553-938e8f8d1808
author: mairaw
ms.author: mairaw
ms.openlocfilehash: a0561ff5212fd6bc4e9015bea8da1d1082dd027e
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71046689"
---
# <a name="constrained-execution-regions"></a>제약이 있는 실행 영역
CER(제약이 있는 실행 영역)은 신뢰할 수 있는 관리 코드를 작성하기 위한 메커니즘에 포함됩니다. CER은 CLR(공용 언어 런타임 지원)이 영역의 전체 코드가 실행되지 않도록 하는 대역 외 예외를 throw하지 못하도록 제한되는 영역을 정의합니다. 해당 영역 내에서 사용자 코드는 대역 외 예외 throw를 초래하는 실행이 제한됩니다. <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions%2A> 메서드는 `try` 블록 바로 앞에 와야 하고 `catch`, `finally` 및 `fault` 블록을 제약이 있는 실행 영역으로 표시합니다. 제약이 있는 영역으로 표시된 후 코드는 강한 안정성 계약을 사용하여 다른 코드를 호출해야 하고 코드는 실패를 처리할 준비가 된 경우에만 준비되지 않거나 신뢰할 수 없는 메서드에 대한 가상 호출을 할당하거나 수행할 수 있습니다. CLR은 CER에서 실행되는 코드의 스레드 중단을 지연합니다.  
  
 제약이 있는 실행 영역은 <xref:System.Runtime.CompilerServices.RuntimeHelpers.ExecuteCodeWithGuaranteedCleanup%2A> 메서드를 사용하여 실행된 <xref:System.Runtime.ConstrainedExecution.CriticalFinalizerObject> 클래스 및 코드에서 파생된 클래스에서 실행되는 특히 중요한 종료자인 주석이 달린 `try` 블록 이외에 CLR의 다양한 형식으로 사용됩니다.  
  
## <a name="cer-advance-preparation"></a>CER 사전 준비  
 CLR은 메모리 부족 조건을 피하기 위해 사전에 CER을 준비합니다. CLR이 Just-In-Time 컴파일 또는 형식 로딩 중에 메모리 부족 조건을 초래하지 않으려면 사전 준비가 필요합니다.  
  
 개발자는 코드 영역이 CER임을 나타내야 합니다.  
  
- <xref:System.Runtime.ConstrainedExecution.ReliabilityContractAttribute> 특성이 적용된 전체 호출 그래프의 최상위 CER 영역 및 메서드는 사전에 준비됩니다. <xref:System.Runtime.ConstrainedExecution.ReliabilityContractAttribute>는 <xref:System.Runtime.ConstrainedExecution.Cer.Success> 또는 <xref:System.Runtime.ConstrainedExecution.Cer.MayFail>의 보장만 명시할 수 있습니다.  
  
- 가상 디스패치와 같이 정적으로 결정될 수 없는 호출의 경우 사전 준비를 수행할 수 없습니다. 이 경우 <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareMethod%2A> 메서드를 사용합니다. <xref:System.Runtime.CompilerServices.RuntimeHelpers.ExecuteCodeWithGuaranteedCleanup%2A> 메서드를 사용할 경우 <xref:System.Runtime.ConstrainedExecution.PrePrepareMethodAttribute> 특성을 정리 코드에 적용해야 합니다.  
  
## <a name="constraints"></a>제약 조건  
 사용자는 CER에서 작성할 수 있는 코드 형식이 제한됩니다. 코드는 다음 작업에서 발생할 수 있는 것과 같은 대역 외 예외를 초래할 수 없습니다.  
  
- 명시적 할당  
  
- Boxing  
  
- 잠금 획득  
  
- 가상으로 준비되지 않은 메서드 호출  
  
- 약하거나 존재하지 않는 안전성 계약을 사용하여 메서드 호출  
  
 .NET Framework 버전 2.0에서 이러한 제약 조건은 지침입니다. 진단은 코드 분석 도구를 통해 제공됩니다.  
  
## <a name="reliability-contracts"></a>안정성 계약  
 <xref:System.Runtime.ConstrainedExecution.ReliabilityContractAttribute>는 특정 메서드의 안전성 보장 및 손상 상태를 설명하는 사용자 지정 특성입니다.  
  
### <a name="reliability-guarantees"></a>안전성 보장  
 <xref:System.Runtime.ConstrainedExecution.Cer> 열거 값을 통해 표현되는 안전성 보장은 특정 메서드의 안정성 정도를 나타냅니다.  
  
- <xref:System.Runtime.ConstrainedExecution.Cer.MayFail>. 예외 조건에서 메서드가 실패할 수 있습니다. 이 경우 메서드는 성공 여부를 호출 메서드에 다시 보고합니다. 반환 값을 보고할 수 있으려면 메서드가 CER에 포함되어야 합니다.  
  
- <xref:System.Runtime.ConstrainedExecution.Cer.None>. 메서드, 형식 또는 어셈블리에는 CER 개념이 없으며 상태 손상으로 인한 큰 완화 없이 CER 내에서 호출하기에 안전하지 않을 수 있습니다. CER 보장의 장점을 활용하지 못합니다. 이것은 다음을 의미합니다.  
  
    1. 예외 조건에서 메서드가 실패할 수 있습니다.  
  
    2. 메서드는 실패 사실을 보고할 수도 있고 보고하지 않을 수도 있습니다.  
  
    3. 메서드는 CER을 사용하도록 작성되지 않을 가능성이 큽니다.  
  
    4. 메서드, 형식 또는 어셈블리가 성공한 것으로 명시적으로 식별되지 않으면 암시적으로 <xref:System.Runtime.ConstrainedExecution.Cer.None>으로 식별됩니다.  
  
- <xref:System.Runtime.ConstrainedExecution.Cer.Success>. 예외 조건에서 메서드가 성공하도록 보장됩니다. 이 안전성 수준을 획득하려면 CER이 아닌 영역 내에서 호출되는 경우에도 항상 호출되는 메서드 주위에 CER을 생성해야 합니다. 성공을 주관적으로 볼 수 있더라도 메서드가 의도된 작업을 수행하면 성공한 것입니다. 예를 들어 `ReliabilityContractAttribute(Cer.Success)`를 사용하여 Count를 표시하는 것은 CER에서 실행되는 경우 항상 <xref:System.Collections.ArrayList>에 있는 요소 수를 반환하고 내부 필드를 결정되지 않은 상태로 남겨 두지 않음을 의미합니다.  그러나 성공의 경우 값이 경합 상태로 인해 새 값으로 대체될 수 없음을 의미할 수도 있다는 것을 이해하면 <xref:System.Threading.Interlocked.CompareExchange%2A> 메서드가 성공으로도 표시됩니다.  핵심 포인트는 메서드가 설명된 방식대로 동작하고 CER 코드가 올바르지만 신뢰할 수 없는 코드가 어떻게 보이는지에 관계없이 비정상적인 동작을 예상하도록 작성될 필요가 없다는 것입니다.  
  
### <a name="corruption-levels"></a>손상 수준  
 <xref:System.Runtime.ConstrainedExecution.Consistency> 열거 값을 통해 표현되는 손상 수준은 상태가 특정 환경에서 손상될 수 있는 정도를 나타냅니다.  
  
- <xref:System.Runtime.ConstrainedExecution.Consistency.MayCorruptAppDomain>. 예외 조건에서 CLR(공용 언어 런타임)이 현재 애플리케이션 도메인에서 상태 일관성에 관한 보장을 하지 않습니다.  
  
- <xref:System.Runtime.ConstrainedExecution.Consistency.MayCorruptInstance>. 예외 조건에서 메서드가 상태 손상을 현재 인스턴스로 제한하도록 보장합니다.  
  
- <xref:System.Runtime.ConstrainedExecution.Consistency.MayCorruptProcess>. 예외 조건에서 CLR은 상태 일관성에 관한 보장을 하지 않습니다. 즉, 조건이 프로세스를 손상시킬 수 있습니다.  
  
- <xref:System.Runtime.ConstrainedExecution.Consistency.WillNotCorruptState>. 예외 조건에서 메서드가 상태를 손상시키지 않도록 보장합니다.  
  
## <a name="reliability-trycatchfinally"></a>안전성 try/catch/finally  
 안전성 `try/catch/finally`는 관리되지 않는 버전과 동일한 수준의 예측 가능성 보장을 사용하는 예외 처리 메커니즘입니다. `catch/finally` 블록은 CER입니다. 블록에 있는 메서드의 경우 사전 준비가 필요하고 중단할 수 없어야 합니다.  
  
 .NET Framework 버전 2.0에서 코드는 try 블록 바로 전에 <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions%2A>를 호출하여 try를 신뢰할 수 있음을 런타임에 알립니다. <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions%2A>는 컴파일러 지원 클래스인 <xref:System.Runtime.CompilerServices.RuntimeHelpers>의 멤버입니다. 컴파일러를 통해 가성을 보류하여 직접 <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions%2A>를 호출합니다.  
  
## <a name="noninterruptible-regions"></a>중단할 수 없는 영역  
 중단할 수 없는 영역은 명령 집합을 CER로 그룹화합니다.  
  
 .NET Framework 버전 2.0에서 컴파일러 지원을 통해 가용성을 보류하면 사용자 코드는 <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions%2A> 메서드 호출 뒤에 빈 try/catch가 포함된 신뢰할 수 있는 try/catch/finally를 사용하여 중단할 수 없는 영역을 만듭니다.  
  
## <a name="critical-finalizer-object"></a>중요 종료자 개체  
 <xref:System.Runtime.ConstrainedExecution.CriticalFinalizerObject>는 가비지 수집이 종료자를 실행하도록 보장합니다. 할당 시 종료자 및 해당 호출 그래프는 사전에 준비됩니다. 종료자 메서드는 CER에서 실행되고 CER 및 종료자에 대한 모든 제약 조건을 따라야 합니다.  
  
 <xref:System.Runtime.InteropServices.SafeHandle> 및 <xref:System.Runtime.InteropServices.CriticalHandle>에서 상속되는 모든 형식은 CER 내에 종료자 실행이 포함되도록 보장합니다. 핸들을 해제하는 데 필요한 코드를 실행하도록 <xref:System.Runtime.InteropServices.SafeHandle> 파생 클래스에서 <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A>을 구현합니다.  
  
## <a name="code-not-permitted-in-cers"></a>CER에서 허용되지 않는 코드  
 다음 작업은 CER에서 허용되지 않습니다.  
  
- 명시적 할당.  
  
- 잠금 획득  
  
- Boxing  
  
- 다차원 배열 액세스.  
  
- 리플렉션을 통한 메서드 호출.  
  
- <xref:System.Threading.Monitor.Enter%2A> 또는 <xref:System.IO.FileStream.Lock%2A>  
  
- 보안 검사. 링크 요청만 수행하지 않습니다.  
  
- COM 개체 및 프록시에 대한 <xref:System.Reflection.Emit.OpCodes.Isinst> 및 <xref:System.Reflection.Emit.OpCodes.Castclass>  
  
- 투명 프록시에 대한 필드 가져오기 또는 설정.  
  
- serialization.  
  
- 함수 포인터 및 대리자.  
  
## <a name="see-also"></a>참고자료

- [안전성 모범 사례](reliability-best-practices.md)
