---
title: CorElementType 열거형
ms.date: 03/30/2017
api_name:
- CorElementType
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorElementType
helpviewer_keywords:
- CorElementType enumeration [.NET Framework metadata]
ms.assetid: c3809c8f-1737-4f0f-9442-0c01ee689871
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 6057bd48ff4fe3f852f82de2bab972d95fef138c
ms.sourcegitcommit: 9ee6cd851b6e176a5811ea28ed0d5935c71950f9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68868562"
---
# <a name="corelementtype-enumeration"></a>CorElementType 열거형

메타 데이터 형식 시그니처의 형식 <xref:System.Type>에 대 한 공용 언어 런타임, 형식 한정자 또는 정보를 지정 합니다.

## <a name="syntax"></a>구문

```cpp
typedef enum CorElementType {
    ELEMENT_TYPE_END            = 0x0,
    ELEMENT_TYPE_VOID           = 0x1,
    ELEMENT_TYPE_BOOLEAN        = 0x2,
    ELEMENT_TYPE_CHAR           = 0x3,
    ELEMENT_TYPE_I1             = 0x4,
    ELEMENT_TYPE_U1             = 0x5,
    ELEMENT_TYPE_I2             = 0x6,
    ELEMENT_TYPE_U2             = 0x7,
    ELEMENT_TYPE_I4             = 0x8,
    ELEMENT_TYPE_U4             = 0x9,
    ELEMENT_TYPE_I8             = 0xa,
    ELEMENT_TYPE_U8             = 0xb,
    ELEMENT_TYPE_R4             = 0xc,
    ELEMENT_TYPE_R8             = 0xd,
    ELEMENT_TYPE_STRING         = 0xe,

    ELEMENT_TYPE_PTR            = 0xf,
    ELEMENT_TYPE_BYREF          = 0x10,

    ELEMENT_TYPE_VALUETYPE      = 0x11,
    ELEMENT_TYPE_CLASS          = 0x12,
    ELEMENT_TYPE_VAR            = 0x13,
    ELEMENT_TYPE_ARRAY          = 0x14,
    ELEMENT_TYPE_GENERICINST    = 0x15,
    ELEMENT_TYPE_TYPEDBYREF     = 0x16,

    ELEMENT_TYPE_I              = 0x18,
    ELEMENT_TYPE_U              = 0x19,
    ELEMENT_TYPE_FNPTR          = 0x1B,
    ELEMENT_TYPE_OBJECT         = 0x1C,
    ELEMENT_TYPE_SZARRAY        = 0x1D,
    ELEMENT_TYPE_MVAR           = 0x1e,

    ELEMENT_TYPE_CMOD_REQD      = 0x1F,
    ELEMENT_TYPE_CMOD_OPT       = 0x20,

    ELEMENT_TYPE_INTERNAL       = 0x21,
    ELEMENT_TYPE_MAX            = 0x22,

    ELEMENT_TYPE_MODIFIER       = 0x40,
    ELEMENT_TYPE_SENTINEL       = 0x01 | ELEMENT_TYPE_MODIFIER,
    ELEMENT_TYPE_PINNED         = 0x05 | ELEMENT_TYPE_MODIFIER

} CorElementType;
```

## <a name="members"></a>멤버

|멤버|설명|
|------------|-----------------|
|`ELEMENT_TYPE_END`|내부적으로 사용됩니다.|
|`ELEMENT_TYPE_VOID`|Void 형식입니다.|
|`ELEMENT_TYPE_BOOLEAN`|부울 형식|
|`ELEMENT_TYPE_CHAR`|문자 형식입니다.|
|`ELEMENT_TYPE_I1`|부호 있는 1 바이트 정수입니다.|
|`ELEMENT_TYPE_U1`|부호 없는 1바이트 정수입니다.|
|`ELEMENT_TYPE_I2`|부호 있는 2 바이트 정수입니다.|
|`ELEMENT_TYPE_U2`|부호 없는 2 바이트 정수입니다.|
|`ELEMENT_TYPE_I4`|부호 있는 4 바이트 정수입니다.|
|`ELEMENT_TYPE_U4`|부호 없는 4 바이트 정수입니다.|
|`ELEMENT_TYPE_I8`|부호 있는 8 바이트 정수입니다.|
|`ELEMENT_TYPE_U8`|부호 없는 8 바이트 정수입니다.|
|`ELEMENT_TYPE_R4`|4 바이트 부동 소수점입니다.|
|`ELEMENT_TYPE_R8`|8 바이트 부동 소수점입니다.|
|`ELEMENT_TYPE_STRING`|System.string 형식입니다.|
|`ELEMENT_TYPE_PTR`|포인터 형식 한정자입니다.|
|`ELEMENT_TYPE_BYREF`|참조 형식 한정자입니다.|
|`ELEMENT_TYPE_VALUETYPE`|값 형식 한정자입니다.|
|`ELEMENT_TYPE_CLASS`|클래스 형식 한정자입니다.|
|`ELEMENT_TYPE_VAR`|클래스 변수 형식 한정자입니다.|
|`ELEMENT_TYPE_ARRAY`|다차원 배열 형식 한정자입니다.|
|`ELEMENT_TYPE_GENERICINST`|제네릭 형식에 대 한 형식 한정자입니다.|
|`ELEMENT_TYPE_TYPEDBYREF`|형식화된 참조입니다.|
|`ELEMENT_TYPE_I`|네이티브 정수의 크기입니다.|
|`ELEMENT_TYPE_U`|부호 없는 네이티브 정수의 크기입니다.|
|`ELEMENT_TYPE_FNPTR`|함수에 대 한 포인터입니다.|
|`ELEMENT_TYPE_OBJECT`|System.object 형식입니다.|
|`ELEMENT_TYPE_SZARRAY`|0이 아닌 1 차원 배열 형식 한정자입니다.|
|`ELEMENT_TYPE_MVAR`|메서드 변수 형식 한정자입니다.|
|`ELEMENT_TYPE_CMOD_REQD`|C 언어 필수 한정자입니다.|
|`ELEMENT_TYPE_CMOD_OPT`|C 언어 선택적 한정자입니다.|
|`ELEMENT_TYPE_INTERNAL`|내부적으로 사용됩니다.|
|`ELEMENT_TYPE_MAX`|잘못된 형식입니다.|
|`ELEMENT_TYPE_MODIFIER`|내부적으로 사용됩니다.|
|`ELEMENT_TYPE_SENTINEL`|변수 수의 변수 목록에 대 한 센티널 인 형식 한정자입니다.|
|`ELEMENT_TYPE_PINNED`|내부적으로 사용됩니다.|

## <a name="remarks"></a>설명

형식 한정자는 보다 복잡 한 형식을 나타내는 기본을 형성 합니다. `CorElementType` 형식 한정자 값은 형식 시그니처에서 바로 다음에 오는 값에 적용 됩니다. 다음 표에 지정 된 것 `CorElementType` 처럼 형식 한정자 값 다음에 `CorElementType` 오는 값은 단순 형식 값, 메타 데이터 토큰 또는 다른 값일 수 있습니다.

> [!NOTE]
> 모든 숫자 (*숫자*, *인수 개수*, *메타 데이터 토큰*, *순위*, *개수*및 *바운드*)는 압축 된 정수로 저장 됩니다. 자세한 내용은 ECMA 웹 사이트의 [표준 ECMA-335-CLI (공용 언어 인프라)](https://go.microsoft.com/fwlink/?LinkID=116487) 를 참조 하세요.

|형식 한정자|형식|
|-------------------|------------|
|`ELEMENT_TYPE_PTR`|ELEMENT_TYPE_PTR \<값> `CorElementType`|
|`ELEMENT_TYPE_BYREF`|ELEMENT_TYPE_BYREF \<값> `CorElementType`|
|`ELEMENT_TYPE_VALUETYPE`|메타 \<데이터 `mdTypeDef` 토큰을 ELEMENT_TYPE_VALUETYPE >|
|`ELEMENT_TYPE_CLASS`|메타 \<데이터 `mdTypeDef` 토큰을 ELEMENT_TYPE_CLASS >|
|`ELEMENT_TYPE_VAR`|ELEMENT_TYPE_VAR \<number >|
|`ELEMENT_TYPE_ARRAY`|ELEMENT_TYPE_ARRAY \< \<> `CorElementType` count1>\<> 순위 값을 bound1 > ... \< countn > \<boundN> \<|
|`ELEMENT_TYPE_GENERICINST`|ELEMENT_TYPE_GENERICINST \<> `mdTypeDef` \<arg1 >>메타데이터토큰을계산하는동안...\< \<argn >|
|`ELEMENT_TYPE_FNPTR`|호출 \<규칙을 포함 하 여 함수에 대 한 전체 시그니처를 ELEMENT_TYPE_FNPTR >|
|`ELEMENT_TYPE_SZARRAY`|ELEMENT_TYPE_SZARRAY \<값> `CorElementType`|
|`ELEMENT_TYPE_MVAR`|ELEMENT_TYPE_MVAR \<number >|
|`ELEMENT_TYPE_CMOD_REQD`|ELEMENT_TYPE_\<또는 메타`mdTypeDef` 데이터 토큰 `mdTypeRef` >|
|`ELEMENT_TYPE_CMOD_OPT`|E_T_CMOD_OPT \<또는 메타`mdTypeDef` 데이터 토큰 `mdTypeRef` >|

## <a name="requirements"></a>요구 사항

**플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.

**헤더:** CorHdr.h

**.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]

## <a name="see-also"></a>참고자료

- [메타데이터 열거형](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
