---
title: IMetaDataDispenser::OpenScope 메서드
ms.date: 03/30/2017
api_name:
- IMetaDataDispenser.OpenScope
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataDispenser::OpenScope
helpviewer_keywords:
- IMetaDataDispenser::OpenScope method [.NET Framework metadata]
- OpenScope method, IMetaDataDispenser interface [.NET Framework metadata]
ms.assetid: 65063ad5-e0d9-4c01-8f8b-9a5950109fa6
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 6e157c758b472ea89e21c1ed1ba8c17693c20a3d
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67777801"
---
# <a name="imetadatadispenseropenscope-method"></a>IMetaDataDispenser::OpenScope 메서드
기존의 디스크에 파일을 열고 해당 메타 데이터를 메모리에 매핑합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT OpenScope (  
    [in]  LPCWSTR     szScope,   
    [in]  DWORD       dwOpenFlags,   
    [in]  REFIID      riid,   
    [out] IUnknown    **ppIUnk  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `szScope`  
 [in] 열려는 파일의 이름입니다. 파일에는 공용 언어 런타임 (CLR) 메타 데이터가 있어야 합니다.  
  
 `dwOpenFlags`  
 [in] 값을 [CorOpenFlags](../../../../docs/framework/unmanaged-api/metadata/coropenflags-enumeration.md) 열기 위한 모드 (읽기, 쓰기 및 등)를 지정 하는 열거형입니다.  
  
 `riid`  
 [in] 반환 될 원하는 메타 데이터 인터페이스의 IID 호출자에 게 가져오기 (읽기) 또는 (쓰기) 메타 데이터 내보내기 인터페이스를 사용 합니다.  
  
 변수의 `riid` "가져오기" 또는 "내보내기" 인터페이스 중 하나를 지정 해야 합니다. 유효한 값은 IID_IMetaDataEmit, IID_IMetaDataImport, IID_IMetaDataAssemblyEmit, IID_IMetaDataAssemblyImport, IID_IMetaDataEmit2, 또는 IID_IMetaDataImport2입니다.  
  
 `ppIUnk`  
 [out] 반환 되는 인터페이스에 대 한 포인터입니다.  
  
## <a name="remarks"></a>설명  
 "가져오기" 인터페이스 중 하나에서 메서드를 사용 하거나 "내보내기" 인터페이스 중 하나에서 메서드를 사용 하 여 추가할 메타 데이터의 메모리 내 복사본을 쿼리할 수 있습니다.  
  
 CLR 메타 데이터를 대상 파일에 없으면는 `OpenScope` 메서드가 실패 합니다.  
  
 .NET Framework 버전 1.0 및 1.1 경우 범위는으로 열고 `dwOpenFlags` ofRead로 설정한 것이 공유에 적합 합니다. 즉, 후속 경우 호출 `OpenScope` 이전에 연 파일의 이름을 전달, 기존 범위를 다시 사용 되 고 새 데이터 구조 집합이 만들어지지 않습니다. 그러나 이러한 공유로 인해 문제가 발생할 수 있습니다.  
  
 .NET framework 버전 2.0에서 범위 사용 하 여 연 `dwOpenFlags` ofRead로 더 이상 공유 됩니다. 범위를 공유할 수 있도록 ofReadOnly 값을 사용 합니다. 범위를 공유 하면 "읽기/쓰기" 메타 데이터 인터페이스를 사용 하는 쿼리가 실패 합니다.  
  
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
