---
title: Winres.exe(Windows 리소스 지역화 편집기)
ms.date: 08/15/2018
helpviewer_keywords:
- Winres.exe
- Windows Forms Resource Editor
- Windows Resource Localization Editor
- localization
- Windows Forms, localization
- forms, localizing
- resx files
- .resx files
ms.assetid: cb8bc835-9221-4888-af53-1a4f5fad6c48
author: mairaw
ms.author: mairaw
ms.openlocfilehash: df7ce0795daabdf34f46e20460bef23e7c486467
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71043900"
---
# <a name="winresexe-windows-resource-localization-editor"></a>Winres.exe(Windows 리소스 지역화 편집기)

Winres.exe(Windows 리소스 지역화 편집기)는 지역화 전문가가 폼에 사용된 Windows Forms UI(사용자 인터페이스)를 쉽게 지역화하는 데 사용할 수 있는 시각적 레이아웃 도구입니다. Winres.exe의 입력으로 사용되는 .resx 또는 .resources 파일은 Microsoft Visual Studio 같은 시각적 디자인 환경을 사용하여 만들 수 있습니다. .NET Framework 애플리케이션의 리소스를 배포하는 데 대한 자세한 내용은 [데스크톱 앱의 리소스](../resources/index.md)를 참조하세요.

Winres.exe는 Visual Studio와 함께 설치됩니다. 도구를 실행하려면 Visual Studio용 개발자 명령 프롬프트를 사용합니다. 자세한 내용은 [명령 프롬프트](developer-command-prompt-for-vs.md)를 참조하세요.

## <a name="syntax"></a>구문

```console
winres resourceFile
winres /?
```

## <a name="arguments"></a>인수

|인수|설명|
|--------------|-----------------|
|`resourceFile`|지역화할 리소스 파일입니다. 이 파일은 Visual Studio 디자이너에서 생성한 Windows Forms 폼 .resx 또는 .resources 파일이어야 합니다. Winres.exe는 일반 .resx 또는 .resources 파일을 열 수 없습니다.|

|옵션|설명|
|------------|-----------------|
|**/?**|이 도구의 명령 구문 및 옵션을 표시합니다.|

## <a name="remarks"></a>설명

Windows Forms 프로젝트의 폼에 있는 UI 요소의 상태는 일반적으로 리소스 파일에 저장됩니다. 이러한 리소스 파일은 .resx 확장명을 사용하는 XML 기반 파일이거나 .resources 확장명을 사용하는 컴파일된 이진 버전의 파일입니다. Winres.exe는 이러한 두 가지 형식의 파일을 Visual Studio 디자인 환경 외부에서 제한적으로 편집할 수 있는 도구입니다. 특히 이 도구에서는 다음과 같은 종류의 편집 작업을 수행할 수 있습니다.

- 중립 또는 특정 문화권 리소스 파일을 편집하여 폼이나 폼의 컨트롤에서 텍스트, 크기 또는 위치 등의 UI 속성을 변경할 수 있습니다.

- 기본 리소스 파일에서 중립 또는 특정 문화권 리소스 파일을 생성할 수 있습니다.

- 문화권 리소스 파일을 다른 문화권의 리소스 파일로 저장할 수 있습니다. 예를 들어, 영어(미국) 리소스 파일을 폴란드어 리소스 파일로 저장할 수 있습니다. 새 파일을 저장한 다음에는 새 문화권과 호환되도록 편집하는 것이 일반적입니다.

또한 [Hierarchical Organization of Resources for Localization](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2012/756hydy4(v=vs.110))(지역화를 위한 리소스의 계층적 구성) 또는 [Hierarchical Organization of Resources for Localization](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/756hydy4(v=vs.120))(지역화를 위한 리소스의 계층적 구성)을 참조하세요.

Winres.exe로는 .resx 파일을 상응하는 .resources 파일로 변환할 수 없습니다. 이를 위해서는 Resgen.exe 도구를 대신 사용합니다. Resgen.exe에 대한 자세한 내용은 [Resgen.exe(리소스 파일 생성기)](resgen-exe-resource-file-generator.md)를 참조하세요.

Winres.exe는 소스 코드에 액세스하지 않고 리소스 파일만을 사용하여 Windows Forms 폼의 디자인 타임 버전을 다시 만드는 그래픽 애플리케이션입니다. Winres.exe는 Visual Studio의 **Windows Forms 폼 디자이너** 및 **속성** 창을 호스팅합니다. 이러한 기능을 통해 Windows Forms 폼이 포함된 .resources 또는 .resx 파일을 시각적으로 편집할 수 있습니다. 일반적으로 지역화 담당자는 Winres.exe를 사용하여 컨트롤 레이블을 편집하고 컨트롤의 위치 및 크기를 조정함으로써 레이블을 대상 문화권에 적합하게 만듭니다.

Winres.exe가 컨트롤 형식을 확인할 수 없는 경우에는 지역화된 .resx 또는 .resources 파일에 자리 표시자 컨트롤을 만듭니다. 자리 표시자 컨트롤은 Windows Forms 폼에 X 표시된 창으로 나타납니다. X 표시된 창의 크기와 위치는 실제 컨트롤의 크기 및 위치와 일치합니다. 자리 표시자 컨트롤의 사용 가능한 모든 지역화 가능 속성은 **속성** 창에 나타납니다. 자리 표시자 컨트롤에 대한 모든 변경 사항은 실제 컨트롤에 저장됩니다.

## <a name="winresexe-versus-visual-studio"></a>Winres.exe와 Visual Studio 비교

일반적으로 애플리케이션의 Windows Forms 폼을 지역화하기 전에 지역화 도구로 Visual Studio와 Winres.exe 중 어떤 것을 사용할지 결정해야 합니다. 버전 호환성 문제로 인해 사용자가 이러한 도구 사이에 전환하지 못할 수도 있습니다. 버전 호환성에 대해서는 뒷부분에서 설명합니다.

Visual Studio의 장점은 애플리케이션의 개발과 지역화에 모두 사용할 수 있다는 점입니다. 개발이 완료된 후 폼을 지역화하려면 폼의 <xref:System.ComponentModel.LocalizableAttribute>(**속성** 편집기의 **지역화 가능** 속성)를 `true`로 설정하고 **언어** 속성을 원하는 대상 문화권으로 변경합니다. 그런 다음 문자열을 편집하고 해당 문화권의 문자열에 맞게 컨트롤의 위치와 크기를 조정합니다. 지역화된 .resx 파일을 저장하면 Visual Studio는 지역화 가능 속성(대상 문화권에서 변경된 속성)만 파일에 씁니다. 또한 Visual Studio에서는 지역화된 .resx 파일에 대한 위성 어셈블리를 정확한 디렉터리 위치에 자동으로 만듭니다.

Visual Studio는 통합 개발 및 지역화 환경을 제공하지만 타사 지역화 담당자가 지역화를 수행하는 경우에는 Winres.exe가 권장됩니다. Winres.exe는 지역화 도구일 뿐이므로 애플리케이션의 코드와 지역화할 폼을 분명하게 구분할 수 있으며, 이러한 구분은 대형 프로젝트의 관리에 보다 실용적입니다.

## <a name="using-winresexe"></a>Winres.exe 사용

Winres.exe를 사용하여 지역화하려면 먼저 Visual Studio의 **Windows Forms 디자이너** 같은 시각적 디자이너를 사용하여 애플리케이션을 개발해야 합니다. 개발이 완료되면 폼의 <xref:System.ComponentModel.LocalizableAttribute>(**속성 편집기**의 **Localizable** 속성)를 `true`로 설정한 다음, 기본 문화권에 대한 .resx 파일을 타사 지역화 담당자에게 전달합니다. 이 .resx 파일에는 Winres.exe가 원래 폼의 디자인 타임 버전을 다시 만들 때 사용하는 추가 정보가 있습니다.

> [!NOTE]
> Winres.exe에서는 기본 리소스 파일을 편집할 수 없습니다. Winres.exe는 모든 변경된 속성을 지역화된 속성으로 해석하여 대상 문화권 리소스 파일에 저장합니다.

문화권 리소스 파일의 최종 버전은 마지막에 애플리케이션의 지역화된 버전을 만드는 데 사용할 수 있습니다. 자세한 내용은 [데스크톱 앱의 리소스](../resources/index.md)를 참조하세요.

Winres.exe에는 다음 기능과 특징이 있습니다.

- Winres는 SFM(단일 파일 모드) 또는 VSFM(Visual Studio 파일 모드)에서 작동할 수 있습니다. SFM은 폼과 폼의 내용에 대한 완전한 정보가 리소스 파일에 저장되는 레거시 모드입니다. VSFM에서는 문화권 변경 사항만 리소스 파일에 저장됩니다.

- 오류 보고 창은 주 창의 왼쪽 아래에 고정되어 있습니다.

- **서식** 메뉴에서 **바로 가기 키 확인** 명령을 클릭하여 바로 가기 키의 중복 여부를 검사할 수 있습니다.

## <a name="version-compatibility"></a>버전 호환성

사용 중인 .NET Framework와 함께 릴리스된 Winres.exe 버전을 사용해야 합니다. 다음 표에서는 호환 가능한 버전을 보여 줍니다.

|Visual Studio|.NET Framework|Winres.exe|
|-------------------|--------------------|----------------|
|Visual Studio .NET 2002|1.0|1.0|
|Visual Studio .NET 2003|1.1|1.1|
|Visual Studio 2005|2.0|2.0|
|Visual Studio 2008|3.0 및 3.5|3.0 및 3.5|
|Visual Studio 2010|4.0|4.0|
|Visual Studio 2017|4.6|4.6|

> [!NOTE]
> VSFM에는 Visual Studio와 호환 가능하다는 장점이 있지만, 변경된 값만 리소스 파일에 저장하므로 Winres.exe를 사용하려면 현재 리소스 파일의 부모가 동일한 디렉터리에 있어야 합니다. 예를 들어, 독일어(독일) 리소스 파일인 `TestApp.de-DE.resources`를 편집하는 경우에는 기본 리소스 파일인 `TestApp.resx`가 있어야 하며, 중립 문화권 리소스 파일인 `TestApp.de.resources`도 필요할 수 있습니다.

## <a name="examples"></a>예

### <a name="to-localize-a-resx-or-resources-file-associated-with-a-form"></a>폼과 연결된 .resx 또는 .resources 파일을 지역화하려면

1. 개발자 명령 프롬프트에 `winres`를 입력하여 Winres.exe를 실행합니다.

2. 지역화할 폼에 대한 기본 리소스를 열려면 **파일** 메뉴에서 **열기** 명령을 클릭하고 파일로 이동하여 파일을 엽니다.

     또는

     Winres.exe를 시작할 때 열려는 파일을 명령줄에 지정합니다.

     다음 명령은 Winres.exe를 시작하고 `TestApp.resx`와 연결된 폼을 폼 디자이너에 로드합니다.

    ```console
    winres TestApp.resx
    ```

     다음 명령은 Winres.exe를 시작하고 `TestApp.resources`와 연결된 폼을 폼 디자이너에 로드합니다.

    ```console
    winres TestApp.resources
    ```

    > [!NOTE]
    > 편집할 리소스가 있는 폼이 상속된 폼인 경우에는 상속된 폼을 포함하는 어셈블리와 상속하는(파생된) 폼을 포함하는 어셈블리가 모두 GAC(전역 어셈블리 캐시)에 등록되어 있거나 WinRes.exe와 동일한 디렉터리에 있어야 합니다. .NET Framework 구성 요소를 GAC에 설치하는 자세한 내용은 [전역 어셈블리 캐시](../app-domains/gac.md)를 참조하세요.

3. 폼에서 컨트롤을 선택하고 <xref:System.Windows.Forms.Control.Text%2A> 및 기타 속성을 변경하여 지역화된 문화권 및 언어를 반영합니다. 지역화된 텍스트에 맞게 필요한 만큼 컨트롤을 이동하거나 크기를 조정합니다.

4. .resx 또는 .resources 파일의 지역화된 버전을 저장하려면 **저장** 아이콘 또는 **파일** 메뉴에 있는 동일한 명령을 클릭합니다. **문화권 선택** 창이 표시됩니다.

5. 문화권 및 파일 모드를 적절히 선택한 다음 **확인**을 클릭합니다.

   도구는 지역화된 리소스 파일에 대해 런타임에서 예상하는 명명 규칙을 사용하여 파일을 저장합니다. 예를 들어, `TestApp.resources`를 독일어(독일)로 지역화하는 경우 이 도구는 파일을 `TestApp.de-DE.resources`로 저장하고 `TestApp.resx`를 독일어(독일)로 지역화하는 경우 `TestApp.de-DE.resx`로 저장합니다. 리소스 명명 규칙에 대한 자세한 내용은 [리소스 패키지 및 배포](../resources/packaging-and-deploying-resources-in-desktop-apps.md)를 참조하세요. 런타임에서 사용하는 미리 정의된 문화권 이름의 목록은 <xref:System.Globalization.CultureInfo> 클래스를 참조하세요.

## <a name="see-also"></a>참고 항목

- <xref:System.ComponentModel.LocalizableAttribute>
- <xref:System.Globalization.CultureInfo>
- <xref:System.Resources.ResourceManager>
- <xref:System.Resources.ResourceReader>
- <xref:System.Resources.ResourceWriter>
- [도구](index.md)
- [데스크톱 앱의 리소스](../resources/index.md)
- [전역화 및 지역화](../../standard/globalization-localization/index.md)
