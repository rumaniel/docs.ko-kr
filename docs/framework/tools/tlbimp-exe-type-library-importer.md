---
title: Tlbimp.exe(형식 라이브러리 가져오기)
ms.date: 03/30/2017
helpviewer_keywords:
- type libraries [.NET Framework], importing
- importing type library
- Tlbimp.exe
- type definition conversion
- Type Library Importer
- type libraries
- converting type definitions
ms.assetid: ec0a8d63-11b3-4acd-b398-da1e37e97382
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 048c2cd3d6b90dda951128a29a212928ee67c5a5
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70971751"
---
# <a name="tlbimpexe-type-library-importer"></a>Tlbimp.exe(형식 라이브러리 가져오기)
형식 라이브러리 가져오기 도구는 COM 형식 라이브러리에 있는 형식 정의를 공용 언어 런타임 어셈블리의 동등한 정의로 변환합니다. Tlbimp.exe의 출력은 원본 형식 라이브러리에 정의된 형식의 런타임 메타데이터를 포함하는 이진 파일(어셈블리)입니다. [Ildasm.exe](ildasm-exe-il-disassembler.md)와 같은 도구를 사용하여 이 파일을 검토할 수 있습니다.  
  
 이 도구는 자동으로 Visual Studio와 함께 설치됩니다. 이 도구를 실행하려면 Visual Studio용 개발자 명령 프롬프트(또는 Windows 7의 Visual Studio 명령 프롬프트)를 사용합니다. 자세한 내용은 [명령 프롬프트](developer-command-prompt-for-vs.md)를 참조하세요.  
  
 명령 프롬프트에 다음을 입력합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
tlbimp tlbFile [options]  
```  
  
## <a name="parameters"></a>매개 변수  
  
|인수|설명|  
|--------------|-----------------|  
|*tlbFile*|COM 형식 라이브러리를 포함하는 파일의 이름입니다.|  
  
|옵션|설명|  
|------------|-----------------|  
|**/asmversion:** *versionnumber*|만들 어셈블리의 버전 번호를 지정합니다. *versionnumber*를 *major.minor.build.revision* 형식으로 지정합니다.|  
|**/company:** `companyinformation`|출력 어셈블리에 회사 정보를 추가합니다.|  
|**/copyright:** `copyrightinformation`|출력 어셈블리에 저작권 정보를 추가합니다. 이 정보는 어셈블리에 대한 **파일 속성** 대화 상자에서 볼 수 있습니다.|  
|**T:System.Reflection.AssemblyDelaySignAttribute**|Tlbimp.exe에서 지연 서명을 사용하여 강력한 이름의 결과 어셈블리에 서명하도록 지정합니다. 이 옵션은 **/keycontainer:** , **/keyfile:** 또는 **/publickey:** 옵션과 함께 지정해야 합니다. 지연 서명 프로세스에 대한 자세한 내용은 [어셈블리 서명 연기](../../standard/assembly/delay-sign.md)를 참조하세요.|  
|**/help**|이 도구의 명령 구문 및 옵션을 표시합니다.|  
|**/keycontainer:** *containername*|*containername*에서 지정된 키 컨테이너에 있는 퍼블릭/프라이빗 키 쌍을 사용하여 강력한 이름으로 결과 어셈블리를 서명합니다.|  
|**/keyfile:** *filename*|*filename*에 있는 게시자의 공식 퍼블릭/프라이빗 키 쌍을 사용하여 강력한 이름으로 결과 어셈블리를 서명합니다.|  
|**/machine:** `machinetype`|지정된 컴퓨터 종류(마이크로프로세서)를 대상으로 하는 어셈블리를 만듭니다. 지원되는 컴퓨터 종류: x86, x64, Itanium 및 Agnostic.|  
|**/namespace:** *namespace*|어셈블리를 만들 네임스페이스를 지정합니다.|  
|**/noclassmembers**|Tlbimp.exe에서 클래스에 멤버를 추가하지 못하도록 합니다. 이렇게 하면 <xref:System.TypeLoadException>이 발생하지 않습니다.|  
|**/nologo**|Microsoft 시작 배너를 표시하지 않습니다.|  
|**/out:** *filename*|메타데이터 정의를 기록할 출력 파일의 이름, 어셈블리 및 네임스페이스를 지정합니다. 형식 라이브러리에서 어셈블리의 네임스페이스를 명시적으로 제어하는 IDL(Interface Definition Language) 사용자 지정 특성을 지정하면 **/out** 옵션은 어셈블리의 네임스페이스에 영향을 주지 않습니다. 이 옵션을 지정하지 않으면 Tlbimp.exe는 입력 파일 내에 정의한 실제 형식 라이브러리와 이름이 같은 파일에 메타데이터를 기록하고 이 파일의 확장명을 .dll로 지정합니다. 출력 파일과 입력 파일의 이름이 같은 경우 형식 라이브러리를 덮어쓰지 않도록 오류가 생성됩니다.|  
|**/primary**|지정된 형식 라이브러리에 대한 주 interop 어셈블리를 만듭니다. 어셈블리를 만든 형식 라이브러리의 게시자를 나타내는 정보가 어셈블리에 추가됩니다. 주 interop 어셈블리를 지정하면 게시자의 어셈블리를 Tlbimp.exe를 사용하여 형식 라이브러리에서 만든 다른 어셈블리와 구별할 수 있습니다. Tlbimp.exe를 사용하여 가져오는 형식 라이브러리의 게시자인 경우 **/primary** 옵션만 사용해야 합니다. [강력한 이름](../../standard/assembly/strong-named.md)을 사용하여 주 interop 어셈블리를 서명해야 합니다. 자세한 내용은 [주 Interop 어셈블리](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/aax7sdch(v=vs.100))를 참조하세요.|  
|**/product:** `productinformation`|출력 어셈블리에 제품 정보를 추가합니다. 이 정보는 어셈블리에 대한 **파일 속성** 대화 상자에서 볼 수 있습니다.|  
|**/productversion:** `productversioninformation`|출력 어셈블리에 제품 버전 정보를 추가합니다. 형식 제한은 없습니다. 이 정보는 어셈블리에 대한 **파일 속성** 대화 상자에서 볼 수 있습니다.|  
|**/publickey:** *filename*|결과 어셈블리에 서명하는 데 사용할 공개 키를 포함하는 파일을 지정합니다. **/publickey:** 대신 **/keyfile:** 또는 **/keycontainer:** 옵션을 지정하면 Tlbimp.exe는 **/keyfile:** 또는 **/keycontainer:** 와 함께 제공된 퍼블릭/프라이빗 키 쌍에서 퍼블릭 키를 생성합니다. **/publickey:** 옵션은 테스트 키 및 서명 연기 시나리오를 지원합니다. 파일은 Sn.exe에 의해 생성된 형식으로 되어 있습니다. 자세한 내용은 [Sn.exe(강력한 이름 도구)](sn-exe-strong-name-tool.md)에서 Sn.exe의 **-p** 옵션을 참조하세요.|  
|**/reference:** *filename*|현재 형식 라이브러리 외부에 정의된 형식에 대한 참조를 확인하는 데 사용할 어셈블리 파일을 지정합니다. **/reference** 옵션을 지정하지 않으면 Tlbimp.exe는 가져오는 형식 라이브러리에서 참조하는 외부 형식 라이브러리를 재귀적으로 가져옵니다. 이 작업은 자동으로 수행됩니다. **/reference** 옵션을 지정하면 Tlbimp.exe는 다른 형식 라이브러리를 가져오기 전에 참조된 어셈블리에서 외부 형식을 확인하려고 합니다.|  
|**/silence:** `warningnumber`|지정한 경고를 표시하지 않습니다. 이 옵션은 **/silent**와 함께 사용할 수 없습니다.|  
|**/silent**|성공 메시지를 표시하지 않습니다. 이 옵션은 **/silence**와 함께 사용할 수 없습니다.|  
|**/strictref**|도구에서 현재 어셈블리, **/reference** 옵션으로 지정된 어셈블리 또는 등록된 PIA(주 Interop 어셈블리) 내의 모든 참조를 확인할 수 없는 경우 형식 라이브러리를 가져오지 않습니다.|  
|**/strictref:nopia**|**/strictref**와 같지만 PIA를 무시합니다.|  
|**/sysarray**|COM 스타일 SafeArray를 관리되는 <xref:System.Array> 형식으로 가져오는 도구를 지정합니다.|  
|**/tlbreference:** *filename*|레지스트리를 조회하지 않고 형식 라이브러리 참조를 확인하는 데 사용할 형식 라이브러리 파일을 지정합니다.<br /><br /> 이 옵션을 사용하면 이전의 형식 라이브러리 형식 중 일부가 로드되지 않습니다.  그러나 레지스트리나 현재 디렉터리를 통해 암시적으로 이전의 형식 라이브러리 형식을 로드할 수 있습니다.|  
|**/trademark:** `trademarkinformation`|출력 어셈블리에 상표 정보를 추가합니다. 이 정보는 어셈블리에 대한 **파일 속성** 대화 상자에서 볼 수 있습니다.|  
|**/transform:** *transformname*|*transformname* 매개 변수에 지정된 메타데이터를 변형합니다.<br /><br /> *transformname* 매개 변수에 **dispret**를 지정하여 디스패치 전용 인터페이스(dispinterface)에 있는 메서드의 [out, retval] 매개 변수를 반환 값으로 변형합니다.<br /><br /> 이 옵션에 대한 자세한 내용은 이 항목 뒷부분의 예제를 참조하십시오.|  
|**/unsafe**|.NET Framework 보안 검사를 실행하지 않고 인터페이스를 만듭니다. 이런 식으로 노출된 메서드를 호출하면 보안상 위험할 수 있습니다. 이러한 코드 노출의 위험에 대해 잘 모르면 이 옵션을 사용하지 않는 것이 좋습니다.|  
|**/verbose**|세부 정보 표시 모드를 지정합니다. 즉, 가져온 형식 라이브러리에 대한 추가 정보를 표시합니다.|  
|**/VariantBoolFieldToBool**|구조 내 `VARIANT_BOOL` 필드를 <xref:System.Boolean>으로 변환합니다.|  
|**/?**|이 도구의 명령 구문 및 옵션을 표시합니다.|  
  
> [!NOTE]
> Tlbimp.exe의 명령줄 옵션은 대/소문자를 구분하지 않으며 순서에 관계없이 지정할 수 있습니다. 또한, 고유하게 식별할 수 있을 정도로만 옵션을 지정하면 됩니다. 따라서 **/n**은 **/nologo**와 같고, **/ou:** *outfile.dll*은 **/out:** *outfile.dll*과 같습니다.  
  
## <a name="remarks"></a>설명  
 Tlbimp.exe는 한 번에 전체 형식 라이브러리 변환을 수행합니다. 이 도구를 사용하여 단일 형식 라이브러리 내에 정의된 형식의 하위 집합에 대한 형식 정보를 생성할 수는 없습니다.  
  
 어셈블리에 [강력한 이름](../../standard/assembly/strong-named.md)을 할당하는 것이 종종 유용하거나 필요합니다. 따라서 Tlbimp.exe는 강력한 이름의 어셈블리를 생성하는 데 필요한 정보를 제공하는 옵션을 포함합니다. **/keyfile:** 및 **/keycontainer:** 옵션은 둘 다 강력한 이름으로 어셈블리를 서명합니다. 그러므로 한 번에 한 옵션만 지정하면 됩니다.  
  
 **/reference** 옵션을 여러 번 사용하여 여러 개의 참조 어셈블리를 지정할 수 있습니다.
 
 Tlbimp.exe가 어셈블리를 생성하는 방식으로 인해 어셈블리를 다른 `mscorlib` 버전으로 다시 대상 지정할 수 없습니다. 예를 들어 .NET Framework 2.0을 대상으로 하는 어셈블리를 생성하려는 경우 .NET Framework 2.0/3.0/3.5 SDK와 함께 제공되는 Tlbimp.exe를 사용해야 합니다. .NET Framework 4.x를 대상으로 하려면 .NET Framework 4.x SDK와 함께 제공되는 Tlbimp.exe를 사용해야 합니다.
 
 여러 개의 형식 라이브러리를 포함하는 모듈에서 형식 라이브러리를 가져오는 경우 선택적으로 리소스 ID를 형식 라이브러리 파일에 추가할 수 있습니다. 이 파일이 현재 디렉터리에 있거나 전체 경로를 지정하는 경우에만 Tlbimp.exe를 사용하여 파일을 찾을 수 있습니다. 이 항목의 뒷부분에 있는 예제를 참조하십시오.  
  
## <a name="examples"></a>예제  
 다음 명령을 사용하여 `myTest.tlb`에 있는 형식 라이브러리와 이름이 같고 확장명이 .dll인 어셈블리를 생성합니다.  
  
```console  
tlbimp myTest.tlb   
```  
  
 다음 명령을 사용하여 `myTest.dll`이라는 이름의 어셈블리를 생성합니다.  
  
```console  
tlbimp  myTest.tlb  /out:myTest.dll  
```  
  
 다음 명령은 `MyModule.dll\1`에 지정된 형식 라이브러리와 동일한 이름과 .dll 확장명을 사용하는 어셈블리를 생성합니다. `MyModule.dll\1`은 현재 디렉터리에 있어야 합니다.  
  
```console  
tlbimp MyModule.dll\1  
```  
  
 다음 명령을 사용하여 형식 라이브러리 `myTestLib.dll`에 대해 이름이 `TestLib.dll`인 어셈블리를 생성합니다. **/transform:dispret** 옵션은 형식 라이브러리의 dispinterface에 있는 메서드의 모든 [out, retval] 매개 변수를 관리되는 라이브러리의 반환 값으로 변형합니다.  
  
```console  
tlbimp TestLib.dll /transform:dispret /out:myTestLib.dll  
```  
  
 앞의 예제에서 형식 라이브러리 `TestLib.dll`은 void를 반환하고 [out, retval] 매개 변수를 갖는 `SomeMethod`라는 disinterface 메서드를 포함합니다. 다음 코드는 `SomeMethod`에 있는 `TestLib.dll`에 대한 입력 형식 라이브러리 메서드 시그니처입니다.  
  
```cpp  
void SomeMethod([out, retval] VARIANT_BOOL*);  
```  
  
 **/transform:dispret** 옵션을 지정하면 Tlbimp.exe는 `SomeMethod`의 `[out, retval]` 매개 변수를 `bool` 반환 값으로 변형합니다. 다음은 **/transform:dispret** 옵션이 지정될 때 Tlbimp.exe에서 `myTestLib.dll` 관리되는 라이브러리의 `SomeMethod`에 대해 생성하는 메서드 시그니처입니다.  
  
```csharp  
bool SomeMethod();  
```  
  
 Tlbimp.exe를 사용하여 **/transform:dispret**를 지정하지 않고 `TestLib.dll`에 대해 관리되는 라이브러리를 생성하면 도구에서 `myTestLib.dll` 관리되는 라이브러리의 `SomeMethod`에 대해 다음 메서드 시그니처를 생성합니다.  
  
```csharp  
void SomeMethod(out bool x);  
```  
  
## <a name="see-also"></a>참고 항목

- [도구](index.md)
- [Tlbexp.exe(형식 라이브러리 내보내기)](tlbexp-exe-type-library-exporter.md)
- [형식 라이브러리를 어셈블리로 가져오기](../interop/importing-a-type-library-as-an-assembly.md)
- [형식 라이브러리를 어셈블리로 변환 요약](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/k83zzh38(v=vs.100))
- [Ildasm.exe(IL 디스어셈블러)](ildasm-exe-il-disassembler.md)
- [Sn.exe(강력한 이름 도구)](sn-exe-strong-name-tool.md)
- [강력한 이름의 어셈블리](../../standard/assembly/strong-named.md)
- [Interop 어셈블리로 형식 라이브러리를 가져오는 특성](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/y6a7ak23(v=vs.100))
- [명령 프롬프트](developer-command-prompt-for-vs.md)
