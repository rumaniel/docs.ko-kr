---
title: PropertyPath XAML 구문
ms.date: 03/30/2017
helpviewer_keywords:
- PropertyPath object [WPF]
- XAML [WPF], PropertyPath object
ms.assetid: 0e3cdf07-abe6-460a-a9af-3764b4fd707f
ms.openlocfilehash: deebdb690a6ba831730701de2608089af2d6bdfd
ms.sourcegitcommit: 24a4a8eb6d8cfe7b8549fb6d823076d7c697e0c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68401667"
---
# <a name="propertypath-xaml-syntax"></a>PropertyPath XAML 구문

개체 <xref:System.Windows.PropertyPath> 는 <xref:System.Windows.PropertyPath> 형식을 값으로 사용 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 하는 다양 한 속성을 설정 하기 위한 복잡 한 인라인 구문을 지원 합니다. 이 항목에서는 바인딩 <xref:System.Windows.PropertyPath> 및 애니메이션 구문에 적용 되는 구문에 대해 설명 합니다.

<a name="where"></a>

## <a name="where-propertypath-is-used"></a>PropertyPath를 사용하는 경우

<xref:System.Windows.PropertyPath>는 여러 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 기능에서 사용 되는 공통 개체입니다. 일반적 <xref:System.Windows.PropertyPath> 으로 속성 경로 정보를 전달 하는 데에도 불구 하 고 <xref:System.Windows.PropertyPath> 가 형식으로 사용 되는 각 기능 영역에 대 한 사용량은 다양 합니다. 따라서 구문은 기능별로 설명하는 것이 좋습니다.

주로는를 <xref:System.Windows.PropertyPath> 사용 하 여 개체 데이터 소스의 속성을 순회 하 고 대상 애니메이션의 대상 경로를 설명 하는 개체 모델 경로를 설명 합니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]

과 같은 일부 스타일 및 템플릿 속성 <xref:System.Windows.Setter.Property%2A?displayProperty=nameWithType> 은 표면적와 <xref:System.Windows.PropertyPath>비슷한 정규화 된 속성 이름을 사용 합니다. 그러나이는 <xref:System.Windows.PropertyPath>true가 아니라 정규화 된 *소유자입니다.* WPF [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 프로세서에서의 <xref:System.Windows.DependencyProperty>형식 변환기와 함께 사용 하도록 설정 된 속성 문자열 형식 사용입니다.

<a name="databinding_s"></a>

## <a name="propertypath-for-objects-in-data-binding"></a>데이터 바인딩의 개체에 대한 PropertyPath

데이터 바인딩은 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 기능으로 이를 통해 종속성 속성의 대상 값에 바인딩할 수 있습니다. 하지만 해당 데이터 바인딩의 소스는 종속성 속성이어야 하며 적용 가능한 데이터 공급자가 인식하는 모든 속성 형식일 수 있습니다. 속성 경로는 CLR (공용 언어 <xref:System.Windows.Data.ObjectDataProvider>런타임) 개체 및 해당 속성에서 바인딩 소스를 가져오는 데 사용 되는에 특히 사용 됩니다.

에 대 [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] 한 데이터 바인딩은에서을 사용 <xref:System.Windows.PropertyPath> <xref:System.Windows.Data.Binding.Path%2A> <xref:System.Windows.Data.Binding>하지 않으므로를 사용 하지 않습니다. 대신를 사용 <xref:System.Windows.Data.Binding.XPath%2A> 하 여 데이터의에 [!INCLUDE[TLA#tla_xmldom](../../../../includes/tlasharptla-xmldom-md.md)] 올바른 XPath 구문을 지정 합니다. <xref:System.Windows.Data.Binding.XPath%2A>는 문자열로도 지정 되어 있지만 여기서는 설명 하지 않습니다. [XMLDataProvider 및 XPath 쿼리를 사용 하 여 XML 데이터에 바인딩을](../data/how-to-bind-to-xml-data-using-an-xmldataprovider-and-xpath-queries.md)참조 하세요.

데이터 바인딩의 속성 경로를 이해하는 열쇠는 개별 속성 값에 대한 바인딩을 대상으로 지정할 수 있거나 목록이나 컬렉션을 사용하는 대상 속성에 바인딩할 수 있다는 점입니다. 컬렉션을 바인딩하는 경우 컬렉션에 있는 데이터 항목 <xref:System.Windows.Controls.ListBox> 의 수에 따라 확장 되는 인스턴스를 바인딩하는 경우 속성 경로는 개별 컬렉션 항목이 아니라 컬렉션 개체를 참조 해야 합니다. 데이터 바인딩 엔진은 데이터 원본으로 사용 되는 컬렉션을 바인딩 대상의 형식으로 자동으로 일치 시킵니다. 그러면에 <xref:System.Windows.Controls.ListBox> 항목 배열을 채우는 것과 같은 동작이 발생 합니다.

<a name="singlecurrent"></a>

### <a name="single-property-on-the-immediate-object-as-data-context"></a>데이터 컨텍스트로서 직접 실행 개체에 대한 단일 속성

```xml
<Binding Path="propertyName" .../>
```

*propertyName* 은 <xref:System.Windows.FrameworkElement.DataContext%2A> <xref:System.Windows.Data.Binding.Path%2A> 사용에 대 한 현재에 있는 속성의 이름으로 확인 되어야 합니다. 바인딩이 소스를 업데이트하면 해당 속성은 읽기/쓰기여야 하고 소스 개체는 변경 가능해야 합니다.

<a name="singleindex"></a>

### <a name="single-indexer-on-the-immediate-object-as-data-context"></a>데이터 컨텍스트로서 직접 실행 개체에 대한 단일 인덱서

```xml
<Binding Path="[key]" .../>
```

`key`는 사전 및 해시 테이블에 대한 형식화된 인덱스이거나 배열의 정수 인덱스여야 합니다. 또한 키 값은 키 값이 적용되는 속성에 직접 바인딩할 수 있는 형식이어야 합니다. 예를 들어 문자열 키 및 문자열 값을 포함 하는 해시 테이블을이 방법으로 사용 하 여의 <xref:System.Windows.Controls.TextBox>텍스트에 바인딩할 수 있습니다. 또는 키가 컬렉션이나 하위 인덱스를 가리키는 경우 이 구문을 사용하여 대상 컬렉션 속성에 바인딩할 수 있습니다. 이외의 경우에는 `<Binding Path="[key].propertyName" .../>`과 같은 구문을 통해 특정 속성을 참조해야 합니다.

필요한 경우 인덱스의 형식을 지정할 수 있습니다. 인덱싱된 속성 경로의 이러한 측면에 대 한 자세한 내용은을 참조 <xref:System.Windows.Data.Binding.Path%2A?displayProperty=nameWithType>하십시오.

<a name="multipleindirect"></a>

### <a name="multiple-property-indirect-property-targeting"></a>다중 속성(간접 속성 대상 지정)

```xml
<Binding Path="propertyName.propertyName2" .../>
```

`propertyName`는 현재 <xref:System.Windows.FrameworkElement.DataContext%2A>인 속성의 이름으로 확인 되어야 합니다. 경로 속성 `propertyName` 및 `propertyName2`는 관계에 있는 속성일 수 있습니다. 여기서 `propertyName2`는 `propertyName` 값인 형식에 있는 속성입니다.

<a name="singleattached"></a>

### <a name="single-property-attached-or-otherwise-type-qualified"></a>연결된 또는 정규화된 형식의 단일 속성

```xml
<object property="(ownerType.propertyName)" .../>
```

괄호는의 <xref:System.Windows.PropertyPath> 이 속성이 부분 정규화를 사용 하 여 생성 되어야 함을 의미 합니다. XML 네임스페이스를 사용하여 적절한 매핑이 있는 형식을 찾을 수 있습니다. 는 `ownerType` 각 어셈블리의 <xref:System.Windows.Markup.XmlnsDefinitionAttribute> 선언을 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 통해 프로세서가 액세스할 수 있는 형식을 검색 합니다. 대부분 애플리케이션에서는 기본 XML 네임스페이스가 [!INCLUDE[TLA#tla_wpfxmlnsv1](../../../../includes/tlasharptla-wpfxmlnsv1-md.md)] 네임스페이스에 매핑되므로 접두사는 대개 사용자 지정 형식 또는 해당 네임스페이스 외부의 형식에만 필요합니다.  `propertyName`은 `ownerType`에 있는 속성의 이름으로 확인되어야 합니다. 일반적으로 이 구문은 다음 경우 중 하나에 사용됩니다.

- 경로는 지정된 대상 형식이 없는 스타일 또는 템플릿인 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]에 지정됩니다. 스타일이 아니고 템플릿이 아닌 경우에 속성은 형식이 아닌 인스턴스에 있으므로 일반적으로 이를 제외한 다른 경우에는 정규화된 사용이 적절하지 않습니다.

- 속성은 연결된 속성입니다.

- 정적 속성이 바인딩 중입니다.

스토리 보드 대상으로 사용 하는 경우로 `propertyName` 지정 된 속성은 이어야 합니다. <xref:System.Windows.DependencyProperty>

<a name="sourcetraversal"></a>

### <a name="source-traversal-binding-to-hierarchies-of-collections"></a>소스 순회(컬렉션 계층 구조에 바인딩)

```xml
<object Path="propertyName/propertyNameX" .../>
```

이 구문의 /는 계층적 데이터 소스 개체 내에서 탐색하는 데 사용되고 연속 / 문자가 있는 계층 구조에 대한 여러 단계는 지원되지 않습니다. 소스 순회는 데이터를 뷰의 UI와 동기화할 때 결정되는 현재 레코드 포인터 위치를 처리합니다. 계층적 데이터 소스 개체를 사용한 바인딩 및 데이터 바인딩의 현재 레코드 포인터 개념에 대한 자세한 내용은 [계층적 데이터에 마스터-세부 패턴 사용](../data/how-to-use-the-master-detail-pattern-with-hierarchical-data.md) 또는 [데이터 바인딩 개요](../data/data-binding-overview.md)를 참조하세요.

> [!NOTE]
> 표면적으로 이 구문은 [!INCLUDE[TLA2#tla_xpath](../../../../includes/tla2sharptla-xpath-md.md)]와 비슷합니다. 데이터 원본 [!INCLUDE[TLA2#tla_xpath](../../../../includes/tla2sharptla-xpath-md.md)] <xref:System.Windows.Data.Binding.Path%2A> <xref:System.Windows.Data.Binding.XPath%2A> 에 바인딩하기 위한 true 식은 값으로 사용 되지 않으며, 대신 함께 사용할 수 없는 속성에 사용 해야 합니다. [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)]

### <a name="collection-views"></a>컬렉션 뷰

명명된 컬렉션 뷰를 참조하려면 해시 문자(`#`)를 컬렉션 뷰 이름에 접두사로 추가합니다.

### <a name="current-record-pointer"></a>현재 레코드 포인터

컬렉션 뷰 또는 마스터 세부 데이터 바인딩 시나리오에 대한 현재 레코드 포인터를 참조하려면 경로 문자열을 슬래시(`/`)로 시작합니다. 슬래시를 통과하는 모든 경로는 현재 레코드 포인터부터 이동합니다.

### <a name="multiple-indexers"></a>여러 인덱서

```xaml
<object Path="[index1,index2...]" .../>
```

로 구분하거나 여러

```xaml
<object Path="propertyName[index,index2...]" .../>
```

특정 개체가 여러 인덱서를 지원할 경우 이러한 인덱서는 배열 참조 구문처럼 순서대로 지정될 수 있습니다. 해당 개체는 현재 컨텍스트이거나 여러 인덱스 개체를 포함하는 속성의 값일 수 있습니다.

기본적으로 인덱서 값은 기본 개체의 특징을 사용해서 형식화됩니다. 필요한 경우 인덱스의 형식을 지정할 수 있습니다. 인덱서를 입력 하는 방법에 대 <xref:System.Windows.Data.Binding.Path%2A?displayProperty=nameWithType>한 자세한 내용은을 참조 하십시오.

<a name="mixing"></a>

### <a name="mixing-syntaxes"></a>구문 혼합

위에 표시되는 각 구문은 섞여 있을 수 있습니다. 예를 들어, 다음은 개체의 `ColorGrid` <xref:System.Windows.Media.SolidColorBrush> 픽셀 그리드 배열을 포함 하는 속성의 특정 x, y에서 색에 대 한 속성 경로를 만드는 예제입니다.

```xml
<Rectangle Fill="{Binding ColorGrid[20,30].SolidColorBrushResult}" .../>
```

### <a name="escapes-for-property-path-strings"></a>속성 경로 문자열에 대한 이스케이프

특정 비즈니스 개체의 경우 제대로 구문 분석되려면 속성 경로 문자열에 이스케이프 시퀀스가 있어야 하는 경우가 있습니다. 이스케이프해야 하는 경우는 드뭅니다. 대부분의 이러한 문자에는 일반적으로 비즈니스 개체를 정의하는 데 사용되는 언어에 비슷한 명명 상호 작용 문제가 있기 때문입니다.

- 인덱서([ ]) 안의 캐럿 문자(^)는 다음 문자를 이스케이프합니다.

- XML 언어 정의와 관련된 특정 문자를 이스케이프(XML 엔터티 사용)해야 합니다. "&" 문자를 이스케이프하려면 `&`를 사용합니다. ">" 끝 태그를 이스케이프하려면 `>`를 사용합니다.

- 태그 확장을 처리하기 위해 WPF XAML 구문 분석기 동작과 관련된 특정 문자를 이스케이프해야 합니다(백슬래시 `\` 사용).

  - 백슬래시(`\`)는 그 자체로 이스케이프 문자입니다.

  - 등호(`=`)는 속성 값에서 속성 이름을 구분합니다.

  - 쉼표(`,`)는 속성을 구분합니다.

  - 오른쪽 중괄호(`}`)는 태그 확장의 끝입니다.

> [!NOTE]
> 기술적으로 이러한 이스케이프는 스토리보드 속성 경로에도 적용되지만 대개 기존 WPF 개체에 대한 개체 모델을 통과하므로 이스케이프가 필요하지 않습니다.

<a name="databinding_sa"></a>

## <a name="propertypath-for-animation-targets"></a>애니메이션 대상에 대한 PropertyPath

애니메이션의 target 속성은 <xref:System.Windows.Freezable> 또는 기본 형식을 사용 하는 종속성 속성 이어야 합니다. 하지만 형식의 대상 속성 및 최종 애니메이션 효과가 적용된 속성은 서로 다른 개체에 있을 수 있습니다. 애니메이션에 대한 속성 경로는 속성 값에서 개체 속성 관계를 통과하는 방식으로 명명된 애니메이션 대상 개체의 속성과 의도한 대상 애니메이션 속성 간 연결을 정의하는 데 사용됩니다.

<a name="general"></a>

### <a name="general-object-property-considerations-for-animations"></a>애니메이션에 대한 일반 개체 속성 고려 사항

일반적인 애니메이션 개념에 대한 자세한 내용은 [Storyboard 개요](../graphics-multimedia/storyboards-overview.md) 및 [애니메이션 개요](../graphics-multimedia/animation-overview.md)를 참조하세요.

애니메이션 효과가 적용 되는 값 형식 또는 속성은 <xref:System.Windows.Freezable> 형식 이거나 기본 형식 이어야 합니다. 경로를 시작 하는 속성은 지정 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 된 형식에 있는 종속성 속성의 이름으로 확인 되어야 합니다.

이미 <xref:System.Windows.Freezable> 고정 된에 애니메이션을 적용 하기 위한 복제를 지원 하기 위해에 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 지정 <xref:System.Windows.FrameworkElement> 된 개체는 또는 <xref:System.Windows.FrameworkContentElement> 파생 클래스 여야 합니다.

<a name="singlestepanim"></a>

### <a name="single-property-on-the-target-object"></a>대상 개체에 대한 단일 속성

```xml
<animation Storyboard.TargetProperty="propertyName" .../>
```

`propertyName`는 지정 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 된 형식에 있는 종속성 속성의 이름으로 확인 되어야 합니다.

<a name="indirectanim"></a>

### <a name="indirect-property-targeting"></a>간접 속성 대상 지정

```xml
<animation Storyboard.TargetProperty="propertyName.propertyName2" .../>
```

`propertyName`는 지정 <xref:System.Windows.Freezable> <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 된 형식에 있는 값 형식 또는 기본 형식인 속성 이어야 합니다.

`propertyName2`는 `propertyName` 값인 개체에 있는 종속성 속성의 이름이어야 합니다. 즉, `propertyName2` 는 인 형식 `propertyName` <xref:System.Windows.DependencyProperty.PropertyType%2A>에 대 한 종속성 속성으로 존재 해야 합니다.

적용된 스타일 및 템플릿 때문에 애니메이션의 간접 대상 지정이 필요합니다. 애니메이션을 대상으로 하려면 대상 개체에가 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> 필요 하며,이 이름은 [x:Name](../../xaml-services/x-name-directive.md) 또는 <xref:System.Windows.FrameworkElement.Name%2A>로 설정 됩니다. 템플릿 및 스타일 요소에 이름이 있을 수 있지만 해당 이름은 스타일 및 템플릿의 네임스페이스 내에서만 유효합니다. 템플릿 및 스타일이 네임스페이스를 애플리케이션 태그와 공유한 경우 이름이 고유하지 않습니다. 스타일 및 템플릿은 문자 그대로 인스턴스 간에 공유되고 중복 이름을 영구화합니다. 따라서 애니메이션 효과를 줄 요소의 개별 속성이 스타일이나 템플릿을 기반으로 한 경우 스타일 템플릿을 기반으로 하지 않은 명명된 요소 인스턴스로 시작한 다음 애니메이션 효과를 줄 속성에 도착할 스타일 또는 템플릿 시각적 트리를 대상으로 지정해야 합니다.

예를 <xref:System.Windows.Controls.Panel.Background%2A> 들어 <xref:System.Windows.Controls.Panel> 의 속성은 테마 템플릿에서 가져온 전체 <xref:System.Windows.Media.Brush> (실제로 <xref:System.Windows.Media.SolidColorBrush>)입니다. <xref:System.Windows.Media.Brush> 전체에 애니메이션 효과를 주려면 BrushAnimation (모든 <xref:System.Windows.Media.Brush> 형식에 대해 하나)가 필요 하 고 이러한 형식이 없는 것입니다. 브러시에 애니메이션 효과를 주려면 특정 <xref:System.Windows.Media.Brush> 형식의 속성에 애니메이션 효과를 주는 것이 좋습니다. 에서 <xref:System.Windows.Media.SolidColorBrush> <xref:System.Windows.Media.Animation.ColorAnimation> 로 이동하여이를적용해야합니다.<xref:System.Windows.Media.SolidColorBrush.Color%2A> 이 예제의 속성 경로는 `Background.Color`입니다.

<a name="attachedanim"></a>

### <a name="attached-properties"></a>연결된 속성

```xml
<animation Storyboard.TargetProperty="(ownerType.propertyName)" .../>
```

괄호는의 <xref:System.Windows.PropertyPath> 이 속성이 부분 정규화를 사용 하 여 생성 되어야 함을 의미 합니다. XML 네임스페이스를 사용하여 형식을 찾을 수 있습니다. 는 `ownerType` 각 어셈블리의 <xref:System.Windows.Markup.XmlnsDefinitionAttribute> 선언을 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 통해 프로세서가 액세스할 수 있는 형식을 검색 합니다. 대부분 애플리케이션에서는 기본 XML 네임스페이스가 [!INCLUDE[TLA#tla_wpfxmlnsv1](../../../../includes/tlasharptla-wpfxmlnsv1-md.md)] 네임스페이스에 매핑되므로 접두사는 대개 사용자 지정 형식 또는 해당 네임스페이스 외부의 형식에만 필요합니다. `propertyName`은 `ownerType`에 있는 속성의 이름으로 확인되어야 합니다. 로 `propertyName` 지정 된 속성은 이어야 합니다 <xref:System.Windows.DependencyProperty>. 모든 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 연결된 속성은 종속성 속성으로 구현되므로 이 문제는 사용자 지정 연결된 속성에만 관련됩니다.

<a name="indexanim"></a>

### <a name="indexers"></a>인덱서

```xml
<animation Storyboard.TargetProperty="propertyName.propertyName2[index].propertyName3" .../>
```

대부분의 종속성 속성 <xref:System.Windows.Freezable> 또는 형식은 인덱서를 지원 하지 않습니다. 따라서 애니메이션 경로에서 인덱서는 명명된 대상에서 체인을 시작하는 속성과 최종 애니메이션 효과가 적용된 속성 사이의 중간 위치에만 사용됩니다. 제공된 구문에서 인덱서는 `propertyName2`입니다. 예를 들어와 같은 속성 경로 <xref:System.Windows.Media.TransformGroup> `RenderTransform.Children[1].Angle`에 중간 속성이와 같은 컬렉션인 경우 인덱서를 사용 해야 할 수 있습니다.

<a name="ppincode"></a>

## <a name="propertypath-in-code"></a>코드의 PropertyPath

를 <xref:System.Windows.PropertyPath> <xref:System.Windows.PropertyPath>구성 하는 방법을 비롯 하 여의 코드 사용은에 대 한 참조 항목에 설명 되어 있습니다. <xref:System.Windows.PropertyPath>

일반적 <xref:System.Windows.PropertyPath> 으로는 바인딩 사용 및 가장 간단한 애니메이션 사용을 위한 생성자와 복잡 한 애니메이션 사용을 위한 두 가지 생성자를 사용 하도록 설계 되었습니다. 개체를 문자열로 사용 하는 바인딩 사용에 대 한 서명을사용합니다.<xref:System.Windows.PropertyPath.%23ctor%28System.Object%29> 개체가 인 1 단계 애니메이션 경로에 <xref:System.Windows.PropertyPath.%23ctor%28System.Object%29> 서명을 사용 합니다 <xref:System.Windows.DependencyProperty>. 복합 애니메이션 <xref:System.Windows.PropertyPath.%23ctor%28System.String%2CSystem.Object%5B%5D%29> 에는 서명을 사용 합니다. 후자의 생성자는 첫 번째 매개 변수에 토큰 문자열을 사용하고 속성 경로 관계를 정의하기 위해 토큰 문자열의 위치를 채우는 개체 배열을 사용합니다.

## <a name="see-also"></a>참고자료

- <xref:System.Windows.PropertyPath>
- [데이터 바인딩 개요](../data/data-binding-overview.md)
- [Storyboard 개요](../graphics-multimedia/storyboards-overview.md)
