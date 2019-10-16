---
title: IMetaDataImport::GetEventProps 메서드
ms.date: 03/30/2017
api_name:
- IMetaDataImport.GetEventProps
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport::GetEventProps
helpviewer_keywords:
- IMetaDataImport::GetEventProps method [.NET Framework metadata]
- GetEventProps method [.NET Framework metadata]
ms.assetid: 5eaf3b4a-92b7-4d5b-97e0-1e83721e0052
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: c87f2212c761dc31a75addabca6970c5497aa2a0
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67782423"
---
# <a name="imetadataimportgeteventprops-method"></a>IMetaDataImport::GetEventProps 메서드
선언 형식, 추가 및 제거 메서드를 대리자에 대해 플래그 및 기타 관련된 데이터를 포함 하 여, 지정한 이벤트 토큰이 나타내는 이벤트에 대 한 메타 데이터 정보를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT GetEventProps (  
   [in]  mdEvent       ev,  
   [out] mdTypeDef     *pClass,   
   [out] LPCWSTR       szEvent,   
   [in]  ULONG         cchEvent,   
   [out] ULONG         *pchEvent,   
   [out] DWORD         *pdwEventFlags,  
   [out] mdToken       *ptkEventType,  
   [out] mdMethodDef   *pmdAddOn,   
   [out] mdMethodDef   *pmdRemoveOn,   
   [out] mdMethodDef   *pmdFire,   
   [out] mdMethodDef   rmdOtherMethod[],   
   [in]  ULONG         cMax,  
   [out] ULONG         *pcOtherMethod  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `ev`  
 [in] 이벤트 메타 데이터에 대 한 메타 데이터를 가져올 이벤트를 나타내는 토큰입니다.  
  
 `pClass`  
 [out] 이벤트를 선언 하는 클래스를 나타내는 TypeDef 토큰에 대 한 포인터입니다.  
  
 `szEvent`  
 [out] 참조 하는 이벤트의 이름을 `ev`입니다.  
  
 `pchEvent`  
 [in] 요청된 된 길이의 와이드 문자 `szEvent`합니다.  
  
 `pdwEventFlags`  
 [out] 와이드 문자에서는 반환 된 길이 `szEvent`입니다.  
  
 `ptkEventType`  
 [out] TypeRef 또는 TypeDef 메타 데이터 토큰을 나타내는에 대 한 포인터를 <xref:System.Delegate> 이벤트 유형입니다.  
  
 `pmdAddOn`  
 [out] 이벤트 처리기를 추가 하는 메서드를 나타내는 메타 데이터 토큰에 대 한 포인터입니다.  
  
 `pmdRemoveOn`  
 [out] 이벤트 처리기를 제거 하는 메서드를 나타내는 메타 데이터 토큰에 대 한 포인터입니다.  
  
 `pmdFire`  
 [out] 이벤트를 발생 시키는 메서드를 나타내는 메타 데이터 토큰에 대 한 포인터입니다.  
  
 `rmdOtherMethod`  
 [out] 이벤트와 연결 된 다른 메서드를 토큰 포인터의 배열입니다.  
  
 `cMax`  
 [in] `rmdOtherMethod` 배열의 최대 크기입니다.  
  
 `pcOtherMethod`  
 [out] 반환 된 토큰 수 `rmdOtherMethod`입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IMetaDataImport 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)
- [IMetaDataImport2 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
