---
title: ICorPublishProcess::EnumAppDomains 메서드
ms.date: 03/30/2017
api_name:
- ICorPublishProcess.EnumAppDomains
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorPublishProcess::EnumAppDomains
helpviewer_keywords:
- EnumAppDomains method [.NET Framework debugging]
- ICorPublishProcess::EnumAppDomains method [.NET Framework debugging]
ms.assetid: 7da621fc-e7d0-4c00-9439-5c93619d7414
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: c614afee18824e1672b378dd468cb11c9c173d9f
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67764954"
---
# <a name="icorpublishprocessenumappdomains-method"></a>ICorPublishProcess::EnumAppDomains 메서드
이 참조 되는 프로세스의 응용 프로그램 도메인에 대 한 열거자를 가져옵니다 [ICorPublishProcess](../../../../docs/framework/unmanaged-api/debugging/icorpublishprocess-interface.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT EnumAppDomains (  
    [out] ICorPublishAppDomainEnum   **ppEnum  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `ppEnum`  
 [out] 주소에 대 한 포인터를 [ICorPublishAppDomainEnum](../../../../docs/framework/unmanaged-api/debugging/icorpublishappdomainenum-interface.md) 인스턴스가이 프로세스에서 응용 프로그램 도메인의 컬렉션을 반복할 수 있도록 합니다.  
  
## <a name="remarks"></a>설명  
 응용 프로그램 도메인 목록에는 스냅숏을 기반으로 존재 하는 응용 프로그램 도메인의 경우는 `EnumAppDomains` 메서드가 호출 됩니다. 새 최신 목록을 만들려면이 메서드를 두 번 이상 호출할 수 있습니다. 이 메서드가 이후에 호출 하 여 기존 목록을 받지 않습니다.  
  
 프로세스 종료 된 경우 `EnumAppDomains` CORDBG_E_PROCESS_TERMINATED의 HRESULT 값을 사용 하 여 실패 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorPub.idl, CorPub.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorPublishProcess 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icorpublishprocess-interface.md)
