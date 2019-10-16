---
title: IMetaDataEmit::SetClassLayout 메서드
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.SetClassLayout
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::SetClassLayout
helpviewer_keywords:
- IMetaDataEmit::SetClassLayout method [.NET Framework metadata]
- SetClassLayout method [.NET Framework metadata]
ms.assetid: 2576c449-388d-4434-a0e1-9f53991e11b6
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: c455b5196ceafef924de59e9134b89ed62455520
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67737221"
---
# <a name="imetadataemitsetclasslayout-method"></a>IMetaDataEmit::SetClassLayout 메서드
에 대 한 이전 호출에서 정의 된 클래스에 대 한 필드 레이아웃을 완료 [DefineTypeDef 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-definetypedef-method.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT SetClassLayout (  
    [in]  mdTypeDef           td,   
    [in]  DWORD               dwPackSize,   
    [in]  COR_FIELD_OFFSET    rFieldOffsets[],   
    [in]  ULONG               ulClassSize   
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `td`  
 [in] `mdTypeDef` 배치 클래스를 지정 하는 토큰입니다.  
  
 `dwPackSize`  
 [in] 압축 크기: 1, 2, 4, 8 또는 16 바이트입니다. 압축 크기가 인접 한 필드 사이의 바이트 수입니다.  
  
 `rFieldOffsets`  
 [in] 배열을 [COR_FIELD_OFFSET](../../../../docs/framework/unmanaged-api/metadata/cor-field-offset-structure.md) 구조를 각각 클래스 내에서 클래스의 필드와 필드 오프셋을 지정 합니다. 배열 종료 `mdTokenNil`합니다.  
  
 `ulClassSize`  
 [in] 클래스의 바이트 크기입니다.  
  
## <a name="remarks"></a>설명  
 클래스가 호출 하 여 처음에 정의 되는 [imetadataemit:: Definetypedef](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-definetypedef-method.md) 메서드 및 클래스의 필드에 대 한 세 가지 레이아웃 중 하나를 지정: 자동, 순차적으로 또는 명시적입니다. 일반적으로 자동 레이아웃을 사용 하는 공용 언어 런타임이 가장 좋은 방법은 필드 레이아웃을 선택 합니다.  
  
 그러나 코드는 관리 되지 않는 정렬에 따라 배치 필드 경우가 있습니다. 이 경우 sequential 또는 explicit 레이아웃 및 호출을 선택 `SetClassLayout` 필드의 레이아웃을 완료 하려면:  
  
- 순차적 레이아웃: 압축 크기를 지정 합니다. 필드는 자연 스러운 크기 또는 어떤 결과 필드의 작은 오프셋의 압축 크기에 따라 정렬 됩니다. 설정할 `rFieldOffsets` 고 `ulClassSize` 0입니다.  
  
- 명시적 레이아웃: 각 필드의 오프셋을 지정 하거나 클래스와 압축 크기를 지정 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MSCorEE.dll에서 리소스로 사용  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IMetaDataEmit 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md)
- [IMetaDataEmit2 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-interface.md)
