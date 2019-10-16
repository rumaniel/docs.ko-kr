---
title: Mpgo.exe(관리되는 프로필 기반 최적화 도구)
ms.date: 03/30/2017
helpviewer_keywords:
- Mpgo.exe
- training scenarios, generating profiles with
- Managed Profile Guided Optimization Tool
- Ngen.exe
- Ngen.exe, profilers and native images
ms.assetid: f6976502-a000-4fbe-aaf5-a7aab9ce4ec2
author: mairaw
ms.author: mairaw
ms.openlocfilehash: e8c9093faa80249a2c5898c1f250e97208764be6
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71044405"
---
# <a name="mpgoexe-managed-profile-guided-optimization-tool"></a>Mpgo.exe(관리되는 프로필 기반 최적화 도구)

관리되는 프로필 기반 최적화 도구(Mpgo.exe)는 공통 최종 사용자 시나리오를 사용하여 [네이티브 이미지 생성기(Ngen.exe)](ngen-exe-native-image-generator.md)로 만들어지는 네이티브 이미지 어셈블리를 최적화하는 명령줄 도구입니다. 이 도구를 사용하면 프로필 데이터를 생성하는 교육 시나리오를 실행할 수 있습니다. [네이티브 이미지 생성기(Ngen.exe)](ngen-exe-native-image-generator.md)는 이 데이터를 사용하여 생성된 네이티브 이미지 애플리케이션 어셈블리를 최적화합니다. 교육 시나리오는 애플리케이션의 정상적 용도에 대한 평가 실행입니다. Mpgo.exe는 Visual Studio Ultimate 2012 이상 버전에서 사용할 수 있습니다. Visual Studio 2013부터 Mpgo.exe를 사용하여 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱을 최적화할 수도 있습니다.  
  
프로필 기반 최적화는 교육 시나리오에서 데이터를 수집하고 네이티브 이미지의 레이아웃을 최적화하는 데 사용하여 애플리케이션 시작 시간, 메모리 사용률(작업 집합 크기), 처리량을 개선합니다.  
  
중간 언어(IL) 어셈블리에 대한 시작 시간 및 작업 집합에서 성능 문제가 발생하면 먼저 Ngen.exe를 사용하여 JIT(Just-In-Time) 컴파일 비용을 제거하고 코드 공유를 지원하는 것이 좋습니다. 추가 개선이 필요한 경우 Mpgo.exe를 사용하여 애플리케이션을 더 최적화할 수 있습니다. 최적화되지 않은 네이티브 이미지 어셈블리의 성능 데이터를 성능 향상을 평가하는 기준선으로 사용할 수 있습니다. Mpgo.exe를 사용하면 콜드 시작 시간이 단축되고 작업 집합 크기가 작아질 수 있습니다. Mpgo.exe는 Ngen.exe가 정보 최적화 네이티브 이미지 어셈블리를 생성하는 데 사용하는 정보를 IL 어셈블리에 추가합니다. 자세한 내용은 .NET 블로그의 [데스크톱 애플리케이션의 시작 성능 개선](https://go.microsoft.com/fwlink/p/?LinkId=248943) 항목을 참조하세요.  
  
이 도구는 자동으로 Visual Studio와 함께 설치됩니다. 도구를 실행하려면 Visual Studio용 개발자 명령 프롬프트(또는 Windows 7의 Visual Studio 명령 프롬프트)를 관리자 자격 증명과 함께 사용하고 다음 명령 프롬프트를 입력합니다. 자세한 내용은 [명령 프롬프트](developer-command-prompt-for-vs.md)를 참조하세요.  
  
데스크톱 응용 프로그램:  
  
```console  
mpgo –Scenario <command> [-Import <directory>] –AssemblyList <assembly1>  <assembly2> ... -OutDir <directory> [options]  
```  
  
[!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 응용 프로그램:  
  
## <a name="syntax"></a>구문  
  
```console  
mpgo –Scenario <packageName> -AppID <appId> -Timeout <seconds>  
```  
  
## <a name="parameters"></a>매개 변수  
 Mpgo.exe에 대한 모든 인수는 대/소문자를 구분하지 않습니다. 명령에 대시가 접두사로 붙습니다.  
  
> [!NOTE]
> `–Scenario` 또는 `–Import`를 필수 명령으로 사용할 수 있지만 둘 다 사용할 수는 없습니다. `–Reset` 옵션을 지정하는 경우 필수 매개 변수는 사용되지 않습니다.

|필수적 매개 변수|설명|
|------------------------|-----------------|
|`-Scenario` \<*command*><br /><br /> 또는<br /><br /> `-Scenario` \<*packageName*><br /><br /> 또는<br /><br /> `-Import` \<*directory*>|데스크톱 앱의 경우 `–Scenario`를 사용하여 명령줄 인수 등의 최적화할 애플리케이션을 실행할 명령을 지정합니다. 공백이 포함된 경로를 지정하는 경우 *command*에 세 개의 큰따옴표를 사용합니다(예: `mpgo.exe -scenario """C:\My App\myapp.exe""" -assemblylist """C:\My App\myapp.exe""" -outdir "C:\optimized files"`). *command*에 공백이 포함되어 있는 경우 큰따옴표를 사용하면 제대로 작동하지 않으므로 큰따옴표를 사용하지 마세요.<br /><br /> 또는<br /><br /> [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱의 경우 `–Scenario`를 사용하여 프로필 정보를 생성할 패키지를 지정합니다. 전체 패키지 이름 대신 패키지의 표시 이름 또는 패키지 제품군 이름을 지정하는 경우, Mpgo.exe는 일치 항목이 하나뿐이면 사용자가 입력한 이름과 일치하는 패키지를 선택합니다. 여러 패키지가 지정된 이름과 일치하는 경우, Mpgo.exe는 패키지를 선택하라는 메시지를 표시합니다.<br /><br /> 또는<br /><br /> `-Import`를 사용하여 이전에 최적화된 어셈블리의 최적화 데이터가 `-AssemblyList`에서 어셈블리를 최적화하는 데 사용해야 함을 지정합니다. *directory*는 이전에 최적화된 파일이 들어있는 디렉터리를 지정합니다. `–AssemblyList` 또는 `–AssemblyListFile`에서 지정된 어셈블리는 가져온 파일의 데이터를 사용하여 최적화할 어셈블리의 새 버전입니다. 이전 어셈블리 버전의 최적화 데이터를 사용하면 시나리오를 다시 실행하지 않고도 새 버전의 어셈블리를 최적화할 수 있습니다.  그러나 가져온 어셈블리와 대상 어셈블리가 현저히 다른 코드를 포함하는 경우, 최적화 데이터의 효율성이 저하됩니다. `–AssemblyList` 또는 `–AssemblyListFile`에 지정된 어셈블리 이름은 `–Import`*directory*로 지정된 디렉터리에 있어야 합니다. 공백이 포함된 경로를 지정하는 경우 *directory*를 세 개의 큰따옴표로 묶습니다.<br /><br /> `–Scenario` 또는 `–Import` 매개 변수를 지정해야 하지만 둘 다 지정할 수는 없습니다.|
|`-OutDir` \<*directory*>|최적화된 어셈블리를 저장할 디렉터리 출력 디렉터리 폴더에 어셈블리가 이미 있으면, 새 복사본이 생성되고 이름에 인덱스 번호가 추가됩니다(예: *assemblyname*-1.exe). 공백이 포함된 경로를 지정하는 경우 *directory*를 큰따옴표로 묶습니다.|
|`-AssemblyList` \<*assembly1 assembly2 ...* ><br /><br /> 또는<br /><br /> `-AssemblyListFile` \<*file*>|공백으로 분리된 프로필 정보를 수집할 어셈블리(.exe 및 .dll 파일 등)의 목록 `C:\Dir\*.dll` 또는 `*.dll`을 지정하여 지정된 또는 현재 작업 디렉터리에 있는 모든 어셈블리를 선택할 수 있습니다. 자세한 내용은 설명 부분을 참조하세요.<br /><br /> 또는<br /><br /> 줄당 하나의 어셈블리로 나열된 어셈블리에 대한 프로필 정보를 수집한 어셈블리 목록이 포함된 텍스트 파일 어셈블리 이름이 하이픈(-)으로 시작되면 어셈블리 파일 목록을 사용하거나 어셈블리의 이름을 변경합니다.|
|`-AppID` \<*appId*>|지정된 패키지에 있는 애플리케이션의 ID입니다. 와일드카드(\*)를 사용하는 경우, Mpgo.exe는 패키지에서 AppID를 열거하려고 하고, 실패하는 경우 \<*package_family_name*>!App으로 대체합니다. 앞에 느낌표(!)가 있는 문자열을 지정하는 경우, Mpgo.exe는 제공되는 인수를 사용하여 패키지 제품군 이름을 연결합니다.|
|`-Timeout` \<*seconds*>|응용 프로그램이 종료되기 전에 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 응용 프로그램을 실행할 수 있는 시간|

|선택적 매개 변수|설명|
|------------------------|-----------------|
|`-64bit`|64비트 시스템의 어셈블리를 계측합니다.  64비트로 자체 어셈블리를 선언하더라도 64비트 어셈블리에 대해 이 매개 변수를 지정해야 합니다.|
|`-ExeConfig` \<*filename*>|시나리오가 버전 및 로더 정보를 제공하기 위해 사용하는 구성 파일을 지정합니다.|
|`-f`|서명을 했더라도 바이너리 어셈블리에 프로필 데이터를 강제로 포함되게 합니다.  어셈블리에 서명했더라도 다시 서명해야 합니다. 그렇지 않으면 어셈블리가 로드 및 실행되지 않습니다.|
|`-Reset`|환경을 다시 설정하여 종료된 프로파일링 세션이 어셈블리에 영향을 주지 않음을 확인한 다음 끝냅니다. 기본적으로 환경은 프로파일링 세션 전후 다시 설정됩니다.|
|`-Timeout` \<*time in seconds*>|프로파일링 지속 시간을 초 단위로 지정합니다. GUI 애플리케이션에는 관찰한 시작 시간보다 조금 더 높은 값을 사용합니다. 시간 제한 기간이 끝나면 애플리케이션이 계속 실행되어도 프로필 데이터가 기록됩니다. 이 옵션을 설정하지 않으면 애플리케이션 종료까지 프로파일링이 계속되며, 애플리케이션이 종료하는 시점에 데이터가 기록됩니다.|
|`-LeaveNativeImages`|시나리오를 실행한 후에 계측된 네이티브 이미지가 삭제되지 않도록 지정합니다. 이 옵션은 실행 중인 시나리오에 지정한 애플리케이션을 가져올 때 주로 사용됩니다. 이렇게 하면 Mpgo.exe의 후속 실행에 대한 네이티브 이미지가 다시 작성되지 않습니다. 애플리케이션의 실행을 종료하면 이 옵션을 지정하는 경우 캐시에 고아가 된 원시 이미지가 있을 수 있습니다. 이 경우 Mpgo.exe를 동일한 시나리오 및 어셈블리 목록을 사용하여 실행하고 `–RemoveNativeImages` 매개 변수를 사용하여 원시 이미지를 제거합니다.|
|`-RemoveNativeImages`|`–LeaveNativeImages`가 지정된 실행에서 정리합니다. `-RemoveNativeImages`를 지정하는 경우, Mpgo.exe는 `-64bit` 및 `–AssemblyList`를 제외한 모든 인수를 무시하고 계측된 모든 네이티브 이미지를 삭제한 후 종료됩니다.|

## <a name="remarks"></a>설명
 명령줄에서 `–AssemblyList` 및 `- AssemblyListFile`을 여러 번 사용할 수 있습니다.

 어셈블리를 지정할 때 전체 경로 이름을 지정하지 않으면 Mpgo.exe는 현재 디렉터리에서 찾습니다. 잘못된 경로를 지정하는 경우 Mpgo.exe는 오류 메시지를 표시하지만 다른 어셈블리에 대한 데이터는 계속 생성합니다. 교육 시나리오 중 로드되지 않은 어셈블리를 지정하는 경우 해당 어셈블리에 대해 교육 데이터가 생성되지 않습니다.

 목록의 어셈블리가 전역 어셈블리 캐시에 있는 경우 프로필 정보를 포함하도록 업데이트되지 않습니다.  전역 어셈블리 캐시에서 제거하여 프로필 정보를 수집합니다.

 미리 컴파일된 네이티브 이미지의 장점은 일반적으로 런타임에서 중요한 JIT 컴파일을 제거하는 경우에만 확인되기 때문에, Ngen.exe 및 Mpgo.exe는 대형의 관리된 애플리케이션에만 사용하는 것이 좋습니다. 작업 집합을 많이 사용하지 않는 "Hello World" 스타일의 애플리케이션에서는 Mpgo.exe을 실행해도 어떠한 이점도 없을 것이고, Mpgo.exe는 프로필 데이터 수집에도 실패할 수 있습니다.

> [!NOTE]
> Ngen.exe 및 Mpgo.exe는 ASP.NET 애플리케이션 및 WCF(Windows Communication Foundation) 서비스에 권장되지 않습니다.  
  
## <a name="to-use-mpgoexe"></a>Mpgo.exe를 사용하려면  
  
1. Visual Studio Ultimate 2012와 애플리케이션이 설치된 컴퓨터를 사용합니다.  
  
2. Mpgo.exe를 관리자 권한으로 필요한 매개 변수를 사용하여 실행합니다.  샘플 명령은 다음 단원을 참조하십시오.  
  
     최적화된 IL(중간 언어) 어셈블리는 `–OutDir` 매개 변수로 지정된 폴더(이 예제에서는 `C:\Optimized` 폴더)에 생성됩니다.  
  
3. Ngen.exe에 사용한 IL 어셈블리를 `–OutDir`로 지정된 디렉터리의 프로필 정보가 포함된 새로운 IL 어셈블리로 바꿉니다.  
  
4. 애플리케이션을 설정하면(Mpgo.exe에서 제공하는 이미지를 사용) 최적화된 원시 이미지가 설치됩니다.  
  
## <a name="suggested-workflow"></a>제안된 워크플로  
  
1. Mpgo.exe를 `–Scenario` 매개 변수와 함께 사용하여 최적화된 IL 어셈블리 집합을 만듭니다.  
  
2. 소스 제어에 최적화된 IL 어셈블리를 확인합니다.  
  
3. 빌드 프로세스에서, 최적화된 IL 이미지를 생성하여 Ngen.exe에 전달하기 위한 빌드 후 단계로 `–Import` 매개 변수와 함께 Mpgo.exe를 호출합니다.  
  
 이렇게 하면 모든 어셈블리의 데이터가 최적화됩니다. 최적화된 어셈블리 업데이트(1단계와 2단계)를 더 자주 체크 인하는 경우, 성능 수치의 일관성이 제품 개발 과정 전체에 걸쳐 향상됩니다.  
  
## <a name="using-mpgoexe-from-visual-studio"></a>Visual Studio에서 Mpgo.exe 사용  
 Visual Studio의 Mpgo.exe를 다음과 같은 제한에 따라 실행할 수 있습니다([방법: 빌드 이벤트 지정(C#)](/visualstudio/ide/how-to-specify-build-events-csharp) 참조).  
  
- Visual Studio 매크로도 기본적으로 후행 슬래시 기호를 사용하기 때문에 따옴표로 묶은 경로를 후행 슬래시 기호와 함께 사용할 수 없습니다. 예를 들어 `–OutDir "C:\Output Folder\"`는 올바르지 않습니다. 이 제한을 해결하려면 후행 슬래시를 이스케이프할 수 있습니다. 예를 들어 `-OutDir "$(OutDir)\"`을 대신 사용합니다.  
  
- 기본적으로 Mpgo.exe는 Visual Studio 빌드 경로에 없습니다. Visual Studio에 경로를 추가하거나 또는 Mpgo 명령줄에서 전체 경로를 지정해야 합니다. Visual Studio의 빌드 후 이벤트에서 `–Scenario` 또는 `–Import` 매개 변수를 사용할 수 있습니다. 그러나 일반적인 프로세스는 Visual Studio용 개발자 명령 프롬프트에서 `–Scenario`를 한 번 사용한 후 `–Import`를 사용하여 각 빌드 후 최적화된 어셈블리를 업데이트하는 것입니다(예: `"C:\Program Files\Microsoft Visual Studio 11.0\Team Tools\Performance Tools\mpgo.exe" -import "$(OutDir)tmp" -assemblylist "$(TargetPath)" -outdir "$(OutDir)\"`).  
  
<a name="samples"></a>   
## <a name="examples"></a>예  
 Visual Studio용 개발자 명령 프롬프트의 다음 Mpgo.exe 명령은 세금 애플리케이션을 최적화합니다.  
  
```console  
mpgo –scenario "C:\MyApp\MyTax.exe /params par" –AssemblyList Mytax.dll MyTaxUtil2011.dll –OutDir C:\Optimized –TimeOut 15  
```  
  
 다음 Mpgo.exe 명령은 사운드 애플리케이션을 최적화합니다.  
  
```console  
mpgo –scenario "C:\MyApp\wav2wma.exe –input song1.wav –output song1.wma" –AssemblyList transcode.dll –OutDir C:\Optimized –TimeOut 15  
```  
  
 다음 Mpgo.exe 명령은 이전에 최적화된 어셈블리의 데이터를 사용하여 새 버전의 어셈블리를 최적화합니다.  
  
```console  
mpgo.exe -import "C:\Optimized" -assemblylist "C:\MyApp\MyTax.dll" "C:\MyApp\MyTaxUtil2011.dll" -outdir C:\ReOptimized  
```  
  
## <a name="see-also"></a>참고 항목

- [Ngen.exe(네이티브 이미지 생성기)](ngen-exe-native-image-generator.md)
- [명령 프롬프트](developer-command-prompt-for-vs.md)
- [데스크톱 애플리케이션의 시작 성능 개선](https://go.microsoft.com/fwlink/p/?LinkId=248943)
- [.NET 4.5의 성능 개선 개요](https://go.microsoft.com/fwlink/p/?LinkId=249131)
