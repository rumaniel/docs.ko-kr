---
title: invalidGCHandleCookie MDA
ms.date: 03/30/2017
helpviewer_keywords:
- MDAs (managed debugging assistants), invalid cookies
- cookies, invalid
- managed debugging assistants (MDAs), invalid cookies
- InvalidGCHandleCookie MDA
- invalid cookies
ms.assetid: 613ad742-3c11-401d-a6b3-893ceb8de4f8
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 7452ae28d63c89845b45bf500c02e771f0b8f4df
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052606"
---
# <a name="invalidgchandlecookie-mda"></a>invalidGCHandleCookie MDA
`invalidGCHandleCookie` MDA(관리 디버깅 도우미)는 잘못된 <xref:System.IntPtr> 쿠키에서 <xref:System.Runtime.InteropServices.GCHandle>로 변환하려고 시도하면 활성화됩니다.  
  
## <a name="symptoms"></a>증상  
 <xref:System.IntPtr>에서 <xref:System.Runtime.InteropServices.GCHandle>을 사용하거나 검색하려고 시도할 때 액세스 위반 및 메모리 손상과 같은 정의되지 않은 동작이 나타납니다.  
  
## <a name="cause"></a>원인  
 쿠키가 원래 <xref:System.Runtime.InteropServices.GCHandle>에서 만들어지지 않았거나, 이미 해제된 <xref:System.Runtime.InteropServices.GCHandle>을 나타내거나, 다음 애플리케이션 도메인의 <xref:System.Runtime.InteropServices.GCHandle>에 대한 쿠키이거나, 네이티브 코드에 <xref:System.Runtime.InteropServices.GCHandle>로 마샬링되지만 캐스팅이 시도된 <xref:System.IntPtr>로 다시 CLR에 전달되었기 때문에 쿠키가 잘못될 수 있습니다.  
  
## <a name="resolution"></a>해결  
 <xref:System.Runtime.InteropServices.GCHandle>에 대한 유효한 <xref:System.IntPtr> 쿠키를 지정합니다.  
  
## <a name="effect-on-the-runtime"></a>런타임에 대한 영향  
 이 MDA가 사용하도록 설정되면 다시 전달된 쿠키 값이 MDA가 사용되지 않을 경우 반환되는 쿠키 값과 다르기 때문에 디버거는 더 이상 원래 개체에 대한 루트를 추적할 수 없습니다.  
  
## <a name="output"></a>출력  
 잘못된 <xref:System.IntPtr> 쿠키 값이 보고됩니다.  
  
## <a name="configuration"></a>Configuration  
  
```xml  
<mdaConfig>  
  <assistants>  
    <invalidGCHandleCookie />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.InteropServices.GCHandle.FromIntPtr%2A>
- <xref:System.Runtime.InteropServices.GCHandle>
- [관리 디버깅 도우미를 사용하여 오류 진단](diagnosing-errors-with-managed-debugging-assistants.md)
