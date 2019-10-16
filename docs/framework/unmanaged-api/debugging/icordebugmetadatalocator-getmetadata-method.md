---
title: ICorDebugMetaDataLocator::GetMetaData 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugMetaDataLocator.GetMetaData
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugMetaDataLocator::GetMetaData
helpviewer_keywords:
- ICorDebugMetaDataLocator::GetMetaData method [.NET Framework debugging]
- GetMetaData method, ICorDebugMetaDataLocator interface [.NET Framework debugging]
ms.assetid: f9b0ff22-54db-45eb-9cc3-508000a3141d
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9b761d31e640063e11c1e549966bb372449fe743
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67762278"
---
# <a name="icordebugmetadatalocatorgetmetadata-method"></a>ICorDebugMetaDataLocator::GetMetaData 메서드
디버거가 요청한 작업을 완료하는 데 필요한 메타데이터가 포함된 모듈의 전체 경로를 반환하도록 디버거에 요청합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetMetaData(  
      [in] LPCWSTR wszImagePath,  
      [in] DWORD   dwImageTimeStamp,  
      [in] DWORD   dwImageSize,  
      [in] ULONG32 cchPathBuffer,  
      [out] ULONG32 * pcchPathBuffer,  
      [out, size_is(cchPathBuffer), length_is(*pcchPathBuffer)]  
               WCHAR wszPathBuffer[]  
      );  
```  
  
## <a name="parameters"></a>매개 변수  
 `wszImagePath`  
 [in] 파일의 전체 경로를 나타내는 null로 종료된 문자열입니다. 전체 경로 사용할 수 없는 경우 이름 및 파일의 확장명 (*filename*. *확장*).  
  
 `dwImageTimeStamp`  
 [in] 이미지 PE 파일 헤더의 타임스탬프입니다. 이 매개 변수 기호 서버에 사용 될 수 있습니다 ([SymSrv](/windows/desktop/debug/using-symsrv)) 조회 합니다.  
  
 `dwImageSize`  
 [in] PE 파일 헤더의 이미지 크기입니다. 이 매개 변수는 SymSrv 조회에 사용될 수 있습니다.  
  
 `cchPathBuffer`  
 [in] `wszPathBuffer`의 문자 개수입니다.  
  
 `pcchPathBuffer`  
 [out] `wszPathBuffer`에 기록된 `WCHAR` 개수입니다.  
  
 메서드가 E_NOT_SUFFICIENT_BUFFER를 반환할 경우 경로를 저장하는 데 필요한 `WCHAR` 개수가 포함됩니다.  
  
 `wszPathBuffer`  
 [out] 디버거가 요청된 메타데이터를 포함한 파일의 전체 경로를 복사할 대상 버퍼에 대한 포인터입니다.  
  
 합니다 `ofReadOnly` 에서 플래그를 [CorOpenFlags](../../../../docs/framework/unmanaged-api/metadata/coropenflags-enumeration.md) 열거형이이 파일의 메타 데이터에 대 한 읽기 전용 액세스를 요청 하는 데 사용 됩니다.  
  
## <a name="return-value"></a>반환 값  
 이 메서드는 다음과 같은 특정 HRESULT뿐만 아니라 메서드 오류를 나타내는 HRESULT 오류도 반환합니다. 모든 기타 오류 HRESULT는 파일을 검색할 수 없음을 의미합니다.  
  
|HRESULT|Description|  
|-------------|-----------------|  
|S_OK|메서드가 완료되었습니다. `wszPathBuffer`는 파일의 전체 경로를 포함하고 null로 종료됩니다.|  
|E_NOT_SUFFICIENT_BUFFER|`wszPathBuffer`의 현재 크기는 전체 경로를 포함하기에 충분하지 않습니다. 이 경우 `pcchPathBuffer`는 종료 null 문자를 비롯하여 필요한 `WCHAR` 개수를 포함하고, `GetMetaData`는 요청된 버퍼 크기와 함께 두 번째로 호출됩니다.|  
  
## <a name="remarks"></a>설명  
 `wszImagePath`에 덤프부터 모듈의 전체 경로가 포함되면 이 매개 변수는 덤프가 수집된 컴퓨터의 경로를 지정합니다. 이 위치에 파일이 있을 수 없거나 같은 이름을 가진 잘못된 파일이 경로에 저장될 수 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorDebugThread4 인터페이스](../../../../docs/framework/unmanaged-api/debugging/icordebugthread4-interface.md)
- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
- [디버깅](../../../../docs/framework/unmanaged-api/debugging/index.md)
