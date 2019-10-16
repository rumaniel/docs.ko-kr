---
title: jitCompilationStart MDA
ms.date: 03/30/2017
helpviewer_keywords:
- JIT compilation
- MDAs (managed debugging assistants), JIT compilation
- JitCompilationStart MDA
- managed debugging assistants (MDAs), JIT compilation
ms.assetid: 5ffd2857-d0ba-4342-9824-9ffe04ec135d
author: mairaw
ms.author: mairaw
ms.openlocfilehash: fa6d3832dcd842631d290e046b5e32908ce4bb7e
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052537"
---
# <a name="jitcompilationstart-mda"></a>jitCompilationStart MDA
JIT(Just-In-Time) 컴파일러에서 함수 컴파일을 시작하는 시기를 보고하기 위해 `jitCompilationStart` MDA(관리 디버깅 도우미)가 활성화됩니다.  
  
## <a name="symptoms"></a>증상  
 mscorjit.dll이 프로세스에 로드되므로 이미 네이티브 이미지 형식을 사용하는 프로그램용으로 작업 집합 크기가 증가합니다.  
  
## <a name="cause"></a>원인  
 프로그램이 종속된 어셈블리 중 일부가 원시 형식으로 생성되지 않았거나 올바르게 등록되지 않았습니다.  
  
## <a name="resolution"></a>해결 방법  
 이 MDA를 사용하면 JIT 컴파일되는 함수를 판별할 수 있습니다. 함수가 포함된 어셈블리가 원시 형식으로 생성되어 적절하게 등록되었는지 판별합니다.  
  
## <a name="effect-on-the-runtime"></a>런타임에 대한 영향  
 이 MDA는 메서드가 JIT 컴파일되기 직전의 메시지를 로깅하므로 이 MDA를 사용하면 성능에 상당한 영향을 미칩니다. 메서드가 인라인인 경우 이 MDA는 개별 메시지를 생성하지 않습니다.  
  
## <a name="output"></a>출력  
 다음 코드 샘플은 샘플 출력을 표시합니다. 이 경우 어셈블리 테스트에서 “ns2.CO” 클래스의 “m” 메서드가 JIT 컴파일되었음이 출력에 표시됩니다.  
  
```output
method name="Test!ns2.C0::m"  
```  
  
## <a name="configuration"></a>Configuration  
 다음 구성 파일은 처음 JIT 컴파일될 때 보고되는 메서드를 필터링하기 위해 사용할 수 있는 다양한 필터를 보여 줍니다. Name 특성의 값을로 \*설정 하 여 모든 메서드를 보고 하도록 지정할 수 있습니다.  
  
```xml  
<mdaConfig>  
  <assistants>  
    <jitCompilationStart>  
      <methods>  
        <match name="C0::m" />  
        <match name="MyMethod" />  
        <match name="C2::*" />  
        <match name="ns0::*" />  
        <match name="ns1.C0::*" />  
        <match name="ns2.C0::m" />  
        <match name="ns2.C0+N0::m" />  
      </methods>  
    </jitCompilationStart >  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="example"></a>예제  
 다음 코드 샘플은 이전 구성 파일과 함께 사용됩니다.  
  
```csharp
using System;  
using System.Reflection;  
using System.Runtime.CompilerServices;  
using System.Runtime.InteropServices;  
  
public class Entry  
{  
    public static void Main(string[] args)  
    {  
        C0.m();  
        C1.MyMethod();  
        C2.m();  
  
        ns0.C0.m();  
        ns0.C0.N0.m();  
        ns0.C1.m();  
  
        ns1.C0.m();  
        ns1.C0.N0.m();  
  
        ns2.C0.m();  
        ns2.C0.N0.m();  
    }  
}  
  
public class C0  
{  
    [MethodImpl(MethodImplOptions.NoInlining)]  
    public static void m() { }  
}  
  
public class C1  
{  
    [MethodImpl(MethodImplOptions.NoInlining)]  
    public static void MyMethod() { }  
}  
  
public class C2  
{  
    [MethodImpl(MethodImplOptions.NoInlining)]  
    public static void m() { }  
}  
  
namespace ns0  
{  
    public class C0  
    {  
        [MethodImpl(MethodImplOptions.NoInlining)]  
        public static void m() { }  
  
        public class N0  
        {  
            [MethodImpl(MethodImplOptions.NoInlining)]  
            public static void m() { }  
        }  
    }  
  
    public class C1  
    {  
        [MethodImpl(MethodImplOptions.NoInlining)]  
        public static void m() { }  
    }  
}  
  
namespace ns1  
{  
    public class C0  
    {  
        [MethodImpl(MethodImplOptions.NoInlining)]  
        public static void m() { }  
        public class N0  
        {  
            [MethodImpl(MethodImplOptions.NoInlining)]  
            public static void m() { }  
        }  
    }  
}  
  
namespace ns2  
{  
    public class C0  
    {  
        [MethodImpl(MethodImplOptions.NoInlining)]  
        public static void m() { }  
  
        public class N0  
        {  
            [MethodImpl(MethodImplOptions.NoInlining)]  
            public static void m() { }  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [관리 디버깅 도우미를 사용하여 오류 진단](diagnosing-errors-with-managed-debugging-assistants.md)
- [interop 마샬링](../interop/interop-marshaling.md)
