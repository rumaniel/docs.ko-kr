---
title: ImportTypes2 메서드
ms.date: 03/30/2017
api_name:
- IALink2.ImportTypes2
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- ImportTypes2
helpviewer_keywords:
- ImportTypes2 method
ms.assetid: 32f3ba58-9695-41e9-ba58-fd19e45ed396
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: ce09eca30e1edb9e1afc02216a07955a5fed4fd2
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70787261"
---
# <a name="importtypes2-method"></a>ImportTypes2 메서드
형식의 가져오기를 시작 합니다. [Importfile 메서드](importfile-method.md)를 통해 가져온 각 범위에서 형식 가져오기를 시작 하려면이 메서드를 호출 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT ImportTypes2(  
    mdAssembly AssemblyID,  
    mdToken FileToken,  
    DWORD dwScope,  
    HALINKENUM* phEnum,  
    IMetaDataImport2** ppImportScope,  
    DWORD* pdwCountOfTypes  
) PURE;  
```  
  
## <a name="parameters"></a>매개 변수  
 `AssemblyID`  
 가져올 어셈블리의 ID입니다.  
  
 `FileToken`  
 가져올 파일의 ID입니다.  
  
 `dwScope`  
 가져올 범위 (0부터 시작)입니다.  
  
 `phEnum`  
 지정 된 범위에 있는 형식에 대 한 열거자 핸들을 받습니다.  
  
 `ppImportScope`  
 선택적으로 [IMetaDataImport2 인터페이스](../metadata/imetadataimport2-interface.md) 인터페이스를 수신 합니다.  
  
 `pdwCountOfTypes`  
 선택적으로 지정 된 범위에 있는 형식의 수를 받습니다.  
  
## <a name="return-value"></a>반환 값  
 메서드가 성공 하면 S_OK를 반환 합니다.  
  
## <a name="requirements"></a>요구 사항  
 Alink 필요  
  
## <a name="see-also"></a>참고자료

- [IALink2 인터페이스](ialink2-interface.md)
- [IALink 인터페이스](ialink-interface.md)
- [ALink API](index.md)
