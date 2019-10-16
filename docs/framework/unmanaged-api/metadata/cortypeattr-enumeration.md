---
title: CorTypeAttr 열거형
ms.date: 03/30/2017
api_name:
- CorTypeAttr
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorTypeAttr
helpviewer_keywords:
- CorTypeAttr enumeration [.NET Framework metadata]
ms.assetid: 9bede0ec-5fdf-42a2-b5b7-bee64056acb6
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 5786f24f6543d4d262dd8a6389132aba02f9aacc
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67779205"
---
# <a name="cortypeattr-enumeration"></a>CorTypeAttr 열거형
형식 메타데이터를 나타내는 값을 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef enum CorTypeAttr {  
  
    tdVisibilityMask        =   0x00000007,  
    tdNotPublic             =   0x00000000,  
    tdPublic                =   0x00000001,  
    tdNestedPublic          =   0x00000002,  
    tdNestedPrivate         =   0x00000003,  
    tdNestedFamily          =   0x00000004,  
    tdNestedAssembly        =   0x00000005,  
    tdNestedFamANDAssem     =   0x00000006,  
    tdNestedFamORAssem      =   0x00000007,  
  
    tdLayoutMask            =   0x00000018,  
    tdAutoLayout            =   0x00000000,  
    tdSequentialLayout      =   0x00000008,  
    tdExplicitLayout        =   0x00000010,  
  
    tdClassSemanticsMask    =   0x00000020,  
    tdClass                 =   0x00000000,  
    tdInterface             =   0x00000020,  
  
    tdAbstract              =   0x00000080,  
    tdSealed                =   0x00000100,  
    tdSpecialName           =   0x00000400,  
  
    tdImport                =   0x00001000,  
    tdSerializable          =   0x00002000,  
    tdWindowsRuntime        =   0x00004000,  
  
    tdStringFormatMask      =   0x00030000,  
    tdAnsiClass             =   0x00000000,  
    tdUnicodeClass          =   0x00010000,  
    tdAutoClass             =   0x00020000,  
    tdCustomFormatClass     =   0x00030000,  
    tdCustomFormatMask      =   0x00C00000,  
  
    tdBeforeFieldInit       =   0x00100000,  
    tdForwarder             =   0x00200000,  
  
    tdReservedMask          =   0x00040800,  
    tdRTSpecialName         =   0x00000800,  
    tdHasSecurity           =   0x00040000,  
  
} CorTypeAttr;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|Description|  
|------------|-----------------|  
|`tdVisibilityMask`|형식 표시 유형 정보를 사용 합니다.|  
|`tdNotPublic`|형식을 공용 범위에 있지 않음을 지정 합니다.|  
|`tdPublic`|형식이 공용 범위에서를 지정 합니다.|  
|`tdNestedPublic`|형식을 공용 표시 유형으로 중첩 되도록 지정 합니다.|  
|`tdNestedPrivate`|개인 표시 유형으로 유형을 중첩 되도록 지정 합니다.|  
|`tdNestedFamily`|형식 패밀리 표시 유형으로 중첩 되도록 지정 합니다.|  
|`tdNestedAssembly`|형식 어셈블리 표시 유형이 있는 중첩 되도록 지정 합니다.|  
|`tdNestedFamANDAssem`|형식 패밀리 및 어셈블리 표시 유형으로 중첩 되도록 지정 합니다.|  
|`tdNestedFamORAssem`|형식 패밀리 또는 어셈블리 표시 유형으로 중첩 되도록 지정 합니다.|  
|`tdLayoutMask`|형식에 대 한 레이아웃 정보를 가져옵니다.|  
|`tdAutoLayout`|이 형식의 필드가 자동으로 배치 되도록 지정 합니다.|  
|`tdSequentialLayout`|이 형식의 필드가 순차적으로 배치 됩니다 지정 합니다.|  
|`tdExplicitLayout`|해당 필드 레이아웃을 명시적으로 제공 됨을 지정 합니다.|  
|`tdClassSemanticsMask`|유형에 대 한 의미 체계 정보를 가져옵니다.|  
|`tdClass`|형식을 클래스로 지정합니다.|  
|`tdInterface`|형식을 인터페이스로 지정합니다.|  
|`tdAbstract`|형식을 추상으로 지정합니다.|  
|`tdSealed`|형식을 확장할 수 없습니다 지정 합니다.|  
|`tdSpecialName`|특수 한 클래스 이름을 지정 합니다. 해당 이름에 설명 하는 방법입니다.|  
|`tdImport`|형식 가져왔는지 지정 합니다.|  
|`tdSerializable`|직렬화 가능 유형을 지정 합니다.|  
|`tdWindowsRuntime`|이 형식은 Windows 런타임 형식 인지를 지정 합니다.|  
|`tdStringFormatMask`|문자열은 인코딩 및 형식 지정 하는 방법에 대 한 정보를 가져옵니다.|  
|`tdAnsiClass`|이 형식은 LPTSTR ANSI로 해석 하는 것을 지정 합니다.|  
|`tdUnicodeClass`|이 형식은 LPTSTR 유니코드로 해석 하는 것을 지정 합니다.|  
|`tdAutoClass`|이 형식은 LPTSTR를 자동으로 해석 하는 것을 지정 합니다.|  
|`tdCustomFormatClass`|형식에는 비표준 인코딩을 지정 하 여 지정 된 대로 `CustomFormatMask`입니다.|  
|`tdCustomFormatMask`|이 마스크를 사용 하 여 네이티브 interop에 대 한 비표준 인코딩 정보를 가져옵니다. 이러한 두 비트 값의 의미는 지정 되지 않습니다.|  
|`tdBeforeFieldInit`|형식 정적 필드에 액세스 하는 첫 번째 하려고 하기 전에 초기화 해야를 지정 합니다.|  
|`tdForwarder`|형식을 내보낸 지정 및 형식 전달자입니다.|  
|`tdReservedMask`|이 플래그와 아래 플래그는 공용 언어 런타임에 의해 내부적으로 사용 됩니다.|  
|`tdRTSpecialName`|공용 언어 런타임에서 이름 인코딩을 확인 해야 지정 합니다.|  
|`tdHasSecurity`|연결 된 보안 형식을 갖도록 지정 합니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorHdr.h  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [메타데이터 열거형](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
