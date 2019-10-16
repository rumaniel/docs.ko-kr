---
title: IHostAssemblyStore::ProvideAssembly 메서드
ms.date: 03/30/2017
api_name:
- IHostAssemblyStore.ProvideAssembly
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostAssemblyStore::ProvideAssembly
helpviewer_keywords:
- ProvideAssembly method [.NET Framework hosting]
- IHostAssemblyStore::ProvideAssembly method [.NET Framework hosting]
ms.assetid: 625c3dd5-a3f0-442c-adde-310dadbb5054
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: f5fab4ef0d67ab6b86510bd4b2f814d9456213fb
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67763986"
---
# <a name="ihostassemblystoreprovideassembly-method"></a>IHostAssemblyStore::ProvideAssembly 메서드
참조 되지 않은 어셈블리에 대 한 참조를 가져옵니다 합니다 [ICLRAssemblyReferenceList](../../../../docs/framework/unmanaged-api/hosting/iclrassemblyreferencelist-interface.md) 에서 반환 되는 [ihostassemblymanager:: Getnonhoststoreassemblies](../../../../docs/framework/unmanaged-api/hosting/ihostassemblymanager-getnonhoststoreassemblies-method.md)합니다. 호출 하는 CLR (공용 언어 런타임) `ProvideAssembly` 목록에 나타나지 않는 각 어셈블리에 대 한 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
HRESULT ProvideAssembly (  
    [in]  AssemblyBindInfo *pBindInfo,  
    [out] UINT64           *pAssemblyId,  
    [out] UINT64           *pHostContext,  
    [out] IStream          **ppStmAssemblyImage,  
    [out] IStream          **ppStmPDB  
);  
```  
  
## <a name="parameters"></a>매개 변수  
 `pBindInfo`  
 [in] 에 대 한 포인터를 [AssemblyBindInfo](../../../../docs/framework/unmanaged-api/hosting/assemblybindinfo-structure.md) 버전 관리 정책의 유무를 포함 하 여 특정 바인딩 특성을 결정 하는 호스트 인스턴스 및 바인딩할 어셈블리입니다.  
  
 `pAssemblyId`  
 [out] 이 요청된 된 어셈블리에 대 한 고유 식별자에 대 한 포인터 `IStream`합니다.  
  
 `pHostContext`  
 [out] 플랫폼에 대 한 필요 없이 요청된 된 어셈블리의 증명 정보를 확인 하는 데 사용 되는 호스트 관련 데이터에 대 한 포인터를 호출 합니다. `pHostContext` 에 해당 하는 <xref:System.Reflection.Assembly.HostContext%2A> 관리 되는 속성 <xref:System.Reflection.Assembly> 클래스입니다.  
  
 `ppStmAssemblyImage`  
 [out] 주소에 대 한 포인터는 `IStream` 를 로드할 어셈블리를 찾을 수 없는 경우 null 또는 이식 가능한 실행 파일 (PE) 이미지를 포함 하는 합니다.  
  
 `ppStmPDB`  
 [out] 주소에 대 한 포인터는 `IStream` 경우 포함 된 null을 프로그램 디버그 (PDB) 정보를.pdb 파일을 찾을 수 없습니다.  
  
## <a name="return-value"></a>반환 값  
  
|HRESULT|Description|  
|-------------|-----------------|  
|S_OK|`ProvideAssembly` 성공적으로 반환 합니다.|  
|HOST_E_CLRNOTAVAILABLE|CLR이 로드 된 프로세스에 또는 CLR 상태인는 관리 코드를 실행 하거나 호출을 처리할 수 없습니다.|  
|HOST_E_TIMEOUT|호출 시간이 초과 되었습니다.|  
|HOST_E_NOT_OWNER|호출자가 잠금을 소유 하지 않습니다.|  
|HOST_E_ABANDONED|이벤트가 차단 된 스레드가 취소 된 또는 파이버를 대기 하 고 있습니다.|  
|E_FAIL|알 수 없는 치명적인 오류가 발생 했습니다. 메서드 E_FAIL을 반환 하는 경우 CLR은 프로세스 내에서 사용할 수 없습니다. 메서드를 호스트 하는 데 대 한 후속 호출 HOST_E_CLRNOTAVAILABLE를 반환 합니다.|  
|COR_E_FILENOTFOUND (0X80070002)|요청된 된 어셈블리를 찾을 수 없습니다.|  
|E_NOT_SUFFICIENT_BUFFER|지정 된 버퍼 크기가 `pAssemblyId` 호스트 반환 하려고 하는 식별자를 보유할 만큼 크지 않습니다.|  
  
## <a name="remarks"></a>설명  
 에 대 한 id 값을 반환 `pAssemblyId` 호스트에 의해 지정 됩니다. 식별자는 프로세스의 수명 내에서 고유 해야 합니다. CLR은 스트림에 대 한 고유 식별자로이 값을 사용 합니다. 값에 대해 각 값을 검사 `pAssemblyId` 에 대 한 다른 호출에서 반환 된 `ProvideAssembly`합니다. 동일한 호스트 반환 `pAssemblyId` 다른 값 `IStream`, CLR 해당 스트림의 내용을 이미 매핑되는지 여부를 확인 합니다. 그렇다면 런타임 대신 새 이미지의 기존 복사본을 로드 합니다.  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MSCorEE.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [ICLRAssemblyReferenceList 인터페이스](../../../../docs/framework/unmanaged-api/hosting/iclrassemblyreferencelist-interface.md)
- [IHostAssemblyManager 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihostassemblymanager-interface.md)
- [IHostAssemblyStore 인터페이스](../../../../docs/framework/unmanaged-api/hosting/ihostassemblystore-interface.md)
