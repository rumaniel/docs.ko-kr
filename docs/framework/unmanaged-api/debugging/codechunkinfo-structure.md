---
title: CodeChunkInfo 구조체
ms.date: 03/30/2017
api_name:
- CodeChunkInfo
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CodeChunkInfo
helpviewer_keywords:
- CodeChunkInfo structure [.NET Framework debugging]
ms.assetid: 0f482454-8517-48de-ba7a-d7aedab13bb5
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 36afee8af3de046683c55215a677a529b0837c77
ms.sourcegitcommit: 3caa92cb97e9f6c31f21769c7a3f7c4304024b39
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2019
ms.locfileid: "71274248"
---
# <a name="codechunkinfo-structure"></a>CodeChunkInfo 구조체

메모리 내의 단일 코드 청크를 나타냅니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef struct _CodeChunkInfo {  
    CORDB_ADDRESS startAddr;  
    ULONG32       length;  
} CodeChunkInfo;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|설명|  
|------------|-----------------|  
|`startAddr`|청크의 시작 주소를 지정 하는 값입니다.`CORDB_ADDRESS`|  
|`length`|청크의 크기 (바이트)입니다.|  
  
## <a name="remarks"></a>설명  
 코드의 단일 청크는 함수와 같은 코드 개체의 일부인 네이티브 코드의 영역입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl  
  
 **라이브러리** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고 항목

- [GetCodeChunks 메서드](icordebugcode2-getcodechunks-method.md)
- [디버깅 구조체](debugging-structures.md)
- [디버깅](index.md)
