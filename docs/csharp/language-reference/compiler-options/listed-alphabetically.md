---
title: C# 컴파일러 옵션 사전순 목록
ms.date: 05/15/2018
helpviewer_keywords:
- compiler options [C#], listed alphabetically
- C# language, compiler options listed alphabetically
- Visual C# compiler, options listed alphabetically
- Visual C#, compiler options listed alphabetically
ms.assetid: 43535ea0-ca47-4a15-b528-615087a86092
ms.openlocfilehash: 450463100782f98b6ded0781b1d3c19b0db97534
ms.sourcegitcommit: 3ac05b2c386c8cc5e73f4c7665f6c0a7ed3da1bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/20/2019
ms.locfileid: "71151771"
---
# <a name="c-compiler-options-listed-alphabetically"></a>C# 컴파일러 옵션 사전순 목록

여기에서는 컴파일러 옵션을 사전순으로 정렬합니다. 범주별 목록을 보려면 [C# 컴파일러 옵션 범주별 목록](listed-by-category.md)을 참조하세요.

|옵션|용도|
|------------|-------------|
|[@](response-file-compiler-option.md)|추가 옵션에 대한 지시 파일을 읽습니다.|
|[-?](help-compiler-option.md)|stdout에 사용법 메시지를 표시합니다.|
|-additionalfile|코드 생성에 직접 영향을 주지 않지만 오류 또는 경고를 생성하기 위해 분석기에서 사용할 수 있는 추가 파일에 이름을 지정합니다.|
|[-addmodule](addmodule-compiler-option.md)|지정한 모듈을 이 어셈블리에 링크합니다.|
|-analyzer|이 어셈블리에서 분석기를 실행합니다(약식: -a).|
|[/appconfig](appconfig-compiler-option.md)|어셈블리 바인딩 시간에 app.config의 위치를 지정합니다.|
|[-baseaddress](baseaddress-compiler-option.md)|빌드할 라이브러리의 기준 주소를 지정합니다.|
|[-bugreport](bugreport-compiler-option.md)|'버그 보고서' 파일을 만듭니다. -errorreport:prompt 또는 -errorreport:send와 함께 사용하면 이 파일이 충돌 정보와 함께 전송됩니다.|
|[/checked](checked-compiler-option.md)|컴파일러에서 오버플로 검사를 생성하도록 합니다.|
|-checksumalgorithm:\<alg>|PDB에 저장된 소스 파일 체크섬을 계산하기 위한 알고리즘을 지정합니다.  지원되는 값은 다음과 같습니다. SHA256(기본값) 또는 SHA1.<br>SHA1 관련 충돌 문제로 인해 SHA256을 사용하는 것이 좋습니다. |
|[-codepage](codepage-compiler-option.md)|소스 파일을 열 때 사용할 코드 페이지를 지정합니다.|
|[-debug](debug-compiler-option.md)|디버깅 정보를 내보냅니다.|
|[-define](define-compiler-option.md)|조건부 컴파일 기호를 정의합니다.|
|[-delaysign](delaysign-compiler-option.md)|강력한 이름 키의 공용 부분만 사용하여 어셈블리 서명을 연기합니다.|
|[-deterministic](deterministic-compiler-option.md)|입력이 동일한 경우 컴파일 간에 이진 콘텐츠가 동일한 어셈블리를 컴파일러에서 출력하도록 합니다.|
|[-doc](doc-compiler-option.md)|생성할 XML 문서 파일을 지정합니다.|
|-embed|PDB에 모든 소스 파일을 포함합니다.|
|-embed:\<file list>|PDB에 특정 파일을 포함합니다.|
|-errorendlocation|각 오류의 끝 위치에 해당하는 줄과 열을 출력합니다.|
|-errorlog:\<file>|모든 컴파일러와 분석기 진단을 로그할 파일을 지정합니다.|
|[-errorreport](errorreport-compiler-option.md)|내부 컴파일러 오류를 처리하는 방법을 지정합니다. prompt, send 또는 none 중에서 선택할 수 있으며 기본값은 none입니다.|
|[-filealign](filealign-compiler-option.md)|출력 파일 섹션에 사용되는 맞춤을 지정합니다.|
|[/fullpaths](fullpaths-compiler-option.md)|컴파일러에서 정규화된 경로를 생성하도록 합니다.|
|[-help](help-compiler-option.md)|stdout에 사용법 메시지를 표시합니다.|
|[-highentropyva](highentropyva-compiler-option.md)|높은 엔트로피 ASLR을 지원하도록 지정합니다.|
|-incremental|증분 컴파일을 사용하도록 설정합니다(사용되지 않음).|
|[-keycontainer](keycontainer-compiler-option.md)|강력한 이름의 키 컨테이너를 지정합니다.|
|[-keyfile](keyfile-compiler-option.md)|강력한 이름의 키 파일을 지정합니다.|
|[-langversion:\<string>](langversion-compiler-option.md)|언어 버전 지정: 기본값, ISO-1, ISO-2, 3, 4, 5, 6, 7, 7.1, 7.2, 7.3 또는 최신 |
|[/lib](lib-compiler-option.md)|참조를 검색할 추가 디렉터리를 지정합니다.|
|[-link](link-compiler-option.md)|지정된 어셈블리의 COM 형식 정보를 프로젝트에 사용할 수 있도록 합니다.|
|[-linkresource](linkresource-compiler-option.md)|지정한 리소스를 이 어셈블리에 링크합니다.|
|[-main](main-compiler-option.md)|진입점을 포함하는 형식을 지정합니다. 다른 모든 가능한 진입점은 무시합니다.|
|[-moduleassemblyname](moduleassemblyname-compiler-option.md)|.netmodule에서 public이 아닌 형식에 액세스할 수 있는 어셈블리를 지정합니다.|
|-modulename:\<string>|소스 모듈의 이름을 지정합니다.|
|[-noconfig](noconfig-compiler-option.md)|컴파일러에서 CSC.RSP 파일을 자동으로 포함하지 않도록 합니다.|
|[-nologo](nologo-compiler-option.md)|컴파일러 저작권 메시지를 표시하지 않습니다.|
|[-nostdlib](nostdlib-compiler-option.md)|컴파일러에서 표준 라이브러리(mscorlib.dll)를 참조하지 않도록 합니다.|
|[-nowarn](nowarn-compiler-option.md)|특정 경고 메시지를 사용하지 않도록 설정합니다.|
|[-nowin32manifest](nowin32manifest-compiler-option.md)|애플리케이션 매니페스트를 실행 파일에 포함하지 않도록 컴파일러에 지시합니다.|
|[-optimize](optimize-compiler-option.md)|최적화를 사용하거나 사용하지 않도록 설정합니다.|
|[-out](out-compiler-option.md)|출력 파일 이름을 지정합니다(기본값: 주 클래스가 있는 파일의 기본 이름 또는 첫째 파일).|
|-parallel[+&#124;-]|동시 빌드(+)를 사용할지 여부를 지정합니다.|
|[-pathmap](pathmap-compiler-option.md)|컴파일러에서 출력되는 소스 경로 이름에 대한 매핑을 지정합니다.|
|[/pdb](pdb-compiler-option.md)|.pdb 파일의 이름과 위치를 지정합니다.|
|[-platform](platform-compiler-option.md)|이 코드를 실행할 수 있는 플랫폼을 x86, Itanium, x64, anycpu 또는 anycpu32bitpreferred로 제한합니다. 기본값은 anycpu입니다.|
|[/preferreduilang](preferreduilang-compiler-option.md)|컴파일러 출력에 사용할 언어를 지정합니다.|
|[-publicsign](publicsign-compiler-option.md)|어셈블리에 서명하지 않고 공개 키를 적용하지만 어셈블리가 서명되었음을 나타내는 비트를 어셈블리에 설정합니다.|
|[-recurse](recurse-compiler-option.md)|와일드카드 지정에 따라 현재 디렉터리와 하위 디렉터리에 있는 모든 파일을 포함합니다.|
|[-reference](reference-compiler-option.md)|지정한 어셈블리 파일에서 메타데이터를 참조합니다.|
|[/refout](refout-compiler-option.md)|주 어셈블리 외에도 참조 어셈블리를 생성합니다.|
|[/refonly](refonly-compiler-option.md)|주 어셈블리를 대신 참조 어셈블리를 생성합니다.|
|-reportanalyzer|실행 시간과 같은 추가적인 분석 정보를 보고합니다.|
|[-resource](resource-compiler-option.md)|지정한 리소스를 포함합니다.|
|-ruleset:\<file>|특정 진단을 사용하지 않는 규칙 집합 파일을 지정합니다.|
|[-subsystemversion](subsystemversion-compiler-option.md)|실행 파일이 사용할 수 있는 하위 시스템의 최소 버전을 지정합니다.|
|[-target](target-compiler-option.md)|네 가지 옵션([-target:appcontainerexe](target-appcontainerexe-compiler-option.md), [-target:exe](target-exe-compiler-option.md), [-target:library](target-library-compiler-option.md), [-target:module](target-module-compiler-option.md), [-target:winexe](target-winexe-compiler-option.md),  [-target:winmdobj](target-winmdobj-compiler-option.md)) 중 하나를 사용하여 출력 파일의 형식을 지정합니다.|
|[/unsafe](unsafe-compiler-option.md)|[안전하지 않은](../keywords/unsafe.md) 코드를 허용합니다.|
|[-utf8output](utf8output-compiler-option.md)|컴파일러 메시지를 UTF-8 인코딩으로 출력합니다.|
|-version|컴파일러 버전 번호를 표시하고 종료합니다.|
|[/warn](warn-compiler-option.md)|경고 수준(0-4)을 설정합니다.|
|[-warnaserror](warnaserror-compiler-option.md)|특정 경고를 오류로 보고합니다.|
|[-win32icon](win32icon-compiler-option.md)|이 아이콘을 사용하여 출력합니다.|
|[-win32manifest](win32manifest-compiler-option.md)|사용자 지정 win32 매니페스트 파일을 지정합니다.|
|[/win32res:](win32res-compiler-option.md)|win32 리소스 파일(.res)을 지정합니다.|

## <a name="see-also"></a>참고 항목

- [C# 컴파일러 옵션](index.md)
- [범주별 C# 컴파일러 옵션 목록](listed-by-category.md)
- [방법: Visual Studio 명령줄에 필요한 환경 변수 설정](how-to-set-environment-variables-for-the-visual-studio-command-line.md)
- [\<compiler> 요소](../../../framework/configure-apps/file-schema/compiler/compiler-element.md)
