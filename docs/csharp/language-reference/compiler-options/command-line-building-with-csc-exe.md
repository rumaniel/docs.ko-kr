---
title: csc.exe를 사용한 명령줄 빌드
ms.date: 04/19/2017
helpviewer_keywords:
- builds [C#]
- command line [C#]
ms.assetid: 66e70056-dd20-453c-a9b3-507e0478b015
ms.openlocfilehash: 4b6dfdbce131371553fc729206de29794266bfbe
ms.sourcegitcommit: 69229651598b427c550223d3c58aba82e47b3f82
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2018
ms.locfileid: "48584329"
---
# <a name="command-line-build-with-cscexe"></a>csc.exe를 사용한 명령줄 빌드
명령 프롬프트에서 실행 파일(*csc.exe*)의 이름을 입력하여 C# 컴파일러를 호출할 수 있습니다.

**Visual Studio용 개발자 명령 프롬프트** 창을 사용하는 경우 필요한 환경 변수가 모두 설정됩니다. 이 도구에 액세스하는 방법에 대한 자세한 내용은 [Visual Studio용 개발자 명령 프롬프트](../../../framework/tools/developer-command-prompt-for-vs.md) 항목을 참조하세요. 

표준 명령 프롬프트 창을 사용하는 경우 컴퓨터의 하위 디렉터리에서 *csc.exe*를 호출하려면 먼저 경로를 조정해야 합니다. 또한 *vsvars32.bat*를 실행하여 명령줄 빌드를 지원하도록 적절한 환경 변수를 설정해야 합니다. *vsvars32.bat*를 찾아서 실행하는 방법에 대한 지침을 포함하여 vsvars32.bat에 대한 자세한 내용은 [방법: Visual Studio 명령줄에 필요한 환경 변수 설정](../../../csharp/language-reference/compiler-options/how-to-set-environment-variables-for-the-visual-studio-command-line.md)을 참조하세요.

[!INCLUDE[winsdklong](~/includes/winsdklong-md.md)]만 있는 컴퓨터에서 작업 중인 경우 **Microsoft .NET Framework SDK** 메뉴 옵션에서 여는 **SDK 명령 프롬프트**에서 C# 컴파일러를 사용할 수 있습니다.

또한 MSBuild를 사용하여 프로그래밍 방식으로 C# 프로그램을 빌드할 수도 있습니다. 자세한 내용은 [MSBuild](/visualstudio/msbuild/msbuild)를 참조하세요.

*csc.exe* 실행 파일은 대개 *Windows* 디렉터리 아래의 Microsoft.NET\Framework\\*\<Version>* 폴더에 있습니다. 이 위치는 개별 컴퓨터의 구성에 따라 다를 수 있습니다. 컴퓨터에 .NET Framework 버전이 두 개 이상 설치된 경우 이 파일의 여러 버전을 찾을 수 있습니다. 해당 설치에 대한 자세한 내용은 [방법: 설치된 .NET Framework 버전 확인](../../../framework/migration-guide/how-to-determine-which-versions-are-installed.md)을 참조하세요.

> [!TIP]
>  Visual Studio IDE를 사용하여 프로젝트를 빌드할 때 **출력** 창에 **csc** 명령과 관련 컴파일러 옵션을 표시할 수 있습니다. 이 정보를 표시하려면 [방법: 빌드 로그 파일 보기, 저장 및 구성](/visualstudio/ide/how-to-view-save-and-configure-build-log-files#to-change-the-amount-of-information-included-in-the-build-log)의 지침에 따라 로그 데이터의 세부 정보 표시 수준을 **보통** 또는 **자세히**로 변경합니다. 프로젝트를 다시 빌드한 후 **출력** 창에서 **csc**를 검색하여 C# 컴파일러 호출을 찾습니다.

 **항목 내용**

- [명령줄 구문에 대한 규칙](#-rules-for-command-line-syntax-for-the-c-compiler)

- [샘플 명령줄](#sample-command-lines-for-the-c-compiler)

- [C# 컴파일러 및 C++ 컴파일러 출력의 차이점](#differences-between-c-compiler-and-c-compiler-output)

## <a name="rules-for-command-line-syntax-for-the-c-compiler"></a>C# 컴파일러의 명령줄 구문에 대한 규칙

C# 컴파일러에서는 운영 체제 명령줄에 지정된 인수를 해석할 때 다음 규칙을 사용합니다.

- 인수를 공백이나 탭으로 구분합니다.

- 캐럿 문자(^)는 이스케이프 문자나 구분 기호로 인식되지 않습니다. 문자는 프로그램의 `argv` 배열에 전달된 후 운영 체제의 명령줄 구문 분석기에서 처리됩니다.

- 큰따옴표로 묶은 문자열(“string”)은 포함된 공백에 상관없이 하나의 인수로 해석됩니다. 따옴표로 묶은 문자열은 인수에 포함될 수 있습니다.

- 백슬래시 다음의 큰따옴표(\\")는 리터럴 큰따옴표 문자(")로 해석됩니다.

- 백슬래시는 큰따옴표 바로 앞에 있지 않으면 리터럴로 해석됩니다.

- 짝수 개의 백슬래시 다음에 큰따옴표가 오는 경우, 백슬래시 쌍마다 하나의 백슬래시가 `argv` 배열에 배치되고 큰따옴표는 문자열 구분 기호로 해석됩니다.

- 홀수 개의 백슬래시 다음에 큰따옴표가 오는 경우, 백슬래시 쌍마다 하나의 백슬래시가 `argv` 배열에 배치되고 큰따옴표는 나머지 백슬래시에 의해 "이스케이프"됩니다. 이로 인해 리터럴 큰따옴표(")가 `argv`에 추가됩니다.

## <a name="sample-command-lines-for-the-c-compiler"></a>C# 컴파일러에 대한 샘플 명령줄

- *File.cs*를 컴파일하여 *File.exe*를 생성합니다.

```console
csc File.cs 
```

- *File.cs*를 컴파일하여 *File.dll*을 생성합니다.

```console
csc -target:library File.cs
```

- *File.cs*를 컴파일하여 *My.exe*를 만듭니다.

```console
csc -out:My.exe File.cs
```

- 최적화를 사용하여 현재 디렉터리에 있는 모든 C# 파일을 컴파일하고 DEBUG 기호를 정의합니다. 출력은 *File2.exe*입니다.

```console
csc -define:DEBUG -optimize -out:File2.exe *.cs
```

- 현재 디렉터리에 있는 모든 C# 파일을 컴파일하여 *File2.dll*의 디버그 버전을 생성합니다. 로고 및 경고가 표시되지 않습니다.

```console
csc -target:library -out:File2.dll -warn:0 -nologo -debug *.cs
```

- 현재 디렉터리에 있는 모든 C# 파일을 *Something.xyz*(DLL)로 컴파일합니다.

```console
csc -target:library -out:Something.xyz *.cs
```

## <a name="differences-between-c-compiler-and-c-compiler-output"></a>C# 컴파일러 및 C++ 컴파일러 출력의 차이점
C# 컴파일러를 호출하면 개체 파일(*.obj*)은 만들어지지 않고 출력 파일이 직접 만들어집니다. 따라서 C# 컴파일러에는 링커가 필요하지 않습니다.

## <a name="see-also"></a>참고 항목

- [C# 컴파일러 옵션](../../../csharp/language-reference/compiler-options/index.md)  
- [사전순 C# 컴파일러 옵션 목록](../../../csharp/language-reference/compiler-options/listed-alphabetically.md)  
- [범주별 C# 컴파일러 옵션 목록](../../../csharp/language-reference/compiler-options/listed-by-category.md)  
- [Main()과 명령줄 인수](../../../csharp/programming-guide/main-and-command-args/index.md)  
- [명령줄 인수](../../../csharp/programming-guide/main-and-command-args/command-line-arguments.md)  
- [방법: 명령줄 인수 표시](../../../csharp/programming-guide/main-and-command-args/how-to-display-command-line-arguments.md)  
- [방법: foreach를 사용하여 명령줄 인수 액세스](../../../csharp/programming-guide/main-and-command-args/how-to-access-command-line-arguments-using-foreach.md)  
- [Main() 반환 값](../../../csharp/programming-guide/main-and-command-args/main-return-values.md)
