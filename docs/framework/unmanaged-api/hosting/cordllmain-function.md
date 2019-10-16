---
title: _CorDllMain 함수
ms.date: 03/30/2017
api_name:
- _CorDllMain
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- _CorDllMain
helpviewer_keywords:
- _CorDllMain function [.NET Framework hosting]
ms.assetid: bc7b51cf-39d3-48ec-a5cb-2f179fbefff8
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9a02a899fd6fbffd04ef25913adb6a65ade27177
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67755653"
---
# <a name="cordllmain-function"></a>\_CorDllMain 함수

CLR (공용 언어 런타임)을 초기화 하 고 DLL 어셈블리의 CLR 헤더에서 관리 되는 진입점을 찾습니다 실행을 시작 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
BOOL STDMETHODCALLTYPE _CorDllMain (  
   [in] HINSTANCE hInst,  
   [in] DWORD     dwReason,  
   [in] LPVOID    lpReserved  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `hInst`  
 [in] 로드 된 모듈의 인스턴스 핸들입니다.  
  
 `dwReason`  
 [in] DLL 진입점 함수가 호출 되는 이유를 나타냅니다. 이 매개 변수는 다음 값 중 하나일 수 있습니다. DLL\_PROCESS_ATTACH, DLL\_스레드\_연결, DLL\_스레드\_ATTACH 또는 DLL\_프로세스\_분리 합니다. 이러한 값의 설명을 보려면는 `DllMain` Platform SDK에 대 한 설명서입니다.  
  
 `lpReserved`  
 [in] 사용 되지 않습니다.  
  
## <a name="return-value"></a>반환 값  
 이 메서드는 반환 `true` 성공을 위한 및 `false` 오류가 발생 합니다.  
  
## <a name="remarks"></a>설명  
 이 함수는 DLL 어셈블리에 대 한 운영 체제 로더에 의해 호출 됩니다. 실행 가능 어셈블리 로더 호출을 [ \_CorExeMain](../../../../docs/framework/unmanaged-api/hosting/corexemain-function.md) 함수를 대신 합니다.  
  
 운영 체제 로더는 DLL 파일에 지정 된 진입점에 관계 없이이 메서드를 호출 합니다.  
  
`_CorDllMain` 함수는 운영 체제 로더에 의해 직접 호출 됩니다.
  
 자세한 내용은 주의 섹션을 참조 합니다 [ \_CorValidateImage](../../../../docs/framework/unmanaged-api/hosting/corvalidateimage-function.md) 항목입니다.  
  
## <a name="requirements"></a>요구 사항  

 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [메타데이터 전역 정적 함수](../../../../docs/framework/unmanaged-api/metadata/metadata-global-static-functions.md)
