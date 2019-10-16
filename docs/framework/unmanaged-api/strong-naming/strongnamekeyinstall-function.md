---
title: StrongNameKeyInstall 함수
ms.date: 03/30/2017
api_name:
- StrongNameKeyInstall
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- StrongNameKeyInstall
helpviewer_keywords:
- StrongNameKeyInstall function [.NET Framework strong naming]
ms.assetid: e32fd546-7757-4681-be3d-658e93281e50
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 353898b72f41acd0c49a43ff05e54f61b99444c4
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70799003"
---
# <a name="strongnamekeyinstall-function"></a>StrongNameKeyInstall 함수

퍼블릭/프라이빗 키 쌍을 컨테이너로 가져옵니다.

이 함수는 더 이상 사용 되지 않습니다. 대신 [ICLRStrongName:: StrongNameKeyInstall](../hosting/iclrstrongname-strongnamekeyinstall-method.md) 메서드를 사용 합니다.

## <a name="syntax"></a>구문

```cpp
BOOLEAN StrongNameKeyInstall (
    [in]  LPCWSTR   wszKeyContainer,
    [in]  BYTE      *pbKeyBlob,
    [in]  ULONG     cbKeyBlob
);
```

## <a name="parameters"></a>매개 변수

`wszKeyContainer`\
진행 키 컨테이너의 이름입니다. `wszKeyContainer`비어 있지 않은 문자열 이어야 합니다.

`pbKeyBlob`\
진행 이진 키 쌍입니다.

`cbKeyBlob`\
진행 의 `pbKeyBlob`크기 (바이트)입니다.

## <a name="return-value"></a>반환 값

`true`성공적으로 완료 되 면 그렇지 않으면 `false`입니다.

## <a name="remarks"></a>설명

[StrongNameKeyDelete](strongnamekeydelete-function.md) 함수를 사용 하 여 키 컨테이너를 삭제 합니다.

`StrongNameKeyInstall`함수가 성공적으로 완료되지 않으면 [StrongNameErrorInfo](strongnameerrorinfo-function.md) 함수를 호출하여 마지막으로 생성된 오류를 검색합니다.

## <a name="requirements"></a>요구 사항

**플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.

**헤더:** StrongName.h

**라이브러리** Mscoree.dll에 리소스로 포함 됩니다.

**.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]

## <a name="see-also"></a>참고자료

- [StrongNameKeyInstall 메서드](../hosting/iclrstrongname-strongnamekeyinstall-method.md)
- [StrongNameKeyDelete 메서드](../hosting/iclrstrongname-strongnamekeydelete-method.md)
- [ICLRStrongName 인터페이스](../hosting/iclrstrongname-interface.md)
