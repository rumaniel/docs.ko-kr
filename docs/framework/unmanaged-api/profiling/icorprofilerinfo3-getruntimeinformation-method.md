---
title: ICorProfilerInfo3::GetRuntimeInformation 메서드
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo3.GetRuntimeInformation Method
api_location:
- Mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo3::GetRuntimeInformation
helpviewer_keywords:
- GetRuntimeInformation method [.NET Framework profiling]
- ICorProfilerInfo3::GetRuntimeInformation method [.NET Framework profiling]
ms.assetid: 4400fb8c-0407-4791-8557-f011fd2aee51
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 7087864d0305f0cdb0b4977f037cf5a7c4dee18d
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67783135"
---
# <a name="icorprofilerinfo3getruntimeinformation-method"></a>ICorProfilerInfo3::GetRuntimeInformation 메서드
CLR (공용 언어 런타임) 프로 파일링 되는 버전 정보를 제공 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetRuntimeInformation(  
       [out] USHORT *pClrInstanceId,  
       [out] COR_PRF_RUNTIME_TYPE *pRuntimeType,  
       [out] USHORT *pMajorVersion,  
       [out] USHORT *pMinorVersion,  
       [out] USHORT *pBuildNumber,  
       [out] USHORT *pQFEVersion,  
       [in]  ULONG  cchVersionString,  
       [out] ULONG  *pcchVersionString,  
       [out, size_is(cchVersionString), length_is(*pcchVersionString)]  
                   WCHAR  szVersionString[]);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pClrInstanceId`  
 [out] 프로세스에서 실행 중인 CLR 인스턴스의 담당자 ID입니다. 이 동일 합니다 `ClrInstanceID` Windows (ETW) 시작 이벤트에 대 한 이벤트 추적을 보고 하는 합니다.  
  
 `pRuntimeType`  
 [out] 런타임 형식입니다. 이 매개 변수 반환 `COR_PRF_DESKTOP_CLR` CLR의 데스크톱 버전 또는 `COR_PRF_CORE_CLR` Silverlight에서 사용 하는 CLR의 core 버전에 대 한 합니다.  
  
 `pMajorVersion`  
 [out] Clr 주 버전 번호입니다.  
  
 `pMinorVersion`  
 [out] CLR의 부 버전 번호입니다.  
  
 `pBuildVersion`  
 [out] Clr 빌드 버전 번호입니다.  
  
 `pQFEVersion`  
 [out] 소프트웨어 업데이트와 연결 된 CLR의 버전 번호입니다.  
  
 `cchVersionString`  
 [in] 문자 버퍼의 길이 `szVersionString` 가리킵니다.  
  
 `pcchVersionString`  
 [out] 문자에서 길이의 `szVersionString`합니다.  
  
 `szVersionString`  
 [out] CLR 버전 문자열입니다.  
  
## <a name="remarks"></a>설명  
 매개 변수에 대해 null을 전달할 수 있습니다. 그러나 `pcchVersionString` null 일 수 없습니다 경우가 아니면 `szVersionString` null 이기도 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorProf.idl, CorProf.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICorProfilerInfo3 인터페이스](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-interface.md)
- [프로파일링 인터페이스](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [프로파일링](../../../../docs/framework/unmanaged-api/profiling/index.md)
