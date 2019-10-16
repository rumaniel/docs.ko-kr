---
title: WPF의 Pack URI
ms.date: 03/30/2017
helpviewer_keywords:
- pack URI scheme [WPF]
- loading embedded resources [WPF]
- URIs (Uniform Resource Identifiers)
- Uniform Resource Identifiers (URIs)
- loading non-resource files
- application management [WPF]
ms.assetid: 43adb517-21a7-4df3-98e8-09e9cdf764c4
ms.openlocfilehash: ad928fb223ce22c65bb86a78c7d4cd006651a2d5
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69950752"
---
# <a name="pack-uris-in-wpf"></a>WPF의 Pack URI

WPF (Windows Presentation Foundation) [!INCLUDE[TLA#tla_uri#plural](../../../../includes/tlasharptla-urisharpplural-md.md)] 에서는 다음을 포함 하 여 여러 가지 방법으로 파일을 식별 하 고 로드 하는 데 사용 됩니다.

- 응용 프로그램 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 을 처음 시작할 때 표시할를 지정 하는입니다.

- 이미지 로드

- 페이지 탐색

- 비실행 데이터 파일 로드

또한은 다음을 비롯 한 다양 한 위치에서 파일을 식별 하 고 로드 하는 데 사용할 수있습니다.[!INCLUDE[TLA2#tla_uri#plural](../../../../includes/tla2sharptla-urisharpplural-md.md)]

- 현재 어셈블리입니다.

- 참조된 어셈블리

- 어셈블리에 상대적인 위치

- 애플리케이션의 원본 사이트

이러한 위치에서 이러한 형식의 파일을 식별 하 고 로드 하기 위한 일관 된 메커니즘을 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 제공 하기 위해는 *pack URI 체계*의 확장성을 활용 합니다. 이 항목에서는 스키마에 대해 간략하게 설명 하 고, 다양 한 시나리오 [!INCLUDE[TLA2#tla_uri#plural](../../../../includes/tla2sharptla-urisharpplural-md.md)] 에 대해 pack을 구성 하는 방법에 대해 [!INCLUDE[TLA2#tla_uri#plural](../../../../includes/tla2sharptla-urisharpplural-md.md)] 설명 하 고, 두 태그의 pack [!INCLUDE[TLA2#tla_uri#plural](../../../../includes/tla2sharptla-urisharpplural-md.md)] 을 사용 하는 방법을 보여 주기 위해 절대 및 상대 및 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 해결 방법을 설명 합니다 및 코드.

<a name="The_Pack_URI_Scheme"></a>

## <a name="the-pack-uri-scheme"></a>Pack URI 체계

Pack [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 구성표는 콘텐츠를 구성 하 고 식별 하기 위한 모델을 설명 하는 OPC ( [Open 패키징 규칙](https://go.microsoft.com/fwlink/?LinkID=71255) ) 사양에서 사용 됩니다. 이 모델의 핵심 요소는 패키지 및 파트입니다. 여기서 *패키지* 는 하나 이상의 논리적 *파트*에 대 한 논리적 컨테이너입니다. 다음 그림에서는 이 개념을 보여 줍니다.

![패키지 및 파트 다이어그램](./media/pack-uris-in-wpf/wpf-package-parts-diagram.png)

OPC 사양은 RFC 2396 (URI (Uniform Resource Identifier)의 확장성을 활용 하 여 파트를 식별 합니다. 제네릭 구문)을 지정 하 여 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] pack 스키마를 정의 합니다.

에서 지정 하는 체계는 접두사 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 에 의해 정의 됩니다. http, ftp 및 파일은 잘 알려진 예제입니다. Pack [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 스키마는 "pack"을 체계로 사용 하 고 두 구성 요소인 authority와 path를 포함 합니다. 다음은 pack [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]에 대 한 형식입니다.

pack://*authority*/*path*

*기관은* 파트에 포함 된 패키지 유형을 지정 하는 반면 *경로* 는 패키지 내 파트의 위치를 지정 합니다.

다음 그림에서는 이 개념을 보여 줍니다.

![패키지, 권한 및 경로의 관계](./media/pack-uris-in-wpf/wpf-relationship-diagram.png)

패키지와 파트는 애플리케이션 및 파일과 유사합니다. 즉, 애플리케이션(패키지)은 다음을 비롯한 하나 이상의 파일(파트)을 포함할 수 있습니다.

- 로컬 어셈블리로 컴파일되는 리소스 파일

- 참조된 어셈블리로 컴파일되는 리소스 파일

- 참조하는 어셈블리로 컴파일되는 리소스 파일

- 콘텐츠 파일

- 원본 사이트 파일

이러한 파일 형식에 액세스 하기 위해 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 에서는 application:///및 siteoforigin:///의 두 가지 기관을 지원 합니다. application:/// 인증 기관은 리소스 및 콘텐츠 파일을 비롯하여 컴파일 시 알려진 애플리케이션 데이터 파일을 식별합니다. siteoforigin:/// 인증 기관은 원본 사이트 파일을 식별합니다. 다음 그림에서는 각 인증 기관의 범위를 보여 줍니다.

![Pack URI 다이어그램](./media/pack-uris-in-wpf/wpf-pack-uri-scheme.png)

> [!NOTE]
> Pack [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 의 authority 구성 요소는 패키지를 가리키는 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 포함 된 이며 RFC 2396을 준수 해야 합니다. 또한 “/” 문자를 “,” 문자로 바꾸고 “%” 및 “?” 같은 예약 문자는 이스케이프해야 합니다. 자세한 내용은 OPC를 참조하세요.

다음 섹션에서는 이러한 두 가지 권한을 리소스 [!INCLUDE[TLA2#tla_uri#plural](../../../../includes/tla2sharptla-urisharpplural-md.md)] , 콘텐츠 및 원본 사이트 파일을 식별 하는 적절 한 경로와 함께 사용 하 여 pack을 구성 하는 방법을 설명 합니다.

<a name="Resource_File_Pack_URIs___Local_Assembly"></a>

## <a name="resource-file-pack-uris"></a>리소스 파일 Pack URI

리소스 파일은 MSBuild `Resource` 항목으로 구성 되 고 어셈블리로 컴파일됩니다. WPF는 로컬 어셈블리로 컴파일되거나 로컬 어셈블리에서 참조 되는 어셈블리로 컴파일되는 리소스 파일을 식별 하는 데 사용할 수 있는 pack Uri 생성을 지원 합니다.

<a name="Local_Assembly_Resource_File"></a>

### <a name="local-assembly-resource-file"></a>로컬 어셈블리 리소스 파일

로컬 어셈블리로 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 컴파일되는 리소스 파일에 대 한 pack은 다음 인증 기관과 경로를 사용 합니다.

- **인증 기관**: application:///

- **경로**: 로컬 어셈블리 프로젝트 폴더 루트에 상대적인 경로를 포함 하는 리소스 파일의 이름입니다.

다음 예제에서는 로컬 어셈블리의 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 프로젝트 폴더 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 루트에 있는 리소스 파일의 pack을 보여 줍니다.

`pack://application:,,,/ResourceFile.xaml`

다음 예제에서는 로컬 어셈블리의 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 프로젝트 폴더 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 에 있는 하위 폴더에 있는 리소스 파일의 pack을 보여 줍니다.

`pack://application:,,,/Subfolder/ResourceFile.xaml`

<a name="Resource_File_Pack_URIs___Referenced_Assembly"></a>

### <a name="referenced-assembly-resource-file"></a>참조된 어셈블리 리소스 파일

참조 된 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 어셈블리로 컴파일되는 리소스 파일에 대 한 pack은 다음 인증 기관과 경로를 사용 합니다.

- **인증 기관**: application:///

- **경로**: 참조 된 어셈블리로 컴파일되는 리소스 파일의 이름입니다. 경로는 다음 형식을 따라야 합니다.

  *AssemblyShortName*{ *;Version*]{ *;PublicKey*];component/*Path*

  - **AssemblyShortName**: 참조된 어셈블리에 대한 약식 이름

  - **;Version**[옵션]: 리소스 파일을 포함하는 참조된 어셈블리의 버전. 동일한 약식 이름을 갖는 두 개 이상의 참조된 어셈블리가 로드된 경우 사용됩니다.

  - **;PublicKey**[옵션]: 참조된 어셈블리를 서명하는 데 사용된 공개 키. 동일한 약식 이름을 갖는 두 개 이상의 참조된 어셈블리가 로드된 경우 사용됩니다.

  - **;component**: 참조되는 어셈블리가 로컬 어셈블리에서 참조된다는 것을 지정

  - **/Path**: 참조된 어셈블리 프로젝트 폴더의 루트에 상대적인 경로를 포함한 리소스 파일의 이름

다음 예제에서는 참조 된 어셈블리 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 의 프로젝트 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 폴더 루트에 있는 리소스 파일의 pack을 보여 줍니다.

`pack://application:,,,/ReferencedAssembly;component/ResourceFile.xaml`

다음 예제에서는 참조 된 어셈블리 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 의 프로젝트 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 폴더에 있는 하위 폴더에 있는 리소스 파일의 pack을 보여 줍니다.

`pack://application:,,,/ReferencedAssembly;component/Subfolder/ResourceFile.xaml`

다음 예제에서는 참조 된 버전별 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 어셈블리의 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 프로젝트 폴더에 있는 루트 폴더에 있는 리소스 파일의 pack을 보여 줍니다.

`pack://application:,,,/ReferencedAssembly;v1.0.0.1;component/ResourceFile.xaml`

참조 된 어셈블리 리소스 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 파일의 pack 구문은 application:///authority에만 사용할 수 있습니다. 예를 들어 다음은에서 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]지원 되지 않습니다.

`pack://siteoforigin:,,,/SomeAssembly;component/ResourceFile.xaml`

<a name="Content_File_Pack_URIs"></a>

## <a name="content-file-pack-uris"></a>콘텐츠 파일 Pack URI

콘텐츠 파일 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 의 pack은 다음 인증 기관과 경로를 사용 합니다.

- **인증 기관**: application:///

- **경로**: 응용 프로그램의 주 실행 어셈블리의 파일 시스템 위치에 상대적인 경로를 포함 하는 콘텐츠 파일의 이름입니다.

다음 예제에서는 실행 가능한 어셈블리 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 와 동일한 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 폴더에 있는 콘텐츠 파일의 pack을 보여 줍니다.

`pack://application:,,,/ContentFile.xaml`

다음 예제에서는 응용 프로그램의 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 실행 가능 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 어셈블리에 상대적인 하위 폴더에 있는 콘텐츠 파일의 pack을 보여 줍니다.

`pack://application:,,,/Subfolder/ContentFile.xaml`

> [!NOTE]
> HTML 콘텐츠 파일을 탐색할 수 없습니다. 구성표 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 는 원본 사이트에 있는 HTML 파일 탐색만 지원 합니다.

<a name="The_siteoforigin_____Authority"></a>

## <a name="site-of-origin-pack-uris"></a>원본 사이트 Pack URI

원본 사이트 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 파일에 대 한 팩은 다음 인증 기관과 경로를 사용 합니다.

- **인증 기관**: siteoforigin:///

- **경로**: 실행 가능한 어셈블리가 시작 된 위치에 상대적인 경로를 포함 하는 원본 사이트 파일의 이름입니다.

다음 예제에서는 실행 가능한 어셈블리가 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 시작 된 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 위치에 저장 된 원본 사이트 파일에 대 한 pack을 보여 줍니다.

`pack://siteoforigin:,,,/SiteOfOriginFile.xaml`

다음 예제에서는 응용 프로그램의 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 실행 가능 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 어셈블리가 시작 된 위치에 상대적인 하위 폴더에 저장 된 원본 사이트 파일의 pack을 보여 줍니다.

`pack://siteoforigin:,,,/Subfolder/SiteOfOriginFile.xaml`

<a name="Page_Files"></a>

## <a name="page-files"></a>페이지 파일

MSBuild `Page` 항목으로 구성 된 XAML 파일은 리소스 파일과 같은 방식으로 어셈블리로 컴파일됩니다. 따라서 리소스 파일 `Page` 에 대 한 pack uri를 사용 하 여 MSBuild 항목을 식별할 수 있습니다.

일반적으로 MSBuild [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] `Page` 항목으로 구성 되는 파일 형식에는 다음 중 하나가 루트 요소로 포함 됩니다.

- <xref:System.Windows.Window?displayProperty=nameWithType>

- <xref:System.Windows.Controls.Page?displayProperty=nameWithType>

- <xref:System.Windows.Navigation.PageFunction%601?displayProperty=nameWithType>

- <xref:System.Windows.ResourceDictionary?displayProperty=nameWithType>

- <xref:System.Windows.Documents.FlowDocument?displayProperty=nameWithType>

- <xref:System.Windows.Controls.UserControl?displayProperty=nameWithType>

<a name="Absolute_vs_Relative_Pack_URIs"></a>

## <a name="absolute-vs-relative-pack-uris"></a>절대 및 상대 Pack URI

정규화 된 pack [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 에는 체계, 인증 기관 및 경로가 포함 되며 절대 pack [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]으로 간주 됩니다. 개발자 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 를 위한 단순화를 위해 요소는 일반적으로 경로만 포함 하는 상대 pack [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]을 사용 하 여 적절 한 특성을 설정할 수 있습니다.

예를 들어 로컬 어셈블리에 있는 리소스 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 파일에 대해 다음과 같은 절대 pack을 고려해 보세요.

`pack://application:,,,/ResourceFile.xaml`

이 리소스 파일 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 을 참조 하는 상대 팩은 다음과 같습니다.

`/ResourceFile.xaml`

> [!NOTE]
> 원본 사이트 파일은 어셈블리와 연결 되어 있지 않으므로 절대 pack [!INCLUDE[TLA2#tla_uri#plural](../../../../includes/tla2sharptla-urisharpplural-md.md)]을 통해서만 참조할 수 있습니다.

기본적으로 상대 팩 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 은 참조가 포함 된 태그나 코드의 위치를 기준으로 고려 됩니다. 그러나 선행 백슬래시를 사용 하는 경우에는 응용 프로그램 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 의 루트를 기준으로 상대 팩 참조를 고려할 수 있습니다. 예를 들어 다음과 같은 프로젝트 구조를 가정해 봅니다.

`App.xaml`

`Page2.xaml`

`\SubFolder`

`+ Page1.xaml`

`+ Page2.xaml`

.Root. xaml에 *Root*\subfolder\page2.xaml을 참조 하는가 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 포함 된 경우 참조는 다음 상대 팩을 사용할 수 있습니다.

`Page2.xaml`

.Root. xaml에 *Root*\page2.xaml을 참조 하는가 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 포함 된 경우 참조는 다음 상대 팩을 사용할 수 있습니다.

`/Page2.xaml`

<a name="Pack_URI_Resolution"></a>

## <a name="pack-uri-resolution"></a>Pack URI 확인

Pack [!INCLUDE[TLA2#tla_uri#plural](../../../../includes/tla2sharptla-urisharpplural-md.md)] 형식을 사용 하면 여러 형식의 파일이 동일한 것 [!INCLUDE[TLA2#tla_uri#plural](../../../../includes/tla2sharptla-urisharpplural-md.md)] 으로 표시 될 수 있습니다. 예를 들어 다음과 같은 절대 pack [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]을 살펴보겠습니다.

`pack://application:,,,/ResourceOrContentFile.xaml`

이 절대 pack [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 은 로컬 어셈블리 또는 콘텐츠 파일의 리소스 파일을 참조할 수 있습니다. 다음 상대 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]와 동일한 경우에도 마찬가지입니다.

`/ResourceOrContentFile.xaml`

Pack [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 에서 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 참조[!INCLUDE[TLA2#tla_uri#plural](../../../../includes/tla2sharptla-urisharpplural-md.md)] 하는 파일의 형식을 확인 하기 위해는 다음 추론을 사용 하 여 로컬 어셈블리 및 콘텐츠 파일의 리소스 파일을 확인 합니다.

1. <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute> Pack[!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]과 일치 하는 특성에 대 한 어셈블리 메타 데이터를 검색 합니다.

2. 특성이 있으면 팩 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 의 경로는 콘텐츠 파일을 참조 합니다. <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute>

3. <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute> 특성을 찾을 수 없는 경우 로컬 어셈블리로 컴파일되는 집합 리소스 파일을 검색 합니다.

4. Pack [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 의 경로와 일치 하는 리소스 파일이 있는 경우 pack [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 의 경로는 리소스 파일을 참조 합니다.

5. 리소스를 찾을 수 없는 경우 내부적으로 만든 <xref:System.Uri> 가 잘못 된 것입니다.

[!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]다음을 참조 하는 [!INCLUDE[TLA2#tla_uri#plural](../../../../includes/tla2sharptla-urisharpplural-md.md)] 에 대 한 해결 방법은 적용 되지 않습니다.

- 참조 된 어셈블리의 콘텐츠 파일: 이러한 파일 형식은에서 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]지원 되지 않습니다.

- 참조 된 어셈블리에 포함 된 [!INCLUDE[TLA2#tla_uri#plural](../../../../includes/tla2sharptla-urisharpplural-md.md)] 파일: 참조 된 어셈블리 `;component` 의 이름과 접미사를 모두 포함 하기 때문에 이러한 파일을 식별 하는 파일은 고유 합니다.

- 원본 사이트 파일: [!INCLUDE[TLA2#tla_uri#plural](../../../../includes/tla2sharptla-urisharpplural-md.md)] 이러한 파일은 siteoforigin:///권한이 포함 된 pack [!INCLUDE[TLA2#tla_uri#plural](../../../../includes/tla2sharptla-urisharpplural-md.md)] 에서 식별할 수 있는 유일한 파일이 기 때문에 고유 합니다.

Pack [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 해상도에서 사용할 수 있는 한 가지 단순화는 코드를 리소스 및 콘텐츠 파일의 위치와 약간 독립적입니다. 예를 들어 콘텐츠 파일로 다시 구성 된 로컬 어셈블리의 리소스 파일이 있는 경우 해당 리소스에 대 한 팩 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 은 pack [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]을 사용 하는 코드와 마찬가지로 동일 하 게 유지 됩니다.

<a name="Programming_with_Pack_URIs"></a>

## <a name="programming-with-pack-uris"></a>Pack URI를 사용한 프로그래밍

많은 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 클래스는 다음을 포함 하 여 pack [!INCLUDE[TLA2#tla_uri#plural](../../../../includes/tla2sharptla-urisharpplural-md.md)]을 사용 하 여 설정할 수 있는 속성을 구현 합니다.

- <xref:System.Windows.Application.StartupUri%2A?displayProperty=nameWithType>

- <xref:System.Windows.Controls.Frame.Source%2A?displayProperty=nameWithType>

- <xref:System.Windows.Navigation.NavigationWindow.Source%2A?displayProperty=nameWithType>

- <xref:System.Windows.Documents.Hyperlink.NavigateUri%2A?displayProperty=nameWithType>

- <xref:System.Windows.Window.Icon%2A?displayProperty=nameWithType>

- <xref:System.Windows.Controls.Image.Source%2A?displayProperty=nameWithType>

이러한 속성을 태그와 코드 모두에서 설정할 수 있습니다. 이 섹션에서는 두 경우에 대한 기본 구조를 설명한 다음 일반적인 시나리오 예제를 보여 줍니다.

<a name="Using_Pack_URIs_in_Markup"></a>

### <a name="using-pack-uris-in-markup"></a>태그에서 Pack URI 사용

Pack을 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 사용 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]하 여 특성의 요소를 설정 하 여 태그에 팩을 지정 합니다. 예를 들어:

`<element attribute="pack://application:,,,/File.xaml" />`

표 1에서는 태그에 지정할 수 [!INCLUDE[TLA2#tla_uri#plural](../../../../includes/tla2sharptla-urisharpplural-md.md)] 있는 다양 한 절대 pack을 보여 줍니다.

표 1: 태그의 절대 Pack Uri

|파일|절대 팩[!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]|
|----------|-------------------------------------------------------------------------------------------------------------------------|
|리소스 파일 - 로컬 어셈블리|`"pack://application:,,,/ResourceFile.xaml"`|
|하위 폴더의 리소스 파일 - 로컬 어셈블리|`"pack://application:,,,/Subfolder/ResourceFile.xaml"`|
|리소스 파일 - 참조된 어셈블리|`"pack://application:,,,/ReferencedAssembly;component/ResourceFile.xaml"`|
|참조된 어셈블리의 하위 폴더에 있는 리소스 파일|`"pack://application:,,,/ReferencedAssembly;component/Subfolder/ResourceFile.xaml"`|
|버전이 있는 참조된 어셈블리의 리소스 파일|`"pack://application:,,,/ReferencedAssembly;v1.0.0.0;component/ResourceFile.xaml"`|
|콘텐츠 파일|`"pack://application:,,,/ContentFile.xaml"`|
|하위 폴더의 콘텐츠 파일|`"pack://application:,,,/Subfolder/ContentFile.xaml"`|
|원본 사이트 파일|`"pack://siteoforigin:,,,/SOOFile.xaml"`|
|하위 폴더의 원본 사이트 파일|`"pack://siteoforigin:,,,/Subfolder/SOOFile.xaml"`|

표 2에서는 태그에 지정할 수 [!INCLUDE[TLA2#tla_uri#plural](../../../../includes/tla2sharptla-urisharpplural-md.md)] 있는 다양 한 상대 팩을 보여 줍니다.

표 2: 태그의 상대 Pack Uri

|파일|상대 팩[!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]|
|----------|-------------------------------------------------------------------------------------------------------------------------|
|로컬 어셈블리의 리소스 파일|`"/ResourceFile.xaml"`|
|로컬 어셈블리의 하위 폴더에 있는 리소스 파일|`"/Subfolder/ResourceFile.xaml"`|
|참조된 어셈블리의 리소스 파일|`"/ReferencedAssembly;component/ResourceFile.xaml"`|
|참조된 어셈블리의 하위 폴더에 있는 리소스 파일|`"/ReferencedAssembly;component/Subfolder/ResourceFile.xaml"`|
|콘텐츠 파일|`"/ContentFile.xaml"`|
|하위 폴더의 콘텐츠 파일|`"/Subfolder/ContentFile.xaml"`|

<a name="Using_Pack_URIs_in_Code"></a>

### <a name="using-pack-uris-in-code"></a>코드에서 Pack URI 사용

클래스를 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] <xref:System.Uri> 인스턴스화하고 pack[!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 을 생성자에 매개 변수로 전달 하 여 코드에서 pack을 지정 합니다. 다음 예제를 통해 볼 수 있습니다.

```csharp
Uri uri = new Uri("pack://application:,,,/File.xaml");
```

기본적으로 클래스는 <xref:System.Uri> pack [!INCLUDE[TLA2#tla_uri#plural](../../../../includes/tla2sharptla-urisharpplural-md.md)] 을 절대로 간주 합니다. 따라서 <xref:System.Uri> 클래스의 인스턴스를 상대 팩 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]을 사용 하 여 만들 때 예외가 발생 합니다.

```csharp
Uri uri = new Uri("/File.xaml");
```

다행히 <xref:System.Uri> 클래스 생성자 <xref:System.Uri.%23ctor%28System.String%2CSystem.UriKind%29> 의 오버 로드는 형식의 <xref:System.UriKind> 매개 변수를 허용 하 여 pack [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 이 절대 경로 인지 상대 경로 인지 지정할 수 있습니다.

```csharp
// Absolute URI (default)
Uri absoluteUri = new Uri("pack://application:,,,/File.xaml", UriKind.Absolute);
// Relative URI
Uri relativeUri = new Uri("/File.xaml",
                        UriKind.Relative);
```

제공 된 팩 <xref:System.UriKind.Absolute> <xref:System.UriKind.Relative> 이하나인지아니면다른지만[!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 지정 해야 합니다. 사용자가 런타임에 팩 [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] [!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)] 을 입력 하는 경우와 같이 사용 되는 pack 형식을 모르는 경우를 대신 사용 <xref:System.UriKind.RelativeOrAbsolute> 합니다.

```csharp
// Relative or Absolute URI provided by user via a text box
TextBox userProvidedUriTextBox = new TextBox();
Uri uri = new Uri(userProvidedUriTextBox.Text, UriKind.RelativeOrAbsolute);
```

표 3에서는를 사용 [!INCLUDE[TLA2#tla_uri#plural](../../../../includes/tla2sharptla-urisharpplural-md.md)] <xref:System.Uri?displayProperty=nameWithType>하 여 코드에 지정할 수 있는 다양 한 상대 pack을 보여 줍니다.

표 3: 코드의 절대 Pack Uri

|파일|절대 팩[!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]|
|----------|-------------------------------------------------------------------------------------------------------------------------|
|리소스 파일 - 로컬 어셈블리|`Uri uri = new Uri("pack://application:,,,/ResourceFile.xaml", UriKind.Absolute);`|
|하위 폴더의 리소스 파일 - 로컬 어셈블리|`Uri uri = new Uri("pack://application:,,,/Subfolder/ResourceFile.xaml", UriKind.Absolute);`|
|리소스 파일 - 참조된 어셈블리|`Uri uri = new Uri("pack://application:,,,/ReferencedAssembly;component/ResourceFile.xaml", UriKind.Absolute);`|
|참조된 어셈블리의 하위 폴더에 있는 리소스 파일|`Uri uri = new Uri("pack://application:,,,/ReferencedAssembly;component/Subfolder/ResourceFile.xaml", UriKind.Absolute);`|
|버전이 있는 참조된 어셈블리의 리소스 파일|`Uri uri = new Uri("pack://application:,,,/ReferencedAssembly;v1.0.0.0;component/ResourceFile.xaml", UriKind.Absolute);`|
|콘텐츠 파일|`Uri uri = new Uri("pack://application:,,,/ContentFile.xaml", UriKind.Absolute);`|
|하위 폴더의 콘텐츠 파일|`Uri uri = new Uri("pack://application:,,,/Subfolder/ContentFile.xaml", UriKind.Absolute);`|
|원본 사이트 파일|`Uri uri = new Uri("pack://siteoforigin:,,,/SOOFile.xaml", UriKind.Absolute);`|
|하위 폴더의 원본 사이트 파일|`Uri uri = new Uri("pack://siteoforigin:,,,/Subfolder/SOOFile.xaml", UriKind.Absolute);`|

표 4에서는를 사용 하 여 [!INCLUDE[TLA2#tla_uri#plural](../../../../includes/tla2sharptla-urisharpplural-md.md)] <xref:System.Uri?displayProperty=nameWithType>코드에서 지정할 수 있는 다양 한 상대 pack을 보여 줍니다.

표 4: 코드의 상대 Pack Uri

|파일|상대 팩[!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]|
|----------|-------------------------------------------------------------------------------------------------------------------------|
|리소스 파일 - 로컬 어셈블리|`Uri uri = new Uri("/ResourceFile.xaml", UriKind.Relative);`|
|하위 폴더의 리소스 파일 - 로컬 어셈블리|`Uri uri = new Uri("/Subfolder/ResourceFile.xaml", UriKind.Relative);`|
|리소스 파일 - 참조된 어셈블리|`Uri uri = new Uri("/ReferencedAssembly;component/ResourceFile.xaml", UriKind.Relative);`|
|하위 폴더의 리소스 파일 - 참조된 어셈블리|`Uri uri = new Uri("/ReferencedAssembly;component/Subfolder/ResourceFile.xaml", UriKind.Relative);`|
|콘텐츠 파일|`Uri uri = new Uri("/ContentFile.xaml", UriKind.Relative);`|
|하위 폴더의 콘텐츠 파일|`Uri uri = new Uri("/Subfolder/ContentFile.xaml", UriKind.Relative);`|

<a name="Common_Pack_URI_Scenarios"></a>

### <a name="common-pack-uri-scenarios"></a>일반적인 Pack URI 시나리오

이전 섹션에서는 리소스, 콘텐츠 및 원본 사이트 [!INCLUDE[TLA2#tla_uri#plural](../../../../includes/tla2sharptla-urisharpplural-md.md)] 파일을 식별 하는 팩을 구성 하는 방법에 대해 설명 했습니다. 에서 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]이러한 구성은 다양 한 방법으로 사용 되며, 다음 섹션에서는 몇 가지 일반적인 사용법을 다룹니다.

<a name="Specifying_the_UI_to_Show_when_an_Application_Starts"></a>

#### <a name="specifying-the-ui-to-show-when-an-application-starts"></a>애플리케이션을 시작할 때 표시되는 UI 지정

<xref:System.Windows.Application.StartupUri%2A>[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 응용 프로그램이 시작 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 될 때 표시 되는 첫 번째를 지정 합니다. 독립 실행형 응용 프로그램의 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 경우는 다음 예제와 같이 창이 될 수 있습니다.

[!code-xaml[PackURIOverviewSnippets#StartupUriWindow](~/samples/snippets/csharp/VS_Snippets_Wpf/PackURIOverviewSnippets/CS/Copy of App.xaml#startupuriwindow)]

다음 예제와 [!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)] 같이 독립 실행형 응용 프로그램 및에서는 페이지를 초기 UI로 지정할 수도 있습니다.

[!code-xaml[PackURIOverviewSnippets#StartupUriPage](~/samples/snippets/csharp/VS_Snippets_Wpf/PackURIOverviewSnippets/CS/App.xaml#startupuripage)]

응용 프로그램이 독립 실행형 응용 프로그램이 고를 사용 <xref:System.Windows.Application.StartupUri%2A>하 여 페이지를 지정 하는 경우에서 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 페이지를 호스트 <xref:System.Windows.Navigation.NavigationWindow> 하는를 엽니다. 의 [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)]경우 페이지가 호스트 브라우저에 표시 됩니다.

<a name="Navigating_to_a_Page"></a>

#### <a name="navigating-to-a-page"></a>페이지 탐색

다음 예제에서는 페이지를 탐색하는 방법을 보여 줍니다.

[!code-xaml[NavigationOverviewSnippets#HyperlinkXAML1](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/PageWithHyperlink.xaml#hyperlinkxaml1)]
[!code-xaml[NavigationOverviewSnippets#HyperlinkXAML2](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/PageWithHyperlink.xaml#hyperlinkxaml2)]
[!code-xaml[NavigationOverviewSnippets#HyperlinkXAML3](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/PageWithHyperlink.xaml#hyperlinkxaml3)]

에서 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]탐색 하는 다양 한 방법에 대 한 자세한 내용은 [탐색 개요](navigation-overview.md)를 참조 하세요.

<a name="Specifying_a_Window_Icon"></a>

#### <a name="specifying-a-window-icon"></a>창 아이콘 지정

다음 예제에서는 URI를 사용하여 창 아이콘을 지정하는 방법을 보여 줍니다.

[!code-xaml[WindowIconSnippets#WindowIconSetXAML](~/samples/snippets/xaml/VS_Snippets_Wpf/WindowIconSnippets/XAML/MainWindow.xaml#windowiconsetxaml)]

자세한 내용은 <xref:System.Windows.Window.Icon%2A>을 참조하세요.

<a name="Loading_Image__Audio__and_Video_Files"></a>

#### <a name="loading-image-audio-and-video-files"></a>이미지, 오디오 및 비디오 파일 로드

[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]에서는 다음 예제에 표시 된 것 처럼 응용 프로그램에서 다양 한 미디어 형식을 사용할 수 있습니다 .이는 [!INCLUDE[TLA2#tla_uri#plural](../../../../includes/tla2sharptla-urisharpplural-md.md)]모두 pack을 사용 하 여 식별 하 고 로드할 수 있습니다.

[!code-xaml[MediaPlayerVideoSample#VideoPackURIAtSOO](~/samples/snippets/csharp/VS_Snippets_Wpf/MediaPlayerVideoSample/CS/HomePage.xaml#videopackuriatsoo)]

[!code-xaml[MediaPlayerAudioSample#AudioPackURIAtSOO](~/samples/snippets/csharp/VS_Snippets_Wpf/MediaPlayerAudioSample/CS/HomePage.xaml#audiopackuriatsoo)]

[!code-xaml[ImageSample#ImagePackURIContent](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageSample/CS/HomePage.xaml#imagepackuricontent)]

미디어 콘텐츠로 작업 하는 방법에 대 한 자세한 내용은 [그래픽 및 멀티미디어](../graphics-multimedia/index.md)를 참조 하세요.

<a name="Loading_a_Resource_Dictionary_from_the_Site_of_Origin"></a>

#### <a name="loading-a-resource-dictionary-from-the-site-of-origin"></a>원본 사이트에서 리소스 사전 로드

리소스 사전 (<xref:System.Windows.ResourceDictionary>)을 사용 하 여 응용 프로그램 테마를 지원할 수 있습니다. 테마를 만들고 관리하는 한 가지 방법은 애플리케이션의 원본 사이트에 위치한 리소스 사전으로 여러 개의 테마를 만드는 것입니다. 이렇게 하면 애플리케이션을 다시 컴파일하여 배포할 필요 없이 테마를 추가하고 업데이트할 수 있습니다. 다음 예제와 같이 pack [!INCLUDE[TLA2#tla_uri#plural](../../../../includes/tla2sharptla-urisharpplural-md.md)]을 사용 하 여 이러한 리소스 사전을 식별 하 고 로드할 수 있습니다.

[!code-xaml[ResourceDictionarySnippets#ResourceDictionaryPackURI](~/samples/snippets/csharp/VS_Snippets_Wpf/ResourceDictionarySnippets/CS/App.xaml#resourcedictionarypackuri)]

의 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]테마에 대 한 개요는 [스타일 지정 및 템플릿](../controls/styling-and-templating.md)을 참조 하세요.

## <a name="see-also"></a>참고자료

- [WPF 응용 프로그램 리소스, 콘텐츠 및 데이터 파일](wpf-application-resource-content-and-data-files.md)
