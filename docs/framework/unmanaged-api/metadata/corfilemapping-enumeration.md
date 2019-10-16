---
title: CorFileMapping 열거형
ms.date: 03/30/2017
api_name:
- CorFileMapping
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorFileMapping
helpviewer_keywords:
- CorFileMapping enumeration [.NET Framework metadata]
ms.assetid: 3ca41592-b8da-475a-8032-a15627730003
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 719f0522cc43625a4d6cc8afa838d869e47b40d1
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67781843"
---
# <a name="corfilemapping-enumeration"></a>CorFileMapping 열거형
에 대 한 호출에서 반환 되는 매핑 파일의 형식을 설명 하는 값을 포함 합니다 [imetadatainfo:: Getfilemapping](../../../../docs/framework/unmanaged-api/metadata/imetadatainfo-getfilemapping-method.md) 메서드.  
  
## <a name="syntax"></a>구문  
  
```cpp  
typedef enum CorFileMapping {  
  
    fmFlat                  =   0x0000,  
    fmExecutableImage       =   0x0001  
  
} CorFileMapping;  
```  
  
## <a name="members"></a>멤버  
  
|멤버|Description|  
|------------|-----------------|  
|`fmFlat`|파일을 데이터 파일로 매핑됩니다. 즉, 합니다 `SEC_IMAGE` 플래그는 Microsoft Win32 전달 되지 않으므로 `CreateFileMapping` 함수입니다.|  
|`fmExecutableImage`|파일 중 하나를 사용 하 여 실행을 위해 매핑된 합니다 `LoadLibrary` 함수 또는 `CreateFileMapping` 함수는 `SEC_IMAGE` 플래그입니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorHdr.h  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [메타데이터 열거형](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
- [GetFileMapping 메서드](../../../../docs/framework/unmanaged-api/metadata/imetadatainfo-getfilemapping-method.md)
