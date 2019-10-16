---
title: IMetaDataImport::GetFieldProps 메서드
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetFieldProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetFieldProps
helpviewer_keywords:
- IMetaDataImport::GetFieldProps method [.NET Framework metadata]
- GetFieldProps method [.NET Framework metadata]
ms.assetid: 7b0e9b10-8cef-4ba6-8432-40bf63e65ab1
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 574ac706a07e7fcd701ab04f923d5171bea6f64a
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67782384"
---
# <a name="imetadataimportgetfieldprops-method"></a>IMetaDataImport::GetFieldProps 메서드
지정한 FieldDef 토큰이 참조하는 필드와 연결된 메타데이터를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetFieldProps (  
   [in]  mdFieldDef        mb,   
   [out] mdTypeDef         *pClass,  
   [out] LPWSTR            szField,  
   [in]  ULONG             cchField,   
   [out] ULONG             *pchField,  
   [out] DWORD             *pdwAttr,  
   [in]  PCCOR_SIGNATURE   *ppvSigBlob,   
   [out] ULONG             *pcbSigBlob,   
   [out] DWORD             *pdwCPlusTypeFlag,   
   [out] UVCP_CONSTANT     *ppValue,  
   [out] ULONG             *pcchValue  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `mb`  
 [in] 에 대 한 연결 된 메타 데이터를 가져올 필드를 나타내는 FieldDef 토큰을 반환 합니다.  
  
 `pClass`  
 [out] 클래스에 속하는 필드의 형식을 나타내는 TypeDef 토큰에 대 한 포인터입니다.  
  
 `szField`  
 [out] 필드의 이름입니다.  
  
 `cchField`  
 [in] 와이드 문자에 대 한 버퍼의 크기 *szField*합니다.  
  
 `pchField`  
 [out] 반환된 된 버퍼의 실제 크기입니다.  
  
 `pdwAttr`  
 [out] 필드의 메타 데이터와 관련 된 플래그입니다.  
  
 `ppvSigBlob`  
 [in] 필드를 설명 하는 이진 메타 데이터 값에 대 한 포인터입니다.  
  
 `pcbSigBlob`  
 [out] 크기 (바이트) `ppvSigBlob`합니다.  
  
 `pdwCPlusTypeFlag`  
 [out] 필드의 값 형식을 지정 하는 플래그입니다.  
  
 `ppValue`  
 [out] 필드는 상수 값입니다.  
  
 `pcchValue`  
 [out] 문자 크기 `ppValue`, 문자열이 없는 경우 0입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IMetaDataImport 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
- [IMetaDataImport2 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
