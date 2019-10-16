---
title: ICorDebugModule2::ApplyChanges 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugModule2.ApplyChanges
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule2::ApplyChanges
helpviewer_keywords:
- ApplyChanges method [.NET Framework debugging]
- ICorDebugModule2::ApplyChanges method [.NET Framework debugging]
ms.assetid: 96fa3406-6a6f-41a1-88c6-d9bc5d1a16d1
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 860b87b09ee487f893a1bba2aaa34292c50ffcb7
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67764346"
---
# <a name="icordebugmodule2applychanges-method"></a>ICorDebugModule2::ApplyChanges 메서드
실행 중인 프로세스에 메타 데이터의 변경 내용 및 Microsoft의 MSIL (intermediate language) 코드의 변경 내용을 적용합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT ApplyChanges (  
    [in] ULONG                       cbMetadata,  
    [in, size_is(cbMetadata)] BYTE   pbMetadata[],  
    [in] ULONG                       cbIL,  
    [in, size_is(cbIL)] BYTE         pbIL[]  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `cbMetadata`  
 [in] 델타 메타 데이터의 바이트에서 크기입니다.  
  
 `pbMetadata`  
 [in] 델타 메타 데이터가 들어 있는 버퍼입니다. 버퍼의 주소에서 반환 되는 [IMetaDataEmit2::SaveDeltaToMemory](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-savedeltatomemory-method.md) 메서드.  
  
 메타 데이터에 상대 가상 주소 (Rva) MSIL 코드의 시작을 기준으로 해야 합니다.  
  
 `cbIL`  
 [in] 크기 (바이트)의 델타 MSIL 코드입니다.  
  
 `pbIL`  
 [in] 업데이트 된 MSIL 코드를 포함 하는 버퍼입니다.  
  
## <a name="remarks"></a>설명  
 합니다 `pbMetadata` 특수 델타 메타 데이터 형식으로 매개 변수는 (으로 출력 하 여 [IMetaDataEmit2::SaveDeltaToMemory](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-savedeltatomemory-method.md)). `pbMetadata` 이전 메타 데이터를 기준으로 사용 하 고 해당 자료를 적용 하는 개별 변경 내용을 설명 합니다.  
  
 반면,는 `pbIL[`] 매개 변수 업데이트 메서드에 대 한 새 MSIL이 포함 하 고 해당 메서드에 대 한 이전 MSIL을 완전히 대체 것  
  
 디버거를 호출 하는 디버거의 메모리에 델타 MSIL 및 메타 데이터 생성 되 면 `ApplyChanges` 는 CLR (공용 언어 런타임)에 변경 내용을 보냅니다. 런타임에 해당 메타 데이터 테이블을 업데이트 하 고, 새 MSIL 프로세스에 배치, 새 msil-just-in-time (JIT) 컴파일 설정 합니다. 디버거를 호출 해야 변경 내용이 적용 된 경우 [IMetaDataEmit2::ResetENCLog](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-resetenclog-method.md) 다음 편집 세션에 대 한 준비를 합니다. 디버거는 프로세스를 계속 한 다음 수 있습니다.  
  
 디버거에서 호출할 때마다 `ApplyChanges` 델타 메타 데이터가 있는 모듈의 경우에 호출도 해야 [imetadataemit:: Applyeditandcontinue](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-applyeditandcontinue-method.md) 모든 복사본을 제외 하 고 해당 모듈의 메타 데이터의 복사본에 동일한 델타 메타 데이터를 사용 하 여 변경 내용을 내보내는 데 사용 합니다. 메타 데이터의 복사본에는 어떤 이유로 든 동기화 아웃 되 면 실제 메타 데이터를 사용 하 여 디버거가 항상 해당 복사본을 버리는 새 복사본을 가져옵니다.  
  
 경우는 `ApplyChanges` 메서드가 실패 하면 디버그 세션을 잘못 된 상태 이며 다시 시작 해야 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** CorDebug.idl, CorDebug.h  
  
 **라이브러리:** CorGuids.lib  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
