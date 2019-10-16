---
title: CreateInstallReferenceEnum 함수
ms.date: 03/30/2017
api_name:
- CreateInstallReferenceEnum
api_location:
- fusion.dll
- clr.dll
- mscorwks.dll
api_type:
- DLLExport
f1_keywords:
- CreateInstallReference
helpviewer_keywords:
- CreateInstallReference function [.NET Framework fusion]
ms.assetid: 80dbbbf8-54fc-4894-b74a-0179d3201083
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d696326ff8861ed8496474f76e9eaf89b4ead3e8
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795395"
---
# <a name="createinstallreferenceenum-function"></a>CreateInstallReferenceEnum 함수
지정 된 어셈블리에 대 한 응용 프로그램 참조 목록을 나타내는 [Iinstallreferenceenum](iinstallreferenceenum-interface.md) 인스턴스에 대 한 포인터를 가져옵니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT CreateInstallReferenceEnum (  
    [out] IInstallReferenceEnum **ppRefEnum,  
    [in]  IAssemblyName         *pName,  
    [in]  DWORD                 dwFlags,  
    [in]  LPVOID                pvReserved  
 );  
```  
  
## <a name="parameters"></a>매개 변수  
 `ppRefEnum`  
 제한이 반환 `IInstallReferenceEnum` 된 포인터입니다.  
  
 `pName`  
 진행 참조를 열거 하는 데 사용할 어셈블리를 식별 하는 [IAssemblyName](iassemblyname-interface.md) 입니다.  
  
 `dwFlags`  
 진행 열거자의 동작에 영향을 주는 플래그입니다.  
  
 `pvReserved`  
 진행 향후 확장성을 위해 예약 되었습니다. `pvReserved`는 null 참조 여야 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** Fusion. h  
  
 **라이브러리** Fusion 및 Mscorwks.dll. Mscorwks.dll 대신 Fusion을 사용 하 여 올바른 버전의 .NET Framework를 대상으로 하는지 확인 합니다.  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IInstallReferenceEnum 인터페이스](iinstallreferenceenum-interface.md)
- [IAssemblyName 인터페이스](iassemblyname-interface.md)
- [Fusion 전역 정적 함수](fusion-global-static-functions.md)
