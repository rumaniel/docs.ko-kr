---
title: WPF XAML을 위한 XAML 네임스페이스 및 네임스페이스 매핑
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- custom classes [WPF], mapping namespaces to
- XAML [WPF], namespaces
- namespace mapping [WPF]
- assemblies [WPF], mapping namespaces to
- mapping namespaces [WPF]
- XAML [WPF], namespace mapping
- classes [WPF], mapping namespaces to
- namespaces [WPF]
ms.assetid: 5c0854e3-7470-435d-9fe2-93eec9d3634e
ms.openlocfilehash: 4fc88f1e32b8ddce6abccad085b0c44a5c716e8b
ms.sourcegitcommit: 24a4a8eb6d8cfe7b8549fb6d823076d7c697e0c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68400810"
---
# <a name="xaml-namespaces-and-namespace-mapping-for-wpf-xaml"></a>WPF XAML을 위한 XAML 네임스페이스 및 네임스페이스 매핑
이 항목에서는 WPF XAML 파일의 루트 태그에서 주로 찾을 수 있는 두 XAML 네임스페이스 매핑과 그 용도에 대해 자세하게 설명합니다. 또한 고유한 코드나 별도의 어셈블리에 정의된 요소에 사용할 수 있도록 유사한 매핑을 생성하는 방법에 대해서도 설명합니다.  

## <a name="what-is-a-xaml-namespace"></a>XAML 네임스페이스의 정의  
 XAML 네임스페이스는 XML 네임스페이스 개념을 확장한 것입니다. XAML 네임스페이스를 지정하는 데는 XML 네임스페이스 구문, 네임스페이스 식별자로 URI를 사용하는 규칙이 적용되며 동일한 태그 소스의 여러 네임스페이스를 참조하기 위한 수단을 제공하는 접두사가 사용됩니다. XML 네임스페이스의 XAML 정의에 추가된 주요 개념에 따르면 XAML 네임스페이스는 태그 사용의 고유성 범위를 보장하고, 태그 엔터티가 특정 CLR 네임스페이스 및 참조되는 어셈블리에 의해 지원되는 방식에 영향을 줍니다. 이러한 지원 방식은 XAML 스키마 컨텍스트라는 개념에 의해서도 영향을 받습니다. 그러나 WPF에서 XAML 네임스페이스를 처리하려는 경우에는 일반적으로 기본 XAML 네임스페이스, XAML 언어 네임스페이스 및 추가적인 다른 XAML 네임스페이스 등의 XAML 네임스페이스를 XAML 태그에 의해 특정 지원 CLR 네임스페이스 및 참조되는 어셈블리에 직접 매핑되는 것으로 간주할 수 있습니다.  
  
<a name="The_WPF_and_XAML_Namespace_Declarations"></a>   
## <a name="the-wpf-and-xaml-namespace-declarations"></a>WPF 및 XAML 네임스페이스 선언  
 많은 XAML 파일의 루트 태그에 있는 네임스페이스 선언에는 일반적으로 두 가지 XML 네임스페이스 선언이 있습니다. 다음과 같은 첫 번째 선언은 전체 WPF 클라이언트/프레임워크 XAML 네임스페이스를 기본값으로 매핑합니다.  
  
 `xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"`  
  
 두 번째 선언은 개별 XAML 네임스페이스를 대개 `x:` 접두사에 매핑합니다.  
  
 `xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"`  
  
 이러한 선언 간의 관계에서 `x:` 접두사 매핑은 XAML 언어 정의의 일부인 내장 항목을 지원하며, [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]는 XAML을 언어로 사용하고 XAML에 대한 해당 개체의 어휘를 정의하는 하나의 구현입니다. WPF 어휘의 사용이 XAML 내장 항목 사용보다 훨씬 더 일반적일 것이므로 WPF 어휘가 기본값으로 매핑됩니다.  
  
 이 [!INCLUDE[TLA2#tla_sdk](../../../../includes/tla2sharptla-sdk-md.md)] 내에서 XAML 언어 내장 항목 지원을 매핑하기 위한 `x:` 접두사 규칙 뒤에는 프로젝트 템플릿, 샘플 코드 및 언어 기능의 설명서가 있습니다. XAML 네임스페이스는 기본적인 WPF 애플리케이션에도 필요한 여러 가지 일반적인 기능을 정의합니다. 예를 들어 partial 클래스를 통해 코드 숨김을 XAML 파일에 결합하려면 관련 XAML 파일의 루트 요소에서 해당 클래스를 `x:Class` 특성으로 명명해야 합니다. 또는 XAML 페이지에 정의된 요소 중 키가 지정된 리소스로 액세스하려는 요소에는 `x:Key` 특성을 설정해야 합니다. XAML의 이러한 특징과 기타 특징에 대한 자세한 내용은 [XAML 개요(WPF)](xaml-overview-wpf.md) 또는 [XAML 구문 정보](xaml-syntax-in-detail.md)를 참조하세요.  
  
<a name="Mapping_To_Custom_Classes_and_Assemblies"></a>   
## <a name="mapping-to-custom-classes-and-assemblies"></a>사용자 지정 클래스 및 어셈블리 매핑  
 표준 WPF 및 XAML 내장 XAML 네임스페이스를 접두사에 매핑하는 방식과 유사하게 `xmlns` 접두사 선언 내에서 일련의 토큰을 사용하여 XML 네임스페이스를 어셈블리에 매핑할 수 있습니다.  
  
 구문에는 다음과 같은 명명된 토큰과 값을 사용할 수 있습니다.  
  
 `clr-namespace:` 요소로 노출되는 공용 형식을 포함하는 어셈블리 내에서 선언된 CLR 네임스페이스입니다.  
  
 `assembly=`참조 된 CLR 네임 스페이스의 전체 또는 일부를 포함 하는 어셈블리입니다. 이 값은 일반적으로 경로가 아니라 어셈블리의 이름이며 .dll 또는 .exe와 같은 확장명을 포함하지 않습니다. 해당 어셈블리의 경로는 매핑하려는 XAML을 포함하는 프로젝트 파일에서 프로젝트 참조로 설정해야 합니다. 버전 관리 및 강력한 이름 서명을 통합 하기 위해이 값은 `assembly` 단순 문자열 이름이 아니라에 의해 <xref:System.Reflection.AssemblyName>정의 된 문자열일 수 있습니다.  
  
 `clr-namespace` 토큰과 해당 값을 구분하는 문자는 콜론(:)이지만, `assembly` 토큰과 해당 값을 구분하는 문자는 등호(=)입니다. 이 두 토큰 간을 구분하는 데 사용되는 문자는 세미콜론입니다. 또한 선언에서 아무 곳에 나 공백을 포함 하지 마십시오.  
  
### <a name="a-basic-custom-mapping-example"></a>기본 사용자 지정 매핑 예제  
 다음 코드에서는 예제 사용자 지정 클래스를 정의합니다.  
  
```csharp  
namespace SDKSample {  
    public class ExampleClass : ContentControl {  
        public ExampleClass() {  
        ...  
        }  
    }  
}  
```  
  
```vb  
Namespace SDKSample  
    Public Class ExampleClass  
        Inherits ContentControl  
         ...  
        Public Sub New()  
        End Sub  
    End Class  
End Namespace  
```  
  
 이 사용자 지정 클래스는 라이브러리로 컴파일되며 라이브러리의 이름은 프로젝트 설정(표시되지 않음)별로 `SDKSampleLibrary`로 지정됩니다.  
  
 이 사용자 지정 클래스를 참조하려면 이 클래스를 현재 프로젝트의 참조로도 포함해야 합니다. 이 작업은 일반적으로 Visual Studio에서 솔루션 탐색기 UI를 사용하여 수행합니다.  
  
 이제 클래스가 포함된 라이브러리가 있고, 프로젝트 설정에 이 라이브러리에 대한 참조가 있으므로 다음 접두사 매핑을 XAML에서 루트 요소의 일부로 추가할 수 있습니다.  
  
 `xmlns:custom="clr-namespace:SDKSample;assembly=SDKSampleLibrary"`  
  
 이 모두를 결합하면 다음과 같이 루트 태그에 일반적인 기본 및 x: 매핑과 함께 사용자 지정 매핑을 포함하고 접두사가 지정된 참조를 사용하여 해당 UI의 `ExampleClass`를 인스턴스화하는 XAML이 됩니다.  
  
```xaml  
<Page x:Class="WPFApplication1.MainPage"  
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"   
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
    xmlns:custom="clr-namespace:SDKSample;assembly=SDKSampleLibrary">  
  ...  
  <custom:ExampleClass/>  
...  
</Page>  
```  
  
### <a name="mapping-to-current-assemblies"></a>현재 어셈블리에 매핑  
 사용자 지정 클래스를 참조하는 응용 프로그램 코드와 동일한 어셈블리 내에서 `clr-namespace` 참조를 정의하는 경우에는 `assembly`를 생략할 수 있습니다. 등호 다음에 문자열 토큰 없이 `assembly=`를 지정하는 구문도 이와 동일합니다.  
  
 사용자 지정 클래스는 동일한 어셈블리에 정의된 경우 페이지의 루트 요소로 사용할 수 없습니다. partial 클래스는 매핑할 필요가 없으며 애플리케이션에서 페이지의 partial 클래스가 아닌 클래스 중 XAML에서 요소로 참조하려는 클래스만 매핑하면 됩니다.  
  
<a name="Mapping_CLR_Namespaces_to_XML_Namespaces_in_an"></a>   
## <a name="mapping-clr-namespaces-to-xml-namespaces-in-an-assembly"></a>CLR 네임스페이스를 어셈블리의 XML 네임스페이스에 매핑  
 WPF는 여러 CLR 네임스페이스를 단일 XAML 네임스페이스에 매핑하기 위해 XAML 프로세서에서 사용되는 CLR 특성을 정의합니다. 이 특성 <xref:System.Windows.Markup.XmlnsDefinitionAttribute>은 어셈블리를 생성 하는 소스 코드의 어셈블리 수준에 배치 됩니다. WPF 어셈블리 소스 코드에서는이 특성을 사용 하 여 <xref:System.Windows> 및 <xref:System.Windows.Controls>와 같은 다양 한 일반 네임 스페이스를 [!INCLUDE[TLA#tla_wpfxmlnsv1](../../../../includes/tlasharptla-wpfxmlnsv1-md.md)] 네임 스페이스에 매핑합니다.  
  
 는 <xref:System.Windows.Markup.XmlnsDefinitionAttribute> 두 개의 매개 변수인 XML/XAML 네임 스페이스 이름과 CLR 네임 스페이스 이름을 사용 합니다. 여러 CLR 네임 스페이스를 동일한 XML 네임 스페이스에 매핑하기 위해 둘 이상의가 있을 수있습니다.<xref:System.Windows.Markup.XmlnsDefinitionAttribute> 매핑한 후에는 partial 클래스의 코드 숨김 페이지에서 적절한 `using` 문을 사용하여 정규화된 이름 없이도 이러한 네임스페이스의 멤버를 참조할 수 있습니다. 자세한 내용은 <xref:System.Windows.Markup.XmlnsDefinitionAttribute>을 참조하십시오.  
  
## <a name="designer-namespaces-and-other-prefixes-from-xaml-templates"></a>XAML 템플릿의 디자이너 네임스페이스 및 기타 접두사  
 여러 가지 WPF XAML 개발 환경 및/또는 디자인 도구를 사용하는 경우 XAML 태그 내에 다른 XAML 네임스페이스 및 접두사가 정의되어 있을 수 있습니다.  
  
 [!INCLUDE[wpfdesigner_current_long](../../../../includes/wpfdesigner-current-long-md.md)]에서는 일반적으로 접두사 `d:`에 매핑되는 디자이너 네임스페이스를 사용합니다. 최신 WPF용 프로젝트 템플릿의 경우 [!INCLUDE[wpfdesigner_current_long](../../../../includes/wpfdesigner-current-long-md.md)]와 다른 디자인 환경 간의 XAML 교환을 지원하기 위해 이 XAML 네임스페이스가 미리 매핑되어 있을 수 있습니다. 이 디자인 XAML 네임스페이스는 디자이너에서 XAML 기반 UI를 왕복하는 동안 디자인 상태를 계속 유지하는 데 사용됩니다. 또한 디자이너에서 런타임 데이터 소스를 사용할 수 있게 하는 `d:IsDataSource` 등의 기능에도 사용됩니다.  
  
 매핑되는 또 다른 접두사로 `mc:`이 있을 수 있습니다. `mc:`은 태그 호환성을 위해 사용되며, XAML에 반드시 필요하지는 않은 태그 호환성 패턴을 활용합니다. 일정 범위 내에서 태그 호환성 기능은 프레임워크 간 또는 지원 구현의 여러 경계를 넘어 XAML을 교환하는 데 사용될 수 있으며, XAML 스키마 컨텍스트 간에 작업하고 디자이너에서 제한된 모드에 대해 호환성을 제공하는 데 사용될 수 있습니다. 태그 호환성 개념과 WPF와의 관계에 대 한 자세한 내용은 태그 호환성 ( [mc:)을 참조 하세요. 언어 기능](markup-compatibility-mc-language-features.md).  
  
## <a name="wpf-and-assembly-loading"></a>WPF 및 어셈블리 로딩  
 WPF에 대 한 XAML 스키마 컨텍스트는 WPF 응용 프로그램 모델과 통합 되며,이 모델은의 <xref:System.AppDomain>CLR 정의 개념을 사용 합니다. 다음 시퀀스에서는 XAML 스키마 컨텍스트에서 <xref:System.AppDomain> 및 기타 요소의 WPF 사용에 따라 어셈블리를 로드 하거나 런타임 또는 디자인 타임에 형식을 찾는 방법을 해석 하는 방법을 설명 합니다.  
  
1. 를 반복 하 <xref:System.AppDomain>여 가장 최근에 로드 된 어셈블리에서 시작 하는 이름의 모든 측면과 일치 하는 이미 로드 된 어셈블리를 찾습니다.  
  
2. 이름이 정규화 된 경우 정규화 된 이름 <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=nameWithType> 에 대해를 호출 합니다.  
  
3. 약식 이름 + 정규화된 이름의 공개 키 토큰이 로드한 태그의 소스 어셈블리와 일치하는 경우 이 어셈블리를 반환합니다.  
  
4. 약식 이름 + 공개 키 토큰을 사용 하 여 <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=nameWithType>를 호출 합니다.  
  
5. 이름이 정규화 되지 않은 경우를 호출 <xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=nameWithType>합니다.  
  
 느슨한 XAML에서는 로드할 소스 어셈블리가 없으므로 3단계가 사용되지 않습니다.  
  
 WPF 용 컴파일된 XAML (xamlbuildtask를 통해 생성)은의 <xref:System.AppDomain> 이미 로드 된 어셈블리를 사용 하지 않습니다 (1 단계). 또한 XamlBuildTask 출력에서 이름이 정규화되지 않아서는 안되므로 5단계가 적용되지 않습니다.  
  
 BAML도 정규화되지 않은 어셈블리 이름을 포함해서는 안되지만 PresentationBuildTask를 통해 생성된 컴파일된 BAML에서는 모든 단계를 사용합니다.  
  
## <a name="see-also"></a>참고자료

- [XML 네임 스페이스 이해](https://go.microsoft.com/fwlink/?LinkId=98069)
- [XAML 개요(WPF)](xaml-overview-wpf.md)
