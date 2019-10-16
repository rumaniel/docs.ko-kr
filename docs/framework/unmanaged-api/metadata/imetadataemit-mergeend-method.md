---
title: IMetaDataEmit::MergeEnd 메서드
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.MergeEnd
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::MergeEnd
helpviewer_keywords:
- MergeEnd method [.NET Framework metadata]
- IMetaDataEmit::MergeEnd method [.NET Framework metadata]
ms.assetid: 2d64315a-1af1-4c60-aedf-f8a781914aea
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 6e512b7cd8869c6ede1472bbc5b6ec4c428b40ef
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67757648"
---
# <a name="imetadataemitmergeend-method"></a>IMetaDataEmit::MergeEnd 메서드

병합 현재 범위에 하나 이상의 이전 호출에 의해 지정 된 모든 메타 데이터 범위가 [imetadataemit:: 병합](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-merge-method.md)입니다.

## <a name="syntax"></a>구문

```cppcpp
HRESULT MergeEnd ();
```

## <a name="parameters"></a>매개 변수

이 메서드는 매개 변수 없이 합니다.

## <a name="remarks"></a>설명

이 루틴은 메타 데이터의 실제 병합 트리거, 모든 가져오기에 대 한 호출 앞에서 지정한 범위 `IMetaDataEmit::Merge`, 현재 출력 범위로 합니다.

다음과 같은 특수 병합에 적용 됩니다.

- 메타 데이터 가져오기 범위에 고유 하기 때문에 모듈 버전 식별자 (MVID) 되지 가져오게 됩니다.

- 없는 기존 모듈 수준의 속성을 덮어씁니다.

  현재 범위에 대 한 모듈 속성이 이미 설정 된 경우 모듈 속성이 없는 가져와집니다. 그러나 현재 범위의 모듈 속성을 설정 하지 않은 경우 가져온 처음 발생할 때 한 번만 합니다. 이러한 모듈 속성 다시 발생 하는 경우 중복 됩니다. (MVID)를 제외한 모든 모듈 속성의 값이 비교 됩니다. 중복 되 고 오류가 발생 합니다.

- 형식 정의 (`TypeDef`), 현재 범위에 중복 항목이 없으면 병합 됩니다. `TypeDef` 개체를 각각에 대해 중복 검사 *정규화 된 개체 이름* + *GUID* + *버전 번호*합니다. 이름 또는 GUID에서 일치 하는 경우 다른 두 요소 중 하나라도 다른 오류가 발생 합니다. 그렇지 않으면 일치 하는 모든 세 항목이 `MergeEnd` 는 항목은 실제로 중복 항목이 되도록 대략적인 검사를 그렇지 않은 경우 오류가 발생 합니다. 대략적인이 검사를 찾습니다.

  - 동일한 멤버 선언 같은 순서로 발생 합니다. 으로 플래그가 지정 되는 멤버 `mdPrivateScope` (참조를 [CorMethodAttr](../../../../docs/framework/unmanaged-api/metadata/cormethodattr-enumeration.md) 열거형)이이 확인은 특수 병합 된 합니다.

  - 동일한 클래스 레이아웃입니다.

  즉, 한 `TypeDef` 개체 항상 완벽 하 게 하 고 일관 되 게에서 정의 해야 모든 메타 데이터 범위는 선언 된; 전체 정의로 간주 됩니다 (클래스)에 대 한 해당 멤버 구현을 여러 컴파일 단위에 분산 되어, 하는 경우 모든 범위에 증분이 아닌 각 범위에 있습니다. 예를 들어, 매개 변수 이름을 계약 관련 된 경우 내보내야 동일한 방식으로 모든 범위로; 관련 없는 경우는 내보내지 않아야 메타 데이터에 있습니다.

  예외를 `TypeDef` 로 플래그가 지정 된 증분 멤버 개체에 있을 수 `mdPrivateScope`입니다. 이러한 발생 했을 때 `MergeEnd` 증분 방식으로 중복 항목에 관계 없이 현재 범위에 추가 합니다. 전용 범위를 인식 하기 때문에 컴파일러는 규칙을 적용 하는 일을 담당 해야 합니다.

- 가상 Rva (상대 주소)는 가져오거나 병합; 컴파일러는이 정보를 다시 생성 해야 합니다.

- 연결 된 항목을 병합 하는 경우에 사용자 지정 특성이 병합 됩니다. 예를 들어, 클래스와 연관 된 사용자 지정 특성 클래스 처음 발생 하는 경우 병합 됩니다. 사용자 지정 특성이 연결 된 경우는 `TypeDef` 또는 `MemberDef` 입니다 (예: 멤버 컴파일 타임 스탬프) 컴파일 단위, 병합 되지 않습니다 및 컴파일러에서 제거 하거나 이러한 메타 데이터를 업데이트 하는 것입니다.

## <a name="requirements"></a>요구 사항

**플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.

**헤더:** Cor.h

**라이브러리:** MSCorEE.dll에서 리소스로 사용

**.NET Framework 버전:** [!INCLUDE[net_current_v11plus](../../../../includes/net-current-v11plus-md.md)]

## <a name="see-also"></a>참고자료

- [IMetaDataEmit 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md)
- [IMetaDataEmit2 인터페이스](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-interface.md)
