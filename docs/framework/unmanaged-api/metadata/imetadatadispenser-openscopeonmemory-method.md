---
title: IMetaDataDispenser::OpenScopeOnMemory 메서드
ms.date: 03/30/2017
api_name:
- IMetaDataDispenser.OpenScopeOnMemory
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataDispenser::OpenScopeOnMemory
helpviewer_keywords:
- OpenScopeOnMemory method [.NET Framework metadata]
- IMetaDataDispenser::OpenScopeOnMemory method [.NET Framework metadata]
ms.assetid: 14218249-bdec-48ae-b5fc-9f57f7ca8501
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 204e5660e95434f8d0c44d54f4fdbb1c2acc1e5d
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67777780"
---
# <a name="imetadatadispenseropenscopeonmemory-method"></a>IMetaDataDispenser::OpenScopeOnMemory 메서드
기존 메타 데이터를 포함 하는 메모리 영역을 엽니다. 즉,이 메서드는 메타 데이터로 기존 데이터가 처리 되는 메모리의 지정된 된 영역을 엽니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT OpenScopeOnMemory (  
    [in]  LPCVOID     pData,   
    [in]  ULONG       cbData,   
    [in]  DWORD       dwOpenFlags,   
    [in]  REFIID      riid,   
    [out] IUnknown    **ppIUnk  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pData`  
 [in] 메모리 영역의 시작 주소를 지정 하는 포인터입니다.  
  
 `cbData`  
 [in] 바이트의 메모리 영역의 크기입니다.  
  
 `dwOpenFlags`  
 [in] 값을 [CorOpenFlags](../../../../docs/framework/unmanaged-api/metadata/coropenflags-enumeration.md) 열기 위한 모드 (읽기, 쓰기 및 등)를 지정 하는 열거형입니다.  
  
 `riid`  
 [in] 반환 될 원하는 메타 데이터 인터페이스의 IID 호출자에 게 가져오기 (읽기) 또는 (쓰기) 메타 데이터 내보내기 인터페이스를 사용 합니다.  
  
 변수의 `riid` "가져오기" 또는 "내보내기" 인터페이스 중 하나를 지정 해야 합니다. 유효한 값은 IID_IMetaDataEmit, IID_IMetaDataImport, IID_IMetaDataAssemblyEmit, IID_IMetaDataAssemblyImport, IID_IMetaDataEmit2, 또는 IID_IMetaDataImport2입니다.  
  
 `ppIUnk`  
 [out] 반환 되는 인터페이스에 대 한 포인터입니다.  
  
## <a name="remarks"></a>설명  
 "가져오기" 인터페이스 중 하나에서 메서드를 사용 하거나 "내보내기" 인터페이스 중 하나에서 메서드를 사용 하 여 추가할 메타 데이터의 메모리 내 복사본을 쿼리할 수 있습니다.  
  
 합니다 `OpenScopeOnMemory` 메서드는 비슷합니다는 [imetadatadispenser:: Openscope](../../../../docs/framework/unmanaged-api/metadata/imetadatadispenser-openscope-method.md) 메서드를 관심의 메타 데이터 메모리 대신 디스크의 파일에 이미 존재 한다는 점을 제외 합니다.  
  
 메모리의 대상 영역에 공용 언어 런타임 (CLR) 메타 데이터가 없는 경우는 `OpenScopeOnMemory` 메서드가 실패 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에서 리소스로 사용  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IMetaDataDispenser 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadatadispenser-interface.md)
- [IMetaDataDispenserEx 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadatadispenserex-interface.md)
- [IMetaDataAssemblyEmit 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataassemblyemit-interface.md)
- [IMetaDataAssemblyImport 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataassemblyimport-interface.md)
- [IMetaDataEmit 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md)
- [IMetaDataEmit2 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-interface.md)
- [IMetaDataImport 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
- [IMetaDataImport2 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
