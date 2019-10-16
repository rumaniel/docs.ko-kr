---
title: ICorDebugNativeFrame::GetLocalDoubleRegisterValue 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugNativeFrame.GetLocalDoubleRegisterValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugNativeFrame::GetLocalDoubleRegisterValue
helpviewer_keywords:
- ICorDebugNativeFrame::GetLocalDoubleRegisterValue method [.NET Framework debugging]
- GetLocalDoubleRegisterValue method [.NET Framework debugging]
ms.assetid: 1f838215-ac8a-434f-8ce6-03021d3098d9
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ed7436ff73fa9cc19790859581930875f39e499e
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67746290"
---
# <a name="icordebugnativeframegetlocaldoubleregistervalue-method"></a>ICorDebugNativeFrame::GetLocalDoubleRegisterValue 메서드
네이티브 프레임에 대 한 지정 된 두 레지스터에 저장 된 로컬 변수 또는 인수 값을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetLocalDoubleRegisterValue (  
    [in] CorDebugRegister   highWordReg,  
    [in] CorDebugRegister   lowWordReg,  
    [in] ULONG              cbSigBlob,  
    [in] PCCOR_SIGNATURE    pvSigBlob,  
    [out] ICorDebugValue    **ppValue  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `highWordReg`  
 [in] 값의 상위 단어를 포함 하는 레지스터를 지정 하는 "CorDebugRegister" 열거형의 값입니다.  
  
 `lowWordReg`  
 [in] 값은 `CorDebugRegister` 값의 낮은 단어를 포함 하는 레지스터를 지정 하는 열거형입니다.  
  
 `cbSigBlob`  
 [in] 참조 하는 이진 메타 데이터 서명의 크기를 지정 하는 정수를 `pvSigBlob` 매개 변수입니다.  
  
 `pvSigBlob`  
 [in] `PCCOR_SIGNATURE` 이진 메타 데이터 서명의 값의 형식 가리키는 값입니다.  
  
 `ppValue`  
 [out] 지정 된 레지스터에 저장 된 검색된 된 값을 나타내는 "ICorDebugValue" 개체의 주소에 대 한 포인터입니다.  
  
## <a name="remarks"></a>설명  
 `GetLocalDoubleRegisterValue` 네이티브 프레임이 또는-just-in-time (JIT) 메서드를 사용할 수 있습니다-프레임 컴파일됩니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료
