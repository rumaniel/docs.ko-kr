---
title: IHostSecurityManager 인터페이스
ms.date: 03/30/2017
api_name:
- IHostSecurityManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostSecurityManager
helpviewer_keywords:
- IHostSecurityManager interface [.NET Framework hosting]
ms.assetid: c3be2cbd-2d93-438b-9888-9a0251b63c03
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a2c71f32dfd190e188bb28aad5d51c72160eb4bc
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64603250"
---
# <a name="ihostsecuritymanager-interface"></a>IHostSecurityManager 인터페이스
에 대 한 액세스 및 현재 실행 중인 스레드의 보안 컨텍스트를 제어할 수 있는 방법을 제공 합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[GetSecurityContext 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostsecuritymanager-getsecuritycontext-method.md)|요청 된 가져옵니다 [IHostSecurityContext](../../../../docs/framework/unmanaged-api/hosting/ihostsecuritycontext-interface.md) 호스트에서 합니다.|  
|[ImpersonateLoggedOnUser 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostsecuritymanager-impersonateloggedonuser-method.md)|요청 된 현재 사용자 id의 자격 증명을 사용 하 여 코드를 실행 하는 합니다.|  
|[OpenThreadToken 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostsecuritymanager-openthreadtoken-method.md)|현재 스레드와 연결 된 임의 액세스 토큰을 엽니다.|  
|[RevertToSelf 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostsecuritymanager-reverttoself-method.md)|현재 사용자 id의 가장을 종료 하 고 원래 스레드 토큰을 반환 합니다.|  
|[SetSecurityContext 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostsecuritymanager-setsecuritycontext-method.md)|현재 실행 중인 스레드에 대 한 보안 컨텍스트를 설정합니다.|  
|[SetThreadToken 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostsecuritymanager-setthreadtoken-method.md)|현재 실행 중인 스레드에 대 한 핸들을 설정합니다.|  
  
## <a name="remarks"></a>설명  
 호스트는 CLR (공용 언어 런타임)와 사용자 코드에서 스레드 토큰에 대 한 모든 코드 액세스를 제어할 수 있습니다. 전체 보안을 보장할 수도 있습니다 비동기 작업이 나 제한 된 코드 액세스를 사용 하 여 코드 포인트 컨텍스트 정보가 전달 됩니다. `IHostSecurityContext` CLR에 불투명이 보안 컨텍스트 정보를 캡슐화 합니다.  
  
 CLR 관리 되는 스레드 컨텍스트를 내부적으로 처리합니다. 프로세스 관련 쿼리 `IHostSecurityManager` 다음과 같은 경우에서:  
  
- 종료자 스레드 종료 자가 실행 중입니다.  
  
- 클래스 및 모듈 생성자 실행 중  
  
- 작업자 스레드에 대 한 호출에 비동기 지점에는 [ihostthreadpoolmanager:: Queueuserworkitem](../../../../docs/framework/unmanaged-api/hosting/ihostthreadpoolmanager-queueuserworkitem-method.md) 메서드.  
  
- I/O 완료 포트의 서비스입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [IHostSecurityContext 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihostsecuritycontext-interface.md)
- [호스팅 인터페이스](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
