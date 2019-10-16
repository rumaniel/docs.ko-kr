---
title: Al.exe(어셈블리 링커)
ms.date: 03/30/2017
helpviewer_keywords:
- Al.exe
- Assembly Linker
- modules, Assembly Linker
- assembly manifest, Assembly Linker
ms.assetid: b5382965-0053-47cf-b92f-862860275a01
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 7fdb364769be6d8c7c53ca05a7d7cb967678123a
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71044899"
---
# <a name="alexe-assembly-linker"></a>Al.exe(어셈블리 링커)

어셈블리 링커는 모듈 또는 리소스 파일인 하나 이상의 파일에서 어셈블리 매니페스트가 있는 파일을 생성합니다. 모듈이란 어셈블리 매니페스트가 없는 IL(Intermediate Language) 파일입니다.

> [!NOTE]
> Visual Studio 2008부터 C# 및 Visual Basic 컴파일러가 모두 Win32 매니페스트를 어셈블리에 자동으로 포함합니다. 자세한 내용은 [/win32manifest(C# 컴파일러 옵션)](../../csharp/language-reference/compiler-options/win32manifest-compiler-option.md)을 참조하세요.

이 도구는 자동으로 Visual Studio와 함께 설치됩니다. 이 도구를 실행하려면 Visual Studio용 개발자 명령 프롬프트(또는 Windows 7의 Visual Studio 명령 프롬프트)를 사용합니다. 자세한 내용은 [명령 프롬프트](developer-command-prompt-for-vs.md)를 참조하세요.

명령 프롬프트에 다음을 입력합니다.

## <a name="syntax"></a>구문

```console
al sources options
```

## <a name="parameters"></a>매개 변수

다음 `sources` 중에서 하나 이상 지정할 수 있습니다.

| 원본 | 설명 |
| ------ | ----------- |
|`file`[,`target`]|`file`(모듈)의 내용을 `target`이 지정하는 파일 이름에 복사합니다. 복사한 후 *Al.exe*가 `target`을 어셈블리로 컴파일합니다.|
|**/embed[resource]:** `file`[,`name`[,`private`]]|`file`이 지정하는 리소스를 어셈블리 매니페스트가 포함된 이미지에 포함합니다. *Al.exe*는 `file`의 내용을 이식 가능한 실행 파일(PE) 이미지에 복사합니다.<br /><br /> `name` 매개 변수는 리소스의 내부 식별자입니다. 기본적으로 리소스는 어셈블리에서 공용입니다. 즉, 다른 어셈블리가 볼 수 있습니다. `private`를 지정하면 다른 어셈블리에서 리소스를 볼 수 없습니다.<br /><br /> 예를 들어, `file`이 [리소스 파일 생성기(*Resgen.exe*)](resgen-exe-resource-file-generator.md)나 개발 환경에서 만들어진 .NET Framework 리소스 파일인 경우에는 <xref:System.Resources>의 멤버를 사용하여 해당 파일에 액세스할 수 있습니다. 자세한 내용은 <xref:System.Resources.ResourceManager>을 참조하세요. 다른 모든 리소스의 경우에는 런타임에 `GetManifestResource`의 <xref:System.Reflection.Assembly>* 메서드를 사용하여 리소스에 액세스합니다.<br /><br /> 리소스 파일만 *Al.exe*에 전달되는 경우에는 출력 파일이 위성 리소스 어셈블리입니다.|
|**/link[resource]:** `file`[,`name`[,`target`[,`private`]]]|리소스 파일을 어셈블리에 링크합니다. `file`이 지정하는 리소스가 어셈블리의 일부가 되고 파일은 복사되지 않습니다. `file` 매개 변수는 어떠한 파일 형식도 될 수 있습니다. 예를 들어, 네이티브 DLL을 `file` 매개 변수로 지정할 수 있습니다. 이렇게 하면 네이티브 DLL이 어셈블리의 일부가 되므로 전역 어셈블리 캐시에 설치하고 어셈블리의 관리 코드에서 액세스할 수 있습니다. 이 작업은 **/linkresource** 컴파일러 옵션을 사용하여 수행할 수도 있습니다. 자세한 내용은 [/linkresource(C# 컴파일러 옵션)](../../csharp/language-reference/compiler-options/linkresource-compiler-option.md)를 참조하세요.<br /><br /> `name` 매개 변수는 리소스의 내부 식별자입니다. `target` 매개 변수는 *Al.exe*에서 `file`*을 복사하는 경로와 파일 이름을 지정합니다.* 복사한 후 *Al.exe*가 `target`을 어셈블리로 컴파일합니다. 기본적으로 리소스는 어셈블리에서 공용입니다. 즉, 다른 어셈블리가 볼 수 있습니다. `private`를 지정하면 다른 어셈블리에서 리소스를 볼 수 없습니다.<br /><br /> 예를 들어, `file`이 리소스 파일 생성기 (*Resgen.exe*)나 개발 환경에서 만들어진 .NET Framework 리소스 파일인 경우에는 <xref:System.Resources> 네임스페이스의 멤버를 사용하여 해당 파일에 액세스할 수 있습니다. 자세한 내용은 <xref:System.Resources.ResourceManager>을 참조하세요. 다른 모든 리소스의 경우에는 런타임에 `GetManifestResource` 클래스의 <xref:System.Reflection.Assembly>* 메서드를 사용하여 리소스에 액세스합니다.<br /><br /> 리소스 파일만 *Al.exe*에 전달되는 경우에는 출력 파일이 위성 리소스 어셈블리입니다.|

다음 `options`를 지정할 수 있으며, **/out**은 반드시 지정해야 합니다.

| 옵션 | 설명 |
| ------ | ----------- |
|**/algid:** `id`|어셈블리 매니페스트가 포함된 파일을 제외하고 다중 파일 어셈블리에 있는 모든 파일을 해시하는 알고리즘을 지정합니다. 기본 알고리즘은 CALG_SHA1입니다. 다른 알고리즘에 대해서는 Platform SDK 설명서의 ALG_ID를 참조하세요. .NET Framework의 첫 릴리스에서는 CALG_SHA1과 CALG_MD5만 유효합니다.<br /><br /> 해시 값은 어셈블리 매니페스트의 파일 테이블에 저장됩니다. 설치 및 로드할 때 어셈블리의 파일을 해시와 비교하여 확인합니다.<br /><br /> 모듈의 소스 코드에서 이 옵션을 사용자 지정 특성(<xref:System.Reflection.AssemblyAlgorithmIdAttribute>)으로 지정할 수도 있습니다.|
|**/base[address]:** `addr`|런타임에 DLL이 사용자의 컴퓨터에 로드되는 주소를 지정합니다. 운영 체제가 프로세스 공간에서 DLL을 재배치하게 하지 않고 DLL의 기본 주소를 직접 지정하면 애플리케이션의 로드 속도가 빨라집니다.|
|**/bugreport**: `filename`|버그를 보고하기 위한 정보가 포함된 파일(`filename`)을 만듭니다.|
|**/comp[any]:** `text`|어셈블리의 Company 필드에 대한 문자열을 지정합니다. `text`에 공백이 있으면 문자열을 큰따옴표(" ")로 묶습니다. 이 문자열은 어셈블리의 사용자 지정 속성이며 리플렉션과 함께 볼 수 있습니다.<br /><br /> **/win32res**를 지정하지 않으면 파일 탐색기에서 `text`가 파일의 `Company` 속성으로 나타납니다. **/win32res**를 지정하면 파일 탐색기에서 리소스 파일의 회사 정보가 `Company` 속성으로 파일 탐색기에 나타납니다.<br /><br /> 텍스트가 빈 문자열("")이면 Win32 `Company` 리소스가 단일 공백으로 표시됩니다.<br /><br /> **/win32res**를 지정하면 **/company**는 Win32 리소스 정보에 영향을 주지 않습니다.<br /><br /> MSIL 모듈의 소스 코드에서 이 옵션을 사용자 지정 특성(<xref:System.Reflection.AssemblyCompanyAttribute>)으로 지정할 수도 있습니다.|
|**/config[uration]:** `text`|어셈블리의 Configuration 필드에 대한 문자열을 지정합니다. `text`에 공백이 있으면 문자열을 큰따옴표(" ")로 묶습니다. 이 문자열은 어셈블리의 사용자 지정 속성이며 리플렉션과 함께 볼 수 있습니다.<br /><br /> 텍스트가 빈 문자열이면 Win32 Configuration 리소스가 단일 공백으로 표시됩니다.<br /><br /> MSIL 모듈의 소스 코드에서 이 옵션을 사용자 지정 특성(<xref:System.Reflection.AssemblyConfigurationAttribute>)으로 지정할 수도 있습니다.|
|**/copy[right]:** `text`|어셈블리의 Copyright 필드에 대한 문자열을 지정합니다. `text`에 공백이 있으면 문자열을 큰따옴표(" ")로 묶습니다. 이 문자열은 어셈블리의 사용자 지정 속성이며 리플렉션과 함께 볼 수 있습니다.<br /><br /> **/win32res**를 지정하지 않으면 파일 탐색기에서 **/copyright**가 Win32 Copyright(저작권) 리소스로 나타납니다.<br /><br /> 텍스트가 빈 문자열이면 Win32 Copyright 리소스가 단일 공백으로 표시됩니다.<br /><br /> **/win32res**를 지정하면 **/copyright**는 Win32 리소스 정보에 영향을 주지 않습니다.<br /><br /> MSIL 모듈의 소스 코드에서 이 옵션을 사용자 지정 특성(<xref:System.Reflection.AssemblyCopyrightAttribute>)으로 지정할 수도 있습니다.|
|**/c[ulture]:** `text`|어셈블리에 연결할 문화권 문자열을 지정합니다. "Tags for the Identification of Languages"라는 제목의 인터넷 RFC(Requests for Comments) 문서 1766에서 정의하는 값이 문화권의 유효한 값입니다.<br /><br /> `text`에 공백이 있으면 문자열을 큰따옴표(" ")로 묶습니다. 기본 문화권 문자열은 없습니다. 이 문자열을 리플렉션과 함께 볼 수 있습니다.<br /><br /> 유효한 `text` 문자열에 대한 자세한 내용은 <xref:System.Globalization.CultureInfo>를 참조하세요.<br /><br /> MSIL 모듈의 소스 코드에서 이 옵션을 사용자 지정 특성(<xref:System.Reflection.AssemblyCultureAttribute>)으로 지정할 수도 있습니다.|
|**/delay[sign][+&#124;-]**|어셈블리를 완전히 서명할지, 아니면 부분적으로 서명할지를 지정합니다. 완전히 서명된 어셈블리가 필요하면 **/delaysign-** 를 사용합니다. 어셈블리에 공개 키만 포함하려면 **/delaysign+** 를 사용합니다.<br /><br /> 완전히 서명된 어셈블리를 요청할 경우 *Al.exe*는 매니페스트(어셈블리 메타데이터)가 포함된 파일을 해시하고 공개 키로 해당 해시에 서명합니다. 결과로 생성되는 디지털 서명은 매니페스트가 포함된 파일에 저장됩니다. 어셈블리 서명이 연기된 경우 *Al.exe*는 시그니처를 컴퓨팅하거나 저장하지 않고 나중에 시그니처를 추가할 수 있도록 파일에 공간을 예약합니다.<br /><br /> 기본값은 **/delaysign-** 입니다.<br /><br /> **/delaysign** 옵션은 **/keyfile** 또는 **/keyname**과 함께 사용하지 않으면 효과가 없습니다.<br /><br /> 예를 들어 **/delaysign+** 를 사용하면 테스터를 통해 전역 캐시에 어셈블리를 넣을 수 있습니다. 테스트를 마친 후 어셈블리에 프라이빗 키를 포함하여 어셈블리에 완전히 서명할 수 있습니다.<br /><br /> 참고: [*Gacutil.exe*(전역 어셈블리 캐시 도구)](gacutil-exe-gac-tool.md)를 사용하여 전역 캐시에 서명이 연기된 어셈블리를 넣으려면, 먼저 [*Sn.exe*(강력한 이름 도구)](sn-exe-strong-name-tool.md)를 사용하여 확인을 건너뛰는 어셈블리를 등록합니다. 예: `Sn.exe –Vr delaySignedAssembly`. 개발에서만 이 기능을 사용하세요.<br /><br /> MSIL 모듈의 소스 코드에서 이 옵션을 사용자 지정 특성(<xref:System.Reflection.AssemblyDelaySignAttribute>)으로 지정할 수도 있습니다.|
|**/descr[iption]:** `text`|어셈블리의 <xref:System.Reflection.AssemblyDescriptionAttribute.Description%2A> 필드에 대한 문자열을 지정합니다. `text`에 공백이 있으면 문자열을 큰따옴표(" ")로 묶습니다. 이 문자열은 어셈블리의 사용자 지정 속성이며 리플렉션과 함께 볼 수 있습니다.<br /><br /> **/win32res**를 지정하지 않으면 파일 탐색기에서 **/description**이 Win32 **Comments**(설명) 리소스로 나타납니다.<br /><br /> 텍스트가 빈 문자열이면 Win32 **Comments** 리소스가 단일 공백으로 나타납니다.<br /><br /> **/win32res**를 지정하면 **/description**은 Win32 리소스 정보에 영향을 주지 않습니다.<br /><br /> MSIL 모듈의 소스 코드에서 이 옵션을 사용자 지정 특성(<xref:System.Reflection.AssemblyDescriptionAttribute.Description%2A>)으로 지정할 수도 있습니다.|
|**/e[vidence]:** `file`|어셈블리에 `file`을 Security.Evidence라는 리소스 이름으로 포함시킵니다.<br /><br /> 기본 리소스에는 Security.Evidence를 사용할 수 없습니다.|
|**/fileversion:** `version`|어셈블리의 **File Version**(파일 버전) 필드에 대한 문자열을 지정합니다. 이 문자열은 어셈블리의 사용자 지정 속성이며 리플렉션과 함께 볼 수 있습니다.<br /><br /> **/win32res**를 지정하지 않으면 **/fileversion**이 Win32 **File Version** 리소스로 사용됩니다. **/fileversion**을 지정하지 않으면 Win32 **File Version** 리소스가 Win32 **Assembly Version**(어셈블리 버전) 리소스로 채워집니다.<br /><br /> **/win32res**를 지정하면 **/fileversion**은 Win32 리소스에 영향을 주지 않습니다.<br /><br /> MSIL 모듈의 소스 코드에서 이 옵션을 사용자 지정 특성(AssemblyFileVersionAttribute)으로 지정할 수도 있습니다.|
|**/flags:** `flags`|어셈블리의 `Flags` 필드에 대한 값을 지정합니다. `flags`에 사용할 수 있는 값은 다음과 같습니다.<br /><br /> 0x0000<br /> 어셈블리가 side-by-side로 호환됩니다.<br /><br /> 0x0010<br /> 어셈블리는 같은 애플리케이션 도메인에서 실행할 경우 다른 버전과 함께 실행할 수 없습니다.<br /><br /> 0x0020<br /> 어셈블리는 같은 프로세스에서 실행할 경우 다른 버전과 함께 실행할 수 없습니다.<br /><br /> 0x0030<br /> 같은 컴퓨터에서 실행되는 경우에는 어셈블리를 다른 버전과 함께 실행할 수 없습니다.<br /><br /> MSIL 모듈의 소스 코드에서 이 옵션을 사용자 지정 특성(<xref:System.Reflection.AssemblyFlagsAttribute>)으로 지정할 수도 있습니다.|
|**/fullpaths**|오류 메시지에 보고되는 파일에 대해 *Al.exe*가 절대 경로를 사용합니다.|
|**/help**|이 도구의 명령 구문 및 옵션을 표시합니다.|
|**/keyf[ile]:** `filename`|어셈블리에 서명하기 위한 키 쌍 또는 공개 키를 포함하는 파일(`filename`)을 지정합니다. 컴파일러는 퍼블릭 키를 어셈블리 매니페스트에 삽입한 다음 프라이빗 키를 사용하여 최종 어셈블리에 서명합니다. 키 파일을 생성하고 키 쌍을 키 컨테이너에 설치하는 방법에 대한 자세한 내용은 [Strong Name Tool (*Sn.exe*)](sn-exe-strong-name-tool.md)(Sn.exe(강력한 이름 도구))을 참조하세요.<br /><br /> 연기된 서명을 사용할 경우 이 파일에는 일반적으로 퍼블릭 키가 있으며 프라이빗 키는 없습니다.<br /><br /> 키 쌍의 공개 키 정보는 어셈블리의 .publickey 필드에 나타납니다.<br /><br /> MSIL 모듈의 소스 코드에서 이 옵션을 사용자 지정 특성(<xref:System.Reflection.AssemblyKeyFileAttribute>)으로 지정할 수도 있습니다.<br /><br /> **/keyfile** 및 **/keyname**이 모두 동일한 컴파일에서 명령줄 옵션이나 사용자 지정 특성으로 지정되면 *Al.exe*에서 먼저 **/keyname**으로 지정된 컨테이너를 찾으려고 합니다. 이 시도에 성공하면 키 컨테이너의 정보를 사용하여 어셈블리가 서명됩니다. *Al.exe*에서 키 컨테이너를 찾지 못하면 **/keyfile**로 지정된 파일을 찾으려고 합니다. 해당 파일을 찾으면 어셈블리가 키 파일의 정보로 서명되고 키 정보가 키 컨테이너에 설치됩니다([*Sn.exe*](sn-exe-strong-name-tool.md)의 -i 옵션과 비슷함). 이에 따라 다음에 컴파일할 때 **/keyname** 옵션이 유효하게 됩니다.|
|**/keyn[ame]:** `text`|키 쌍을 보관하는 컨테이너를 지정합니다. 어셈블리 매니페스트에 공개 키를 삽입하여 어셈블리에 서명(강력한 이름을 부여)합니다. 그런 다음 *Al.exe*가 프라이빗 키를 사용하여 최종 어셈블리에 서명합니다.<br /><br /> *Sn.exe*를 사용하여 키 쌍을 생성합니다.<br /><br /> 어셈블리의 .publickey 필드에 키 정보가 나타납니다.<br /><br /> `text`에 공백이 있으면 큰따옴표(" ")로 묶습니다.<br /><br /> MSIL 모듈의 소스 코드에서 이 옵션을 사용자 지정 특성(<xref:System.Reflection.AssemblyKeyNameAttribute>)으로 지정할 수도 있습니다.|
|**/main:** `method`|모듈을 실행 파일로 변환할 때 진입점으로 사용할 메서드의 정규화된 이름(`class`.`method`)을 지정합니다.|
|**/nologo**|*Al.exe*를 호출할 때 명령줄에 표시되는 배너 또는 로고를 표시하지 않습니다.|
|**/out:** `filename`|*Al.exe*가 생성한 파일의 이름을 지정합니다. 필수 옵션입니다.|
|**/platform:** `text`|이 코드를 실행할 수 있는 플랫폼은 x86, Itanium, x64, anycpu(기본값) 또는 anycpu32bitpreferred로 제한됩니다.|
|**/prod[uct]:** `text`|어셈블리의 **Product**(제품) 필드에 대한 문자열을 지정합니다. `text`에 공백이 있으면 문자열을 큰따옴표(" ")로 묶습니다. 이 문자열은 어셈블리의 사용자 지정 속성이며 리플렉션과 함께 볼 수 있습니다.<br /><br /> **/win32res**를 지정하지 않으면 파일 탐색기에서 **/product**가 Win32 **Product Name**(제품 이름) 리소스로 나타납니다.<br /><br /> 텍스트가 빈 문자열이면 Win32 **Product Name** 리소스가 단일 공백으로 나타납니다.<br /><br /> **/win32res**를 지정하면 **/product**는 Win32 리소스 정보에 영향을 주지 않습니다.<br /><br /> MSIL 모듈의 소스 코드에서 이 옵션을 사용자 지정 특성(<xref:System.Reflection.AssemblyProductAttribute>)으로 지정할 수도 있습니다.|
|**/productv[ersion]:** `text`|어셈블리의 **Product Version**(제품 버전) 필드에 대한 문자열을 지정합니다. `text`에 공백이 있으면 문자열을 큰따옴표(" ")로 묶습니다. 이 문자열은 어셈블리의 사용자 지정 속성이며 리플렉션과 함께 볼 수 있습니다.<br /><br /> **/win32res**를 지정하지 않으면 **/productversion**이 Win32 **Product Version** 리소스로 사용됩니다. **/productversion**을 지정하지 않으면 Win32 **Product Version** 리소스가 Win32 **File Version** 리소스로 채워집니다.<br /><br /> **/win32res**를 지정하면 **/productversion**은 Win32 리소스 정보에 영향을 주지 않습니다.<br /><br /> MSIL 모듈의 소스 코드에서 이 옵션을 사용자 지정 특성(<xref:System.Reflection.AssemblyInformationalVersionAttribute>)으로 지정할 수도 있습니다.|
|**/t[arget]:** `lib[rary]` &#124; `exe` &#124; `win[exe]`|출력 파일의 파일 형식 즉, `lib[rary]`(코드 라이브러리), `exe`(콘솔 애플리케이션) 또는 `win[exe]`(Windows 기반 애플리케이션)을 지정합니다. 기본값은 `lib[rary]`입니다.|
|**/template:** `filename`|culture 필드를 제외한 모든 어셈블리 메타데이터를 상속받을 상위 어셈블리, `filename`을 지정합니다.<br /><br /> **/template**으로 만든 어셈블리는 위성 어셈블리가 됩니다.|
|**/title:** `text`|어셈블리의 **Title**(제목) 필드에 대한 문자열을 지정합니다. `text`에 공백이 있으면 문자열을 큰따옴표(" ")로 묶습니다. 이 문자열은 어셈블리의 사용자 지정 속성이며 리플렉션과 함께 볼 수 있습니다.<br /><br /> **/win32res**를 지정하지 않으면 파일 탐색기에서 **/title**이 셸에서 애플리케이션의 이름으로 사용되는 Win32 **Description**(설명) 리소스로 나타납니다. 또한 여러 애플리케이션이 지원하는 파일 형식에 대한 바로 가기 메뉴의 **연결 프로그램** 하위 메뉴에도 표시됩니다.<br /><br /> 텍스트가 빈 문자열이면 Win32 **Description** 리소스가 단일 공백으로 나타납니다.<br /><br /> **/win32res**를 지정하면 **/title**은 Win32 리소스 정보에 영향을 주지 않습니다.<br /><br /> MSIL 모듈의 소스 코드에서 이 옵션을 사용자 지정 특성(<xref:System.Reflection.AssemblyTitleAttribute>)으로 지정할 수도 있습니다.|
|**/trade[mark]:** `text`|어셈블리의 **Trademark**(상표) 필드에 대한 문자열을 지정합니다. `text`에 공백이 있으면 문자열을 큰따옴표(" ")로 묶습니다. 이 문자열은 어셈블리의 사용자 지정 속성이며 리플렉션과 함께 볼 수 있습니다.<br /><br /> **/win32res**를 지정하지 않으면 파일 탐색기에서 **/trademark**가 Win32 **Trademark** 리소스로 나타납니다.<br /><br /> 텍스트가 빈 문자열이면 Win32 **Trademark** 리소스가 단일 공백으로 나타납니다.<br /><br /> **/win32res**를 지정하면 **/trademark**는 Win32 리소스 정보에 영향을 주지 않습니다.<br /><br /> MSIL 모듈의 소스 코드에서 이 옵션을 사용자 지정 특성(<xref:System.Reflection.AssemblyTrademarkAttribute>)으로 지정할 수도 있습니다.|
|**/v[ersion]:** `version`|이 어셈블리의 버전 정보를 지정합니다. 버전 문자열의 형식은 `major`.`minor`.`build`.`revision`입니다. 기본값은 0입니다.<br /><br /> **/version**을 지정하면 `major`도 지정해야 합니다. `major` 및 `minor`를 지정하면 `build`에 별표(\*)를 지정할 수 있습니다. 이 경우 `build`는 현지 시간 2000년 1월 1일부터 경과된 일수와 일치하며, `revision`은 현재 날짜, 현지 시간, 자정부터 경과된 초 수를 2로 나눈 값과 일치합니다.<br /><br /> `major`, `minor` 및 `build`를 지정하면 `revision`에 대해 별표를 지정할 수 있습니다. 이 경우 `revision`은 현재 날짜, 현지 시간, 자정부터 경과된 초 수를 2로 나눈 값과 일치합니다.<br /><br /> 유효한 버전 문자열을 요약하면 다음과 같습니다.<br /><br /> X<br /><br /> X.X<br /><br /> X.X.\*<br /><br /> X.X.X<br /><br /> X.X.X.\*<br /><br /> X.X.X.X<br /><br /> 여기서 X는 65535를 제외한 부호 없는 short 상수(0-65534)입니다.<br /><br /> **/win32res**를 지정하지 않으면 **/version**이 Win32 **Assembly Version**(어셈블리 버전) 리소스로 사용됩니다.<br /><br /> **/win32res**, **/productversion** 및 **/fileversion**을 지정하지 않으면 **/version**이 Win32 **Assembly Version**, File Version 및 **Product Version** 리소스에 사용됩니다.<br /><br /> **/win32res**를 지정하면 **/version**은 Win32 리소스 정보에 영향을 주지 않습니다.<br /><br /> MSIL 모듈의 소스 코드에서 이 옵션을 사용자 지정 특성(<xref:System.Reflection.AssemblyVersionAttribute>)으로 지정할 수도 있습니다.|
|**/win32icon:** `filename`|.ico 파일을 어셈블리에 삽입합니다. .ico 파일을 사용하면 파일 탐색기에서 출력 파일을 원하는 모양으로 나타납니다.|
|**/win32res:** `filename`|Win32 리소스(.res 파일)를 출력 파일에 삽입합니다. Win32 리소스 파일은 리소스 컴파일러를 사용하여 만듭니다. 리소스 컴파일러는 Visual C++ 프로그램을 컴파일할 때 실행되며 .rc 파일에서 .res 파일이 만들어집니다.|
|`@filename`|*Al.exe* 명령을 포함하는 지시 파일을 지정합니다.<br /><br /> 지시 파일의 명령은 한 줄에 하나씩 나타나거나 하나 이상의 공백으로 분리되어 같은 줄에 나타날 수 있습니다.|
|**/?**|이 도구의 명령 구문 및 옵션을 표시합니다.|

## <a name="remarks"></a>설명

모든 Visual Studio 컴파일러는 어셈블리를 만듭니다. 그러나 모듈(매니페스트 없는 메타데이터)이 하나 이상 있으면 *Al.exe*를 사용하여 별도의 파일에 매니페스트가 있는 어셈블리를 만들 수 있습니다.

캐시에서 어셈블리를 설치하거나, 제거하거나, 캐시의 내용을 나열하려면 [Global Assembly Cache Tool (*Gacutil.exe*)](gacutil-exe-gac-tool.md)(Gacutil.exe(전역 어셈블리 캐시 도구))을 사용합니다.

## <a name="errors-and-warnings"></a>오류 및 경고

다음 표에서는 *Al.exe*에 의해 생성된 오류를 보여 줍니다.

| 오류 | 설명 |
| ----- | ----------- |
|al1001|내부 컴파일러 오류<br /><br /> *Al.exe*가 예기치 않은 구문을 분석할 수 없어 실패하는지 여부를 확인합니다. 그런 다음 Microsoft 기술 지원 서비스에 문의하세요.|
|al1002|메모리 부족<br /><br /> *Al.exe*가 메모리 부족으로 중지되었습니다. 사용 가능한 메모리 양을 늘립니다.|
|al1003|'option' 컴파일러 옵션 다음에는 인수가 와야 합니다.<br /><br /> *Al.exe*에서 명령줄 옵션에 인수가 전달될 것으로 예상했습니다. 예를 들어 **/algid:** 를 지정하는 경우 알고리즘 식별자를 전달해야 합니다.|
|al1004|예기치 않은 공용 언어 런타임 초기화 오류 - 'reason'<br /><br /> *Al.exe*에서 지정된 이유로 Visual Studio 또는 공용 언어 런타임 설치 오류를 보고했습니다.|
|al1005|'file' 파일이 너무 커서 열 수 없습니다.<br /><br /> *Al.exe*에서 여는 모든 파일은 4GB(기가바이트)보다 작아야 합니다.|
|al1006|'file' 지시 파일이 이미 포함되었습니다.<br /><br /> 동일한 지시 파일이 명령줄에서 두 번 이상 지정되었습니다(`@file`). 지시 파일은 한 번만 포함될 수 있습니다.|
|al1007|'file' 지시 파일을 여는 동안 오류가 발생했습니다. 'reason'<br /><br /> *Al.exe*에서 지정된 이유로 지정된 지시 파일을 열 수 없습니다.|
|al1008|'option' 명령줄 옵션에 대한 파일 사양이 없습니다.<br /><br /> *Al.exe*에서 명령줄 옵션에 파일이 전달될 것으로 예상했습니다. 예를 들어 **/out** 옵션을 지정하는 경우 파일을 지정해야 합니다.|
|al1009|'file'을 쓰기용으로 열 수 없습니다.<br /><br /> *Al.exe*에서 출력 어셈블리 파일과 같은 파일에 쓸 수 없습니다. 디스크가 꽉 찼거나, 파일이 읽기 전용이거나, 파일에 대한 권한이 없을 수 있습니다.|
|al1010|명령줄 구문 오류: 'option' 옵션에 ':text' 누락<br /><br /> *Al.exe*에서 명령줄 옵션에 인수가 전달될 것으로 예상했습니다. 예를 들어 **/title** 옵션을 지정하는 경우 문자열을 전달해야 합니다.|
|al1011|'file' 파일은 실행 파일이며 텍스트 파일로 열 수 없습니다.<br /><br /> 텍스트 파일이 필요한 위치에 이진 파일이 지정되었습니다. 예를 들어 명령줄에서 이진 파일이 지시 파일로 전달되면 이 오류가 발생합니다.|
|al1012|'value'가 'option' 옵션에 유효한 설정이 아닙니다.<br /><br /> 예기치 않은 값이 명령줄 옵션에 전달되었습니다. 예를 들어 **/target** 옵션에 잘못된 값을 지정하는 경우 이 오류가 발생합니다.|
|al1013|인식할 수 없는 명령줄 옵션: 'option'<br /><br /> 잘못된 명령줄 옵션을 지정했습니다.|
|al1014|예기치 않은 초기화 오류 - 'reason'<br /><br /> *Al.exe*에서 COM 초기화 오류를 발견했습니다. 이 오류는 메모리 부족으로 발생할 수도 있지만 시스템 DLL 파일 때문일 가능성이 더 큽니다. Microsoft Visual Studio와 같은 자동화 인식 또는 COM 인식 프로그램을 실행하면 유사한 오류가 표시됩니다.<br /><br /> 운영 체제를 다시 설치합니다.|
|al1015|'alinkui.dll' 메시지 파일을 찾을 수 없습니다.<br /><br /> *Al.exe*를 사용하려면 *Alinkui.dll*이 필요합니다. 이 파일이 경로에 있는지 확인합니다. 필요한 경우 제품 CD에서 복사합니다.|
|al1016|유효한 입력 파일을 지정하지 않았습니다.<br /><br /> *Al.exe*를 사용하려면 어셈블리 정보가 없는 입력 파일이 하나 이상 필요합니다.|
|al1017|대상 파일 이름을 지정하지 않았습니다.<br /><br /> 대상 파일 이름을 지정하는 필수 **/out** 옵션이 없습니다.|
|al1018|‘file’ 필수 파일을 로드할 수 없습니다.<br /><br /> 특정 DLL 파일을 로드할 수 없습니다. Visual Studio 또는 Windows SDK를 다시 설치합니다.|
|al1019|어셈블리를 만드는 동안 메타데이터 오류 발생 - reason<br /><br /> 지정된 이유로 어셈블리 생성이 중단되었습니다. 예를 들어 **/win32res** 옵션으로 지정한 파일을 찾을 수 없는 경우 이 오류가 발생합니다.|
|al1020|포함된 어셈블리 'file'을 무시합니다.<br /><br /> 어셈블리를 포함하는 입력 파일을 지정했습니다. *Al.exe* 입력 파일은 어셈블리를 포함할 수 없습니다.|
|al1021|'setting': 이전 설정 재정의<br /><br /> 모듈에 사용자 지정 특성을 통해 할당된 특정 설정 값이 있었습니다. 이 값이 *Al.exe* 명령줄 옵션을 사용하여 전달된 값으로 재정의되었습니다.|
|al1022|포함된 리소스 'file'을 읽는 동안 오류 발생 - reason<br /><br /> *Al.exe*에서 지정된 이유로 **/embedresource** 옵션에 전달된 파일을 읽을 수 없습니다.|
|al1023|리소스 'file'을 포함하는 동안 오류 발생 - reason<br /><br /> 운영 체제에서 지정된 이유로 어셈블리에 리소스 파일을 포함할 수 없습니다.|
|al1025|ComType 레코드 'record'가 잘못 된 파일 레코드 'record'를 가리킵니다.<br /><br /> 입력 모듈의 메타데이터가 잘못되었습니다. 모듈을 생성한 도구를 수정해야 합니다.|
|al1026|지정된 ‘version’ 버전이 잘못되었습니다.<br /><br /> 유효한 형식은 **/version** 옵션에 대한 정보를 참조하세요.|
|al1028|file' 키 파일에 서명에 필요한 프라이빗 키가 없습니다.<br /><br /> 공개 키만 포함된 키 파일이 **/keyfile** 옵션에 전달되었습니다. 다음 명령과 같이 [*Sn.exe*(강력한 이름 도구)](sn-exe-strong-name-tool.md)를 사용하여 퍼블릭 키와 프라이빗 키가 둘 다 포함된 파일을 생성합니다.<br /><br /> `sn -k keypair.snk.`|
|al1029|키 컨테이너 이름 ‘container’가 없습니다.<br /><br /> **/keyname** 옵션에 전달된 값이 유효한 컨테이너가 아닙니다. [*Sn.exe*(강력한 이름 도구)](sn-exe-strong-name-tool.md)를 사용하여 컨테이너를 만듭니다.|
|al1030|암호화 서비스가 제대로 설치되지 않았거나 적절한 키 공급자가 없습니다.<br /><br /> 운영 체제를 다시 설치하거나, 키를 만드는 데 사용되는 일부 암호화 유틸리티를 설치해야 할 수 있습니다.|
|al1031|'file' 아이콘을 읽는 동안 오류 발생 - reason<br /><br /> *Al.exe*에서 지정된 이유로 **/win32icon** 옵션에 전달된 파일을 읽을 수 없습니다.|
|al1032|'file'에 대한 리소스를 생성하는 동안 오류 발생 - reason<br /><br /> 디스크 공간 부족 또는 일부 다른 오류로 인해 *Al.exe*에서 파일을 만들 수 없습니다. **/win32icon** 옵션(.ico 파일 생성)을 지정하거나 **/win32res** 옵션(리소스 정보가 포함된 파일 생성)을 지정하지 않으면 이 오류가 발생합니다.<br /><br /> 파일 생성 문제를 해결할 수 없는 경우 버전 또는 비트맵(아이콘) 정보를 포함할 수 있는 파일을 지정하는 **/win32res**를 사용합니다.|
|al1033|어셈블리 사용자 지정 특성 'attribute'가 서로 다른 값으로 여러 번 지정되었습니다.<br /><br /> *Al.exe*에 대한 입력으로 지정된 소스 모듈의 동일한 사용자 지정 특성 발생 두 개에 서로 다른 값이 전달되었습니다.|
|al1034|'file' 어셈블리를 복사하거나 이름을 바꿀 수 없습니다.<br /><br /> 입력 파일을 지정하고 복사할 수 있게 해주는 *Al.exe* 구문을 사용하는 동안 이름 충돌이 발생하여 컴파일러가 중지되었습니다. 예를 들어 이 오류는 `input.dll,somename.dll /out:somename.dll`을 지정하는 경우 발생합니다.|
|al1035|라이브러리는 진입점을 포함할 수 없습니다.<br /><br /> **/target:lib** 옵션(기본값) 및 **/main** 옵션을 모두 지정할 수 없습니다.|
|al1036|실행 가능한 애플리케이션에는 진입점이 필요합니다.<br /><br /> **/target:exe** 또는 **/target:win** 옵션을 사용할 때는 **/main** 옵션도 지정해야 합니다.|
|al1037|'main' 진입점 메서드를 찾을 수 없습니다.<br /><br /> *Al.exe*가 **/main** 옵션으로 지정된 위치에서 `Main` 메서드를 찾을 수 없습니다.|
|al1039|전역 어셈블리 캐시 관리자 초기화 실패 - reason<br /><br /> Visual Studio 또는 Windows SDK를 다시 설치합니다.|
|al1040|캐시에 어셈블리를 설치하지 못했습니다. reason<br /><br /> 서명된 어셈블리만 캐시에 설치할 수 있습니다. 자세한 내용은 [전역 어셈블리 캐시](../app-domains/gac.md)를 참조하세요.|
|al1041|'method': 서명 또는 표시 유형이 잘못되었거나 제네릭이기 때문에 진입점이 될 수 없습니다.<br /><br /> 메서드가 **/main** 옵션으로 지정되었지만 해당 메서드가 정적이 아니거나, `int` 또는 `void`를 반환하지 않거나, 제네릭이거나, 잘못된 인수를 포함하고 있습니다.|
|al1042|'exe': EXE를 모듈로 추가할 수 없습니다.<br /><br /> 어셈블리가 없는 *.exe* 파일이 *Al.exe*에 대한 입력 파일로 지정되었습니다. *Al.exe*는 어셈블리가 없는 *dll* 파일만 입력 파일로 사용할 수 있습니다.|
|al1043|'name' 매니페스트 파일 이름은 모듈과 같을 수 없습니다.<br /><br /> **/out** 옵션으로 지정된 이름은 *Al.exe*에 대한 입력으로 지정된 파일 이름 중 하나와 같을 수 없습니다.|
|al1044|'file' 키 파일을 읽는 동안 오류 발생 - reason<br /><br /> **/keyfile** 또는 <xref:System.Reflection.AssemblyKeyFileAttribute>에 지정된 파일을 열거나 읽는 동안 오류가 발생했습니다.|
|al1045|‘file’ 파일 이름이 너무 길거나 잘못되었습니다.<br /><br /> 260자보다 긴 파일 이름이 *Al.exe*에 전달되었습니다. 더 적은 문자를 포함하거나 경로가 더 짧은 파일 이름을 선택하거나 파일 이름을 바꿉니다.|
|al1046|'ID' 리소스 식별자가 이 어셈블리에서 이미 사용되었습니다.<br /><br /> 포함 또는 연결된 두 리소스에 동일한 식별자 또는 이름(두 번째 인수)이 있습니다. 충돌하는 리소스 중 하나를 제거하거나 이름을 바꿉니다.|
|al1047|'file' 파일을 가져오는 동안 오류 발생 - reason<br /><br /> 지정된 이유로 모듈 파일을 열 수 없습니다.|
|al1048|'assembly' 어셈블리의 'module' 모듈을 가져오는 동안 오류 발생 - reason<br /><br /> 다중 파일 어셈블리의 비매니페스트 파일을 열 때 오류가 발생했습니다. 이 오류는 *Al.exe*에서 직접 내보내지 않고 *Al.exe*를 사용하는 프로세스에 프로그래밍 방식으로 전달될 수 있습니다.|
|al1049|2000년 1월 1일 이전 날짜에 대한 빌드 및 수정 버전 번호를 자동으로 생성할 수 없습니다.<br /><br /> 컴퓨터의 시스템 시계가 2000년 1월 1일 이전 날짜로 설정되었습니다.|
|al1050|'old feature'를 사용하는 기능은 더 이상 지원되지 않습니다. 'new feature'를 대신 사용하세요.<br /><br /> 이전에 *Al.exe*에서 지원한 기능이 이제 사용되지 않습니다. 권장 기능을 대신 사용합니다.|
|al1051|'attribute' 특성을 내보내는 동안 오류 발생 - 'reason'<br /><br /> 지정된 이유로 어셈블리 사용자 지정 특성이 *Al.exe*에서 처리되지 않았습니다.|
|al1052|‘filename’ 파일은 어셈블리가 아닙니다.<br /><br /> **/template**으로 지정된 파일은 어셈블리 메타데이터를 포함해야 합니다. 이 오류는 **/template**으로 지정된 파일에 어셈블리가 포함되지 않았음을 나타냅니다.|
|al1053|'옵션'에 대해 지정된 'version' 버전은 일반적인 'major.minor.build.revision' 형식이 아닙니다.<br /><br /> *Al.exe*에서 **/fileversion** 또는 **/productversion** 옵션으로 지정된 형식이 아닌 버전 정보를 발견했습니다.|
|al1054|'옵션'에 대해 지정된 'version' 버전은 일반적인 'major.minor.build.revision' 형식이 아닙니다.<br /><br /> *Al.exe*에서 <xref:System.Resources.SatelliteContractVersionAttribute>에 잘못된 형식의 버전 정보가 지정된 것을 발견했습니다.|
|al1055|참조된 ‘filename’ 어셈블리에 강력한 이름이 없습니다.<br /><br /> 이 오류는 강력한 이름의 어셈블리를 빌드하고 강력한 이름이 없는 어셈블리를 참조하는 경우에 발생합니다. 이 오류를 수정하려면 강력한 이름으로 어셈블리를 다시 생성하거나 *sn.exe*를 사용하여 어셈블리에 강력한 이름을 연결해야 합니다([*sn.exe*](sn-exe-strong-name-tool.md)에 대한 설명서 참조).<br /><br /> 일반적으로 이 오류는 Visual Studio IDE를 통해 C# 프로젝트에 COM 모듈 참조를 추가하는 경우와 같이 래퍼 어셈블리를 통해 COM 개체를 사용하는 경우에 발생합니다. 오류를 방지하려면 "래퍼 어셈블리 키 파일/이름" 프로젝트 속성에서 COM 래퍼 어셈블리에 대한 강력한 이름 키 파일을 지정할 수 있습니다.<br /><br /> tlbimp를 통해 래퍼 어셈블리를 만드는 경우 래퍼 어셈블리에 강력한 이름을 할당하는 방법에 대한 자세한 내용은 [tlbimp](tlbimp-exe-type-library-importer.md) 설명서를 참조하세요.<br /><br /> 어셈블리에 강력한 이름이 있는 경우 전역 어셈블리 캐시에 설치할 수 있습니다. 결과적으로, 참조된 어셈블리도 전역 어셈블리 캐시로 이동됩니다. 강력한 이름을 가진 어셈블리만 전역 어셈블리 캐시로 이동될 수 있습니다.|
|al1056|참조된 'filename' 어셈블리는 지역화된 위성 어셈블리입니다.<br /><br /> <xref:System.Reflection.AssemblyCultureAttribute> 특성을 사용하여 만든 어셈블리가 현재 어셈블리를 만들 때 참조되었습니다. <xref:System.Reflection.AssemblyCultureAttribute> 특성은 파일이 지역화된 위성 어셈블리이며 위성 어셈블리를 참조하는 데 적합하지 않음을 나타냅니다. 기본 부모 어셈블리를 대신 참조해야 합니다.|
|al1057|실행 파일을 지역화할 수 없습니다. 문화권은 항상 비어 있어야 합니다.<br /><br /> **/target:exe**를 사용하여 어셈블리를 만들고 있지만 **/culture**를 지정했습니다. *.exe*의 어셈블리는 Culture 필드에 정보를 포함할 수 없습니다.|
|al1058|'file'은 어셈블리이며 모듈로 추가할 수 없습니다.<br /><br /> C++ 컴파일에서 **/assemblymodule**(링커 옵션)에 어셈블리가 포함된 파일이 전달되었습니다.|
|al1059|알 수 없는 오류(code)<br /><br /> *Al.exe*가 알 수 없는 오류 코드(`code`)를 받았습니다.<br /><br /> 가능한 해결 방법은 다음과 같습니다.<br /><br /> Visual Studio를 다시 설치합니다.<br /><br /> Windows SDK를 다시 설치합니다.<br /><br /> 누락된 파일이 있는지 확인합니다.<br /><br /> 디스크 공간이 충분한지 확인합니다.<br /><br /> 메모리가 충분한지 확인합니다.<br /><br /> 파일에 액세스할 수 있는 다른 프로세스를 중지합니다.<br /><br /> 컴퓨터를 다시 부팅합니다.|
|al1060|해시를 만드는 동안 암호화 오류 발생 - reason<br /><br /> 다중 파일 어셈블리에 대한 파일 해시를 만드는 동안 오류가 발생했습니다.|
|al1061|'reason' 때문에 'option' 옵션을 설정할 수 없습니다.<br /><br /> 지정된 이유로 이 옵션에 대해 지정된 값이 잘못되었습니다.|
|al1062|'module' 모듈이 여러 번 지정되었습니다. 한 번만 포함됩니다.<br /><br /> 이 경고는 동일한 소스, 입력 또는 모듈 파일이 명령줄에서 여러 번 지정될 때 생성됩니다. 파일 이름을 한 번만 지정해야 합니다.|
|al1063|이 어셈블리의 여러 위치에서 'type' 공용 형식이 정의되었습니다. 'file1' 및 'file2'<br /><br /> 어셈블리의 둘 이상 모듈에서 동일한 형식이 발견되었습니다. 각 형식의 버전이 어셈블리에 하나씩만 포함될 수 있습니다.|
|al1064|/bugreport 옵션을 여러 개 지정할 수 없습니다.<br /><br /> **/bugreport** 옵션은 하나만 허용됩니다.|
|al1065|‘File Name’ 파일 이름이 너무 길거나 잘못되었습니다.<br /><br /> 지정된 파일 이름이 허용되는 최대값보다 깁니다.|
|al1066|'character' 문자는 명령줄 또는 지시 파일에서 사용할 수 없습니다.<br /><br /> 명령줄 또는 파일에서 잘못된 문자가 발견되었습니다.|
|al1067|'filename'은 텍스트 파일이 아니라 이진 파일입니다.<br /><br /> 파일이 텍스트가 아니라 이진 형식입니다.|
|al1068|'ModuleName' 모듈은 이 어셈블리에서 이미 정의되었습니다. 연결된 각 리소스 및 모듈에 고유한 파일 이름이 있어야 합니다.<br /><br /> 이 어셈블리에서 모듈이 두 번 이상 발생합니다.|
|al1069|동일한 약식 파일 이름을 가진 긴 파일 이름이 이미 있을 경우 'filename' 약식 파일 이름을 만들 수 없습니다.<br /><br /> 현재 파일 이름의 약식 버전이 이미 존재합니다. 예를 들어 LongFileName.cs를 컴파일한 다음 LongFi~1.cs 이름으로 다시 컴파일하면 다음과 비슷한 컴파일러 오류가 발생합니다. 긴 이름을 가진 컴파일러 출력 파일이 삭제되었지만 유사한 링커 파일이 남아 있는 경우 이 오류가 발생할 수 있습니다.|
|al1070|알 수 없는 어셈블리는 프로세서의 특정 모듈('Module Name')을 포함할 수 없습니다.<br /><br /> **/platform:agnostic**을 사용하여 빌드하는 경우(또는 **/platform**을 지정하지 않은 경우), **/addmodule**을 사용하여 agnostic이 아닌 모듈을 추가하려고 하면 오류가 생성됩니다. 이는 ia64 obj에 i386 obj 파일을 연결하려는 것과 같습니다.<br /><br /> 특정 모듈의 기본 소스는 C++입니다. **/addmodule**을 C++ 모듈과 함께 사용하는 경우 빌드 스크립트를 수정하여 적절한 **/platform** 설정을 지정해야 할 수도 있습니다.|
|al1072|어셈블리 및 'Module Name' 모듈은 다른 프로세서를 대상으로 할 수 없습니다.<br /><br /> 결과를 단일 프로세서에서 실행해야 하므로 서로 다른 프로세서를 대상으로 하는 어셈블리와 모듈을 연결할 수 없습니다.|
|al1073|참조된 ‘assembly’ 어셈블리가 다른 프로세서를 대상으로 합니다.<br /><br /> 결과를 단일 프로세서에서 실행해야 하므로 서로 다른 프로세서를 대상으로 하는 어셈블리를 연결할 수 없습니다.|
|al1074|'File Name'에 저장된 'Module Name' 모듈 이름은 해당 파일 이름과 일치해야 합니다.<br /><br /> 이는 링커에 필요합니다. 이 문제를 해결하려면 두 이름이 일치하도록 만듭니다.|
|al1075|서명 연기가 요청되었지만 키가 지정되지 않았습니다.<br /><br /> 어셈블리 서명이 연기된 경우 컴파일러는 서명을 컴퓨팅하거나 저장하지 않고 나중에 서명을 추가할 수 있도록 파일에 공간을 예약합니다.<br /><br /> 예를 들어 **/delaysign+** 를 사용하면 테스터를 통해 전역 캐시에 어셈블리를 넣을 수 있습니다. 테스트를 마친 후 어셈블리 링커 유틸리티를 통해 어셈블리에 프라이빗 키를 추가하여 어셈블리에 완전히 서명할 수 있습니다.|
|al1076|'type' 형식이 여러 어셈블리에 전달되었습니다. 'assembly' 및 'assembly'.<br /><br /> 각 형식을 하나의 어셈블리에만 전달할 수 있습니다.|
|al1077|'type' public 형식이 'assembly'에서 정의되고 'assembly'로 전달됩니다.<br /><br /> 생성되는 어셈블리에 중복된 public 형식이 있습니다. 하나는 유효한 형식 정의이고 다른 하나는 형식 전달자입니다.|

## <a name="example"></a>예

다음 명령은 `t2.netmodule` 모듈의 어셈블리를 사용하여 실행 파일 *t2a.exe*를 만듭니다. 진입점은 `Main`의 `MyClass` 메서드입니다.

```console
al t2.netmodule /target:exe /out:t2a.exe /main:MyClass.Main
```

## <a name="see-also"></a>참고 항목

- [도구](index.md)
- [*Sn.exe* (Strong Name Tool)](sn-exe-strong-name-tool.md)(Sn.exe(강력한 이름 도구))
- [*Gacutil.exe* (Global Assembly Cache Tool)](gacutil-exe-gac-tool.md)(Gacutil.exe(전역 어셈블리 캐시 도구))
- [어셈블리를 사용한 프로그래밍](../../standard/assembly/program.md)
- [명령 프롬프트](developer-command-prompt-for-vs.md)
