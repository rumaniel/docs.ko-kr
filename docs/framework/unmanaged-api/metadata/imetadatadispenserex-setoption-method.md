---
title: IMetaDataDispenserEx::SetOption 메서드
ms.date: 03/30/2017
api_name:
- IMetaDataDispenserEx.SetOption
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataDispenserEx::SetOption
helpviewer_keywords:
- IMetaDataDispenserEx::SetOption method [.NET Framework metadata]
- SetOption method [.NET Framework metadata]
ms.assetid: 9f1c7ccd-7fb2-41d8-aa00-24b823376527
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 6916e6344fe5c112b216ca753c372fa73a4d5af5
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67777705"
---
# <a name="imetadatadispenserexsetoption-method"></a>IMetaDataDispenserEx::SetOption 메서드
현재 메타 데이터 범위에 대 한 지정 된 값으로 지정된 된 옵션을 설정합니다. 현재 메타 데이터 범위에 대 한 호출을 처리 하는 방법을 제어 하는 옵션입니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT SetOption (  
    [in] REFGUID optionId,   
    [in] const VARIANT *pValue  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `optionId`  
 [in] 설정할 옵션을 지정 하는 GUID에 대 한 포인터입니다.  
  
 `pValue`  
 [in] 옵션을 설정 하는 데 값입니다. 이 값의 형식 지정된 옵션의 종류의 변형 이어야 합니다.  
  
## <a name="remarks"></a>설명  
 다음 표에서 사용할 수 있는 Guid는를 `optionId` 매개 변수를 가리킬 수 있습니다 및 해당 유효 값을 `pValue` 매개 변수입니다.  
  
|GUID|Description|`pValue` 매개 변수|  
|----------|-----------------|------------------------|  
|MetaDataCheckDuplicatesFor|중복 항목을 검사할 제어 합니다. 호출할 때마다를 [IMetaDataEmit](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md) 새 항목을 만드는 메서드를 현재 범위에 항목이 이미 있는지 여부를 검사 하도록 요청할 수 있습니다. 예를 들어 있는지 확인할 수 있습니다 `mdMethodDef` 항목;이 경우 호출 하는 경우 [imetadataemit:: Definemethod](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-definemethod-method.md), 확인 메서드가 현재 범위에 이미 존재 하지 않습니다. 지정된 된 메서드를 고유 하 게 식별 하는 키를 사용 하는이 검사: 유형, 이름 및 서명을 부모입니다.|UI4, 형식의 variant 이어야 하며 값 조합을 포함 해야 합니다 [CorCheckDuplicatesFor](../../../../docs/framework/unmanaged-api/metadata/corcheckduplicatesfor-enumeration.md) 열거형입니다.|  
|MetaDataRefToDefCheck|항목을 참조 하는 컨트롤 정의로 변환 됩니다. 기본적으로 메타 데이터 엔진은 참조 된 항목은 실제로 현재 범위에서 정의 하는 경우 해당 정의에 참조 된 항목을 변환 하 여 코드를 최적화 합니다.|UI4, 형식의 variant 이어야 하며 값 조합을 포함 해야 합니다 [CorRefToDefCheck](../../../../docs/framework/unmanaged-api/metadata/correftodefcheck-enumeration.md) 열거형입니다.|  
|MetaDataNotificationForTokenMovement|토큰 메타 데이터를 병합 하는 동안 발생 재매핑을 제어 콜백을 생성 합니다. 사용 된 [imetadataemit:: Sethandler](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-sethandler-method.md) 설정 하는 방법에 [IMapToken](../../../../docs/framework/unmanaged-api/metadata/imaptoken-interface.md) 인터페이스입니다.|UI4, 형식의 variant 이어야 하며 값 조합을 포함 해야 합니다 [CorNotificationForTokenMovement](../../../../docs/framework/unmanaged-api/metadata/cornotificationfortokenmovement-enumeration.md) 열거형입니다.|  
|MetaDataSetENC|편집 하며 계속 하기 (ENC)의 동작을 제어 합니다. 한 번에 하나의 모드 동작을 설정할 수 있습니다.|UI4, 형식의 variant 이어야 하며 값을 포함 해야 합니다 [CorSetENC](../../../../docs/framework/unmanaged-api/metadata/corsetenc-enumeration.md) 열거형입니다. 값이 비트 마스크입니다.|  
|MetaDataErrorIfEmitOutOfOrder|내보낸--순서가 오류 콜백을 생성을 제어 합니다. 심각한; 아닙니다 순서가 메타 데이터 내보내기 그러나 메타 데이터 엔진에 의해 적용 된 순서에 따라 메타 데이터를 내보낼 있습니다 경우 메타 데이터는 보다 간단한 및 하므로 보다 효율적으로 검색할 수 있습니다. 사용 된 `IMetaDataEmit::SetHandler` 설정 하는 방법에 [IMetaDataError](../../../../docs/framework/unmanaged-api/metadata/imetadataerror-interface.md) 인터페이스입니다.|UI4, 형식의 variant 이어야 하며 값 조합을 포함 해야 합니다 [CorErrorIfEmitOutOfOrder](../../../../docs/framework/unmanaged-api/metadata/corerrorifemitoutoforder-enumeration.md) 열거형입니다.|  
|MetaDataImportOption|열거자에서 어떤 종류의 ENC 중 삭제 된 항목 검색을 제어 합니다.|UI4, 형식의 variant 이어야 하며 값 조합을 포함 해야 합니다 [CorImportOptions 열거형](../../../../docs/framework/unmanaged-api/metadata/corimportoptions-enumeration.md) 열거형입니다.|  
|MetaDataThreadSafetyOptions|메타 데이터 엔진 가져옵니다 스레드로부터의 안전성을 보장 하는 잠금 판독기/기록기 여부를 제어 합니다. 기본적으로 엔진에서는 액세스는 호출자가 단일 스레드 잠금을 사용 하지 않는 이루어지고 것을 가정 합니다. 클라이언트는 메타 데이터 API를 사용 하는 경우 적절 한 스레드 동기화를 유지 관리 하는 일을 담당 합니다.|UI4, 형식의 variant 이어야 하며 값을 포함 해야 합니다 [CorThreadSafetyOptions](../../../../docs/framework/unmanaged-api/metadata/corthreadsafetyoptions-enumeration.md) 열거형입니다. 값이 비트 마스크입니다.|  
|MetaDataGenerateTCEAdapters|형식 라이브러리 가져오기 COM 연결 지점 컨테이너에 대 한 밀접 하 게 결합 된 이벤트 (TCE) 어댑터를 생성할지 여부를 제어 합니다.|BOOL 형식의 variant를 해야 합니다. 하는 경우 `pValue` 로 설정 되어 `true`, 형식 라이브러리 가져오기 TCE 어댑터를 생성 합니다.|  
|MetaDataTypeLibImportNamespace|가져오는 형식 라이브러리에 대 한 기본이 아닌 네임 스페이스를 지정 합니다.|Null 값 또는 bstr의 변형 중 하나 여야 합니다. 경우 `pValue` null 값인 경우에 null이 고 그렇지 않으면 현재 네임 스페이스로 설정 되어, 현재 네임 스페이스는 variant BSTR 형식에 저장 된 문자열에 설정 됩니다.|  
|MetaDataLinkerOptions|링커가 어셈블리 또는.NET Framework 모듈 파일을 생성할지 여부를 제어 합니다.|UI4, 형식의 variant 이어야 하며 값 조합을 포함 해야 합니다 [CorLinkerOptions](../../../../docs/framework/unmanaged-api/metadata/corlinkeroptions-enumeration.md) 열거형입니다.|  
|MetaDataRuntimeVersion|공용 언어 런타임에서이 이미지를 빌드할 대상의 버전을 지정 합니다. 버전은 "v1.0.3705" 같은 문자열로 저장 됩니다.|Null 값, 값을 VT_EMPTY 또는 BSTR 형식 변형에 있어야 합니다. 경우 `pValue` 가 null 인 런타임 버전이 설정 되어 null로 합니다. 경우 `pValue` 는 VT_EMPTY를 버전 메타 데이터 코드를 실행 되 고 있는 Mscorwks.dll 버전에서 출발 하는 기본 값으로 설정 되어 있습니다. 그렇지 않으면 런타임 버전 variant의 BSTR 형식에 저장 된 문자열에 설정 됩니다.|  
|MetaDataMergerOptions|메타 데이터를 병합 하는 것에 대 한 옵션을 지정 합니다.|UI4, 형식의 variant 이어야 하며 값 조합을 포함 해야 합니다는 `MergeFlags` CorHdr.h 파일에 설명 된 열거형입니다.|  
|MetaDataPreserveLocalRefs|정의에 대 한 로컬 참조를 최적화 하는 사용 하지 않도록 설정 합니다.|값 조합을 포함 해야 합니다 [CorLocalRefPreservation](../../../../docs/framework/unmanaged-api/metadata/corlocalrefpreservation-enumeration.md) 열거형입니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Cor.h  
  
 **라이브러리:** MsCorEE.dll에서 리소스로 사용  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IMetaDataDispenserEx 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadatadispenserex-interface.md)
- [IMetaDataDispenser 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadatadispenser-interface.md)
