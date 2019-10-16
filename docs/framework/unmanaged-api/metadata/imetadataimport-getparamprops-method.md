---
title: IMetaDataImport::GetParamProps 메서드
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetParamProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetParamProps
helpviewer_keywords:
- IMetaDataImport::GetParamProps method [.NET Framework metadata]
- GetParamProps method [.NET Framework metadata]
ms.assetid: 4d5e5f00-bcab-4f41-b191-176511a186a7
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: e9d2c74adecdfb0201f9f0c08998feba674f9e0f
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67778930"
---
# <a name="imetadataimportgetparamprops-method"></a>IMetaDataImport::GetParamProps 메서드
지정한 ParamDef 토큰이 참조하는 매개 변수에 대한 메타데이터 값을 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetParamProps (  
   [in]  mdParamDef      tk,  
   [out] mdMethodDef     *pmd,  
   [out] ULONG           *pulSequence,  
   [out] LPWSTR          szName,  
   [in]  ULONG           cchName,  
   [out] ULONG           *pchName,  
   [out] DWORD           *pdwAttr,  
   [out] DWORD           *pdwCPlusTypeFlag,  
   [out] UVCP_CONSTANT   *ppValue,  
   [out] ULONG           *pcchValue  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `tk`  
 [in] 에 대 한 메타 데이터를 반환 하려면 매개 변수를 나타내는 ParamDef 토큰입니다.  
  
 `pmd`  
 [out] 매개 변수를 사용 하는 메서드를 나타내는 MethodDef 토큰에 대 한 포인터입니다.  
  
 `pulSequence`  
 [out] 메서드 인수 목록에 있는 매개 변수의 서 수 위치입니다.  
  
 `szName`  
 [out] 매개 변수의 이름을 포함 하도록 버퍼입니다.  
  
 `cchName`  
 [in] 요청된 된 크기의 와이드 문자에서 `szName`합니다.  
  
 `pchName`  
 [out] 반환 되는 크기의 와이드 문자에서 `szName`합니다.  
  
 `pdwAttr`  
 [out] 매개 변수를 사용 하 여 연결 된 모든 특성 플래그에 대 한 포인터입니다. 이 비트 마스크의 `CorParamAttr` 값입니다.  
  
 `pdwCPlusTypeFlag`  
 [out] 매개 변수가 지정 하는 플래그에 대 한 포인터를 <xref:System.ValueType>입니다.  
  
 `ppValue`  
 [out] 매개 변수에서 반환 하는 상수 문자열 포인터입니다.  
  
 `pcchValue`  
 [out] 크기인 `ppValue` 와이드 문자인 경우 0에 `ppValue` 문자열이 포함 되지 않습니다.  
  
## <a name="remarks"></a>설명

시퀀스 값 `pulSequence` 매개 변수에 대 한 1부터 시작 합니다. 반환 값에 0의 시퀀스 번호가 있습니다.

## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IMetaDataImport 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
- [IMetaDataImport2 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
