---
title: F# Interactive 옵션
description: 대화형, fsi.exe에서 F# 지 원하는 명령줄 옵션에 대해 알아봅니다.
ms.date: 05/16/2016
ms.openlocfilehash: c9cd5c2e73a6e2f6ce0a9b2f2a631b6a2658423c
ms.sourcegitcommit: a2d0e1f66367367065bc8dc0dde488ab536da73f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/18/2019
ms.locfileid: "71083115"
---
# <a name="f-interactive-options"></a>F# Interactive 옵션

> [!NOTE]
> 이 문서에서는 현재 Windows만을 위한 환경에 대해 설명합니다.  다시 작성될 예정입니다.

이 항목에서는 F# 대화형, `fsi.exe`에서 지원 되는 명령줄 옵션에 대해 설명 합니다. F#대화형은 F# 컴파일러와 동일한 명령줄 옵션을 많이 허용 하지만 몇 가지 추가 옵션도 허용 합니다.

## <a name="using-f-interactive-for-scripting"></a>스크립팅에 F# 대화형 사용
F#대화형, `fsi.exe`는 대화형으로 실행 하거나 명령줄에서 실행 하 여 스크립트를 실행할 수 있습니다. 명령줄 구문은

```console
> fsi.exe [options] [ script-file [arguments] ]
```

스크립트 파일 F# `.fsx`의 파일 확장명은입니다.

## <a name="table-of-f-interactive-options"></a>F# 대화형 옵션 표
다음 표에는 대화형에서 F# 지원 되는 옵션이 요약 되어 있습니다. 명령줄에서 또는 Visual Studio IDE를 통해 이러한 옵션을 설정할 수 있습니다. Visual Studio IDE에서 이러한 옵션을 설정 하려면 **도구** 메뉴를 열고 **옵션 ...** 을 선택한 다음  **F# 도구** 노드를 확장 하 고  **F# 대화형**을 선택 합니다.

대화형 옵션 인수에 F# 목록이 표시 되는 경우 목록 요소는 세미콜론 (`;`)으로 구분 됩니다.

|옵션|Description|
|------|-----------|
|**--**|나머지 인수를 F# F# 프로그램 또는 스크립트에 대 한 명령줄 인수로 처리 하도록 Interactive에 지시 하는 데 사용 됩니다 .이는 **fsi.exe**목록을 사용 하 여 코드에서 액세스할 수 있습니다.|
|**--checked**[ **+** &#124; **-** ]|**Fsc.exe** 컴파일러 옵션과 동일 합니다. 자세한 내용은 [컴파일러 옵션](compiler-options.md)을 참조하세요.|
|**--codepage:&lt;int&gt;**|**Fsc.exe** 컴파일러 옵션과 동일 합니다. 자세한 내용은 [컴파일러 옵션](compiler-options.md)을 참조하세요.|
|**--consolecolors**[ **+** &#124; **-** ]|경고 및 오류 메시지를 색으로 출력 합니다.|
|**--crossoptimize**[ **+** &#124; **-** ]|크로스 모듈 최적화를 사용 하거나 사용 하지 않도록 설정 합니다.|
|**--debug**[ **+** &#124; **-** ]<br /><br />**--debug:** [**full**&#124;**pdbonly**&#124;**portable**&#124;**embedded**]<br /><br />**-g**[ **+** &#124; **-** ]<br /><br />**-g:** [**full**&#124;**pdbonly**&#124;**portable**&#124;**embedded**]|**Fsc.exe** 컴파일러 옵션과 동일 합니다. 자세한 내용은 [컴파일러 옵션](compiler-options.md)을 참조하세요.|
|**--define:&lt;string&gt;**|**Fsc.exe** 컴파일러 옵션과 동일 합니다. 자세한 내용은 [컴파일러 옵션](compiler-options.md)을 참조하세요.|
|**--deterministic**[ **+** &#124; **-** ]|결정적 어셈블리 (모듈 버전 GUID 및 타임 스탬프 포함)를 생성 합니다.|
|**--exec**|명령줄 F# 에 지정 된 스크립트 파일을 실행 하거나 파일을 로드 한 후에 대화형으로 종료 하도록 지시 합니다.|
|**--fullpaths**|**Fsc.exe** 컴파일러 옵션과 동일 합니다. 자세한 내용은 [컴파일러 옵션](compiler-options.md)을 참조하세요.|
|**--gui**[ **+** &#124; **-** ]|Windows Forms 이벤트 루프를 사용 하거나 사용 하지 않도록 설정 합니다. 기본값은 사용입니다.|
|**--help**<br /><br />**-?**|명령줄 구문 및 각 옵션에 대 한 간단한 설명을 표시 하는 데 사용 됩니다.|
|**--lib:&lt;folder-list&gt;**<br /><br />**-I:&lt;folder-list&gt;**|**Fsc.exe** 컴파일러 옵션과 동일 합니다. 자세한 내용은 [컴파일러 옵션](compiler-options.md)을 참조하세요.|
|**--load:&lt;filename&gt;**|시작 시 지정 된 소스 코드를 컴파일하고 컴파일된 F# 구문을 세션에 로드 합니다. 대상 소스에 **#use** 또는 **#load**같은 스크립팅 지시문이 포함 되어 있는 경우-- **load** 또는 **#load**대신-- **use** 또는 **#use** 를 사용 해야 합니다.|
|**--mlcompatibility**|**Fsc.exe** 컴파일러 옵션과 동일 합니다. 자세한 내용은 [컴파일러 옵션](compiler-options.md)을 참조하세요.|
|**--noframework**|**Fsc.exe** 컴파일러 옵션과 동일 합니다. 자세한 내용은 [컴파일러 옵션](compiler-options.md) 을 참조 하세요.|
|**--nologo**|**Fsc.exe** 컴파일러 옵션과 동일 합니다. 자세한 내용은 [컴파일러 옵션](compiler-options.md)을 참조하세요.|
|**--nowarn:&lt;warning-list&gt;**|**Fsc.exe** 컴파일러 옵션과 동일 합니다. 자세한 내용은 [컴파일러 옵션](compiler-options.md)을 참조하세요.|
|**--optimize**[ **+** &#124; **-** ]|**Fsc.exe** 컴파일러 옵션과 동일 합니다. 자세한 내용은 [컴파일러 옵션](compiler-options.md)을 참조하세요.|
|**--preferreduilang:&lt;lang&gt;**| 기본 출력 언어 문화권 이름 (예: es, ja-jp)을 지정 합니다. |
|**--quiet**|Stdout F# 스트림에 대 한 대화형 출력 을 표시 하지 않습니다.|
|**--quotations-debug**|따옴표 리터럴 및 리플렉션된 정의에서 F# 파생 된 식에 대 한 추가 디버깅 정보를 내보내도록 지정 합니다. 디버그 정보는 F# 식 트리 노드의 사용자 지정 특성에 추가 됩니다. [코드 인용](code-quotations.md) 및 [Expr. customattributes](https://msdn.microsoft.com/library/eb89943f-5f5b-474e-b125-030ca412edb3)를 참조 하세요.|
|**--readline**[ **+** &#124; **-** ]|대화형 모드에서 탭 완성 기능을 사용 하거나 사용 하지 않도록 설정 합니다.|
|**--reference:&lt;filename&gt;**<br /><br />**-r:&lt;filename&gt;**|**Fsc.exe** 컴파일러 옵션과 동일 합니다. 자세한 내용은 [컴파일러 옵션](compiler-options.md)을 참조하세요.|
|**--shadowcopyreferences**[ **+** &#124; **-** ]|F# 대화형 프로세스에서 참조를 잠그지 않도록 합니다.|
|**--simpleresolution**|MSBuild 확인이 아닌 디렉터리 기반 규칙을 사용 하 여 어셈블리 참조를 확인 합니다.|
|**--tailcalls**[ **+** &#124; **-** ]|Tail IL 명령을 사용 하거나 사용 하지 않도록 설정 하 여 tail 재귀 함수에 스택 프레임을 다시 사용 하도록 합니다. 기본적으로 이 옵션은 사용하도록 설정됩니다.|
|**--targetprofile:&lt;string&gt;**|이 어셈블리의 대상 프레임 워크 프로필을 지정 합니다. 유효한 값은 mscorlib, microsoft.netcore.portable.compatibility 또는 microsoft.netcore.portable.compatibility입니다.  기본값은 mscorlib입니다.|
|**--사용:&lt;파일 이름&gt;**|시작 시 지정 된 파일을 초기 입력으로 사용 하도록 인터프리터에 지시 합니다.|
|**--utf8output**|Fsc.exe 컴파일러 옵션과 동일 합니다. 자세한 내용은 [컴파일러 옵션](compiler-options.md)을 참조하세요.|
|**--warn:&lt;warning-level&gt;**|**Fsc.exe** 컴파일러 옵션과 동일 합니다. 자세한 내용은 [컴파일러 옵션](compiler-options.md)을 참조하세요.|
|**--warnaserror**[ **+** &#124; **-** ]|**Fsc.exe** 컴파일러 옵션과 동일 합니다. 자세한 내용은 [컴파일러 옵션](compiler-options.md)을 참조하세요.|
|**--warnaserror**[ **+** &#124; **-** ]: **&lt;int-list&gt;**|**Fsc.exe** 컴파일러 옵션과 동일 합니다. 자세한 내용은 [컴파일러 옵션](compiler-options.md)을 참조하세요.|

## <a name="related-topics"></a>관련 항목

|제목|Description|
|-----|-----------|
|[컴파일러 옵션](compiler-options.md)|F# **Fsc.exe**컴파일러에 사용할 수 있는 명령줄 옵션에 대해 설명 합니다.|
