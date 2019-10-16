---
title: memberInfoCacheCreation MDA
ms.date: 03/30/2017
helpviewer_keywords:
- member info cache creation
- MemberInfoCacheCreation MDA
- reflection, run-time errors
- MDAs (managed debugging assistants), cache
- cache [.NET Framework], reflection
- managed debugging assistants (MDAs), cache
- MemberInfo cache
ms.assetid: 5abdad23-1335-4744-8acb-934002c0b6fe
author: mairaw
ms.author: mairaw
ms.openlocfilehash: d3b65ecc226c1caf7b53d746f0583e1f57c7d8c1
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052461"
---
# <a name="memberinfocachecreation-mda"></a>memberInfoCacheCreation MDA
`memberInfoCacheCreation` MDA(관리 디버깅 도우미)는 <xref:System.Reflection.MemberInfo> 캐시를 만들 때 활성화됩니다. 리소스 사용량이 많은 리플렉션 기능을 활용하는 프로그램을 나타냅니다.  
  
## <a name="symptoms"></a>증상  
 프로그램에서 리소스 사용량이 많은 리플렉션을 사용하므로 프로그램의 작업 집합이 증가합니다.  
  
## <a name="cause"></a>원인  
 <xref:System.Reflection.MemberInfo> 개체와 관련된 리플렉션 작업은 콜드 페이지에 저장된 메타데이터를 읽고 일반적으로 프로그램에서 런타임에 바인딩된 시나리오 형식을 사용하는 것을 나타내므로 리소스 이용률이 높은 것으로 간주됩니다.  
  
## <a name="resolution"></a>해결 방법  
 이 MDA를 사용하도록 설정하고 디버거에서 코드를 실행하거나 MDA가 활성화될 때 디버거와 연결하여 프로그램에서 리플렉션이 사용되는 위치를 판별할 수 있습니다. 디버거에서 <xref:System.Reflection.MemberInfo> 캐시가 생성된 위치를 보여 주는 스택 추적을 얻을 수 있으며, 여기에서 프로그램이 리플렉션을 사용하는 위치를 판별할 수 있습니다.  
  
 해결 방법은 코드의 목적에 따라 달라집니다. 이 MDA에서는 프로그램에 런타임에 바인딩된 시나리오가 있음을 알려줍니다. 초기 바인딩 시나리오를 대체할 수 있는지 결정하거나 런타임에 바인딩된 시나리오의 성능을 고려할 수 있습니다.  
  
## <a name="effect-on-the-runtime"></a>런타임에 대한 영향  
 이 MDA는 생성된 모든 <xref:System.Reflection.MemberInfo> 캐시에 사용되도록 활성화됩니다. 성능에 주는 영향은 매우 적습니다.  
  
## <a name="output"></a>출력  
 MDA에서 <xref:System.Reflection.MemberInfo> 캐시가 생성되었음을 표시하는 메시지를 출력합니다. 디버거를 사용하여 프로그램에서 리플렉션을 사용하는 위치를 보여 주는 스택 추적을 가져옵니다.  
  
## <a name="configuration"></a>Configuration  
  
```xml  
<mdaConfig>  
  <assistants>  
    <memberInfoCacheCreation/>  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="example"></a>예제  
 이 샘플 코드에서는 `memberInfoCacheCreation` MDA를 활성화합니다.  
  
```csharp
using System;  
  
public class Exe  
{  
    public static void Main()  
    {  
        typeof(object).GetMethods();  
    }  
}  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Reflection.MemberInfo>
- [관리 디버깅 도우미를 사용하여 오류 진단](diagnosing-errors-with-managed-debugging-assistants.md)
