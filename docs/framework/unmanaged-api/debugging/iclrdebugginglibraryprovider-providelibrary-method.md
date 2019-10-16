---
title: ICLRDebuggingLibraryProvider::ProvideLibrary 메서드
ms.date: 03/30/2017
api_name:
- ICLRDebuggingLibraryProvider.ProvideLibrary Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDebuggingLibraryProvider::ProvideLibrary
helpviewer_keywords:
- ProvideLibrary method [.NET Framework debugging]
- ICLRDebuggingLibraryProvider::ProvideLibrary method [.NET Framework debugging]
ms.assetid: 86f06245-9517-49be-8d8c-ca5deaf34c02
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a1b02bb74a61e64a3ed9875fcf88e018de9f6317
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70041438"
---
# <a name="iclrdebugginglibraryproviderprovidelibrary-method"></a>ICLRDebuggingLibraryProvider::ProvideLibrary 메서드

CLR (공용 언어 런타임) 버전별 디버깅 라이브러리를 요청 시 배치 하 고 로드할 수 있도록 하는 라이브러리 공급자 콜백 인터페이스를 가져옵니다.

## <a name="syntax"></a>구문

```cpp
HRESULT ProvideLibrary(
     [in] const WCHAR* pwszFileName,
     [in] DWORD dwTimestamp,
     [in] DWORD dwSizeOfImage,
     [out] HMODULE* hModule);
```

## <a name="parameters"></a>매개 변수

`pwszFilename` \
진행 요청 되는 모듈의 이름입니다.

`dwTimestamp` \
진행 PE 파일의 COFF 파일 헤더에 저장 된 날짜 타임 스탬프입니다.

`pLibraryProvider` \
진행 PE 파일의 COFF 선택적 파일 헤더에 저장 된 필드입니다.`SizeOfImage`

`hModule` \
제한이 요청 된 모듈에 대 한 핸들입니다.

## <a name="return-value"></a>반환 값

이 메서드는 다음과 같은 특정 HRESULT뿐만 아니라 메서드 오류를 나타내는 HRESULT 오류도 반환합니다.

|HRESULT|Description|
|-------------|-----------------|
|S_OK|메서드가 완료되었습니다.|

## <a name="exceptions"></a>예외

## <a name="remarks"></a>설명

`ProvideLibrary`디버거가 mscordbi.dll 및 mscordacwks와 같은 특정 CLR 파일을 디버깅 하는 데 필요한 모듈을 제공할 수 있도록 합니다. [ICLRDebugging:: CanUnloadNow](../../../../docs/framework/unmanaged-api/debugging/iclrdebugging-canunloadnow-method.md) 메서드를 호출할 때까지 모듈 핸들은 유효한 상태로 유지 되어야 합니다 .이 경우에는 호출자가 핸들을 해제할 책임이 있습니다.

디버거는 사용 가능한 모든 방법을 사용 하 여 디버깅 모듈을 찾거나 사용할 수 있습니다.

> [!IMPORTANT]
> 이 기능을 통해 API 호출자는 실행 파일 및 악성 코드가 포함 된 모듈을 제공할 수 있습니다. 보안 예방 조치로 서 호출자는를 사용 `ProvideLibrary` 하 여 자체적으로 실행 하지 않을 코드를 배포 하면 안 됩니다.
>
> Mscordbi.dll 또는 mscordacwks와 같은 이미 릴리스된 라이브러리에서 심각한 보안 문제가 발견 되 면 shim을 패치 하 여 잘못 된 버전의 파일을 인식할 수 있습니다. 그러면 shim은 패치 된 버전의 파일에 대 한 요청을 발급 하 고 요청에 대 한 응답으로 제공 된 경우 잘못 된 버전을 거부할 수 있습니다. 이는 사용자가 새 버전의 shim에 패치를 적용 한 경우에만 발생할 수 있습니다. 패치가 적용 되지 않은 버전은 취약 하 게 유지 됩니다.

## <a name="requirements"></a>요구 사항

**플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.

**헤더:** CorDebug.idl, CorDebug.h

**라이브러리** CorGuids.lib

**.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]

## <a name="see-also"></a>참고자료

- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
- [디버깅](../../../../docs/framework/unmanaged-api/debugging/index.md)
