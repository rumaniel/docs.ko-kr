---
title: StrongNameKeyDelete 함수
ms.date: 03/30/2017
api_name:
- StrongNameKeyDelete
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- StrongNameKeyDelete
helpviewer_keywords:
- StrongNameKeyDelete function [.NET Framework strong naming]
ms.assetid: 313e71e4-1790-4d2f-b68b-5040ebd1c149
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 17d35193f69966e02ac5e483924fcb3ee2e06758
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70799025"
---
# <a name="strongnamekeydelete-function"></a>StrongNameKeyDelete 함수

지정된 키 컨테이너를 삭제합니다.

이 함수는 더 이상 사용 되지 않습니다. 대신 [ICLRStrongName:: StrongNameKeyDelete](../hosting/iclrstrongname-strongnamekeydelete-method.md) 메서드를 사용 합니다.

## <a name="syntax"></a>구문

```cpp
BOOLEAN StrongNameKeyDelete (
    [in]  LPCWSTR   wszKeyContainer
);
```

## <a name="parameters"></a>매개 변수

`wszKeyContainer`\
진행 삭제할 키 컨테이너의 이름입니다.

## <a name="return-value"></a>반환 값

`true`성공적으로 완료 되 면 그렇지 않으면 `false`입니다.

## <a name="remarks"></a>설명

[StrongNameKeyInstall](strongnamekeyinstall-function.md) 함수를 사용 하 여 공개/개인 키 쌍을 컨테이너로 가져옵니다.

`StrongNameKeyDelete` 함수가 성공적으로 완료 되지 않으면 [StrongNameErrorInfo](strongnameerrorinfo-function.md) 함수를 호출하여 마지막으로 생성된 오류를 검색합니다.

## <a name="requirements"></a>요구 사항

**플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.

**헤더:** StrongName.h

**라이브러리** Mscoree.dll에 리소스로 포함 됩니다.

**.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]

## <a name="see-also"></a>참고자료

- [StrongNameKeyDelete 메서드](../hosting/iclrstrongname-strongnamekeydelete-method.md)
- [StrongNameKeyInstall 메서드](../hosting/iclrstrongname-strongnamekeyinstall-method.md)
- [ICLRStrongName 인터페이스](../hosting/iclrstrongname-interface.md)
