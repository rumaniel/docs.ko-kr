---
title: '방법: 등록이 필요 없는 활성화를 위한 .NET Framework 기반 COM 구성 요소 구성'
ms.date: 03/30/2017
helpviewer_keywords:
- components [.NET Framework], manifest
- application manifests [.NET Framework]
- manifests [.NET Framework]
- registration-free COM interop, configuring .NET-based components
- activation, registration-free
ms.assetid: 32f8b7c6-3f73-455d-8e13-9846895bd43b
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: baabff187fb8a22aea37c4fb4c1dc11a680d3bb8
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70853846"
---
# <a name="how-to-configure-net-framework-based-com-components-for-registration-free-activation"></a>방법: 등록이 필요 없는 활성화를 위한 .NET Framework 기반 COM 구성 요소 구성
.NET Framework 기반 구성 요소에 대한 등록 없는 활성화는 COM 구성 요소보다 약간 더 복잡합니다. 설치 프로그램에 다음 두 개의 매니페스트가 필요합니다.  
  
- COM 애플리케이션이 관리되는 구성 요소를 식별하려면 Win32 스타일 애플리케이션 매니페스트가 있어야 합니다.  
  
- .NET Framework 기반 구성 요소에는 런타임에 필요한 활성화 정보를 위해 구성 요소 매니페스트가 있어야 합니다.  
  
 이 항목에서는 애플리케이션 매니페스트를 애플리케이션에 연결하고, 구성 요소 매니페스트를 구성 요소에 연결하며, 구성 요소 매니페스트를 어셈블리에 포함하는 방법을 설명합니다.  
  
### <a name="to-create-an-application-manifest"></a>애플리케이션 매니페스트를 만들려면  
  
1. XML 편집기를 사용하여 하나 이상의 관리되는 구성 요소와 상호 운용되는 COM 애플리케이션이 소유하는 애플리케이션 매니페스트를 만들거나 수정합니다.  
  
2. 파일의 시작 부분에 다음과 같은 표준 헤더를 삽입합니다.  
  
    ```xml  
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>  
    <assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0">  
    ```  
  
     매니페스트 요소와 해당 특성에 대한 자세한 내용을 보려면 [애플리케이션 매니페스트](/windows/desktop/SbsCs/application-manifests)를 참조하세요.  
  
3. 매니페스트의 소유자를 식별합니다. 다음 예제에서는 `myComApp` 버전 1이 매니페스트 파일을 소유합니다.  
  
    ```xml  
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>  
    <assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0">  
      <assemblyIdentity type="win32"   
                        name="myOrganization.myDivision.myComApp"   
                        version="1.0.0.0"   
                        processorArchitecture="msil"   
      />  
    ```  
  
4. 종속 어셈블리를 식별합니다. 다음 예제에서는 `myComApp`이 `myManagedComp`에 종속됩니다.  
  
    ```xml  
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>  
    <assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0">  
      <assemblyIdentity type="win32"   
                        name="myOrganization.myDivision.myComApp"   
                        version="1.0.0.0"   
                        processorArchitecture="x86"   
                        publicKeyToken="8275b28176rcbbef"  
      />  
      <dependency>  
        <dependentAssembly>  
          <assemblyIdentity type="win32"   
                        name="myOrganization.myDivision.myManagedComp"   
                        version="6.0.0.0"   
                        processorArchitecture="X86"   
                        publicKeyToken="8275b28176rcbbef"  
          />  
        </dependentAssembly>  
      </dependency>  
    </assembly>  
    ```  
  
5. 매니페스트 파일을 저장하고 이름을 지정합니다. 애플리케이션 매니페스트 이름은 어셈블리 실행 파일의 이름 뒤에 .manifest 확장명이 추가된 것입니다. 예를 들어 myComApp.exe의 애플리케이션 매니페스트 파일 이름은 myComApp.exe.manifest입니다.  
  
 COM 애플리케이션과 동일한 디렉터리에 애플리케이션 매니페스트를 설치할 수 있습니다. 또는 애플리케이션의 .exe 파일에 리소스로 추가할 수 있습니다. 자세한 내용은 [About Side-by-Side Assemblies](/windows/desktop/SbsCs/about-side-by-side-assemblies-)(Side-by-Side 어셈블리 정보)를 참조하세요.  
  
#### <a name="to-create-a-component-manifest"></a>구성 요소 매니페스트를 만들려면  
  
1. XML 편집기를 사용하여 관리되는 어셈블리를 설명하는 구성 요소 매니페스트를 만듭니다.  
  
2. 파일의 시작 부분에 다음과 같은 표준 헤더를 삽입합니다.  
  
    ```xml  
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>  
    <assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0">  
    ```  
  
3. 파일의 소유자를 식별합니다. 애플리케이션 매니페스트 파일에 있는 `<dependentAssembly>` 요소의 `<assemblyIdentity>` 요소는 구성 요소 매니페스트에 있는 요소와 일치해야 합니다. 다음 예제에서는 `myManagedComp` 버전 1.2.3.4가 매니페스트 파일을 소유합니다.  
  
    ```xml  
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>  
    <assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0">  
           <assemblyIdentity  
                        name="myOrganization.myDivision.myManagedComp"  
                        version="1.2.3.4"  
                        publicKeyToken="8275b28176rcbbef"  
                        processorArchitecture="msil"  
           />  
    ```  
  
4. 어셈블리에 있는 각 클래스를 식별합니다. `<clrClass>` 요소를 사용하여 관리되는 어셈블리에 있는 각 클래스를 고유하게 식별합니다. `<assembly>` 요소의 하위 요소인 요소에는 다음 표에 설명된 특성이 있습니다.  
  
    |특성|설명|필수|  
    |---------------|-----------------|--------------|  
    |`clsid`|활성화할 클래스를 지정하는 식별자입니다.|예|  
    |`description`|구성 요소에 대해 사용자에게 알려주는 문자열입니다. 기본값은 빈 문자열입니다.|아니요|  
    |`name`|관리되는 클래스를 나타내는 문자열입니다.|예|  
    |`progid`|런타임에 바인딩된 활성화에 사용할 식별자입니다.|아니요|  
    |`threadingModel`|COM 스레딩 모델. "Both"가 기본값입니다.|아니요|  
    |`runtimeVersion`|사용할 CLR(공용 언어 런타임) 버전을 지정합니다. 이 특성을 지정하지 않고 CLR이 아직 로드되지 않은 경우 CLR 버전 4 이전의 최신 설치된 CLR과 함께 구성 요소가 로드됩니다. v1.0.3705, v1.1.4322 또는 v2.0.50727을 지정하면 버전이 CLR 버전 4 이전의 최신 설치된 CLR 버전(일반적으로 v2.0.50727)으로 자동으로 롤포워드합니다. 다른 버전의 CLR이 이미 로드되었으며 지정된 버전을 In-Process Side-by-Side로 로드할 수 있는 경우 지정된 버전이 로드되고, 그러지 않으면 로드된 CLR이 사용됩니다. 이 경우 로드에 실패할 수 있습니다.|아니요|  
    |`tlbid`|클래스에 대한 형식 정보를 포함하는 형식 라이브러리의 식별자입니다.|아니요|  
  
     모든 특성 태그는 대/소문자를 구분합니다. OLE/COM ObjectViewer(Oleview.exe)를 사용하여 어셈블리에 대해 내보낸 형식 라이브러리를 보면 CLSID, ProgID, 스레딩 모델, 런타임 버전을 확인할 수 있습니다.  
  
     다음 구성 요소 매니페스트는 `testClass1` 및 `testClass2`라는 두 개의 클래스를 식별합니다.  
  
    ```xml  
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>  
    <assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0">  
           <assemblyIdentity  
                        name="myOrganization.myDivision.myManagedComp"  
                        version="1.2.3.4"   
                        publicKeyToken="8275b28176rcbbef"  
           />  
           <clrClass  
                        clsid="{65722BE6-3449-4628-ABD3-74B6864F9739}"  
                        progid="myManagedComp.testClass1"  
                        threadingModel="Both"  
                        name="myManagedComp.testClass1"  
                        runtimeVersion="v1.0.3705">  
           </clrClass>  
           <clrClass  
                        clsid="{367221D6-3559-3328-ABD3-45B6825F9732}"  
                        progid="myManagedComp.testClass2"  
                        threadingModel="Both"  
                        name="myManagedComp.testClass2"  
                        runtimeVersion="v1.0.3705">  
           </clrClass>  
           <file name="MyManagedComp.dll">  
           </file>  
    </assembly>  
    ```  
  
5. 매니페스트 파일을 저장하고 이름을 지정합니다. 구성 요소 매니페스트 이름은 어셈블리 라이브러리의 이름 뒤에 .manifest 확장명이 추가된 것입니다. 예를 들어 myManagedComp.dll은 myManagedComp.manifest입니다.  
  
 구성 요소 매니페스트를 어셈블리에 리소스로 포함해야 합니다.  
  
#### <a name="to-embed-a-component-manifest-in-a-managed-assembly"></a>관리되는 어셈블리에 구성 요소 매니페스트를 포함하려면  
  
1. 다음 문을 포함하는 리소스 스크립트를 만듭니다.  
  
     `RT_MANIFEST 1 myManagedComp.manifest`  
  
     이 문에서 `myManagedComp.manifest`는 포함되는 구성 요소 매니페스트의 이름입니다. 이 예제에서 스크립트 파일 이름은 `myresource.rc`입니다.  
  
2. Microsoft Windows Resource Compiler(Rc.exe)를 사용하여 스크립트를 컴파일합니다. 명령 프롬프트에 다음 명령을 입력합니다.  
  
     `rc myresource.rc`  
  
     Rc.exe는 `myresource.res` 리소스 파일을 생성합니다.  
  
3. 어셈블리의 소스 파일을 다시 컴파일하고 **/win32res** 옵션을 사용하여 리소스 파일을 지정합니다.  
  
    `/win32res:myresource.res`  
  
     이번에도 `myresource.res`는 포함 리소스를 포함하는 리소스 파일의 이름입니다.  
  
## <a name="see-also"></a>참고 항목

- [등록이 필요 없는 COM interop](registration-free-com-interop.md)
- [등록이 필요 없는 COM Interop에 대한 요구 사항](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/f8h7012w(v=vs.100))
- [등록이 필요 없는 활성화를 위한 COM 구성 요소 구성](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/x65a421a(v=vs.100))
- [.NET 기반 구성 요소의 등록이 필요 없는 활성화: 연습](https://docs.microsoft.com/previous-versions/dotnet/articles/ms973915(v=msdn.10))
