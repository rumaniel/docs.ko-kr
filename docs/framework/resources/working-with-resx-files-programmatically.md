---
title: 프로그래밍 방식으로 .resx 파일 작업
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- resource files, .resx files
- .resx files
ms.assetid: 168f941a-2b84-43f8-933f-cf4a8548d824
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7e5a57664c5d86ebf394ce026608be9a55872eb8
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71045542"
---
# <a name="working-with-resx-files-programmatically"></a>프로그래밍 방식으로 .resx 파일 작업
XML 리소스 파일(.resx)이 이름/값 쌍의 데이터가 뒤에 오는 특정 스키마를 따라야 하는 헤더를 비롯한 잘 정의된 XML로 구성되어야 하기 때문에 이러한 파일을 수동으로 만드는 경우 오류가 발생하기 쉽습니다. 또는 .NET 클래스 라이브러리의 형식 및 멤버를 사용하여 프로그래밍 방식으로 .resx 파일을 만들 수 있습니다. .NET 클래스 라이브러리를 사용하여 .resx 파일에 저장된 리소스를 가져올 수도 있습니다. 이 항목에서는 <xref:System.Resources> 네임스페이스의 형식 및 멤버를 사용하여 .resx 파일로 작업하는 방법에 대해 설명합니다.

 이 문서에서는 리소스를 포함하는 XML 파일(.resx)로 작업하는 방법을 설명합니다. 어셈블리에 포함된 이진 리소스 파일로 작업하는 방법에 대한 자세한 내용은 <xref:System.Resources.ResourceManager> 항목을 참조하세요.

> [!WARNING]
> 프로그래밍 방식 이외의 방법을 통해 .resx 파일로 작업할 수도 있습니다. 리소스 파일을 [Visual Studio](https://visualstudio.microsoft.com/vs/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link) 프로젝트에 추가하면 Visual Studio에서는 .resx 파일을 만들고 유지 관리하기 위한 인터페이스를 제공하고 컴파일 시간에 자동으로 .resx 파일을 .resources 파일로 변환합니다. 텍스트 편집기를 사용하여 .resx 파일을 직접 조작할 수도 있습니다. 그러나 파일이 손상되지 않도록 파일에 저장된 이진 정보를 수정하지 않아야 합니다.

## <a name="create-a-resx-file"></a>.resx 파일 만들기

다음 단계에 따라 <xref:System.Resources.ResXResourceWriter?displayProperty=nameWithType> 클래스를 사용하여 프로그래밍 방식으로 .resx 파일을 만들 수 있습니다.

1. <xref:System.Resources.ResXResourceWriter> 메서드를 호출하고 .resx 파일의 이름을 제공하여 <xref:System.Resources.ResXResourceWriter.%23ctor%28System.String%29?displayProperty=nameWithType> 개체를 인스턴스화합니다. 파일 이름에는 .resx 확장명이 포함되어야 합니다. <xref:System.Resources.ResXResourceWriter> 블록에서 `using` 개체를 인스턴스화하는 경우 3단계에서 <xref:System.Resources.ResXResourceWriter.Close%2A?displayProperty=nameWithType> 메서드를 명시적으로 호출할 필요가 없습니다.

2. 파일에 추가할 각 리소스에 대해 <xref:System.Resources.ResXResourceWriter.AddResource%2A?displayProperty=nameWithType> 메서드를 호출합니다. 이 메서드의 오버로드를 사용하여 문자열, 개체 및 이진 데이터(바이트 배열)를 추가합니다. 리소스가 개체이면 serialize 가능해야 합니다.

3. <xref:System.Resources.ResXResourceWriter.Close%2A?displayProperty=nameWithType> 메서드를 호출하여 리소스 파일을 생성하고 모든 리소스를 해제합니다. <xref:System.Resources.ResXResourceWriter> 개체가 `using` 블록 내에서 만들어진 경우 리소스가 .resx 파일에 기록되고 <xref:System.Resources.ResXResourceWriter> 개체에서 사용되는 리소스가 `using` 블록 끝에서 해제됩니다.

생성되는 .resx 파일에는 적절한 헤더와 `data` 메서드에서 추가된 각 리소스에 대한 <xref:System.Resources.ResXResourceWriter.AddResource%2A?displayProperty=nameWithType> 태그가 있습니다.

> [!WARNING]
> 암호, 보안이 중요한 정보 또는 개인 데이터를 저장할 때는 리소스 파일을 사용하지 마세요.

다음 예제에서는 문자열 6개, 아이콘 한 개 및 애플리케이션 정의 개체 2개( `Automobile` 개체 2개)를 저장하는 CarResources.resx라는 .resx 파일을 만듭니다. 이 예제에서 정의되고 인스턴스화된 `Automobile` 클래스는 <xref:System.SerializableAttribute> 특성으로 태그가 지정됩니다.

[!code-csharp[Conceptual.Resources.ResX#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.resx/cs/create1.cs#1)]
[!code-vb[Conceptual.Resources.ResX#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.resx/vb/create1.vb#1)]

> [!TIP]
> [Visual Studio](https://visualstudio.microsoft.com/vs/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link)를 사용하여 .resx 파일을 만들 수도 있습니다. 컴파일 타임에 Visual Studio에서는 [리소스 파일 생성기 (Resgen.exe)](../tools/resgen-exe-resource-file-generator.md) 를 사용하여 .resx 파일을 이진 리소스 파일(.resources)로 변환하고 애플리케이션 어셈블리나 위성 어셈블리에도 포함합니다.

.resx 파일은 런타임 실행 파일에 포함하거나 위성 어셈블리로 컴파일할 수 없습니다. [리소스 파일 생성기 (Resgen.exe)](../tools/resgen-exe-resource-file-generator.md)를 사용하여 .resx 파일을 이진 리소스 파일(.resources)로 변환해야 합니다. 생성되는 .resources 파일은 애플리케이션 어셈블리나 위성 어셈블리에 포함될 수 있습니다. 자세한 내용은 [Creating Resource Files](creating-resource-files-for-desktop-apps.md)을 참조하세요.

## <a name="enumerate-resources"></a>리소스 열거
 경우에 따라 .resx 파일에서 특정 리소스 대신 모든 리소스를 검색할 수 있습니다. 이렇게 하려면 .resx 파일의 모든 리소스에 대한 열거자를 제공하는 <xref:System.Resources.ResXResourceReader?displayProperty=nameWithType> 클래스를 사용하면 됩니다. <xref:System.Resources.ResXResourceReader?displayProperty=nameWithType> 클래스는 루프의 각 반복에 대한 특정 리소스를 나타내는 <xref:System.Collections.IDictionaryEnumerator>개체를 반환하는 <xref:System.Collections.DictionaryEntry> 를 구현합니다. <xref:System.Collections.DictionaryEntry.Key%2A?displayProperty=nameWithType> 속성은 리소스의 키를 반환하고, <xref:System.Collections.DictionaryEntry.Value%2A?displayProperty=nameWithType> 속성은 리소스의 값을 반환합니다.

 다음 예제에서는 이전 예제에서 만들어진 CarResources.resx 파일에 대한 <xref:System.Resources.ResXResourceReader> 개체를 만들고 리소스 파일을 반복합니다. 이 예제에서는 리소스 파일에 정의된 두 `Automobile` 개체를 <xref:System.Collections.Generic.List%601?displayProperty=nameWithType> 개체에 추가하고 문자열 6개 중 5개를 <xref:System.Collections.SortedList> 개체에 추가합니다. <xref:System.Collections.SortedList> 개체의 값은 열 머리글을 콘솔에 표시하는 데 사용되는 매개 변수 배열로 변환됩니다. `Automobile` 속성 값도 콘솔에 표시됩니다.

 [!code-csharp[Conceptual.Resources.ResX#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.resx/cs/enumerate1.cs#2)]
 [!code-vb[Conceptual.Resources.ResX#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.resx/vb/enumerate1.vb#2)]

## <a name="retrieve-a-specific-resource"></a>특정 리소스 가져오기
 .resx 파일의 항목을 열거할 수 있을 뿐만 아니라 <xref:System.Resources.ResXResourceSet?displayProperty=nameWithType> 클래스를 사용하여 이름별로 특정 리소스를 검색할 수 있습니다. <xref:System.Resources.ResourceSet.GetString%28System.String%29?displayProperty=nameWithType> 메서드는 명명된 문자열 리소스의 값을 검색합니다. <xref:System.Resources.ResourceSet.GetObject%28System.String%29?displayProperty=nameWithType> 메서드는 명명된 개체 또는 이진 데이터의 값을 검색합니다. 이 메서드는 올바른 형식의 개체로 캐스팅(C#의 경우)되거나 변환(Visual Basic의 경우)되어야 하는 개체를 반환합니다.

 다음 예제에서는 리소스 이름별로 폼의 캡션 문자열과 아이콘을 검색합니다. 또한 이전 예제에서 사용된 애플리케이션 정의 `Automobile` 개체를 검색하고 <xref:System.Windows.Forms.DataGridView> 컨트롤에 표시합니다.

 [!code-csharp[Conceptual.Resources.ResX#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.resx/cs/retrieve1.cs#3)]
 [!code-vb[Conceptual.Resources.ResX#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.resx/vb/retrieve1.vb#3)]

## <a name="convert-resx-files-to-binary-resources-files"></a>.resx 파일을 이진 .resources 파일로 변환
 .resx 파일을 포함된 이진 리소스 파일(.resources)로 변환하면 상당한 이점이 있습니다. .resx 파일은 애플리케이션 개발 중에 쉽게 읽고 유지 관리할 수 있지만 완성된 애플리케이션에 포함되는 경우는 드뭅니다. .resx 파일이 애플리케이션과 함께 배포되는 경우 애플리케이션 실행 파일 및 함께 제공된 라이브러리와는 별도의 파일로 존재합니다. 반면에 .resources 파일은 애플리케이션 실행 파일이나 함께 제공된 어셈블리에 포함됩니다. 또한 지역화된 애플리케이션의 경우 런타임에 .resx 파일을 사용하려면 개발자가 리소스 대체를 처리해야 합니다. 반면에 포함된 .resources 파일을 포함하는 위성 어셈블리의 집합이 만들어진 경우 공용 언어 런타임에서 리소스 대체 프로세스를 처리합니다.

 .resx 파일을 .resources 파일로 변환하려면 다음 기본 구문을 사용하는 [리소스 파일 생성기 (Resgen.exe)](../tools/resgen-exe-resource-file-generator.md)를 사용합니다.

 **Resgen.exe** *.resxFilename*

 결과는 .resx 파일 및 .resources 파일 확장과 동일한 루트 파일 이름이 있는 이진 리소스 파일입니다. 이 파일은 컴파일 시간에 실행 파일이나 라이브러리로 컴파일될 수 있습니다. Visual Basic 컴파일러를 사용하는 경우 다음 구문을 사용하여 .resources 파일을 애플리케이션의 실행 파일에 포함합니다.

 **vbc** *filename* **.vb -resource:** *.resourcesFilename*

 C#을 사용하는 경우 구문은 다음과 같습니다.

 **csc** *filename* **.cs -resource:** *.resourcesFilename*

 다음 기본 구문을 사용하는 [어셈블리 링커(AL.exe)](../tools/al-exe-assembly-linker.md)를 사용하여 .resources 파일을 위성 어셈블리에 포함할 수도 있습니다.

 **al** *resourcesFilename* **-out:** *assemblyFilename*

## <a name="see-also"></a>참고 항목

- [리소스 파일 만들기](creating-resource-files-for-desktop-apps.md)
- [Resgen.exe(리소스 파일 생성기)](../tools/resgen-exe-resource-file-generator.md)
- [Al.exe(어셈블리 링커)](../tools/al-exe-assembly-linker.md)
