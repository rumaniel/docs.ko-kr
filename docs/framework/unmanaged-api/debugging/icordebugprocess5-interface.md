---
title: ICorDebugProcess5 인터페이스
ms.date: 03/30/2017
api_name:
- ICorDebugProcess5
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess5
helpviewer_keywords:
- ICorDebugProcess5 interface [.NET Framework debugging]
ms.assetid: 30a39d79-1f10-4328-9c5d-094ed824e2ba
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 31ecea4857dabc55e8acd3c22a025895a686efcd
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69931082"
---
# <a name="icordebugprocess5-interface"></a>ICorDebugProcess5 인터페이스
관리 되는 힙에 대 한 액세스를 지원 하 고, 관리 되는 개체의 가비지 수집에 대 한 정보를 제공 하 고, 디버거가 응용 프로그램 로컬 네이티브 이미지 캐시에서 이미지를 로드 하는지 여부를 확인 하기 위해 ICorDebugProcess 인터페이스를 확장 합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|Description|  
|------------|-----------------|  
|[EnableNGenPolicy 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess5-enablengenpolicy-method.md)|응용 프로그램에서 관리 되는 디버거를 실행 하는 동안 네이티브 이미지를 로드 하는 방법을 결정 하는 값을 설정 합니다.|  
|[EnumerateGCReferences 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess5-enumerategcreferences-method.md)|프로세스에서 가비지 수집 될 모든 개체에 대 한 열거자를 가져옵니다.|  
|[EnumerateHandles 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess5-enumeratehandles-method.md)|프로세스의 개체 핸들에 대 한 열거자를 가져옵니다.|  
|[EnumerateHeap 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess5-enumerateheap-method.md)|관리 되는 힙의 개체에 대 한 열거자를 가져옵니다.|  
|[EnumerateHeapRegions 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess5-enumerateheapregions-method.md)|관리 되는 힙의 영역에 대 한 열거자를 가져옵니다.|  
|[GetArrayLayout 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess5-getarraylayout-method.md)|메모리에서 배열의 레이아웃에 대 한 정보를 가져옵니다.|  
|[GetGCHeapInformation 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess5-getgcheapinformation-method.md)|관리 되는 힙에서 가비지 수집 될 개체에 대 한 정보를 포함 하는 [COR_HEAPINFO](../../../../docs/framework/unmanaged-api/debugging/cor-heapinfo-structure.md) 구조체에 대 한 포인터를 가져옵니다.|  
|[GetObject 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess5-getobject-method.md)|관리 되는 힙의 개체에 대 한 포인터를 가져옵니다.|  
|[GetTypeFields 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess5-gettypefields-method.md)|형식 식별자를 기반으로 하는 형식에 대 한 필드 정보가 포함 된 배열에 대 한 포인터를 가져옵니다.|  
|[GetTypeForTypeID 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess5-gettypefortypeid-method.md)|해당 형식 식별자를 기반으로 하는 개체에 대 한 정보를 제공 하는 형식 개체를 가져옵니다.|  
|[GetTypeID 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess5-gettypeid-method.md)|지정 된 주소에 있는 개체의 형식 식별자를 가져옵니다.|  
|[GetTypeLayout 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess5-gettypelayout-method.md)|형식 식별자를 기반으로 메모리에 있는 개체의 레이아웃에 대 한 정보를 가져옵니다.|  
  
## <a name="remarks"></a>설명  
 이 인터페이스는 ICorDebugProcess, ICorDebugProcess2 및 [ICorDebugProcess3](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess3-interface.md) 인터페이스를 논리적으로 확장 합니다.  
  
> [!NOTE]
> 이 인터페이스는 다른 컴퓨터 또는 다른 프로세스에서 원격으로 호출 되는 것을 지원 하지 않습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
- [디버깅](../../../../docs/framework/unmanaged-api/debugging/index.md)
