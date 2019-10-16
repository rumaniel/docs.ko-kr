---
title: IMetaDataImport::GetNameFromToken 메서드
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetNameFromToken
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetNameFromToken
helpviewer_keywords:
- GetNameFromToken method [.NET Framework metadata]
- IMetaDataImport::GetNameFromToken method [.NET Framework metadata]
ms.assetid: 32114ecf-8916-4ab2-a201-179c017344f1
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: fa6e8665e5e2194eb4a3dffad8e97a69deb202d0
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67778983"
---
# <a name="imetadataimportgetnamefromtoken-method"></a>IMetaDataImport::GetNameFromToken 메서드
지정한 메타데이터 토큰에서 참조된 개체의 UTF-8 이름을 가져옵니다. 이 메서드는 사용되지 않습니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetNameFromToken (  
   [in] mdToken      tk,  
   [out] MDUTF8CSTR  *pszUtf8NamePtr  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `tk`  
 [in] 에 대 한 이름을 반환할 개체를 나타내는 토큰입니다.  
  
 `pszUtf8NamePtr`  
 [out] 힙에 있는 u t F-8 개체 이름에 대 한 포인터입니다.  
  
## <a name="remarks"></a>설명  
 `GetNameFromToken`는 사용되지 않습니다. 대신 특정 형식의 토큰이 필요한 경우와 같은 속성을 가져오는 메서드를 호출 `GetFieldProps` 필드에 대해 또는 `GetMethodProps` 메서드에 대 한 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에 리소스로 포함  
  
 **.NET framework 버전:** 1.0  
  
## <a name="see-also"></a>참고자료

- [IMetaDataImport 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
- [IMetaDataImport2 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
