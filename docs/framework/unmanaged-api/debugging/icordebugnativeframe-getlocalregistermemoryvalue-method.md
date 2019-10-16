---
title: ICorDebugNativeFrame::GetLocalRegisterMemoryValue 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugNativeFrame.GetLocalRegisterMemoryValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugNativeFrame::GetLocalRegisterMemoryValue
helpviewer_keywords:
- ICorDebugNativeFrame::GetLocalRegisterMemoryValue method [.NET Framework debugging]
- GetLocalRegisterMemoryValue method [.NET Framework debugging]
ms.assetid: d350f69d-9aff-4f5a-8301-daea22dee2da
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: cc179236f5453724639d47558770179a1e80f706
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67746199"
---
# <a name="icordebugnativeframegetlocalregistermemoryvalue-method"></a>ICorDebugNativeFrame::GetLocalRegisterMemoryValue 메서드
하위 워드 및 높은 word 메모리 위치에 저장 됩니다 및 네이티브 프레임에 대 한 레지스터를 각각 지정 된 지역 변수 또는 인수의 값을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetLocalRegisterMemoryValue (  
    [in] CorDebugRegister   highWordReg,  
    [in] CORDB_ADDRESS      lowWordAddress,  
    [in] ULONG              cbSigBlob,  
    [in] PCCOR_SIGNATURE    pvSigBlob,  
    [out] ICorDebugValue    **ppValue  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `highWordReg`  
 [in] 값의 상위 단어를 포함 하는 레지스터를 지정 하는 "CorDebugRegister" 열거형의 값입니다.  
  
 `lowWordAddress`  
 [in] `CORDB_ADDRESS` 값의 낮은 단어를 포함 하는 메모리 위치를 지정 하는 값입니다.  
  
 `cbSigBlob`  
 [in] 참조 하는 이진 메타 데이터 서명의 크기를 지정 하는 정수를 `pvSigBlob` 매개 변수입니다.  
  
 `pvSigBlob`  
 [in] `PCCOR_SIGNATURE` 이진 메타 데이터 서명의 값의 형식 가리키는 값입니다.  
  
 `ppValue`  
 [out] 지정된 된 등록 및 메모리 위치에 저장 된 검색된 된 값을 나타내는 "ICorDebugValue" 개체의 주소에 대 한 포인터입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료
