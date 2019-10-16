---
title: IMetaDataImport 인터페이스
ms.date: 03/30/2017
api_name:
- IMetaDataImport
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataImport
helpviewer_keywords:
- IMetaDataImport interface [.NET Framework metadata]
ms.assetid: 0adbbd35-5e8d-4fec-8268-dc70a07c5975
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: a0f4eb244e02e13e418a55351dbc1eb1f5b5d16d
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64617737"
---
# <a name="imetadataimport-interface"></a>IMetaDataImport 인터페이스
PE(이식 가능) 파일이나 형식 라이브러리 또는 독립 실행형 런타임 메타데이터 이진과 같은 기타 소스에서 기존 메타데이터를 가져오고 조작하는 메서드를 제공합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[CloseEnum 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-closeenum-method.md)|지정된 핸들을 사용하여 열거자를 닫습니다.|  
|[CountEnum 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-countenum-method.md)|지정된 핸들을 사용하여 열거자의 요소 수를 가져옵니다.|  
|[EnumCustomAttributes 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-enumcustomattributes-method.md)|지정한 형식이나 멤버와 연결된 사용자 지정 특성 정의 토큰 목록을 열거합니다.|  
|[EnumEvents 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-enumevents-method.md)|지정한 TypeDef 토큰에 대한 이벤트 정의 토큰을 열거합니다.|  
|[EnumFields 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-enumfields-method.md)|지정한 TypeDef 토큰이 참조하는 형식에 대한 FieldDef 토큰을 열거합니다.|  
|[EnumFieldsWithName 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-enumfieldswithname-method.md)|지정한 이름을 가진 지정한 형식의 FieldDef 토큰을 열거합니다.|  
|[EnumInterfaceImpls 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-enuminterfaceimpls-method.md)|인터페이스 구현을 나타내는 MethodDef 토큰을 열거합니다.|  
|[EnumMemberRefs 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-enummemberrefs-method.md)|지정한 형식의 멤버를 나타내는 MemberRef 토큰을 열거합니다.|  
|[EnumMembers 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-enummembers-method.md)|지정한 형식의 멤버를 나타내는 MemberDef 토큰을 열거합니다.|  
|[EnumMembersWithName 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-enummemberswithname-method.md)|지정한 이름을 가진 지정한 형식의 멤버를 나타내는 MemberDef 토큰을 열거합니다.|  
|[EnumMethodImpls 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-enummethodimpls-method.md)|지정한 형식의 메서드를 나타내는 MethodBody 및 MethodDeclaration 토큰을 열거합니다.|  
|[EnumMethods 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-enummethods-method.md)|지정한 형식의 메서드를 나타내는 MethodDef 토큰을 열거합니다.|  
|[EnumMethodSemantics 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-enummethodsemantics-method.md)|지정한 메서드와 관련된 속성 및 속성 변경 이벤트를 열거합니다.|  
|[EnumMethodsWithName 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-enummethodswithname-method.md)|지정한 TypeDef 토큰이 참조하는 형식으로 정의되고 지정한 이름을 가진 메서드를 열거합니다.|  
|[EnumModuleRefs 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-enummodulerefs-method.md)|가져온 모듈을 나타내는 ModuleRef 토큰을 열거합니다.|  
|[EnumParams 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-enumparams-method.md)|지정한 MethodDef 토큰이 참조하는 메서드의 매개 변수를 나타내는 ParamDef 토큰을 열거합니다.|  
|[EnumPermissionSets 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-enumpermissionsets-method.md)|지정한 메타데이터 범위의 개체에 대한 권한을 열거합니다.|  
|[EnumProperties 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-enumproperties-method.md)|지정한 TypeDef 토큰이 참조하는 형식의 속성을 나타내는 PropertyDef 토큰을 열거합니다.|  
|[EnumSignatures 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-enumsignatures-method.md)|현재 범위의 독립 실행형 서명을 나타내는 Signature 토큰을 열거합니다.|  
|[EnumTypeDefs 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-enumtypedefs-method.md)|현재 범위 내의 모든 형식을 나타내는 TypeDef 토큰을 열거합니다.|  
|[EnumTypeRefs 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-enumtyperefs-method.md)|현재 메타데이터 범위에서 정의된 TypeRef 토큰을 열거합니다.|  
|[EnumTypeSpecs 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-enumtypespecs-method.md)|현재 메타데이터 범위에서 정의된 TypeSpec 토큰을 열거합니다.|  
|[EnumUnresolvedMethods 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-enumunresolvedmethods-method.md)|현재 메타데이터 범위에서 확인되지 않은 메서드를 나타내는 MemberDef 토큰을 열거합니다.|  
|[EnumUserStrings 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-enumuserstrings-method.md)|현재 메타데이터 범위에서 하드 코드된 문자열을 나타내는 String 토큰을 열거합니다.|  
|[FindField 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-findfield-method.md)|지정한 형식의 멤버이며 지정한 이름 및 메타데이터 서명을 가진 필드에 대한 FieldDef 토큰을 가져옵니다.|  
|[FindMember 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-findmember-method.md)|지정한 형식으로 정의되고 지정한 이름 및 메타데이터 서명을 가진 멤버에 대한 MemberDef 토큰을 가져옵니다.|  
|[FindMemberRef 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-findmemberref-method.md)|지정한 형식으로 정의되고 지정한 이름 및 메타데이터 서명을 가진 멤버에 대한 MemberRef 토큰을 가져옵니다.|  
|[FindMethod 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-findmethod-method.md)|지정한 형식으로 정의되고 지정한 이름 및 메타데이터 서명을 가진 메서드에 대한 MethodDef 토큰을 가져옵니다.|  
|[FindTypeDefByName 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-findtypedefbyname-method.md)|지정한 이름을 가진 형식의 TypeDef 메타데이터 토큰에 대한 포인터를 가져옵니다.|  
|[FindTypeRef 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-findtyperef-method.md)|지정한 검색 범위에서 지정한 이름을 가진 형식을 참조하는 TypeRef 메타데이터 토큰에 대한 포인터를 가져옵니다.|  
|[GetClassLayout 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-getclasslayout-method.md)|지정한 TypeDef 토큰이 참조하는 클래스에 대한 레이아웃 정보를 가져옵니다.|  
|[GetCustomAttributeByName 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-getcustomattributebyname-method.md)|해당 이름이 지정된 경우 사용자 지정 특성의 값을 가져옵니다.|  
|[GetCustomAttributeProps 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-getcustomattributeprops-method.md)|해당 메타데이터 토큰이 지정된 경우 사용자 지정 특성의 값을 가져옵니다.|  
|[GetEventProps 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-geteventprops-method.md)|지정한 이벤트 토큰이 나타내는 이벤트에 대한 메타데이터 정보(선언 형식, 대리자에 대한 추가 및 제거 메서드, 플래그 및 기타 관련 데이터 포함)를 가져옵니다.|  
|[GetFieldMarshal 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-getfieldmarshal-method.md)|지정한 Field 메타데이터 토큰이 나타내는 필드의 관리되지 않는 기본 형식에 대한 포인터를 가져옵니다.|  
|[GetFieldProps 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-getfieldprops-method.md)|지정한 FieldDef 토큰이 참조하는 필드와 연결된 메타데이터를 가져옵니다.|  
|[GetInterfaceImplProps 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-getinterfaceimplprops-method.md)|지정한 메서드를 구현하는 형식 및 해당 메서드를 선언하는 인터페이스의 메타데이터 토큰에 대한 포인터를 가져옵니다.|  
|[GetMemberProps 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-getmemberprops-method.md)|지정한 메타데이터 토큰이 참조하는 형식 멤버의 메타데이터 정보(이름, 이진 서명 및 상대 가상 주소 포함)를 가져옵니다.|  
|[GetMemberRefProps 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-getmemberrefprops-method.md)|지정한 토큰이 참조하는 멤버와 연결된 메타데이터를 가져옵니다.|  
|[GetMethodProps 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-getmethodprops-method.md)|지정한 MethodDef 토큰이 참조하는 메서드와 연결된 메타데이터를 가져옵니다.|  
|[GetMethodSemantics 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-getmethodsemantics-method.md)|지정한 MethodDef 토큰이 참조하는 메서드와 지정한 EventProp 토큰이 참조하는 속성 및 이벤트 쌍 간의 관계에 대한 포인터를 가져옵니다.|  
|[GetModuleFromScope 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-getmodulefromscope-method.md)|현재 메타데이터 범위에서 참조된 모듈의 메타데이터 토큰에 대한 포인터를 가져옵니다.|  
|[GetModuleRefProps 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-getmodulerefprops-method.md)|지정한 메타데이터 토큰에서 참조된 모듈의 이름을 가져옵니다.|  
|[GetNameFromToken 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-getnamefromtoken-method.md)|지정한 메타데이터 토큰에서 참조된 개체의 UTF-8 이름을 가져옵니다.|  
|[GetNativeCallConvFromSig 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-getnativecallconvfromsig-method.md)|지정한 서명 포인터가 나타내는 메서드에 대한 기본 호출 규칙을 가져옵니다.|  
|[GetNestedClassProps 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-getnestedclassprops-method.md)|지정한 중첩 형식의 바깥쪽 부모 형식에 대한 TypeDef 토큰을 가져옵니다.|  
|[GetParamForMethodIndex 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-getparamformethodindex-method.md)|지정한 MethodDef 토큰이 나타내는 메서드에 대한 메서드 매개 변수 시퀀스에서 지정한 서수 위치에 있는 매개 변수를 나타내는 토큰에 대한 포인터를 가져옵니다.|  
|[GetParamProps 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-getparamprops-method.md)|지정한 ParamDef 토큰이 참조하는 매개 변수에 대한 메타데이터 값을 가져옵니다.|  
|[GetPermissionSetProps 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-getpermissionsetprops-method.md)|지정한 권한 토큰이 나타내는 System.Security.PermissionSet와 연결된 메타데이터를 가져옵니다.|  
|[GetPinvokeMap](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-getpinvokemap-method.md)|PInvoke 호출의 대상 어셈블리를 나타내는 ModuleRef 토큰을 가져옵니다.|  
|[GetPropertyProps 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-getpropertyprops-method.md)|지정한 토큰이 나타내는 속성과 연결된 메타데이터를 가져옵니다.|  
|[GetRVA 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-getrva-method.md)|지정한 토큰이 나타내는 코드 개체의 상대 가상 주소 오프셋을 가져옵니다.|  
|[GetScopeProps 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-getscopeprops-method.md)|현재 메타데이터 범위에서 어셈블리 또는 모듈의 이름과 선택적으로 버전 식별자를 가져옵니다.|  
|[GetSigFromToken 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-getsigfromtoken-method.md)|지정한 토큰과 연결된 이진 메타데이터 서명을 가져옵니다.|  
|[GetTypeDefProps 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-gettypedefprops-method.md)|지정한 TypeDef 토큰이 나타내는 형식에 대한 메타데이터 정보를 반환합니다.|  
|[GetTypeRefProps 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-gettyperefprops-method.md)|지정한 TypeRef 토큰이 참조하는 형식과 연결된 메타데이터를 가져옵니다.|  
|[GetTypeSpecFromToken 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-gettypespecfromtoken-method.md)|지정한 토큰이 나타내는 형식 사양의 이진 메타데이터 서명을 가져옵니다.|  
|[GetUserString 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-getuserstring-method.md)|지정한 메타데이터 토큰이 나타내는 리터럴 문자열을 가져옵니다.|  
|[IsGlobal 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-isglobal-method.md)|지정한 메타데이터 토큰이 나타내는 필드, 메서드 또는 형식에 전역 범위가 있는지 여부를 나타내는 값을 가져옵니다.|  
|[IsValidToken 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-isvalidtoken-method.md)|지정한 토큰이 코드 개체에 대한 유효한 참조를 포함하는지 여부를 나타내는 값을 가져옵니다.|  
|[ResetEnum 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-resetenum-method.md)|지정한 열거자를 지정한 위치로 다시 설정합니다.|  
|[ResolveTypeRef 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-resolvetyperef-method.md)|지정한 TypeRef 토큰이 참조하는 형식에 대한 형식 정보를 가져옵니다.|  
  
## <a name="remarks"></a>설명  
 `IMetaDataImport` 인터페이스의 디자인은 주로 형식 정보를 가져오거나(예: 개발 도구) 배포된 구성 요소를 관리(예: 확인/활성화 서비스)하는 도구 및 서비스에서 사용하기 위한 것입니다. `IMetaDataImport`의 메서드는 다음과 같은 작업 범주로 나뉩니다.  
  
- 메타데이터 범위의 항목 컬렉션 열거  
  
- 특정 특성 집합을 가진 항목 찾기  
  
- 지정한 항목의 속성 가져오기  
  
- Get 메서드는 특히 메타데이터 항목의 단일값 속성을 반환하기 위한 것입니다. 속성이 다른 항목에 대한 참조인 경우 해당 항목의 토큰이 반환됩니다. 모든 포인터 입력 유형은 특정 값이 요청되지 않음을 나타내는 NULL일 수 있습니다. 기본적으로 컬렉션 개체(예: 클래스가 구현하는 인터페이스 컬렉션)인 속성을 가져오려면 열거 메서드를 사용합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에서 리소스로 사용  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [메타데이터 인터페이스](../../../../docs/framework/unmanaged-api/metadata/metadata-interfaces.md)
- [IMetaDataImport2 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataimport2-interface.md)
