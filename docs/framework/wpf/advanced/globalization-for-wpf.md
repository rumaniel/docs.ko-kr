---
title: WPF의 전역화
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [WPF], international user interface
- XAML [WPF], globalization
- international user interface [WPF], XAML
- globalization [WPF]
ms.assetid: 4571ccfe-8a60-4f06-9b37-7ac0b1c2d10f
ms.openlocfilehash: 32caf87435e23008f9f300d231c2705e7894280f
ms.sourcegitcommit: 9c3a4f2d3babca8919a1e490a159c1500ba7a844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2019
ms.locfileid: "72291468"
---
# <a name="globalization-for-wpf"></a>WPF의 전역화
이 항목에서는 글로벌 시장을 위한 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 응용 프로그램을 작성할 때 알아야 하는 문제를 소개 합니다. 세계화 프로그래밍 요소는 <xref:System.Globalization> 네임 스페이스의 .NET에서 정의 됩니다.

<a name="xaml_globalization"></a>
## <a name="xaml-globalization"></a>XAML 전역화
 Extensible Application Markup Language (XAML)는 [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)]을 기반으로 하며 [!INCLUDE[TLA2#tla_xml](../../../../includes/tla2sharptla-xml-md.md)] 사양에 정의 된 세계화 지원을 활용 합니다. 다음 섹션에서는 알고 있어야 하는 몇 가지 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 기능에 대해 설명 합니다.

<a name="char_reference"></a>
### <a name="character-references"></a>문자 참조
문자 참조는 10 진수 또는 16 진수에서 나타내는 특정 [!INCLUDE[TLA#tla_unicode](../../../../includes/tlasharptla-unicode-md.md)] 문자의 UTF16 코드 단위를 제공 합니다. 다음 예제에서는 콥트어 대문자 가로 또는 ' Ϩ '에 대 한 10 진수 문자 참조를 보여 줍니다.

```
&#1000;
```

다음 예제에서는 16 진수 문자 참조를 보여 줍니다. 16 진수 앞에 **x** 가 있습니다.

```
&#x3E8;
```

<a name="encoding"></a>
### <a name="encoding"></a>인코딩
 @No__t-0에서 지원 되는 인코딩은 ASCII, [!INCLUDE[TLA2#tla_unicode](../../../../includes/tla2sharptla-unicode-md.md)] UTF-16 및 u t f-8입니다. Encoding 문은 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 문서의 시작 부분에 있습니다. 인코딩 특성이 없으며 바이트 순서가 없으면 기본적으로 구문 분석기가 UTF-8로 설정됩니다. UTF-8과 UTF-16이 기본 인코딩입니다. UTF-7은 지원되지 않습니다. 다음 예에서는 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 파일에서 UTF-8 인코딩을 지정 하는 방법을 보여 줍니다.

```xaml
?xml encoding="UTF-8"?
```

<a name="lang_attrib"></a>
### <a name="language-attribute"></a>언어 특성
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]은 [xml: lang](../../xaml-services/xml-lang-handling-in-xaml.md) 을 사용 하 여 요소의 language 특성을 나타냅니다.  @No__t-0 클래스를 활용 하려면 언어 특성 값이 <xref:System.Globalization.CultureInfo>로 미리 정의 된 문화권 이름 중 하나 여야 합니다. [xml:lang](../../xaml-services/xml-lang-handling-in-xaml.md)은 요소 트리에서 상속 가능하며(반드시 종속성 속성 상속성때문이 아니라 XML 규칙에 따름), 명시적으로 할당되지 않은 경우 기본값은 비어 있습니다.

 언어를 지정할 때 언어 특성이 매우 유용합니다. 예를 들어, 프랑스, 퀘벡, 벨기에 및 스위스의 프랑스어에는 다른 철자, 어휘 및 발음이 있습니다. 또한 중국어, 일본어 및 한국어는 [!INCLUDE[TLA2#tla_unicode](../../../../includes/tla2sharptla-unicode-md.md)]의 코드 요소를 공유 하지만 표의 문자 모양은 서로 다르며 완전히 다른 글꼴을 사용 합니다.

 다음 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 예제에서는 `fr-CA` 언어 특성을 사용 하 여 캐나다 프랑스어를 지정 합니다.

```xaml
<TextBlock xml:lang="fr-CA">Découvrir la France</TextBlock>
```

<a name="unicode"></a>
### <a name="unicode"></a>유니코드
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]은 서로게이트를 비롯 한 모든 [!INCLUDE[TLA2#tla_unicode](../../../../includes/tla2sharptla-unicode-md.md)] 기능을 지원 합니다. 문자 집합을 [!INCLUDE[TLA2#tla_unicode](../../../../includes/tla2sharptla-unicode-md.md)]에 매핑할 수 있으면 지원 됩니다. 예를 들어, GB18030에서는 중국어, 일본어 및 한국어(CFK) 확장 A와 B에 매핑되는 일부 문자와 서로게이트 쌍을 소개하므로 완전히 지원됩니다. @No__t-0 응용 프로그램은 <xref:System.Globalization.StringInfo>을 사용 하 여 서로게이트 쌍 또는 조합 문자가 있는지 여부를 알 필요 없이 문자열을 조작할 수 있습니다.

<a name="design_intl_ui_with_xaml"></a>
## <a name="designing-an-international-user-interface-with-xaml"></a>XAML로 국가별 사용자 인터페이스 설계
 이 섹션에서는 응용 프로그램을 작성할 때 고려해 야 하는 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 기능에 대해 설명 합니다.

<a name="intl_text"></a>
### <a name="international-text"></a>국가별 텍스트
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에는 모든 Microsoft .NET Framework에서 지원 되는 쓰기 시스템에 대 한 기본 제공 처리가 포함 됩니다.

 현재 지원되는 스크립트는 다음과 같습니다.

- 아랍어

- 벵골어

- 데바나가리어

- 키릴 자모

- 그리스어

- 구자라트어

- 굴묵키어

- 히브리어

- 표의 문자 스크립트

- 칸나다어

- 라오어

- 라틴어

- 말라얄람어

- 몽골어

- 오리야어

- 시리아어

- 타밀어

- 텔루구어

- 타나 문자

- 태국어*

- 티베트어

 \* 이 릴리스에서는 태국어 텍스트의 표시 및 편집이 지원되며, 단어 구분은 지원되지 않습니다.

 현재 지원되지 않는 스크립트는 다음과 같습니다.

- 크메르어

- 한국어 옛 한글

- 미얀마어

- 스리랑카어

 모든 쓰기 시스템 엔진은 OpenType 글꼴을 지원 합니다. OpenType 글꼴에는 글꼴 작성자가 향상 된 국제 글꼴 및 고급 인쇄 글꼴을 디자인할 수 있도록 하는 OpenType 레이아웃 테이블이 포함 될 수 있습니다. OpenType 글꼴 레이아웃 표에는 문자 모양 대체, 문자 모양 위치 지정, 양쪽 맞춤 및 기준선 위치에 대 한 정보가 포함 되어 텍스트 처리 응용 프로그램이 텍스트 레이아웃을 향상 시킬 수 있도록 합니다.

 OpenType 글꼴을 사용 하면 [!INCLUDE[TLA2#tla_unicode](../../../../includes/tla2sharptla-unicode-md.md)] 인코딩을 사용 하 여 긴 문자 모양 집합을 처리할 수 있습니다. 이러한 인코딩을 사용하면 글꼴 문자 모양 변형 외에도 광범위한 국가별 지원이 가능합니다.

 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 텍스트 렌더링은 해상도 독립성을 지 원하는 Microsoft ClearType 하위 픽셀 기술을 기반으로 합니다. 이 기능을 통해 가독성이 크게 향상되며, 모든 스크립트에 대해 고품질 잡지 스타일 문서를 지원하는 기능을 제공합니다.

<a name="intl_layout"></a>
### <a name="international-layout"></a>국가별 레이아웃
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서는 가로, 양방향 및 세로 레이아웃을 지원하는 매우 편리한 방법을 제공합니다. 프레젠테이션 프레임 워크에서 <xref:System.Windows.FrameworkElement.FlowDirection%2A> 속성은 레이아웃을 정의 하는 데 사용할 수 있습니다. 흐름 방향 패턴은 다음과 같습니다.

- *LeftToRight* - 라틴어, 동아시아어 등을 위한 가로 레이아웃.

- *RightToLeft* - 아랍어, 히브리어 등을 위한 양방향.

<a name="developing_localizable_apps"></a>
## <a name="developing-localizable-applications"></a>지역화 가능 애플리케이션 개발
 글로벌 사용을 위해 애플리케이션을 작성할 때 애플리케이션을 지역화해야 한다는 점에 유의해야 합니다. 다음 항목에서는 고려할 사항을 제공합니다.

<a name="mui"></a>
### <a name="multilingual-user-interface"></a>다국어 사용자 인터페이스
 MUI (다국어 사용자 인터페이스)는 한 언어에서 다른 언어로 Ui를 전환 하기 위한 Microsoft 지원입니다. @No__t-0 응용 프로그램은 어셈블리 모델을 사용 하 여 MUI를 지원 합니다. 한 애플리케이션에는 언어 중립 어셈블리 외에도 언어별 위성 리소스 어셈블리도 포함됩니다. 진입점은 기본 어셈블리에서 관리되는 .EXE입니다.  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 리소스 로더는 [!INCLUDE[TLA2#tla_netframewk](../../../../includes/tla2sharptla-netframewk-md.md)]의 resource manager를 활용 하 여 리소스 조회 및 대체를 지원 합니다. 여러 언어 위성 어셈블리는 동일한 기본 어셈블리와 작동합니다. 로드 되는 리소스 어셈블리는 현재 스레드의 <xref:System.Globalization.CultureInfo.CurrentUICulture%2A>에 따라 다릅니다.

<a name="localizable_ui"></a>
### <a name="localizable-user-interface"></a>지역화할 수 있는 사용자 인터페이스
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 응용 프로그램은 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]을 사용 하 여 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]를 정의 합니다. [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]를 사용하면 개발자가 속성 및 논리 집합이 포함된 개체의 계층 구조를 지정할 수 있습니다. @No__t-0을 주로 사용 하는 것은 @no__t 1 응용 프로그램을 개발 하는 것 이지만 CLR (공용 언어 런타임) 개체의 계층 구조를 지정 하는 데 사용할 수 있습니다. 대부분의 개발자는 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]을 사용 하 여 응용 프로그램의 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]을 지정 하 고 C# 와 같은 프로그래밍 언어를 사용 하 여 사용자 상호 작용에 대응 합니다.

 리소스 관점에서 언어 종속 @no__t를 설명 하도록 설계 된 @no__t 0 파일은 리소스 요소 이므로 최종 배포 형식을 지역화 하 여 국제 언어를 지원 해야 합니다. @No__t-0은 이벤트를 처리할 수 없으므로 많은 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 응용 프로그램은이 작업을 수행 하는 코드 블록을 포함 합니다. 자세한 내용은 [XAML 개요 (WPF)](xaml-overview-wpf.md)합니다. @No__t-0 파일을 BAML 형식의 XAML로 토큰화 하면 코드가 제거 되 고 다른 이진 파일로 컴파일됩니다. XAML 파일의 BAML 양식, 이미지 및 기타 형식의 관리 리소스 개체는 위성 리소스 어셈블리에 포함되어 다른 언어로 지역화되거나, 지역화가 필요하지 않은 경우 기본 어셈블리에 포함됩니다.

> [!NOTE]
> [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 응용 프로그램은 문자열 테이블, 이미지 등을 비롯 한 모든 [!INCLUDE[TLA2#tla_netframewk](../../../../includes/tla2sharptla-netframewk-md.md)]CLR 리소스를 지원 합니다.

<a name="building_localizable_apps"></a>
### <a name="building-localizable-applications"></a>지역화 가능 애플리케이션 빌드
 지역화는 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]을 다른 문화권에 맞게 조정 하는 것을 의미 합니다. @No__t-0 응용 프로그램을 지역화할 수 있도록 개발자는 지역화 가능한 리소스를 모두 리소스 어셈블리에 빌드해야 합니다. 리소스 어셈블리는 다른 언어로 지역화 되며 코드 숨김이 리소스 관리 API를 사용 하 여 로드 합니다. @No__t-0 응용 프로그램에 필요한 파일 중 하나는 프로젝트 파일 (proj)입니다. 애플리케이션에서 사용하는 모든 리소스는 프로젝트 파일에 포함되어야 합니다. .csprop 파일의 다음 예에서는 이 작업을 수행하는 방법을 보여줍니다.

```xml
<Resource Include="data\picture1.jpg"/>
<EmbeddedResource Include="data\stringtable.en-US.restext"/>
```

 응용 프로그램에서 리소스를 사용 하려면 <xref:System.Resources.ResourceManager>을 인스턴스화하고 사용 하려는 리소스를 로드 합니다. 다음 예제에서는 이 작업을 수행하는 방법을 보여 줍니다.

 [!code-csharp[LocalizationResources#2](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizationResources/CSharp/page1.xaml.cs#2)]

<a name="using_clickonce"></a>
## <a name="using-clickonce-with-localized-applications"></a>지역화된 애플리케이션에서 ClickOnce 사용
 ClickOnce는 Visual Studio 2005와 함께 제공 되는 새로운 Windows Forms 배포 기술입니다. 애플리케이션 설치 및 웹 애플리케이션의 업그레이드를 수행할 수 있습니다. ClickOnce로 배포된 애플리케이션이 지역화되면 지역화된 문화권에서만 볼 수 있습니다. 예를 들어, 배포 된 응용 프로그램을 일본어로 지역화 하는 경우 일본어 [!INCLUDE[TLA#tla_win](../../../../includes/tlasharptla-win-md.md)]은 영어 창이 아닌 경우에만 볼 수 있습니다. 이것은 일본어 사용자가 영어 버전의 Windows를 실행 하는 일반적인 시나리오 이기 때문에 문제가 발생 합니다.

 이 문제는 중립 언어 대체 특성을 설정하여 해결합니다. 애플리케이션 개발자가 선택적으로 기본 어셈블리에서 리소스를 제거하고 특정 문화권에 해당하는 위성 어셈블리에서 해당 리소스를 찾을 수 있게 지정할 수 있습니다. 이 프로세스를 제어 하려면 <xref:System.Resources.NeutralResourcesLanguageAttribute>을 사용 합니다. @No__t-0 클래스의 생성자에는 두 개의 시그니처가 있습니다. 하나는 <xref:System.Resources.UltimateResourceFallbackLocation> 매개 변수를 사용 하 여 <xref:System.Resources.ResourceManager>가 대체 (fallback) 리소스 (주 어셈블리 또는 위성 어셈블리)를 추출 해야 하는 위치를 지정 합니다. 다음 예제에서는 이 특성을 사용하는 방법을 보여 줍니다. 최종 대체 (fallback) 위치에 대해 코드는 <xref:System.Resources.ResourceManager>이 현재 실행 중인 어셈블리의 디렉터리에 있는 "de" 하위 디렉터리에서 리소스를 찾도록 합니다.

```csharp
[assembly: NeutralResourcesLanguageAttribute(
    "de" , UltimateResourceFallbackLocation.Satellite)]
```

## <a name="see-also"></a>참조

- [WPF 전역화 및 지역화 개요](wpf-globalization-and-localization-overview.md)
