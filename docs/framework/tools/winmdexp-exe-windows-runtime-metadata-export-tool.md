---
title: Winmdexp.exe(Windows 런타임 메타데이터 내보내기 도구)
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Runtime Metadata Export Tool
- Winmdexp.exe
ms.assetid: d2ce0683-343d-403e-bb8d-209186f7a19d
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 0b3cf60d670e7fdfa624599bc0eeddc99219c202
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71044014"
---
# <a name="winmdexpexe-windows-runtime-metadata-export-tool"></a>Winmdexp.exe(Windows 런타임 메타데이터 내보내기 도구)
Windows 런타임 메타데이터 내보내기 도구(Winmdexp.exe)는 .NET Framework 모듈을 Windows 런타임 메타데이터가 포함된 파일로 변환합니다. .NET Framework 어셈블리 및 Windows 런타임 메타데이터 파일이 같은 물리적 형식을 사용하지만 메타데이터 테이블의 내용에 차이가 있습니다. 즉, .NET Framework 어셈블리는 Windows 런타임 구성 요소로 자동으로 사용할 수 있습니다. .NET Framework 모듈을 Windows 런타임 구성 요소로 전환하는 프로세스를 ‘내보내기’라고 합니다.  .NET Framework 4.5 및 .NET Framework 4.5.1에서 결과 Windows 메타데이터(.winmd) 파일은 메타데이터와 구현이 모두 포함됩니다.  
  
 **Microsoft Store**에 있는 Visual Studio 2013 또는 Visual Studio 2012의 C# 및 Visual Basic용 **Windows 런타임 구성 요소** 템플릿을 사용할 경우 컴파일러 대상은 .winmdobj 파일이고, 이후 빌드 단계에서는 Winmdexp.exe를 호출하여 .winmdobj 파일을 .winmd 파일로 내보냅니다. 이러한 방법으로 Windows 런타임 구성 요소를 빌드하는 것이 좋습니다. Visual Studio가 제공하는 것보다 빌드 프로세스를 더 자세하게 제어하려면 Winmdexp.exe를 사용합니다.  
  
 이 도구는 자동으로 Visual Studio와 함께 설치됩니다. 이 도구를 실행하려면 Visual Studio용 개발자 명령 프롬프트(또는 Windows 7의 Visual Studio 명령 프롬프트)를 사용합니다. 자세한 내용은 [명령 프롬프트](developer-command-prompt-for-vs.md)를 참조하세요.  
  
 명령 프롬프트에 다음을 입력합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
winmdexp [options] winmdmodule  
```  
  
## <a name="parameters"></a>매개 변수  
  
|인수 또는 옵션|설명|  
|------------------------|-----------------|  
|`winmdmodule`|내보낼 모듈(.winmdobj)을 지정합니다. 하나의 모듈만 허용됩니다. 이 모듈을 만들려면 `/target` 컴파일러 옵션을 `winmdobj` 대상과 함께 사용합니다. [/target:winmdobj(C# 컴파일러 옵션)](../../csharp/language-reference/compiler-options/target-winmdobj-compiler-option.md) 또는 [/target(Visual Basic)](../../visual-basic/reference/command-line-compiler/target.md)을 참조하세요.|  
|`/docfile:` `docfile`<br /><br /> `/d:` `docfile`|Winmdexp.exe가 생성하는 출력 XML 문서 파일을 지정합니다. .NET Framework 4.5에서는 기본적으로 출력 파일이 XML 설명서 파일과 같습니다.|  
|`/moduledoc:` `docfile`<br /><br /> `/md:` `docfile`|컴파일러가 `winmdmodule`로 생성한 XML 문서 파일의 이름을 지정합니다.|  
|`/modulepdb:` `symbolfile`<br /><br /> `/mp:` `symbolfile`|`winmdmodule`에 대한 기호를 포함하는 프로그램 데이터베이스(PDB) 파일의 이름을 지정합니다.|  
|`/nowarn:` `warning`|지정한 경고 번호를 표시하지 않습니다. *warning*에는 오류 코드의 숫자 부분(선행 0 없음)만 제공합니다.|  
|`/out:` `file`<br /><br /> `/o:` `file`|출력 Windows 메타데이터(.winmd) 파일의 이름을 지정합니다.|  
|`/pdb:` `symbolfile`<br /><br /> `/p:` `symbolfile`|내보낸 Windows 메타데이터(.winmd) 파일의 기호를 포함하는 출력 프로그램 데이터베이스(PDB) 파일의 이름을 지정합니다.|  
|`/reference:` `winmd`<br /><br /> `/r:` `winmd`|내보내기 중 참조할 메타데이터 파일(.winmd 또는 assembly)을 지정합니다. "\Program Files (x86)\Reference Assemblies\Microsoft\Framework\\.NETCore\v4.5"(32비트 컴퓨터의 경우 "\Program Files\\...")의 참조 어셈블리를 사용하는 경우 System.Runtime.dll 및 mscorlib.dll 모두에 대한 참조를 포함합니다.|  
|`/utf8output`|출력 메시지가 UTF-8 인코딩이 되도록 지정합니다.|  
|`/warnaserror+`|모든 경고를 오류로 처리하도록 지정합니다.|  
|**@** `responsefile`|옵션이 포함된 지시(.rsp) 파일이나 `winmdmodule`을 지정합니다. `responsefile`의 각 줄은 하나의 인수 또는 옵션을 포함해야 합니다.|  
  
## <a name="remarks"></a>설명  
 Winmdexp.exe는 임의의 .NET Framework 어셈블리를 .winmd 파일로 변환할 수 없습니다. `/target:winmdobj` 옵션으로 컴파일된 모듈이 필요하고 추가 제한 사항이 적용됩니다. 이러한 제한 사항 중 가장 중요한 사항은 어셈블리의 API 표면에 공개되는 모든 형식이 Windows 런타임 형식이어야 한다는 것입니다. 자세한 내용은 Windows 개발자 센터에 있는 [C# 및 Visual Basic으로 Windows 런타임 구성 요소 만들기](https://go.microsoft.com/fwlink/p/?LinkID=238313) 문서의 "Windows 런타임 구성 요소에서 형식 선언" 섹션을 참조하세요.  
  
 C# 또는 Visual Basic으로 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 앱 또는 Windows 런타임 구성 요소를 작성하는 경우, .NET Framework는 Windows 런타임을 사용하여 더 자연스럽게 프로그래밍할 수 있도록 지원합니다. 이 내용은 [Windows 스토어 앱 및 Windows 런타임에 대한 .NET Framework 지원](../../standard/cross-platform/support-for-windows-store-apps-and-windows-runtime.md) 문서에서 설명합니다. 이 프로세스에서, 자주 사용되는 몇 가지 Windows 런타임 형식이 .NET Framework 형식에 매핑됩니다. Winmdexp.exe는 이 프로세스를 반대로 하여, 해당 Windows 런타임 형식을 사용하는 API 표면을 생성합니다. 예를 들어 <xref:System.Collections.Generic.IList%601> 인터페이스에서 생성된 형식이 Windows 런타임[IVector\<T>](https://go.microsoft.com/fwlink/p/?LinkId=251132) 인터페이스에서 생성된 형식에 매핑됩니다.  
  
## <a name="see-also"></a>참고 항목

- [Windows 스토어 앱 및 Windows 런타임에 대한 .NET Framework 지원](../../standard/cross-platform/support-for-windows-store-apps-and-windows-runtime.md)
- [C# 및 Visual Basic으로 Windows 런타임 구성 요소 만들기](https://go.microsoft.com/fwlink/p/?LinkID=238313)
- [Winmdexp.exe 오류 메시지](winmdexp-exe-error-messages.md)
- [빌드, 배포 및 구성 도구(.NET Framework)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dd233108(v=vs.100))
