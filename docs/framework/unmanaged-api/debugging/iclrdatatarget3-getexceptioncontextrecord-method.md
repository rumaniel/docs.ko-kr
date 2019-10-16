---
title: ICLRDataTarget3::GetExceptionContextRecord 메서드
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- ICLRDataTarget3.GetContextRecord
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: 66076ed5-f05c-4114-9788-94cb143abb8a
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 07065b15f449c2bcb84df7bbdcce65d61de007ee
ms.sourcegitcommit: cf9515122fce716bcfb6618ba366e39b5a2eb81e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69038341"
---
# <a name="iclrdatatarget3getexceptioncontextrecord-method"></a>ICLRDataTarget3::GetExceptionContextRecord 메서드
CLR(공용 언어 런타임) 데이터 액세스 서비스에 의해 호출되어 대상 프로세스와 연결된 컨텍스트 레코드를 검색합니다. 예를 들어 덤프 대상의 경우,이는 `ExceptionParam` 인수를 통해 Windows 디버그 도움말 라이브러리 (dbghelp.dll)의 [MiniDumpWriteDump](/windows/desktop/api/minidumpapiset/nf-minidumpapiset-minidumpwritedump) 함수에 전달 된 컨텍스트 레코드와 동일 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetExceptionContextRecord(  
    [in] ULONG32 bufferSize,  
    [out] ULONG32* bufferUsed,  
    [out, size_is(bufferSize)] BYTE* buffer  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `bufferSize`  
 [in] 입력 버퍼 크기(바이트)로, 컨텍스트 레코드를 포함할 수 있을 정도로 커야 합니다.  
  
 `bufferUsed`  
 [out] 실제로 버퍼에 기록되는 바이트 수를 받는 `ULONG32` 형식에 대한 포인터입니다.  
  
 `buffer`  
 [out] 컨텍스트 레코드 복사본을 받는 메모리 버퍼에 대한 포인터입니다. 예외 레코드는 [컨텍스트](/windows/win32/api/winnt/ns-winnt-arm64_nt_context) 형식으로 반환 됩니다.  
  
## <a name="return-value"></a>반환 값  
 반환 값은 성공 시 `S_OK`이고 실패 시에는 오류 `HRESULT` 코드입니다. `HRESULT` 코드는 다음을 비롯한 여러 항목을 포함할 수 있습니다.  
  
|반환 코드|Description|  
|-----------------|-----------------|  
|`S_OK`|메서드가 정상적으로 실행되었습니다. 컨텍스트 레코드가 출력 버퍼에 복사되었습니다.|  
|`HRESULT_FROM_WIN32(ERROR_NOT_FOUND)`|컨텍스트 레코드가 대상에 연결되지 않았습니다.|  
|`HRESULT_FROM_WIN32(ERROR_BAD_LENGTH)`|입력 버퍼 크기가 컨텍스트 레코드를 수용할 수 있을 정도로 크지 않습니다.|  
  
## <a name="remarks"></a>설명  
 [컨텍스트](/windows/win32/api/winnt/ns-winnt-arm64_nt_context) 는 Windows SDK에서 제공 하는 헤더에 정의 된 플랫폼별 구조입니다.  
  
 이 메서드는 디버깅 애플리케이션의 작성자가 구현합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** ClrData .idl, ClrData .h  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[v451_update](../../../../includes/net-current-v451-nov-plus.md)]  
  
## <a name="see-also"></a>참고자료

- [ICLRDataTarget3 인터페이스](../../../../docs/framework/unmanaged-api/debugging/iclrdatatarget3-interface.md)
- [GetExceptionRecord 메서드](../../../../docs/framework/unmanaged-api/debugging/iclrdatatarget3-getexceptionrecord-method.md)
- [GetExceptionThreadID 메서드](../../../../docs/framework/unmanaged-api/debugging/iclrdatatarget3-getexceptionthreadid-method.md)
