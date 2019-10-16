---
title: ICorDebugAppDomain3 인터페이스
ms.date: 03/30/2017
api_name:
- ICorDebugAppDomain3
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugAppDomain3
helpviewer_keywords:
- ICorDebugAppDomain3 interface [.NET Framework debugging]
ms.assetid: 875ef5be-c1e7-4d95-97e9-d3a667aeaba0
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c3676cb32ceaf6f241672751f0feafbd3cb83e05
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69968866"
---
# <a name="icordebugappdomain3-interface"></a>ICorDebugAppDomain3 인터페이스
응용 프로그램 도메인에 현재 로드 된 Windows 런타임 형식의 관리 되는 표현에 대 한 정보를 검색 하는 메서드를 제공 합니다. 이 인터페이스는 ICorDebugAppDomain 및 ICorDebugAppDomain2 인터페이스의 확장입니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[ICorDebugAppDomain3::GetCachedWinRTTypes](../../../../docs/framework/unmanaged-api/debugging/icordebugappdomain3-getcachedwinrttypes-method.md)|모든 캐시 된 Windows 런타임 형식에 대 한 열거자를 가져옵니다.|  
|[ICorDebugAppDomain3::GetCachedWinRTTypesForIIDs](../../../../docs/framework/unmanaged-api/debugging/icordebugappdomain3-getcachedwinrttypesforiids-method.md)|인터페이스 식별자를 기반으로 응용 프로그램 도메인의 캐시 된 Windows 런타임 형식에 대 한 열거자를 가져옵니다.|  
  
## <a name="remarks"></a>설명  
 이 인터페이스는 디버거에서의 함수 계산 호출과 `M:System.Runtime.InteropServices.Marshal.GetInspectableIIDs(System.Object)`함께 사용 됩니다. 메서드가 Windows 런타임 서버 개체에서 지 원하는 인터페이스 식별자를 검색 하는 경우 디버거는이 인터페이스에 정의 된 메서드를 사용 하 여 해당 인터페이스에 해당 하는 관리 되는 형식에 매핑할 수 있습니다.  
  
 이 인터페이스의 인스턴스를 검색 하려면 ICorDebugAppDomain 또는 `QueryInterface` ICorDebugAppDomain2 인터페이스의 인스턴스에서를 실행 합니다.  
  
> [!NOTE]
> 이 인터페이스는 크로스 시스템 또는 크로스 프로세스 원격 호출을 지원하지 않습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** Windows 런타임  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
