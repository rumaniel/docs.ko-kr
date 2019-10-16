---
title: 사용되지 않는 CLR 호스팅 함수
ms.date: 03/30/2017
helpviewer_keywords:
- .NET Framework 1.1, hosting global static functions
- global static functions [.NET Framework hosting], version 2.0
- .NET Framework 2.0, hosting global static functions
- hosting global static functions [.NET Framework], version 2.0
ms.assetid: 91fbbb35-e543-4814-b806-371cebae8c5a
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: dde711f2d626d88fd80009fa83f1198dd9d47810
ms.sourcegitcommit: 155012a8a826ee8ab6aa49b1b3a3b532e7b7d9bd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66490486"
---
# <a name="deprecated-clr-hosting-functions"></a>사용되지 않는 CLR 호스팅 함수
이 섹션에서는 호스팅 API의 이전 버전에서 사용 되는 관리 되지 않는 전역 정적 함수를 설명 합니다.  
  
 인프라 기능을 제외 하 고 (`_Cor*` 함수),.NET Framework 에서만 사용 되는, 이러한 함수는.NET Framework 4에서 되지 않습니다.  
  
## <a name="activation-functions"></a>활성화 함수  
 [ClrCreateManagedInstance 함수](../../../../docs/framework/unmanaged-api/hosting/clrcreatemanagedinstance-function.md)  
 더 이상 사용되지 않습니다. 지정 된 관리 되는 형식의 인스턴스를 만듭니다.  
  
 [CoInitializeCor 함수](../../../../docs/framework/unmanaged-api/hosting/coinitializecor-function.md)  
 사용되지 않습니다. CLR (공용 언어 런타임)을 초기화 하려면 [CorBindToRuntimeEx](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md) 하거나 [CorBindToCurrentRuntime](../../../../docs/framework/unmanaged-api/hosting/corbindtocurrentruntime-function.md)합니다.  
  
 [CoInitializeEE 함수](../../../../docs/framework/unmanaged-api/hosting/coinitializeee-function.md)  
 더 이상 사용되지 않습니다. CLR 실행 엔진이 프로세스에 로드 되도록 합니다. 사용 된 [iclrruntimehost:: Start](../../../../docs/framework/unmanaged-api/hosting/iclrruntimehost-start-method.md) 메서드 대신 합니다.  
  
 [CorBindToCurrentRuntime 함수](../../../../docs/framework/unmanaged-api/hosting/corbindtocurrentruntime-function.md)  
 더 이상 사용되지 않습니다. XML 파일에 저장 된 버전 정보를 사용 하 여 프로세스에는 CLR (공용 언어 런타임)을 로드 합니다.  
  
 [CorBindToRuntime 함수](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntime-function.md)  
 더 이상 사용되지 않습니다. 관리 되지 않는 호스트에서 CLR을 프로세스로 로드할 수 있도록 합니다.  
  
 [CorBindToRuntimeByCfg 함수](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimebycfg-function.md)  
 더 이상 사용되지 않습니다. XML 파일에서 읽은 버전 정보를 사용 하 여 CLR을 프로세스로 로드 합니다.  
  
 [CorBindToRuntimeEx 함수](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md)  
 더 이상 사용되지 않습니다. 관리 되지 않는 호스트가 CLR을 프로세스로 로드할 수 있으며 CLR의 동작을 지정 하는 플래그를 설정할 수 있습니다.  
  
 [CorBindToRuntimeHost 함수](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimehost-function.md)  
 더 이상 사용되지 않습니다. 호스트를 지정된 된 버전의 CLR 프로세스로 로드할 수 있습니다.  
  
 [GetCORRequiredVersion 함수](../../../../docs/framework/unmanaged-api/hosting/getcorrequiredversion-function.md)  
 더 이상 사용되지 않습니다. 필요한 CLR 버전 번호를 가져옵니다.  
  
 [GetCORSystemDirectory 함수](../../../../docs/framework/unmanaged-api/hosting/getcorsystemdirectory-function.md)  
 더 이상 사용되지 않습니다. 프로세스에 로드 된 CLR의 설치 디렉터리를 반환 합니다.  
  
 [GetRealProcAddress 함수](../../../../docs/framework/unmanaged-api/hosting/getrealprocaddress-function.md)  
 더 이상 사용되지 않습니다. CLR의 최신 설치 버전에서 내보낸 지정 된 함수의 주소를 가져옵니다.  
  
 [GetRequestedRuntimeInfo 함수](../../../../docs/framework/unmanaged-api/hosting/getrequestedruntimeinfo-function.md)  
 더 이상 사용되지 않습니다. 응용 프로그램에서 요청한 CLR에 대 한 버전 및 디렉터리 정보를 가져옵니다.  
  
## <a name="clr-version-functions"></a>CLR 버전 함수  
 이 단원의 함수는 CLR 버전;를 반환합니다. CLR를 활성화 하지 마십시오.  
  
 [GetCORVersion 함수](../../../../docs/framework/unmanaged-api/hosting/getcorversion-function.md)  
 더 이상 사용되지 않습니다. 현재 프로세스에서 실행 되는 CLR의 버전 번호를 반환 합니다.  
  
 [GetFileVersion 함수](../../../../docs/framework/unmanaged-api/hosting/getfileversion-function.md)  
 더 이상 사용되지 않습니다. 지정된 된 버퍼를 사용 하 여 지정된 된 파일의 CLR 버전 정보를 가져옵니다.  
  
 [GetRequestedRuntimeVersion 함수](../../../../docs/framework/unmanaged-api/hosting/getrequestedruntimeversion-function.md)  
 더 이상 사용되지 않습니다. 지정된 된 응용 프로그램에서 요청한 CLR의 버전 번호를 가져옵니다. 해당 버전이 설치 되지 않은 경우 요청 된 버전 보다 먼저 설치 되는 최신 버전을 가져옵니다.  
  
 [GetRequestedRuntimeVersionForCLSID 함수](../../../../docs/framework/unmanaged-api/hosting/getrequestedruntimeversionforclsid-function.md)  
 더 이상 사용되지 않습니다. 지정된 된 CLSID 사용 하 여 클래스에 대 한 적절 한 CLR 버전 정보를 가져옵니다.  
  
 [GetVersionFromProcess 함수](../../../../docs/framework/unmanaged-api/hosting/getversionfromprocess-function.md)  
 더 이상 사용되지 않습니다. 지정 된 프로세스 핸들에 연관 된 CLR의 버전 번호를 가져옵니다.  
  
 [LockClrVersion 함수](../../../../docs/framework/unmanaged-api/hosting/lockclrversion-function.md)  
 더 이상 사용되지 않습니다. 호스트가 명시적으로 CLR을 초기화 하기 전에 프로세스 내에서 사용할는 CLR의 버전을 결정할 수 있습니다.  
  
## <a name="hosting-functions"></a>호스팅 함수  
 [CallFunctionShim 함수](../../../../docs/framework/unmanaged-api/hosting/callfunctionshim-function.md)  
 더 이상 사용되지 않습니다. 지정한 이름 및 매개 변수는 지정 된 라이브러리에 있는 함수를 호출 합니다.  
  
 [CoEEShutDownCOM 함수](../../../../docs/framework/unmanaged-api/hosting/coeeshutdowncom-function.md)  
 더 이상 사용되지 않습니다. 프로세스에서 COM 어셈블리를 언로드합니다.  
  
 [CorExitProcess 함수](../../../../docs/framework/unmanaged-api/hosting/corexitprocess-function.md)  
 더 이상 사용되지 않습니다. 현재 관리 되지 않는 프로세스를 종료합니다.  
  
 [CorLaunchApplication 함수](../../../../docs/framework/unmanaged-api/hosting/corlaunchapplication-function.md)  
 더 이상 사용되지 않습니다. 지정한 매니페스트 및 기타 응용 프로그램 데이터를 사용 하 여 지정 된 네트워크 경로에서 응용 프로그램을 시작 합니다.  
  
 [CorMarkThreadInThreadPool 함수](../../../../docs/framework/unmanaged-api/hosting/cormarkthreadinthreadpool-function.md)  
 더 이상 사용되지 않습니다. 관리 코드의 실행에 대 한 현재 실행 중인 스레드 풀 스레드를 표시합니다. .NET Framework 버전 2.0부터,이 함수는 효과가 없습니다. 필요 하지 않습니다 하 고 코드에서 제거할 수 있습니다.  
  
 [CoUninitializeCor 함수](../../../../docs/framework/unmanaged-api/hosting/couninitializecor-function.md)  
 사용되지 않습니다. CLR은 프로세스에서 언로드할 수 없습니다.  
  
 [CoUninitializeEE 함수](../../../../docs/framework/unmanaged-api/hosting/couninitializeee-function.md)  
 사용되지 않습니다.  
  
 [CreateDebuggingInterfaceFromVersion 함수](../../../../docs/framework/unmanaged-api/hosting/createdebugginginterfacefromversion-function.md)  
 더 이상 사용되지 않습니다. 만듭니다는 [ICorDebug](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md) 개체 정보를 기반으로 지정 된 버전입니다.  
  
 [CreateICeeFileGen 함수](../../../../docs/framework/unmanaged-api/hosting/createiceefilegen-function.md)  
 더 이상 사용되지 않습니다. 만듭니다는 [ICeeFileGen](../../../../docs/framework/unmanaged-api/hosting/iceefilegen-class.md) 개체입니다.  
  
 [DestroyICeeFileGen 함수](../../../../docs/framework/unmanaged-api/hosting/destroyiceefilegen-function.md)  
 더 이상 사용되지 않습니다. 제거는 [ICeeFileGen](../../../../docs/framework/unmanaged-api/hosting/iceefilegen-class.md) 개체입니다.  
  
 [FExecuteInAppDomainCallback 함수 포인터](../../../../docs/framework/unmanaged-api/hosting/fexecuteinappdomaincallback-function-pointer.md)  
 더 이상 사용되지 않습니다. CLR 호출 관리 코드를 실행 하는 함수를 가리킵니다.  
  
 [FLockClrVersionCallback 함수 포인터](../../../../docs/framework/unmanaged-api/hosting/flockclrversioncallback-function-pointer.md)  
 더 이상 사용되지 않습니다. CLR 호스트에 알리기 위해 호출 하는 함수를 가리킵니다 해당 초기화가 시작 또는 완료 합니다.  
  
 [GetCLRIdentityManager 함수](../../../../docs/framework/unmanaged-api/hosting/getclridentitymanager-function.md)  
 더 이상 사용되지 않습니다. CLR id를 관리할 수 있도록 하는 인터페이스에 대 한 포인터를 가져옵니다.  
  
 [LoadLibraryShim 함수](../../../../docs/framework/unmanaged-api/hosting/loadlibraryshim-function.md)  
 더 이상 사용되지 않습니다. 지정된 된 버전의.NET Framework DLL을 로드합니다.  
  
 [LoadStringRC 함수](../../../../docs/framework/unmanaged-api/hosting/loadstringrc-function.md)  
 더 이상 사용되지 않습니다. HRESULT 값을 현재 스레드의 기본 문화권을 사용 하 여 오류 메시지로 변환 합니다.  
  
 [LoadStringRCEx 함수](../../../../docs/framework/unmanaged-api/hosting/loadstringrcex-function.md)  
 더 이상 사용되지 않습니다. 지정된 된 문화권에 대 한 적절 한 오류 메시지에는 HRESULT 값으로 변환합니다.  
  
 [LPOVERLAPPED_COMPLETION_ROUTINE 함수 포인터](../../../../docs/framework/unmanaged-api/hosting/lpoverlapped-completion-routine-function-pointer.md)  
 더 이상 사용되지 않습니다. Overlapped는 호스트에 알리는 함수를 가리키는 (즉, 비동기) 장치에는 I/O 완료 합니다.  
  
 [LPTHREAD_START_ROUTINE 함수 포인터](../../../../docs/framework/unmanaged-api/hosting/lpthread-start-routine-function-pointer.md)  
 더 이상 사용되지 않습니다. 스레드 실행을 시작 했음을 호스트에 알리는 함수를 가리킵니다.  
  
 [RunDll32ShimW 함수](../../../../docs/framework/unmanaged-api/hosting/rundll32shimw-function.md)  
 더 이상 사용되지 않습니다. 지정된 명령을 실행합니다.  
  
 [WAITORTIMERCALLBACK 함수 포인터](../../../../docs/framework/unmanaged-api/hosting/waitortimercallback-function-pointer.md)  
 더 이상 사용되지 않습니다. 대기 핸들 중 신호 되었거나 시간이 초과 되었습니다 호스트에 알리는 함수를 가리킵니다.  
  
## <a name="infrastructure-functions"></a>인프라 함수  
 이 섹션의 함수는.NET Framework에서 사용 됩니다.  
  
 [_CorDllMain 함수](../../../../docs/framework/unmanaged-api/hosting/cordllmain-function.md)  
 CLR을 초기화 하 고 DLL 어셈블리의 CLR 헤더에서 관리 되는 진입점을 찾고 실행을 시작 합니다.  
  
 [_CorExeMain 함수](../../../../docs/framework/unmanaged-api/hosting/corexemain-function.md)  
 CLR을 초기화 하 고 실행 가능한 어셈블리의 CLR 헤더에서 관리 되는 진입점을 찾고 실행을 시작 합니다.  
  
 [_CorExeMain2 함수](../../../../docs/framework/unmanaged-api/hosting/corexemain2-function.md)  
 지정된 된 메모리 매핑된 코드에서 진입점을 실행합니다. 이 함수는 운영 체제 로더에 의해 호출 됩니다.  
  
 [_CorImageUnloading 함수](../../../../docs/framework/unmanaged-api/hosting/corimageunloading-function.md)  
 관리 되는 모듈 이미지가 언로드될 때 로더에 알립니다.  
  
 [_CorValidateImage 함수](../../../../docs/framework/unmanaged-api/hosting/corvalidateimage-function.md)  
 관리 되는 모듈 이미지의 유효성을 검사 하 고 로드 된 후 운영 체제 로더에 알립니다.  
  
## <a name="see-also"></a>참고자료

- [.NET Framework 4 호스팅 전역 정적 함수](../../../../docs/framework/unmanaged-api/hosting/net-framework-4-hosting-global-static-functions.md)
