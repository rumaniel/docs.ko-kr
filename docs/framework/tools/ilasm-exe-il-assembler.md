---
title: Ilasm.exe(IL 어셈블러)
ms.date: 03/30/2017
helpviewer_keywords:
- MSIL generators
- metadata, MSIL Assembler
- MSIL Assembler
- portable executable files, MSIL Assembler
- PE files, MSIL Assembler
- MSIL
- Ilasm.exe
- verifying MSIL performance
ms.assetid: 4ca3a4f0-4400-47ce-8936-8e219961c76f
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b8d1ad081c8d783cd18054078a6eeb82428faa4d
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71044628"
---
# <a name="ilasmexe-il-assembler"></a>Ilasm.exe(IL 어셈블러)

IL 어셈블러는 IL(Intermediate Language)로 PE(이식 가능한 실행) 파일을 생성합니다. IL에 대한 자세한 내용은 [관리되는 실행 프로세스](../../standard/managed-execution-process.md)를 참조하세요. 이렇게 생성된 실행 파일에는 IL 및 필요한 메타데이터가 들어 있으며, 이 파일을 실행하면 IL이 예상대로 실행되는지 여부를 확인할 수 있습니다.

이 도구는 자동으로 Visual Studio와 함께 설치됩니다. 이 도구를 실행하려면 Visual Studio용 개발자 명령 프롬프트(또는 Windows 7의 Visual Studio 명령 프롬프트)를 사용합니다. 자세한 내용은 [명령 프롬프트](developer-command-prompt-for-vs.md)를 참조하세요.

명령 프롬프트에 다음을 입력합니다.

## <a name="syntax"></a>구문

```console
ilasm [options] filename [[options]filename...]
```

## <a name="parameters"></a>매개 변수

| 인수 | 설명 |
| -------- | ----------- |
|`filename`|.il 소스 파일의 이름을 나타냅니다. 이 파일은 메타데이터 선언 지시문과 기호화된 IL 명령으로 구성됩니다. *Ilasm.exe*를 사용하여 여러 개의 소스 파일 인수를 제공하면 하나의 PE 파일을 생성할 수 있습니다. **참고:** .il 소스 파일의 마지막 코드 줄에는 후행 공백이나 줄 끝(EOL) 문자가 있어야 합니다.|

| 옵션 | 설명 |
| ------ | ----------- |
|**/32bitpreferred**|32비트 우선의 이미지(PE32)를 만듭니다.|
|**/alignment:** `integer`|FileAlignment를 NT 선택적 헤더의 `integer`에서 지정한 값으로 설정합니다. .alignment IL 지시문이 파일에 지정된 경우 이 옵션을 사용하면 재정의됩니다.|
|**/appcontainer**|Windows 앱 컨테이너에서 출력으로 실행되는 *.dll* 또는 *.exe* 파일을 만듭니다.|
|**/arm**|Advanced RISC Machine(ARM)을 대상 프로세서로 지정합니다.<br /><br /> 이미지 비트가 지정되지 않은 경우 기본값은 **/32bitpreferred**입니다.|
|**/base:** `integer`|ImageBase를 NT 선택적 헤더의 `integer`에서 지정한 값으로 설정합니다. .imagebase IL 지시문이 파일에 지정된 경우 이 옵션을 사용하면 재정의됩니다.|
|**/clock**|지정된 .il 소스 파일에 대해 다음 컴파일 타임을 밀리초 단위로 측정하여 보고합니다.<br /><br /> **Total Run**: 다음의 특정 작업을 모두 수행하는 데 걸린 총 시간.<br /><br /> **Startup**: 파일 로드 및 열기.<br /><br /> **Emitting MD**: 메타데이터 내보내기.<br /><br /> **Ref to Def Resolution**: 파일의 참조를 정의로 확인.<br /><br /> **CEE File Generation**: 메모리에 파일 이미지 생성.<br /><br /> **PE File Writing**: PE 파일에 이미지 작성.|
|**/debug**[:**IMPL**&#124;**OPT**]|지역 변수 및 인수 이름과 줄 번호 등의 디버깅 정보를 포함합니다. PDB 파일을 만듭니다.<br /><br /> **/debug** 에 추가 값을 지정하지 않으면 JIT 최적화를 사용할 수 없고 PDB 파일의 시퀀스 위치를 사용합니다.<br /><br /> **IMPL** 은 JIT 최적화를 사용할 수 없도록 하고 암시적 시퀀스 위치를 사용합니다.<br /><br /> **OPT** 는 JIT 최적화를 사용할 수 있도록 하고 암시적 시퀀스 위치를 사용합니다.|
|**/dll**|*.dll* 파일을 출력 파일로 생성합니다.|
|**/enc:** `file`|지정한 소스 파일에서 편집하며 계속하기 델타를 만듭니다.<br /><br /> 이 인수는 교육용 버전에서만 사용되며, 상업용 버전에서는 지원되지 않습니다.|
|**/exe**|실행 파일을 출력 파일로 생성합니다. 이 값이 기본값입니다.|
|**/flags:** `integer`|ImageFlags를 공용 언어 런타임 헤더의 `integer`에서 지정한 값으로 설정합니다. .corflags IL 지시문이 파일에 지정된 경우 이 옵션을 사용하면 재정의됩니다. *integer*의 올바른 값 목록은 CorHdr.h, COMIMAGE_FLAGS를 참조하십시오.|
|**/fold**|동일한 메서드 본문을 하나로 만듭니다.|
|/**highentropyva**|높은 엔트로피 주소 공간 레이아웃 불규칙화(ASLR)가 지원되는 출력 실행 파일을 생성합니다. ( **/appcontainer**의 기본값)|
|**/include:** `includePath`|`#include`에 포함된 파일을 검색할 경로를 설정합니다.|
|**/itanium**|Intel Itanium을 대상 프로세서로 지정합니다.<br /><br /> 이미지 비트가 지정되지 않은 경우 기본값은 **/pe64**입니다.|
|**/key:** `keyFile`|`keyFile`에 들어 있는 프라이빗 키를 사용하여 강력한 시그니처가 있는 `filename`을 컴파일합니다.|
|**/key:**  @`keySource`|`keySource`에 생성된 프라이빗 키를 사용하여 강력한 시그니처가 있는 `filename`을 컴파일합니다.|
|**/listing**|표준 출력 파일에 대한 목록 파일을 생성합니다. 이 옵션을 생략하면 목록 파일이 생성되지 않습니다.<br /><br /> 이 매개 변수는 .NET Framework 2.0 이상에서 지원되지 않습니다.|
|**/mdv:** `versionString`|메타데이터 버전 문자열을 설정합니다.|
|**/msv:** `major`.`minor`|`major` 및 `minor` 가 정수인 메타데이터 스트림 버전을 설정합니다.|
|**/noautoinherit**|기준 클래스를 지정하지 않으면 <xref:System.Object> 에서 기본 상속을 사용할 수 없습니다.|
|**/nocorstub**|CORExeMain 스텁을 생성하지 않습니다.|
|**/nologo**|Microsoft 시작 배너를 표시하지 않습니다.|
|**/output:** `file.ext`|출력 파일 이름 및 확장명을 지정합니다. 기본적으로 출력 파일 이름은 첫 번째 소스 파일의 이름과 같으며, 기본 확장명은 *.exe*입니다. **/dll** 옵션을 지정하는 경우 기본 확장명은 *.dll*입니다. **참고:** **/output**:myfile.dll을 지정하면 **/dll** 옵션이 설정되지 않습니다. **/dll**을 지정하지 않으면 *myfile.dll*이라는 실행 파일이 생성됩니다.|
|**/optimize**|긴 명령을 짧게 최적화합니다. 예를 들면, `br` 를 `br.s`로 입력합니다.|
|**/pe64**|64비트 이미지(PE32+)를 만듭니다.<br /><br /> 대상 프로세서가 지정되지 않은 경우 기본값은 `/itanium`입니다.|
|**/pdb**|디버그 정보 추적을 사용하지 않고 PDB 파일을 만듭니다.|
|**/quiet**|자동 모드를 지정하여 어셈블리 진행률을 보고하지 않습니다.|
|**/resource:** `file.res`|결과로 만들어지는 *.exe* 또는 *.dll* 파일에 \*.res 형식의 지정된 리소스 파일을 포함합니다. **/resource** 옵션을 사용하여 .res 파일을 하나만 지정할 수 있습니다.|
|**/ssver:** `int`.`int`|NT 선택적 헤더의 하위 시스템 버전 번호를 설정합니다. **/appcontainer** 및 **/arm** 의 최소 버전 번호는 6.02입니다.|
|**/stack:** `stackSize`|NT 선택적 헤더의 SizeOfStackReserve 값을 `stackSize`로 설정합니다.|
|**/stripreloc**|기준 재배치가 필요하지 않도록 지정합니다.|
|**/subsystem:** `integer`|하위 시스템을 NT 선택적 헤더의 `integer`에서 지정한 값으로 설정합니다. .subsystem IL 지시문이 파일에 지정된 경우 이 명령을 사용하면 재정의됩니다. `integer`의 올바른 값 목록은 winnt.h, IMAGE_SUBSYSTEM을 참조하세요.|
|**/x64**|64비트 AMD 프로세서를 대상 프로세서로 지정합니다.<br /><br /> 이미지 비트가 지정되지 않은 경우 기본값은 **/pe64**입니다.|
|**/?**|이 도구의 명령 구문 및 옵션을 표시합니다.|

> [!NOTE]
> *Ilasm.exe*의 모든 옵션은 대/소문자가 구분되지 않으며 처음 세 문자로 인식됩니다. 예를 들어 **/lis**는 **/listing**과 같고, **/res:** myresfile.res는 **/resource:** myresfile.res와 같습니다. 인수를 지정하는 옵션에는 옵션과 인수 사이의 구분 기호로 콜론(:) 또는 등호(=) 중 하나만 사용할 수 있습니다. 예를 들어, **/output**:*file.ext*는 **/output**=*file.ext*와 같습니다.

## <a name="remarks"></a>설명

IL 어셈블러를 사용하면 도구 공급업체는 IL 생성기를 쉽게 디자인하여 구현할 수 있으며, *Ilasm.exe*를 사용하면 도구 및 컴파일러 개발자는 IL을 PE 파일 형식으로 내보내는 것에 신경 쓰지 않고 IL 및 메타데이터 생성에만 몰두할 수 있습니다.

*Ilasm.exe*를 사용하면 C# 및 Visual Basic과 같이 런타임을 대상으로 하는 다른 컴파일러처럼 중간 개체 파일이 생성되지 않으며 PE 파일을 만들 때 링크하는 단계가 필요 없습니다.

IL 어셈블러를 사용하면 런타임을 대상으로 하는 프로그래밍 언어의 IL 기능 및 기존 메타데이터를 모두 표현할 수 있습니다. 이렇게 하면 이러한 프로그래밍 언어로 작성된 관리 코드를 IL 어셈블러에서 적절히 표현하고 *Ilasm.exe*를 사용하여 컴파일할 수 있습니다.

> [!NOTE]
> .il 소스 파일의 마지막 코드 줄에 후행 공백이나 줄 끝(EOL) 문자가 없으면 컴파일이 실패할 수 있습니다.

*Ilasm.exe*는 자매 도구인 [*Ildasm.exe*](ildasm-exe-il-disassembler.md)와 함께 사용할 수 있습니다. *Ildasm.exe*는 IL 코드가 포함된 PE 파일을 가져와서 *Ildasm.exe*에 입력하기에 적합한 텍스트 파일을 만듭니다. 이렇게 하면 런타임 메타데이터 특성을 모두 지원하지 않는 프로그래밍 언어로 코드를 컴파일할 때 유용합니다. 코드를 컴파일하고 *Ildasm.exe*를 사용하여 출력을 실행한 후에는 결과로 만들어지는 IL 텍스트 파일을 수동으로 편집하여 손실된 특성을 추가할 수 있습니다. 그런 다음에는 *Ilasm.exe*를 통해 이 텍스트 파일을 실행하여 최종 실행 파일을 생성할 수 있습니다.

또한, 이 기술을 사용하면 서로 다른 컴파일러에서 생성된 여러 개의 PE 파일에서 하나의 PE 파일을 생성할 수도 있습니다.

> [!NOTE]
> 포함된 네이티브 코드가 들어 있는 PE 파일(예: Visual C++로 생성된 PE 파일)에는 현재 이 방법을 사용할 수 없습니다.

가능한 정확하게 *Ildasm.exe* 및 *Ilasm.exe*를 복합적으로 사용하려면, 디폴트로 어셈블러가 IL 소스에서 기록한 (혹은 다른 컴파일러에 의하여 빠뜨려진) 긴 인코딩에 대한 짧은 인코딩을 대체하지 않아야 합니다. **/optimize** 옵션을 사용하여 가능한 짧은 인코딩으로 대체합니다.

> [!NOTE]
> *Ildasm.exe*는 디스크의 파일에 대해서만 작동하며, 전역 어셈블리 캐시에 설치된 파일에 대해서는 작동하지 않습니다.

IL 문법에 대한 자세한 내용은 Windows SDK에서 asmparse.grammar 파일을 참조하세요.

## <a name="version-information"></a>버전 정보

.NET Framework 4.5부터 다음과 같은 코드를 사용하여 사용자 지정 특성을 인터페이스 구현에 연결할 수 있습니다.

```il
.class interface public abstract auto ansi IMyInterface
{
  .method public hidebysig newslot abstract virtual
    instance int32 method1() cil managed
  {
  } // end of method IMyInterface::method1
} // end of class IMyInterface
.class public auto ansi beforefieldinit MyClass
  extends [mscorlib]System.Object
  implements IMyInterface
  {
    .interfaceimpl type IMyInterface
    .custom instance void
      [mscorlib]System.Diagnostics.DebuggerNonUserCodeAttribute::.ctor() = ( 01 00 00 00 )
      …
```

.NET Framework 4.5부터 다음 코드와 같이 원시 이진 표현을 사용하여 임의의 마샬 BLOB(이진 대형 개체)을 지정할 수 있습니다.

```il
.method public hidebysig abstract virtual
        instance void
        marshal({ 38 01 02 FF })
        Test(object A_1) cil managed
```

IL 문법에 대한 자세한 내용은 Windows SDK에서 asmparse.grammar 파일을 참조하세요.

## <a name="examples"></a>예

다음 명령은 IL 파일 *myTestFile.il*을 어셈블하고 실행 파일 *myTestFile.exe*를 생성합니다.

```console
ilasm myTestFile
```

다음 명령은 IL 파일 *myTestFile.il*을 어셈블하고 *.dll* 파일 *myTestFile.dll*을 생성합니다.

```console
ilasm myTestFile /dll
```

다음 명령은 IL 파일 *myTestFile.il*을 어셈블하고 *.dll* 파일 *myNewTestFile.dll*을 생성합니다.

```console
ilasm myTestFile /dll /output:myNewTestFile.dll
```

다음 코드 예제에서는 "Hello World!"를 콘솔에 표시하는 매우 간단한 애플리케이션을 표시합니다. 이 코드를 컴파일한 다음 [*Ildasm.exe*](ildasm-exe-il-disassembler.md) 도구를 사용하여 IL 파일을 생성할 수 있습니다.

```csharp
using System;

public class Hello
{
    public static void Main(String[] args)
    {
        Console.WriteLine("Hello World!");
    }
}
```

다음 IL 코드 예제는 이전 C# 코드 예제에 해당합니다. IL 어셈블러 도구를 사용하여 이 코드를 어셈블리로 컴파일할 수 있습니다. IL과 C# 코드 예제 모두 콘솔에 "Hello World!"를 표시합니다.

```il
// Metadata version: v2.0.50215
.assembly extern mscorlib
{
  .publickeytoken = (B7 7A 5C 56 19 34 E0 89 )                         // .z\V.4..
  .ver 2:0:0:0
}
.assembly sample
{
  .custom instance void [mscorlib]System.Runtime.CompilerServices.CompilationRelaxationsAttribute::.ctor(int32) = ( 01 00 08 00 00 00 00 00 )
  .hash algorithm 0x00008004
  .ver 0:0:0:0
}
.module sample.exe
// MVID: {A224F460-A049-4A03-9E71-80A36DBBBCD3}
.imagebase 0x00400000
.file alignment 0x00000200
.stackreserve 0x00100000
.subsystem 0x0003       // WINDOWS_CUI
.corflags 0x00000001    //  ILONLY
// Image base: 0x02F20000

// =============== CLASS MEMBERS DECLARATION ===================

.class public auto ansi beforefieldinit Hello
       extends [mscorlib]System.Object
{
  .method public hidebysig static void  Main(string[] args) cil managed
  {
    .entrypoint
    // Code size       13 (0xd)
    .maxstack  8
    IL_0000:  nop
    IL_0001:  ldstr      "Hello World!"
    IL_0006:  call       void [mscorlib]System.Console::WriteLine(string)
    IL_000b:  nop
    IL_000c:  ret
  } // end of method Hello::Main

  .method public hidebysig specialname rtspecialname
          instance void  .ctor() cil managed
  {
    // Code size       7 (0x7)
    .maxstack  8
    IL_0000:  ldarg.0
    IL_0001:  call       instance void [mscorlib]System.Object::.ctor()
    IL_0006:  ret
  } // end of method Hello::.ctor

} // end of class Hello
```

## <a name="see-also"></a>참고 항목

- [도구](index.md)
- [*Ildasm.exe* (IL Disassembler)](ildasm-exe-il-disassembler.md)(Ildasm.exe(IL 디스어셈블러))
- [관리되는 실행 프로세스](../../standard/managed-execution-process.md)
- [명령 프롬프트](developer-command-prompt-for-vs.md)
