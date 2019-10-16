---
title: IMetaDataDispenserEx 인터페이스
ms.date: 03/30/2017
api_name:
- IMetaDataDispenserEx
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataDispenserEx
helpviewer_keywords:
- IMetaDataDispenserEx interface [.NET Framework metadata]
ms.assetid: 78b3629e-77a2-4406-89c3-56b5cc2c4594
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 96475086b1244ae75ed692dd10cb693af0be9af7
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61992604"
---
# <a name="imetadatadispenserex-interface"></a>IMetaDataDispenserEx 인터페이스
확장 된 [IMetaDataDispenser 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadatadispenser-interface.md) 메타 데이터 Api는 현재 메타 데이터 범위에서 작동 하는 방법을 제어 하는 기능을 제공 하는 인터페이스입니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[FindAssembly 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadatadispenserex-findassembly-method.md)|이 메서드가 구현되지 않았습니다. 를 호출 하는 경우 E_NOTIMPL을 반환 합니다.|  
|[FindAssemblyModule 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadatadispenserex-findassemblymodule-method.md)|이 메서드가 구현되지 않았습니다. 를 호출 하는 경우 E_NOTIMPL을 반환 합니다.|  
|[GetCORSystemDirectory 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadatadispenserex-getcorsystemdirectory-method.md)|현재 CLR (공용 언어 런타임) 저장 하는 디렉터리를 가져옵니다. 이 메서드는 out-of-process-디버거에서 사용에 대해서만 지원 됩니다. 다른 구성 요소에서 호출 하는 경우 E_NOTIMPL이 반환 됩니다.|  
|[GetOption 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadatadispenserex-getoption-method.md)|현재 메타 데이터 범위에 대 한 지정된 된 옵션의 값을 가져옵니다. 현재 메타 데이터 범위에 대 한 호출을 처리 하는 방법을 제어 하는 옵션입니다.|  
|[OpenScopeOnITypeInfo 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadatadispenserex-openscopeonitypeinfo-method.md)|이 메서드가 구현되지 않았습니다. 를 호출 하는 경우 E_NOTIMPL을 반환 합니다.|  
|[SetOption 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadatadispenserex-setoption-method.md)|현재 메타 데이터 범위에 대 한 지정 된 값으로 지정된 된 옵션을 설정합니다. 현재 메타 데이터 범위에 대 한 호출을 처리 하는 방법을 제어 하는 옵션입니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에서 리소스로 사용  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [메타데이터 인터페이스](../../../../docs/framework/unmanaged-api/metadata/metadata-interfaces.md)
- [IMetaDataDispenser 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadatadispenser-interface.md)
- [IMetaDataEmit 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md)
- [IMetaDataImport 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
