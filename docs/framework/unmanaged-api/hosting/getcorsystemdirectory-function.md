---
title: GetCORSystemDirectory 함수
ms.date: 03/30/2017
api_name:
- GetCORSystemDirectory
api_location:
- mscoree.dll
- mscoreei.dll
api_type:
- DLLExport
f1_keywords:
- GetCORSystemDirectory
helpviewer_keywords:
- GetCORSystemDirectory function [.NET Framework hosting]
ms.assetid: 3dcd16a7-dafc-4ca8-b5cd-20ffb37db91d
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d30384ea8b9ff4eee41abd43ae39486f770039e7
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70041432"
---
# <a name="getcorsystemdirectory-function"></a>GetCORSystemDirectory 함수
프로세스에 로드 된 CLR (공용 언어 런타임)의 설치 디렉터리를 반환 합니다. 설치 디렉터리는 정규화 된 것입니다 (예: "c:\windows\microsoft.net\framework\v1.0.3705").  
  
 이 함수는 사용 되지 않습니다. .NET Framework 4에서 제공 하는 [ICLRRuntimeInfo:: GetRuntimeDirectory](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-getruntimedirectory-method.md) 메서드로 대체 됩니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetCORSystemDirectory (   
    [out] LPWSTR  pbuffer,     
    [in]  DWORD   cchBuffer,   
    [out] DWORD*  dwlength  
);   
```  
  
## <a name="parameters"></a>매개 변수  
 `pbuffer`  
 제한이 런타임이 프로세스에 로드 되는 런타임에 대 한 설치 디렉터리의 정규화 된 이름을 포함 하는 문자열을 반환 하는 버퍼입니다. 런타임이 아직 프로세스에 로드 되지 않은 경우이 함수는 컴퓨터에 설치 된 런타임의 최신 버전에 대 한 적절 한 디렉터리 정보를 반환 합니다.  
  
 `cchBuffer`  
 진행 의 `pbuffer`크기 (바이트)입니다.  
  
 `dwLength`  
 제한이 에서 `pbuffer`반환 되는 문자 수입니다.  
  
## <a name="remarks"></a>설명  
  
> [!CAUTION]
> CLR 버전 4를 실행 하는 프로세스에서는이 함수를 사용 하지 마십시오. 이전 버전의 CLR이 컴퓨터에 설치 되어 있는 경우이 함수는 해당 버전의 설치 디렉터리를 반환 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리** MSCorEE.dll  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [사용되지 않는 CLR 호스팅 함수](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-functions.md)
