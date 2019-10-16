---
title: GetHashFromAssemblyFile 함수
ms.date: 03/30/2017
api_name:
- GetHashFromAssemblyFile
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- GetHashFromAssemblyFile
helpviewer_keywords:
- GetHashFromAssemblyFile function [.NET Framework strong naming]
ms.assetid: 751ed69f-b7ab-4e07-80de-e17ca9319b0c
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9f984d44d0a8acb85562a58653dfd2882053a0ce
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70799277"
---
# <a name="gethashfromassemblyfile-function"></a>GetHashFromAssemblyFile 함수
지정된 해시 알고리즘을 사용하여 지정된 어셈블리 파일의 해시를 가져옵니다.  
  
 이 함수는 더 이상 사용 되지 않습니다. 대신 [ICLRStrongName:: GetHashFromAssemblyFile](../hosting/iclrstrongname-gethashfromassemblyfile-method.md) 메서드를 사용 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetHashFromAssemblyFile (  
    [in]  LPCSTR   szFilePath,  
    [in, out] unsigned int   *piHashAlg,  
    [out] BYTE     *pbHash,  
    [in]  DWORD    cchHash,  
    [out] DWORD    *pchHash  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `szFilePath`  
 진행 해시할 파일의 경로입니다.  
  
 `piHashAlg`  
 [in, out] 해시 알고리즘을 지정 하는 상수입니다. 기본 해시 알고리즘에 대해 0을 사용 합니다.  
  
 `pbHash`  
 제한이 반환 된 해시 버퍼입니다.  
  
 `cchHash`  
 진행 요청 된 최대 크기 `pbHash`입니다.  
  
 `pchHash`  
 제한이 반환 된 크기 (바이트) `pbHash`입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** StrongName.h  
  
 **라이브러리** Mscoree.dll에 리소스로 포함 됩니다.  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [GetHashFromAssemblyFile 메서드](../hosting/iclrstrongname-gethashfromassemblyfile-method.md)
- [GetHashFromAssemblyFileW 메서드](../hosting/iclrstrongname-gethashfromassemblyfilew-method.md)
- [ICLRStrongName 인터페이스](../hosting/iclrstrongname-interface.md)
