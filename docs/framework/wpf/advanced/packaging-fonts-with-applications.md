---
title: 애플리케이션과 함께 글꼴 패키징
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- applications [WPF], packaging fonts with
- fonts [WPF], packaging with applications
- typography [WPF], packaging fonts with applications
- packaging fonts with applications [WPF]
ms.assetid: db15ee48-4d24-49f5-8b9d-a64460865286
ms.openlocfilehash: 18a8037b6b4433a4a83860eae205174f3036d6e8
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005020"
---
# <a name="packaging-fonts-with-applications"></a>애플리케이션과 함께 글꼴 패키징
이 항목에서는 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 응용 프로그램으로 글꼴을 패키지 하는 방법에 대 한 개요를 제공 합니다.  
  
> [!NOTE]
> 대부분의 소프트웨어와 마찬가지로 글꼴 파일도 판매되는 것이 아니라 사용이 허가됩니다. 글꼴 사용을 관리 하는 라이선스는 공급 업체 마다 다르지만 일반적으로 Microsoft에서 제공 하는 글꼴을 포함 하 여 응용 프로그램 및 Windows에서 제공 하는 글꼴을 포함 하 여 응용 프로그램 내에 글꼴을 포함 하거나 재배포 하는 것을 허용 하지 않습니다. 따라서 개발자는 애플리케이션 내에 포함하거나 기타 다른 방법으로 재배포하려는 글꼴에 대해 필요한 라이선스 권한이 있는지 확인해야 합니다.  

<a name="introduction_to_packaging_fonts"></a>   
## <a name="introduction-to-packaging-fonts"></a>글꼴 패키징 소개  
 @No__t-0 응용 프로그램 내에서 사용자 인터페이스 텍스트 및 다른 유형의 텍스트 기반 콘텐츠를 표시 하는 리소스로 글꼴을 쉽게 패키지할 수 있습니다. 글꼴은 애플리케이션의 어셈블리 파일 내에 포함하거나 별도로 저장할 수 있습니다. 리소스 전용 글꼴 라이브러리를 만들어 애플리케이션에서 이를 참조하도록 할 수도 있습니다.  
  
 OpenType 및 TrueType® 글꼴에는 글꼴에 대 한 글꼴 포함 라이선스 권한을 나타내는 형식 플래그 fsType가 포함 되어 있습니다. 그러나 이 형식 플래그는 문서에 저장된 포함된 글꼴만 참조하고 애플리케이션에 포함된 글꼴은 참조하지 않습니다. @No__t-0 개체를 만들고 <xref:System.Windows.Media.GlyphTypeface.EmbeddingRights%2A> 속성을 참조 하 여 글꼴에 대 한 글꼴 포함 권한을 검색할 수 있습니다. FsType 플래그에 대 한 자세한 내용은 [OpenType 사양의](https://www.microsoft.com/typography/otspec/os2.htm) "OS/2 및 Windows 메트릭" 섹션을 참조 하세요.  
  
 [Microsoft 입력 체계](https://docs.microsoft.com/typography/) 웹 사이트에는 특정 글꼴 공급 업체를 찾거나 사용자 지정 작업을 위한 글꼴 공급 업체를 찾는 데 도움이 되는 연락처 정보가 포함 되어 있습니다.  
  
<a name="adding_fonts_as_content_items"></a>   
## <a name="adding-fonts-as-content-items"></a>콘텐츠 항목으로 글꼴 추가  
 애플리케이션의 어셈블리 파일과는 별도의 프로젝트 콘텐츠 항목으로 애플리케이션에 글꼴을 추가할 수 있습니다. 이 경우 콘텐츠 항목이 어셈블리에 리소스로 포함되지 않습니다. 다음 프로젝트 파일 예제에서는 콘텐츠 항목을 정의하는 방법을 보여 줍니다.  
  
```xml  
<Project DefaultTargets="Build"  
                xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <!-- Other project build settings ... -->  
  
  <ItemGroup>  
    <Content Include="Peric.ttf" />  
    <Content Include="Pericl.ttf" />  
  </ItemGroup>  
</Project>  
```  
  
 애플리케이션에서 런타임에 글꼴을 사용할 수 있도록 하려면 애플리케이션의 배포 디렉터리에서 해당 글꼴에 액세스할 수 있어야 합니다. 응용 프로그램의 프로젝트 파일에서 `<CopyToOutputDirectory>` 요소를 사용 하면 빌드 프로세스 중에 응용 프로그램 배포 디렉터리에 글꼴을 자동으로 복사할 수 있습니다. 다음 프로젝트 파일 예제에서는 글꼴을 배포 디렉터리에 복사하는 방법을 보여 줍니다.  
  
```xml  
<ItemGroup>  
  <Content Include="Peric.ttf">  
    <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>  
  </Content>  
  <Content Include="Pericl.ttf">  
    <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>  
  </Content>  
</ItemGroup>  
```  
  
 다음 코드 예제에서는 애플리케이션의 글꼴을 콘텐츠 항목으로 참조하는 방법을 보여 줍니다. 참조되는 콘텐츠 항목은 애플리케이션의 어셈블리 파일과 동일한 디렉터리에 있어야 합니다.  
  
 [!code-xaml[FontSnippets#FontPackageSnippet8](~/samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/FontPackageSnippets.xaml#fontpackagesnippet8)]  
  
<a name="adding_fonts_as_resource_items"></a>   
## <a name="adding-fonts-as-resource-items"></a>리소스 항목으로 글꼴 추가  
 애플리케이션의 어셈블리 파일에 포함된 프로젝트 리소스 항목으로 애플리케이션에 글꼴을 추가할 수 있습니다. 리소스에 별도의 하위 디렉터리를 사용하면 애플리케이션의 프로젝트 파일을 보다 간편하게 구성할 수 있습니다. 다음 프로젝트 파일 예제에서는 별도의 하위 디렉터리에 리소스 항목으로 글꼴을 정의하는 방법을 보여 줍니다.  
  
```xml  
<Project DefaultTargets="Build"  
                xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <!-- Other project build settings ... -->  
  
  <ItemGroup>  
    <Resource Include="resources\Peric.ttf" />  
    <Resource Include="resources\Pericl.ttf" />  
  </ItemGroup>  
</Project>  
```  
  
> [!NOTE]
> 응용 프로그램에 리소스를 리소스로 추가 하는 경우 응용 프로그램의 프로젝트 파일에서 `<EmbeddedResource>` 요소가 아니라 `<Resource>` 요소를 설정 해야 합니다. 빌드 작업에 대 한 `<EmbeddedResource>` 요소는 지원 되지 않습니다.  
  
 다음 태그 예제에서는 애플리케이션의 글꼴 리소스를 참조하는 방법을 보여 줍니다.  
  
 [!code-xaml[FontSnippets#FontPackageSnippet1](~/samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/FontPackageSnippets.xaml#fontpackagesnippet1)]  
  
### <a name="referencing-font-resource-items-from-code"></a>코드에서 글꼴 리소스 항목 참조  
 코드에서 글꼴 리소스 항목을 참조 하려면 두 부분으로 구성 된 글꼴 리소스 참조 (기본 [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)])를 제공 해야 합니다. 및 글꼴 위치 참조입니다. 이러한 값은 <xref:System.Windows.Media.FontFamily.%23ctor%2A> 메서드에 대 한 매개 변수로 사용 됩니다. 다음 코드 예제에서는 `resources` 이라는 프로젝트 하위 디렉터리에서 응용 프로그램의 글꼴 리소스를 참조 하는 방법을 보여 줍니다.  
  
 [!code-csharp[FontSnippets#FontPackageSnippet2](~/samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/FontPackageSnippets.xaml.cs#fontpackagesnippet2)]
 [!code-vb[FontSnippets#FontPackageSnippet2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FontSnippets/visualbasic/fontpackagesnippets.xaml.vb#fontpackagesnippet2)]  
  
 기본 [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)]은 글꼴 리소스가 있는 응용 프로그램 하위 디렉터리를 포함할 수 있습니다. 이 경우 글꼴 위치 참조는 디렉터리를 지정할 필요가 없지만 선행 "`./`"을 포함 해야 합니다 .이는 글꼴 리소스가 기본 [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)]로 지정 된 동일한 디렉터리에 있음을 나타냅니다. 다음 코드 예제에서는 위의 코드 예제에 나오는 것과 동일한 글꼴 리소스 항목을 참조하는 다른 방법을 보여 줍니다.  
  
 [!code-csharp[FontSnippets#FontPackageSnippet5](~/samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/FontPackageSnippets.xaml.cs#fontpackagesnippet5)]
 [!code-vb[FontSnippets#FontPackageSnippet5](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FontSnippets/visualbasic/fontpackagesnippets.xaml.vb#fontpackagesnippet5)]  
  
### <a name="referencing-fonts-from-the-same-application-subdirectory"></a>동일한 애플리케이션 하위 디렉터리에서 글꼴 참조  
 애플리케이션 콘텐츠와 리소스 파일을 모두 애플리케이션 프로젝트의 동일한 사용자 정의 하위 디렉터리에 배치할 수 있습니다. 다음 프로젝트 파일 예제에서는 동일한 하위 디렉터리에 정의된 콘텐츠 페이지와 글꼴 리소스를 보여 줍니다.  
  
```xml  
<ItemGroup>  
  <Page Include="pages\HomePage.xaml" />  
</ItemGroup>  
<ItemGroup>  
  <Resource Include="pages\Peric.ttf" />  
  <Resource Include="pages\Pericl.ttf" />  
</ItemGroup>  
```  
  
 애플리케이션 콘텐츠와 글꼴이 동일한 하위 디렉터리에 있으므로 글꼴 참조가 애플리케이션 콘텐츠를 기준으로 합니다. 다음 예제에서는 글꼴이 애플리케이션과 동일한 디렉터리에 있는 경우 애플리케이션의 글꼴 리소스를 참조하는 방법을 보여 줍니다.  
  
 [!code-xaml[FontSnippets#FontPackageSnippet3](~/samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/pages/HomePage.xaml#fontpackagesnippet3)]  
  
 [!code-csharp[FontSnippets#FontPackageSnippet4](~/samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/pages/HomePage.xaml.cs#fontpackagesnippet4)]
 [!code-vb[FontSnippets#FontPackageSnippet4](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FontSnippets/visualbasic/pages/homepage.xaml.vb#fontpackagesnippet4)]  
  
### <a name="enumerating-fonts-in-an-application"></a>애플리케이션의 글꼴 열거  
 응용 프로그램에서 리소스 항목으로 글꼴을 열거 하려면 <xref:System.Windows.Media.Fonts.GetFontFamilies%2A> 또는 <xref:System.Windows.Media.Fonts.GetTypefaces%2A> 메서드를 사용 합니다. 다음 예제에서는 <xref:System.Windows.Media.Fonts.GetFontFamilies%2A> 메서드를 사용 하 여 응용 프로그램 글꼴 위치에서 <xref:System.Windows.Media.FontFamily> 개체의 컬렉션을 반환 하는 방법을 보여 줍니다. 이 경우에는 응용 프로그램에 “resources”라는 하위 디렉터리가 있습니다.  
  
 [!code-csharp[FontSnippets#FontsSnippet3](~/samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/FontFamilySnippets.xaml.cs#fontssnippet3)]
 [!code-vb[FontSnippets#FontsSnippet3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FontSnippets/visualbasic/fontfamilysnippets.xaml.vb#fontssnippet3)]  
  
 다음 예제에서는 <xref:System.Windows.Media.Fonts.GetTypefaces%2A> 메서드를 사용 하 여 응용 프로그램 글꼴 위치에서 <xref:System.Windows.Media.Typeface> 개체의 컬렉션을 반환 하는 방법을 보여 줍니다. 이 경우에는 응용 프로그램에 “resources”라는 하위 디렉터리가 있습니다.  
  
 [!code-csharp[FontSnippets#FontsSnippet7](~/samples/snippets/csharp/VS_Snippets_Wpf/FontSnippets/CSharp/FontFamilySnippets.xaml.cs#fontssnippet7)]
 [!code-vb[FontSnippets#FontsSnippet7](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FontSnippets/visualbasic/fontfamilysnippets.xaml.vb#fontssnippet7)]  
  
<a name="creating_a_font_resource_library"></a>   
## <a name="creating-a-font-resource-library"></a>글꼴 리소스 라이브러리 만들기  
 글꼴만 포함된 리소스 전용 라이브러리를 만들 수 있습니다. 이러한 유형의 라이브러리 프로젝트에는 코드가 포함되지 않습니다. 리소스 전용 라이브러리는 일반적으로 리소스와 리소스를 사용하는 애플리케이션 코드를 분리하려는 경우에 만듭니다. 리소스 전용 라이브러리를 만들면 라이브러리 어셈블리를 여러 애플리케이션 프로젝트에 포함할 수 있습니다. 다음 프로젝트 파일 예제에서는 리소스 전용 라이브러리 프로젝트의 주요 부분을 보여 줍니다.  
  
```xml  
<PropertyGroup>  
  <AssemblyName>FontLibrary</AssemblyName>  
  <OutputType>library</OutputType>  
  ...  
</PropertyGroup>  
...  
<ItemGroup>  
  <Resource Include="Kooten.ttf" />  
  <Resource Include="Pesca.ttf" />  
</ItemGroup  
```  
  
### <a name="referencing-a-font-in-a-resource-library"></a>리소스 라이브러리의 글꼴 참조  
 애플리케이션에서 리소스 라이브러리의 글꼴을 참조하려면 라이브러리 어셈블리의 이름을 글꼴 참조의 접두사로 지정해야 합니다. 이 경우 글꼴 리소스 어셈블리는 “FontLibrary”입니다. 어셈블리 이름을 어셈블리 내의 참조와 구분하려면 ‘;’ 문자를 사용합니다. 글꼴 이름에 “Component” 키워드와 참조를 차례로 추가하면 글꼴 라이브러리의 리소스에 대한 전체 참조가 완성됩니다. 다음 코드 예제에서는 리소스 라이브러리 어셈블리의 글꼴을 참조하는 방법을 보여 줍니다.  
  
 [!code-xaml[OpenTypeFontsSample#OpenTypeFontsSample1](~/samples/snippets/csharp/VS_Snippets_Wpf/OpenTypeFontsSample/CS/Kootenay.xaml#opentypefontssample1)]  
  
> [!NOTE]
> 이 SDK에는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 응용 프로그램에서 사용할 수 있는 샘플 OpenType 글꼴 집합이 포함 되어 있습니다. 글꼴은 리소스 전용 라이브러리에 정의되어 있습니다. 자세한 내용은 [샘플 OpenType 글꼴 팩](sample-opentype-font-pack.md)을 참조하세요.  
  
<a name="limitations_on_font_usage"></a>   
## <a name="limitations-on-font-usage"></a>글꼴 사용의 제한 사항  
 다음 목록에서는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 응용 프로그램에서 글꼴 패키징 및 사용에 대 한 몇 가지 제한 사항을 설명 합니다.  
  
- **글꼴 포함 권한 비트:** [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 애플리케이션은 글꼴 포함 권한 비트를 확인하거나 적용하지 않습니다. 자세한 내용은 [Introduction_to_Packing Fonts](#introduction_to_packaging_fonts) 섹션을 참조 하세요.  
  
- **원본 사이트 글꼴:** [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 응용 프로그램은 http 또는 ftp [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)]에 대 한 글꼴 참조를 허용 하지 않습니다.  
  
- Pack: notation: [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 응용 프로그램을 **사용 하는 절대 URI** 는 글꼴에 대 한 절대 [!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)] 참조의 일부로 "pack:"를 사용 하 여 프로그래밍 방식으로 <xref:System.Windows.Media.FontFamily> 개체를 만들 수 없습니다. 예를 들어 `"pack://application:,,,/resources/#Pericles Light"`은 잘못 된 글꼴 참조입니다.  
  
- **자동 글꼴 포함:** 디자인 타임에는 응용 프로그램의 글꼴 사용을 검색 하 고 응용 프로그램의 리소스에 글꼴을 자동으로 포함 하는 것을 지원 하지 않습니다.  
  
- **글꼴 하위 집합:** [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 애플리케이션은 고정되지 않은 문서에 대해서는 글꼴 하위 집합을 만드는 것을 지원하지 않습니다.  
  
- 올바르지 않은 참조가 있는 경우 애플리케이션에서는 사용 가능한 글꼴로 대체합니다.  
  
## <a name="see-also"></a>참조

- <xref:System.Windows.Documents.Typography>
- <xref:System.Windows.Media.FontFamily>
- [Microsoft 입력 체계: 링크, 뉴스 및 연락처 @ no__t-0
- [OpenType 사양](https://www.microsoft.com/typography/otspec/)
- [OpenType 글꼴 기능](opentype-font-features.md)
- [샘플 OpenType 글꼴 팩](sample-opentype-font-pack.md)
