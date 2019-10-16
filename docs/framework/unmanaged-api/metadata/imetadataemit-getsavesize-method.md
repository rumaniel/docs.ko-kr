---
title: IMetaDataEmit::GetSaveSize 메서드
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.GetSaveSize
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::GetSaveSize
helpviewer_keywords:
- IMetaDataEmit::GetSaveSize method [.NET Framework metadata]
- GetSaveSize method [.NET Framework metadata]
ms.assetid: 8aea2e2c-23a3-4cda-9a06-e19f97383830
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 7337222f7f419c68ae21d604d1673158acca85ba
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67777397"
---
# <a name="imetadataemitgetsavesize-method"></a>IMetaDataEmit::GetSaveSize 메서드
현재 범위에서 어셈블리 및 해당 메타 데이터의 이진 예상된 크기를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetSaveSize (  
    [in]  CorSaveSize fSave,  
    [out] DWORD       *pdwSaveSize  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `fSave`  
 [in] 값을 [CorSaveSize](../../../../docs/framework/unmanaged-api/metadata/corsavesize-enumeration.md) 정확 하거나 대략적인 크기를 가져올 것인지를 지정 하는 열거형입니다. 세 개의 값이 유효한: cssAccurate, cssQuick, 및 cssDiscardTransientCAs:  
  
- cssAccurate 정확한 저장 크기를 반환 하지만 계산 하는 데 시간이 오래 걸립니다.  
  
- cssQuick은 안전을 위해 패딩 크기를 반환 하지만 계산 시간이 줄어듭니다.  
  
- cssDiscardTransientCAs 지시 `GetSaveSize` 는 발생할 수 있습니다 제거 사용자 지정 특성을 무시할 수 있습니다.  
  
 `pdwSaveSize`  
 [out] 파일을 저장 하는 데 필요한 크기에 대 한 포인터입니다.  
  
## <a name="remarks"></a>설명  
 `GetSaveSize` 하는 데 필요한 바이트를 현재 범위에서 어셈블리 및 해당 모든 메타 데이터를 저장 공간을 계산 합니다. (에 대 한 호출을 [imetadataemit:: Savetostream](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-savetostream-method.md) 메서드는이 바이트 수를 내보냅니다.)  
  
 호출자가 구현 하는 경우는 [IMapToken](../../../../docs/framework/unmanaged-api/metadata/imaptoken-interface.md) 인터페이스 (통해 [imetadataemit:: Sethandler](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-sethandler-method.md) 하거나 [imetadataemit:: 병합](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-merge-method.md)), `GetSaveSize` 두 가지 단계로 수행 됩니다 최적화 하 고 압축 메타 데이터입니다. 그렇지 않으면 없습니다 최적화가 수행 됩니다.  
  
 최적화를 수행 하는 경우 첫 번째 패스는 단순히 가져올 때 검색의 성능을 조정 하기 위해 메타 데이터 구조를 정렬 합니다. 이 단계는 일반적으로 나중에 참조할 수에 대 한 도구에서 유지 하는 토큰이 유효 하지 않습니다는 부작용으로 레코드가 이동에 발생 합니다. 하지만 메타 데이터를 알리지 않습니다 토큰 변경 될 때까지 호출자에 게 두 번째 패스 후. 두 번째 단계에서는 다양 한 최적화가 수행 됩니다 (초기 바인딩)를 최적화 하는 등의 메타 데이터의 전체 크기를 줄이기 위한 `mdTypeRef` 고 `mdMemberRef` 참조 형식 또는 멤버에 선언 된 경우 토큰을 현재 메타 데이터 범위입니다. 이 단계에서는 또 다른 토큰 매핑이 발생합니다. 이 단계 후 메타 데이터 엔진에 알립니다. 호출자를 통해 해당 `IMapToken` 인터페이스의 토큰 값을 변경 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MSCorEE.dll에서 리소스로 사용  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v11plus](../../../../includes/net-current-v11plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IMetaDataEmit 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md)
- [IMetaDataEmit2 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-interface.md)
