---
title: SetManifestFile 메서드
ms.date: 03/30/2017
api_name:
- IALink3.SetManifestFile
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- SetManifestFile
helpviewer_keywords:
- SetManifestFile method
ms.assetid: 1b33de4c-19cb-4a36-a93f-8675b2a36d58
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: b293c30060107d18c6b609efc82c4128a73cc1c7
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70787200"
---
# <a name="setmanifestfile-method"></a>SetManifestFile 메서드
링커가 어셈블리를 만들 때 사용 하는 매니페스트 파일을 지정 하거나 다시 설정할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT SetManifestFile(  
    LPCWSTR pszFile  
) PURE;  
```  
  
## <a name="parameters"></a>매개 변수  
 `pszFile`  
  
 Win32 리소스 blob에 콘텐츠를 포함 하는 매니페스트 파일의 이름입니다.  
  
## <a name="return-value"></a>반환 값  
 메서드가 성공 하면 S_OK를 반환 합니다.  
  
## <a name="remarks"></a>설명  
 Win32ResBlob를 요청 하기 전에이를 호출 합니다. `pszFile` 매개 변수 값은 콘텐츠를 읽고 Win32 리소스에서 ID가 RT_MANIFEST 인 매니페스트 파일의 이름입니다. NULL의 매개 변수를 사용 하 여 호출 하면 이전에 읽은 모든 매니페스트가 지워집니다. 이렇게 하면 링커가 초기화 시간의 상태를 다시 설정할 수 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 ALink 필요  
  
## <a name="see-also"></a>참고자료

- [IALink3 인터페이스](ialink3-interface.md)
- [ALink API](index.md)
- [IALink 인터페이스](ialink-interface.md)
- [Al.exe(어셈블리 링커)](../../tools/al-exe-assembly-linker.md)
