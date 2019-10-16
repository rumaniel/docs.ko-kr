---
title: 바인딩 선언 개요
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- markup extensions [WPF]
- data binding [WPF], declarations
- object element syntax [WPF]
- binding data [WPF], declarations
- syntax [WPF], object elements
- binding declarations [WPF]
ms.assetid: b97fd626-4c0d-4761-872a-2bca5820da2c
ms.openlocfilehash: 3cf128a8d05dbc089f2b481da6b51865b419e25c
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64754450"
---
# <a name="binding-declarations-overview"></a>바인딩 선언 개요

이 항목에서는 바인딩을 선언할 수 있는 여러 가지 방법을 설명합니다.

<a name="Prereq"></a>

## <a name="prerequisites"></a>전제 조건

이 항목은 태그 확장의 개념 및 사용 방법에 익숙하다는 것을 전제로 합니다. 태그 확장에 대한 자세한 내용은 [XAML 태그 확장 및 WPF XAML](../advanced/markup-extensions-and-wpf-xaml.md)을 참조하세요.

이 항목에서는 데이터 바인딩 개념에 대해 다루지 않습니다. 데이터 바인딩 개념에 대한 자세한 내용은 [데이터 바인딩 개요](data-binding-overview.md)를 참조하세요.

<a name="BindinginXAML"></a>

## <a name="declaring-a-binding-in-xaml"></a>XAML에서 바인딩 선언

이 섹션에서는 XAML에서 바인딩을 선언하는 방법을 설명합니다.

<a name="MarkupExtensionSyntax"></a>

### <a name="markup-extension-usage"></a>태그 확장 사용

<xref:System.Windows.Data.Binding>은 태그 확장입니다. 바인딩 확장을 사용하여 바인딩을 선언할 때 선언은 `Binding` 키워드 뒤에 일련의 절이 쉼표(,)로 구분된 형태로 구성됩니다. 바인딩 선언의 절 순서는 중요하지 않으며 수많은 조합이 가능합니다. 절을 *이름*=*값* 위치 쌍 *이름* 이름인 합니다 <xref:System.Windows.Data.Binding> 속성 및 *값* 는 속성에 대해 설정 하는 값입니다.

태그에서 바인딩 선언 문자열을 만들 때는 대상 개체의 특정 종속성 속성에 연결해야 합니다. 다음 예제에서는 바인딩하는 방법을 보여줍니다 합니다 <xref:System.Windows.Controls.TextBox.Text%2A?displayProperty=nameWithType> 속성 바인딩 확장을 사용 하 여, 지정 하는 <xref:System.Windows.Data.Binding.Source%2A> 및 <xref:System.Windows.Data.Binding.Path%2A> 속성.

[!code-xaml[SimpleBinding](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleBinding/CSharp/Page1.xaml#L37-L37)]

대부분의 속성을 지정할 수 있습니다는 <xref:System.Windows.Data.Binding> 이 이런 클래스입니다. 목록은 물론 바인딩 확장에 대 한 자세한 내용은 <xref:System.Windows.Data.Binding> 바인딩 확장을 사용 하 여 설정할 수 없는 속성 참조를 [바인딩 태그 확장](../advanced/binding-markup-extension.md) 개요.

<a name="ObjectElementSyntax"></a>

### <a name="object-element-syntax"></a>개체 요소 구문

개체 요소 구문은 바인딩 선언을 만드는 대신 사용할 수 있습니다. 대부분의 경우 태그 확장 또는 개체 요소 구문을 사용할 때의 특별한 이점은 없습니다. 그러나 태그 확장을 사용할 수 없는 시나리오, 예를 들어 속성 값이 문자열 형식이 아니어서 형식 변환이 존재하지 않는 경우에는 개체 요소 구문을 사용해야 합니다.

다음은 개체 요소 구문 및 태그 확장 사용의 예제입니다.

[!code-xaml[BindConversionMarkup#1](~/samples/snippets/csharp/VS_Snippets_Wpf/BindConversionMarkup/CSharp/Page1.xaml#1)]

이 예제에서는 바인딩하는 <xref:System.Windows.Controls.TextBlock.Foreground%2A> 확장 구문을 사용 하 여 바인딩을 선언 하 여 속성. 바인딩 선언은 <xref:System.Windows.Controls.TextBlock.Text%2A> 속성 개체 요소 구문을 사용 합니다.

다양한 용어에 대한 자세한 내용은 [XAML 구문 정보](../advanced/xaml-syntax-in-detail.md)를 참조하세요.

<a name="MBandPB"></a>

### <a name="multibinding-and-prioritybinding"></a>MultiBinding 및 PriorityBinding

<xref:System.Windows.Data.MultiBinding> 및 <xref:System.Windows.Data.PriorityBinding> XAML 확장 구문을 지원 하지 않습니다. 따라서 선언 하는 경우 개체 요소 구문을 사용 해야 합니다 있습니다를 <xref:System.Windows.Data.MultiBinding> 또는 <xref:System.Windows.Data.PriorityBinding> XAML에서.

<a name="BindinginCode"></a>

## <a name="creating-a-binding-in-code"></a>코드에서 바인딩 만들기

바인딩을 지정 하는 또 다른 방법은 속성을 직접 설정 하는 것을 <xref:System.Windows.Data.Binding> 코드의 개체입니다. 다음 예제에서는 만드는 방법을 보여 줍니다는 <xref:System.Windows.Data.Binding> 개체 및 코드에서 속성을 지정 합니다.  이 예에서 `TheConverter` 를 구현 하는 개체는 <xref:System.Windows.Data.IValueConverter> 인터페이스입니다.

[!code-csharp[BindConversion#1](~/samples/snippets/csharp/VS_Snippets_Wpf/BindConversion/CSharp/Window1.xaml.cs#1)]
[!code-vb[BindConversion#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BindConversion/visualbasic/window1.xaml.vb#1)]

바인딩하는 개체가 <xref:System.Windows.FrameworkElement> 또는 <xref:System.Windows.FrameworkContentElement> 호출할 수 있습니다 합니다 `SetBinding` 메서드를 사용 하는 대신 직접 개체 <xref:System.Windows.Data.BindingOperations.SetBinding%2A?displayProperty=nameWithType>합니다. 예제는 [코드에서 바인딩 만들기](how-to-create-a-binding-in-code.md)를 참조하세요.

<a name="Path_Syntax"></a>

## <a name="binding-path-syntax"></a>바인딩 경로 구문

사용 된 <xref:System.Windows.Data.Binding.Path%2A> 속성에 바인딩할 원본 값을 지정 하려면:

- 가장 간단한 경우에는 <xref:System.Windows.Data.Binding.Path%2A> 속성 값이 같은 바인딩에 사용할 소스 개체의 속성 이름을 `Path=PropertyName`입니다.

- 와 같이 유사한 구문을 사용 하 여 속성의 하위 속성을 지정할 수 있습니다 C#입니다. 예를 들어 `Path=ShoppingCart.Order` 절은 개체 또는 속성 `ShoppingCart`의 하위 속성 `Order`에 대한 바인딩을 설정합니다.

- 연결된 속성에 바인딩하려면 연결된 속성을 괄호로 묶습니다. 예를 들어 연결된 된 속성에 바인딩할 <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType>, 구문은 `Path=(DockPanel.Dock)`합니다.

- 속성의 인덱서는 인덱서가 적용되는 속성 이름 뒤에 대괄호로 묶어서 지정할 수 있습니다. 예를 들어 `Path=ShoppingCart[0]` 절은 속성의 내부 인덱싱에서 리터럴 문자열 "0"을 처리하는 방법에 해당하는 인덱스에 대한 바인딩을 설정합니다. 중첩된 인덱서도 지원됩니다.

- `Path=ShoppingCart.ShippingInfo[MailingAddress,Street].`와 같이 `Path` 절에서 인덱서와 하위 속성을 혼합할 수 있습니다.

- 여러 인덱서 매개 변수를 쉼표(,)로 구분하여 인덱서 안에 포함할 수 있습니다. 각 매개 변수의 형식은 괄호를 사용하여 지정할 수 있습니다. 예를 들어 `Path="[(sys:Int32)42,(sys:Int32)24]"`를 사용할 수 있으며 여기서 `sys`는 `System` 네임스페이스에 매핑됩니다.

- 소스가 컬렉션 뷰인 경우 슬래시(/)를 사용하여 현재 항목을 지정할 수 있습니다. 예를 들어 `Path=/` 절은 뷰의 현재 항목에 대한 바인딩을 설정합니다. 소스가 컬렉션인 경우 이 구문은 기본 컬렉션 뷰의 현재 항목을 지정합니다.

- 속성 이름과 슬래시를 결합하여 컬렉션인 속성을 트래버스할 수 있습니다. 예를 들어 `Path=/Offices/ManagerName`은 소스 컬렉션의 현재 항목을 지정하며 여기에는 컬렉션인 `Offices` 속성이 포함됩니다. 현재 항목은 `ManagerName` 속성을 포함하는 개체입니다.

- 필요에 따라 마침표(.) 경로를 사용하여 현재 소스에 바인딩할 수 있습니다. 예를 들어 `Text="{Binding}"`은 `Text="{Binding Path=.}"`와 같습니다.

### <a name="escaping-mechanism"></a>이스케이프 메커니즘

- 인덱서([ ]) 안의 캐럿 문자(^)는 다음 문자를 이스케이프합니다.

- 설정한 경우 <xref:System.Windows.Data.Binding.Path%2A> XAML에도 해야 이스케이프 (XML 엔터티 사용) XML 언어 정의와 관련 된 특정 문자:

  - "&" 문자를 이스케이프하려면 `&`를 사용합니다.

  - ">" 태그를 이스케이프하려면 `>`를 사용합니다.

- 또한 태그 확장 구문을 사용하여 특성의 전체 바인딩을 설명하는 경우 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 태그 확장 파서와 관련된 문자를 이스케이프(백슬래시 \\ 사용)해야 합니다.

  - 백슬래시(\\)는 그 자체로 이스케이프 문자입니다.

  - 등호(=)는 속성 값에서 속성 이름을 구분합니다.

  - 쉼표(,)는 속성을 구분합니다.

  - 오른쪽 중괄호(})는 태그 확장의 끝입니다.

<a name="Default"></a>

## <a name="default-behaviors"></a>기본 동작

선언에서 지정되지 않은 경우 기본 동작은 다음과 같습니다.

- 바인딩 소스 값과 바인딩 대상 값 간에 형식을 변환하는 기본 변환기가 만들어집니다. 변환을 만들 수 없는 경우 기본 변환기는 `null`을 반환합니다.

- 설정 하지 않은 경우 <xref:System.Windows.Data.Binding.ConverterCulture%2A>, 바인딩 엔진은는 `Language` 바인딩 대상 개체의 속성입니다. XAML에서 이 값을 명시적으로 설정하지 않은 경우 기본적으로 "en-US"로 설정되거나 페이지 루트 요소(또는 임의의 요소)에서 값이 상속됩니다.

- 바인딩으로 있다면 이미 데이터 컨텍스트가 (예를 들어의 데이터 컨텍스트가 상속 된 부모 요소에서), 및 항목 또는 해당 컨텍스트에 의해 반환 되는 컬렉션에 적합 한 바인딩을 추가 경로 수정 없이 바인딩 선언의 절을 사용 하지를 전혀 가질 수 있습니다. `{Binding}` 이것이 종종 데이터 스타일링에 바인딩이 컬렉션에 대해 작동 하는 위치에 대 한 바인딩이 지정 되는 방법입니다. 자세한 내용은 [바인딩 소스 개요](binding-sources-overview.md)의 "전체 개체를 바인딩 소스로 사용" 섹션을 참조하세요.

- 기본 <xref:System.Windows.Data.Binding.Mode%2A> 간의 단방향 및 양방향 바인딩되는 종속성 속성에 따라 달라 집니다. 바인딩이 원하는 대로 동작하도록 항상 바인딩 모드를 명시적으로 선언할 수 있습니다. 일반적으로 사용자가 편집 가능한 컨트롤 속성에서와 같은 <xref:System.Windows.Controls.TextBox.Text%2A?displayProperty=nameWithType> 및 <xref:System.Windows.Controls.Primitives.RangeBase.Value%2A?displayProperty=nameWithType>, 기본값 양방향 바인딩으로 설정 되지만 대부분의 다른 속성 기본값은 단방향 바인딩으로 합니다.

- 기본값 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 값에 따라 다릅니다 <xref:System.Windows.Data.UpdateSourceTrigger.PropertyChanged> 고 <xref:System.Windows.Data.UpdateSourceTrigger.LostFocus> 도 바인딩된 종속성 속성에 따라 합니다. 대부분의 종속성 속성에 대한 기본값이 <xref:System.Windows.Data.UpdateSourceTrigger.PropertyChanged>인 반면 <xref:System.Windows.Controls.TextBox.Text%2A?displayProperty=nameWithType> 속성의 기본값은 <xref:System.Windows.Data.UpdateSourceTrigger.LostFocus>입니다.

## <a name="see-also"></a>참고자료

- [데이터 바인딩 개요](data-binding-overview.md)
- [방법 항목](data-binding-how-to-topics.md)
- [데이터 바인딩](../advanced/optimizing-performance-data-binding.md)
- [PropertyPath XAML 구문](../advanced/propertypath-xaml-syntax.md)
