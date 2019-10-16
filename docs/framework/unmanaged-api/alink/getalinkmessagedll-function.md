---
title: GetALinkMessageDll 함수
ms.date: 03/30/2017
api_name:
- GetALinkMessageDll
api_location:
- alink.dll
api_type:
- DLLExport
f1_keywords:
- GetALinkMessageDll
helpviewer_keywords:
- Alink API, GetALinkMessageDll function
- GetALinkMessageDll function
ms.assetid: 67985a22-88a2-4c54-8d99-4bcde9d6213e
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 323e53c45a26d5703548ebe9863978f6d3929f0b
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70787465"
---
# <a name="getalinkmessagedll-function"></a>GetALinkMessageDll 함수
메시지 DLL을 찾아서 로드 합니다. 메시지 DLL을 찾을 수 없거나 로드할 수 없는 경우 0을 반환 합니다. 메시지 DLL은 이름이 언어 ID 이거나 현재 디렉터리에 있는 하위 디렉터리에 있어야 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HINSTANCE WINAPI GetALinkMessageDll();  
```  
  
## <a name="requirements"></a>요구 사항  
 **헤더:** alink. h  
  
 **라이브러리**: alink .dll  
  
## <a name="see-also"></a>참고자료

- [Al.exe(어셈블리 링커)](../../tools/al-exe-assembly-linker.md)
