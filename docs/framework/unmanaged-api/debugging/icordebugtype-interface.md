---
title: ICorDebugType 인터페이스
ms.date: 03/30/2017
api_name:
- ICorDebugType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugType
helpviewer_keywords:
- ICorDebugType interface [.NET Framework debugging]
ms.assetid: 94e02e31-67ea-4b00-8148-a46740a4571d
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b830af5d59c0eb177d815451ecedbdc14121aaad
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69964755"
---
# <a name="icordebugtype-interface"></a>ICorDebugType 인터페이스
기본 또는 복합 형식 (즉, 사용자 정의)을 나타냅니다. 형식이 제네릭이면 `ICorDebugType`는 인스턴스화된 제네릭 형식을 나타냅니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|Description|  
|------------|-----------------|  
|[EnumerateTypeParameters 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugtype-enumeratetypeparameters-method.md)|<xref:System.Type> 이`ICorDebugType`에서 참조 하는 클래스의 제네릭 매개 변수를 참조 하는 ICorDebugTypeEnum에 대 한 인터페이스 포인터를 가져옵니다.|  
|[GetBase 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugtype-getbase-method.md)|`ICorDebugType` 이`ICorDebugType`가 참조 하는 클래스의 기본 클래스 (있는 경우)를 참조 하는에 대 한 인터페이스 포인터를 가져옵니다.|  
|[GetClass 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugtype-getclass-method.md)|이 `ICorDebugType`의 형식화 된 생성자를 참조 하는 ICorDebugClass에 대 한 인터페이스 포인터를 가져옵니다.|  
|[GetFirstTypeParameter 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugtype-getfirsttypeparameter-method.md)|이 <xref:System.Type> `ICorDebugType` 에서참조하는클래스의생성자에대한첫번째제네릭매개변수를참조하는에대한인터페이스포인터를가져옵니다.`ICorDebugType`|  
|[GetRank 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugtype-getrank-method.md)|배열 형식의 차원 수를 가져옵니다.|  
|[GetStaticFieldValue 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugtype-getstaticfieldvalue-method.md)|지정 된 스택 프레임에서 지정 된 필드 토큰이 참조 하는 정적 필드의 값을 포함 하는 ICorDebugValue에 대 한 인터페이스 포인터를 가져옵니다.|  
|[GetType 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugtype-gettype-method.md)|<xref:System.Type> 이`ICorDebugType`에서 참조 하는 공용 언어 런타임의 네이티브 형식을 설명 하는 corelementtype 값을 가져옵니다.|  
  
## <a name="remarks"></a>설명  
 형식이 제네릭인 `ICorDebugClass` 경우는 인스턴스화되지 않은 형식을 나타냅니다. 인터페이스 `ICorDebugType` 는 인스턴스화된 제네릭 형식을 나타냅니다. 예를 들어 해시\<테이블 K, V >는에 의해 `ICorDebugClass`표현 되는\<반면 해시 테이블 Int32, 문자열 >는 `ICorDebugType`로 표시 됩니다.  
  
 제네릭이 아닌 형식은 `ICorDebugClass` 및 `ICorDebugType`로 표시 됩니다. 후자 인터페이스는 형식 인스턴스화를 처리 하기 위해 .NET Framework 버전 2.0에서 도입 되었습니다.  
  
> [!NOTE]
> 이 인터페이스는 크로스 시스템 또는 크로스 프로세스 원격 호출을 지원하지 않습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
