---
title: loadFromContext MDA
ms.date: 03/30/2017
helpviewer_keywords:
- MDAs (managed debugging assistants), LoadFrom context
- managed debugging assistants (MDAs), LoadFrom context
- LoadFrom context
- LoadFromContext MDA
ms.assetid: a9b14db1-d3a9-4150-a767-dcf3aea0071a
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 89605a119e8251ffd577ff402366dff0fd4af4d7
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052513"
---
# <a name="loadfromcontext-mda"></a>loadFromContext MDA
`loadFromContext` MDA(관리 디버깅 도우미)는 어셈블리가 `LoadFrom` 컨텍스트에 로드되면 활성화됩니다. 이 상황은 <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=nameWithType>을 호출하거나 비슷한 메서드를 호출한 결과 발생할 수 있습니다.  
  
## <a name="symptoms"></a>증상  
 일부 로더 메서드를 사용하면 어셈블리가 `LoadFrom` 컨텍스트에 로드될 수 있습니다. 이 컨텍스트를 사용하면 예기치 않은 serialization, 캐스팅 및 종속성 확인 동작이 발생할 수 있습니다. 일반적으로 이러한 문제점을 방지하기 위해 어셈블리를 `Load` 컨텍스트에 로드하는 것이 좋습니다. 이 MDA 없으면 어셈블리가 로드된 컨텍스트를 판별하기가 어렵습니다.  
  
## <a name="cause"></a>원인  
 일반적으로 `Load` 컨텍스트 외부의 경로에서 로드된 경우(예: 전역 어셈블리 캐시 또는 <xref:System.AppDomainSetup.ApplicationBase%2A?displayProperty=nameWithType> 속성) 어셈블리가 `LoadFrom` 컨텍스트에 로드됩니다.  
  
## <a name="resolution"></a>해결  
 더 이상 <xref:System.Reflection.Assembly.LoadFrom%2A>을 호출하지 않아도 되도록 애플리케이션을 구성합니다. 이 작업을 수행할 때 다음 기술을 사용할 수 있습니다.  
  
- 전역 어셈블리 캐시에 어셈블리 설치  
  
- <xref:System.AppDomain>의 <xref:System.AppDomainSetup.ApplicationBase%2A> 디렉터리에 어셈블리를 둡니다. 기본 도메인의 경우 <xref:System.AppDomainSetup.ApplicationBase%2A> 디렉터리에 프로세스를 시작하는 실행 파일이 포함되어 있습니다. 어셈블리를 쉽게 이동할 수 없는 경우 새로운 <xref:System.AppDomain>을 만들어야 할 수도 있습니다.  
  
- 종속 어셈블리가 실행 파일과 관련된 하위 디렉터리에 있는 경우 보조 애플리케이션 도메인 또는 애플리케이션 구성(.config) 파일에 검색 경로를 추가합니다.  
  
 각각의 경우 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 메서드를 사용하도록 코드를 변경할 수 있습니다.  
  
## <a name="effect-on-the-runtime"></a>런타임에 대한 영향  
 MDA는 CLR에 영향을 미치지 않습니다. 로드 요청 결과로 사용된 컨텍스트를 보고합니다.  
  
## <a name="output"></a>출력  
 MDA는 어셈블리가 `LoadFrom` 컨텍스트에 로드되었음을 보고합니다. 어셈블리의 단순한 이름과 경로를 지정합니다. `LoadFrom` 컨텍스트를 사용하지 못하게 완화하도록 제안합니다.  
  
## <a name="configuration"></a>구성하기  
  
```xml  
<mdaConfig>  
  <assistants>  
    <loadFromContext />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="example"></a>예제  
 다음 코드 예제에서는 이 MDA를 활성화할 수 있는 상황을 보여 줍니다.  
  
```csharp
using System.Reflection;  
namespace ConsoleApplication1  
{  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            // The following call caused the LoadFrom context to be used  
            // because the assembly is loaded using LoadFrom and the path is   
            // located outside of the Load context probing path.   
            Assembly.LoadFrom(@"C:\Text\Test.dll");  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>참고자료

- [관리 디버깅 도우미를 사용하여 오류 진단](diagnosing-errors-with-managed-debugging-assistants.md)
