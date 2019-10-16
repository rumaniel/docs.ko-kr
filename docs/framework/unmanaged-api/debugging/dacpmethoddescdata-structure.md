---
title: DacpMethodDescData 구조체
ms.date: 02/01/2019
api.name:
- DacpMethodDescData Structure
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- DacpMethodDescData Structure
helpviewer.keywords:
- DacpMethodDescData Structure [.NET Framework debugging]
topic_type:
- apiref
author: hoyosjs
ms.author: juhoyosa
ms.openlocfilehash: 97079b824dbd0e056374af4173e49304babd6c32
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67739140"
---
# <a name="dacpmethoddescdata-structure"></a>DacpMethodDescData 구조체

메서드의 런타임 정보에 대 한 전송 버퍼를 정의합니다.

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="syntax"></a>구문

```cpp
struct DacpMethodDescData
{
    int             bHasNativeCode;
    int             bIsDynamic;
    unsigned short  wSlotNumber;
    CLRDATA_ADDRESS NativeCodeAddr;
    CLRDATA_ADDRESS data;
    CLRDATA_ADDRESS MethodDescPtr;
    CLRDATA_ADDRESS nativeCodeInfo;
    CLRDATA_ADDRESS moduleInfo;
    mdToken         MDToken;
    CLRDATA_ADDRESS payloadGC;
    CLRDATA_ADDRESS payloadGC2;
    CLRDATA_ADDRESS managedDynamicMethodObject;
    CLRDATA_ADDRESS requestedIP;
    DacpReJitData   rejitDataCurrent;
    DacpReJitData   rejitDataRequested;
    unsigned long   cJittedRejitVersions;
};
```

## <a name="members"></a>멤버

| 멤버                       | 설명                                                                                     |
| ---------------------------- | ----------------------------------------------------------------------------------------------- |
| `bHasNativeCode`             | 런타임은 메서드의 지정된 인스턴스화에 대 한 사용 가능한 네이티브 코드에 있는지를 나타냅니다. |
| `bIsDynamic`                 | 경량 코드 생성을 통해 메서드를 동적으로 생성 하는 경우를 나타냅니다.           |
| `wSlotNumber`                | 메서드의 메서드 테이블의 슬롯 번호.                                                   |
| `NativeCodeAddr`             | 메서드의 초기 기본 주소입니다.                                                            |
| `data`                       | 런타임에서 내부적으로 사용 하는 버퍼에 대 한 포인터입니다.                                             |
| `MethodDescPtr`              | 에 대 한 포인터를 `MethodDesc` 런타임에서입니다.                                                     |
| `nativeCodeInfo`             | 메서드를 추적 하는 런타임에서 내부적으로 사용 되는 버퍼에 대 한 포인터입니다.                            |
| `moduleInfo`                 | 모듈 정보에 대 한 런타임에 의해 내부적으로 사용 되는 버퍼에 대 한 포인터입니다.                      |
| `MDToken`                    | 지정된 된 메서드를 사용 하 여 연결 된 토큰입니다.                                                         |
| `payloadGC`                  | 런타임에서 내부적으로 사용 하는 가비지 컬렉션 버퍼에 대 한 포인터입니다.                          |
| `payloadGC2`                 | 런타임에서 내부적으로 사용 하는 가비지 컬렉션 버퍼에 대 한 포인터입니다.                          |
| `managedDynamicMethodObject` | 메서드가 동적 이면 런타임에서이 버퍼 내부적으로 사용 정보 추적에 대 한 합니다.     |
| `requestedIP`                | 네이티브 코드 주소를 지정 하는 경우 요청당 구조를 채우는 데 사용 합니다.                    |
| `rejitDataCurrent`           | 계측 된 메서드는 최신 버전에 대 한 정보입니다.                                   |
| `rejitDataRequested`         | 요청된 된 기본 주소에 대 한 Rejit 정보입니다.                                             |
| `cJittedRejitVersions`       | 메서드는 계측을 통해 rejitted 된 횟수입니다.                           |

## <a name="remarks"></a>설명

이 구조는 런타임 내에서 있으며 모든 헤더 또는 라이브러리 파일을 통해 노출 되지 않습니다. 를 사용 하려면 위에서 지정한 대로 구조를 정의 합니다.

## <a name="requirements"></a>요구 사항
**플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
**헤더:** 없음  
**라이브러리:** 없음  
**.NET Framework 버전:** [!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  

## <a name="see-also"></a>참고자료

- [디버깅](../../../../docs/framework/unmanaged-api/debugging/index.md)
- [디버깅 구조체](../../../../docs/framework/unmanaged-api/debugging/debugging-structures.md)
- [공통 데이터 형식](../../../../docs/framework/unmanaged-api/common-data-types-unmanaged-api-reference.md)
