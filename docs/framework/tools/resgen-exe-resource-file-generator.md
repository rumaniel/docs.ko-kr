---
title: Resgen.exe(리소스 파일 생성기)
ms.date: 03/30/2017
helpviewer_keywords:
- resource files, .resources files
- resource files, .resx files
- resx files (resource files)
- .resources files
- files, converting
- Resource File Generator
- .resx files
- Resgen.exe
- resource files, converting
- converting files, Resource File Generator
- binary resources files
- embedding files in runtime binary executable
ms.assetid: 8ef159de-b660-4bec-9213-c3fbc4d1c6f4
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2db85781b48fd75c3d2ef70834fd8451647f6917
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71044229"
---
# <a name="resgenexe-resource-file-generator"></a>Resgen.exe(리소스 파일 생성기)
리소스 파일 생성기(Resgen.exe)를 사용하면 텍스트 파일(.txt 또는 .restext)과 XML 기반 리소스 형식 파일(.resx)을 런타임 이진 실행 파일에 포함하거나 위성 어셈블리에 포함할 수 있는 공용 언어 런타임의 이진 파일(.resources)로 변환할 수 있습니다. [리소스 파일 만들기](../resources/creating-resource-files-for-desktop-apps.md)를 참조하세요.  
  
 Resgen.exe는 다음 작업을 수행하는 범용 리소스 변환 유틸리티입니다.  
  
- .txt 또는 .restext 파일을 .resources 또는 .resx 파일로 변환합니다. .restext 파일의 형식은 .txt 파일의 형식과 동일합니다. 그러나 .restext 확장명을 통해 리소스 정의를 포함하고 있는 텍스트 파일을 보다 쉽게 확인할 수 있습니다.  
  
- .resources 파일을 텍스트 또는 .resx 파일로 변환합니다.  
  
- .resx 파일을 텍스트 또는 .resources 파일로 변환합니다.  
  
- 어셈블리로부터 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 응용 프로그램에서 사용하기 적합한 .resw 파일로 문자열 리소스를 추출합니다.  
  
- 개별 명명된 리소스와 <xref:System.Resources.ResourceManager> 인스턴스에 대한 액세스를 제공하는 강력한 형식의 클래스를 만듭니다.  
  
 Resgen.exe에서 어떤 이유로든 오류가 발생하면 –1 값이 반환됩니다.  
  
 Resgen.exe의 도움말을 보려면 다음 명령을 명령 구문 및 Resgen.exe에 대한 옵션을 표시하도록 지정하는 옵션 없이 사용할 수 있습니다.  
  
```console  
resgen  
```  
  
 또한 `/?` 스위치를 사용할 수도 있습니다.  
  
```console  
resgen /?  
```  
  
 Resgen.exe를 사용하여 이진 .resources 파일을 만드는 경우 언어 컴파일러를 사용하여 이진 파일을 실행 가능 어셈블리에 포함하거나 [어셈블리 링커(Al.exe)](al-exe-assembly-linker.md)를 사용하여 위성 어셈블리에 컴파일할 수 있습니다.  
  
 이 도구는 자동으로 Visual Studio와 함께 설치됩니다. 이 도구를 실행하려면 Visual Studio용 개발자 명령 프롬프트(또는 Windows 7의 Visual Studio 명령 프롬프트)를 사용합니다. 자세한 내용은 [명령 프롬프트](developer-command-prompt-for-vs.md)를 참조하세요.  
  
 명령 프롬프트에 다음을 입력합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
resgen  [/define:symbol1[,symbol2,...]] [/useSourcePath] filename.extension  | /compile filename.extension... [outputFilename.extension] [/r:assembly] [/str:lang[,namespace[,class[,file]]] [/publicclass]]   
```  
  
```console  
resgen filename.extension [outputDirectory]  
```  
  
## <a name="parameters"></a>매개 변수  
  
|매개 변수 또는 스위치|설명|  
|-------------------------|-----------------|  
|`/define:` *symbol1*[, *symbol2*,...]|.NET Framework 4.5로 시작하며 텍스트 기반(.txt 또는 .restext) 리소스 파일로 된 조건부 컴파일을 지원합니다. *symbol*이 `#ifdef` 구문 안의 입력 텍스트 파일에 포함된 기호에 해당하는 경우 연결된 문자열 리소스가 .resources 파일에 포함됩니다. 입력 텍스트 파일에 `#if !` 문이 `/define` 스위치에 의해 정의되지 않은 기호와 함께 포함되어 있는 경우 연결된 문자열 리소스는 리소스 파일에 포함됩니다.<br /><br /> `/define`은 텍스트가 아닌 파일과 함께 사용하는 경우 무시됩니다. 기호는 대/소문자를 구분합니다.<br /><br /> 이 옵션에 대한 자세한 내용은 이 항목의 뒤에 나오는 [리소스 조건부 컴파일](#Conditional)을 참조하세요.|  
|`useSourcePath`|입력 파일의 현재 디렉터리를 사용하여 상대 경로를 확인하도록 지정합니다.|  
|`/compile`|단일 일괄 작업을 통해 여러 .resources 파일로 변환할 여러 .resx 또는 텍스트 파일을 지정할 수 있습니다. 이 옵션을 지정하지 않으면 입력 파일 인수를 하나만 지정할 수 있습니다. 출력 파일의 이름은 *filename*.resources입니다.<br /><br /> 이 옵션은 `/str:` 옵션과 함께 사용할 수 없습니다.<br /><br /> 이 옵션에 대한 자세한 내용은 이 항목의 뒤에 나오는 [다중 파일 컴파일 또는 변환](#Multiple)을 참조하세요.|  
|`/r:` `assembly`|지정한 어셈블리에서 메타데이터를 참조합니다. .Resx 파일을 변환할 때 사용하고 Resgen.exe를 통해 개체 리소스를 serialize하거나 deserialize할 수 있습니다. C# 및 Visual Basic 컴파일러에 대한 `/reference:` 또는 `/r:` 옵션과 유사합니다.|  
|`filename.extension`|변환할 입력 파일의 이름을 지정합니다. 이 테이블 앞에 나타난 첫째, 긴 명령줄 구문을 사용하는 경우 `extension`은 다음 중 하나여야 합니다.<br /><br /> .txt 또는 .restext<br /> .resources 또는 .resx 파일로 변환할 텍스트 파일입니다. 텍스트 파일에는 문자열 리소스만 포함될 수 있습니다. 파일 형식에 대한 자세한 내용은 [리소스 파일 만들기](../resources/creating-resource-files-for-desktop-apps.md)에서 "텍스트 파일의 리소스" 섹션을 참조하세요.<br /><br /> .resx<br /> .resources 또는 텍스트 파일(.txt 또는 .restext)로 변환할 XML 기반 리소스 파일입니다.<br /><br /> .resources<br /> .resx 또는 텍스트(.txt 또는 .restext) 파일로 변환할 이진 리소스 파일입니다.<br /><br /> 이 테이블 앞에 표시되는 두 번째, 짧은 명령줄 구문을 사용하는 경우 `extension`은 다음과 같아야 합니다.<br /><br /> .exe 또는 .dll<br /> [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 응용 프로그램을 개발하는 데 사용하는 .resw 파일로 문자열 리소스를 추출할 .NET Framework 어셈블리(실행 파일 또는 라이브러리)입니다.|  
|`outputFilename.extension`|만들 리소스 파일의 이름 및 유형을 지정합니다.<br /><br /> .txt, .restext 또는 .resx 파일을 .resources 파일로 변환하는 경우 이 인수는 선택적 인수입니다. `outputFilename`을 지정하지 않으면 Resgen.exe에서는 입력 `filename`에 .resources 확장명을 추가하고 `filename,extension`이 들어 있는 디렉터리에 해당 파일을 씁니다.<br /><br /> `outputFilename.extension` 인수는 .resources 파일에서 변환할 때 사용되는 필수 항목입니다. .resources 파일을 XML 기반 리소스 파일로 변환할 때에는 .resx 확장명을 갖는 파일 이름을 지정합니다. .resources 파일을 텍스트 파일로 변환할 때는 .txt 또는 .restext 확장명을 갖는 파일 이름을 지정합니다. .resources 파일에 문자열 값만 있는 경우에는 .resources 파일을 .txt 파일로만 변환해야 합니다.|  
|`outputDirectory`|[!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 응용 프로그램의 경우 `filename.extension`에 있는 문자열 리소스를 포함하는 .resw 파일은 디렉터리를 지정합니다. `outputDirectory`가 이미 있어야 합니다.|  
|`/str:` `language[,namespace[,classname[,filename]]]`|`language` 옵션에 지정된 프로그래밍 언어로 강력한 형식의 리소스 클래스 파일을 만듭니다. `language`는 다음과 같은 리터럴 중 하나로 구성할 수 있습니다.<br /><br /> -   C#의 경우: `c#`, `cs` 또는 `csharp`입니다.<br />-   Visual Basic의 경우: `vb` 또는 `visualbasic`입니다.<br />-   VBScript의 경우: `vbs` 또는 `vbscript`입니다.<br />-   C++의 경우: `c++`, `mc` 또는 `cpp`입니다.<br />-   JavaScript의 경우: `js`, `jscript` 또는 `javascript`입니다.<br /><br /> `namespace` 옵션은 프로젝트의 기본 네임스페이스를 지정하고, `classname` 옵션은 생성되는 클래스의 이름을 지정하고, `filename` 옵션은 클래스 파일의 이름을 지정합니다.<br /><br /> `/str:` 옵션에서는 입력 파일을 하나만 지정할 수 있으므로 이 옵션과 `/compile` 옵션을 함께 사용할 수 없습니다.<br /><br /> `namespace`만 지정하고 `classname`은 지정하지 않을 경우 출력 파일 이름에서 마침표를 밑줄로 대체하는 등의 방식으로 클래스 이름이 파생됩니다. 따라서 강력한 형식의 리소스가 제대로 작동하지 않을 수도 있습니다. 이 문제를 방지하려면 클래스 이름과 출력 파일 이름을 모두 지정해야 합니다.<br /><br /> 이 옵션에 대한 자세한 내용은 이 항목의 뒤에 나오는 [강력한 형식의 리소스 클래스 생성](#Strong)을 참조하세요.|  
|`/publicClass`|공용 클래스로 강력한 형식의 리소스 클래스를 만듭니다. 기본적으로 리소스 클래스는 C#에서 `internal`이고 Visual Basic에서는 `Friend`입니다.<br /><br /> `/str:` 옵션을 사용하지 않으면 이 옵션은 무시됩니다.|  
  
## <a name="resgenexe-and-resource-file-types"></a>Resgen.exe 및 리소스 파일 생성기  
 Resgen.exe를 통해 리소스를 성공적으로 변환하기 위해 텍스트 및 .resx 파일은 올바른 형식을 따라야 합니다.  
  
### <a name="text-txt-and-restext-files"></a>텍스트(.txt 및 .restext) 파일  
 텍스트 파일(.txt 또는 .restext)은 문자열 리소스만 포함할 수 있습니다. 문자열을 여러 가지 언어로 번역해야 하는 애플리케이션을 작성하는 경우에는 문자열 리소스를 사용하는 것이 좋습니다. 예를 들어, 해당 문자열 리소스를 사용하면 메뉴 문자열을 쉽게 지역화할 수 있습니다. Resgen.exe를 사용하여 이름/값 쌍이 들어 있는 텍스트 파일을 읽습니다. 여기에서 이름은 해당 리소스를 설명하는 문자열이고, 값은 리소스 문자열 자체입니다.  
  
> [!NOTE]
> .txt 및 .restext 파일 형식에 대한 자세한 내용은 [리소스 파일 만들기](../resources/creating-resource-files-for-desktop-apps.md)에서 "텍스트 파일의 리소스" 섹션을 참조하세요.  
  
 리소스를 포함하고 있는 텍스트 파일은 기본 라틴 범위(U+007F까지)의 문자만 포함하지 않는 경우 UTF-8 또는 유니코드(UTF-16) 인코딩으로 저장해야 합니다. Resgen.exe에서는 ANSI 인코딩으로 저장된 텍스트 파일을 처리할 때 확장된 ANSI 문자를 제거합니다.  
  
 Resgen.exe를 사용하여 텍스트 파일에 중복된 리소스 이름이 있는지 확인합니다. 텍스트 파일에 중복된 리소스 이름이 있으면 Resgen.exe에서는 경고를 표시하고 두 번째 값을 무시합니다.  
  
### <a name="resx-files"></a>.resx 파일  
 .resx 리소스 파일 형식은 XML 엔트리로 구성되며 텍스트 파일과 유사한 방식으로 이 XML 엔트리 내에 문자열 리소스를 지정할 수 있습니다. 텍스트 파일과 비교했을 때 .resx 파일에는 개체를 포함하거나 지정할 수 있다는 이점이 있습니다. .resx 파일을 볼 때 그림과 같은 포함 개체의 이진 형식이 리소스 매니페스트의 일부인 경우에는 해당 이진 형식을 볼 수 있습니다. 텍스트 파일과 마찬가지로 .resx 파일을 텍스트 편집기(예: 메모장 또는 Microsoft Word)에서 열어 내용을 쓰고 구문 분석 및 조작할 수 있습니다. 이러한 작업을 수행하려면 XML 태그 및 .resx 파일의 구조에 대해 잘 알고 있어야 합니다. .resx 파일 형식에 대한 자세한 내용은 [리소스 파일 만들기](../resources/creating-resource-files-for-desktop-apps.md)에서 ".resx 파일의 리소스" 섹션을 참조하세요.  
  
 비문자열 포함 개체가 들어 있는 .resources 파일을 만들려면 Resgen.exe를 사용하여 개체가 들어 있는 .resx 파일을 변환하거나, <xref:System.Resources.ResourceWriter> 클래스에서 제공하는 메서드를 호출하여 코드에서 개체 리소스를 해당 파일에 직접 추가해야 합니다.  
  
 개체가 들어 있는 .resx 또는 .resources 파일을 Resgen.exe를 사용하여 텍스트 파일로 변환하면 모든 문자열 리소스는 올바르게 변환되지만 문자열이 아닌 개체의 데이터 형식도 파일에 문자열로 기록됩니다. 따라서 변환 시 포함 개체가 손실되고 Resgen.exe에서는 리소스 검색 시 오류가 발생했다는 메시지를 전달합니다.  
  
### <a name="converting-between-resources-file-types"></a>리소스 파일 형식 간 변환  
 다른 리소스 파일 형식 사이에 변환하는 경우, Resgen.exe는 변환을 수행할 수 없거나 원본 및 대상 파일 형식에 따라 특정 리소스에 대한 정보가 손실될 수 있습니다. 다음 표에서는 리소스 파일 형식을 다른 형식으로 변환하는 경우 성공적으로 수행되는 변환의 형식을 지정합니다.  
  
|변환 원본|텍스트 파일로|.resx 파일로|.resw 파일로|.resources 파일로|  
|------------------|------------------|-------------------|-------------------|------------------------|  
|텍스트(.txt 또는 .restext) 파일|--|문제 없음|지원 안 함|문제 없음|  
|.resx 파일|파일에 문자열이 아닌 리소스(파일 링크 포함)를 포함하는 경우 변환 실패|--|지원 안 함|문제 없음|  
|.resources 파일|파일에 문자열이 아닌 리소스(파일 링크 포함)를 포함하는 경우 변환 실패|문제 없음|지원 안 함|--|  
|.exe 또는 .dll 어셈블리|지원 안 함|지원 안 함|문자열 리소스(경로 이름 포함)만 리소스로 인식됩니다.|지원 안 함|  
  
## <a name="performing-specific-resgenexe-tasks"></a>특정 Resgen.exe 작업을 수행합니다.  
 텍스트 기반 또는 XML 기반 리소스 파일을 바이너리 파일로 컴파일, <xref:System.Resources.ResourceManager> 기능 래핑, 리소스로의 액세스를 제공하는 클래스 생성 등 다양한 방법으로 Resgen.exe를 사용할 수 있습니다. 이 단원에서는 각 작업에 대해 자세하게 설명합니다.  
  
- [이진 파일에 리소스 컴파일](resgen-exe-resource-file-generator.md#Compiling)  
  
- [리소스 파일 형식 간 변환](resgen-exe-resource-file-generator.md#Convert)  
  
- [다중 파일 컴파일 또는 변환](resgen-exe-resource-file-generator.md#Multiple)  
  
- [.resw 파일에 리소스 내보내기](resgen-exe-resource-file-generator.md#Exporting)  
  
- [리소스 조건부 컴파일](resgen-exe-resource-file-generator.md#Conditional)  
  
- [강력한 형식의 리소스 클래스 생성](resgen-exe-resource-file-generator.md#Strong)  
  
<a name="Compiling"></a>   
### <a name="compiling-resources-into-a-binary-file"></a>이진 파일에 리소스 컴파일  
 resgen.exe는 텍스트 기반 리소스 파일(.txt 또는 .restext) 또는 XML 기반 리소스 파일(.resx 파일)을 이진 .resources 파일로 컴파일하는 데 가장 일반적으로 사용됩니다. 언어 컴파일러를 사용하여 메인 어셈블리에 출력 파일을 포함시키거나, [어셈블리 링커(Al.exe)](al-exe-assembly-linker.md)를 사용하여 위성 어셈블리에 포함시킬 수 있습니다.  
  
 리소스 파일을 컴파일하는 구문은 다음과 같습니다.  
  
```console  
resgen inputFilename [outputFilename]   
```  
  
 여기서 매개 변수는 다음과 같습니다.  
  
 `inputFilename`  
 컴파일할 리소스 파일의 파일 이름(확장명 포함)입니다. Resgen.exe는 .txt, .restext 또는 .resx 확장명을 가진 파일만 컴파일합니다.  
  
 `outputFilename`  
 출력 파일의 이름입니다. `outputFilename`을 생략하면 Resgen.exe가 `inputFilename`과 같은 디렉터리에 루트 파일 이름이 `inputFilename`인 .resources 파일을 만듭니다. `outputFilename`에 디렉터리 경로가 포함되는 경우 디렉터리가 있어야 합니다.  
  
 파일 이름에 지정하고 루트 파일 이름과 마침표로 구분하여 .resources 파일에 대한 완전히 정규화된 네임스페이스를 제공합니다. 예를 들어 `outputFilename`이 `MyCompany.Libraries.Strings.resources`이면 네임스페이스는 MyCompany.Libraries입니다.  
  
 다음 명령을 사용하여 Resources.txt에 있는 이름/값 쌍을 읽고 Resources.resources라는 이진 리소스 파일을 작성합니다. 출력 파일 이름은 명시적으로 지정되지 않기 때문에 기본적으로 입력 파일과 같은 이름을 받습니다.  
  
```console  
resgen Resources.txt   
```  
  
 다음 명령을 사용하여 Resources.restext에 있는 이름/값 쌍을 읽고 StringResources.resources라는 이진 리소스 파일을 작성합니다.  
  
```console  
resgen Resources.restext StringResources.resources  
```  
  
 다음 명령을 사용하여 Resources.resx라는 XML 기반 입력 파일을 읽고 Resources.resources라는 이진 .resources 파일을 작성합니다.  
  
```console  
resgen Resources.resx Resources.resources  
```  
  
<a name="Convert"></a>   
### <a name="converting-between-resource-file-types"></a>리소스 파일 형식 간 변환  
 텍스트 기반 또는 XML 기반 리소스 파일을 이진 .resources 파일로 컴파일하는 것 이외에, Resgen.exe는 지원되는 모든 파일 형식을 지원되는 다른 파일 형식으로 변환할 수 있습니다. 이것은 다음과 변환을 수행할 수 있음을 의미합니다.  
  
- .txt 및 .restext 파일을 .resx 파일로 변환합니다.  
  
- .resx 파일을 .txt 및 .restext 파일로 변환합니다.  
  
- .resources 파일을 .txt 및 .restext 파일로 변환합니다.  
  
- .resources 파일을 .resx 파일로 변환합니다.  
  
 구문은 이전 단원에 나와 있는 것과 동일합니다.  
  
 또한, Resgen.exe을 사용하여 .NET Framework 어셈블리의 포함 리소스를 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 응용 프로그램용 .resw 파일로 변환할 수 있습니다.  
  
 다음 명령을 사용하여 이진 리소스 파일 Resources.resources를 읽고 Resources.resx라는 XML 기반 출력 파일을 작성합니다.  
  
```console  
resgen Resources.resources Resources.resx  
```  
  
 다음 명령을 사용하여 StringResources.txt라는 텍스트 기반 리소스 파일을 읽고, LibraryResources.resx라는 XML 기반 입력 파일을 작성합니다. 문자열 리소스를 포함하는 용도 외에 .resx 파일은 문자열 이외의 리소스를 저장하는 데에도 사용할 수 있습니다.  
  
```console  
resgen StringResources.txt LibraryResources.resx  
```  
  
 다음 두 명령은 Resources.resx라는 XML 기반 입력 파일을 읽고 Resources.txt 및 Resources.restext라는 텍스트 파일을 작성합니다. .resx 파일에 포함 개체가 있으면 텍스트 파일로 정확하게 변환되지 않습니다.  
  
```console  
resgen Resources.resx Resources.txt  
resgen Resources.resx Resources.restext  
```  
  
<a name="Multiple"></a>   
### <a name="compiling-or-converting-multiple-files"></a>다중 파일 컴파일 또는 변환  
 `/compile` 스위치를 사용하여 단일 연산에서 하나의 포맷으로부터 다른 포맷으로 리소스 파일 목록을 전환할 수 있습니다. 사용되는 구문은 다음과 같습니다.  
  
```console  
resgen /compile filename.extension [filename.extension...]  
```  
  
 다음 명령은 세 파일, StringResources.txt, TableResources.resw 및 ImageResources.resw를 StringResources.resources, TableResources.resources 및 ImageResources.resources라는 별도의 resources 파일로 컴파일합니다.  
  
```console  
resgen /compile StringResources.txt TableResources.resx ImageResources.resx  
```  
  
<a name="Exporting"></a>   
### <a name="exporting-resources-to-a-resw-file"></a>.resw 파일에 리소스 내보내기  
 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 응용 프로그램을 개발하는 경우, 기존 데스크톱 응용 프로그램의 리소스를 사용하려는 경우가 있습니다. 하지만 두 종류의 애플리케이션은 다른 파일 형식을 지원합니다. 데스크톱 응용 프로그램에서 텍스트(.txt 또는.restext) 또는.resx 파일의 리소스는 이진 .resources 파일로 컴파일됩니다. [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 응용 프로그램에서 .resw 파일은 이진 패키지 리소스 인덱스(PRI) 파일로 컴파일됩니다. 실행 가능한 또는 위성 어셈블리에서 리소스를 추출하거나 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 응용 프로그램 개발 시 사용할 수 있는 하나 이상의 .resw 파일을 작성하여 이 간격을 연결하는 데 Resgen.exe을 사용할 수 있습니다.  
  
> [!IMPORTANT]
> Visual Studio는 휴대용 라이브러리에서 리소스를 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 응용 프로그램에 통합시키는 데 필요한 모든 변환을 자동으로 처리합니다. 어셈블리에서 리소스를 .resw 파일 형식으로 변환하기 위해 .Resgen.exe를 직접 사용하는 것은 Visual Studio 외부에서 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 응용 프로그램을 개발하려고 하는 개발자에게만 필요합니다.  
  
 어셈블리에서 .resw 파일을 생성하는 구문은 다음과 같습니다.  
  
```console  
resgen filename.extension  [outputDirectory]  
```  
  
 여기서 매개 변수는 다음과 같습니다.  
  
 `filename.extension`  
 .NET Framework 어셈블리(실행 파일 또는 .DLL)의 이름입니다. 파일에 리소스가 포함되어 있으면 Resgen.exe는 파일을 만들지 않습니다.  
  
 `outputDirectory`  
 .resw 파일을 쓸 기존 디렉터리입니다. `outputDirectory`를 생략하면 .resw 파일이 현재 디렉터리에 기록됩니다. Resgen.exe는 어셈블리에 각 .resources 파일에 대한 .resw 파일을 만듭니다. .resw 파일의 루트 파일 이름은 .resources 파일의 루트 이름과 같습니다.  
  
 다음 명령은 MyApp.exe에 포함된 각 resources 파일에 대한 Win8Resources 디렉터리에 .resw 파일을 만듭니다.  
  
```console  
resgen MyApp.exe Win8Resources  
```  
  
<a name="Conditional"></a>   
### <a name="conditionally-compiling-resources"></a>리소스 조건부 컴파일  
 .NET Framework 4.5로 시작하는 Resgen.exe에서는 텍스트(.txt 및 .restext) 파일로 된 문자열 리소스의 조건부 컴파일을 지원합니다. 이것은 여러 빌드 구성에 단일 텍스트 기반 리소스 파일을 사용할 수 있도록 합니다.  
  
 .txt 또는 .restext 파일에서 기호가 정의된 경우 `#ifdef`...`#endif` 구문을 사용하며 이진 .resources 파일에 리소스를 포함하고, 기호가 정의되지 않은 경우 `#if !`...`#endif` 구문을 사용하여 리소스를 포함합니다. 컴파일할 때 `/define:` 옵션과 쉼표로 구분된 기호 목록을 사용하여 기호를 정의합니다. 비교는 대/소문자를 구분합니다. `/define`으로 정의된 기호의 대/소문자는 컴파일될 텍스트 파일에 있는 기호의 대/소문자와 일치해야 합니다.  
  
 예를 들어, 다음의 UIResources.rext라는 파일에는 `AppTitle`, `PRODUCTION` 또는 `CONSULT`이라는 기호가 정의되어 있는지 여부에 따라 3개의 값 중 하나를 사용할 수 있는 `RETAIL`이라는 문자열 리소스가 포함되어 있습니다.  
  
```text
#ifdef PRODUCTION  
AppTitle=My Software Company Project Manager   
#endif  
#ifdef CONSULT  
AppTitle=My Consulting Company Project Manager  
#endif  
#ifdef RETAIL  
AppTitle=My Retail Store Project Manager  
#endif  
FileMenuName=File  
```  
  
 그런 다음 파일은 다음 명령을 사용하여 이진 .resources 파일로 컴파일됩니다.  
  
```console  
resgen /define:CONSULT UIResources.restext  
```  
  
 그러면 두 문자열 리소스가 있는 리소스 파일이 생성됩니다. `AppTitle` 리소스 값은 "내 컨설팅 회사 프로젝트 관리자"입니다.  
  
<a name="Strong"></a>   
### <a name="generating-a-strongly-typed-resource-class"></a>강력한 형식의 리소스 클래스 생성  
 Resgen.exe는 강력한 형식의 리소스를 지원하고, 이러한 리소스는 컴파일 타임에 읽기 전용의 정적 속성을 포함하는 클래스를 만들어 리소스에 대한 액세스를 캡슐화합니다. 이 기능은 리소스를 검색하기 위해 <xref:System.Resources.ResourceManager> 클래스의 메서드를 직접 호출하는 대신 사용할 수 있습니다. `/str` 클래스의 함수를 래핑하는 Resgen.exe의 <xref:System.Resources.Tools.StronglyTypedResourceBuilder> 옵션을 사용하여 강력한 형식의 리소스 지원이 가능합니다. `/str` 옵션을 지정하면 입력 매개 변수에서 참조되는 리소스와 일치하는 강력한 형식의 속성이 포함된 클래스가 Resgen.exe의 출력이 됩니다. 이 클래스는 처리된 파일에서 사용할 수 있는 리소스에 대한 강력한 형식의 읽기 전용 액세스를 제공합니다.  
  
 강력한 형식의 리소스를 만드는 구문은 다음과 같습니다.  
  
```console  
resgen inputFilename [outputFilename] /str:language[,namespace,[classname[,filename]]] [/publicClass]  
```  
  
 매개 변수 및 스위치는 다음과 같습니다.  
  
 `inputFilename`  
 강력한 형식의 리소스 클래스를 생성할 리소스 파일의 파일 이름입니다(확장명 포함). 파일은 텍스트 기반, XML 기반 또는 이진 .resources 파일일 수 있으며 .txt, .restext, .resw 또는 .resources 확장명을 가질 수 있습니다.  
  
 `outputFilename`  
 출력 파일의 이름입니다. `outputFilename`에 디렉터리 경로가 포함되는 경우 디렉터리가 있어야 합니다. `outputFilename`을 생략하면 Resgen.exe가 `inputFilename`과 같은 디렉터리에 루트 파일 이름이 `inputFilename`인 .resources 파일을 만듭니다.  
  
 `outputFilename`은 텍스트 기반 XML 기반 또는 이진 .resources 파일일 수 있습니다. `outputFilename`의 파일 확장명이 `inputFilename`의 파일 확장명과 다를 경우 Resgen.exe는 파일 변환을 수행합니다.  
  
 `inputFilename`이 .resources 파일인 경우 `outputFilename`도 .resources 파일이면 Resgen.exe가 .resources 파일을 복사합니다. `outputFilename`을 생략할 경우 Resgen.exe가 `inputFilename`을 동일한 .resources 파일로 덮어씁니다.  
  
 *language*  
 강력한 형식의 리소스 클래스에 대한 소스 코드를 생성할 언어입니다. 가능한 값은 `cs`, `C#`, `csharp`(C# 코드), `vb`, `visualbasic`(Visual Basic 코드), `vbs`, `vbscript`(VBScript 코드), `c++`, `mc`, `cpp`(C++ 코드)입니다.  
  
 *namespace*  
 강력한 형식의 리소스 클래스에 포함된 네임스페이스입니다. .Resources 파일과 리소스 클래스의 네임스페이스는 같아야 합니다. `outputFilename`에서 네임스페이스를 지정하는 방법에 대한 자세한 내용은 [이진 파일에 리소스 컴파일](resgen-exe-resource-file-generator.md#Compiling)을 참조하세요. *namespace*를 생략하면 리소스 클래스가 네임스페이스에 포함되지 않습니다.  
  
 *classname*  
 강력한 형식의 리소스 클래스의 이름입니다. 이 값은 .resources 파일의 루트 이름과 일치해야 합니다. 예를 들어, Resgen.exe에서 MyCompany.Libraries.Strings.resources라는 이름의 .resources 파일을 생성하면 강력한 형식의 리소스 클래스의 이름은 Strings입니다. *classname*을 생략할 경우 생성된 클래스는 `outputFilename`의 루트 이름에서 파생됩니다. `outputFilename`을 생략할 경우 생성된 클래스는 `inputFilename`의 루트 이름에서 파생됩니다.  
  
 *classname*은 공백과 같은 유효하지 않은 문자를 포함할 수 없습니다. *classname*이 공백을 포함하거나 *classname*이 *inputFilename*에서 기본적으로 생성되었고 *inputFilename*이 공백을 포함한다면, Resgen.exe는 유효하지 않은 모든 문자를 밑줄(\_)로 대체합니다.  
  
 *filename*  
 클래스 파일의 이름입니다.  
  
 `/publicclass`  
 강력한 형식의 리소스 클래스를 `internal`(C#) 또는 `Friend`(Visual Basic)가 아닌 공용으로 설정합니다. 이렇게 하면 리소스가 포함된 어셈블리 외부에서 리소스를 액세스할 수 있습니다.  
  
> [!IMPORTANT]
> 강력한 형식의 리소스 클래스를 만들 때 .resources 파일의 이름은 생성된 코드의 네임스페이스 및 클래스 이름과 일치해야 합니다. 하지만 Resgen.exe를 사용하면 호환되지 않는 이름을 가진 .resources 파일을 생성하는 옵션을 지정할 수 있습니다. 이 문제를 해결하려면 생성된 후에 출력 파일 이름을 바꿉니다.  
  
 강력한 형식의 리소스 클래스에는 다음과 같은 구성원이 있습니다.  
  
- 강력한 형식의 리소스 클래스를 인스턴스화하는 데 사용할 수 있는 매개 변수 없는 생성자입니다.  
  
- 강력한 형식의 리소스를 관리하는 `static` 인스턴스를 반환하는 `Shared`(C#) 또는 `ResourceManager`(Visual Basic) 및 읽기 전용 <xref:System.Resources.ResourceManager> 속성입니다.  
  
- 리소스 검색에 사용되는 문화권을 설정할 수 있도록 하는 정적 `Culture` 속성입니다. 기본적으로 값은 현재 UI 문화권이 사용됨을 의미하는 `null`입니다.  
  
- 하나의 `static`(C#) 또는 `Shared`(Visual Basic) 및 .resources 파일의 각 리소스에 대한 읽기 전용 속성입니다. 속성 이름은 리소스 이름입니다.  
  
 예를 들어, 다음 명령은 StringResources.txt라는 리소스 파일을 StringResources.resources로 컴파일하고 리소스 관리자에 액세스하는 데 사용할 수 있는 StringResources.vb라는 Visual Basic 소스 코드 파일에서 `StringResources`라는 클래스를 생성합니다.  
  
```console  
resgen StringResources.txt /str:vb,,StringResources   
```  
  
## <a name="see-also"></a>참고 항목

- [도구](index.md)
- [데스크톱 앱의 리소스](../resources/index.md)
- [리소스 파일 만들기](../resources/creating-resource-files-for-desktop-apps.md)
- [Al.exe(어셈블리 링커)](al-exe-assembly-linker.md)
- [명령 프롬프트](developer-command-prompt-for-vs.md)
