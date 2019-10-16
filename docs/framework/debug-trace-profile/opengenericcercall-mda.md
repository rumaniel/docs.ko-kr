---
title: openGenericCERCall MDA
ms.date: 03/30/2017
helpviewer_keywords:
- MDAs (managed debugging assistants), CER calls
- open generic CER calls
- constrained execution regions
- openGenericCERCall MDA
- CER calls
- managed debugging assistants (MDAs), CER calls
- generics [.NET Framework], open generic CER calls
ms.assetid: da3e4ff3-2e67-4668-9720-fa776c97407e
author: mairaw
ms.author: mairaw
ms.openlocfilehash: fa6ad656a5f762bf86d277d986bb087c97d7a78f
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052412"
---
# <a name="opengenericcercall-mda"></a>openGenericCERCall MDA
루트 메서드에서 제네릭 형식 변수를 사용하는 제약이 있는 실행 지역(CER) 그래프가 JIT 컴파일 또는 네이티브 이미지 생성 시에 처리되며 제네릭 형식 변수 중 하나 이상의 개체 참조 형식임을 경고하기 위해 `openGenericCERCall` 관리 디버깅 도우미가 활성화됩니다.  
  
## <a name="symptoms"></a>증상  
 스레드가 중단되거나 애플리케이션 도메인이 언로드되면 CER 코드가 실행되지 않습니다.  
  
## <a name="cause"></a>원인  
 결과적으로 생성되는 코드는 공유되며 각 개체 참조 형식 변수는 임의 개체 참조 형식일 수 있으므로 JIT 컴파일 시 개체 참조 형식을 포함하는 인스턴스는 대표일 뿐입니다. 따라서 런타임 리소스를 미리 준비하지 못할 수 있습니다.  
  
 특히 제네릭 형식 변수를 사용하는 메서드는 백그라운드에서 리소스 할당을 지연시킬 수 있습니다. 이러한 항목은 제네릭 사전 항목이라고 합니다. 예를 들어, `T`가 제네릭 형식 변수인 `List<T> list = new List<T>();` 문의 경우 런타임 시 인스턴스를 검색하고 정확하게 생성해야 할 수도 있습니다(예: `List<Object>, List<String>` 등). 메모리 부족과 같이 개발자가 제어할 수 없는 다양한 이유 때문일 수 있습니다.  
  
 이 MDA는 정확한 인스턴스가 있을 때가 아니라 JIT 컴파일 시에만 활성화되어야 합니다.  
  
 이 MDA가 활성화되면 잘못된 인스턴스에 대해 CER이 작동하지 않는 증상이 발생할 가능성이 큽니다. 실제로 MDA를 활성화하게 한 환경에서 런타임 시 CER을 구현하지 않았습니다. 따라서 개발자가 CER의 공유 인스턴스를 사용하는 경우, 의도된 CER 지역 내의 JIT 컴파일 오류, 제네릭 형식 로딩 오류 또는 스레드 중단이 발견되지 않습니다.  
  
## <a name="resolution"></a>해결  
 CER을 포함할 수 있는 메서드의 개체 참조 형식인 제네릭 형식 변수를 사용하지 마세요.  
  
## <a name="effect-on-the-runtime"></a>런타임에 대한 영향  
 이 MDA는 CLR에 아무런 영향을 미치지 않습니다.  
  
## <a name="output"></a>출력  
 다음은 이 MDA의 출력 샘플입니다.  
  
 `Method 'GenericMethodWithCer', which contains at least one constrained execution region, cannot be prepared automatically since it has one or more unbound generic type parameters.`  
  
 `The caller must ensure this method is prepared explicitly at run time prior to execution.`  
  
 `method name="GenericMethodWithCer"`  
  
 `declaringType name="OpenGenericCERCall"`  
  
## <a name="configuration"></a>구성하기  
  
```xml  
<mdaConfig>  
  <assistants>  
    <openGenericCERCall/>  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="example"></a>예제  
 CER 코드가 실행되지 않습니다.  
  
```csharp
using System;  
using System.Collections.Generic;  
using System.Runtime.CompilerServices;  
  
class Program  
{  
    static void Main(string[] args)  
    {  
        CallGenericMethods();  
    }  
    static void CallGenericMethods()  
    {  
        // This call is correct. The instantiation of the method  
        // contains only nonreference types.  
        MyClass.GenericMethodWithCer<int>();  
  
        // This call is incorrect. A shared version of the method that  
        // cannot be completely analyzed will be JIT-compiled. The   
        // MDA will be activated at JIT-compile time, not at run time.  
        MyClass.GenericMethodWithCer<String>();  
    }  
}  
  
    class MyClass  
{  
    public static void GenericMethodWithCer<T>()  
    {  
        RuntimeHelpers.PrepareConstrainedRegions();  
        try  
        {  
  
        }  
        finally  
        {  
            // This is the start of the CER.  
            Console.WriteLine("In finally block.");  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareMethod%2A>
- <xref:System.Runtime.ConstrainedExecution>
- [관리 디버깅 도우미를 사용하여 오류 진단](diagnosing-errors-with-managed-debugging-assistants.md)
