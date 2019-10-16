---
title: IEnumRAWINPUTDEVICE
ms.date: 03/30/2017
helpviewer_keywords:
- IEnumRAWINPUTDEVICE interface [WPF]
ms.assetid: 88c8b389-a48b-46b9-b895-8ed7b1e26fea
ms.openlocfilehash: 5249d7ea359db5d5c58ae87600f61048b465b4c1
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69964774"
---
# <a name="ienumrawinputdevice"></a>IEnumRAWINPUTDEVICE
이 인터페이스는 원시 입력 디바이스를 열거하며 PresentationHost.exe에서만 사용됩니다.  
  
> [!NOTE]
> 이 API는 로컬 클라이언트 컴퓨터에서만 사용할 수 있도록 지원됩니다.  
  
## <a name="members"></a>멤버  
  
|멤버|Description|  
|------------|-----------------|  
|[IEnumRAWINPUTDEVIC:Next](ienumrawinputdevic-next.md)|열거자 목록에서 다음 `celt` 요소(즉, RAWINPUTDEVICE 구조체)를 열거하고 `rgelt`의 실제 열거된 요소 수와 함께 `pceltFetched`에 반환합니다.|  
|[IEnumRAWINPUTDEVIC:Skip](ienumrawinputdevic-skip.md)|[IEnumRAWINPUTDEVIC: next](ienumrawinputdevic-next.md) 에 대 한 다음 `celt` 호출이 해당 요소를 반환 하지 않도록 열거자가 열거형의 다음 요소를 건너뛰도록 지시 합니다.|  
|[IEnumRAWINPUTDEVIC:Reset](ienumrawinputdevic-reset.md)|열거형 시퀀스를 시작 부분으로 다시 설정합니다.|  
|[IEnumRAWINPUTDEVIC:Clone](ienumrawinputdevic-clone.md)|현재 열거자와 동일한 상태인 다른 원시 입력 디바이스 열거자를 만들어 동일한 목록을 반복합니다.|  
  
## <a name="see-also"></a>참고자료

- [원시 입력 정보](/windows/desktop/inputdev/about-raw-input)
