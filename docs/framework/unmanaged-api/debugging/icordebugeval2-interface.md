---
title: ICorDebugEval2 인터페이스
ms.date: 03/30/2017
api_name:
- ICorDebugEval2
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugEval2
helpviewer_keywords:
- ICorDebugEval2 interface [.NET Framework debugging]
ms.assetid: fce34531-2687-406d-9131-d6ad94f2ce0e
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7cad998ec30ee97cf6c1eb27640567b3fe233a19
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69951956"
---
# <a name="icordebugeval2-interface"></a>ICorDebugEval2 인터페이스

"ICorDebugEval"를 확장 하 여 제네릭 형식에 대 한 지원을 제공 합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|Description|  
|------------|-----------------|  
|[CallParameterizedFunction 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugeval2-callparameterizedfunction-method.md)|지정 된 "ICorDebugFunction"에 대 한 호출을 설정 합니다 .이는 생성자에서 형식 매개 변수를 사용 하거나 형식 매개 변수를 사용할 수 있는 형식 내에 중첩 될 수 있습니다.|  
|[CreateValueForType 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugeval2-createvaluefortype-method.md)|초기 값이 null 또는 0 인 지정 된 형식의 새 "ICorDebugValue"에 대 한 포인터를 가져옵니다.|  
|[NewParameterizedArray 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugeval2-newparameterizedarray-method.md)|지정 된 요소 형식 및 차원의 새 배열을 할당 합니다.|  
|[NewParameterizedObject 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugeval2-newparameterizedobject-method.md)|매개 변수가 있는 새 형식 개체를 인스턴스화하고 개체의 생성자 메서드를 호출 합니다.|  
|[NewParameterizedObjectNoConstructor 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugeval2-newparameterizedobjectnoconstructor-method.md)|생성자 메서드 호출을 시도 하지 않고 지정 된 클래스의 매개 변수가 있는 새 형식 개체를 인스턴스화합니다.|  
|[NewStringWithLength 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugeval2-newstringwithlength-method.md)|지정 된 내용을 사용 하 여 지정 된 길이의 새 문자열을 만듭니다.|  
|[RudeAbort 메서드](../../../../docs/framework/unmanaged-api/debugging/icordebugeval2-rudeabort-method.md)|현재 수행 중인 계산 `ICorDebugEval2` 을 중단 합니다.|  
  
## <a name="remarks"></a>설명  
  
> [!NOTE]
> 이 인터페이스는 크로스 시스템 또는 크로스 프로세스 원격 호출을 지원하지 않습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
