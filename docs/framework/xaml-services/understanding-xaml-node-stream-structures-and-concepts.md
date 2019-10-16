---
title: XAML 노드 스트림 구조 및 개념 이해
ms.date: 03/30/2017
helpviewer_keywords:
- XAML node streams [XAML Services]
- nodes [XAML Services], XAML node stream
- XAML [XAML Services], XAML node streams
ms.assetid: 7c11abec-1075-474c-9d9b-778e5dab21c3
ms.openlocfilehash: d6b2975b8e0338b121d00f5ec7f4ffb69d32ab6a
ms.sourcegitcommit: 093571de904fc7979e85ef3c048547d0accb1d8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "70400731"
---
# <a name="understanding-xaml-node-stream-structures-and-concepts"></a>XAML 노드 스트림 구조 및 개념 이해

.NET Framework XAML 서비스에 구현된 XAML 판독기와 XAML 작성기는 XAML 노드 스트림의 디자인 개념을 기반으로 합니다. XAML 노드 스트림은 XAML 노드 집합의 개념화입니다. 이 개념화에서 XAML 프로세서는 한 번에 하나씩 XAML의 노드 관계 구조를 처리합니다. 언제든지 하나의 현재 레코드 또는 현재 위치만 열린 XAML 노드 스트림에 있으며 API는 대부분 해당 위치에서 사용할 수 있는 정보만 보고합니다. XAML 노드 스트림의 현재 노드는 개체, 멤버 또는 값으로 설명될 수 있습니다. XAML을 XAML 노드 스트림으로 처리하여 XAML 판독기는 XAML 작성기와 통신하고 XAML을 포함하는 경로 로드 또는 경로 저장 작업 중에 프로그램이 XAML 노드 스트림을 보거나, 상호 작용하거나, 콘텐츠를 변경할 수 있게 할 수 있습니다. XAML 판독기/작성기 API 디자인 및 XAML 노드 스트림 개념은 이전의 관련된 판독기/작성기 디자인 및 개념과 비슷합니다(예: [!INCLUDE[TLA#tla_xmldom](../../../includes/tlasharptla-xmldom-md.md)] , <xref:System.Xml.XmlReader> 및 <xref:System.Xml.XmlWriter> 클래스). 이 항목에서는 XAML 노드 스트림 개념과 XAML 노드 수준에서 XAML 표현과 상호 작용하는 루틴을 작성하는 방법을 설명합니다.

<a name="loading_into_a_xaml_reader"></a>

## <a name="loading-xaml-into-a-xaml-reader"></a>XAML 판독기에 XAML 로드

기본 <xref:System.Xaml.XamlReader> 클래스는 XAML 판독기에 초기 XAML을 로드하기 위한 특정 기술을 선언하지 않습니다. 대신, 파생 클래스가 XAML에 대한 입력 소스의 일반적인 특징 및 제약 조건을 포함하여 로드 기술을 선언하고 구현합니다. 예를 들어 <xref:System.Xaml.XamlObjectReader> 는 루트 또는 기준을 나타내는 단일 개체의 입력 소스부터 시작하여 개체 그래프를 읽습니다. 그런 다음 <xref:System.Xaml.XamlObjectReader> 는 개체 그래프에서 XAML 노드 스트림을 생성합니다.

.NET Framework XAML 서비스에서 정의된 가장 두드러진 <xref:System.Xaml.XamlReader> 하위 클래스는 <xref:System.Xaml.XamlXmlReader>입니다. <xref:System.Xaml.XamlXmlReader> 는 스트림 또는 파일 경로를 통해 직접적으로 또는 관련된 판독기 클래스(예: <xref:System.IO.TextReader>)를 통해 간접적으로 텍스트 파일을 로드하여 초기 XAML을 로드합니다. <xref:System.Xaml.XamlReader> 를 로드 후 전체 XAML 입력 소스를 포함하는 것으로 생각할 수 있습니다. 그러나 <xref:System.Xaml.XamlReader> 기본 API는 판독기가 XAML의 단일 노드와 상호 작용하도록 설계되었습니다. 처음 로드할 때 발견되는 첫 번째 단일 노드는 XAML 루트 및 해당 시작 개체입니다.

### <a name="the-xaml-node-stream-concept"></a>XAML 노드 스트림 개념

일반적으로 DOM, 트리 메타포 또는 XML 기반 기술에 액세스하는 쿼리 기반 접근 방식에 더 익숙한 경우 XAML 노드 스트림을 개념화하는 데 유용한 방법은 다음과 같습니다. 로드된 XAML이 가능한 모든 노드가 전체 확장된 다음 선형적으로 표시되는 트리 또는 DOM이라고 가정합니다. 노드를 탐색할 때 DOM과 관련된 수준을 "진입" 또는 "진출"할 수 있지만 이러한 수준 개념은 노드 스트림과 관련이 없기 때문에 XAML 노드 스트림에서 명시적으로 추적하지 않습니다. 노드 스트림에는 "현재" 위치가 있지만 스트림 자체의 다른 부분을 참조로 저장하지 않은 한 현재 노드 위치를 제외한 노드 스트림의 다른 모든 측면은 표시되지 않습니다.

XAML 노드 스트림 개념에는 전체 노드 스트림을 통과할 경우 전체 XAML 표현을 처리했음을 확신할 수 있다는 장점이 있습니다. 쿼리, DOM 작업 또는 정보 처리에 대한 기타 비선형 접근 방식이 전체 XAML 표현의 일부분에서 누락되지 않았는지 걱정할 필요가 없습니다. 이러한 이유로, XAML 노드 스트림 표현은 XAML 판독기와 XAML 작성기를 연결하고 XAML 처리 작업의 읽기 및 쓰기 단계 사이에 작동하는 고유한 프로세스를 삽입할 수 있는 시스템을 제공하는 데 적합합니다. 대부분의 경우 XAML 노드 스트림의 노드 순서는 XAML 판독기에 의해 의도적으로 소스 텍스트, 이진 또는 개체 그래프에 표시될 수 있는 순서와 반대로 최적화되거나 다시 정렬됩니다. 이 동작은 XAML 작성기가 노드 스트림에서 "뒤로" 이동해야 하는 위치에 있지 않도록 하는 XAML 처리 아키텍처를 적용하기 위한 것입니다. 이상적일 경우, 모든 XAML 쓰기 작업은 스키마 컨텍스트와 노드 스트림의 현재 위치에 따라 작동할 수 있어야 합니다.

<a name="a_basic_reading_node_loop"></a>

## <a name="a-basic-reading-node-loop"></a>기본 읽기 노드 루프

XAML 노드 스트림을 검사하기 위한 기본 읽기 노드 루프는 다음과 같은 개념으로 구성됩니다. 이 항목에서 설명하는 노드 루프의 목적을 위해 <xref:System.Xaml.XamlXmlReader>를 사용하여 사람이 읽을 수 있는 텍스트 기반 XAML 파일을 읽고 있다고 가정합니다. 이 섹션의 링크는 <xref:System.Xaml.XamlXmlReader>에서 구현된 특정 XAML 노드 루프 API를 참조합니다.

- XAML 노드 스트림의 끝에 있지 않은지 확인합니다( <xref:System.Xaml.XamlXmlReader.IsEof%2A>확인 또는 <xref:System.Xaml.XamlXmlReader.Read%2A> 반환 값 사용). 스트림의 끝에 있는 경우 현재 노드가 없으며 종료해야 합니다.

- <xref:System.Xaml.XamlXmlReader.NodeType%2A>을 호출하여 XAML 노드 스트림이 현재 노출하는 노드 형식을 확인합니다.

- 직접 연결된 관련 XAML 개체 작성기가 있는 경우 일반적으로 이때 <xref:System.Xaml.XamlWriter.WriteNode%2A> 를 호출합니다.

- 현재 노드 또는 현재 레코드로 보고된 <xref:System.Xaml.XamlNodeType> 에 따라 다음 중 하나를 호출하여 노드 내용에 대한 정보를 가져옵니다.

  - <xref:System.Xaml.XamlXmlReader.NodeType%2A> 이 <xref:System.Xaml.XamlNodeType.StartMember> 또는 <xref:System.Xaml.XamlNodeType.EndMember>인 경우 <xref:System.Xaml.XamlXmlReader.Member%2A> 를 호출하여 멤버에 대한 <xref:System.Xaml.XamlMember> 정보를 가져옵니다. 멤버가 <xref:System.Xaml.XamlDirective>일 수도 있으므로 이전 개체의 형식이 정의된 기존 멤버가 아닐 수도 있습니다. 예를 들어 개체에 적용된 `x:Name` 은 <xref:System.Xaml.XamlMember.IsDirective%2A> 가 true이고 멤버의 <xref:System.Xaml.XamlMember.Name%2A> 이 `Name`이며 이 지시문이 XAML 언어 XAML 네임스페이스 아래에 있음을 나타내는 기타 속성이 있는 XAML 멤버로 나타납니다.

  - <xref:System.Xaml.XamlXmlReader.NodeType%2A> 이 <xref:System.Xaml.XamlNodeType.StartObject> 또는 <xref:System.Xaml.XamlNodeType.EndObject>인 경우 <xref:System.Xaml.XamlXmlReader.Type%2A> 를 호출하여 개체에 대한 <xref:System.Xaml.XamlType> 정보를 가져옵니다.

  - <xref:System.Xaml.XamlXmlReader.NodeType%2A> 이 <xref:System.Xaml.XamlNodeType.Value>인 경우 <xref:System.Xaml.XamlXmlReader.Value%2A>를 호출합니다. 멤버에 대한 가장 간단한 값 식이거나 개체에 대한 초기화 텍스트인 경우에만 노드가 값입니다(그러나 이 항목의 이후 섹션에서 설명하는 형식 변환 동작에 주의해야 함).

  - <xref:System.Xaml.XamlXmlReader.NodeType%2A> 이 <xref:System.Xaml.XamlNodeType.NamespaceDeclaration>인 경우 <xref:System.Xaml.XamlXmlReader.Namespace%2A> 를 호출하여 네임스페이스 노드에 대한 네임스페이스 정보를 가져옵니다.

- <xref:System.Xaml.XamlXmlReader.Read%2A> 를 호출하여 XAML 판독기를 XAML 노드 스트림의 다음 노드로 진행하고 다시 단계를 반복합니다.

.NET Framework XAML 서비스 XAML 판독기에서 제공하는 XAML 노드 스트림은 항상 가능한 모든 노드의 전체 순회를 제공합니다. XAML 노드 루프에 대한 일반적인 흐름 제어 기술에는 `while (reader.Read())`내에서 본문을 정의하고 노드 루프의 각 노드 지점에서 <xref:System.Xaml.XamlXmlReader.NodeType%2A> 으로 전환하는 작업이 포함됩니다.

노드 스트림이 파일의 끝에 있는 경우 현재 노드는 null입니다.

판독기 및 작성기를 사용하는 가장 간단한 루프는 다음 예제와 유사합니다.

```csharp
XamlXmlReader xxr = new XamlXmlReader(new StringReader(xamlStringToLoad));
//where xamlStringToLoad is a string of well formed XAML
XamlObjectWriter xow = new XamlObjectWriter(xxr.SchemaContext);
while (xxr.Read()) {
  xow.WriteNode(xxr);
}
```

로드 경로 XAML 노드 루프의 기본 예제에서는 XAML 판독기 및 XAML 작성기를 투명하게 연결하고 <xref:System.Xaml.XamlServices.Parse%2A?displayProperty=nameWithType>를 사용한 경우와 다른 아무 작업도 수행하지 않습니다. 그러나 이 기본 구조는 읽기 또는 쓰기 시나리오에 적용하기 위해 확장됩니다. 가능한 몇 가지 시나리오는 다음과 같습니다.

- <xref:System.Xaml.XamlXmlReader.NodeType%2A>으로 전환합니다. 읽고 있는 노드 형식에 따라 다른 작업을 수행합니다.

- 모든 경우에서 <xref:System.Xaml.XamlWriter.WriteNode%2A> 를 호출하지는 마세요. 일부 <xref:System.Xaml.XamlWriter.WriteNode%2A> 경우에서만 <xref:System.Xaml.XamlXmlReader.NodeType%2A> 를 호출합니다.

- 특정 노드 형식에 대한 논리 내에서 해당 노드의 고유 정보를 분석하고 작업을 수행합니다. 예를 들어 특정 XAML 네임스페이스에서 제공된 개체만 쓰고 해당 XAML 네임스페이스에서 제공되지 않은 개체는 모두 삭제하거나 지연할 수 있습니다. 또는 XAML 시스템에서 멤버 처리의 일부로 지원하지 않는 XAML 지시문을 모두 삭제하거나 다른 방식으로 다시 처리할 수 있습니다.

- <xref:System.Xaml.XamlObjectWriter> 메서드를 재정의하고 XAML 스키마 컨텍스트를 건너뛰는 형식 매핑을 수행할 수 있는 사용자 지정 `Write*` 를 정의합니다.

- XAML 동작의 사용자 지정 차이가 판독기와 작성기 둘 다에서 사용되도록 기본이 아닌 XAML 스키마 컨텍스트를 사용하는 <xref:System.Xaml.XamlXmlReader> 를 생성합니다.

### <a name="accessing-xaml-beyond-the-node-loop-concept"></a>노드 루프 개념을 벗어난 XAML 액세스

XAML 노드 루프가 아닌 다른 방법으로 XAML 표현을 사용할 수 있습니다. 예를 들어 인덱싱된 노드를 읽을 수 있거나 특히 `x:Name`, `x:Uid`또는 다른 식별자를 통해 노드에 직접 액세스하는 XAML 판독기가 있을 수 있습니다. .NET framework XAML 서비스는 전체 구현을 제공하지 않고 서비스 및 지원 형식을 통해 제안 패턴을 제공합니다. 자세한 내용은 <xref:System.Xaml.IXamlIndexingReader> 및 <xref:System.Xaml.XamlNodeList>를 참조하세요.

<a name="working_with_the_current_node"></a>

## <a name="working-with-the-current-node"></a>현재 노드 작업

XAML 노드 루프를 사용하는 대부분의 시나리오는 노드 읽기 이상의 작업을 수행합니다. 대부분의 시나리오에서는 현재 노드를 처리하고 한번에 하나씩 각 노드를 <xref:System.Xaml.XamlWriter>구현에 전달합니다.

일반적인 로드 경로 시나리오에서 <xref:System.Xaml.XamlXmlReader> 는 XAML 노드 스트림을 생성합니다. XAML 노드는 해당 논리 및 XAML 스키마 컨텍스트에 따라 처리되고 노드가 <xref:System.Xaml.XamlObjectWriter>에 전달됩니다. 그런 다음 결과 개체 그래프를 애플리케이션 또는 프레임워크에 통합합니다.

일반적인 저장 경로 시나리오에서 <xref:System.Xaml.XamlObjectReader> 는 개체 그래프를 읽고, 개별 XAML 노드가 처리되며, <xref:System.Xaml.XamlXmlWriter> 가 직렬화된 결과를 XAML 텍스트 파일로 출력합니다. 핵심은 경로 및 시나리오 둘 다에서 한 번에 정확히 하나의 XAML 노드 작업이 포함되며 XAML 형식 시스템 및 .NET Framework XAML 서비스 API에서 정의된 표준화된 방식으로 XAML 노드를 처리할 수 있다는 것입니다.

### <a name="frames-and-scope"></a>프레임 및 범위

XAML 노드 루프는 선형 방식으로 XAML 노드 스트림을 처리합니다. 노드 스트림은 개체, 다른 개체를 포함하는 멤버 등으로 트래버스합니다. 프레임 및 스택 개념을 구현하여 XAML 노드 스트림 내에서 범위를 추적하면 유용한 경우가 많습니다. 노드 스트림에 있는 동안 노드 스트림을 적극적으로 조정하는 경우에 특히 유용합니다. DOM 측면에서 구조를 고려할 경우 XAML 노드 구조를 깊이 탐색할 때 노드 루프 논리의 일부로 구현된 프레임 및 스택 지원에서 `StartObject` (또는 `GetObject`) 및 `EndObject` 범위 수를 계산할 수 있습니다.

<a name="traversing_and_entering_object_nodes"></a>

## <a name="traversing-and-entering-object-nodes"></a>개체 노드 트래버스 및 진입

XAML 판독기에서 열릴 때 노드 스트림의 첫 번째 노드는 루트 개체의 시작 개체 노드입니다. 정의상, 이 개체는 항상 단일 개체 노드이며 피어가 없습니다. 실제 XAML 예제에서는 루트 개체가 추가 개체를 포함하는 하나 이상의 속성을 가진 것으로 정의되며, 이러한 속성에는 멤버 노드가 있습니다. 멤버 노드는 하나 이상의 개체 노드를 포함하거나 대신 값 노드에서 종료될 수도 있습니다. 일반적으로 루트 개체는 구문상 XAML 텍스트 태그에서 특성으로 할당되지만 XAML 노드 스트림 표현에서 `Namescope` 노드 유형에 매핑되는 XAML 이름 범위를 정의합니다.

다음 XAML 예제를 고려해 보세요(.NET Framework의 기존 형식에서 지원되지 않는 임의 XAML임). 이 개체 모델에서 `FavorCollection` 은 `List<T>` 의 `Favor`이고, `Balloon` 및 `NoiseMaker` 는 `Favor`에 할당될 수 있고, `Balloon.Color` 속성은 WPF에서 색을 알려진 색 이름으로 정의하는 방법과 비슷하게 `Color` 개체에 의해 지원되며, `Color` 는 특성 구문에 대해 형식 변환기를 지원한다고 가정합니다.

|XAML 태그|결과로 생성되는 XAML 노드 스트림|
|-----------------|--------------------------------|
|`<Party`|`Namespace` 에 대한 `Party`|
|`xmlns="PartyXamlNamespace">`|`StartObject` 에 대한 `Party`|
|`<Party.Favors>`|`StartMember` 에 대한 `Party.Favors`|
||암시적`StartObject` 에 대한 `FavorCollection`노드|
||암시적`StartMember` 속성 항목에 대한 `FavorCollection` 노드입니다.|
|`<Balloon`|`StartObject` 에 대한 `Balloon`|
|`Color="Red"`|`StartMember` 에 대한 `Color`<br /><br /> 특성 값 문자열`Value` 에 대한 `"Red"`노드<br /><br /> `EndMember` 에 대한 `Color`|
|`HasHelium="True"`|`StartMember` 에 대한 `HasHelium`<br /><br /> 특성 값 문자열`Value` 에 대한 `"True"`노드<br /><br /> `EndMember` 에 대한 `HasHelium`|
|`>`|`EndObject` 에 대한 `Balloon`|
|`<NoiseMaker>Loudest</NoiseMaker>`|`StartObject` 에 대한 `NoiseMaker`<br /><br /> `StartMember` 에 대한 `_Initialization`<br /><br /> 초기화 값 문자열`Value` 에 대한 `"Loudest"`노드<br /><br /> `EndMember` 에 대한 `_Initialization`<br /><br /> `EndObject` 에 대한 `NoiseMaker`|
||암시적`EndMember` 속성 항목에 대한 `FavorCollection` 노드입니다.|
||암시적`EndObject` 에 대한 `FavorCollection`노드|
|`</Party.Favors>`|`EndMember` 에 대한 `Favors`|
|`</Party>`|`EndObject` 에 대한 `Party`|

XAML 노드 스트림에서 다음 동작에 의존할 수 있습니다.

- `Namespace` 노드가 있는 경우 스트림에서 `StartObject` 로 XAML 네임스페이스를 선언한 `xmlns`바로 앞에 추가됩니다. XAML 및 예제 노드 스트림이 포함된 앞의 표를 다시 확인합니다. `StartObject` 및 `Namespace` 노드가 텍스트 태그에서의 선언 위치와 반대로 배치된 것 같습니다. 이는 네임스페이스 노드가 항상 노드 스트림에서 적용되는 노드 앞에 표시되는 동작을 나타냅니다. 이 디자인의 목적은 네임스페이스 정보가 개체 작성기에 필수적이며 개체 작성기가 형식 매핑을 수행하거나 다른 방식으로 개체를 처리하기 전에 알고 있어야 한다는 것입니다. 스트림에서 해당 애플리케이션 범위 앞에 XAML 네임스페이스 정보를 배치하면 항상 노드 스트림을 표시된 순서대로 간단하게 처리할 수 있습니다.

- 위의 고려 사항으로 인해 루트의 `Namespace` 가 아니라 시작부터 노드를 트래버스할 때 대부분의 실제 태그 경우에서는 하나 이상의 `StartObject` 노드를 먼저 읽습니다.

- `StartObject` 노드 뒤에는 `StartMember`, `Value`또는 즉시 실행 `EndObject`가 올 수 있습니다. 다른 `StartObject`가 바로 뒤에 오는 경우는 없습니다.

- `StartMember` 뒤에는 `StartObject`, `Value`또는 즉시 실행 `EndMember`가 올 수 있습니다. 값이 새 값을 인스턴스화하는 `GetObject`가 아니라 부모 개체의 기존 값에서 제공되어야 하는 멤버의 경우 `StartObject` 가 뒤에 올 수 있습니다. 이후의 `Namespace` 에 적용되는 `StartObject`노드가 뒤에 올 수도 있습니다. 다른 `StartMember`가 바로 뒤에 오는 경우는 없습니다.

- `Value` 노드는 값 자체를 나타내며 "EndValue"가 없습니다. `EndMember`만 뒤에 올 수 있습니다.

  - 구문에서 사용할 수 있는 개체의 XAML 초기화 텍스트는 개체-값 구조를 생성하지 않습니다. 대신, `_Initialization` 이라는 멤버에 대한 전용 멤버 노드가 만들어지고 해당 멤버 노드에 초기화 값 문자열이 포함됩니다. 있는 경우 `_Initialization` 은 항상 첫 번째 `StartMember`입니다. 일부 XAML 서비스 표현에서는 XAML 언어 XAML 이름 범위로`_Initialization` 을 정규화하여 `_Initialization` 이 지원 형식에서 정의된 속성이 아님을 명확히 할 수 있습니다.

  - 멤버-값 조합은 값의 특성 설정을 나타냅니다. 결국 이 값을 처리하는 데 값 변환기가 사용될 수 있으며 값은 일반 문자열입니다. 그러나 XAML 개체 작성기에서 이 노드 스트림을 처리할 때까지는 평가되지 않습니다. XAML 개체 작성기는 필요한 XAML 스키마 컨텍스트, 형식 시스템 매핑 및 값 변환에 필요한 기타 지원을 소유합니다.

- `EndMember` 노드 뒤에는 이후 멤버에 대한 `StartMember` 노드 또는 멤버 소유자에 대한 `EndObject` 노드가 올 수 있습니다.

- `EndObject` 노드 뒤에는 `EndMember` 노드가 올 수 있습니다. 개체가 컬렉션 항목의 피어인 경우 `StartObject` 가 뒤에 올 수도 있습니다. 또는 이후의 `Namespace` 에 적용되는 `StartObject`노드가 뒤에 올 수 있습니다.

  - 전체 노드 스트림을 닫는 고유한 경우 루트의 `EndObject` 뒤에는 아무것도 오지 않습니다. 이제 판독기가 파일의 끝이며 <xref:System.Xaml.XamlReader.Read%2A> 에서 `false`를 반환합니다.

<a name="value_converters_and_the_xaml_node_stream"></a>

## <a name="value-converters-and-the-xaml-node-stream"></a>값 변환기 및 XAML 노드 스트림

값 변환기는 태그 확장, 형식 변환기(값 직렬화기 포함) 또는 XAML 형식 시스템을 통해 값 변환기로 보고되는 다른 전용 클래스를 가리키는 일반적인 용어입니다. XAML 노드 스트림에서 형식 변환기 사용과 태그 확장 사용은 전혀 다른 표현을 갖습니다.

### <a name="type-converters-in-the-xaml-node-stream"></a>XAML 노드 스트림의 형식 변환기

결국 형식 변환기가 사용되는 특성 집합은 XAML 노드 스트림에서 멤버의 값으로 보고됩니다. XAML 노드 스트림은 형식 변환기 인스턴스 개체를 생성하고 값을 전달하려고 시도하지 않습니다. 형식 변환기의 변환 구현을 사용하려면 XAML 스키마 컨텍스트를 호출하고 형식 매핑에 사용해야 합니다. 값을 처리하는 데 사용해야 하는 형식 변환기 클래스를 확인할 때에도 간접적으로 XAML 스키마 컨텍스트가 필요합니다. 기본 XAML 스키마 컨텍스트를 사용하는 경우 해당 정보는 XAML 형식 시스템에서 제공됩니다. XAML 작성기에 연결하기 전에 XAML 노드 스트림 수준의 형식 변환기 클래스 정보가 필요한 경우 설정되는 멤버의 <xref:System.Xaml.XamlMember> 정보에서 가져올 수 있습니다. 하지만 그러지 않은 경우 형식 매핑 시스템 및 XAML 스키마 컨텍스트가 필요한 나머지 작업(예: XAML 개체 작성기에 의한 개체 생성)이 수행될 때까지 형식 변환기 입력을 XAML 노드 스트림에 일반 값으로 유지해야 합니다.

예를 들어 다음과 같은 클래스 정의 개요와 XAML 사용을 고려해 보세요.

```csharp
public class BoardSizeConverter : TypeConverter {
  //converts from string to an int[2] by splitting on an "x" char
}
public class GameBoard {
  [TypeConverter(typeof(BoardSizeConverter))]
  public int[] BoardSize; //2x2 array, initialization not shown
}
```

```xaml
<GameBoard BoardSize="8x8"/>
```

이 사용을 위한 XAML 노드 스트림의 텍스트 표현은 다음과 같이 표현될 수 있습니다.

`StartObject` 이 <xref:System.Xaml.XamlType> 를 나타내는 `GameBoard`

`StartMember` 이 <xref:System.Xaml.XamlMember> 를 나타내는 `BoardSize`

텍스트 문자열 "`Value` "을 포함하는`8x8`노드

`EndMember` 가 `BoardSize`

`EndObject` 가 `GameBoard`

이 노드 스트림에는 형식 변환기 인스턴스가 없습니다. 그러나 `BoardSize`에 대한 <xref:System.Xaml.XamlMember>에서 <xref:System.Xaml.XamlMember.TypeConverter%2A?displayProperty=nameWithType>를 호출하여 형식 변환기 정보를 가져올 수 있습니다. 유효한 XAML 스키마 컨텍스트가 있는 경우 <xref:System.Xaml.Schema.XamlValueConverter%601.ConverterInstance%2A>에서 인스턴스를 가져와 변환기 메서드를 호출할 수도 있습니다.

### <a name="markup-extensions-in-the-xaml-node-stream"></a>XAML 노드 스트림의 태그 확장

태그 확장 사용은 XAML 노드 스트림에서 멤버 내의 개체 노드로 보고됩니다. 여기서 개체는 태그 확장 인스턴스를 나타냅니다. 따라서 태그 확장 사용은 노드 스트림 표현에서 형식 변환기 사용보다 더 명시적으로 표시되며 자세한 정보를 전달합니다. 사용이 상황에 따라 결정되고 가능한 각 태그의 경우에서 달라지므로<xref:System.Xaml.XamlMember> 정보에서 태그 확장에 대한 정보를 제공하지 못할 수도 있습니다. 형식 변환기의 경우처럼 형식 또는 멤버별로 전용 및 암시적이 아닙니다.

XAML 텍스트 태그에서 특성 형태로 태그 확장 사용이 수행된 경우에도 태그 확장을 개체 노드로 표현하는 노드 스트림 표현이 이러한 경우에 해당합니다(자주 발생함). 명시적 개체 요소 형태를 사용한 태그 확장 사용은 동일한 방식으로 처리됩니다.

태그 확장 개체 노드 내에 해당 태그 확장의 멤버가 있을 수 있습니다. XAML 노드 스트림 표현은 위치 매개 변수 사용인지 또는 명명된 명시적 매개 변수를 통한 사용인지에 관계없이 해당 태그 확장의 사용을 유지합니다.

위치 매개 변수 사용의 경우 XAML 노드 스트림에 사용을 기록하는 XAML 언어로 정의된 속성 `_PositionalParameters` 가 포함됩니다. 이 속성은 <xref:System.Collections.Generic.List%601> 제약 조건이 있는 제네릭 <xref:System.Object> 입니다. 위치 매개 변수 사용 내에 중첩된 태그 확장 사용이 포함될 수 있으므로 제약 조건은 문자열이 아니라 개체입니다. 사용에서 위치 매개 변수에 액세스하려면 목록을 반복하고 개별 목록 값의 인덱서를 사용할 수 있습니다.

명명된 매개 변수 사용의 경우 명명된 각 매개 변수가 노드 스트림에서 해당 이름의 멤버 노드로 표시됩니다. 중첩된 태그 확장 사용이 있을 수 있으므로 멤버 값은 문자열이 아닐 수도 있습니다.

태그 확장의`ProvideValue` 가 아직 호출되지 않았습니다. 그러나 노드 스트림에서 검사할 때 태그 확장 노드에서 `WriteEndObject` 가 호출되도록 XAML 판독기 및 XAML 작성기를 연결하면 호출됩니다. 이러한 이유로, 일반적으로 로드 경로에서 개체 그래프를 형성하기 위해 사용되는 것과 동일한 XAML 스키마 컨텍스트를 사용할 수 있어야 합니다. 그러지 않으면 필요한 서비스를 사용할 수 없기 때문에 태그 확장의 `ProvideValue` 에서 예외가 발생할 수 있습니다.

<a name="xaml_and_xml_languagedefined_members_in_the_xaml_node_stream"></a>

## <a name="xaml-and-xml-language-defined-members-in-the-xaml-node-stream"></a>XAML 노드 스트림의 XAML 및 XML 언어로 정의된 멤버

명시적 <xref:System.Xaml.XamlMember> 조회 또는 생성을 사용하는 대신 XAML 판독기의 해석과 규칙으로 인해 특정 멤버가 XAML 노드 스트림에 소개됩니다. 대개 이러한 멤버는 XAML 지시문입니다. 경우에 따라 XAML 노드 스트림에 지시문을 소개하는 XAML 읽기 동작입니다. 즉, 원래 입력 XAML 텍스트는 멤버 지시문을 명시적으로 지정 하지 않았지만 XAML 판독기는 xaml 노드 스트림에서 구조 XAML 규칙 및 보고서 정보를 충족 하기 위해 지시문을 삽입 하 여 정보를 손실 합니다.

다음 목록에서는 XAML 판독기가 지시문 XAML 멤버 노드를 소개해야 하는 모든 경우 및 .NET Framework XAML 서비스 구현에서 해당 멤버 노드가 식별되는 방식을 보여 줍니다.

- **개체 노드에 대 한 초기화 텍스트:** 이 멤버 노드의 `_Initialization`이름은이 고, xaml 지시문을 나타내며, xaml 언어 xaml 네임 스페이스에서 정의 됩니다. <xref:System.Xaml.XamlLanguage.Initialization%2A>에서 해당 정적 엔터티를 가져올 수 있습니다.

- **태그 확장에 대 한 위치 매개 변수:** 이 멤버 노드의 `_PositionalParameters`이름은이 고 xaml 언어 xaml 네임 스페이스에서 정의 됩니다. 각각 입력 XAML에서 제공될 때 `,` 구분 기호 문자에서 분할하여 미리 구분된 위치 매개 변수인 개체의 제네릭 목록을 항상 포함합니다. <xref:System.Xaml.XamlLanguage.PositionalParameters%2A>에서 위치 매개 변수 지시문에 대한 정적 엔터티를 가져올 수 있습니다.

- **알 수 없는 내용:** 이 멤버 노드의 `_UnknownContent`이름은입니다. 엄격히 말해서, <xref:System.Xaml.XamlDirective>이며 XAML 언어 XAML 네임스페이스에서 정의됩니다. 이 지시문은 XAML 개체 요소에 소스 XAML의 콘텐츠가 포함되지만 현재 사용할 수 있는 XAML 스키마 컨텍스트에서 콘텐츠 속성을 확인할 수 없는 경우에 대한 센티널로 사용됩니다. XAML 노드 스트림에서 `_UnknownContent`라는 멤버를 확인하여 이러한 경우를 검색할 수 있습니다. 로드 경로 XAML 노드 스트림에서 다른 작업을 수행하지 않는 경우 임의 개체에서 <xref:System.Xaml.XamlObjectWriter> 멤버를 발견하면 시도된 `WriteEndObject` 에서 기본 `_UnknownContent` 가 발생합니다. 기본 <xref:System.Xaml.XamlXmlWriter> 가 발생하지 않고 멤버를 암시적으로 처리합니다. `_UnknownContent` 에서 <xref:System.Xaml.XamlLanguage.UnknownContent%2A>에 대한 정적 엔터티를 가져올 수 있습니다.

- **컬렉션의 컬렉션 속성:** 일반적으로 XAML에 사용 되는 컬렉션 클래스의 지원 CLR 형식에는 컬렉션 항목을 포함 하는 명명 된 전용 속성이 있지만이 속성은 지원 형식 확인 전에 XAML 형식 시스템에서 알 수 없습니다. 대신, XAML 노드 스트림은 `Items` 자리 표시자를 컬렉션 XAML 형식의 멤버로 소개합니다. .NET Framework XAML 서비스 구현의 노드 스트림에서 이 지시문/멤버의 이름은 `_Items`입니다. 이 지시문에 대한 상수는 <xref:System.Xaml.XamlLanguage.Items%2A>에서 가져올 수 있습니다.

    XAML 노드 스트림에는 지원 형식 확인 및 XAML 스키마 컨텍스트를 기준으로 구문 분석할 수 없는 항목이 있는 Items 속성이 포함 될 수 있습니다. 예를 들면 다음과 같습니다.

- **XML 정의 멤버:** `xml:base`XML로 정의 `xml:lang` 된 및 `xml:space` 멤버는 .NET Framework xaml 서비스 구현에서, `base` `lang`및 `space` 라는 xaml 지시문으로 보고 됩니다. 이러한 멤버에 대한 네임스페이스는 XML 네임스페이스 `http://www.w3.org/XML/1998/namespace`입니다. 각 멤버에 대한 상수는 <xref:System.Xaml.XamlLanguage>에서 가져올 수 있습니다.

## <a name="node-order"></a>노드 순서

경우에 따라 <xref:System.Xaml.XamlXmlReader> 는 태그에서 보는 경우 또는 XML로 처리되는 경우 노드가 나타나는 순서와 반대로 XAML 노드 스트림의 XAML 노드 순서를 변경합니다. 이 작업은 <xref:System.Xaml.XamlObjectWriter> 가 정방향으로만 노드 스트림을 처리할 수 있도록 노드를 정렬하기 위해 수행됩니다.  .NET Framework XAML 서비스에서 XAML 판독기는 노드 스트림의 XAML 개체 작성기 소비자에 대한 성능 최적화로 XAML 작성기에 이 작업을 맡기지 않고 노드를 다시 정렬합니다.

특정 지시문은 특히 object 요소에서 개체를 만들기 위한 자세한 정보를 제공하는 데 사용됩니다. 해당 지시문은 `Initialization`, `PositionalParameters`, `TypeArguments`, `FactoryMethod`, `Arguments`입니다. .NET Framework XAML 서비스 XAML 판독기는 다음 섹션에서 설명하는 이유로 이러한 지시문을 개체의 `StartObject`뒤에 노드 스트림의 첫 번째 멤버로 배치하려고 합니다.

### <a name="xamlobjectwriter-behavior-and-node-order"></a>XamlObjectWriter 동작 및 노드 순서

`StartObject` 에 대한 <xref:System.Xaml.XamlObjectWriter> 는 XAML 개체 작성기에 개체 인스턴스를 즉시 생성하라는 신호가 아닐 수도 있습니다. XAML에는 추가 입력으로 개체를 초기화할 수 있도록 하 고, 매개 변수가 없는 생성자를 호출 하 여 초기 개체를 생성 한 다음 속성을 설정 하는 것에 전적으로 의존 하지 않는 여러 언어 기능이 포함 되어 있습니다. 이러한 기능에는 <xref:System.Windows.Markup.XamlDeferLoadAttribute>초기화 텍스트, [x:TypeArguments](x-typearguments-directive.md), 태그 확장의 위치 매개 변수, 팩터리 메서드 및 연결된 [x:Arguments](x-arguments-directive.md) 노드(XAML 2009)가 포함됩니다. 이러한 각 경우에서는 실제 개체 생성이 지연되며 노드 스트림이 다시 정렬되므로, XAML 개체 작성기가 구체적으로 해당 개체 유형에 대한 생성 지시문이 아닌 시작 멤버를 발견할 때마다 인스턴스를 실제로 생성하는 동작에 의존할 수 있습니다.

### <a name="getobject"></a>GetObject

`GetObject` 는 새 개체를 생성하는 대신 XAML 개체 작성기가 개체의 포함 속성 값을 가져와야 하는 XAML 노드를 나타냅니다. `GetObject` 노드가 XAML 노드 스트림에서 발견되는 일반적인 경우는 컬렉션 개체 또는 사전 개체에 대해 지원 형식의 개체 모델에서 포함 속성이 의도적으로 읽기 전용일 때입니다. 이 시나리오에서는 컬렉션 또는 사전이 소유 형식의 초기화 논리에 의해 만들어지고 초기화(일반적으로 비어 있음)되는 경우가 많습니다.

## <a name="see-also"></a>참고자료

- <xref:System.Xaml.XamlObjectReader>
- [XAML 서비스](index.md)
- [XAML 네임스페이스](xaml-namespaces-for-net-framework-xaml-services.md)
