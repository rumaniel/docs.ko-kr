---
title: Ildasm.exe(IL 디스어셈블러)
ms.date: 03/30/2017
helpviewer_keywords:
- PE files, MSIL Disassembler
- portable executable files, MSIL Disassembler
- Ildasm.exe
- MSIL Disassembler
- text files produced by MSIL Disassembler
- disassembling file for MSIL Assembler input
ms.assetid: db27f6b2-f1ec-499e-be3a-7eecf95ca42b
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 9d08d6164c00d2b5b750c9edda46a7be18153152
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71044651"
---
# <a name="ildasmexe-il-disassembler"></a>Ildasm.exe(IL 디스어셈블러)

IL 디스어셈블러는 IL 어셈블러(*Ilasm.exe*)의 자매 도구입니다. *Ildasm.exe*는 IL(intermediate language) 코드가 포함된 PE(이식 가능한 실행) 파일을 가져와서 *Ildasm.exe*에 입력하기에 적합한 텍스트 파일을 만듭니다.

이 도구는 자동으로 Visual Studio와 함께 설치됩니다. 이 도구를 실행하려면 Visual Studio용 개발자 명령 프롬프트(또는 Windows 7의 Visual Studio 명령 프롬프트)를 사용합니다. 자세한 내용은 [명령 프롬프트](developer-command-prompt-for-vs.md)를 참조하세요.

명령 프롬프트에 다음을 입력합니다.

## <a name="syntax"></a>구문

```console
ildasm [options] [PEfilename] [options]
```

## <a name="parameters"></a>매개 변수

*.exe*, *.dll*, *.obj*, *.lib* 및 *.winmd* 파일에 사용할 수 있는 옵션은 다음과 같습니다.

| 옵션 | 설명 |
| ------ | ----------- |
|**/out=** `filename`|결과를 그래픽 사용자 인터페이스에 표시하지 않고 지정된 `filename`을 사용하여 출력 파일을 만듭니다.|
|**/rtf**|서식 있는 텍스트로 출력을 생성합니다. **/text** 옵션과 함께 사용할 수 없습니다.|
|**/text**|결과를 그래픽 사용자 인터페이스에 표시하거나 출력 파일로 표시하지 않고 콘솔 창에 표시합니다.|
|**/html**|HTML 형식으로 출력을 생성합니다. **/output** 옵션으로만 사용할 수 있습니다.|
|**/?**|이 도구의 명령 구문 및 옵션을 표시합니다.|

*.exe*, *.dll* 및 *.winmd* 파일에 사용할 수 있는 추가 옵션은 다음과 같습니다.

| 옵션 | 설명 |
| ------ | ----------- |
|**/bytes**|16진수 형식의 실제 바이트 수를 명령 주석으로 표시합니다.|
|**/caverbal**|사용자 지정 특성 blob을 일반 텍스트 형식으로 생성합니다. 기본값은 이진 형식입니다.|
|**/linenum**|원본 소스 줄에 대한 참조를 포함합니다.|
|**/nobar**|디스어셈블리 진행률 표시줄 팝업 창을 표시하지 않습니다.|
|**/noca**|사용자 지정 특성 출력을 생성하지 않습니다.|
|**/project**|메타데이터를 기본 Windows 런타임에서 표시되는 방식 대신, 관리 코드에 표시되는 방식으로 표시합니다. 만약 `PEfilename`이 Windows 메타데이터( *.winmd*) 파일이 아니라면, 이 옵션은 효과가 없습니다. [Windows 스토어 앱 및 Windows 런타임에 대한 .NET Framework 지원](../../standard/cross-platform/support-for-windows-store-apps-and-windows-runtime.md)을 참조하세요.|
|**/pubonly**|공용 형식 및 멤버만 디스어셈블합니다. **/visibility:PUB**와 같습니다.|
|**/quoteallnames**|모든 이름을 작은따옴표 내에 포함시킵니다.|
|**/raweh**|예외 처리 절을 원시 형식으로 표시합니다.|
|**/source**|주석에 따라 원본 소스 줄을 표시합니다.|
|**/tokens**|클래스 및 멤버의 메타데이터 토큰을 표시합니다.|
|**/visibility:** `vis`[+`vis`...]|지정된 표시 범위의 형식 또는 멤버만 디스어셈블합니다. 다음은 `vis`에 사용할 수 있는 값입니다.<br /><br /> **PUB** - Public<br /><br /> **PRI** - Private<br /><br /> **FAM** - Family<br /><br /> **ASM** - Assembly<br /><br /> **FAA** - Family and Assembly<br /><br /> **FOA** - Family or Assembly<br /><br /> **PSC** - Private Scope<br /><br /> 이러한 표시 한정자의 정의는 <xref:System.Reflection.MethodAttributes> 및 <xref:System.Reflection.TypeAttributes>를 참조하십시오.|

*.exe*, *.dll* 및 *.winmd* 파일에 대해 파일 또는 콘솔 출력 전용으로 사용할 수 있는 옵션은 다음과 같습니다.

| 옵션 | 설명 |
| ------ | ----------- |
|**/all**|**/header**, **/bytes**, **/stats**, **/classlist**, **/tokens** 옵션 조합을 지정합니다.|
|**/classlist**|모듈에 정의된 클래스 목록을 포함합니다.|
|**/forward**|정방향 클래스 선언을 사용합니다.|
|**/headers**|출력에 파일 헤더 정보를 포함시킵니다.|
|**/item:** `class`[ **::** `member`[`(sig`]]|지정된 인수에 따라 다음과 같이 디스어셈블합니다.<br /><br /> -   지정된 `class`를 디스어셈블합니다.<br />-   지정된 `class`의 `member`를 디스어셈블합니다.<br />-   지정된 시그니처 `sig`가 포함된 `class`의 `member`를 디스어셈블합니다. `sig` 형식은 다음과 같습니다.<br />     [`instance`] `returnType`(`parameterType1`, `parameterType2`, …, `parameterTypeN`)<br />     **참고** .NET Framework 버전 1.0 및 1.1에서는 `(sig)`와 같이 `sig` 다음에 닫는 괄호가 있어야 합니다. .Net Framework 2.0부터는 `(sig`와 같이 닫는 괄호를 생략해야 합니다.|
|**/noil**|IL 어셈블리 코드 출력을 표시하지 않습니다.|
|**/stats**|이미지에 대한 통계를 포함합니다.|
|**/typelist**|라운드트립에서 형식 순서를 유지하기 위해 전체 형식 목록을 생성합니다.|
|**/unicode**|출력에 유니코드 인코딩을 사용합니다.|
|**/utf8**|출력에 UTF-8 인코딩을 사용합니다. ANSI가 기본값입니다.|

*.exe*, *.dll*, *.obj*, *.lib* 및 *.winmd* 파일에 대해 파일 또는 콘솔 출력 전용으로 사용할 수 있는 옵션은 다음과 같습니다.

| 옵션 | 설명 |
| ------ | ----------- |
|**/metadata**[=`specifier`]|메타데이터를 표시합니다. `specifier`는 다음과 같습니다.<br /><br /> **MDHEADER** - 메타데이터 헤더 정보 및 크기를 표시합니다.<br /><br /> **HEX** - 정보를 단어뿐만 아니라 16진수로 표시합니다.<br /><br /> **CSV** - 레코드 개수 및 힙 크기를 표시합니다.<br /><br /> **UNREX** - 확인할 수 없는 외부 참조를 표시합니다.<br /><br /> **SCHEMA** - 메타데이터 헤더 및 스키마 정보를 표시합니다.<br /><br /> **RAW** - 원시 메타데이터 테이블을 표시합니다.<br /><br /> **HEAPS** - 원시 힙을 표시합니다.<br /><br /> **VALIDATE** - 메타데이터의 일관성을 확인합니다.<br /><br /> `specifier`에 대해 다른 값을 사용하여 **/metadata**를 여러 번 지정할 수 있습니다.|

*.lib* 파일에 대해 파일 또는 콘솔 출력 전용으로 사용할 수 있는 옵션은 다음과 같습니다.

| 옵션 | 설명 |
| ------ | ----------- |
|**/objectfile**=`filename`|지정된 라이브러리에 있는 단일 개체 파일의 메타데이터를 표시합니다|

> [!NOTE]
> *Ildasm.exe*의 모든 옵션은 대/소문자가 구분되지 않으며 처음 세 문자로 인식됩니다. 예를 들어 **/quo**는 **/quoteallnames**와 같습니다. 인수를 지정하는 옵션에는 옵션과 인수 사이의 구분 기호로 콜론(:) 또는 등호(=) 중 하나만 사용할 수 있습니다. 예를 들어 **/output:** *filename*은 **/output=** *filename*과 같습니다.

## <a name="remarks"></a>설명

*Ildasm.exe*는 디스크의 PE 파일에 대해서만 작동하며, 전역 어셈블리 캐시에 설치된 파일에 대해서는 작동하지 않습니다.

*Ildasm.exe*를 사용하여 생성한 텍스트 파일은 IL 어셈블러(*Ilasm.exe*)에 대한 입력 파일로 사용될 수 있습니다. 이렇게 하면 런타임 메타데이터 특성을 모두 지원하지 않는 프로그래밍 언어로 코드를 컴파일할 때 유용합니다. 코드를 컴파일하고 *Ildasm.exe*를 사용하여 출력을 실행한 후에는 결과로 만들어지는 IL 텍스트 파일을 수동으로 편집하여 손실된 특성을 추가할 수 있습니다. 그런 다음에는 IL 어셈블러를 통해 이 텍스트 파일을 실행하여 최종 실행 파일을 생성할 수 있습니다.

> [!NOTE]
> 포함된 네이티브 코드가 들어 있는 PE 파일(예: Visual C++로 생성된 PE 파일)에는 현재 이 방법을 사용할 수 없습니다.  

IL 디스어셈블러의 기본 GUI를 사용하면 계층 구조 트리 뷰에서 기존 PE 파일의 메타데이터 및 디스어셈블된 코드를 볼 수 있습니다. 이 GUI를 사용하려면 해당 명령줄에서 **ildasm**을 입력합니다. 이때 *PEfilename* 인수나 기타 옵션은 지정하지 않습니다. **파일** 메뉴에서 *Ildasm.exe*에 로드하려는 PE 파일 탐색할 수 있습니다. 선택한 PE에 대해 표시된 메타데이터 및 디스어셈블된 코드를 저장하려면 **파일** 메뉴에서 **덤프** 명령을 선택합니다. 계층 구조 트리 뷰만 저장하려면 **파일** 메뉴에서 **트리 뷰 덤프** 명령을 선택합니다. *Ildasm.exe*로 파일을 로드하고 출력 내용을 해석하는 방법에 대한 자세한 지침을 보려면 Windows SDK와 함께 제공되는 Samples 폴더의 *Ildasm.exe* 자습서를 참조하세요.

*Ildasm.exe*에 포함 리소스가 들어 있는 *PEfilename* 인수를 제공하면 여러 개의 출력 파일이 생성됩니다. 즉, IL 코드가 들어 있는 텍스트 파일이 생성되고, 관리되는 각 포함 리소스의 경우 메타데이터의 리소스 이름을 사용하여 .resources 파일이 생성됩니다. 관리되지 않는 리소스가 *PEfilename*에 포함되어 있으면 **/output** 옵션으로 IL 출력에 대해 지정한 파일 이름을 사용하여 .res 파일이 생성됩니다.

> [!NOTE]
> *Ildasm.exe*를 사용하면 *.obj* 및 *.lib* 입력 파일에 대해 메타데이터 설명만 표시되며, 이러한 파일 형식에 대한 IL 코드는 디스어셈블되지 않습니다.

.exe 또는 *.dll* 파일을 통해 *Ildasm.exe*를 실행하여 파일이 관리되는지 여부를 확인할 수 있습니다. 파일이 관리되지 않으면 파일에 올바른 공용 언어 런타임 헤더가 없어 디스어셈블될 수 없음을 나타내는 메시지가 표시됩니다. 파일이 관리되면 도구가 성공적으로 실행됩니다.

## <a name="version-information"></a>버전 정보

.NET Framework 4.5부터 제공되는 *Ildasm.exe*는 원시 이진 콘텐츠를 표시하여 인식할 수 없는 마샬 BLOB(Binary Large Object)을 처리합니다. 예를 들어, 다음 코드는 C# 프로그램에서 생성된 마샬 BLOB가 표시되는 방법을 보여 줍니다.

```csharp
public void Test([MarshalAs((short)70)] int test) { }
```

```il
// IL from Ildasm.exe output
.method public hidebysig instance void Test(int32  marshal({ 46 }) test) cil managed
```

.NET Framework 4.5부터 제공되는 *Ildasm.exe*는 *Ildasm.exe* 출력에서 발췌한 다음 예제에서와 같이 인터페이스 구현에 적용되는 특성을 표시합니다.

```il
.class public auto ansi beforefieldinit MyClass
  extends [mscorlib]System.Object
  implements IMyInterface
  {
    .interfaceimpl type IMyInterface
    .custom instance void
      [mscorlib]System.Diagnostics.DebuggerNonUserCodeAttribute::.ctor() = ( 01 00 00 00 )
      …
```

## <a name="examples"></a>예

다음 명령을 사용하여 PE 파일 `MyHello.exe`에 대한 메타데이터 및 디스어셈블된 코드를 *Ildasm.exe*의 기본 GUI에 표시합니다.

```console
ildasm myHello.exe
```

다음 명령을 사용하여 `MyFile.exe` 파일을 디스어셈블하고 그 결과로 만들어지는 IL 어셈블러 텍스트를 *MyFile.il* 파일에 저장합니다.

```console
ildasm MyFile.exe /output:MyFile.il
```

다음 명령을 사용하여 `MyFile.exe` 파일을 디스어셈블하고 그 결과로 만들어지는 IL 어셈블러 텍스트를 콘솔 창에 표시합니다.

```console
ildasm MyFile.exe /text
```

`MyApp.exe` 파일에 관리되는 포함 리소스와 관리되지 않는 포함 리소스가 들어 있는 경우, 다음 명령을 사용하여 다음과 같은 4개 파일을 생성합니다. *MyApp.il*, *MyApp.res*, *Icons.resources* 및 *Message.resources*.

```console
ildasm MyApp.exe /output:MyApp.il
```

다음 명령을 사용하여 `MyFile.exe`의 `MyClass` 클래스 내에 있는 `MyMethod` 메서드를 디스어셈블하고 해당 출력을 콘솔 창에 표시합니다.

```console
ildasm /item:MyClass::MyMethod MyFile.exe /text
```

앞의 예제에서는 시그니처가 서로 다른 `MyMethod` 메서드가 여러 개 있을 수 있습니다. 다음 명령을 사용하여 반환 형식이 **void**이고 매개 변수 형식이 **int32** 및 **string**인 인스턴스 메서드 `MyMethod`를 디스어셈블합니다.

```console
ildasm /item:"MyClass::MyMethod(instance void(int32,string)" MyFile.exe /text
```

> [!NOTE]
> .NET Framework 버전 1.0 및 1.1에서는 `MyMethod(instance void(int32))`와 같이 메서드 이름 다음의 왼쪽 괄호와 시그니처 다음의 오른쪽 괄호가 짝을 이뤄야 합니다. .NET Framework 2.0부터는 `MyMethod(instance void(int32)`와 같이 닫는 괄호를 생략해야 합니다.

`static` 메서드(Visual Basic의 경우 `Shared` 메서드)를 검색하려면 `instance` 키워드를 생략합니다. `int32` 및 `string`과 같이 기본 형식이 아닌 클래스 형식은 네임스페이스를 포함해야 하며 앞에 `class` 키워드가 있어야 합니다. 외부 형식 앞에는 대괄호로 묶인 라이브러리 이름이 있어야 합니다. 다음 명령은 `MyMethod` 형식의 매개 변수가 하나 있고 반환 형식이 <xref:System.AppDomain>인 <xref:System.AppDomain>라는 정적 메서드를 디스어셈블합니다.

```console
ildasm /item:"MyClass::MyMethod(class [mscorlib]System.AppDomain(class [mscorlib]System.AppDomain)" MyFile.exe /text
```

중첩 형식은 해당 형식을 포함하는 클래스와 슬래시 다음에 있어야 합니다. 예를 들어, `MyNamespace.MyClass` 클래스에 `NestedClass`라는 중첩 클래스가 들어 있으면 중첩 클래스는 `class MyNamespace.MyClass/NestedClass`로 식별됩니다.

## <a name="see-also"></a>참고 항목

- [도구](index.md)
- [Ilasm.exe(IL 어셈블러)](ilasm-exe-il-assembler.md)
- [관리되는 실행 프로세스](../../standard/managed-execution-process.md)
- [명령 프롬프트](developer-command-prompt-for-vs.md)
