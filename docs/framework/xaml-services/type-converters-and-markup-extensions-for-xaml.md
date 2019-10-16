---
title: XAML을 위한 형식 변환기 및 태그 확장
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [XAML Services], type converter services
- XAML [XAML Services], value converters
- XAML [XAML Services], markup extension services
- value converters for XAML [XAML Services]
- XAML [XAML Services], service context
ms.assetid: db07a952-05ce-4aa4-b6f9-aac7397d0326
ms.openlocfilehash: dee5ec65993cf20cb57377694f61af092b0ccf26
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69939696"
---
# <a name="type-converters-and-markup-extensions-for-xaml"></a>XAML을 위한 형식 변환기 및 태그 확장
형식 변환기 및 태그 확장은 XAML 형식 시스템과 XAML 작성기가 개체 그래프 구성 요소를 생성하는 데 사용하는 두 가지 기술입니다. 일부 특징을 공유하지만 형식 변환기 및 태그 확장은 XAML 노드 스트림에서 다르게 표현됩니다. 이 설명서 집합에서는 때때로 형식 변환기, 태그 확장 및 유사한 구문을 총체적으로 값 변환기라고 합니다.  
  
<a name="value_converters"></a>   
## <a name="value-converters"></a>값 변환기  
 XAML에서 값 변환기는 다양한 시나리오에 사용됩니다. 다음 목록에서는 XAML의 다양한 값 변환기 유형을 보여 줍니다.  
  
- 형식 변환기  
  
- 태그 확장  
  
- 값 직렬 변환기  
  
- XAML 텍스트 구문에 대한 논리를 제공하는 관련 클래스 또는 지원 클래스  
  
<a name="type_converters"></a>   
## <a name="type-converters"></a>형식 변환기  
 .NET Framework XAML 서비스 정의에서 형식 변환기는 CLR <xref:System.ComponentModel.TypeConverter> 클래스에서 파생되는 클래스입니다. <xref:System.ComponentModel.TypeConverter>는 XAML이 존재 하기 전에 Microsoft .NET 프레임 워크에 있던 클래스입니다. 원래 용도는 IDE 속성에 대해 속성 창 및 유사한 텍스트 기반 편집 메타포를 지 원하는 것 이었습니다. .NET Framework에 XAML을 도입하는 경우 <xref:System.ComponentModel.TypeConverter> 를 사용하여 텍스트 구문(특성 값 또는 XAML 값 노드에 있음)을 개체로 변환합니다. <xref:System.ComponentModel.TypeConverter> 를 사용하여 개체 값을 텍스트 구문으로 직렬화할 수도 있습니다. <xref:System.ComponentModel.TypeConverter>는 Windows Presentation Foundation (WPF) 및 Windows Communication Foundation (WCF)의 이전 프레임 워크 관련 XAML 구현 에서도 사용 되었습니다. XAML의 <xref:System.ComponentModel.TypeConverter> 에 대한 자세한 내용은 [Type Converters for XAML Overview](type-converters-for-xaml-overview.md)의 이전 프레임워크별 XAML 구현에서도 사용되었습니다.  
  
<a name="markup_extensions"></a>   
## <a name="markup-extensions"></a>태그 확장  
 .NET Framework XAML 서비스 구현에서 태그 확장은 <xref:System.Windows.Markup.MarkupExtension> 클래스에서 파생되는 클래스입니다. 태그 확장은 이 폼에서 XAML 언어에 의해 시작되는 개념입니다. 태그 확장은 논리 제공을 위해 서비스 클래스를 호출하는 확장 가능한 이스케이프 시퀀스와 같은 것으로 간주할 수 있습니다. 태그 측면에서 XAML 프로세서는 텍스트 문자열에서 여는 중괄호({)로 시작하는 텍스트 시퀀스를 통해 태그 확장을 보편적으로 인식합니다.  
  
 태그 확장은 형식 변환기와 다릅니다. 형식 변환기는 일반적으로 형식 또는 멤버와 연결됩니다. 개체 그래프를 만들거나 직렬화 시 해당 엔터티와 연결된 텍스트 구문이 발견될 때 호출됩니다.  
  
 태그 확장은 단일 지원 서비스 클래스와 연결되지만 모든 멤버 값에 대해 적용할 수 있습니다. 그러나 서비스 컨텍스트를 사용하여 의도적으로 특정 멤버 또는 대상 형식에만 제한적으로 사용되도록 태그 확장을 구현할 수 있습니다. 태그 확장은 형식 변환기 연결을 재정의할 수 있습니다. 또는 그렇지 않을 경우 텍스트 구문을 지원하지 않는 멤버에 대한 특성 값을 지정하는 데 사용할 수 있습니다.  
  
 XAML에 대한 태그 확장 구현 패턴에 대한 자세한 내용은 [Markup Extensions for XAML Overview](markup-extensions-for-xaml-overview.md).  
  
> [!NOTE]
> <xref:System.Windows.Markup.MarkupExtension> 및 <xref:System.Windows.Markup.ValueSerializer> 형식은 둘 다 <xref:System.Windows.Markup> 네임스페이스에 있고 <xref:System.Xaml> 네임스페이스에는 없습니다. 이는 이러한 형식이 문자열 `Windows`을 포함 하는 CLR 네임 스페이스를 채우는 WPF 또는 Windows Forms 기술에만 적용 되는 것을 의미 하지는 않습니다. <xref:System.Windows.Markup.MarkupExtension> 및 <xref:System.Windows.Markup.ValueSerializer> 는 System.Xaml 어셈블리에 있으며 특정 프레임워크 종속성이 없습니다. 이러한 형식은 .NET Framework 3.0에 대 한 CLR 네임 스페이스에 있었으며 .NET Framework 4의 CLR 네임 스페이스에 남아 있으므로 기존 WPF 프로젝트의 참조가 손상 되지 않습니다. 자세한 내용은 [Types Migrated from WPF to System.Xaml](types-migrated-from-wpf-to-system-xaml.md)을 참조하세요.  
  
<a name="value_serializers"></a>   
## <a name="value-serializers"></a>값 직렬 변환기  
 <xref:System.Windows.Markup.ValueSerializer> 는 개체를 문자열로 변환하는 작업에 최적화된 특수 형식 변환기입니다. XAML용 <xref:System.Windows.Markup.ValueSerializer> 는 `ConvertFrom` 메서드를 구현하지 않을 수도 있습니다. <xref:System.Windows.Markup.ValueSerializer> 구현은 <xref:System.ComponentModel.TypeConverter> 구현과 유사한 방식으로 서비스를 가져옵니다. 가상 메서드는 입력 `context` 매개 변수를 제공합니다. `context` 매개 변수는 <xref:System.Windows.Markup.IValueSerializerContext>인터페이스에서 상속되고 <xref:System.IServiceProvider> 메서드를 포함하는 <xref:System.IServiceProvider.GetService%2A> 형식입니다.  
  
 XAML 형식 시스템에서 직렬화를 위해 XAML 노드 루프 처리를 사용하는 XAML 작성기 구현의 경우 형식 또는 멤버와 연결된 값 변환기가 자체 <xref:System.Xaml.XamlType.ValueSerializer%2A?displayProperty=nameWithType> 속성에 의해 보고됩니다. 직렬화를 수행하는 XAML 작성기에 대한 의미는 <xref:System.Xaml.XamlType.TypeConverter%2A?displayProperty=nameWithType> 및 <xref:System.Xaml.XamlType.ValueSerializer%2A?displayProperty=nameWithType> 가 있을 경우 부하 경로에 대해 형식 변환기를 사용해야 하고 저장 경로에 대해 값 직렬 변환기를 사용해야 한다는 것입니다. <xref:System.Xaml.XamlType.TypeConverter%2A?displayProperty=nameWithType> 가 있지만 <xref:System.Xaml.XamlType.ValueSerializer%2A?displayProperty=nameWithType> 가 `null`이면 저장 경로에도 형식 변환기가 사용됩니다.  
  
<a name="other_value_converters"></a>   
## <a name="other-value-converters"></a>기타 값 변환기  
 값 변환기는 형식 변환기 또는 태그 확장의 특정 패턴 이상으로 확장할 수 있습니다. 그러나 이러한 사용자 지정을 수행하려면 .NET Framework XAML 서비스에서 제공하는 XAML 형식 시스템도 재정의해야 합니다. 기존 XAML 형식 시스템은 형식 변환기, 태그 확장 및 값 직렬 변환기에 대한 표현 및 보고 시스템을 포함하지만 사용자 지정 형식의 값 변환에 대한 표현 및 보고 시스템은 없습니다. 사용자 지정 값 변환기를 만들려는 경우 <xref:System.Xaml.Schema.XamlValueConverter%601> 형식을 사용합니다.  
  
<a name="type_converters_and_markup_extensions_in_combination"></a>   
## <a name="type-converters-and-markup-extensions-in-combination"></a>형식 변환기 및 태그 확장 조합  
 태그 확장 및 형식 변환기는 XAML에서 다양한 상황에 사용됩니다. 태그 확장 사용에 컨텍스트를 사용할 수는 있지만 태그 확장에서 값을 제공하는 속성의 형식 변환 동작은 일반적으로 태그 확장 구현에서 확인되지 않습니다. 즉, 태그 확장에서 텍스트 문자열을 해당 `ProvideValue` 출력으로 반환하는 경우에도 특정 속성 또는 속성 값 형식에 적용될 때 해당 문자열의 형식 변환 동작은 호출되지 않습니다. 일반적으로 태그 확장의 목적은 문자열을 처리하고 관련된 형식 변환기 없이 개체를 반환하는 것입니다.  
  
<a name="service_context_for_a_value_converter"></a>   
## <a name="service-context-for-a-value-converter"></a>값 변환기에 대한 서비스 컨텍스트  
 값 변환기를 구현할 때 값 변환기가 적용되는 컨텍스트에 액세스해야 하는 경우가 많습니다. 이 컨텍스트를 서비스 컨텍스트라고 합니다. 서비스 컨텍스트에는 활성 XAML 스키마 컨텍스트와 같은 정보, XAML 스키마 컨텍스트 및 XAML 개체 작성기에서 제공하는 형식 매핑 시스템에 대한 액세스 권한 등이 포함될 수 있습니다. 값 변환기에 사용 가능한 서비스 컨텍스트 및 서비스 컨텍스트에서 제공하는 서비스에 액세스하는 방법에 대한 자세한 내용은 [형식 변환기 또는 태그 확장에서 사용할 수 있는 서비스 컨텍스트](service-contexts-available-to-type-converters-and-markup-extensions.md)를 참조하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Markup.MarkupExtension>
- <xref:System.Xaml.XamlObjectWriter>
- [XAML 태그 확장명 개요](markup-extensions-for-xaml-overview.md)
- [XAML을 위한 형식 변환기 개요](type-converters-for-xaml-overview.md)
- [Service Contexts Available to Type Converters and Markup Extensions](service-contexts-available-to-type-converters-and-markup-extensions.md)
