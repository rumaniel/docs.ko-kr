---
title: 종속성 속성 개요
description: WPF 속성 시스템에서 지원하는 속성을 종속성 속성이라고 합니다. 이 개요에서는 WPF 속성 시스템 및 종속성 속성의 기능에 대해 설명합니다.
ms.date: 06/06/2018
dev_langs:
- csharp
- vb
helpviewer_keywords:
- properties [WPF], attached
- properties [WPF], overview
- styles [WPF]
- attached properties [WPF]
- data binding [WPF]
- dependency properties [WPF]
- resources [WPF], references to
ms.assetid: d119d00c-3afb-48d6-87a0-c4da4f83dee5
ms.openlocfilehash: b7401cd3e9551b378983193f4c5e8e4107954b74
ms.sourcegitcommit: 24a4a8eb6d8cfe7b8549fb6d823076d7c697e0c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68401421"
---
# <a name="dependency-properties-overview"></a>종속성 속성 개요

WPF(Windows Presentation Foundation)에서는 형식의 [속성](../../../standard/base-types/common-type-system.md#Properties) 기능을 확장하는 데 사용할 수 있는 서비스 집합을 제공합니다. 일반적으로 이러한 서비스를 WPF 속성 시스템이라고 통칭합니다. WPF 속성 시스템에서 지원하는 속성을 종속성 속성이라고 합니다. 이 개요에서는 WPF 속성 시스템 및 종속성 속성의 기능에 대해 설명합니다. XAML 및 코드에서 기존 종속성 속성을 사용하는 방법도 설명합니다. 또한 이 개요에서는 종속성 속성 메타데이터 같은 종속성 속성의 특수한 측면과 사용자 지정 클래스에서 종속성 속성을 직접 만드는 방법을 소개합니다.

## <a name="prerequisites"></a>필수 구성 요소
이 항목에서는 .NET 형식 시스템 및 개체 지향 프로그래밍에 대한 기본 지식이 있다고 가정합니다. 이 항목의 예제를 따르려면 XAML을 이해하고 WPF 애플리케이션을 작성하는 방법도 알아야 합니다. 자세한 내용은 [연습: 내 첫 번째 WPF 데스크톱](../getting-started/walkthrough-my-first-wpf-desktop-application.md)응용 프로그램입니다.  
  
## <a name="dependency-properties-and-clr-properties"></a>종속성 속성 및 CLR 속성
 WPF에서 속성은 일반적으로 표준 .NET [속성](../../../standard/base-types/common-type-system.md#Properties)으로 노출됩니다. 기본 수준에서는 이러한 속성을 직접 조작할 수 있으며 종속성 속성으로 구현되는지를 알 수 없습니다. 그러나 WPF 속성 시스템 기능의 일부 또는 전체를 잘 알고 있어야 이러한 기능을 활용할 수 있습니다.

종속성 속성의 용도는 다른 입력 값을 기반으로 속성의 값을 계산하는 방법을 제공하는 것입니다. 이러한 다른 입력에는 테마 및 사용자 기본 설정과 같은 시스템 속성, 데이터 바인딩 및 애니메이션/스토리보드 같은 just-in-time 속성 결정 메커니즘, 리소스 및 스타일 같은 여러 용도의 템플릿, 요소 트리의 다른 요소와 부모-자식 관계를 통해 알려진 값 등이 포함될 수 있습니다. 또한 종속성 속성은 자체 포함 유효성 검사, 기본값, 다른 속성의 변경 내용을 모니터링하는 콜백 및 잠재적으로 런타임 정보에 따라 속성 값을 강제 변환할 수 있는 시스템을 제공하도록 구현할 수 있습니다. 파생 클래스는 기존 속성의 실제 구현을 재정의하거나 새 속성을 만드는 대신 종속성 속성 메타데이터를 재정의하여 기존 속성의 특정 특성을 변경할 수도 있습니다.

SDK 참조에서는 속성에 대한 관리되는 참조 페이지에 [종속성 속성 정보] 섹션이 있는지 여부에 따라 해당 속성이 종속성 속성인지를 식별할 수 있습니다. 종속성 속성 정보 섹션에는 해당 종속성 속성의 <xref:System.Windows.DependencyProperty> 식별자 필드에 대한 링크가 포함되어 있으며, 해당 속성에 대해 설정되는 메타데이터 옵션 목록, 클래스별 재정의 정보 및 기타 정보도 포함되어 있습니다.

## <a name="dependency-properties-back-clr-properties"></a>종속성 속성의 CLR 속성 지원
종속성 속성 및 WPF 속성 시스템은 private 필드로 속성을 지원하는 표준 패턴에 대한 대체 구현으로 속성을 지원하는 형식을 제공하여 속성 기능을 확장합니다. 이 형식의 이름은 <xref:System.Windows.DependencyProperty>입니다. WPF 속성 시스템을 정의하는 다른 중요한 형식은 <xref:System.Windows.DependencyObject>입니다. <xref:System.Windows.DependencyObject>는 종속성 속성을 등록하고 소유할 수 있는 기본 클래스를 정의합니다.

다음은 종속성 속성에 사용되는 용어를 나열합니다.

- **종속성 속성:** 에 <xref:System.Windows.DependencyProperty>의해 지원 되는 속성입니다.

- **종속성 속성 식별자:** 종속성 속성을 등록할 때 반환 값으로 가져온 다음 클래스의 정적 멤버로 저장 되는 인스턴스입니다.<xref:System.Windows.DependencyProperty> 이 식별자는 WPF 속성 시스템과 상호 작용하는 많은 API에 대한 매개 변수로 사용됩니다.

- **CLR "래퍼":** 속성에 대 한 실제 get 및 set 구현입니다. 이러한 구현은 <xref:System.Windows.DependencyObject.GetValue%2A> 및 <xref:System.Windows.DependencyObject.SetValue%2A> 호출에서 종속성 속성 식별자를 사용하여 이 식별자를 통합하므로 WPF 속성 시스템을 사용하는 속성에 대한 지원을 제공합니다.

다음 예제에서는 `IsSpinning` 종속성 속성을 정의하고 <xref:System.Windows.DependencyProperty> 식별자와 이 식별자가 지원하는 속성의 관계를 보여 줍니다.

[!code-csharp[PropertiesOvwSupport#DPFormBasic](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page4.xaml.cs#dpformbasic)]
[!code-vb[PropertiesOvwSupport#DPFormBasic](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertiesOvwSupport/visualbasic/page4.xaml.vb#dpformbasic)]  
  
속성과 해당 지원 <xref:System.Windows.DependencyProperty> 필드의 명명 규칙은 중요합니다. 필드의 이름은 항상 접미사 `Property`가 추가된 속성의 이름입니다. 이 규칙과 그 이유에 대한 자세한 내용은 [사용자 지정 종속성 속성](custom-dependency-properties.md)을 참조하세요.  

## <a name="setting-property-values"></a>속성 값 설정
속성은 코드 또는 XAML에서 설정할 수 있습니다.

### <a name="setting-property-values-in-xaml"></a>XAML에서 속성 값 설정 
다음 XAML 예제에서는 빨간색으로 단추의 배경색을 지정합니다. 이 예제에서는 XAML 특성에 대한 간단한 문자열 값이 WPF XAML 파서에 의해 생성된 코드에서 WPF 형식(<xref:System.Windows.Media.SolidColorBrush>를 통한 <xref:System.Windows.Media.Color>)으로 형식 변환되는 경우를 보여 줍니다.

[!code-xaml[PropertiesOvwSupport#MostBasicProperty](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/Page1.xaml#mostbasicproperty)]

XAML은 속성을 설정하는 다양한 구문 형식 지원 특정 속성에 사용할 구문은 형식 변환기의 존재 여부와 같은 다른 요소뿐만 아니라 속성에서 사용하는 값 형식에 따라 달라집니다. 속성 설정을 위한 XAML 구문에 대한 자세한 내용은 [XAML 개요(WPF)](xaml-overview-wpf.md) 및 [XAML 구문 정보](xaml-syntax-in-detail.md)를 참조하세요.

비 특성 구문 예제로 다음 XAML 예제에서는 또 다른 단추 배경을 보여 줍니다. 이번에는 간단한 단색을 설정하는 대신 배경을 이미지로 설정하여 해당 이미지와 해당 이미지의 소스를 나타내는 요소가 중첩된 요소의 특성으로 지정됩니다. 이 예제는 속성 요소 구문의 예제입니다.

[!code-xaml[PropertiesOvwSupport#PESyntaxProperty](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/Page1.xaml#pesyntaxproperty)]

### <a name="setting-properties-in-code"></a>코드에서 속성 설정
 코드에서 종속성 속성 값을 설정 하는 것은 일반적으로 CLR "래퍼"에 의해 노출 되는 집합 구현에 대 한 호출입니다.

[!code-csharp[PropertiesOvwSupport#ProceduralPropertySet](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/Page1.xaml.cs#proceduralpropertyset)]
[!code-vb[PropertiesOvwSupport#ProceduralPropertySet](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertiesOvwSupport/visualbasic/page1.xaml.vb#proceduralpropertyset)]

또한 속성 값을 가져오려면 기본적으로 get "래퍼" 구현을 호출합니다.

[!code-csharp[PropertiesOvwSupport#ProceduralPropertyGet](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/Page1.xaml.cs#proceduralpropertyget)]
 [!code-vb[PropertiesOvwSupport#ProceduralPropertyGet](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertiesOvwSupport/visualbasic/page1.xaml.vb#proceduralpropertyget)]

속성 시스템 api <xref:System.Windows.DependencyObject.GetValue%2A> <xref:System.Windows.DependencyObject.SetValue%2A> 를 직접 호출할 수도 있습니다. 이는 일반적으로 기존 속성을 사용 하는 경우에는 필요 하지 않습니다 (래퍼가 더 편리 하 고 개발자 도구에 대 한 속성을 더 잘 제공 함). 그러나 Api를 직접 호출 하는 것이 특정 시나리오에 적합 합니다.

또한 속성은 XAML에서 설정한 다음 나중에 코드 숨김을 통해 코드에서 액세스할 수 있습니다. 자세한 내용은 [WPF의 코드 숨김 및 XAML](code-behind-and-xaml-in-wpf.md)을 참조하세요.

## <a name="property-functionality-provided-by-a-dependency-property"></a>종속성 속성이 제공하는 속성 기능
종속성 속성은 필드에서 지원하는 속성과 반대로 속성의 기능을 확장하는 기능을 제공합니다. 종종 이러한 기능은 다음과 같은 특정 기능 중 하나를 지원하거나 나타냅니다.

- [리소스](#resources)

- [데이터 바인딩](#data-binding)

- [스타일](#styles)

- [애니메이션](#animations)

- [메타데이터 재정의](#metadata-overrides)

- [속성 값 상속](#property-value-inheritance)

- [WPF Designer 통합](#wpf-designer-integration)

### <a name="resources"></a>리소스
종속성 속성 값은 리소스를 참조하여 설정할 수 있습니다. 일반적으로 리소스는 페이지 루트 요소 또는 애플리케이션의 `Resources` 속성 값으로 지정됩니다. 이러한 위치를 통해 리소스에 가장 편리하게 액세스할 수 있습니다. 다음 예제에서는 <xref:System.Windows.Media.SolidColorBrush> 리소스를 정의하는 방법을 보여 줍니다.

[!code-xaml[PropertiesOvwSupport#ResourcesResource](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page2.xaml#resourcesresource)]

리소스가 정의되면 리소스를 참조하고 사용하여 속성 값을 제공할 수 있습니다.

[!code-xaml[PropertiesOvwSupport#ResourcesReference](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page2.xaml#resourcesreference)]

이 특정 리소스는 [DynamicResource 태그 확장](dynamicresource-markup-extension.md)으로 참조됩니다. WPF XAML에서는 정적 또는 동적 리소스 참조를 사용할 수 있습니다. 동적 리소스 참조를 사용하려면 종속성 속성으로 설정되어 있어야 합니다. 구체적으로 WPF 속성 시스템에서 사용하는 동적 리소스 참조 사용입니다. 자세한 내용은 [XAML 리소스](xaml-resources.md)를 참조하세요.

> [!NOTE]
> 리소스는 로컬 값으로 처리되며, 다른 로컬 값을 설정하면 리소스 참조가 제거됩니다. 자세한 내용은 [종속성 속성 값 우선 순위](dependency-property-value-precedence.md)를 참조하세요.

### <a name="data-binding"></a>데이터 바인딩
종속성 속성은 데이터 바인딩을 통해 값을 참조할 수 있습니다. 데이터 바인딩은 XAML의 특정 태그 확장 구문이나 코드의 <xref:System.Windows.Data.Binding> 개체를 통해 작동합니다. 데이터 바인딩을 사용하면 데이터 소스에서 값을 가져오는 시간인 런타임까지 최종 속성 값 결정이 지연됩니다.

다음 예에서는 XAML에서 선언된 바인딩을 사용하여 <xref:System.Windows.Controls.Button>에 대한 <xref:System.Windows.Controls.ContentControl.Content%2A> 속성을 설정합니다. 바인딩은 상속된 데이터 컨텍스트 및 <xref:System.Windows.Data.XmlDataProvider> 데이터 원본(표시되지 않음)을 사용합니다. 바인딩 자체는 데이터 소스 내에서 <xref:System.Windows.Data.Binding.XPath%2A>로 원하는 소스 속성을 지정합니다.

[!code-xaml[PropertiesOvwSupport#BasicInlineBinding](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page3.xaml#basicinlinebinding)]

> [!NOTE]
> 바인딩은 로컬 값으로 처리되며, 다른 로컬 값을 설정하면 바인딩이 제거됩니다. 자세한 내용은 [종속성 속성 값 우선 순위](dependency-property-value-precedence.md)를 참조하세요.

종속성 속성, 즉 <xref:System.Windows.DependencyObject> 클래스는 데이터 바인딩 작업에 대한 <xref:System.Windows.DependencyObject> 소스 속성 값의 변경 내용에 대해 알림을 생성하는 용도로 <xref:System.ComponentModel.INotifyPropertyChanged>를 기본적으로 지원하지 않습니다. 데이터 바인딩 대상의 변경 내용을 보고할 수 있도록 데이터 바인딩에서 사용할 속성을 만드는 방법에 대한 자세한 내용은 [데이터 바인딩 개요](../data/data-binding-overview.md)를 참조하세요.

### <a name="styles"></a>스타일
스타일과 템플릿은 종속성 속성 사용에 대한 주요 시나리오 중 두 가지입니다. 스타일은 애플리케이션 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]를 정의하는 속성을 설정하는 데 특히 유용합니다. 스타일은 일반적으로 XAML의 리소스로 정의됩니다. 일반적으로 스타일은 또 다른 속성에 대한 실시간 값에 따라 속성 값을 변경하는 "트리거"뿐만 아니라 특정 속성에 대한 "setter"를 포함하기 때문에 속성 시스템과 상호 작용합니다.

다음 예제에서는 매우 간단한 스타일(<xref:System.Windows.FrameworkElement.Resources%2A> 사전 내에서 정의되지만 표시되지 않는)을 만든 다음, 직접 해당 스타일을 <xref:System.Windows.Controls.Button>에 대한 <xref:System.Windows.FrameworkElement.Style%2A> 속성에 적용합니다. 스타일 내의 setter는 스타일이 적용된 <xref:System.Windows.Controls.Button>에 대한 <xref:System.Windows.Controls.Control.Background%2A> 속성을 녹색으로 설정합니다.

[!code-xaml[PropertiesOvwSupport#SimpleStyleDef](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page3.xaml#simplestyledef)]

[!code-xaml[PropertiesOvwSupport#SimpleStyle](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page3.xaml#simplestyle)]

자세한 내용은 [스타일 지정 및 템플릿](../controls/styling-and-templating.md)을 참조하세요.

### <a name="animations"></a>애니메이션
종속성 속성에 애니메이션을 적용할 수 있습니다. 애니메이션을 적용하고 실행하면 애니메이션된 값이 속성의 다른 모든 값(예: 로컬 값)보다 높은 우선 순위로 작동합니다.

다음 예제에서는 <xref:System.Windows.Controls.Button> 속성에 대한 <xref:System.Windows.Controls.Control.Background%2A>에 애니메이션을 적용합니다(기술적으로 빈 <xref:System.Windows.Media.SolidColorBrush>를 <xref:System.Windows.Controls.Control.Background%2A>로 지정하려면 <xref:System.Windows.Controls.Control.Background%2A>는 속성 요소 구문을 사용하여 애니메이션을 적용한 다음, 해당 <xref:System.Windows.Media.SolidColorBrush>의 <xref:System.Windows.Media.SolidColorBrush.Color%2A> 속성은 직접 애니메이션이 적용된 속성이 됩니다).

[!code-xaml[PropertiesOvwSupport#MiniAnimate](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page3.xaml#minianimate)]

속성에 애니메이션을 적용하는 방법에 대한 자세한 내용은 [애니메이션 개요](../graphics-multimedia/animation-overview.md) 및 [스토리보드 개요](../graphics-multimedia/storyboards-overview.md)를 참조하세요.

### <a name="metadata-overrides"></a>메타데이터 재정의
원래 종속성 속성을 등록하는 클래스에서 파생시킬 때 해당 속성에 대한 메타데이터를 재정의하여 종속성 속성의 특정 동작을 변경할 수 있습니다. 메타데이터 재정의는 <xref:System.Windows.DependencyProperty> 식별자에 따라 다릅니다. 메타데이터 재정의에서는 속성을 다시 구현할 필요가 없습니다. 메타데이터 변경은 기본적으로 속성 시스템에서 처리됩니다. 각 클래스는 잠재적으로 기본 클래스에서 상속되는 모든 속성에 대해 개별 메타데이터를 형식별로 보유합니다.

다음 예제에서는 종속성 속성 <xref:System.Windows.FrameworkElement.DefaultStyleKey%2A>에 대한 메타데이터를 재정의합니다. 이 특정 종속성 속성 메타데이터 재정의는 테마에서 기본 스타일을 사용할 수 있는 컨트롤을 만드는 구현 패턴의 일부입니다.

[!code-csharp[PropertiesOvwSupport#OverrideMetadata](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page3.xaml.cs#overridemetadata)]
[!code-vb[PropertiesOvwSupport#OverrideMetadata](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertiesOvwSupport/visualbasic/page3.xaml.vb#overridemetadata)]

속성 메타데이터 재정의 또는 가져오기에 대한 자세한 내용은 [종속성 속성 메타데이터](dependency-property-metadata.md)를 참조하세요.

### <a name="property-value-inheritance"></a>속성 값 상속
요소는 개체 트리의 부모에서 종속성 속성의 값을 상속할 수 있습니다.

> [!NOTE]
> 속성 값 상속 동작은 모든 종속성 속성에 전역으로 사용되지는 않는데 상속에 대한 계산 시간이 일부 성능에 영향을 주기 때문입니다. 속성 값 상속은 일반적으로 특정 시나리오에서 속성 값 상속이 적절하다고 제안하는 속성에만 사용됩니다. 종속성 속성이 상속되는지 여부는 SDK 참조에서 해당 종속성 속성에 대한 **종속성 속성 정보** 섹션을 통해 확인할 수 있습니다.

다음 예제에서는 이전 바인딩 예제에 표시되지 않은 바인딩을 보여 주며 바인딩의 소스를 지정하는 <xref:System.Windows.FrameworkElement.DataContext%2A> 속성을 설정합니다. 자식 개체의 모든 후속 바인딩은 소스를 지정할 필요가 없으며, 부모 <xref:System.Windows.Controls.StackPanel> 개체의 <xref:System.Windows.FrameworkElement.DataContext%2A>에서 상속된 값을 사용할 수 있습니다. (또는 자식 개체는 대신 <xref:System.Windows.Data.Binding>에서 고유의 <xref:System.Windows.FrameworkElement.DataContext%2A> 또는 <xref:System.Windows.Data.Binding.Source%2A>를 직접 지정하고 바인딩의 데이터 컨텍스트에 대한 상속된 값을 사용하지 않도록 선택할 수 있습니다.)

[!code-xaml[PropertiesOvwSupport#InheritanceContext](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page3.xaml#inheritancecontext)]

자세한 내용은 [속성 값 상속](property-value-inheritance.md)을 참조하세요.

### <a name="wpf-designer-integration"></a>WPF Designer 통합
종속성 속성으로 구현되는 속성이 있는 사용자 지정 컨트롤은 적절한 [!INCLUDE[wpfdesigner_current_long](../../../../includes/wpfdesigner-current-long-md.md)] 지원을 받습니다. 한 가지 예는 **속성** 창을 사용하여 직접 및 연결된 종속성 속성을 편집하는 기능입니다. 자세한 내용은 [컨트롤 제작 개요](../controls/control-authoring-overview.md)를 참조하십시오.

## <a name="dependency-property-value-precedence"></a>종속성 속성 값 우선 순위
종속성 속성의 값을 가져오면 WPF 속성 시스템에 참여하는 다른 속성 기반 입력 중 하나를 통해 해당 속성에 설정된 값을 가져오는 것입니다. 종속성 속성 값 우선 순위는 속성이 해당 값을 가져오는 방법에 대한 다양한 시나리오가 예측 가능한 방식으로 상호 작용할 수 있도록 존재합니다.

다음 예제를 살펴보십시오. 예제는 모든 단추 및 해당 <xref:System.Windows.Controls.Control.Background%2A> 속성에 적용되는 스타일을 포함하지만 또한 로컬로 설정된 <xref:System.Windows.Controls.Control.Background%2A> 값으로 단추 하나를 지정합니다.

> [!NOTE]
> SDK 설명서에서는 종속성 속성에 대해 설명할 때 경우에 따라 "로컬 값" 또는 "로컬로 설정된 값"이라는 용어를 사용합니다. 로컬로 설정된 값은 코드의 개체 인스턴스에서 직접 설정되거나 XAML의 요소에 대한 특성으로 설정되는 속성 값입니다.  
  
원칙적으로 첫 번째 단추의 경우 속성은 두 번 설정되지만 값은 우선 순위가 가장 높은 값 하나만 적용됩니다. 로컬로 설정된 값은 우선 순위가 가장 높으므로(실행 중인 애니메이션 제외, 이 예제에서는 애니메이션이 적용되지 않음) style setter 값 대신 첫 번째 단추의 배경에 사용됩니다. 두 번째 단추에는 로컬 값 및 style setter보다 우선 순위가 높은 다른 값이 없으므로 해당 단추의 배경이 style setter에 기반합니다.

[!code-xaml[PropertiesOvwSupport#MiniPrecedence](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page3.xaml#miniprecedence)]  

### <a name="why-does-dependency-property-precedence-exist"></a>종속성 속성 우선 순위의 존재 이유
일반적으로 스타일이 항상 적용되고 개별 요소의 로컬로 설정된 값이 모호해지기를 원하지 않습니다. 그렇지 않으면 일반적으로 스타일이나 요소를 사용하기가 매우 어려워집니다. 따라서 스타일에 기반한 값은 로컬로 설정된 값보다 낮은 우선 순위로 작동합니다. 종속성 속성 목록 및 종속성 속성 유효 값의 출처에 대한 자세한 내용은 [종속성 속성 값 우선 순위](dependency-property-value-precedence.md)를 참조하세요.

> [!NOTE]
> WPF 요소에는 종속성 속성이 아닌 많은 속성이 정의되어 있습니다. 일반적으로 속성은 데이터 바인딩, 스타일 지정, 애니메이션, 기본값 지원, 상속, 연결된 속성, 무효화 등 속성 시스템에서 사용되는 시나리오 중 하나 이상을 지원해야 하는 경우에만 종속성 속성으로 구현되었습니다.

## <a name="learning-more-about-dependency-properties"></a>종속성 속성에 대해 자세히 알아보기  

- 연결된 속성은 XAML에서 특수한 구문을 지원하는 속성의 형식입니다. 연결 된 속성에는 일반적으로 CLR (공용 언어 런타임) 속성과의 1:1 대응이 없으며 종속성 속성이 아닐 수도 있습니다. 연결된 속성의 일반적인 용도는 부모 요소와 자식 요소가 클래스 멤버 목록의 일부로 해당 속성을 소유하지 않는 경우에도 자식 요소가 부모 요소에 속성 값을 보고할 수 있도록 허용하는 것입니다. 한 기본 시나리오는 자식 요소가 부모 요소에게 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]에 표시되는 방법(예를 들어 <xref:System.Windows.Controls.DockPanel.Dock%2A> 또는 <xref:System.Windows.Controls.Canvas.Left%2A> 참조)을 알려주게 하는 것입니다. 자세한 내용은 [연결된 속성 개요](attached-properties-overview.md)를 참조하세요.

- 구성 요소 개발자 또는 애플리케이션 개발자는 데이터 바인딩이나 스타일 지원과 같은 기능을 사용하거나 무효화 및 값 강제 변환을 지원하기 위해 종속성 속성을 직접 만들려고 할 수 있습니다. 자세한 내용은 [사용자 지정 종속성 속성](custom-dependency-properties.md)을 참조하세요.

- 일반적으로 종속성 속성은 인스턴스에 액세스할 수 있는 모든 호출자가 액세스할 수 있거나 적어도 검색할 수 있는 public 속성으로 간주되어야 합니다. 자세한 내용은 [종속성 속성 보안](dependency-property-security.md)을 참조하세요.

## <a name="see-also"></a>참고자료

- [사용자 지정 종속성 속성](custom-dependency-properties.md)
- [읽기 전용 종속성 속성](read-only-dependency-properties.md)
- [XAML 개요(WPF)](xaml-overview-wpf.md)
- [WPF 아키텍처](wpf-architecture.md)
