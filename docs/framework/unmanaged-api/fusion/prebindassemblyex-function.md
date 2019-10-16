---
title: PreBindAssemblyEx 함수
ms.date: 03/30/2017
api_name:
- PreBindAssemblyEx
api_location:
- fusion.dll
api_type:
- DLLExport
f1_keywords:
- PreBindAssemblyEx
helpviewer_keywords:
- PreBindAssemblyEx function [.NET Framework fusion]
ms.assetid: bd285233-a4a2-4b52-bbca-0025a60e4864
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 8aa2d174200db76f5c7a6db43e14bb6904604226
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70796334"
---
# <a name="prebindassemblyex-function"></a>PreBindAssemblyEx 함수
어셈블리의 정책 후 표시 이름을 가져옵니다.  
  
 이 함수는 .NET Framework 인프라를 지원 하며 사용자 코드에서 직접 사용 하기 위한 것이 아닙니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT PreBindAssemblyEx (  
    [in]  IApplicationContext *pAppCtx,  
    [in]  IAssemblyName       *pName,  
    [in]  IAssembly           *pAsmParent,  
    [in]  LPCWSTR             pwzRuntimeVersion,  
    [out] IAssemblyName       **ppNamePostPolicy,  
    [in]  LPVOID              pvReserved  
 );  
```  
  
## <a name="parameters"></a>매개 변수  
 `pAppCtx`  
 진행 응용 프로그램 컨텍스트를 식별 합니다.  
  
 `pName`  
 진행 어셈블리 이름을 식별 합니다.  
  
 `pAsmParent`  
 진행 부모 어셈블리를 식별 합니다. 이 매개 변수는 무시됩니다.  
  
 `pwzRuntimeVersion`  
 진행 런타임 버전을 식별 합니다.  
  
 `ppNamePostPolicy`  
 제한이 사후 정책 표시 이름을 포함 합니다.  
  
 `pvReserved`  
 진행 향후 확장성을 위해 예약 되었습니다. `pvReserved`는 null 참조 여야 합니다.  
  
## <a name="remarks"></a>설명  
 `ppNamePostPolicy` 출력 매개 변수는 함수가 HRESULT FUSION_E_REF_DEF_MISMATCH을 반환 하는 경우에만 설정 됩니다. 그렇지 않으면 null입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Fusion. h  
  
 **라이브러리** Mscoree.dll에 리소스로 포함 됩니다.  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [Fusion 전역 정적 함수](fusion-global-static-functions.md)
