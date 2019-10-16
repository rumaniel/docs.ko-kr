---
title: Peverify.exe(PEVerify 도구)
ms.date: 03/30/2017
helpviewer_keywords:
- portable executable files, PEVerify
- verifying MSIL and metadata
- PEVerify tool
- type safety requirements
- MSIL
- PEverify.exe
- PE files, PEVerify
ms.assetid: f4f46f9e-8d08-4e66-a94b-0c69c9b0bbfa
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 4f0828409a8c57baecf7c81fd7a4df6e7844c7ce
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71044329"
---
# <a name="peverifyexe-peverify-tool"></a>Peverify.exe(PEVerify 도구)
PEVerify 도구를 사용하면 MSIL(Microsoft Intermediate Language)을 생성하는 개발자(컴파일러 작성자, 스크립트 엔진 개발자 등)는 MSIL 코드 및 관련 메타데이터가 형식 안전성 요구 사항을 충족시키는지 여부를 쉽게 확인할 수 있습니다. 일부 컴파일러에서는 특정 언어 구문을 사용하지 않는 경우에만 확인 가능한 형식 안전 코드가 생성됩니다. 이러한 컴파일러를 사용하는 개발자라면 해당 코드의 형식이 안전한지를 확인하려고 할 것입니다. 이런 경우, 해당 파일에 대해 PEVerify 도구를 실행하면 MSIL 및 메타데이터를 검사할 수 있습니다.  
  
 이 도구는 자동으로 Visual Studio와 함께 설치됩니다. 이 도구를 실행하려면 Visual Studio용 개발자 명령 프롬프트(또는 Windows 7의 Visual Studio 명령 프롬프트)를 사용합니다. 자세한 내용은 [명령 프롬프트](developer-command-prompt-for-vs.md)를 참조하세요.  
  
 명령 프롬프트에 다음을 입력합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
peverify filename [options]  
```  
  
## <a name="parameters"></a>매개 변수  
  
|인수|설명|  
|--------------|-----------------|  
|*filename*|MSIL 및 메타데이터를 검사할 대상 PE(이식 가능한 실행) 파일을 나타냅니다.|  
  
|옵션|설명|  
|------------|-----------------|  
|**/break=** *maxErrorCount*|*maxErrorCount* 오류가 발생하면 확인을 중단합니다.<br /><br /> 이 매개 변수는 .NET Framework 버전 2.0 이상에서 지원되지 않습니다.|  
|**/clock**|다음 확인 시간을 밀리초 단위로 측정하여 보고합니다.<br /><br /> **MD Val. cycle**<br /> 메타데이터 유효성 검사 순환<br /><br /> **MD Val. pure**<br /> 메타데이터 유효성 검사 순수<br /><br /> **IL Ver. cycle**<br /> MSIL(Microsoft Intermediate Language) 확인 순환<br /><br /> **IL Ver pure**<br /> MSIL 확인 순수<br /><br /> **MD Val. cycle** 및 **IL Ver. cycle** 시간에는 필수 시작 및 종료 프로시저를 수행하는 데 필요한 시간이 포함됩니다. **MD Val. pure** 및 **IL Ver pure** 시간에는 유효성 검사 또는 확인만 수행하는 데 필요한 시간이 반영됩니다.|  
|**/help**|이 도구의 명령 구문 및 옵션을 표시합니다.|  
|**/hresult**|16진수 형식의 오류 코드를 표시합니다.|  
|**/ignore=** *hex.code* [, *hex.code*]|지정된 오류 코드를 무시합니다.|  
|**/ignore=@** *responseFile*|지정된 지시 파일에 나열된 오류 코드를 무시합니다.|  
|**/il**|*filename*으로 지정된 어셈블리에 구현된 메서드에 대해 MSIL 형식 안전성 확인 검사를 수행합니다. **/quiet** 옵션을 지정하지 않으면 발견된 각 문제점에 대해 자세한 설명이 반환됩니다.|  
|**/md**|*filename*으로 지정된 어셈블리에 대해 메타데이터 유효성 검사를 수행합니다. 이 작업은 파일 내의 전체 메타데이터 구조에 대해 수행되며, 발생한 모든 유효성 검사 문제를 보고합니다.|  
|**/nologo**|제품 버전과 저작권 정보를 표시하지 않습니다.|  
|**/nosymbols**|.NET Framework 버전 2.0에서 이전 버전과의 호환성에 대한 줄 번호를 표시하지 않습니다.|  
|**/quiet**|자동 모드를 지정합니다. 즉, 확인 문제 보고서를 출력하지 않습니다. Peverify.exe를 통해 파일의 형식 안전성 여부는 보고되지만, 형식 안전성 확인을 방해하는 문제점에 대한 정보는 보고되지 않습니다.|  
|`/transparent`|투명 메서드만 확인합니다.|  
|**/unique**|반복되는 오류 코드를 무시합니다.|  
|**/verbose**|.NET Framework 버전 2.0에서 MSIL 확인 메시지에 추가 정보를 표시합니다.|  
|**/?**|이 도구의 명령 구문 및 옵션을 표시합니다.|  
  
## <a name="remarks"></a>설명  
 공용 언어 런타임에서는 애플리케이션 코드의 형식 안전 실행을 통해 보안 및 격리 메커니즘을 적용합니다. 일반적으로 [확인할 수 있도록 형식이 안전](../../standard/security/key-security-concepts.md#type-safety-and-security)  
  
 **/md** 및 **/il** 옵션이 모두 지정되지 않은 경우 Peverify.exe를 사용하면 두 종류의 검사를 모두 수행할 수 있습니다. 먼저 **/md** 검사가 수행되고, 오류가 없으면 **/il** 검사가 수행됩니다. **/md** 및 **/il**을 모두 지정하면 메타데이터에 오류가 있는 경우에도 **/il** 검사가 수행됩니다. 따라서 메타데이터 오류가 없는 경우 **peverify** *filename*은 **peverify** *filename* **/md** **/il**과 같습니다.  
  
 Peverify.exe를 사용하여 데이터 흐름 분석과 올바른 메타데이터에 대한 수백 개의 규칙 목록에 따라 포괄적인 MSIL 확인 검사를 수행할 수 있습니다. Peverify.exe를 사용하여 수행하는 검사에 대한 자세한 내용은 Windows SDK의 Tools Developers Guide 폴더에 있는 "메타데이터 유효성 검사 사양" 및 "MSIL 명령 집합 사양"을 참조하세요.  
  
 .NET Framework 버전 2.0 이상은 `byref`, `dup`, `ldsflda`, `ldflda`, `ldelema`, `call` 등의 MSIL 지침을 사용하여 지정된 확인할 수 있는 `unbox` 반환을 지원합니다.  
  
## <a name="examples"></a>예  
 다음 명령을 사용하여 어셈블리 `myAssembly.exe`에 구현된 메서드에 대해 메타데이터 유효성 검사 및 MSIL 형식 안전성 확인 검사를 수행합니다.  
  
```console  
peverify myAssembly.exe /md /il  
```  
  
 위의 요청이 성공적으로 완료되면 Peverify.exe를 사용하여 다음과 같은 메시지를 표시할 수 있습니다.  
  
```output
All classes and methods in myAssembly.exe Verified  
```  
  
 다음 명령을 사용하여 어셈블리 `myAssembly.exe`에 구현된 메서드에 대해 메타데이터 유효성 검사 및 MSIL 형식 안전성 확인 검사를 수행합니다. 도구에서는 이러한 확인을 수행하는 데 필요한 시간을 표시합니다.  
  
```console  
peverify myAssembly.exe /md /il /clock  
```  
  
 위의 요청이 성공적으로 완료되면 Peverify.exe를 사용하여 다음과 같은 메시지를 표시할 수 있습니다.  
  
```output
All classes and methods in myAssembly.exe Verified  
Timing: Total run     320 msec  
        MD Val.cycle  40 msec  
        MD Val.pure   10 msec  
        IL Ver.cycle  270 msec  
        IL Ver.pure   230 msec  
```  
  
 다음 명령을 사용하여 어셈블리 `myAssembly.exe`에 구현된 메서드에 대해 메타데이터 유효성 검사 및 MSIL 형식 안전성 확인 검사를 수행합니다. 그러나 최대 100의 오류 수에 도달하면 Peverify.exe를 중지합니다. 도구는 지정된 오류 코드를 무시합니다.  
  
```console  
peverify myAssembly.exe /break=100 /ignore=0x12345678,0xABCD1234  
```  
  
 다음 명령을 사용하여 앞의 예제와 동일한 결과를 생성하지만, 지시 파일 `ignoreErrors.rsp`에서 무시할 오류 코드를 지정합니다.  
  
```console  
peverify myAssembly.exe /break=100 /ignore@ignoreErrors.rsp  
```  
  
 지시 파일에 다음과 같이 쉼표로 구분된 오류 코드 목록이 있을 수 있습니다.  
  
```text
0x12345678, 0xABCD1234  
```  
  
 또한, 다음과 같이 한 줄에 하나의 오류 코드가 오도록 지시 파일의 서식을 설정할 수도 있습니다.  
  
```text
0x12345678  
0xABCD1234  
```  
  
## <a name="see-also"></a>참고 항목

- [도구](index.md)
- [형식 안정성이 확인된 코드 작성](../misc/code-access-security-basics.md#typesafe_code)
- [형식 안전성 및 보안](../../standard/security/key-security-concepts.md#type-safety-and-security)
- [명령 프롬프트](developer-command-prompt-for-vs.md)
