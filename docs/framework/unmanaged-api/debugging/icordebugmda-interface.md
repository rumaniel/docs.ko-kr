---
title: ICorDebugMDA 인터페이스
ms.date: 03/30/2017
api_name:
- ICorDebugMDA
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugMDA
helpviewer_keywords:
- ICorDebugMDA interface [.NET Framework debugging]
ms.assetid: 8ecbb854-295c-4dd4-b9fc-01ebeac46e06
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a662185bb84e9a66573b43b26ffcd256ecb943f5
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69909845"
---
# <a name="icordebugmda-interface"></a>ICorDebugMDA 인터페이스
MDA(관리 디버깅 도우미) 메시지를 나타냅니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|Description|  
|------------|-----------------|  
|[GetDescription 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugmda-getdescription-method.md)|이 MDA에 대 한 설명을 포함 하는 문자열을 가져옵니다.|  
|[GetFlags 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugmda-getflags-method.md)|이 MDA와 연결 된 플래그를 가져옵니다.|  
|[GetName 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugmda-getname-method.md)|이 MDA의 이름을 포함 하는 문자열을 가져옵니다.|  
|[GetOSThreadId 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugmda-getosthreadid-method.md)|이 MDA가 실행 되 고 있는 운영 체제 스레드 식별자를 가져옵니다.|  
|[GetXML 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugmda-getxml-method.md)|이 MDA와 연결 된 전체 XML 스트림을 가져옵니다.|  
  
## <a name="remarks"></a>설명  
  
> [!NOTE]
> 이 인터페이스는 크로스 시스템 또는 크로스 프로세스 원격 호출을 지원하지 않습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
- [관리 디버깅 도우미를 사용하여 오류 진단](../../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)
