---
title: ISymUnmanagedWriter::GetDebugInfo 메서드
ms.date: 03/30/2017
api_name:
- ISymUnmanagedWriter.GetDebugInfo
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- ISymUnmanagedWriter::GetDebugInfo
helpviewer_keywords:
- ISymUnmanagedWriter::GetDebugInfo method [.NET Framework debugging]
- GetDebugInfo method [.NET Framework debugging]
ms.assetid: dd31c210-6829-45eb-927e-cc53932638b7
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 8737885015055994bff3f6066bccb551f19f74f4
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67777314"
---
# <a name="isymunmanagedwritergetdebuginfo-method"></a>ISymUnmanagedWriter::GetDebugInfo 메서드
컴파일러가 이식 가능한 실행 파일 (PE) 파일 헤더의 디버그 디렉터리 항목을 작성 하는 데 필요한 정보를 반환 합니다. 기호 작성기를 제외한 모든 필드를 채워 `TimeDateStamp` 고 `PointerToRawData`입니다. (컴파일러는 이러한 두 필드를 적절 하 게 설정 하는 일을 담당 합니다.)  
  
 컴파일러는이 메서드를 호출, PE 파일에 데이터 blob을 내보낼, 설정 된 `PointerToRawData` 내보낸 데이터를 가리키고는 IMAGE_DEBUG_DIRECTORY PE 파일에 쓸 IMAGE_DEBUG_DIRECTORY 필드입니다. 컴파일러 설정 해야 합니다 `TimeDateStamp` 과 동일 하 게 필드는 `TimeDateStamp` 생성 되는 PE 파일의 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetDebugInfo(  
    [in, out] IMAGE_DEBUG_DIRECTORY *pIDD,  
    [in]  DWORD cData,  
    [out] DWORD *pcData,  
    [out, size_is(cData),  
        length_is(*pcData)] BYTE data[]);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pIDD`  
 [out에서] 기호 작성기가 데이터를 입력 하는 IMAGE_DEBUG_DIRECTORY 포인터입니다.  
  
 `cData`  
 [in] `DWORD` 디버그 데이터의 크기를 포함 하는 합니다.  
  
 `pcData`  
 [out] 에 대 한 포인터를 `DWORD` 디버그 데이터를 포함 하는 데 필요한 버퍼의 크기를 받는 합니다.  
  
 `data`  
 [out] 기호 저장소에 대 한 디버그 데이터를 저장할 수 있도록 충분히 큰 버퍼에 대 한 포인터입니다.  
  
## <a name="return-value"></a>반환 값  
 메서드가 성공 하면 s_ok이 고 그렇지 않으면 E_FAIL 또는 일부 다른 오류 코드입니다.  
  
## <a name="requirements"></a>요구 사항  
 **헤더:** CorSym.idl, CorSym.h  
  
## <a name="see-also"></a>참고자료

- [ISymUnmanagedWriter 인터페이스](../../../../docs/framework/unmanaged-api/diagnostics/isymunmanagedwriter-interface.md)
