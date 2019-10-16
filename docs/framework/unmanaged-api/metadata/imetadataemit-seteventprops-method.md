---
title: IMetaDataEmit::SetEventProps 메서드
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.SetEventProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::SetEventProps
helpviewer_keywords:
- IMetaDataEmit::SetEventProps method [.NET Framework metadata]
- SetEventProps method [.NET Framework metadata]
ms.assetid: 3b039e50-63ec-4730-99ff-2327408de477
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 271ecd7e757340becccb7bf52362487a2b277299
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67737187"
---
# <a name="imetadataemitseteventprops-method"></a>IMetaDataEmit::SetEventProps 메서드
설정 하거나 지정된 된 기능에 대 한 이전 호출에서 정의 된 이벤트의 업데이트 [imetadataemit:: Defineevent](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-defineevent-method.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT SetEventProps (  
    [in]  mdEvent     ev,   
    [in]  DWORD       dwEventFlags,   
    [in]  mdToken     tkEventType,   
    [in]  mdMethodDef mdAddOn,   
    [in]  mdMethodDef mdRemoveOn,   
    [in]  mdMethodDef mdFire,   
    [in]  mdMethodDef rmdOtherMethods[]   
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `ev`  
 [in] 이벤트 토큰입니다.  
  
 `dwEventFlags`  
 [in] 이벤트 플래그입니다. 이 비트 마스크의 `CorEventAttr` 값입니다.  
  
 `tkEventType`  
 [in] 이벤트 클래스에 대 한 토큰입니다. 이 값은 `mdTypeDef` 또는 `mdTypeRef` 토큰입니다.  
  
 `mdAddOn`  
 [in] 이벤트 또는 null을 구독 하는 데 사용 된 메서드.  
  
 `mdRemoveOn`  
 [in] 이벤트 또는 null로 구독을 취소 하는 데 사용 된 메서드.  
  
 `mdFire`  
 [in] 이벤트를 발생 시킬 (파생된 클래스)에 의해 사용 되는 방법  
  
 `rmdOtherMethods[]`  
 [in] 이벤트에 연결 된 다른 방법에 대 한 토큰의 배열입니다. 배열의 마지막 요소 여야 합니다 `mdMethodDefNil`합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MSCorEE.dll에서 리소스로 사용  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IMetaDataEmit 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md)
- [IMetaDataEmit2 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-interface.md)
