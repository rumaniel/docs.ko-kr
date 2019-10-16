---
title: ICorDebugThread::EnumerateChains 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugThread.EnumerateChains
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread::EnumerateChains
helpviewer_keywords:
- EnumerateChains method [.NET Framework debugging]
- ICorDebugThread::EnumerateChains method [.NET Framework debugging]
ms.assetid: ec00bc21-117e-4acd-9301-2cfafd5be8d3
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a6f0ed843f72d3f1e1575da15776a94a9097fd02
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67771106"
---
# <a name="icordebugthreadenumeratechains-method"></a>ICorDebugThread::EnumerateChains 메서드
이 ICorDebugThread 개체의 모든 스택 체인을 포함 하는 ICorDebugChainEnum 열거자에 대 한 인터페이스 포인터를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT EnumerateChains (  
    [out] ICorDebugChainEnum **ppChains  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `ppChains`  
 [out] 주소에 대 한 포인터는 `ICorDebugChainEnum` 활성 (즉, 가장 최근) 체인에서 시작,이 스레드의 모든 스택 열거를 사용할 수 있는 개체 체인입니다.  
  
## <a name="remarks"></a>설명  
 스택 체인 스레드의 실제 호출 스택을 나타냅니다. 다음과 같은 경우 스택 체인 경계를 만듭니다.  
  
- 관리-비관리 또는 관리 되지 않는 관리로 전환 합니다.  
  
- 컨텍스트 전환 합니다.  
  
- 사용자 스레드의 하이재킹 디버거.  
  
 단일 컨텍스트에 순수 관리 코드를 실행 하는 스레드에 대 한 간단한 경우 스레드 스택 체인 간의 일대일로 대응 존재 합니다.  
  
 디버거 논리 호출 스택을에 모든 스레드의 실제 호출 스택을 다시 정렬 하려고 할 수 있습니다. 여기에 모든 스레드의 체인이 해당 호출자/호출 수신자 관계에 의해 정렬 되 고 이러한 다시 그룹화 포함 됩니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
