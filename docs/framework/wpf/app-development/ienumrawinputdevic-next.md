---
title: IEnumRAWINPUTDEVIC:Next
ms.date: 03/30/2017
helpviewer_keywords:
- Next method [WPF]
ms.assetid: 3698b44d-510e-4d18-b32b-85f17188ee26
ms.openlocfilehash: c7450a9ababa9cf3cb02d572f5ed84f0791d74e4
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053407"
---
# <a name="ienumrawinputdevicnext"></a>IEnumRAWINPUTDEVIC:Next
열거자 목록에서 `celt` 다음 [rawinputdevice](/windows/desktop/api/winuser/ns-winuser-rawinputdevice) 구조를 열거 하 고의 실제 열거 된 `rgelt` 요소 `pceltFetched`수와 함께에 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT Next(  
      [in] ULONG celt,  
      [out, size_is(celt), length_is(*pceltFetched)] RAWINPUTDEVICE *rgelt,  
      [out] ULONG *pceltFetched);  
```  
  
## <a name="parameters"></a>매개 변수  
 `celt`  
  
 진행 에서`rgelt`반환 된 [rawinputdevice](/windows/desktop/api/winuser/ns-winuser-rawinputdevice) 구조체의 수입니다.  
  
 `rgelt`  
  
 [out] 열거된 RAWINPUTDEVICE 구조체를 수신할 celt 크기(또는 더 큰)의 배열입니다.  
  
 `pceltFetched`  
  
 [out] `rgelt`에 실제로 제공된 요소 수에 대한 포인터입니다. `NULL`가 1이면 호출자가 `rgelt`을 전달할 수 있습니다.  
  
## <a name="property-valuereturn-value"></a>속성 값/반환 값  
 HRESULT: 제공 된 요소의 수가 이면 S_OK이 `celt`고, 그렇지 않으면입니다. 그렇지 않으면 S_FALSE입니다.
