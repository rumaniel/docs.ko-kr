---
title: IEnumRAWINPUTDEVIC:Clone
ms.date: 03/30/2017
helpviewer_keywords:
- Clone method [WPF]
ms.assetid: 2a6a1900-aa55-45fa-9382-241d569a2dc4
ms.openlocfilehash: cd634b4d4a88d83d425b787ed8493f9aa2504988
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053415"
---
# <a name="ienumrawinputdevicclone"></a>IEnumRAWINPUTDEVIC:Clone
현재 열거자와 동일한 상태인 다른 원시 입력 디바이스 열거자를 만들어 동일한 목록을 반복합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT Clone( [out] IEnumRAWINPUTDEVICE **ppenum);  
```  
  
## <a name="parameters"></a>매개 변수  
 `ppenum`  
  
 제한이 [IEnumRAWINPUTDEVICE](ienumrawinputdevice.md) 인터페이스 포인터를 받는 output 변수의 주소입니다. 메서드가 실패 하면이 출력 변수의 값이 정의 되지 않습니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 HRESULT: 이 메서드는 표준 반환 값인 E_INVALIDARG, E_OUTOFMEMORY 및 E_UNEXPECTED를 지원 합니다.  
  
## <a name="remarks"></a>설명  
 이 메서드를 사용 하면 나중에 해당 지점으로 돌아갈 수 있도록 열거형 시퀀스의 지점을 기록할 수 있습니다. 호출자는 첫 번째 열거자와 별도로이 새 열거자를 해제 해야 합니다.
