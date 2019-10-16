---
title: IMetaDataInfo::GetFileMapping 메서드
ms.date: 03/30/2017
api_name:
- IMetaDataInfo.GetFileMapping
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataInfo::GetFileMapping
helpviewer_keywords:
- IMetaDataInfo::GetFileMapping method [.NET Framework metadata]
- GetFileMapping method [.NET Framework metadata]
ms.assetid: 2868dfec-c992-4606-88bb-a8e0b6b18271
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 22af95ef4bd1fca0a8253faa6ce0e1c7a862054d
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67782655"
---
# <a name="imetadatainfogetfilemapping-method"></a>IMetaDataInfo::GetFileMapping 메서드
매핑의 형식과 매핑된 파일의 메모리 영역을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetFileMapping (  
    [out] const void           **ppvData,   
    [out] ULONGLONG            *pcbData,   
    [out] DWORD                *pdwMappingType  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `ppvData`  
 [out] 매핑된 파일의 시작 부분에 대 한 포인터입니다.  
  
 `pcbData`  
 [out] 매핑된 영역의 크기입니다. 하는 경우 `pdwMappingType` 는 `fmFlat`, 파일의 크기입니다.  
  
 `pdwMappingType`  
 [out] A [CorFileMapping](../../../../docs/framework/unmanaged-api/metadata/corfilemapping-enumeration.md) 매핑 형식을 나타내는 값입니다. CLR (공용 언어 런타임)의 현재 구현은 항상 `fmFlat`합니다. 다른 값은 나중에 사용에 대 한 예약 됩니다. 그러나 항상 확인 해야 반환된 된 값이 다른 값 이후 버전에서 사용할 수 있습니다 하거나 서비스 릴리스 합니다.  
  
## <a name="return-value"></a>반환 값  
  
|HRESULT|Description|  
|-------------|-----------------|  
|`S_OK`|모든 출력은 채워집니다.|  
|`E_INVALIDARG`|NULL 인수 값으로 전달 되었습니다.|  
|`COR_E_NOTSUPPORTED`|CLR 구현은 메모리 영역에 대 한 정보를 제공할 수 없습니다. 이 작업은 다음과 같은 이유로 발생할 수 있습니다.<br /><br /> -메타 데이터 범위를 사용 하 여 열린 합니다 `ofWrite` 또는 `ofCopyMemory` 플래그입니다.<br />하지 않고 열림-메타 데이터 범위는 `ofReadOnly` 플래그입니다.<br />- [Imetadatadispenser:: Openscopeonmemory](../../../../docs/framework/unmanaged-api/metadata/imetadatadispenser-openscopeonmemory-method.md) 메서드는 파일의 메타 데이터 부분에 여는 데 사용 되었습니다.<br />-파일이 pe (이식 가능) 파일이 아닙니다. **참고:**  이러한 조건을 CLR 구현에 종속 되며 기능이 약화 될 수 이후 버전의 CLR.|  
  
## <a name="remarks"></a>설명  
 메모리는 `ppvData` 동안만 기본 메타 데이터 범위의 열려 가리키는 유효 합니다.  
  
 이 메서드를 호출 하 여 메모리에는 디스크에 있는 파일의 메타 데이터를 매핑할 때는 작동 되려면 합니다 [imetadatadispenser:: Openscope](../../../../docs/framework/unmanaged-api/metadata/imetadatadispenser-openscope-method.md) 지정 해야 합니다는 `ofReadOnly` 플래그를 지정 해야 합니다는 `ofWrite` 또는 `ofCopyMemory` 플래그입니다.  
  
 선택한 각 범위에 대 한 파일 매핑 형식은 CLR의 특정된 구현에 따라 다릅니다. 사용자가 설정할 수 없습니다. CLR의 현재 구현은 항상 `fmFlat` 에서 `pdwMappingType`, CLR의 버전 또는 나중에 지정된 된 버전의 서비스 릴리스에서도 나중에 변경할 수 있습니다이 있지만. 반환된 된 값을 항상 확인 해야 `pdwMappingType`이므로 다양 한 레이아웃 및 오프셋 다른 형식을 갖습니다.  
  
 세 가지 매개 변수 중 하나는 NULL을 전달 하는 것은 지원 되지 않습니다. 메서드는 반환 `E_INVALIDARG`, 출력 하나도 채워집니다. 매핑 형식 또는 영역의 크기를 무시 하 고 비정상적인 프로그램 종료 될 수 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에서 리소스로 사용  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IMetaDataInfo 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadatainfo-interface.md)
- [CorFileMapping 열거형](../../../../docs/framework/unmanaged-api/metadata/corfilemapping-enumeration.md)
