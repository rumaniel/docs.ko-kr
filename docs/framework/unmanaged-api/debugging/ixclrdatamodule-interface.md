---
title: IXCLRDataModule 인터페이스
ms.date: 01/16/2019
api.name:
- IXCLRDataModule Interface
api.location:
- mscordacwks.dll
api.type:
- COM
f1.keywords:
- IXCLRDataModule Interface
helpviewer.keywords:
- IXCLRDataModule Interface [.NET Framework debugging]
topic_type:
- apiref
author: cshung
ms.author: andrewau
ms.openlocfilehash: c8d6e36687fd43bbc59304eee64dd42eb78101e3
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54676525"
---
# <a name="ixclrdatamodule-interface"></a>IXCLRDataModule 인터페이스

로드 된 모듈에 대 한 정보를 쿼리 하기 위한 메서드를 제공 합니다.

[!INCLUDE[debugging-api-recommended-note](../../../../includes/debugging-api-recommended-note.md)]

## <a name="methods"></a>메서드

| 메서드                                                                                                                                | 설명                                                         |
| ------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| [GetMethodDefinitionByToken](../../../../docs/framework/unmanaged-api/debugging/ixclrdatamodule-getmethoddefinitionbytoken-method.md) | 지정 된 메타 데이터 토큰에 해당 하는 메서드 정을 가져옵니다. |
| [요청](../../../../docs/framework/unmanaged-api/debugging/ixclrdatamodule-request-method.md)                                       | 모듈의 데이터를 사용 하 여 지정 된 버퍼를 채우는 데 요청 합니다.       |
| [GetVersionId](../../../../docs/framework/unmanaged-api/debugging/ixclrdatamodule-getversionid-method.md)                             | 모듈의 버전 ID를 가져옵니다.                                       |

## <a name="remarks"></a>설명

이 인터페이스는 런타임 내에서 있으며 모든 헤더 또는 라이브러리 파일을 통해 노출 되지 않습니다. 그러나 COM 인터페이스에서 파생 되는 것 `IUnknown` GUID를 사용 하 여 `88E32849-0A0A-4cb0-9022-7CD2E9E139E2` 일반적인 COM 메커니즘을 통해 얻을 수 있습니다.

## <a name="requirements"></a>요구 사항

**플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
**헤더:** 없음  
**라이브러리:** 없음  
**.NET Framework 버전:** [!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  

## <a name="see-also"></a>참고자료

- [디버깅](../../../../docs/framework/unmanaged-api/debugging/index.md)
- [디버깅 인터페이스](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
