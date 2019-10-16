---
title: SecAnnotate.exe(.NET Security Annotator 도구)
ms.date: 03/30/2017
helpviewer_keywords:
- SecAnnotate.exe
- Security Annotator tool
ms.assetid: 8104d208-7813-4a1d-8a75-58f9a7bcb8c9
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 146aef8c1e085ee3146585c3b5b1cda8004b9f7e
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71044207"
---
# <a name="secannotateexe-net-security-annotator-tool"></a>SecAnnotate.exe(.NET Security Annotator 도구)
.NET Security Annotator 도구(SecAnnotate.exe)는 하나 이상의 어셈블리의 `SecurityCritical` 및 `SecuritySafeCritical` 부분을 식별하는 명령줄 애플리케이션입니다.  
  
 Visual Studio 확장인 [Security Annotator](https://go.microsoft.com/fwlink/?LinkId=198007)는 SecAnnotate.exe에 대한 그래픽 사용자 인터페이스를 제공하며 Visual Studio에서 도구를 실행할 수 있습니다.  
  
 이 도구는 자동으로 Visual Studio와 함께 설치됩니다. 이 도구를 실행하려면 Visual Studio용 개발자 명령 프롬프트(또는 Windows 7의 Visual Studio 명령 프롬프트)를 사용합니다. 자세한 내용은 [명령 프롬프트](developer-command-prompt-for-vs.md)를 참조하세요.  
  
 명령 프롬프트에서 다음을 입력하세요. *parameters*는 다음 섹션에서 설명하며 *assemblies*는 공백으로 구분된 하나 이상의 어셈블리 이름으로 구성됩니다.  
  
## <a name="syntax"></a>구문  
  
```console  
SecAnnotate.exe [parameters] [assemblies]  
```  
  
## <a name="parameters"></a>매개 변수  
  
|옵션|설명|  
|------------|-----------------|  
|`/a`<br /><br /> 또는<br /><br /> `/showstatistics`|분석 중인 어셈블리에서 투명도 사용에 대한 통계를 보여 줍니다.|  
|`/d:` *directory*<br /><br /> 또는<br /><br /> `/referencedir:` *directory*|주석 도중 종속 어셈블리를 검색할 디렉터리를 지정합니다.|  
|`/i`<br /><br /> 또는<br /><br /> `/includesignatures`|주석 보고서 파일에 확장된 시그니처 정보를 포함합니다.|  
|`/n`<br /><br /> 또는<br /><br /> `/nogac`|전역 어셈블리 캐시에서 참조된 어셈블리를 검색하지 않습니다.|  
|`/o:` *output.xml*<br /><br /> 또는<br /><br /> `/out:` *output.xml*|출력 주석 파일을 지정합니다.|  
|`/p:` *maxpasses*<br /><br /> 또는<br /><br /> `/maximumpasses:` *maxpasses*|새 주석의 생성을 중지하기 전에 어셈블리에 대해 수행할 주석 패스의 최대 횟수를 지정합니다.|  
|`/q`<br /><br /> 또는<br /><br /> `/quiet`|주석 처리기가 상태 메시지를 출력하지 않는 자동 모드를 지정합니다. 오류 정보만 출력합니다.|  
|`/r:` *assembly*<br /><br /> 또는<br /><br /> `/referenceassembly:` *assembly*|주석을 추가하는 동안 종속 어셈블리를 확인할 때 지정한 어셈블리를 포함합니다. 참조 어셈블리는 참조 경로에서 발견된 어셈블리를 통해 우선 순위가 지정됩니다.|  
|`/s:` *rulename*<br /><br /> 또는<br /><br /> `/suppressrule:` *rulename*|입력 어셈블리에 지정된 투명도 규칙의 실행을 표시하지 않습니다.|  
|`/t`<br /><br /> 또는<br /><br /> `/forcetransparent`|Annotator 도구를 사용하면 투명 주석이 없는 모든 어셈블리를 완전히 투명한 것처럼 처리할 수 있습니다.|  
|`/t`:*assembly*<br /><br /> 또는<br /><br /> `/forcetransparent`:*assembly*|현재 어셈블리 수준 주석에 관계없이 지정된 어셈블리를 강제로 투명하게 설정합니다.|  
|||  
|`/v`<br /><br /> 또는<br /><br /> `/verify`|어셈블리의 주석이 올바른지만 확인하고, 어셈블리가 확인되지 않은 경우 여러 번의 패스를 수행하여 필요한 모든 주석을 찾는 작업은 하지 않습니다.|  
|`/x`<br /><br /> 또는<br /><br /> `/verbose`|주석을 추가하는 동안 자세한 출력을 지정합니다.|  
|`/y:` *directory*<br /><br /> 또는<br /><br /> `/symbolpath:` *directory*|주석을 추가하는 동안 기호 파일을 검색할 때 지정한 디렉터리를 포함합니다.|  
  
## <a name="remarks"></a>설명  
 매개 변수 및 어셈블리는 명령줄에 지정되고 (@) 기호에 접두사가 있는 응답 파일에 제공될 수도 있습니다. 응답 파일의 각 줄은 단일 매개 변수 또는 어셈블리 이름을 포함해야 합니다.  
  
 .NET Security Annotator에 대한 자세한 내용은 .NET Security 블로그의 [SecAnnotate를 사용하여 어셈블리의 투명도 위반 분석](https://go.microsoft.com/fwlink/?LinkId=187648) 항목을 참조하세요.  
  
## <a name="examples"></a>예
