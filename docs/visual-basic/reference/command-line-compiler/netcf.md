---
title: -netcf
ms.date: 03/13/2018
f1_keywords:
- /netcf
- -netcf
helpviewer_keywords:
- -netcf compiler option [Visual Basic]
- netcf compiler option [Visual Basic]
- /netcf compiler option [Visual Basic]
ms.assetid: db7cfa59-c315-401c-a59b-0daf355343d6
ms.openlocfilehash: 3df7e622f97a5a1291736180e3964b1b3deaea2f
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005457"
---
# <a name="-netcf"></a>-netcf

.NET Compact Framework를 대상으로 하는 컴파일러를 설정 합니다.

## <a name="syntax"></a>구문

```console
-netcf
```

## <a name="remarks"></a>설명

@No__t-0 옵션을 선택 하면 Visual Basic 컴파일러가 전체 .NET Framework 아닌 .NET Compact Framework를 대상으로 합니다. 전체 .NET Framework에만 표시 되는 언어 기능은 사용할 수 없습니다.

@No__t-0 옵션은 [-sdkpath](../../../visual-basic/reference/command-line-compiler/sdkpath.md)와 함께 사용 하도록 설계 되었습니다. @No__t-0에서 사용 하지 않도록 설정 된 언어 기능은 `-sdkpath`로 지정 된 파일에 없는 언어 기능입니다.

> [!NOTE]
> @No__t-0 옵션은 Visual Studio 개발 환경에서 사용할 수 없습니다. 명령줄에서 컴파일하는 경우에만 사용할 수 있습니다. @No__t-0 옵션은 Visual Basic 장치 프로젝트가 로드 될 때 설정 됩니다.

@No__t-0 옵션은 다음과 같은 언어 기능을 변경 합니다.

- 프로그램의 실행을 종료 하는 [End \<keyword > Statement](../../../visual-basic/language-reference/statements/end-keyword-statement.md) 키워드는 사용할 수 없습니다. 다음 프로그램은 @no__t 없이 컴파일되고 실행 되지만 `-netcf`을 사용 하 여 컴파일 타임에 실패 합니다.

  [!code-vb[VbVbalrCompiler#34](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCompiler/VB/netcf.vb#34)]

- 런타임에 바인딩은 모든 폼에서 사용할 수 없습니다. 컴파일 시간 오류는 인식 되는 런타임에 바인딩 시나리오가 발견 될 때 생성 됩니다. 다음 프로그램은 @no__t 없이 컴파일되고 실행 되지만 `-netcf`을 사용 하 여 컴파일 타임에 실패 합니다.

  [!code-vb[VbVbalrCompiler#35](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCompiler/VB/OptionStrictOff.vb#35)]

- [Auto](../../../visual-basic/language-reference/modifiers/auto.md), [Ansi](../../../visual-basic/language-reference/modifiers/ansi.md)및 [유니코드](../../../visual-basic/language-reference/modifiers/unicode.md) 한정자를 사용할 수 없습니다. [Declare statement](../../../visual-basic/language-reference/statements/declare-statement.md) 문의 구문도 `Declare Sub|Function name Lib "library" [Alias "alias"] [([arglist])]`로 수정 됩니다. 다음 코드는 컴파일할 때 `-netcf`의 효과를 보여 줍니다.

  [!code-vb[VbVbalrCompiler#36](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCompiler/VB/OptionStrictOff.vb#36)]

- Visual Basic에서 제거 된 Visual Basic 6.0 키워드를 사용 하면 `-netcf`이 사용 되는 경우 다른 오류가 생성 됩니다. 이는 다음 키워드에 대 한 오류 메시지에 영향을 줍니다.

  - `Open`

  - `Close`

  - `Put`

  - `Print`

  - `Write`

  - `Input`

  - `Lock`

  - `Unlock`

  - `Seek`

  - `Width`

  - `Name`

  - `FreeFile`

  - `EOF`

  - `Loc`

  - `LOF`

  - `Line`

## <a name="example"></a>예제

다음 코드는 C 드라이브에 있는 .NET Compact Framework의 기본 설치 디렉터리에 있는 mscorlib.dll 및 Microsoft.visualbasic 버전을 사용 하 여 .NET Compact Framework `Myfile.vb`을 컴파일합니다. 일반적으로 .NET Compact Framework의 최신 버전을 사용 합니다.

```console
vbc -netcf -sdkpath:"c:\Program Files\Microsoft Visual Studio .NET 2003\CompactFrameworkSDK\v1.0.5000\Windows CE " myfile.vb
```

## <a name="see-also"></a>참조

- [Visual Basic 명령줄 컴파일러](../../../visual-basic/reference/command-line-compiler/index.md)
- [샘플 컴파일 명령줄](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
- [-sdkpath](../../../visual-basic/reference/command-line-compiler/sdkpath.md)
