---
title: ICLRStrongName2 인터페이스
ms.date: 03/30/2017
api_name:
- ICLRStrongName2
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName2
helpviewer_keywords:
- ICLRStrongName2 interface [.NET Framework hosting]
ms.assetid: 9f098a74-201e-4628-a468-8dee9ab99b4a
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6bf9e3d2df8f507e118b393007c3958358a830cc
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61763726"
---
# <a name="iclrstrongname2-interface"></a>ICLRStrongName2 인터페이스
보안 해시 알고리즘 (SHA-256, SHA-384 및 SHA-512)의 sha-2 그룹을 사용 하 여 강력한 이름을 만드는 기능을 제공 합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[StrongNameGetPublicKeyEx 메서드](../../../../docs/framework/unmanaged-api/hosting/strongnamegetpublickeyex-method.md)|공개/개인 키 쌍에서 공개 키를 가져옵니다 하 고 해시 알고리즘 및 서명 알고리즘을 지정 합니다.|  
|[StrongNameSignatureVerificationEx2 메서드](../../../../docs/framework/unmanaged-api/hosting/strongnamesignatureverificationex2-method.md)|강력한 이름의 어셈블리의 서명을 확인 하 고 실제 키에 대 한 매핑을 ECMA 키에서를 제공 합니다.|  
  
## <a name="remarks"></a>설명  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MetaHost.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]
