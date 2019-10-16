---
title: reportAvOnComRelease MDA
ms.date: 03/30/2017
helpviewer_keywords:
- MDAs (managed debugging assistants), reference counting errors
- exceptions, reference counting errors
- ReportAvOnComRelease MDA
- COM release access violations
- user reference counting errors
- managed debugging assistants (MDAs), reference counting errors
- report access violation on Com release
- reference counting errors
ms.assetid: a2b86b63-08b2-4943-b344-3c2cf46ccd31
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 0bea73a30cb103f0e72caf73a633229a0719dc6c
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052323"
---
# <a name="reportavoncomrelease-mda"></a>reportAvOnComRelease MDA
`reportAvOnComRelease` MDA(관리 디버깅 도우미)는 COM interop를 수행하고 원시 COM 호출과 결합된 <xref:System.Runtime.InteropServices.Marshal.Release%2A> 또는 <xref:System.Runtime.InteropServices.Marshal.ReleaseComObject%2A> 메서드를 사용하는 동안 사용자 참조 계산 오류로 인해 예외가 throw되면 활성화됩니다.  
  
## <a name="symptoms"></a>증상  
 액세스 위반 및 메모리 손상이 발생합니다.  
  
## <a name="cause"></a>원인  
 경우에 따라, COM interop를 수행하고 원시 COM 호출과 결합된 <xref:System.Runtime.InteropServices.Marshal.Release%2A> 또는 <xref:System.Runtime.InteropServices.Marshal.ReleaseComObject%2A> 메서드를 사용하는 동안 사용자 참조 계산 오류로 인해 예외가 throw됩니다. 일반적으로 이 예외는 이렇게 하지 않으면 CLR에서 액세스 위반이 발생하여 CLR이 종료되기 때문에 무시됩니다. 이 도우미를 사용하도록 설정한 경우 이러한 예외는 단순히 무시되는 것이 아니라 감지 및 보고될 수 있습니다.  
  
## <a name="resolution"></a>해결 방법  
 참조 계산 코드를 검토하고 오류를 검색하며, 개체의 네이티브 클라이언트에 참조 계산 오류가 있는지 검토합니다.  
  
## <a name="effect-on-the-runtime"></a>런타임에 대한 영향  
 두 가지 모드를 사용할 수 있습니다. `allowAv` 특성이 `true`인 경우 도우미가 런타임에서 액세스 위반을 무시하지 못하도록 합니다. `allowAv`가 `false`(기본값)인 경우 런타임에서 액세스 위반을 무시하지만 예외가 throw 및 무시되었음을 나타내는 경고 메시지가 사용자에게 보고됩니다.  
  
## <a name="output"></a>출력  
 가능한 경우 출력에 COM 인터페이스 포인터의 원래 vtable이 포함됩니다. 그러지 않으면 정보 메시지가 표시됩니다.  
  
## <a name="configuration"></a>Configuration  
  
```xml  
<mdaConfig>  
  <assistants>  
    <reportAvOnComRelease />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [관리 디버깅 도우미를 사용하여 오류 진단](diagnosing-errors-with-managed-debugging-assistants.md)
- [interop 마샬링](../interop/interop-marshaling.md)
