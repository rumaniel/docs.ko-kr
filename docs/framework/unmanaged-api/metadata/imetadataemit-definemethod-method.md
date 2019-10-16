---
title: IMetaDataEmit::DefineMethod 메서드
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.DefineMethod
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::DefineMethod
helpviewer_keywords:
- DefineMethod method [.NET Framework metadata]
- IMetaDataEmit::DefineMethod method [.NET Framework metadata]
ms.assetid: 3e2102c5-48b7-4c0e-b805-7e2b5e156e3d
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 4297b21970fbca4b5aa53c31680394cab358d255
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67777604"
---
# <a name="imetadataemitdefinemethod-method"></a>IMetaDataEmit::DefineMethod 메서드
지정된 된 시그니처를 사용 하 여 메서드 또는 전역 함수에 대 한 정의 만들고 해당 메서드 정의에 토큰을 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT DefineMethod (      
    [in]  mdTypeDef         td,   
    [in]  LPCWSTR           szName,   
    [in]  DWORD             dwMethodFlags,   
    [in]  PCCOR_SIGNATURE   pvSigBlob,   
    [in]  ULONG             cbSigBlob,   
    [in]  ULONG             ulCodeRVA,   
    [in]  DWORD             dwImplFlags,   
    [out] mdMethodDef      *pmd  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `td`  
 [in] `mdTypedef` 부모 클래스의 부모 인터페이스 메서드의 토큰입니다. 설정할 `td` 에 `mdTokenNil`전역 함수를 정의 하는 경우.  
  
 `szName`  
 [in] 유니코드의 멤버 이름입니다.  
  
 `dwMethodFlags`  
 [in] 값을 [CorMethodAttr](../../../../docs/framework/unmanaged-api/metadata/cormethodattr-enumeration.md) 메서드 또는 전역 함수의 특성을 지정 하는 열거형입니다.  
  
 `pvSigBlob`  
 [in] 메서드 시그니처입니다. 서명은 제공 하는 대로 유지 됩니다. 모든 매개 변수에 대 한 추가 정보를 지정 해야 할 경우 사용 합니다 [imetadataemit:: Setparamprops](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-setparamprops-method.md) 메서드.  
  
 `cbSigBlob`  
 [in] 바이트 수가 `pvSigBlob`합니다.  
  
 `ulCodeRVA`  
 [in] 코드의 주소입니다.  
  
 `dwImplFlags`  
 [in] 값을 [CorMethodImpl](../../../../docs/framework/unmanaged-api/metadata/cormethodimpl-enumeration.md) 메서드 구현 기능을 지정 하는 열거형입니다.  
  
 `pmd`  
 [out] 멤버 토큰입니다.  
  
## <a name="remarks"></a>설명  
 메타 데이터 API 호출자가 내보낸 지정 된 바깥쪽 클래스 또는 인터페이스에 설명 된 대로 동일한 순서로 메서드를 유지 하도록 보장 합니다 `td` 매개 변수입니다.  
  
 사용과 관련 된 추가 정보 `DefineMethod` 및 특정 매개 변수 설정은 다음과 같습니다.  
  
## <a name="slots-in-the-v-table"></a>V-테이블의 슬롯  
 런타임은은 메서드 정의 사용 하 여 v 테이블 슬롯 설정. 하나 이상의 슬롯 건너뛴, 이러한 해야 하는 경우에는 COM 인터페이스 레이아웃으로 패리티를 유지 하는 것에 대 한 더미 메서드를 정의 슬롯 또는 v-테이블에 대 한 슬롯을 차지 하도록 설정를 `dwMethodFlags` 에 `mdRTSpecialName` 의 값을 [CorMethodAttr](../../../../docs/framework/unmanaged-api/metadata/cormethodattr-enumeration.md) 열거형으로 이름을 지정:  
  
 _VtblGap\<*SequenceNumber*>\<\_*CountOfSlots*>
  
 여기서 *SequenceNumber* 메서드의 시퀀스 번호 및 *CountOfSlots* v-table에서 건너뛸 슬롯입니다. 하는 경우 *CountOfSlots* 는 생략 하면 1 이라고 가정 합니다. 이러한 더미 메서드 또는 비관리 코드에서 호출할 수 없는 및 예외를 생성 하는 관리 코드 또는 비관리 코드에서 호출 하려고 합니다. 유일한 용도 런타임에서 COM 통합에 대 한 생성 하는 v-테이블의 공간을 차지 하도록입니다.  
  
## <a name="duplicate-methods"></a>중복 메서드  
 중복 된 메서드를 정의 하면 안 됩니다. 즉, 호출 하면 안 `DefineMethod` 에서 값 중복 집합을 사용 하 여는 `td`, `wzName`, 및 `pvSig` 매개 변수입니다. (이러한 세 개의 매개 변수를 함께 고유 메서드를 정의 합니다.). 메서드 정의 중 하나에 대해 설정 된 중복 3을 사용할 수 있지만 합니다 `mdPrivateScope` 비트는 `dwMethodFlags` 매개 변수입니다. (의 `mdPrivateScope` 비트 의미 컴파일러가 메서드 정의에 대 한 참조를 내보내지 것입니다.)  
  
## <a name="method-implementation-information"></a>메서드 구현 정보  
 메서드 구현에 대 한 정보는 메서드가 선언 시 알 수 없습니다 경우가 많습니다. 값을 전달할 필요가 없습니다 따라서 합니다 `ulCodeRVA` 및 `dwImplFlags` 매개 변수를 호출할 때 `DefineMethod`합니다. 값을 통해 나중에 제공할 수 있습니다 [imetadataemit:: Setmethodimplflags](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-setmethodimplflags-method.md) 하거나 [imetadataemit:: Setrva](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-setrva-method.md)를 적절 하 게 합니다.  
  
 플랫폼 호출 (PInvoke) 또는 COM interop 시나리오에서와 같이 일부 상황에서 메서드 본문은 제공 되지 않으면 및 `ulCodeRVA` 0으로 설정 합니다. 이러한 상황에서는 메서드 없습니다 태그를 지정 해야 abstract로 런타임 구현의 찾이 됩니다.  
  
## <a name="defining-a-method-for-pinvoke"></a>PInvoke에 대 한 메서드를 정의합니다.  
 PInvoke를 통해 호출할 각 관리 되지 않는 함수에 대 한 관리 되지 않는 대상 함수를 나타내는 관리 되는 메서드를 정의 해야 합니다. 관리 되는 메서드를 정의 하려면 사용 하 여 `DefineMethod` PInvoke 사용 되는 방식에 따라 특정 값으로 설정 된 매개 변수 중 일부를 사용 하 여:  
  
- PInvoke-관리 되지 않는 DLL에 상주 하는 외부 관리 되지 않는 메서드 호출이 포함 됩니다.  
  
- 로컬 PInvoke-에 현재 관리 되는 모듈에 포함 된 네이티브 관리 되지 않는 메서드 호출이 포함 됩니다.  
  
 매개 변수 설정은 다음 표에 제공 됩니다.  
  
|매개 변수|True PInvoke 값|로컬 PInvoke 값|  
|---------------|-----------------------------|------------------------------|  
|`dwMethodFlags`||설정할 `mdStatic`; 지우기 `mdSynchronized` 및 `mdAbstract`합니다.|  
|`pvSigBlob`|유효한 공용 언어 런타임 (CLR) 메서드 서명이 잘못 된 매개 변수를 사용 하 여 관리 되는 형식입니다.|유효한 CLR 메서드 서명이 잘못 된 매개 변수를 사용 하 여 관리 되는 형식입니다.|  
|`ulCodeRVA`||0|  
|`dwImplFlags`|설정할 `miCil` 고 `miManaged`입니다.|설정할 `miNative` 고 `miUnmanaged`입니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MSCorEE.dll에서 리소스로 사용  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IMetaDataEmit 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md)
- [IMetaDataEmit2 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-interface.md)
