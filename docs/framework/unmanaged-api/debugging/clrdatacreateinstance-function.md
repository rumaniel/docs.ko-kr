---
title: CLRDataCreateInstance 함수
ms.date: 03/30/2017
api_name:
- CLRDataCreateInstance
api_location:
- mscordbi.dll
- mscordacwks.dll
api_type:
- COM
f1_keywords:
- CLRDataCreateInstance
helpviewer_keywords:
- CLRDataCreateInstance function [.NET Framework debugging]
ms.assetid: 440bad90-5a88-45e7-9157-4596801d8d19
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a5d44f9b5dc42147959d3f1d127a64d39258f515
ms.sourcegitcommit: 3caa92cb97e9f6c31f21769c7a3f7c4304024b39
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2019
ms.locfileid: "71274270"
---
# <a name="clrdatacreateinstance-function"></a>CLRDataCreateInstance 함수
지정 된 대상 항목에 대 한 인터페이스 개체를 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT CLRDataCreateInstance (  
    [in]  REFIID           iid,   
    [in]  ICLRDataTarget  *target,   
    [out] void           **iface  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `iid`  
 진행 인스턴스화할 인터페이스의 식별자입니다.  
  
 `target`  
 진행 인터페이스 개체를 만들 대상 항목을 나타내는 사용자 구현 [ICLRDataTarget](iclrdatatarget-interface.md) 개체에 대 한 포인터입니다.  
  
 `iface`  
 제한이 반환 된 인터페이스 개체의 주소에 대 한 포인터입니다.  
  
## <a name="remarks"></a>설명  
 개체 `ICLRDataTarget` 는 디버깅 응용 프로그램의 작성기에 의해 구현 됩니다. 구현은 표시 되는 대상 항목의 형식에 따라 달라 집니다. 대상 항목은 프로세스, 메모리 덤프, 원격 컴퓨터 등 일 수 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** ClrData.idl  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고 항목

- [디버깅 전역 정적 함수](debugging-global-static-functions.md)
