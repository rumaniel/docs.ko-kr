---
title: ICorProfilerInfo::GetAppDomainInfo 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.GetAppDomainInfo
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::GetAppDomainInfo
helpviewer_keywords:
- ICorProfilerInfo::GetAppDomainInfo method [.NET Framework profiling]
- GetAppDomainInfo method [.NET Framework profiling]
ms.assetid: a6bf5a04-e03e-44f0-917a-96f6a6d3cc96
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 70ab6a94d19f1411e1f79a9f3912158ec02059ed
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67780227"
---
# <a name="icorprofilerinfogetappdomaininfo-method"></a>ICorProfilerInfo::GetAppDomainInfo 메서드
애플리케이션 도메인 ID를 수락합니다. 애플리케이션 도메인 이름 및 해당 이름을 포함하는 프로세스 ID를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetAppDomainInfo(  
    [in]  AppDomainID appDomainId,  
    [in]  ULONG       cchName,  
    [out] ULONG       *pcchName,  
    [out, size_is(cchName), length_is(*pcchName)]  
          WCHAR       szName[] ,  
    [out] ProcessID   *pProcessId);  
```  
  
## <a name="parameters"></a>매개 변수  
 `appDomainId`  
 [in] 애플리케이션 도메인의 ID입니다.  
  
 `cchName`  
 [in] `szName` 반환 버퍼의 길이(문자)입니다.  
  
 `pcchName`  
 [out] 애플리케이션 도메인 이름의 총 문자 길이에 대한 포인터입니다.  
  
 `szName`  
 [out] 호출자가 제공한 와이드 문자 버퍼입니다. 메서드가 반환되면 `szName`에 전체 또는 일부 애플리케이션 도메인 이름이 포함됩니다.  
  
 `pProcessId`  
 [out] 애플리케이션 도메인을 포함하는 프로세스 ID에 대한 포인터입니다.  
  
## <a name="remarks"></a>설명  
 이 메서드가 반환된 후 `szName` 버퍼가 모듈의 애플리케이션 도메인의 전체 이름을 포함하기에 충분히 큰지 확인해야 합니다. 이렇게 하려면 `pcchName`가 가리키는 값을 `cchName` 매개 변수의 값과 비교합니다. `pcchName`이 `cchName`보다 큰 값을 가리키는 경우 더 큰 `szName` 버퍼를 할당하고 `cchName`을 더 큰 새 크기로 업데이트한 후 `GetAppDomainInfo`를 다시 호출합니다.  
  
 또는 길이가 0인 `szName` 버퍼로 `GetAppDomainInfo`를 먼저 호출하여 올바른 버퍼 크기를 구합니다. 그런 다음 버퍼 크기를 `pcchName`에 반환된 값으로 설정하고 `GetAppDomainInfo`을 다시 호출합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerInfo 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)
- [프로파일링 인터페이스](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [프로파일링](../../../../docs/framework/unmanaged-api/profiling/index.md)
