---
title: '방법: CLR 활성화 문제 디버깅'
ms.date: 03/30/2017
helpviewer_keywords:
- CLR activation, debugging issues
ms.assetid: 4fe17546-d56e-4344-a930-6d8e4a545914
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 89724e9a322f2f28dbe5d18ae697acbdd0a32d8e
ms.sourcegitcommit: 9bd8f213b50f0e1a73e03bd1e840c917fbd6d20a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50041624"
---
# <a name="how-to-debug-clr-activation-issues"></a>방법: CLR 활성화 문제 디버깅
응용 프로그램이 올바른 버전의 CLR(공용 언어 런타임)로 실행되도록 하는 데 문제가 있는 경우 CLR 활성화 로그를 보고 디버그할 수 있습니다. 이러한 로그는 응용 프로그램이 예상과 다른 CLR 버전을 로드하거나 CLR을 로드하지 않을 때 활성화 문제의 근본 원인을 파악하는 데 매우 유용할 수 있습니다. [.NET Framework 초기화 오류: 사용자 경험 관리](../../../docs/framework/deployment/initialization-errors-managing-the-user-experience.md)에서는 응용 프로그램에 대한 CLR이 없는 경우의 경험에 대해 설명합니다.  
  
 HKEY_LOCAL_MACHINE 레지스트리 키 또는 시스템 환경 변수를 통해 시스템 전체에서 CLR 활성화 로깅을 사용하도록 설정할 수 있습니다. 레지스트리 항목 또는 환경 변수를 제거할 때까지 로그가 생성됩니다. 또는 사용자 또는 프로세스 로컬 환경 변수를 통해 다양한 범위와 기간으로 로깅을 사용하도록 설정할 수 있습니다.  
  
 CLR 활성화 로그와 [어셈블리 바인딩 로그](../../../docs/framework/tools/fuslogvw-exe-assembly-binding-log-viewer.md)는 완전히 다르므로 혼동하면 안 됩니다.  
  
## <a name="to-enable-clr-activation-logging"></a>CLR 활성화 로깅을 사용하도록 설정하려면  
  
#### <a name="using-the-registry"></a>레지스트리 사용  
  
1.  레지스트리 편집기에서 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework(32비트 컴퓨터) 또는 HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\\.NETFramework 폴더(64비트 컴퓨터)로 이동합니다.  
  
2.  `CLRLoadLogDir`이라는 문자열 값을 추가하고 CLR 활성화 로그를 저장할 기존 디렉터리의 전체 경로로 설정합니다.  
  
 문자열 값을 제거할 때까지 활성화 로깅이 계속 사용됩니다.  
  
#### <a name="using-an-environment-variable"></a>환경 변수 사용  
  
-   CLR 활성화 로그를 저장할 기존 디렉터리의 전체 경로를 나타내는 문자열로 `COMPLUS_CLRLoadLogDir` 환경 변수를 설정합니다.  
  
     환경 변수를 설정하는 방법에 따라 해당 범위가 결정됩니다.  
  
    -   시스템 수준에서 설정하는 경우 환경 변수를 제거할 때까지 해당 컴퓨터의 모든 .NET Framework 응용 프로그램에 대해 활성화 로깅이 사용됩니다.  
  
    -   사용자 수준에서 설정하는 경우 현재 사용자 계정에 대해서만 활성화 로깅이 사용됩니다. 환경 변수를 제거할 때까지 로깅이 계속됩니다.  
  
    -   CLR을 로드하기 전에 프로세스 내에서 설정하는 경우 프로세스가 종료될 때까지 활성화 로깅이 사용됩니다.  
  
    -   응용 프로그램을 실행하기 전에 명령 프롬프트에서 설정하는 경우 해당 명령 프롬프트에서 실행되는 모든 응용 프로그램에 대해 활성화 로깅이 사용됩니다.  
  
     예를 들어 프로세스 수준 범위로 c:\clrloadlogs 디렉터리에 활성화 로그를 저장하려면 응용 프로그램을 실행하기 전에 명령 프롬프트 창을 열고 다음을 입력합니다.  
  
    ```  
    set COMPLUS_CLRLoadLogDir=c:\clrloadlogs  
    ```  
  
## <a name="example"></a>예  
 CLR 활성화 로그는 CLR 활성화 및 CLR 호스팅 API 사용에 대한 많은 양의 데이터를 제공합니다. 이 데이터는 대부분 Microsoft 내부에서 사용되지만 일부 데이터는 이 문서의 설명과 같이 개발자에게도 유용할 수 있습니다.  
  
 로그는 CLR 호스팅 API가 호출된 순서를 반영합니다. 또한 컴퓨터에서 검색된 설치된 런타임 집합에 대한 유용한 데이터도 포함합니다. CLR 활성화 로그 형식 자체는 문서화되지 않지만 CLR 활성화 문제를 해결해야 하는 개발자를 지원하는 데 사용될 수 있습니다.  
  
> [!NOTE]
>  CLR을 사용하는 프로세스가 종료될 때까지 활성화 로그를 열 수 없습니다.  
  
> [!NOTE]
>  CLR 활성화 로그는 지역화되지 않으며 항상 영어로 생성됩니다.  
  
 활성화 로그의 다음 예제에서는 가장 유용한 정보가 강조 표시되고 로그 다음에 설명됩니다.  
  
```  
532,205950.367,CLR Loading log for C:\Tests\myapp.exe   
532,205950.367,Log started at 4:26:12 PM on 10/6/2011   
532,205950.367,-----------------------------------   
532,205950.382,FunctionCall: _CorExeMain   
532,205950.382,FunctionCall: ClrCreateInstance, Clsid: {2EBCD49A-1B47-4A61-B13A-4A03701E594B}, Iid: {E2190695-77B2-492E-8E14-C4B3A7FDD593}   
532,205950.382,MethodCall: ICLRMetaHostPolicy::GetRequestedRuntime. Version: (null), Metahost Policy Flags: 0x168, Binary: (null), Iid: {BD39D1D2-BA2F-486A-89B0-B4B0CB466891}   
532,205950.382,Installed Runtime: v4.0.30319. VERSION_ARCHITECTURE: 0   
532,205950.382,Input values for ComputeVersionString follow this line   
532,205950.382,-----------------------------------   
532,205950.382,Default Application Name: C:\Tests\myapp.exe   
532,205950.382,IsLegacyBind is: 0   
532,205950.382,IsCapped is 0   
532,205950.382,SkuCheckFlags are 0   
532,205950.382,ShouldEmulateExeLaunch is 0   
532,205950.382,LegacyBindRequired is 0   
532,205950.382,-----------------------------------   
532,205950.382,Parsing config file: C:\Tests\myapp.exe   
532,205950.382,UseLegacyV2RuntimeActivationPolicy is set to 0   
532,205950.382,LegacyFunctionCall: GetFileVersion. Filename: C:\Tests\myapp.exe   
532,205950.382,LegacyFunctionCall: GetFileVersion. Filename: C:\Tests\myapp.exe   
532,205950.382,C:\Tests\myapp.exe was built with version: v2.0.50727   
532,205950.382,ERROR: Version v2.0.50727 is not present on the machine.   
532,205950.398,SEM_FAILCRITICALERRORS is set to 0   
532,205950.398,Launching feature-on-demand installation. CmdLine: C:\Windows\system32\fondue.exe /enable-feature:NetFx3   
532,205950.398,FunctionCall: RealDllMain. Reason: 0   
532,205950.398,FunctionCall: OnShimDllMainCalled. Reason: 0  
```  
  
-   **CLR 로드 로그**에서는 관리 코드를 로드하는 프로세스를 시작한 실행 파일의 경로를 제공합니다. 이는 기본 호스트일 수 있습니다.  
  
    ```  
    532,205950.367,CLR Loading log for C:\Tests\myapp.exe  
    ```  
  
-   **설치된 런타임**은 활성화 요청의 후보가 되는, 컴퓨터에 설치된 CLR 버전 집합입니다.  
  
    ```  
    532,205950.382,Installed Runtime: v4.0.30319. VERSION_ARCHITECTURE: 0  
    ```  
  
-   **built with version**은 [ICLRMetaHostPolicy::GetRequestedRuntime](../../../docs/framework/unmanaged-api/hosting/iclrmetahostpolicy-getrequestedruntime-method.md) 등의 메서드에 제공된 이진 파일을 작성하는 데 사용된 CLR 버전입니다.  
  
    ```  
    532,205950.382,C:\Tests\myapp.exe was built with version: v2.0.50727  
    ```  
  
-   **feature-on-demand installation**은 Windows 8에서 .NET Framework 3.5를 사용하는 경우를 가리킵니다. 이 시나리오에 대한 자세한 내용은 [.NET Framework 초기화 오류: 사용자 환경 관리](../../../docs/framework/deployment/initialization-errors-managing-the-user-experience.md)를 참조하세요.  
  
    ```  
    532,205950.398,Launching feature-on-demand installation. CmdLine: C:\Windows\system32\fondue.exe /enable-feature:NetFx3  
    ```  
  
## <a name="see-also"></a>참고 항목  
- [배포](../../../docs/framework/deployment/index.md)  
- [방법: .NET Framework 4 또는 4.5를 지원하도록 앱 구성](../../../docs/framework/migration-guide/how-to-configure-an-app-to-support-net-framework-4-or-4-5.md)
