---
title: StrongNameSignatureGeneration 함수
ms.date: 03/30/2017
api_name:
- StrongNameSignatureGeneration
api_location:
- mscoree.dll
- mscorsn.dll
api_type:
- DLLExport
f1_keywords:
- StrongNameSignatureGeneration
helpviewer_keywords:
- StrongNameSignatureGeneration function [.NET Framework strong naming]
ms.assetid: 839b765c-3e41-44ce-bf1b-dc10453db18e
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 48cdd550e5d8c7c75a603d74456e99a066d5c599
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798973"
---
# <a name="strongnamesignaturegeneration-function"></a>StrongNameSignatureGeneration 함수
지정된 어셈블리에 대한 강력한 이름 서명을 생성합니다.  
  
 이 함수는 더 이상 사용 되지 않습니다. 대신 [ICLRStrongName:: StrongNameSignatureGeneration](../hosting/iclrstrongname-strongnamesignaturegeneration-method.md) 메서드를 사용 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
BOOLEAN StrongNameSignatureGeneration (   
    [in]  LPCWSTR   wszFilePath,  
    [in]  LPCWSTR   wszKeyContainer,  
    [in]  BYTE      *pbKeyBlob,  
    [in]  ULONG     cbKeyBlob,  
    [out] BYTE      **ppbSignatureBlob,  
    [out] ULONG     *pcbSignatureBlob  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `wszFilePath`  
 진행 강력한 이름 서명이 생성 될 어셈블리의 매니페스트가 포함 된 파일의 경로입니다.  
  
 `wszKeyContainer`  
 진행 공개/개인 키 쌍을 포함 하는 키 컨테이너의 이름입니다.  
  
 `pbKeyBlob` 가`wszKeyContainer` null 인 경우는 CSP (암호화 서비스 공급자) 내에 올바른 컨테이너를 지정 해야 합니다. 이 경우 컨테이너에 저장 된 키 쌍을 사용 하 여 파일에 서명 합니다.  
  
 가 `pbKeyBlob` null이 아닌 경우 키 쌍은 키 BLOB (binary large object)에 포함 된 것으로 간주 됩니다.  
  
 키는 1024 비트 RSA (Rivest Rivest-shamir-adleman Rivest-shamir-adleman) 서명 키 여야 합니다. 지금은 다른 유형의 키를 지원 하지 않습니다.  
  
 `pbKeyBlob`  
 진행 공개/개인 키 쌍에 대 한 포인터입니다. 이 쌍은 Win32 `CryptExportKey` 함수에서 만든 형식입니다. 가 `pbKeyBlob` null 인 경우에 `wszKeyContainer` 지정 된 키 컨테이너는 키 쌍을 포함 하는 것으로 간주 됩니다.  
  
 `cbKeyBlob`  
 진행 의 `pbKeyBlob`크기 (바이트)입니다.  
  
 `ppbSignatureBlob`  
 제한이 공용 언어 런타임에서 서명을 반환 하는 위치에 대 한 포인터입니다. 가 `ppbSignatureBlob` null 이면 런타임에서는에 `wszFilePath`지정 된 파일에 서명을 저장 합니다.  
  
 가 `ppbSignatureBlob` null이 아닌 경우 공용 언어 런타임은 서명을 반환할 공간을 할당 합니다. 호출자는 [StrongNameFreeBuffer](strongnamefreebuffer-function.md) 함수를 사용 하 여이 공간을 확보 해야 합니다.  
  
 `pcbSignatureBlob`  
 제한이 반환 된 시그니처의 크기 (바이트)입니다.  
  
## <a name="return-value"></a>반환 값  
 `true`성공적으로 완료 되 면 그렇지 않으면 `false`입니다.  
  
## <a name="remarks"></a>설명  
 에 대해 `wszFilePath` null을 지정 하 여 서명을 만들지 않고 서명의 크기를 계산 합니다.  
  
 시그니처는 파일에 직접 저장 되거나 호출자에 게 반환 될 수 있습니다.  
  
 `StrongNameSignatureGeneration` 함수가 성공적으로 완료 되지 않으면 [StrongNameErrorInfo](strongnameerrorinfo-function.md) 함수를 호출하여 마지막으로 생성된 오류를 검색합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** StrongName.h  
  
 **라이브러리** Mscoree.dll에 리소스로 포함 됩니다.  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [StrongNameSignatureGeneration 메서드](../hosting/iclrstrongname-strongnamesignaturegeneration-method.md)
- [StrongNameSignatureGenerationEx 메서드](../hosting/iclrstrongname-strongnamesignaturegenerationex-method.md)
- [ICLRStrongName 인터페이스](../hosting/iclrstrongname-interface.md)
