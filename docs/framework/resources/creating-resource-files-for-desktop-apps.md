---
title: .NET 앱의 리소스 파일 만들기
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- resource files, .resources files
- .resources files
- application resources, creating files
- resource files, creating
ms.assetid: 6c5ad891-66a0-4e7a-adcf-f41863ba6d8d
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 893b6e6e61e23bdc0da1902407017a836bc6cbe8
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71045677"
---
# <a name="create-resource-files-for-net-apps"></a>.NET 앱의 리소스 파일 만들기

문자열, 이미지 또는 개체 데이터와 같은 리소스를 리소스 파일에 포함하여 애플리케이션에서 쉽게 사용할 수 있게 설정할 수 있습니다. .NET Framework에서는 리소스 파일을 만드는 다섯 가지 방법을 제공합니다.

- 문자열 리소스가 포함된 텍스트 파일을 만듭니다. [리소스 파일 생성기(Resgen.exe)](../tools/resgen-exe-resource-file-generator.md)를 사용하여 텍스트 파일을 이진 리소스(.resources) 파일로 변환할 수 있습니다. 그다음에 언어 컴파일러를 사용하여 이진 리소스 파일을 애플리케이션 실행 파일 또는 애플리케이션 라이브러리에 포함하거나, [어셈블리 링커(Al.exe)](../tools/al-exe-assembly-linker.md)를 사용하여 위성 어셈블리에 포함할 수 있습니다. 자세한 내용은 [텍스트 파일의 리소스](creating-resource-files-for-desktop-apps.md#TextFiles) 섹션을 참조하세요.

- 문자열, 이미지 또는 개체 데이터가 포함된 XML 리소스(.resx) 파일을 만듭니다. [리소스 파일 생성기(Resgen.exe)](../tools/resgen-exe-resource-file-generator.md)를 사용하여 .resx 파일을 이진 리소스(.resources) 파일로 변환할 수 있습니다. 그다음에 언어 컴파일러를 사용하여 이진 리소스 파일을 애플리케이션 실행 파일 또는 애플리케이션 라이브러리에 포함하거나, [어셈블리 링커(Al.exe)](../tools/al-exe-assembly-linker.md)를 사용하여 위성 어셈블리에 포함할 수 있습니다. 자세한 내용은 [.resx 파일의 리소스](creating-resource-files-for-desktop-apps.md#ResxFiles) 섹션을 참조하세요.

- <xref:System.Resources> 네임스페이스의 형식을 사용하여 프로그래밍 방식으로 XML 리소스(.resx) 파일을 만듭니다. .resx 파일을 만들고, 해당 리소스를 열거하고, 특정 리소스를 이름으로 검색할 수 있습니다. 자세한 내용은 [프로그래밍 방식으로 .resx 파일 작업](working-with-resx-files-programmatically.md) 항목을 참조하세요.

- 프로그래밍 방식으로 이진 리소스(.resources) 파일을 만듭니다. 그다음에 언어 컴파일러를 사용하여 파일을 애플리케이션 실행 파일 또는 애플리케이션 라이브러리에 포함하거나, [어셈블리 링커(Al.exe)](../tools/al-exe-assembly-linker.md)를 사용하여 위성 어셈블리에 포함할 수 있습니다. 자세한 내용은 [.resources 파일의 리소스](creating-resource-files-for-desktop-apps.md#ResourcesFiles) 섹션을 참조하세요.

- [Visual Studio](https://visualstudio.microsoft.com/vs/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link)를 사용하여 리소스 파일을 만들고 프로젝트에 포함합니다. Visual Studio에서는 리소스를 추가, 삭제 및 수정할 수 있는 리소스 편집기를 제공합니다. 컴파일 시간에 리소스 파일은 자동으로 이진 .resources 파일로 변환되고 애플리케이션 어셈블리 또는 위성 어셈블리에 포함됩니다. 자세한 내용은 [Visual Studio의 리소스 파일](creating-resource-files-for-desktop-apps.md#VSResFiles) 섹션을 참조하세요.

<a name="TextFiles"></a>
## <a name="resources-in-text-files"></a>텍스트 파일의 리소스

텍스트 파일(.txt 또는 .restext)을 사용하면 문자열 리소스만 저장할 수 있습니다. 문자열이 아닌 리소스의 경우 .resx 파일을 사용하거나 프로그래밍 방식으로 .resx 파일을 만듭니다. 문자열 리소스가 포함된 텍스트 파일의 형식은 다음과 같습니다.

```text
# This is an optional comment.
name = value

; This is another optional comment.
name = value

; The following supports conditional compilation if X is defined.
#ifdef X
name1=value1
name2=value2
#endif

# The following supports conditional compilation if Y is undefined.
#if !Y
name1=value1
name2=value2
#endif
```

 .txt 및 .restext 파일의 리소스 파일 형식은 같습니다. .restext 파일 확장명은 단순히 텍스트 파일을 텍스트 기반 리소스 파일로 즉시 식별할 수 있도록 합니다.

 문자열 리소스는 *name/value* 쌍으로 나타납니다. 여기서 *name*은 리소스를 식별하는 문자열이고, *value*는 *name*을 <xref:System.Resources.ResourceManager.GetString%2A?displayProperty=nameWithType>과 같은 리소스 검색 메서드에 전달할 때 반환되는 리소스 문자열입니다. *name* 및 *value*는 등호(=)로 구분해야 합니다. 예:

```text
FileMenuName=File
EditMenuName=Edit
ViewMenuName=View
HelpMenuName=Help
```

> [!CAUTION]
> 암호, 보안이 중요한 정보 또는 개인 데이터를 저장할 때는 리소스 파일을 사용하지 마세요.

 빈 문자열(즉, <xref:System.String.Empty?displayProperty=nameWithType> 값을 가진 리소스)은 텍스트 파일에 사용할 수 있습니다. 예:

```text
EmptyString=
```

 .NET Framework 4.5부터, 그리고 모든 버전의 .NET Core에서, 텍스트 파일에서는 `#ifdef`*symbol*... `#endif` 및 `#if !`*symbol*... `#endif` 구문을 사용한 조건부 컴파일을 지원합니다. 그런 다음 [리소스 파일 생성기(Resgen.exe)](../tools/resgen-exe-resource-file-generator.md)와 함께 `/define` 스위치를 하여 기호를 정의할 수 있습니다. 각 리소스에는 고유한 `#ifdef`*symbol*... `#endif` 또는 `#if !`*symbol*... `#endif` 구문이 필요합니다. `#ifdef` 문을 사용하고 *symbol*을 정의하면 연관된 리소스는 .resources 파일에 포함되고, 그렇지 않을 경우 포함되지 않습니다. `#if !` 문을 사용하고 *symbol*을 정의하지 않으면 연관된 리소스는 .resources 파일에 포함되고, 그렇지 않을 경우 포함되지 않습니다.

 텍스트 파일에서 주석은 선택 사항이고 줄 시작 부분에서 세미콜론(;) 또는 파운드 기호(#) 뒤에 옵니다. 주석이 포함된 줄은 파일의 어느 곳에나 배치될 수 있습니다. 주석은 [리소스 파일 생성기(Resgen.exe)](../tools/resgen-exe-resource-file-generator.md)를 사용하여 만든 컴파일된 .resources 파일에 포함되지 않습니다.

 텍스트 파일에 있는 빈 줄은 공백으로 간주하고 무시됩니다.

 다음 예제에서는 `OKButton` 및 `CancelButton`이라는 두 개의 문자열 리소스를 정의합니다.

```text
#Define resources for buttons in the user interface.
OKButton=OK
CancelButton=Cancel
```

 텍스트 파일에 중복된 *name*이 포함된 경우 [리소스 파일 생성기(Resgen.exe)](../tools/resgen-exe-resource-file-generator.md)는 경고를 표시하고 두 번째 이름을 무시합니다.

 *value*에는 줄 바꿈 문자가 포함될 수 없지만 `\n` 같은 C 언어 스타일의 이스케이프 문자를 사용하여 새 줄을 나타내고 `\t`를 사용하여 탭을 나타낼 수 있습니다. 이스케이프된 경우 백슬래시 문자를 포함할 수도 있습니다(예: "\\\\"). 또한 빈 문자열이 허용됩니다.

 little-endian 또는 big-endian 바이트 순서의 UTF-8 인코딩이나 UTF-16 인코딩을 사용하여 텍스트 파일 형식으로 리소스를 저장해야 합니다. 하지만 .txt 파일을 .resources 파일로 변환하는 [리소스 파일 생성기(Resgen.exe)](../tools/resgen-exe-resource-file-generator.md)는 기본적으로 파일을 UTF-8로 처리합니다. Resgen.exe가 UTF-16을 사용하여 인코딩된 파일을 인식하게 하려면 파일 시작 부분에 유니코드 바이트 순서 표시(U+FEFF)를 포함해야 합니다.

 텍스트 형식의 리소스 파일을 .NET 어셈블리에 포함하려면 [리소스 파일 생성기(Resgen.exe)](../tools/resgen-exe-resource-file-generator.md)를 사용하여 파일을 이진 리소스(.resources) 파일로 변환해야 합니다. 그런 다음, 언어 컴파일러를 사용하여 .resources 파일을 .NET 어셈블리에 포함하거나, [어셈블리 링커(Al.exe)](../tools/al-exe-assembly-linker.md)를 사용하여 위성 어셈블리에 포함할 수 있습니다.

 다음 예제에서는 간단한 "Hello World" 콘솔 애플리케이션에 GreetingResources.txt라는 텍스트 형식의 리소스 파일을 사용합니다. 텍스트 파일은 사용자에게 이름을 입력하도록 메시지를 표시하고 인사말을 표시하는 두 개의 문자열인 `prompt` 및 `greeting`을 정의합니다.

```text
# GreetingResources.txt
# A resource file in text format for a "Hello World" application.
#
# Initial prompt to the user.
prompt=Enter your name:
# Format string to display the result.
greeting=Hello, {0}!
```

텍스트 파일은 다음 명령을 사용하여 .resources 파일로 변환됩니다.

```console
resgen GreetingResources.txt
```

 다음 예제에서는 .resources 파일을 사용하여 사용자에게 메시지를 표시하는 콘솔 애플리케이션에 대한 소스 코드를 보여 줍니다.

 [!code-csharp[Conceptual.Resources.TextFiles#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.textfiles/cs/greeting.cs#1)]
 [!code-vb[Conceptual.Resources.TextFiles#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.textfiles/vb/greeting.vb#1)]

 Visual Basic을 사용하고 있고 소스 코드 파일 이름이 Greeting.vb라면 다음 명령은 포함된 .resources 파일을 포함하는 실행 파일을 만듭니다.

```console
vbc greeting.vb -resource:GreetingResources.resources
```

 C#을 사용하고 있고 소스 코드 파일 이름이 Greeting.cs라면 다음 명령은 포함된 .resources 파일을 포함하는 실행 파일을 만듭니다.

```console
csc greeting.cs -resource:GreetingResources.resources
```

<a name="ResxFiles"></a>
## <a name="resources-in-resx-files"></a>.resx 파일의 리소스
 문자열 리소스만 저장할 수 있는 텍스트 파일과 달리 XML 리소스(.resx) 파일은 문자열, 이진 데이터(예: 이미지, 아이콘, 오디오 클립) 및 프로그래밍 개체를 저장할 수 있습니다. .resx 파일에는 리소스 항목의 형식을 설명하고 데이터 구문 분석에 사용되는 XML에 대한 버전 관리 정보를 지정하는 표준 헤더가 포함됩니다. 리소스 파일 데이터는 XML 헤더를 따릅니다. 각 데이터 항목은 `data` 태그에 포함된 이름/값 쌍으로 구성됩니다. 해당 `name` 특성은 리소스 이름을 정의하고 중첩된 `value` 태그에는 리소스 값이 포함됩니다. 문자열 데이터의 경우 `value` 태그에 문자열이 포함됩니다.

 예를 들어 다음 `data` 태그는 값이 “Enter your name:”인 `prompt`라는 문자열 리소스를 정의합니다.

```xml
<data name="prompt" xml:space="preserve">
  <value>Enter your name:</value>
</data>
```

> [!WARNING]
> 암호, 보안이 중요한 정보 또는 개인 데이터를 저장할 때는 리소스 파일을 사용하지 마세요.

 리소스 개체의 경우 **data** 태그에는 리소스의 데이터 형식을 나타내는 `type` 특성이 포함됩니다. 이진 데이터로 구성된 개체의 경우 `data` 태그에는 이진 데이터의 `base64` 형식을 나타내는 `mimetype` 특성도 포함됩니다.

> [!NOTE]
> 모든 .resx 파일에는 이진 serialization 포맷터를 사용하여 지정된 형식의 이진 데이터를 생성하고 구문 분석합니다. 따라서 개체에 대한 이진 serialization 형식이 호환되지 않는 방식으로 변경될 경우 .resx 파일이 유효하지 않을 수 있습니다.

 다음 예제에서는 <xref:System.Int32> 리소스 및 비트맵 이미지를 포함하는 .resx 파일의 일부가 포함됩니다.

```xml
<data name="i1" type="System.Int32, mscorlib">
  <value>20</value>
</data>

<data name="flag" type="System.Drawing.Bitmap, System.Drawing,
    Version=1.0.5000.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a"
    mimetype="application/x-microsoft.net.object.bytearray.base64">
  <value>
    AAEAAAD/////AQAAAAAAAAAMAgAAADtTeX…
  </value>
</data>
```

> [!IMPORTANT]
> .resx 파일은 미리 정의된 형식의 잘 구성된(Well-Formed) XML로 구성되어야 하므로, 특히 .resx 파일에 문자열 이외의 리소스가 포함된 경우에는 .resx 파일을 수동으로 사용하지 않는 것이 좋습니다. 대신, [Visual Studio](https://visualstudio.microsoft.com/vs/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link)에서는 .resx 파일을 만들고 조작할 수 있는 투명한 인터페이스가 제공됩니다. 자세한 내용은 [Visual Studio의 리소스 파일](creating-resource-files-for-desktop-apps.md#VSResFiles) 섹션을 참조하세요. 프로그래밍 방식으로 .resx 파일을 만들고 조작할 수도 있습니다. 자세한 내용은 [프로그래밍 방식으로 .resx 파일 작업](working-with-resx-files-programmatically.md)을 참조하세요.

<a name="ResourcesFiles"></a>
## <a name="resources-in-resources-files"></a>.resources 파일의 리소스

<xref:System.Resources.ResourceWriter?displayProperty=nameWithType> 클래스를 사용하여 프로그래밍 방식으로 코드에서 직접 이진 리소스(.resources) 파일을 만들 수 있습니다. [리소스 파일 생성기(Resgen.exe)](../tools/resgen-exe-resource-file-generator.md)를 사용하여 텍스트 파일 또는 .resx 파일에서 .resources 파일을 만들 수도 있습니다. .resources 파일에는 문자열 데이터 외에 이진 데이터(바이트 배열) 및 개체 데이터가 포함될 수 있습니다. 프로그래밍 방식으로 .resources 파일을 만들려면 다음 단계가 필요합니다.

1. 고유한 파일 이름을 사용하여 <xref:System.Resources.ResourceWriter> 개체를 만듭니다. 파일 이름 또는 파일 스트림을 <xref:System.Resources.ResourceWriter> 클래스 생성자로 지정하여 이 작업을 수행할 수 있습니다.

2. 파일에 추가할 각 명명된 리소스에 대해 <xref:System.Resources.ResourceWriter.AddResource%2A?displayProperty=nameWithType> 메서드의 오버로드 중 하나를 호출합니다. 리소스는 문자열, 개체 또는 이진 데이터 컬렉션(바이트 배열)일 수 있습니다.

3. <xref:System.Resources.ResourceWriter.Close%2A?displayProperty=nameWithType> 메서드를 호출하여 리소스를 파일에 쓰고 <xref:System.Resources.ResourceWriter> 개체를 닫습니다.

> [!NOTE]
> 암호, 보안이 중요한 정보 또는 개인 데이터를 저장할 때는 리소스 파일을 사용하지 마세요.

 다음 예제에서는 문자열 6개, 아이콘 한 개 및 애플리케이션 정의 개체 2개(`Automobile` 개체 2개)를 저장하는 CarResources.resources라는 .resources 파일을 프로그래밍 방식으로 만듭니다. 이 예제에서 정의되고 인스턴스화된 `Automobile` 클래스는 <xref:System.SerializableAttribute> 특성으로 태그가 지정되어 이진 serialization 포맷터를 통해 유지될 수 있습니다.

 [!code-csharp[Conceptual.Resources.Resources#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.resources/cs/resources1.cs#1)]
 [!code-vb[Conceptual.Resources.Resources#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.resources/vb/resources1.vb#1)]

 .resources 파일을 만든 후 언어 컴파일러의 `/resource` 스위치를 포함하여 런타임 실행 파일 또는 라이브러리에 포함하거나, [어셈블리 링커(Al.exe)](../tools/al-exe-assembly-linker.md)를 사용하여 위성 어셈블리에 포함할 수 있습니다.

<a name="VSResFiles"></a>
## <a name="resource-files-in-visual-studio"></a>Visual Studio의 리소스 파일

[Visual Studio](https://visualstudio.microsoft.com/vs/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link) 프로젝트에 리소스 파일을 추가하면 Visual Studio에서는 프로젝트 디렉터리에 .resx 파일을 만듭니다. Visual Studio에서는 문자열, 이미지 및 이진 개체를 추가할 수 있는 리소스 편집기를 제공합니다. 편집기는 정적 데이터만 처리하도록 디자인되어 있으므로 프로그래밍 개체를 저장하는 데는 사용할 수 없습니다. 프로그래밍 방식으로 개체 데이터를 .resx 파일 또는 .resources 파일에 써야 합니다. 자세한 내용은 [프로그래밍 방식으로 .resx 파일 작업](working-with-resx-files-programmatically.md) 섹션과 [.resources 파일의 리소스](creating-resource-files-for-desktop-apps.md#ResourcesFiles) 섹션을 참조하세요.

지역화된 리소스를 추가할 경우 기본 리소스 파일과 같은 루트 파일 이름을 리소스에 지정해야 합니다. 파일 이름에서 문화권도 지정해야 합니다. 예를 들어 Resources.resx 리소스 파일을 추가할 경우 Resources.en-US.resx 및 Resources.fr-FR.resx 리소스 파일을 만들어 각각 영어(미국) 및 프랑스어(프랑스) 문화권에 대한 지역화된 리소스를 저장할 수도 있습니다. 애플리케이션의 기본 문화권도 지정해야 합니다. 이 문화권의 리소스는 특정 문화권에 대한 지역화된 리소스를 찾을 수 없는 경우 사용됩니다. 기본 문화권을 지정하려면 Visual Studio의 솔루션 탐색기에서 애플리케이션을 가리키고, **어셈블리 정보**를 클릭하고, **중립 언어** 목록에서 적절한 언어/문화권을 선택합니다.

컴파일 시간에 Visual Studio에서는 먼저 프로젝트의 .resx 파일을 이진 리소스(.resources) 파일로 변환하고 프로젝트 *obj* 디렉터리의 하위 디렉터리에 저장합니다. Visual Studio에서는 지역화된 리소스가 포함되지 않은 모든 리소스 파일을 프로젝트에서 생성된 주 어셈블리에 포함합니다. 리소스 파일에 지역화된 리소스가 포함된 경우 Visual Studio에서는 각 지역화된 문화권에 대한 개별 위성 어셈블리에 리소스 파일을 포함합니다. 그런 다음, 각 위성 어셈블리를 이름이 지역화된 문화권과 일치하는 디렉터리에 저장합니다. 예를 들어 지역화된 영어(미국) 리소스는 en-US 하위 디렉터리의 위성 어셈블리에 저장됩니다.

## <a name="see-also"></a>참고 항목

- <xref:System.Resources>
- [데스크톱 앱의 리소스](index.md)
- [리소스 패키징 및 배포](packaging-and-deploying-resources-in-desktop-apps.md)
