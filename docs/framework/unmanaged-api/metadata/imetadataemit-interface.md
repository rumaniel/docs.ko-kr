---
title: IMetaDataEmit 인터페이스
ms.date: 03/30/2017
api_name:
- IMetaDataEmit
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit
helpviewer_keywords:
- IMetaDataEmit interface [.NET Framework metadata]
ms.assetid: 3b48fd47-7397-4e2c-8bec-8157aa08978c
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 4c77edfff640f796dd3f345eaeb4728830c5f4c6
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33449146"
---
# <a name="imetadataemit-interface"></a>IMetaDataEmit 인터페이스
생성, 수정 및 현재 정의 된 범위에서 어셈블리에 대 한 메타 데이터를 저장 하는 메서드를 제공 합니다. 메타 데이터 메모리에 저장 하거나 디스크에 저장 될 수 있습니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[ApplyEditAndContinue 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-applyeditandcontinue-method.md)|현재 어셈블리 범위 지정 된 변경 내용으로 업데이트 `pImport`합니다.|  
|[DefineCustomAttribute 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-definecustomattribute-method.md)|지정한 메타 데이터 서명이 지정된 된 개체에 연결 될 사용 하 여 사용자 지정 특성에 대 한 정의 만들고 해당 사용자 지정 특성 정의 토큰을 가져옵니다.|  
|[DefineEvent 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-defineevent-method.md)|지정한 메타 데이터 서명을 사용 하 여 이벤트에 대 한 정의 만들고 해당 이벤트 정의 토큰을 가져옵니다.|  
|[DefineField 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-definefield-method.md)|지정한 메타 데이터 서명을 사용 하 여 필드에 대 한 정의 만들고 해당 필드 정의 하는 토큰을 가져옵니다.|  
|[DefineImportMember 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-defineimportmember-method.md)|현재 범위를 벗어난 모듈에서 정의 되 고 해당 참조 정의 대 한 토큰을 가져옵니다 형식의 멤버에 대 한 정의 만듭니다.|  
|[DefineImportType 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-defineimporttype-method.md)|현재 범위를 벗어난 모듈에 정의 되어 있으며 토큰 참조 정의을 가져옵니다 하는 형식에 대 한 참조에 대 한 정의 만듭니다.|  
|[DefineMemberRef 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-definememberref-method.md)|현재 범위를 벗어난 모듈의 멤버에 대 한 참조에 대 한 정의 만들고 해당 참조 정의 하는 토큰을 가져옵니다.|  
|[DefineMethod 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-definemethod-method.md)|지정한 서명을 가진는 메서드에 대 한 정의 만들고 해당 메서드 정의에 토큰을 반환 합니다.|  
|[DefineMethodImpl 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-definemethodimpl-method.md)|인터페이스에서 상속 된 메서드의 구현에 대 한 정의 만들고 해당 메서드 구현 정의에 토큰을 반환 합니다.|  
|[DefineModuleRef 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-definemoduleref-method.md)|지정 된 이름의 모듈에 대 한 메타 데이터 서명을 만듭니다.|  
|[DefineNestedType 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-definenestedtype-method.md)|형식 정의의 메타 데이터 서명을 만들고 반환는 `mdTypeDef` 해당 형식에 정의 된 형식에서 참조 형식의 멤버 임을 지정에 대 한 토큰 `tdEncloser`합니다.|  
|[DefineParam 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-defineparam-method.md)|지정된 된 토큰에서 참조 하는 메서드에 대 한 지정한 서명을 가진 매개 변수 정의 만들고 해당 매개 변수 정의 대 한 토큰을 가져옵니다.|  
|[DefinePermissionSet 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-definepermissionset-method.md)|지정 된 메타 데이터 서명을 가진 권한 집합에 대 한 정의 만들고 해당 사용 권한 집합 정의에 토큰을 가져옵니다.|  
|[DefinePinvokeMap 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-definepinvokemap-method.md)|지정한 토큰이 참조 하는 메서드에 PInvoke 시그니처의 기능을 설정 합니다.|  
|[DefineProperty 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-defineproperty-method.md)|지정 된 지정된 된 형식에 대 한 속성 정의 만들고 `get` 및 `set` 메서드 접근자를 토큰 정의 속성을 가져옵니다.|  
|[DefineSecurityAttributeSet 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-definesecurityattributeset-method.md)|지정한 토큰이 참조 하는 개체에 연결 하는 보안 권한 집합을 만듭니다.|  
|[DefineTypeDef 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-definetypedef-method.md)|공용 언어 런타임 형식에 대 한 형식 정의 만들고 해당 형식 정의에 메타 데이터 토큰을 가져옵니다.|  
|[DefineTypeRefByName 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-definetyperefbyname-method.md)|현재 범위 외부의 다른 모듈에 정의 된 형식에 대 한 메타 데이터를 토큰을 가져옵니다.|  
|[DefineUserString 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-defineuserstring-method.md)|지정된 된 리터럴 문자열에 대 한 메타 데이터를 토큰을 가져옵니다.|  
|[DeleteClassLayout 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-deleteclasslayout-method.md)|지정한 토큰이 참조 하는 형식에 대 한 클래스 레이아웃 메타 데이터 서명을 제거 합니다.|  
|[DeleteFieldMarshal 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-deletefieldmarshal-method.md)|지정한 토큰이 참조 하는 개체에 대 한 메타 데이터 서명을 마샬링 PInvoke를 제거 합니다.|  
|[DeletePinvokeMap 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-deletepinvokemap-method.md)|지정한 토큰이 참조 하는 개체에 대 한 PInvoke 매핑 메타 데이터를 제거 합니다.|  
|[DeleteToken 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-deletetoken-method.md)|현재 메타 데이터 범위에서 지정된 된 토큰을 삭제합니다.|  
|[GetSaveSize 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-getsavesize-method.md)|현재 범위에서 어셈블리의 예상된 이진 크기를 가져옵니다.|  
|[GetTokenFromSig 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-gettokenfromsig-method.md)|지정한 메타 데이터 서명에 대 한 토큰을 가져옵니다.|  
|[GetTokenFromTypeSpec 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-gettokenfromtypespec-method.md)|지정한 메타 데이터 서명 사용 하 여 형식에 대 한 메타 데이터를 토큰을 가져옵니다.|  
|[Merge 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-merge-method.md)|병합 해야 하는 범위 목록에 지정된 된 가져오기 범위를 추가 합니다.|  
|[MergeEnd 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-mergeend-method.md)|하나 이상의 이전 호출에 의해 지정 된 모든 메타 데이터 범위를 범위에 현재 병합 `IMetaDataEmit::Merge`합니다.|  
|[Save 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-save-method.md)|지정된 된 주소에서 파일에는 현재 범위에서 모든 메타 데이터를 저장 합니다.|  
|[SaveToMemory 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-savetomemory-method.md)|메모리의 지정된 된 영역을 현재 범위에서 모든 메타 데이터를 저장 합니다.|  
|[SaveToStream 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-savetostream-method.md)|지정 된 현재 범위에서 모든 메타 데이터를 저장 `IStream`합니다.|  
|[SetClassLayout 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-setclasslayout-method.md)|설정 하거나 업데이트에 대 한 이전 호출에서 정의 된 형식의 클래스 레이아웃 서명을 `IMetaDataEmit::DefineTypeDef`합니다.|  
|[SetCustomAttributeValue 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-setcustomattributevalue-method.md)|설정에 대 한 이전 호출에서 정의한 사용자 지정 특성의 값을 업데이트 하거나 `IMetaDataEmit::DefineCustomAttribute`합니다.|  
|[SetEventProps 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-seteventprops-method.md)|설정 하거나 업데이트에 대 한 이전 호출에서 정의 된 이벤트의 지정된 된 기능 `IMetaDataEmit::DefineEvent`합니다.|  
|[SetFieldMarshal 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-setfieldmarshal-method.md)|지정한 토큰이 참조 하는 필드, return, 메서드 또는 메서드 매개 변수의 대 한 마샬링 정보 PInvoke를 설정 합니다.|  
|[SetFieldProps 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-setfieldprops-method.md)|설정 하거나 지정 된 필드 토큰이 참조 하는 필드에 대 한 기본값을 업데이트 합니다.|  
|[SetFieldRVA 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-setfieldrva-method.md)|지정한 토큰이 참조 하는 필드의 상대 가상 주소에 대 한 전역 변수 값을 설정 합니다.|  
|[SetHandler 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-sethandler-method.md)|지정 된에서 참조 하는 방법을 설정 `IUnknown` 토큰 다시 매핑에 대 한 알림 콜백 포인터입니다.|  
|[SetMethodImplFlags 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-setmethodimplflags-method.md)|설정 하거나 상속 된 메서드 구현에서 지정된 된 토큰 참조의 메타 데이터 서명을 업데이트 합니다.|  
|[SetMethodProps 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-setmethodprops-method.md)|설정 하거나 지정된 된 상대 가상 주소, 이전 호출에서 정의 된 메서드의 저장 하는 기능을 업데이트 `IMetaDataEmit::DefineMethod`합니다.|  
|[SetModuleProps 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-setmoduleprops-method.md)|이전 호출에서 정의 된 모듈에 대 한 참조를 업데이트 `IMetaDataEmit::DefineModuleRef`합니다.|  
|[SetParamProps 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-setparamprops-method.md)|변경 된 기능에 대 한 이전 호출에서 정의 된 메서드의 매개 변수를 설정 하거나 `IMetaDataEmit::DefineParam`합니다.|  
|[SetParent 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-setparent-method.md)|설정에 대 한 이전 호출에 정의 된 대로 지정된 된 멤버를 `IMetaDataEmit::DefineMemberRef`, 이전 호출에 정의 된 대로 지정 된 형식의 멤버는 `IMetaDataEmit::DefineTypeDef`합니다.|  
|[SetPermissionSetProps 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-setpermissionsetprops-method.md)|설정 하거나 업데이트 기능에 대 한 이전 호출에 의해 정의 된 사용 권한 집합의 메타 데이터 서명의 `IMetaDataEmit::DefinePermissionSet`합니다.|  
|[SetPinvokeMap 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-setpinvokemap-method.md)|설정 하거나 이전 호출에 정의 된 대로 메서드의 PInvoke 서명의 기능 변경 `IMetaDataEmit::DefinePinvokeMap`합니다.|  
|[SetPropertyProps 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-setpropertyprops-method.md)|이전 호출에서 정의한 속성에 대 한 메타 데이터에 저장 하는 기능을 설정 `IMetaDataEmit::DefineProperty`합니다.|  
|[SetRVA 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-setrva-method.md)|지정 된 메서드의 상대 가상 주소를 설정합니다.|  
|[SetTypeDefProps 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-settypedefprops-method.md)|이전 호출에서 정의 된 형식 기능을 설정 `IMetaDataEmit::DefineTypeDef`합니다.|  
|[TranslateSigWithScope 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-translatesigwithscope-method.md)|현재 범위에 어셈블리를 가져오고 병합 된 범위에 대 한 새 메타 데이터 서명을 가져옵니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** 참조 [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)합니다.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에서 리소스로 사용  
  
 **.NET framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고 항목  
 [메타데이터 인터페이스](../../../../docs/framework/unmanaged-api/metadata/metadata-interfaces.md)  
 [IMetaDataEmit2 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-interface.md)
