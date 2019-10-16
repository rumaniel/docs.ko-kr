---
title: IMetaDataImport::GetMethodProps 메서드
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetMethodProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetMethodProps
helpviewer_keywords:
- GetMethodProps method [.NET Framework metadata]
- IMetaDataImport::GetMethodProps method [.NET Framework metadata]
ms.assetid: e0667ef7-1d31-4c89-a2d3-d426f023f8d2
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 27b2867019085bf5b44f2ee364c07af66144d4b5
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67782335"
---
# <a name="imetadataimportgetmethodprops-method"></a>IMetaDataImport::GetMethodProps 메서드
지정한 MethodDef 토큰이 참조하는 메서드와 연결된 메타데이터를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetMethodProps (  
    [in]  mdMethodDef         mb,  
    [out] mdTypeDef           *pClass,  
    [out] LPWSTR              szMethod,  
    [in]  ULONG               cchMethod,  
    [out] ULONG               *pchMethod,  
    [out] DWORD               *pdwAttr,  
    [out] PCCOR_SIGNATURE     *ppvSigBlob,  
    [out] ULONG               *pcbSigBlob,  
    [out] ULONG               *pulCodeRVA,  
    [out] DWORD               *pdwImplFlags  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `mb`  
 [in] 에 대 한 메타 데이터를 반환할 메서드를 나타내는 MethodDef 토큰입니다.  
  
 `pClass`  
 [out] 메서드를 구현 하는 형식을 나타내는 TypeDef 토큰에 대 한 포인터입니다.  
  
 `szMethod`  
 [out] 메서드의 이름을 포함 하는 버퍼에 대 한 포인터입니다.  
  
 `cchMethod`  
 [in] 요청된 된 크기의 `szMethod`합니다.  
  
 `pchMethod`  
 [out] 와이드 문자에서 크기에 대 한 포인터 `szMethod`, 또는 메서드 이름에 와이드 문자 수가 실제 잘리는 경우.  
  
 `pdwAttr`  
 [out] 메서드를 사용 하 여 연결 된 모든 플래그에 대 한 포인터입니다.  
  
 `ppvSigBlob`  
 [out] 메서드 서명의 이진 메타 데이터에 대 한 포인터입니다.  
  
 `pcbSigBlob`  
 [out] 바이트의 크기에 대 한 포인터 `ppvSigBlob`합니다.  
  
 `pulCodeRVA`  
 [out] 메서드의 상대 가상 주소에 대 한 포인터입니다.  
  
 `pdwImplFlags`  
 [out] 메서드에 대 한 구현 플래그에 대 한 포인터입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IMetaDataImport 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
- [IMetaDataImport2 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
