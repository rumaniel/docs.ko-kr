---
title: ICorPublish::EnumProcesses 메서드
ms.date: 03/30/2017
api_name:
- ICorPublish.EnumProcesses
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorPublish::EnumProcesses
helpviewer_keywords:
- ICorPublish::EnumProcesses method [.NET Framework debugging]
- EnumProcesses method [.NET Framework debugging]
ms.assetid: 4ae765f0-93b2-4b6f-aea1-7b0cf44e04a7
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1804a14c1197148afbffb5ec2cb4f29cb9ff019e
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67774561"
---
# <a name="icorpublishenumprocesses-method"></a>ICorPublish::EnumProcesses 메서드
이 컴퓨터에서 실행 되는 관리 되는 프로세스에 대 한 열거자를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT EnumProcesses (  
    [in] COR_PUB_ENUMPROCESS       Type,  
    [out] ICorPublishProcessEnum   **ppIEnum  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `Type`  
 값을 [COR_PUB_ENUMPROCESS](../../../../docs/framework/unmanaged-api/debugging/cor-pub-enumprocess-enumeration.md) 검색 해야 하는 프로세스의 형식을 지정 하는 열거형입니다. 현재 버전에서는 COR_PUB_MANAGEDONLY만 유효합니다.  
  
 `ppIEnum`  
 주소에 대 한 포인터를 [ICorPublishProcessEnum](../../../../docs/framework/unmanaged-api/debugging/icorpublishprocessenum-interface.md) 인스턴스 프로세스의 열거자입니다.  
  
## <a name="remarks"></a>설명  
 프로세스의 열거자의 컬렉션은 스냅숏을 기반으로 실행 하는 경우 프로세스의는 `EnumProcesses` 메서드가 호출 됩니다. 열거자는 종료 하기 전에 또는 후에 시작 하는 모든 프로세스를 포함 하지 것입니다 `EnumProcesses` 라고 합니다.  
  
 합니다 `EnumProcesses` 이 메서드를 두 번 이상 호출할 수 있습니다 [ICorPublish](../../../../docs/framework/unmanaged-api/debugging/icorpublish-interface.md) 인스턴스 프로세스의 새 최신 컬렉션을 만듭니다. 기존 컬렉션의 후속 호출에 의해 적용 되지 것입니다는 `EnumProcesses` 메서드.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorPub.idl, CorPub.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorPublish 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icorpublish-interface.md)
