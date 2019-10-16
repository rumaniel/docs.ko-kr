---
title: IHostAssemblyStore 인터페이스
ms.date: 03/30/2017
api_name:
- IHostAssemblyStore
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostAssemblyStore
helpviewer_keywords:
- IHostAssemblyStore interface [.NET Framework hosting]
ms.assetid: cccb650f-abe0-41e2-9fd1-b383788eb1f6
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f881440b2e93745723bd090cfbab0286dcd0a4e5
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69937871"
---
# <a name="ihostassemblystore-interface"></a>IHostAssemblyStore 인터페이스
호스트가 CLR (공용 언어 런타임)과 독립적으로 어셈블리 및 모듈을 로드할 수 있도록 하는 메서드를 제공 합니다.  
  
## <a name="methods"></a>메서드  
  
|메서드|Description|  
|------------|-----------------|  
|[ProvideAssembly 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostassemblystore-provideassembly-method.md)|[IHostAssemblyManager:: Getnonhost 어셈블리](../../../../docs/framework/unmanaged-api/hosting/ihostassemblymanager-getnonhoststoreassemblies-method.md)에 대 한 호출에서 반환 된 [ICLRAssemblyReferenceList](../../../../docs/framework/unmanaged-api/hosting/iclrassemblyreferencelist-interface.md) 가 참조 하지 않는 어셈블리에 대 한 참조를 가져옵니다.|  
|[ProvideModule 메서드](../../../../docs/framework/unmanaged-api/hosting/ihostassemblystore-providemodule-method.md)|어셈블리 또는 연결 된 (포함 되지 않은) 리소스 파일 내에서 모듈을 확인 합니다.|  
  
## <a name="remarks"></a>설명  
 `IHostAssemblyStore`호스트에서 어셈블리 id를 기반으로 어셈블리를 효율적으로 로드할 수 있는 방법을 제공 합니다. 호스트는 바이트를 직접 가리키는 `IStream` 인스턴스를 반환 하 여 어셈블리를 로드 합니다.  
  
 CLR은 초기화 시를 호출 `IHostAssemblyStore` `IHostAssemblyManager::GetNonHostAssemblyStores` 하 여 호스트가 구현 되었는지 여부를 확인 합니다. 이를 통해 호스트는 사용자 어셈블리에 대 한 바인딩을 제어할 수 있을 뿐만 아니라 런타임에 의존 하 여 .NET Framework 어셈블리에 바인딩할 수 있습니다.  
  
> [!NOTE]
> 의 `IHostAssemblyStore`구현을 제공 하는 경우 호스트는에서 `IHostAssemblyManager::GetNonHostStoreAssemblies`반환 된 `ICLRAssemblyReferenceList` 에서 참조 하지 않는 모든 어셈블리를 확인 하는 용도를 지정 합니다.  
  
> [!NOTE]
> .NET Framework 버전 2.0에서는 [네이티브 이미지 생성기 (ngen.exe)](../../../../docs/framework/tools/ngen-exe-native-image-generator.md) 유틸리티에서 제공 하는 것 처럼 호스트에서 어셈블리의 네이티브 이미지를 로드 하는 방법을 제공 하지 않습니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리** Mscoree.dll에 리소스로 포함 됩니다.  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICLRAssemblyReferenceList 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrassemblyreferencelist-interface.md)
- [IHostAssemblyManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihostassemblymanager-interface.md)
- [호스팅 인터페이스](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
