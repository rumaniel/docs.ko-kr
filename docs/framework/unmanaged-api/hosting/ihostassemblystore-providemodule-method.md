---
title: IHostAssemblyStore::ProvideModule 메서드
ms.date: 03/30/2017
api_name:
- IHostAssemblyStore.ProvideModule
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostAssemblyStore::ProvideModule
helpviewer_keywords:
- IHostAssemblyStore::ProvideModule method [.NET Framework hosting]
- ProvideModule method [.NET Framework hosting]
ms.assetid: f42e3dd0-c88e-4748-b6c0-4c515a633180
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9290fd70b17b5a6456d85cb4b037ebbc62e028f8
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67763982"
---
# <a name="ihostassemblystoreprovidemodule-method"></a>IHostAssemblyStore::ProvideModule 메서드
어셈블리 또는 연결 된 (그러나 포함이 아님) 내의 모듈 리소스 파일을 확인합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT ProvideModule (  
    [in]  ModuleBindInfo *pBindInfo,  
    [out] DWORD          *pdwModuleId,  
    [out] IStream        **ppStmModuleImage,  
    [out] IStream        **ppStmPDB  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pBindInfo`  
 [in] 에 대 한 포인터를 [ModuleBindInfo](../../../../docs/framework/unmanaged-api/hosting/modulebindinfo-structure.md) 요청된 된 모듈을 설명 하는 인스턴스 <xref:System.AppDomain>, 어셈블리 및 모듈 이름입니다.  
  
 `pdwModuleId`  
 [out] 에 대 한 고유 식별자에 대 한 포인터를 `IStream` 로드 된 모듈을 포함 합니다.  
  
 `ppStmModuleImage`  
 [out] 주소에 대 한 포인터는 `IStream` 이식 가능한 실행 파일 (PE) 이미지를 로드할 수를 포함 하는 개체 또는 모듈을 찾을 수 없는 경우 null입니다.  
  
 `ppStmPDB`  
 [out] 주소에 대 한 포인터는 `IStream` 요청된 된 모듈에 대 한 프로그램 디버그 (PDB) 정보를 포함 하는 개체 또는.pdb 파일을 찾을 수 없는 경우 null입니다.  
  
## <a name="return-value"></a>반환 값  
  
|HRESULT|Description|  
|-------------|-----------------|  
|S_OK|`ProvideModule` 성공적으로 반환 합니다.|  
|HOST_E_CLRNOTAVAILABLE|프로세스에는 CLR (공용 언어 런타임)에 로드 되지 또는 CLR 상태인는 관리 코드를 실행 하거나 호출을 처리할 수 없습니다.|  
|HOST_E_TIMEOUT|호출 시간이 초과 되었습니다.|  
|HOST_E_NOT_OWNER|호출자가 잠금을 소유 하지 않습니다.|  
|HOST_E_ABANDONED|이벤트가 차단 된 스레드가 취소 된 또는 파이버를 대기 하 고 있습니다.|  
|E_FAIL|알 수 없는 치명적인 오류가 발생 했습니다. 메서드 E_FAIL을 반환 하는 경우 CLR은 프로세스 내에서 사용할 수 없습니다. 메서드를 호스트 하는 데 대 한 후속 호출 HOST_E_CLRNOTAVAILABLE를 반환 합니다.|  
|COR_E_FILENOTFOUND (0X80070002)|요청 된 어셈블리 또는 연결 된 리소스를 찾을 수 없습니다.|  
|E_NOT_SUFFICIENT_BUFFER|`pdwModuleId` 호스트를 반환 하려고 하는 식별자를 포함 하도록 충분히 크지 않습니다.|  
  
## <a name="remarks"></a>설명  
 에 대 한 id 값을 반환 `pdwModuleId` 호스트에 의해 지정 됩니다. 식별자는 프로세스의 수명 내에서 고유 해야 합니다. CLR 연결 된 스트림에 대 한 고유 식별자로이 값을 사용 합니다. 값에 대해 각 값을 검사 하 `pAssemblyId` 에 대 한 호출에서 반환 된 [ProvideAssembly](../../../../docs/framework/unmanaged-api/hosting/ihostassemblystore-provideassembly-method.md) 에 대 한 값과 비교 하 고 `pdwModuleId` 에 대 한 다른 호출에서 반환 된 `ProvideModule`합니다. 호스트가 다른 같은 식별자 값을 반환 하는 경우 `IStream`, CLR 해당 스트림의 내용을 이미 매핑되는지 여부를 확인 합니다. 그렇다면 새 매핑 대신 이미지의 기존 복사본을 CLR에 로드 합니다. 따라서 식별자도 겹치지 않아야에서 반환 된 어셈블리 식별자를 사용 하 여 `ProvideAssembly`입니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICLRAssemblyReferenceList 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrassemblyreferencelist-interface.md)
- [IHostAssemblyManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihostassemblymanager-interface.md)
- [IHostAssemblyStore 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihostassemblystore-interface.md)
