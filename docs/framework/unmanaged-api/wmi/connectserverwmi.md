---
title: ConnectServerWmi 함수 (관리 되지 않는 API 참조)
description: ConnectServerWmi 함수는 DCOM을 사용 하 여 WMI 네임 스페이스에 대 한 연결을 만듭니다.
ms.date: 11/06/2017
api_name:
- ConnectServerWmi
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- ConnectServerWmi
helpviewer_keywords:
- ConnectServerWmi function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2ebb268dcee877f4e9aea0c88852333897030dd1
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798744"
---
# <a name="connectserverwmi-function"></a>ConnectServerWmi 함수

DCOM 통해 지정된 컴퓨터의 WMI 네임스페이스에 대한 연결을 만듭니다.

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>구문

```cpp
HRESULT ConnectServerWmi (
   [in] BSTR               strNetworkResource,
   [in] BSTR               strUser,
   [in] BSTR               strPassword,
   [in] BSTR               strLocale,
   [in] long               lSecurityFlags,
   [in] BSTR               strAuthority,
   [in] IWbemContext*      pCtx,
   [out] IWbemServices**   ppNamespace,
   [in] DWORD              impLevel,
   [in] DWORD              authLevel
);
```

## <a name="parameters"></a>매개 변수

`strNetworkResource`\
진행 올바른 WMI 네임 스페이스 `BSTR` 의 개체 경로를 포함 하는 유효한에 대 한 포인터입니다. 자세한 내용은 [설명](#remarks) 부분을 참조 하세요.

`strUser`\
진행 사용자 이름이 포함 된 유효한 `BSTR` 에 대 한 포인터입니다. 현재 보안 컨텍스트를 나타내는 값입니다.`null` 사용자가 현재 사용자와 다른 도메인에 있는 경우에 `strUser` 는 도메인 및 사용자 이름을 백슬래시로 구분 하 여 포함할 수도 있습니다. `strUser`는와 `userName@domainName`같은 UPN (사용자 계정 이름) 형식으로도 될 수 있습니다. 자세한 내용은 [설명](#remarks) 부분을 참조 하세요.

`strPassword`\
진행 암호가 포함 된 유효한 `BSTR` 에 대 한 포인터입니다. 는 `null` 현재 보안 컨텍스트를 나타냅니다. 빈 문자열 ("")은 길이가 0 인 유효한 암호를 나타냅니다.

`strLocale`\
진행 정보 검색의 올바른 로캘을 `BSTR` 나타내는 유효한에 대 한 포인터입니다. Microsoft 로캘 식별자의 경우 문자열의 형식은 "MS\_*xxx*"입니다. 여기서 *xxx* 는 LCID (로캘 id)를 나타내는 16 진수 형식의 문자열입니다. 잘못 된 로캘이 지정 된 경우 메서드는 Windows 7 `WBEM_E_INVALID_PARAMETER` 을 제외 하 고를 반환 합니다 .이 경우 서버 기본 로캘이 대신 사용 됩니다. ' Null1 ' 이면 현재 로캘이 사용 됩니다.

`lSecurityFlags`\
진행 `ConnectServerWmi` 메서드에 전달할 플래그입니다. 이 매개 변수의 값이 0 이면 서버에 대 한 연결이 설정 된 후 `ConnectServerWmi` 에만를 반환 합니다. 이로 인해 서버가 중단 되 면 응용 프로그램이 무기한 응답 하지 않을 수 있습니다. 다른 유효한 값은 다음과 같습니다.

| 상수  | 값  | 설명  |
|---------|---------|---------|
| `CONNECT_REPOSITORY_ONLY` | 0x40 | 내부용으로 예약됩니다. 사용하지 마십시오. |
| `WBEM_FLAG_CONNECT_USE_MAX_WAIT` | 0x80 | `ConnectServerWmi`2 분 이내에 반환 합니다. |

`strAuthority`\
진행 사용자의 도메인 이름입니다. 다음 값을 가질 수 있습니다.

| 값 | 설명 |
|---------|---------|
| 비어 있음 | NTLM 인증을 사용 하 고 현재 사용자의 NTLM 도메인을 사용 합니다. 에서 `strUser` 도메인을 지정 하는 경우 (권장 위치) 여기에서 지정 하면 안 됩니다. 이 함수는 `WBEM_E_INVALID_PARAMETER` 두 매개 변수 모두에 도메인을 지정 하는 경우를 반환 합니다. |
| Kerberos:*보안 주체 이름* | Kerberos 인증을 사용 하며,이 매개 변수에는 Kerberos 사용자 이름이 포함 됩니다. |
| NTLMDOMAIN:*도메인 이름* | NT LAN Manager 인증을 사용 하며이 매개 변수에는 NTLM 도메인 이름이 포함 됩니다. |

`pCtx`\
진행 일반적으로이 매개 변수 `null`는입니다. 그렇지 않으면 하나 이상의 동적 클래스 공급자가 필요로 하는 [iwbemcontext 개체가 올바르지](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemcontext) 개체에 대 한 포인터입니다.

`ppNamespace`\
제한이 함수가 반환 될 때 지정 된 네임 스페이스에 바인딩된 [IWbemServices](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemservices) 개체에 대 한 포인터를 수신 합니다. 오류가 있는 경우를 `null` 가리키도록 설정 됩니다.

`impLevel`\
진행 가장 수준입니다.

`authLevel`\
진행 권한 수준입니다.

## <a name="return-value"></a>반환 값

이 함수에서 반환 되는 다음 값은 *WbemCli* 헤더 파일에 정의 되어 있거나 코드에서 상수로 정의할 수 있습니다.

|상수  |값  |Description  |
|---------|---------|---------|
| `WBEM_E_FAILED` | 0x80041001 | 일반 오류가 발생 했습니다. |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | 매개 변수가 잘못 되었습니다. |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 메모리가 부족 하 여 작업을 완료할 수 없습니다. |
| `WBEM_S_NO_ERROR` | 0 | 함수 호출에 성공 했습니다.  |

## <a name="remarks"></a>설명

이 함수는 [IWbemLocator:: ConnectServer](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemlocator-connectserver) 메서드에 대 한 호출을 래핑합니다.

기본 네임 스페이스 `strNetworkResource` 에 대 한 로컬 액세스의 경우는 간단한 개체 경로 ("root\default" 또는 "\\.\root\default") 일 수 있습니다. COM 또는 Microsoft 호환 네트워킹을 사용 하는 원격 컴퓨터의 기본 네임 스페이스에 액세스 하려면 컴퓨터 이름 "\\myserver\root\default"를 포함 합니다. 컴퓨터 이름은 DNS 이름 또는 IP 주소일 수도 있습니다. 이 `ConnectServerWmi` 함수는 ipv6 주소를 사용 하 여 i p v 6을 실행 하는 컴퓨터에 연결할 수도 있습니다.

`strUser`는 빈 문자열일 수 없습니다. 에서 `strAuthority`지정 된 도메인은에 `strUser`포함 되지 않아야 합니다. 그렇지 않으면 함수가를 반환 `WBEM_E_INVALID_PARAMETER`합니다.

## <a name="requirements"></a>요구 사항

 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.

 **헤더:** WMINet_Utils.idl

 **.NET Framework 버전:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>참고자료

- [WMI 및 성능 카운터 (관리 되지 않는 API 참조)](index.md)
