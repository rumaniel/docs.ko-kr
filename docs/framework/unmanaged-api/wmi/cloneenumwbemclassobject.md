---
title: CloneEnumWbemClassObject 함수 (관리 되지 않는 API 참조)
description: CloneEnumWbemClassObject 함수는 열거자의 논리적 복사본을 만듭니다.
ms.date: 11/06/2017
api_name:
- CloneEnumWbemClassObject
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- CloneEnumWbemClassObject
helpviewer_keywords:
- CloneEnumWbemClassObject function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1605314f94fd82d2a2cd7be105dde9e273f607bc
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798703"
---
# <a name="cloneenumwbemclassobject-function"></a>CloneEnumWbemClassObject 함수
열거형의 현재 위치를 유지하면서 열거자의 논리적 복사본을 만듭니다.

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>구문

```cpp
HRESULT CloneEnumWbemClassObject (
   [out] IEnumWbemClassObject**  ppEnum, 
   [in] DWORD                    authLevel,
   [in] DWORD                    impLevel,
   [in] IEnumWbemClassObject*    pCurrentEnumWbemClassObject, 
   [in] BSTR                     strUser,
   [in] BSTR                     strPassword,
   [in BSTR]                     strAuthority 
); 
```

## <a name="parameters"></a>매개 변수

`ppEnum`\
제한이 새 [IEnumWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-ienumwbemclassobject)에 대 한 포인터를 받습니다.

`authLevel`\
진행 권한 수준입니다.

`impLevel`\
진행 가장 수준입니다.

`pCurrentEnumWbemClassObject`\
제한이 복제할 [IEnumWbemClassObject](/windows/desktop/api/wbemcli/nn-wbemcli-ienumwbemclassobject) 인스턴스에 대 한 포인터입니다.

`strUser`\
진행 사용자 이름입니다. 자세한 내용은 [Connectserverwmi](connectserverwmi.md) 함수를 참조 하세요.

`strPassword`\
진행 암호입니다. 자세한 내용은 [Connectserverwmi](connectserverwmi.md) 함수를 참조 하세요.

`strAuthority`\ [in] 사용자의 도메인 이름입니다. 자세한 내용은 [Connectserverwmi](connectserverwmi.md) 함수를 참조 하세요.

## <a name="return-value"></a>반환 값

이 함수에서 반환 되는 다음 값은 *WbemCli* 헤더 파일에 정의 되어 있거나 코드에서 상수로 정의할 수 있습니다.

|상수  |값  |설명  |
|---------|---------|---------|
| `WBEM_E_FAILED` | 0x80041001 | 일반 오류가 발생 했습니다. |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | 매개 변수가 잘못 되었습니다. |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 사용 가능한 메모리가 부족 하 여 작업을 완료할 수 없습니다. |
| `WBEM_E_TRANSPORT_FAILURE` | 0x80041015 | 현재 프로세스와 WMI 간의 RPC (원격 프로시저 호출) 링크에 오류가 발생 했습니다. |
| `WBEM_S_NO_ERROR` | 0 | 함수 호출에 성공 했습니다.  |

## <a name="remarks"></a>설명

이 함수는 [IEnumWbemClassObject:: Clone](/windows/desktop/api/wbemcli/nf-wbemcli-ienumwbemclassobject-clone) 메서드에 대 한 호출을 래핑합니다.

이 메서드는 "최상의" 복사만 수행 합니다. 많은 CIM 개체의 동적 특성으로 인해 새 열거자가 원본 열거자와 동일한 개체 집합을 열거 하지 못할 수 있습니다.

함수 호출이 실패 하면 [Geterrorinfo](geterrorinfo.md) 함수를 호출 하 여 추가 오류 정보를 얻을 수 있습니다.

## <a name="example"></a>예제

예제를 보려면 [IEnumWbemClassObject:: Clone](/windows/desktop/api/wbemcli/nf-wbemcli-ienumwbemclassobject-clone) 메서드를 참조 하세요.

## <a name="requirements"></a>요구 사항
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.

 **헤더:** WMINet_Utils.idl

 **.NET Framework 버전:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>참고자료

- [WMI 및 성능 카운터 (관리 되지 않는 API 참조)](index.md)
