---
title: ICLRPolicyManager 인터페이스
ms.date: 03/30/2017
api_name:
- ICLRPolicyManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRPolicyManager
helpviewer_keywords:
- ICLRPolicyManager interface [.NET Framework hosting]
ms.assetid: 5c834aa1-f2db-408a-b230-c7bec093d364
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2eeccc4dfd7a7147fe791444eeeca2bd3a844305
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61638868"
---
# <a name="iclrpolicymanager-interface"></a>ICLRPolicyManager 인터페이스
정책 오류 및 시간 초과가 발생 시 수행할 작업을 지정 하려면 호스트를 사용할 수 있는 메서드를 제공 합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[SetActionOnFailure 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrpolicymanager-setactiononfailure-method.md)|CLR (공용 언어 런타임)은 지정 된 오류가 발생할 때 수행 해야 정책 동작을 지정 합니다.|  
|[SetActionOnTimeout 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrpolicymanager-setactionontimeout-method.md)|지정 된 작업 시간이 초과 되 면 CLR 취해야 정책 동작을 지정 합니다.|  
|[SetDefaultAction 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrpolicymanager-setdefaultaction-method.md)|지정 된 작업이 수행 될 때 CLR 취해야 정책 작업을 지정 합니다.|  
|[SetTimeout 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrpolicymanager-settimeout-method.md)|지정 된 작업에 대 한 제한 시간 값을 설정합니다.|  
|[SetTimeoutAndAction 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrpolicymanager-settimeoutandaction-method.md)|지정된 된 작업에 대 한 제한 시간 값을 설정 하 고 CLR의 작업이 수행 될 때 수행 해야 정책 작업을 지정 합니다.|  
|[SetUnhandledExceptionPolicy 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrpolicymanager-setunhandledexceptionpolicy-method.md)|처리 되지 않은 예외가 발생 하면 CLR의 동작을 지정 합니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [EClrFailure 열거형](../../../../docs/framework/unmanaged-api/hosting/eclrfailure-enumeration.md)
- [EClrOperation 열거형](../../../../docs/framework/unmanaged-api/hosting/eclroperation-enumeration.md)
- [EPolicyAction 열거형](../../../../docs/framework/unmanaged-api/hosting/epolicyaction-enumeration.md)
- [ICLRControl 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrcontrol-interface.md)
