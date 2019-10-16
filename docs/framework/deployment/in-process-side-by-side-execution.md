---
title: In-Process Side-by-Side 실행
ms.date: 03/30/2017
helpviewer_keywords:
- in-process side-by-side execution
- side-by-side execution, in-process
ms.assetid: 18019342-a810-4986-8ec2-b933a17c2267
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 2a33d3c4216ed8c5d79aef4017c6b9256fc1ad7c
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71052097"
---
# <a name="in-process-side-by-side-execution"></a>In-Process Side-by-Side 실행
.NET Framework 4부터 In-Process Side-By-Side 호스팅을 사용하여 단일 프로세스에서 여러 버전의 CLR(공용 언어 런타임)을 실행할 수 있습니다. 기본적으로 관리되는 COM 구성 요소는 프로세스에 대해 로드된 .NET Framework 버전에 관계없이 빌드 시 사용된 .NET Framework 버전을 사용하여 실행됩니다.  
  
## <a name="background"></a>배경  
 .NET Framework는 관리 코드 애플리케이션에 대해 항상 병렬 호스팅을 제공하지만 .NET Framework 4 이전에는 관리되는 COM 구성 요소에 대해 해당 기능을 제공하지 않았습니다. 과거에는 프로세스에 로드된 관리되는 COM 구성 요소를 이미 로드된 런타임 버전 또는 설치된 최신 버전의 .NET Framework로 실행했습니다. 이 버전이 COM 구성 요소와 호환되지 않으면 구성 요소가 실패합니다.  
  
 .NET Framework 4에서는 다음을 보장하는 병렬 호스팅에 대한 새로운 접근 방법을 제공합니다.  
  
- 새로운 버전의 .NET Framework를 설치해도 기존 애플리케이션에는 영향이 없습니다.  
  
- 빌드 시 사용된 .NET Framework 버전에 대해 애플리케이션이 실행됩니다. 명시적으로 지정되지 않은 경우 새로운 버전의 .NET Framework를 사용하지 않습니다. 그러나 애플리케이션이 새로운 버전의 .NET Framework 사용으로 전환하는 것이 더 편리합니다.  
  
## <a name="effects-on-users-and-developers"></a>사용자와 개발자에 대한 영향  
  
- **최종 사용자 및 시스템 관리자**. 이제 이러한 사용자가 독립적으로 또는 애플리케이션을 사용하여 새로운 버전의 런타임을 설치할 때 컴퓨터에 영향을 주지 않을 것을 확신할 수 있습니다. 기존 애플리케이션은 예전과 같이 계속 실행됩니다.  
  
- **애플리케이션 개발자**. 병렬 호스팅은 애플리케이션 개발자에게 거의 영향을 주지 않습니다. 기본적으로 애플리케이션은 항상 빌드 시 사용된 .NET Framework 버전에서 실행되며, 이 동작은 변경되지 않았습니다. 그러나 개발자가 이 동작을 재정의하고 애플리케이션이 최신 버전의 .NET Framework에서 실행되도록 지정할 수 있습니다([시나리오 2](#scenarios) 참조).  
  
- **라이브러리 개발자 및 소비자**. 병렬 호스팅은 라이브러리 개발자가 직면하는 호환성 문제를 해결하지 않습니다. 직접 참조를 통해 또는 <xref:System.Reflection.Assembly.Load%2A?displayProperty=nameWithType> 호출을 통해 애플리케이션에서 직접 로드하는 라이브러리는 로드된 <xref:System.AppDomain>의 런타임을 계속 사용합니다. 지원하려는 모든 버전의 .NET Framework에 대해 라이브러리를 테스트해야 합니다. .NET Framework 4 런타임을 사용하여 애플리케이션이 컴파일되었지만 이전 런타임을 사용하여 빌드된 라이브러리를 포함하는 경우 해당 라이브러리는 .NET Framework 4 런타임도 사용합니다. 그러나 이전 런타임을 사용하여 빌드된 애플리케이션과 .NET Framework 4를 사용하여 빌드된 라이브러리가 있는 경우 애플리케이션이 .NET Framework 4도 사용하도록 강제 적용해야 합니다([시나리오 3](#scenarios) 참조).  
  
- **관리되는 COM 구성 요소 개발자**. 과거에는 관리되는 COM 구성 요소가 자동으로 컴퓨터에 설치된 최신 버전의 런타임을 사용하여 실행되었습니다. 이제 빌드 시 사용된 런타임 버전에서 COM 구성 요소를 실행할 수 있습니다.  
  
     다음 표와 같이 .NET Framework 버전 1.1로 빌드된 구성 요소를 버전 4 구성 요소와 함께 나란히 실행할 수 있지만 버전 2.0, 3.0 또는 3.5 구성 요소의 경우 해당 버전에 병렬 호스팅을 사용할 수 없기 때문에 병렬 실행할 수 없습니다.  
  
    |.NET Framework 버전|1.1|2.0 - 3.5|4|  
    |----------------------------|---------|----------------|-------|  
    |1.1|적용할 수 없음|아니요|예|  
    |2.0 - 3.5|아니요|적용할 수 없음|예|  
    |4|예|예|적용할 수 없음|  
  
> [!NOTE]
> .NET Framework 버전 3.0 및 3.5는 버전 2.0에서 증분 방식으로 빌드되었으며 병렬 실행할 필요가 없습니다. 이들은 기본적으로 동일한 버전입니다.  
  
<a name="scenarios"></a>   
## <a name="common-side-by-side-hosting-scenarios"></a>일반적인 병렬 호스팅 시나리오  
  
- **시나리오 1:** 이전 버전의 .NET Framework를 사용하여 빌드된 COM 구성 요소를 사용하는 네이티브 애플리케이션.  
  
     설치된 .NET Framework 버전: .NET Framework 4 및 COM 구성 요소에서 사용하는 다른 모든 버전의 .NET Framework.  
  
     할 일: 이 시나리오에서는 수행할 작업이 없습니다. COM 구성 요소는 등록된 .NET Framework 버전과 함께 실행됩니다.  
  
- **시나리오 2**: .NET Framework 2.0 SP1로 빌드된 관리형 애플리케이션은 .NET Framework 2.0에서 실행하는 것을 선호하지만, 버전 2.0이 없을 경우 .NET Framework 4에서 실행하려고 합니다.  
  
     설치된 .NET Framework 버전: .NET Framework 및 .NET Framework 4의 이전 버전.  
  
     할 일: 애플리케이션 디렉터리의 [애플리케이션 구성 파일](../configure-apps/index.md)에서 [\<startup> 요소](../configure-apps/file-schema/startup/startup-element.md) 및 [\<supportedRuntime> 요소](../configure-apps/file-schema/startup/supportedruntime-element.md) 집합을 다음과 같이 사용합니다.  
  
    ```xml  
    <configuration>  
      <startup >  
        <supportedRuntime version="v2.0.50727" />  
        <supportedRuntime version="v4.0" />  
      </startup>  
    </configuration>  
    ```  
  
- **시나리오 3:** .NET Framework 4에서 실행하려는 이전 버전의 .NET Framework를 사용하여 빌드된 COM 구성 요소를 사용하는 네이티브 애플리케이션.  
  
     설치된 .NET Framework 버전: .NET Framework 4.  
  
     할 일: 애플리케이션 디렉터리의 애플리케이션 구성 파일에서 `useLegacyV2RuntimeActivationPolicy` 특성이 `true`로 설정된 `<startup>` 요소 및 `<supportedRuntime>` 요소 집합을 다음과 같이 사용합니다.  
  
    ```xml  
    <configuration>  
      <startup useLegacyV2RuntimeActivationPolicy="true">  
        <supportedRuntime version="v4.0" />  
      </startup>  
    </configuration>  
    ```  
  
## <a name="example"></a>예  
 다음 예제에서는 구성 요소가 사용하도록 컴파일된 .NET Framework 버전을 사용하여 관리되는 COM 구성 요소를 실행하는 관리되지 않는 COM 호스트를 보여 줍니다.  
  
 다음 예제를 실행하려면 .NET Framework 3.5를 사용하여 다음 관리 COM 구성 요소를 컴파일하고 등록합니다. 구성 요소를 등록하려면 **프로젝트** 메뉴에서 **속성**을 클릭하고 **빌드** 탭을 클릭한 다음 **COM Interop 등록** 확인란을 선택합니다.  
  
```csharp
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using System.Runtime.InteropServices;  
  
namespace BasicComObject  
{  
    [ComVisible(true), Guid("9C99C4B5-CA54-4c58-8988-49B6811BA53B")]  
    public class MyObject : SimpleObjectModel.IPrintInfo  
    {  
        public MyObject()  
        {  
        }  
        public void PrintInfo()  
        {  
            Console.WriteLine("MyObject was activated in {0} runtime in:\n\tAppDomain {1}:{2}", System.Runtime.InteropServices.RuntimeEnvironment.GetSystemVersion(), AppDomain.CurrentDomain.Id, AppDomain.CurrentDomain.FriendlyName);  
        }  
    }  
}  
```  
  
 앞의 예제에서 만든 COM 개체를 활성화하는 다음과 같은 관리되지 않는 C++ 애플리케이션을 컴파일합니다.  
  
```cpp
#include "stdafx.h"  
#include <string>  
#include <iostream>  
#include <objbase.h>  
#include <string.h>  
#include <process.h>  
  
using namespace std;  
  
int _tmain(int argc, _TCHAR* argv[])  
{  
    char input;  
    CoInitialize(NULL) ;  
    CLSID clsid;  
    HRESULT hr;  
    HRESULT clsidhr = CLSIDFromString(L"{9C99C4B5-CA54-4c58-8988-49B6811BA53B}",&clsid);  
    hr = -1;  
    if (FAILED(clsidhr))  
    {  
        printf("Failed to construct CLSID from String\n");  
    }  
    UUID id = __uuidof(IUnknown);  
    IUnknown * pUnk = NULL;  
    hr = ::CoCreateInstance(clsid,NULL,CLSCTX_INPROC_SERVER,id,(void **) &pUnk);  
    if (FAILED(hr))  
    {  
        printf("Failed CoCreateInstance\n");  
    }else  
    {  
        pUnk->AddRef();  
        printf("Succeeded\n");  
    }  
  
    DISPID dispid;  
    IDispatch* pPrintInfo;  
    pUnk->QueryInterface(IID_IDispatch, (void**)&pPrintInfo);  
    OLECHAR FAR* szMethod[1];  
    szMethod[0]=OLESTR("PrintInfo");   
    hr = pPrintInfo->GetIDsOfNames(IID_NULL,szMethod, 1, LOCALE_SYSTEM_DEFAULT, &dispid);  
    DISPPARAMS dispparams;  
    dispparams.cNamedArgs = 0;  
    dispparams.cArgs = 0;  
    VARIANTARG* pvarg = NULL;  
    EXCEPINFO * pexcepinfo = NULL;  
    WORD wFlags = DISPATCH_METHOD ;  
;  
    LPVARIANT pvRet = NULL;  
    UINT * pnArgErr = NULL;  
    hr = pPrintInfo->Invoke(dispid,IID_NULL, LOCALE_USER_DEFAULT, wFlags,  
        &dispparams, pvRet, pexcepinfo, pnArgErr);  
    printf("Press Enter to exit");  
    scanf_s("%c",&input);  
    CoUninitialize();  
    return 0;  
}  
```  
  
## <a name="see-also"></a>참고 항목

- [\<startup> 요소](../configure-apps/file-schema/startup/startup-element.md)
- [\<supportedRuntime> 요소](../configure-apps/file-schema/startup/supportedruntime-element.md)
