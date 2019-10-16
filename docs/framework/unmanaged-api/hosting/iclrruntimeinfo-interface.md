---
title: ICLRRuntimeInfo 인터페이스
ms.date: 03/30/2017
api_name:
- ICLRRuntimeInfo
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeInfo
helpviewer_keywords:
- ICLRRuntimeInfo interface [.NET Framework hosting]
ms.assetid: 287e5ede-b3a7-4ef8-a756-4fca3f285a82
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 213fa9fda6b154d4548b4163cc7b5890bfcfb49c
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61771727"
---
# <a name="iclrruntimeinfo-interface"></a>ICLRRuntimeInfo 인터페이스
버전, 디렉터리 및 부하 상태를 포함 하 여 특정 공용 언어 런타임 (CLR)에 대 한 정보를 반환 하는 메서드를 제공 합니다. 이 인터페이스는 또한 런타임을 초기화 하지 않고 런타임 관련 기능을 제공 합니다. 여기에 런타임 상대적 [LoadLibrary](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-loadlibrary-method.md) 메서드를 모듈의 특정 런타임 [GetProcAddress](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-getprocaddress-method.md) 메서드를 통해 런타임 제공한 인터페이스는 [GetInterface](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-getinterface-method.md)메서드.  
  
## <a name="methods"></a>메서드  
  
|메서드|설명|  
|------------|-----------------|  
|[BindAsLegacyV2Runtime 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-bindaslegacyv2runtime-method.md)|모든 기존 CLR 버전 2 정품 인증 정책 결정을 위한이 런타임을 바인딩합니다.|  
|[GetDefaultStartupFlags 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-getdefaultstartupflags-method.md)|CLR 시작 플래그와 호스트 구성 파일을 가져옵니다.|  
|[GetInterface 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-getinterface-method.md)|현재 프로세스에 CLR을 로드 하 고 같은 런타임 인터페이스 포인터를 반환 [ICLRRuntimeHost](../../../../docs/framework/unmanaged-api/hosting/iclrruntimehost-interface.md)하십시오 [ICLRStrongName](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-interface.md) 하 고 [IMetaDataDispenser](../../../../docs/framework/unmanaged-api/metadata/imetadatadispenser-interface.md)합니다. 이 메서드를 모두 대체는 `CorBindTo*` 함수입니다.|  
|[GetProcAddress 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-getprocaddress-method.md)|이 인터페이스와 연결 된 CLR에서 내보낸 지정 된 함수의 주소를 가져옵니다. 이 메서드를 대체 합니다 [GetRealProcAddress](../../../../docs/framework/unmanaged-api/hosting/getrealprocaddress-function.md) 메서드.|  
|[GetRuntimeDirectory 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-getruntimedirectory-method.md)|이 인터페이스와 연결 된 CLR의 설치 디렉터리를 가져옵니다. 이 메서드를 대체 합니다 [GetCORSystemDirectory](../../../../docs/framework/unmanaged-api/hosting/getcorsystemdirectory-function.md) 메서드.|  
|[GetVersionString 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-getversionstring-method.md)|연결 된 공용 언어 런타임 (CLR) 버전 정보를 가져옵니다는 주어진 [ICLRRuntimeInfo](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-interface.md) 인터페이스입니다. 이 메서드를 대체 합니다 [GetRequestedRuntimeInfo](../../../../docs/framework/unmanaged-api/hosting/getrequestedruntimeinfo-function.md) 하 고 [GetRequestedRuntimeVersion](../../../../docs/framework/unmanaged-api/hosting/getrequestedruntimeversion-function.md) 메서드.|  
|[IsLoadable 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-isloadable-method.md)|이 인터페이스와 연결 된 런타임 고려 현재 프로세스에 로드할 수 있는지 여부를 나타내는 프로세스에 이미 로드 될 수 있는 다른 런타임과 합니다.|  
|[IsLoaded 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-isloaded-method.md)|CLR 연관 지 여부를 나타내는 합니다 [ICLRRuntimeInfo](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-interface.md) 인터페이스는 프로세스에 로드 됩니다.|  
|[IsStarted 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-isstarted-method.md)|인지 여부를 나타냅니다 CLR을 사용 하 여 연결 합니다 [ICLRRuntimeInfo](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-interface.md) 인터페이스 시작 되었습니다.|  
|[LoadErrorString 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-loaderrorstring-method.md)|HRESULT 값을 지정된 된 문화권에 대 한 적절 한 오류 메시지를 변환 합니다. 이 메서드를 대체 합니다 [LoadStringRC](../../../../docs/framework/unmanaged-api/hosting/loadstringrc-function.md) 하 고 [LoadStringRCEx](../../../../docs/framework/unmanaged-api/hosting/loadstringrcex-function.md) 메서드.|  
|[LoadLibrary 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-loadlibrary-method.md)|라이브러리를 나타내는 CLR의 프레임 워크 디렉터리에서 로드를 [ICLRRuntimeInfo](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-interface.md) 인터페이스입니다. 이 메서드를 대체 합니다 [LoadLibraryShim](../../../../docs/framework/unmanaged-api/hosting/loadlibraryshim-function.md) 메서드.|  
|[SetDefaultStartupFlags 메서드](../../../../docs/framework/unmanaged-api/hosting/iclrruntimeinfo-setdefaultstartupflags-method.md)|CLR 시작 플래그 및 호스트 구성 파일을 설정합니다.|  
  
## <a name="requirements"></a>요구 사항  
 **플랫폼:** [시스템 요구 사항](../../../../docs/framework/get-started/system-requirements.md)을 참조하십시오.  
  
 **헤더:** MetaHost.h  
  
 **라이브러리:** MSCorEE.dll에 리소스로 포함  
  
 **.NET Framework 버전:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>참고자료

- [호스팅 인터페이스](../../../../docs/framework/unmanaged-api/hosting/hosting-interfaces.md)
- [호스팅](../../../../docs/framework/unmanaged-api/hosting/index.md)
