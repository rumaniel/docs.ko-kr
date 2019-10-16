---
title: CorNativeType 열거형
ms.date: 03/30/2017
api_name:
- CorNativeType
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorNativeType
helpviewer_keywords:
- CorNativeType enumeration [.NET Framework metadata]
ms.assetid: e47a72f1-9609-48ed-bb34-97170d7f6890
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 846c754aeb0a710fa70e906e666f694eaa77c576
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67781706"
---
# <a name="cornativetype-enumeration"></a>CorNativeType 열거형
관리되지 않는 네이티브 형식을 설명하는 값을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef enum CorNativeType {  
  
    NATIVE_TYPE_END                  = 0x0,  
    NATIVE_TYPE_VOID                 = 0x1,  
    NATIVE_TYPE_BOOLEAN              = 0x2,  
    NATIVE_TYPE_I1                   = 0x3,  
    NATIVE_TYPE_U1                   = 0x4,  
    NATIVE_TYPE_I2                   = 0x5,  
    NATIVE_TYPE_U2                   = 0x6,  
    NATIVE_TYPE_I4                   = 0x7,  
    NATIVE_TYPE_U4                   = 0x8,  
    NATIVE_TYPE_I8                   = 0x9,  
    NATIVE_TYPE_U8                   = 0xa,  
    NATIVE_TYPE_R4                   = 0xb,  
    NATIVE_TYPE_R8                   = 0xc,  
    NATIVE_TYPE_SYSCHAR              = 0xd,  
    NATIVE_TYPE_VARIANT              = 0xe,  
    NATIVE_TYPE_CURRENCY             = 0xf,  
    NATIVE_TYPE_PTR                  = 0x10,  
  
    NATIVE_TYPE_DECIMAL              = 0x11,  
    NATIVE_TYPE_DATE                 = 0x12,  
    NATIVE_TYPE_BSTR                 = 0x13,  
    NATIVE_TYPE_LPSTR                = 0x14,  
    NATIVE_TYPE_LPWSTR               = 0x15,  
    NATIVE_TYPE_LPTSTR               = 0x16,  
    NATIVE_TYPE_FIXEDSYSSTRING       = 0x17,  
    NATIVE_TYPE_OBJECTREF            = 0x18,  
    NATIVE_TYPE_IUNKNOWN             = 0x19,  
    NATIVE_TYPE_IDISPATCH            = 0x1a,  
    NATIVE_TYPE_STRUCT               = 0x1b,  
    NATIVE_TYPE_INTF                 = 0x1c,  
    NATIVE_TYPE_SAFEARRAY            = 0x1d,  
    NATIVE_TYPE_FIXEDARRAY           = 0x1e,  
    NATIVE_TYPE_INT                  = 0x1f,  
    NATIVE_TYPE_UINT                 = 0x20,  
  
    NATIVE_TYPE_NESTEDSTRUCT         = 0x21,  
    NATIVE_TYPE_BYVALSTR             = 0x22,  
    NATIVE_TYPE_ANSIBSTR             = 0x23,  
    NATIVE_TYPE_TBSTR                = 0x24,  
    NATIVE_TYPE_VARIANTBOOL          = 0x25,  
    NATIVE_TYPE_FUNC                 = 0x26,  
  
    NATIVE_TYPE_ASANY                = 0x28,  
    NATIVE_TYPE_ARRAY                = 0x2a,  
    NATIVE_TYPE_LPSTRUCT             = 0x2b,  
    NATIVE_TYPE_CUSTOMMARSHALER      = 0x2c,  
    NATIVE_TYPE_IINSPECTABLE         = 0x2e,  
    NATIVE_TYPE_HSTRING              = 0x2f,  
  
    NATIVE_TYPE_ERROR                = 0x2d,   
  
    NATIVE_TYPE_MAX                  = 0x50  
  
} CorNativeType;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|Description|  
|------------|-----------------|  
|`NATIVE_TYPE_END`|더 이상 사용되지 않습니다.|  
|`NATIVE_TYPE_VOID`|더 이상 사용되지 않습니다.|  
|`NATIVE_TYPE_BOOLEAN`|4 바이트 부울 값 TRUE은 0이 아닌 값이 고 FALSE는 0입니다.|  
|`NATIVE_TYPE_I1`|부호 있는 8 비트 정수 값입니다.|  
|`NATIVE_TYPE_U1`|부호 없는 8 비트 정수 값입니다.|  
|`NATIVE_TYPE_I2`|부호 있는 16 비트 정수 값입니다.|  
|`NATIVE_TYPE_U2`|부호 없는 16 비트 정수 값입니다.|  
|`NATIVE_TYPE_I4`|부호 있는 32비트 정수 값입니다.|  
|`NATIVE_TYPE_U4`|부호 없는 32비트 정수 값입니다.|  
|`NATIVE_TYPE_I8`|부호 있는 64 비트 정수 값입니다.|  
|`NATIVE_TYPE_U8`|부호 없는 64 비트 정수 값입니다.|  
|`NATIVE_TYPE_R4`|4 바이트 부동 소수점 숫자 값입니다.|  
|`NATIVE_TYPE_R8`|8 바이트 부동 소수점 숫자 값입니다.|  
|`NATIVE_TYPE_SYSCHAR`|더 이상 사용되지 않습니다.|  
|`NATIVE_TYPE_VARIANT`|더 이상 사용되지 않습니다.|  
|`NATIVE_TYPE_CURRENCY`|관리 되는에 해당 하는 COM 형식 숫자 <xref:System.Decimal> 형식입니다.|  
|`NATIVE_TYPE_PTR`|더 이상 사용되지 않습니다.|  
|`NATIVE_TYPE_DECIMAL`|더 이상 사용되지 않습니다.|  
|`NATIVE_TYPE_DATE`|더 이상 사용되지 않습니다.|  
|`NATIVE_TYPE_BSTR`|COM Interop|  
|`NATIVE_TYPE_LPSTR`|LPSTR는 문자열 값입니다.|  
|`NATIVE_TYPE_LPWSTR`|LPWSTR 문자열 값입니다.|  
|`NATIVE_TYPE_LPTSTR`|LPTSTR 문자열 값입니다.|  
|`NATIVE_TYPE_FIXEDSYSSTRING`|고정, 시스템에 정의 된 문자열 값입니다.|  
|`NATIVE_TYPE_OBJECTREF`|더 이상 사용되지 않습니다.|  
|`NATIVE_TYPE_IUNKNOWN`|COM Interop|  
|`NATIVE_TYPE_IDISPATCH`|COM Interop|  
|`NATIVE_TYPE_STRUCT`|네이티브 구조체 값입니다.|  
|`NATIVE_TYPE_INTF`|COM Interop|  
|`NATIVE_TYPE_SAFEARRAY`|COM Interop|  
|`NATIVE_TYPE_FIXEDARRAY`|고정 길이 배열 값입니다.|  
|`NATIVE_TYPE_INT`|네이티브 16 비트 부호 있는 정수 값입니다.|  
|`NATIVE_TYPE_UINT`|네이티브 16 비트 부호 없는 정수 값입니다.|  
|`NATIVE_TYPE_NESTEDSTRUCT`|더 이상 사용되지 않습니다.<br /><br /> NATIVE_TYPE_STRUCT를 사용 합니다.|  
|`NATIVE_TYPE_BYVALSTR`|COM Interop|  
|`NATIVE_TYPE_ANSIBSTR`|COM Interop|  
|`NATIVE_TYPE_TBSTR`|COM Interop<br /><br /> BSTR 또는 ANSIBSTR 플랫폼에 따라 선택 합니다.|  
|`NATIVE_TYPE_VARIANTBOOL`|2 바이트 부울 값, 여기서 TRUE가-1이 고 FALSE는 0입니다.|  
|`NATIVE_TYPE_FUNC`|함수 포인터입니다.|  
|`NATIVE_TYPE_ASANY`|네이티브 형식에 대 한 참조입니다.|  
|`NATIVE_TYPE_ARRAY`|알 수 없는 형식의 멤버를 사용 하 여 배열에 대 한 참조입니다.|  
|`NATIVE_TYPE_LPSTRUCT`|구조에 32 비트 정수 포인터입니다.|  
|`NATIVE_TYPE_CUSTOMMARSHALER`|사용자 지정 마샬러에 기본 형식입니다.<br /><br /> 다음 형식의 문자열 따라야 합니다. "기본 형식 이름/0 사용자 지정 마샬러는 이름/0 선택적 쿠키/0를 입력 하는 데 사용" 또는 "{네이티브 종류 GUID} / 0 사용자 지정 마샬러 유형 이름/0 선택적 쿠키/0"|  
|`NATIVE_TYPE_ERROR`|COM Interop<br /><br /> 이 형식은 ELEMENT_TYPE_I4를 사용 하 여 VT_HRESULT 매핑됩니다.|  
|`NATIVE_TYPE_IINSPECTABLE`|네이티브 `IInspectable` 형식입니다.|  
|`NATIVE_TYPE_HSTRING`|네이티브 `HString`합니다.|  
|`NATIVE_TYPE_MAX`|잘못 된 값입니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorHdr.h  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- <xref:System.Runtime.InteropServices.UnmanagedType>
- [메타데이터 열거형](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
