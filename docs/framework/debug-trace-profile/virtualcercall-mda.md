---
title: virtualCERCall MDA
ms.date: 03/30/2017
helpviewer_keywords:
- MDAs (managed debugging assistants), CER calls
- virtualCERCall MDA
- virtual CER calls
- constrained execution regions
- CER calls
- managed debugging assistants (MDAs), CER calls
ms.assetid: 1eb18c7a-f5e0-443f-80fb-67bfbb047da2
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 561655f1d3de6efcac79c89907602cbf51bd3ff8
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052229"
---
# <a name="virtualcercall-mda"></a>virtualCERCall MDA
`virtualCERCall` MDA(관리 디버깅 도우미)는 CER(제약이 있는 실행 영역) 호출 그래프 내의 호출 사이트가 가상 대상, 즉 최종이 아닌 가상 메서드에 대한 가상 호출 또는 인터페이스를 사용한 호출을 참조함을 나타내는 경고로 활성화됩니다. CLR(공용 언어 런타임)은 중간 언어 및 메타데이터 분석만으로 이러한 호출의 대상 메서드를 예측할 수 없습니다. 결과적으로, CER 그래프의 일부로 호출 트리를 준비할 수 없으며 하위 트리가 자동으로 차단될 수 없다는 점에서 스레드가 중단됩니다. 이 MDA는 호출 대상을 컴퓨팅하는 데 필요한 추가 정보가 런타임 시 확인된 다음 <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareMethod%2A> 메서드에 대한 명시적 호출을 사용하여 CER을 확장해야 하는 경우를 경고합니다.  
  
## <a name="symptoms"></a>증상  
 스레드가 중단되거나 애플리케이션 도메인이 언로드될 때 CER이 실행되지 않습니다.  
  
## <a name="cause"></a>원인  
 CER에 자동으로 준비할 수 없는 가상 메서드 호출이 포함되어 있습니다.  
  
## <a name="resolution"></a>해결  
 가상 메서드에 대해 <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareMethod%2A>를 호출합니다.  
  
## <a name="effect-on-the-runtime"></a>런타임에 대한 영향  
 이 MDA는 CLR에 아무런 영향을 미치지 않습니다.  
  
## <a name="output"></a>출력  
  
```output
Method 'MethodWithCer', while executing within a constrained execution region, makes a call  
at IL offset 0x0024 to 'VirtualMethod', which is virtual and cannot be prepared automatically  
at compile time. The caller must ensure this method is prepared explicitly at  
runtime before entering the constrained execution region.  
method name="VirtualMethod"  
declaringType name="VirtualCERCall+MyClass"  
  declaringModule name="mda"  
    callsite name="MethodWithCer" offset="0x0024"  
```  
  
## <a name="configuration"></a>구성하기  
  
```xml  
<mdaConfig>  
  <assistants>  
    < VirtualCERCall />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="example"></a>예제  
  
```csharp
class MyClass  
{  
    [ReliabilityContract(Consistency.MayCorruptProcess, CER.None)]  
    virtual void VirtualMethod()  
    {  
        ...  
    }  
}  
  
class MyDerivedClass : MyClass  
{  
    [ReliabilityContract(Consistency.MayCorruptProcess, CER.None)]  
    override void VirtualMethod()  
    {  
        ...  
    }  
}  
  
void MethodWithCer(MyClass object)  
{  
    RuntimeHelpers.PrepareConstrainedRegions();  
    try  
    {  
        ...  
    }  
    finally  
    {  
        // Start of the CER.  
  
        // Cannot tell at analysis time whether object is a MyClass  
        // or a MyDerivedClass, so we do not know which version of   
        // VirtualMethod we are going to call.  
        object.VirtualMethod();  
    }  
}  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [관리 디버깅 도우미를 사용하여 오류 진단](diagnosing-errors-with-managed-debugging-assistants.md)
- [interop 마샬링](../interop/interop-marshaling.md)
