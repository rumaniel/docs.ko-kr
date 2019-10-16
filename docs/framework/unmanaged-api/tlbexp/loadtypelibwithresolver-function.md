---
title: LoadTypeLibWithResolver 함수
ms.date: 03/30/2017
api_name:
- LoadTypeLibWithResolver
api_location:
- TlbRef.dll
api_type:
- DLLExport
f1_keywords:
- LoadTypeLibWithResolver
helpviewer_keywords:
- LoadTypeLibWithResolver function [.NET Framework]
ms.assetid: 7123a89b-eb9b-463a-a552-a081e33b0a3a
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b78789344050fd5e1cb0ee3492bf330fbf92bc88
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798929"
---
# <a name="loadtypelibwithresolver-function"></a>LoadTypeLibWithResolver 함수
형식 라이브러리를 로드 하 고 제공 된 [ITypeLibResolver 인터페이스](itypelibresolver-interface.md) 를 사용 하 여 내부적으로 참조 되는 형식 라이브러리를 확인 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT LoadTypeLibWithResolver(  
    [in]  LPCOLESTR           szFile,  
    [in]  REGKIND             regkind,  
    [in]  ITypeLibResolver   *pTlbResolver,  
    [out] ITypeLib          **pptlib);  
```  
  
## <a name="parameters"></a>매개 변수  
 `szFile`  
 진행 형식 라이브러리의 파일 경로입니다.  
  
 `regkind`  
 진행 형식 라이브러리를 등록 하는 방법을 제어 하는 [Regkind 열거형](https://docs.microsoft.com/windows/win32/api/oleauto/ne-oleauto-regkind) 플래그입니다. 가능한 값은 다음과 같습니다.  
  
- `REGKIND_DEFAULT`: 기본 등록 동작을 사용 합니다.  
  
- `REGKIND_REGISTER`: 이 형식 라이브러리를 등록 합니다.  
  
- `REGKIND_NONE`: 이 형식 라이브러리를 등록 하지 마십시오.  
  
 `pTlbResolver`  
 진행 [ITypeLibResolver 인터페이스](itypelibresolver-interface.md)의 구현에 대 한 포인터입니다.  
  
 `pptlib`  
 제한이 로드 되 고 있는 형식 라이브러리에 대 한 참조입니다.  
  
## <a name="return-value"></a>반환 값  
 다음 표에 나열 된 HRESULT 값 중 하나입니다.  
  
|반환 값|의미|  
|------------------|-------------|  
|`S_OK`|명령 실행 성공|  
|`E_OUTOFMEMORY`|메모리가 부족합니다.|  
|`E_POINTER`|하나 이상의 포인터가 잘못 되었습니다.|  
|`E_INVALIDARG`|인수 중 하나 이상이 올바르지 않습니다.|  
|`TYPE_E_IOERROR`|함수에서 파일에 쓸 수 없습니다.|  
|`TYPE_E_REGISTRYACCESS`|시스템 등록 데이터베이스를 열 수 없습니다.|  
|`TYPE_E_INVALIDSTATE`|형식 라이브러리를 열 수 없습니다.|  
|`TYPE_E_CANTLOADLIBRARY`|형식 라이브러리 또는 DLL을 로드할 수 없습니다.|  
  
## <a name="remarks"></a>설명  
 [Tlbexp.exe (형식 라이브러리 내보내기)](../../tools/tlbexp-exe-type-library-exporter.md) 는 어셈블리에서 형식 라이브러리로 `LoadTypeLibWithResolver` 의 변환 프로세스 중에 함수를 호출 합니다.  
  
 이 함수는 레지스트리에 대 한 최소 액세스 권한으로 지정 된 형식 라이브러리를 로드 합니다. 그런 다음 함수는 내부적으로 참조 되는 형식 라이브러리에 대 한 형식 라이브러리를 검사 합니다. 각 라이브러리는 로드 되어 부모 형식 라이브러리에 추가 되어야 합니다.  
  
 참조 된 형식 라이브러리를 로드 하려면 먼저 해당 참조 파일 경로를 전체 파일 경로로 확인 해야 합니다. 이는 `pTlbResolver` 매개 변수로 전달 되는 [ITypeLibResolver 인터페이스](itypelibresolver-interface.md)에서 제공 하는 [ResolveTypeLib 메서드](resolvetypelib-method.md) 를 통해 수행 됩니다.  
  
 참조 된 형식 라이브러리의 전체 파일 경로를 알고 있는 경우 함수는 `LoadTypeLibWithResolver` 참조 된 형식 라이브러리를 로드 하 여 부모 형식 라이브러리에 추가 하 고 결합 된 마스터 형식 라이브러리를 만듭니다.  
  
 함수가 내부적으로 참조 되는 형식 라이브러리를 모두 확인 하 고 로드 한 후에는 `pptlib` 매개 변수에서 마스터의 확인 된 형식 라이브러리에 대 한 참조를 반환 합니다.  
  
 함수 `LoadTypeLibWithResolver` 는 일반적으로 [tlbexp.exe (형식 라이브러리 내보내기)](../../tools/tlbexp-exe-type-library-exporter.md)에서 호출 되며,이는 `pTlbResolver` 매개 변수에 고유한 내부 [ITypeLibResolver 인터페이스](itypelibresolver-interface.md) 구현을 제공 합니다.  
  
 을 직접 호출 `LoadTypeLibWithResolver` 하는 경우 고유한 [ITypeLibResolver 인터페이스](itypelibresolver-interface.md) 구현을 제공 해야 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** TlbRef.h  
  
 **라이브러리** TlbRef.lib  
  
 **.NET Framework 버전:** 3.5, 3.0, 2.0  
  
## <a name="see-also"></a>참고자료

- [Tlbexp 도우미 함수](index.md)
- [LoadTypeLibEx 함수](https://docs.microsoft.com/previous-versions/windows/desktop/api/oleauto/nf-oleauto-loadtypelibex)
