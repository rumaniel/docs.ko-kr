---
title: 형식 변환기 또는 태그 확장에서 사용할 수 있는 서비스 컨텍스트
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [XAML Services], type converter services how-to
ms.assetid: b4dad00f-03da-4579-a4e9-d8d72d2ccbce
ms.openlocfilehash: 0d4e274ad7b64820e74347908c08c7726e96bbe8
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053838"
---
# <a name="service-contexts-available-to-type-converters-and-markup-extensions"></a>형식 변환기 또는 태그 확장에서 사용할 수 있는 서비스 컨텍스트
형식 변환기 및 태그 확장 사용을 지원하는 형식의 작성자에는 태그 또는 주변 개체 그래프 구조에서 사용하는 경우에 대한 컨텍스트 정보를 포함해야 할 수 있습니다. 제공된 개체를 올바르게 인스턴스화하거나 개체 그래프의 기존 개체에 대한 개체 참조를 만들 수 있도록 정보가 필요할 수 있습니다. .NET Framework XAML 서비스를 사용할 경우 필요할 수 있는 컨텍스트는 일련의 서비스 인터페이스로 표시됩니다. 형식 변환기 또는 태그 확장 지원 코드에서는 <xref:System.Xaml.XamlObjectWriter> 또는 관련 형식에서 사용 가능하고 통과되는 서비스 공급자 컨텍스트를 사용하여 서비스를 쿼리할 수 있습니다. XAML 스키마 컨텍스트는 이러한 한 서비스를 통해 직접 사용할 수 있습니다. 이 항목에서는 값 변환기 구현에서 서비스 컨텍스트에 액세스하는 방법을 설명하고 일반적으로 사용 가능한 서비스 및 해당 역할을 나열합니다.  
  
<a name="obtaining_services"></a>   
## <a name="obtaining-services"></a>서비스 가져오기  
 값 변환기의 구현자는 값 변환기가 적용되는 컨텍스트의 몇몇 형식에 액세스해야 할 수 있습니다. 이 컨텍스트에는 활성 XAML 스키마 컨텍스트와 같은 정보, XAML 스키마 컨텍스트 및 XAML 개체 작성기에서 제공하는 형식 매핑 시스템에 대한 액세스 권한 등이 포함될 수 있습니다. 태그 확장 또는 형식 변환기 구현에 사용할 수 있는 서비스는 각 가상 메서드의 서명 일부인 컨텍스트 매개 변수를 통해 전달됩니다. 모든 경우에 컨텍스트에 <xref:System.IServiceProvider>가 구현되어 있고 <xref:System.IServiceProvider.GetService%2A?displayProperty=nameWithType>를 호출하여 서비스를 요청할 수 있습니다.  
  
<a name="services_for_a_markup_extension"></a>   
## <a name="services-for-a-markup-extension"></a>태그 확장에 대한 서비스  
 <xref:System.Windows.Markup.MarkupExtension> 에는 단 하나의 가상 메서드 <xref:System.Windows.Markup.MarkupExtension.ProvideValue%2A>가 있습니다. 입력 `serviceProvider` 매개 변수는 태그 확장이 XAML 프로세서에서 호출될 때 서비스가 구현에 전달되는 방법입니다. 다음 의사 코드에서는 태그 확장 구현이 <xref:System.Windows.Markup.MarkupExtension.ProvideValue%2A>에서 서비스를 쿼리하는 방법을 보여 줍니다.  
  
```csharp  
public override object ProvideValue(IServiceProvider serviceProvider)  
{  
...  
    // Get the IXamlTypeResolver from the service provider  
    if (serviceProvider == null)  
    {  
        throw new ArgumentNullException("serviceProvider");  
    }  
    IXamlTypeResolver xamlTypeResolver = serviceProvider.GetService(typeof(IXamlTypeResolver)) as IXamlTypeResolver;  
    if (xamlTypeResolver == null)  
   {  
        throw new ArgumentException("IXamlTypeResolver"));  
    }  
...  
}  
```  
  
<a name="services_for_a_type_converter"></a>   
## <a name="services-for-a-type-converter"></a>형식 변환기에 대한 서비스  
 <xref:System.ComponentModel.TypeConverter> 에는 서비스 컨텍스트를 사용하고 XAML 사용을 지원하는 가상 메서드 4개가 있습니다. 이들 메서드는 각각 입력 `context` 매개 변수를 전달합니다. 이 매개 변수는 <xref:System.ComponentModel.ITypeDescriptorContext>형식이지만 해당 인터페이스는 <xref:System.IServiceProvider>를 상속하므로 형식 컨버터 구현에 <xref:System.IServiceProvider.GetService%2A> 메서드를 사용할 수 있습니다.  
  
 다음 의사 코드에서는 XAML 사용에 대한 형식 변환기 구현이 재정의의 하나에서 서비스를 쿼리할 수 있습니다(이 경우 <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A>).  
  
```csharp  
public override object ConvertFrom(ITypeDescriptorContext typeDescriptorContext,  
  CultureInfo cultureInfo,  
  object source)  
{  
    IRootObjectProvider rootProvider = typeDescriptorContext.GetService(typeof(IRootObjectProvider)) as IRootObjectProvider;  
    if (rootProvider != null && source is String)  
    {  
        //return something, else ...  
    }  
    throw GetConvertFromException(source);  
}  
```  
  
<a name="services_for_a_value_serializer"></a>   
## <a name="services-for-a-value-serializer"></a>값 Serializer에 대한 서비스  
 값 serializer 컨텍스트의 경우 <xref:System.Windows.Markup.ValueSerializer> 클래스, <xref:System.Windows.Markup.IValueSerializerContext>에 특정한 서비스 공급자 형식을 사용합니다. 해당 컨텍스트는 <xref:System.Windows.Markup.ValueSerializer> 가상 메서드 4개의 재정의에 전달됩니다. 컨텍스트에서 <xref:System.IServiceProvider.GetService%2A> 를 호출하여 서비스를 가져옵니다.  
  
<a name="using_the_xaml_service_provider_contexts"></a>   
## <a name="using-the-xaml-service-provider-contexts"></a>XAML 서비스 공급자 컨텍스트 사용  
 태그 확장 또는 형식 변환기에 사용할 수 있는 XAML 서비스에 대한 <xref:System.IServiceProvider.GetService%2A> 액세스의 서비스 공급자는 내부 클래스로 구현되고, 관련 컨텍스트에 전달된 방법 및 인터페이스를 통해서만 표시됩니다. 로드 경로 또는 저장 경로의 기본 .NET Framework XAML 서비스 구현에서 XAML 처리 작업이 서비스 컨텍스트에 필요한 관련 태그 확장 또는 형식 변환기 메서드를 호출할 때마다 이 내부 개체가 전달됩니다. 상황에 따라 시스템 서비스 컨텍스트는 `MarkupExtensionContext` 또는 `TextSyntaxContext`를 제공하지만 이들 두 클래스의 고유 정보는 내부용입니다. 이들 클래스와의 상호 작용은 <xref:System.IServiceProvider.GetService%2A>를 통해 클래스에서 서비스를 요청하는 것으로 제한됩니다.  
  
<a name="available_systemxaml_services"></a>   
## <a name="available-services-from-the-net-framework-xaml-service-context"></a>.NET Framework XAML 서비스 컨텍스트에서 사용 가능한 서비스  
 .NET Framework XAML 서비스에서는 태그 확장, 형식 변환기, 값 serializer 및 잠재적으로 기타 사용에 대한 서비스를 정의합니다. 다음 섹션에서는 이들 서비스를 각각 설명하고 서비스가 구현에서 사용하는 방법에 대한 지침을 제공합니다.  
  
### <a name="iserviceprovider"></a>IServiceProvider  
 **참조 설명서**: <xref:System.IServiceProvider>  
  
 **관련:** 를 호출할 <xref:System.IServiceProvider.GetService%2A?displayProperty=nameWithType>수 있도록 .NET Framework에서 서비스 기반 인프라의 기본 작업입니다.  
  
### <a name="itypedescriptorcontext"></a>ITypeDescriptorContext  
 **참조 설명서**: <xref:System.ComponentModel.ITypeDescriptorContext>  
  
 <xref:System.IServiceProvider>에서 파생됩니다. 이 클래스는 표준 <xref:System.ComponentModel.TypeConverter> 서명, <xref:System.ComponentModel.TypeConverter> 의 컨텍스트가 .NET Framework 1.0부터 있었던 클래스임을 나타냅니다. 이 클래스는 문자열-값 형식 변환을 위한 XAML 및 XAML <xref:System.ComponentModel.TypeConverter> 시나리오보다 오래되었습니다. .NET Framework XAML 서비스 컨텍스트에서 <xref:System.ComponentModel.TypeConverter> 의 메서드는 명시적으로 구현됩니다. 명시적 구현의 동작은 호출자에게 <xref:System.ComponentModel.ITypeDescriptorContext> API가 XAML 형식 시스템과 관련되거나 XAML에서 개체 읽기 또는 쓰기와 관련되지 않음을 나타냅니다. <xref:System.ComponentModel.ITypeDescriptorContext.Container%2A>, <xref:System.ComponentModel.ITypeDescriptorContext.Instance%2A>, 및 <xref:System.ComponentModel.ITypeDescriptorContext.PropertyDescriptor%2A> 는 일반적으로 .NET Framework XAML 서비스 컨텍스트에서 `null` 을 반환합니다.  
  
### <a name="ivalueserializercontext"></a>IValueSerializerContext  
 **참조 설명서**: <xref:System.Windows.Markup.IValueSerializerContext>  
  
 <xref:System.ComponentModel.ITypeDescriptorContext> 에서 파생되고 명시적 구현을 사용하여 XAML 형식 시스템에 대한 거짓 의미를 방지합니다. <xref:System.Windows.Markup.ValueSerializer>에서 정적 조회 도우미 메서드를 지원합니다.  
  
### <a name="ixamltyperesolver"></a>IXamlTypeResolver  
 **참조 설명서**: <xref:System.Windows.Markup.IXamlTypeResolver>  
  
 **정의 방법:**  <xref:System.Windows.Markup> 네임스페이스, System.Xaml 어셈블리  
  
 **관련:** 로드 경로 시나리오 및 XAML 스키마 컨텍스트와의 상호 작용  
  
 **서비스 API:**  <xref:System.Windows.Markup.IXamlTypeResolver.Resolve%2A>  
  
 XAML 작성기가 개체 그래프에서 CLR 개체를 생성할 때 필요한 XAML-CLR 형식 매핑에 영향을 미칠 수 있습니다. <xref:System.Windows.Markup.IXamlTypeResolver.Resolve%2A>는 XAML 형식 이름(<xref:System.Xaml.XamlType.Name%2A?displayProperty=nameWithType>)에 해당하는 잠재적으로 접두사로 한정된 문자열을 처리하고 CLR <xref:System.Type>을 반환합니다. 형식 확인은 일반적으로 XAML 스키마 컨텍스트에 따라 크게 달라집니다. XAML 스키마 컨텍스트는 어떤 어셈블리가 로드되는지, 그리고 형식 확인을 위해 어떤 어셈블리에 액세스할 수 있거나 액세스해야 하는지 등의 고려 사항만 인식합니다.  
  
### <a name="iuricontext"></a>IUriContext  
 **참조 설명서**: <xref:System.Windows.Markup.IUriContext>  
  
 **정의 방법:**  <xref:System.Windows.Markup> 네임스페이스, System.Xaml 어셈블리  
  
 **관련:** Uri 또는 `x:Uri` 값인 멤버 값의 로드 경로 및 저장 경로를 처리 합니다.  
  
 **서비스 API:**  <xref:System.Windows.Markup.IUriContext.BaseUri%2A>  
  
 이 서비스에서는 전체적으로 사용 가능한 URI 루트를 보고합니다(있는 경우). URI 루트를 사용하여 상대 URI를 절대 URI로 확인하거나 그 반대로 확인할 수 있습니다. 이 시나리오는 주로 특정 프레임워크를 통해 노출되거나 프레임워크에서 자주 사용되는 루트 요소 클래스의 기능을 통해 노출되는 애플리케이션 서비스와 관련됩니다. 기본 URI는 XAML 판독기 설정으로 설정될 수 있고, 이후 이 URL은 XAML 개체 작성기에 전달되고 이 서비스에 의해 보고됩니다.  
  
### <a name="iambientprovider"></a>IAmbientProvider  
 **참조 설명서**: <xref:System.Xaml.IAmbientProvider>  
  
 **정의 방법:**  <xref:System.Xaml> 네임스페이스, System.Xaml 어셈블리  
  
 **관련:** 로드 경로 처리 및 형식 조회 지연과 또는 최적화.  
  
 **서비스 APIs:**  <xref:System.Xaml.IAmbientProvider.GetAllAmbientValues%2A>, 기타 3개.  
  
 XAML의 외계 개념은 형식의 특정 멤버를 앰비언트로 표시하는 방법입니다. 또는 형식 인스턴스를 포함하는 모든 속성 값을 앰비언트 속성으로 간주하도록 형식이 앰비언트일 수 있습니다. 추가로 XAML 노드 스트림을 따라가고 개체 그래프에서 하위 항목인 태그 확장 또는 형식 변환기는 로드 시 앰비언트 속성 또는 형식 인스턴스에 액세스할 수 있거나 저장 시 앰비언트 구조의 정보를 사용할 수 있습니다. 이는 <xref:System.Windows.Markup.IXamlTypeResolver> 또는 `x:Type`과 같은 다른 서비스에 대한 형식을 확인하는 데 필요한 한정 정도에 영향을 미칠 수 있습니다. <xref:System.Xaml.AmbientPropertyValue>을 참조하세요.  
  
### <a name="ixamlschemacontextprovider"></a>IXamlSchemaContextProvider  
 **참조 설명서**: <xref:System.Xaml.IXamlSchemaContextProvider>  
  
 **정의 방법:**  <xref:System.Xaml> 네임스페이스, System.Xaml 어셈블리  
  
 **관련:** 로드 경로 및 XAML 형식을 지원 형식으로 확인 해야 하는 모든 작업입니다.  
  
 **서비스 API:**  <xref:System.Xaml.IXamlSchemaContextProvider.SchemaContext%2A>  
  
 지연된 콘텐츠를 통합하기 위해 지연된 영역에서 같은 스키마 컨텍스트가 작동해야 하므로 XAML 스키마 컨텍스트는 모든 지연 로드 작업에 필요합니다. XAML 스키마 컨텍스트 역할에 대한 자세한 내용은 [XAML Services](index.md)를 참조하세요.  
  
### <a name="irootobjectprovider"></a>IRootObjectProvider  
 **참조 설명서**: <xref:System.Xaml.IRootObjectProvider>  
  
 **정의 방법:**  <xref:System.Xaml> 네임스페이스, System.Xaml 어셈블리  
  
 **관련:** 로드 경로입니다.  
  
 **서비스 API:**  <xref:System.Xaml.IRootObjectProvider.RootObject%2A>  
  
 서비스는 특정 프레임워크를 통해 노출되거나 프레임워크에서 자주 사용되는 루트 요소 클래스의 기능을 통해 노출되는 애플리케이션 서비스와 관련됩니다. 루트 개체를 가져오기 위한 한 가지 시나리오는 코드 숨김 및 이벤트 배선을 연결하는 것입니다. 예를 들어 `x:Class` 의 WPF 구현은 XAML 태그의 다른 위치에 있는 모든 이벤트 처리기 특성의 태그 컴파일 및 배선에 사용됩니다. 태그 연결 지점 및 태그 컴파일에 대한 코드 숨김 정의 부분 클래스는 루트 요소에 있습니다.  
  
### <a name="ixamlnamespaceresolver"></a>IXamlNamespaceResolver  
 **참조 설명서**: <xref:System.Xaml.IXamlNamespaceResolver>  
  
 **정의 방법:**  <xref:System.Xaml> 네임스페이스, System.Xaml 어셈블리  
  
 **관련:** 로드 경로, 저장 경로입니다.  
  
 **서비스 API:** <xref:System.Xaml.IXamlNamespaceResolver.GetNamespace%2A> , 저장 경로에 대한 <xref:System.Xaml.IXamlNamespaceResolver.GetNamespacePrefixes%2A> .  
  
 <xref:System.Xaml.IXamlNamespaceResolver> 는 원래 XAML 태그에 매핑된 대로 접두사에 따라 XAML 네임스페이스 식별자/URI를 반환할 수 있는 서비스입니다.  
  
### <a name="iprovidevaluetarget"></a>IProvideValueTarget  
 **참조 설명서**: <xref:System.Windows.Markup.IProvideValueTarget>  
  
 **정의 방법:**  <xref:System.Windows.Markup> 네임스페이스, System.Xaml 어셈블리  
  
 **관련:** 경로를 로드 하 고 경로를 저장 합니다.  
  
 **서비스 API:**  <xref:System.Windows.Markup.IProvideValueTarget.TargetObject%2A>, <xref:System.Windows.Markup.IProvideValueTarget.TargetProperty%2A>.  
  
 <xref:System.Windows.Markup.IProvideValueTarget> 을 사용하면 형식 변환기 또는 태그 확장이 로드 시 작동할 위치에 대한 컨텍스트를 가져올 수 있습니다. 구현에서 이 컨텍스트를 사용하여 사용을 무효화할 수 있습니다. 예를 들어 WPF에는 몇몇 태그 확장 내부에 <xref:System.Windows.DynamicResourceExtension>과 같은 논리가 있습니다. 이 논리에서는 <xref:System.Windows.Markup.IProvideValueTarget.TargetProperty%2A> 를 확인하여 확장이 종속성 속성을 설정하거나 기타 비종속성 속성의 짧은 목록을 설정하는 데만 사용되는지 확인합니다.  
  
### <a name="ixamlnameresolver"></a>IXamlNameResolver  
 **참조 설명서**: <xref:System.Xaml.IXamlNameResolver>  
  
 **정의 방법:**  <xref:System.Xaml> 네임스페이스, System.Xaml 어셈블리  
  
 **관련:** `x:Name` ,`x:Reference`또는 프레임 워크 특정 기술로 식별 되는 개체를 확인 하는 경로 개체 그래프 정의를 로드 합니다.  
  
 **서비스 API:**  <xref:System.Xaml.IXamlNameResolver.Resolve%2A>, 전방 참조 처리와 같은 더 고급 시나리오를 위한 기타 API.  
  
 `x:Reference` 처리의 .NET Framework XAML 서비스 구현에는 이 서비스를 사용합니다. 프레임워크를 지원하는 특정 프레임워크 또는 도구는 `x:Name` 처리나 동등한 항목(<xref:System.Windows.Markup.RuntimeNamePropertyAttribute> 특성 사용) 속성 처리에 이 서비스를 사용합니다.  
  
### <a name="idestinationtypeprovider"></a>IDestinationTypeProvider  
 **참조 설명서**: <xref:System.Xaml.IDestinationTypeProvider>  
  
 **정의 방법:**  <xref:System.Xaml> 네임스페이스, System.Xaml 어셈블리  
  
 **관련:** 간접 CLR 형식 정보의 로드 경로 확인.  
  
 **서비스 API:** <xref:System.Xaml.IDestinationTypeProvider.GetDestinationType%2A>  
  
 자세한 내용은 <xref:System.Xaml.IDestinationTypeProvider>을 참조하세요.  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Markup.MarkupExtension>
- <xref:System.Xaml.XamlObjectWriter>
- [XAML 태그 확장명 개요](markup-extensions-for-xaml-overview.md)
- [XAML을 위한 형식 변환기 개요](type-converters-for-xaml-overview.md)
