---
title: ICLRAssemblyIdentityManager 인터페이스
ms.date: 03/30/2017
api_name:
- ICLRAssemblyIdentityManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRAssemblyIdentityManager
helpviewer_keywords:
- ICLRAssemblyIdentityManager interface [.NET Framework hosting]
ms.assetid: 6a81c6fe-cc22-4062-ae27-d6eeee03a7b9
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2b209e568b1e65ed785155d045cd48d1248672da
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61985038"
---
# <a name="iclrassemblyidentitymanager-interface"></a>ICLRAssemblyIdentityManager 인터페이스
호스트 및 어셈블리에 대 한 공용 언어 런타임 (CLR) 간의 통신을 지 원하는 메서드를 제공 합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[GetBindingIdentityFromFile 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrassemblyidentitymanager-getbindingidentityfromfile-method.md)|지정된 된 파일 경로에서 어셈블리에 대 한 데이터 바인딩 어셈블리 id를 가져옵니다.|  
|[GetBindingIdentityFromStream 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrassemblyidentitymanager-getbindingidentityfromstream-method.md)|지정한 스트림에서 어셈블리에 대 한 정식 어셈블리 id 데이터를 가져옵니다.|  
|[GetCLRAssemblyReferenceList 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrassemblyidentitymanager-getclrassemblyreferencelist-method.md)|가져옵니다는 [ICLRAssemblyReferenceList](../../../../docs/framework/unmanaged-api/hosting/iclrassemblyreferencelist-interface.md) 부분 어셈블리 id의 제공 된 목록에서 인스턴스.|  
|[GetProbingAssembliesFromReference 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrassemblyidentitymanager-getprobingassembliesfromreference-method.md)|가져옵니다는 [ICLRProbingAssemblyEnum](../../../../docs/framework/unmanaged-api/hosting/iclrprobingassemblyenum-interface.md) 지정된 된 id 사용 하 여 어셈블리에서 참조 된 어셈블리 id에 대 한 열거자입니다.|  
|[GetReferencedAssembliesFromFile 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrassemblyidentitymanager-getreferencedassembliesfromfile-method.md)|가져옵니다는 [ICLRReferenceAssemblyEnum](../../../../docs/framework/unmanaged-api/hosting/iclrreferenceassemblyenum-interface.md) 지정된 된 파일 경로에서 어셈블리에 의해 참조 되는 어셈블리의 목록을 포함 하는 인스턴스.|  
|[GetReferencedAssembliesFromStream 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrassemblyidentitymanager-getreferencedassembliesfromstream-method.md)|포인터를 가져는 `ICLRReferenceAssemblyEnum` 에 지정 된 스트림에 있는 어셈블리에서 참조 하는 어셈블리에 대 한 어셈블리 id 데이터를 포함 하는 개체입니다.|  
|[IsStronglyNamed 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrassemblyidentitymanager-isstronglynamed-method.md)|지정된 된 어셈블리에 강력한 이름을 지정 하는지 여부를 나타내는 값을 가져옵니다.|  
  
## <a name="remarks"></a>설명  
 사용 하 여 `ICLRAssemblyIdentityManager` 의 인스턴스를 가져오는 `ICLRAssemblyReferenceList` 및 어셈블리 id를 열거 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICLRAssemblyReferenceList 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrassemblyreferencelist-interface.md)
- [ICLRProbingAssemblyEnum 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrprobingassemblyenum-interface.md)
- [호스팅 인터페이스](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
