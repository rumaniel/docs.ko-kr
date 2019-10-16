---
title: ICorDebugModule::CreateBreakpoint 메서드
ms.date: 03/30/2017
api_name:
- ICorDebugModule.CreateBreakpoint
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule::CreateBreakpoint
helpviewer_keywords:
- CreateBreakpoint method, ICorDebugModule interface [.NET Framework debugging]
- ICorDebugModule::CreateBreakpoint method [.NET Framework debugging]
ms.assetid: c2541c30-fa6e-43b6-9682-77d8898f33e1
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 28d96177e839613d40e8c500e334c92b05c6e96a
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67762192"
---
# <a name="icordebugmodulecreatebreakpoint-method"></a>ICorDebugModule::CreateBreakpoint 메서드
이 메서드는 현재 버전의.NET Framework에서 구현 되지에.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT CreateBreakpoint(  
    [out] ICorDebugModuleBreakpoint **ppBreakpoint  
);  
```  
  
## <a name="requirements"></a>요구 사항  
 **헤더:** CorDebug.idl, CorDebug.h
