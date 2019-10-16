---
title: COR_GC_REFERENCE 구조체
ms.date: 03/30/2017
api_name:
- COR_GC_REFERENCE
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- COR_GC_REFERENCE
helpviewer_keywords:
- COR_GC_REFERENCE structure [.NET Framework debugging]
ms.assetid: 162e8179-0cd4-4110-8f06-5f387698bd62
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: cc0b67621f77c0741e0b63b84ab1794530d6280b
ms.sourcegitcommit: 3caa92cb97e9f6c31f21769c7a3f7c4304024b39
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2019
ms.locfileid: "71274231"
---
# <a name="cor_gc_reference-structure"></a>COR_GC_REFERENCE 구조체
가비지 수집할 개체에 대한 정보를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef struct _COR_GC_REFERENCE {  
    ICorDebugAppDomain *domain;   
    ICorDebugValue *location;  
    CorGCReferenceType type;  
    UINT64 extraData;  
} COR_GC_REFERENCE;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|설명|  
|------------|-----------------|  
|`domain`|핸들이 나 개체가 속한 응용 프로그램 도메인에 대 한 포인터입니다. 값은 일 `null`수 있습니다.|  
|`location`|가비지 수집 될 개체에 해당 하는 ICorDebugValue 또는 ICorDebugReferenceValue 인터페이스입니다.|  
|`type`|루트의 출처를 나타내는 [CorGCReferenceType](corgcreferencetype-enumeration.md) 열거형 값입니다. 자세한 내용은 설명 섹션을 참조하세요.|  
|`extraData`|가비지 수집 될 개체에 대 한 추가 데이터입니다. 이 정보는 `type` 필드에 표시 되는 개체의 원본에 따라 달라 집니다. 자세한 내용은 설명 섹션을 참조하세요.|  
  
## <a name="remarks"></a>설명  
 `type` 필드는 참조의 출처를 나타내는 [CorGCReferenceType](corgcreferencetype-enumeration.md) 열거형 값입니다. 특정 `COR_GC_REFERENCE` 값은 다음과 같은 종류의 관리 되는 개체를 반영할 수 있습니다.  
  
- 모든 관리 되는 스택 (`CorGCReferenceType.CorReferenceStack`)의 개체입니다. 여기에는 공용 언어 런타임에서 만든 개체 뿐만 아니라 관리 코드의 라이브 참조도 포함 됩니다.  
  
- 핸들 테이블 (`CorGCReferenceType.CorHandle*`)의 개체입니다. 여기에는 모듈의`HNDTYPE_STRONG` 강력한 `HNDTYPE_REFCOUNT`참조 (및) 및 정적 변수가 포함 됩니다.  
  
- 종료자 큐 (`CorGCReferenceType.CorReferenceFinalizer`)의 개체입니다. 종료자는 종료 자가 실행 될 때까지 개체를 큐에 대기 합니다.  
  
 필드 `extraData` 에는 참조의 원본 (또는 형식)에 따라 추가 데이터가 포함 됩니다. 가능한 값은 다음과 같습니다.  
  
- `DependentSource`. 가 이면이 필드는 활성 상태인 경우에서 `COR_GC_REFERENCE.Location`가비지 수집 될 개체의 루트를 나타내는 개체입니다. `CorGCREferenceType.CorHandleStrongDependent` `type`  
  
- `RefCount`. `type` 가`CorGCREferenceType.CorHandleStrongRefCount`이면이 필드는 핸들의 참조 수입니다.  
  
- `Size`. `type` 이 인 `CorGCREferenceType.CorHandleStrongSizedByref`경우이 필드는 가비지 수집기가 개체 루트를 계산 하는 개체 트리의 마지막 크기입니다. 이 계산은 반드시 최신 상태를 유지 해야 하는 것은 아닙니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>참고 항목

- [디버깅 구조체](debugging-structures.md)
- [디버깅](index.md)
