---
title: LPOVERLAPPED_COMPLETION_ROUTINE 함수 포인터
ms.date: 03/30/2017
api_name:
- LPOVERLAPPED_COMPLETION_ROUTINE
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- LPOVERLAPPED_COMPLETION_ROUTINE
helpviewer_keywords:
- LPOVERLAPPED_COMPLETION_ROUTINE function pointer [.NET Framework hosting]
ms.assetid: 5fb645d9-b818-401c-8c2c-c30d86de58ba
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: dcf63000de549b42d92ba157a7e550ac605bbfcd
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67768383"
---
# <a name="lpoverlappedcompletionroutine-function-pointer"></a>LPOVERLAPPED_COMPLETION_ROUTINE 함수 포인터
Overlapped는 호스트에 알리는 함수를 가리키는 (즉, 비동기) 장치에는 I/O 완료 합니다.  
  
 .NET Framework 4에서이 함수 포인터에 사용 되지 않습니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef VOID (*LPOVERLAPPED_COMPLETION_ROUTINE) (  
    [in] DWORD  dwErrorCode,  
    [in] DWORD  dwNumberOfBytesTransfered,  
    [in] LPVOID lpOverlapped  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `dwErrorCode`  
 [in] 장치; 닫힌 경우 오류 코드 값 그렇지 않은 경우이 값은 0입니다.  
  
 장치를 닫으면 모든 보류 중인 장치에는 I/O 즉시 완료 됩니다.  
  
 `dwNumberOfBytesTransfered`  
 [in] I/O 작업에 의해 전송 된 바이트 수입니다.  
  
 `lpOverlapped`  
 [in] I/O 요청을 완료 하는 데 사용할 정보가 포함 된 구조에 대 한 포인터입니다.  
  
## <a name="remarks"></a>설명  
 함수는 `LPOVERLAPPED_COMPLETION_ROUTINE` 지점은 콜백 함수 및 호스팅 응용 프로그램의 작성기에 의해 구현 되어야 합니다. 콜백 함수에는 완료 된 I/O 요청을 처리 하는 데 호스트 수 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorWks.dll  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [사용되지 않는 CLR 호스팅 함수](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-functions.md)
