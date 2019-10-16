---
title: '성능 최적화: 텍스트'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- rendering text [WPF]
- hyperlinks [WPF]
- formatted text [WPF]
- text [WPF], performance
- glyphs [WPF]
ms.assetid: 66b1b9a7-8618-48db-b616-c57ea4327b98
ms.openlocfilehash: 318972c20f6461489226e19b3e517ba0ac069b28
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69933360"
---
# <a name="optimizing-performance-text"></a>성능 최적화: 텍스트

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서는 다양한 기능의 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 컨트롤을 사용하여 텍스트 콘텐츠를 표시할 수 있습니다. 일반적으로 세 가지 계층으로 텍스트 렌더링을 나눌 수 있습니다.

1. <xref:System.Windows.Documents.Glyphs> 및<xref:System.Windows.Media.GlyphRun> 개체를 직접 사용 합니다.

2. 개체를 <xref:System.Windows.Media.FormattedText> 사용 합니다.

3. <xref:System.Windows.Controls.TextBlock> 및<xref:System.Windows.Documents.FlowDocument> 개체와 같은 상위 수준 컨트롤을 사용 합니다.

이 항목에서는 텍스트 렌더링 성능 권장 사항을 제공합니다.

<a name="Glyph_Level"></a>

## <a name="rendering-text-at-the-glyph-level"></a>문자 모양 수준에서 텍스트 렌더링

[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]서식 지정 후 텍스트를 가로채 고 유지 하려는 고객에 대 한 <xref:System.Windows.Documents.Glyphs> 직접 액세스 권한이 있는 문자 수준 태그를 포함 한 고급 텍스트 지원을 제공 합니다. 이러한 기능을 통해 다음과 같은 각 시나리오의 다양한 텍스트 렌더링 요구 사항을 충족시킬 수 있습니다.

- 고정된 형식 문서의 화면 표시

- 인쇄 시나리오

  - 장치 프린터 언어로서의 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]

  - Microsoft XPS Document Writer.

  - 이전 프린터 드라이버, [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] 애플리케이션에서 고정된 형식으로의 출력

  - 인쇄 스풀 형식

- 이전 버전의 Windows 및 기타 컴퓨팅 장치에 대 한 클라이언트를 포함 하는 고정 형식 문서 표시입니다.

> [!NOTE]
> <xref:System.Windows.Documents.Glyphs>및 <xref:System.Windows.Media.GlyphRun> 은 고정 형식의 문서 프레젠테이션 및 인쇄 시나리오를 위해 설계 되었습니다. [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]는 일반적인 레이아웃과 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] <xref:System.Windows.Controls.Label> 및 <xref:System.Windows.Controls.TextBlock>등의 시나리오에 대 한 여러 요소를 제공 합니다. 레이아웃 및 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 시나리오에 대한 자세한 내용은 [WPF의 입력 체계](typography-in-wpf.md)를 참조하세요.

다음 예에서는에서 <xref:System.Windows.Documents.Glyphs> [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]개체에 대 한 속성을 정의 하는 방법을 보여 줍니다. 개체 <xref:System.Windows.Documents.Glyphs> 는의 <xref:System.Windows.Media.GlyphRun> 출력[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]을 나타냅니다. 이 예제에서는 로컬 컴퓨터의 **C:\WINDOWS\Fonts** 폴더에 Arial, Courier New 및 Times New Roman 글꼴이 설치되어 있다고 가정합니다.

[!code-xaml[GlyphsOvwSample1#1](~/samples/snippets/csharp/VS_Snippets_Wpf/GlyphsOvwSample1/CS/default.xaml#1)]

### <a name="using-drawglyphrun"></a>DrawGlyphRun 사용

사용자 지정 컨트롤을 사용 하 고 문자 모양을 렌더링 하려면 <xref:System.Windows.Media.DrawingContext.DrawGlyphRun%2A> 메서드를 사용 합니다.

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]는 또한 <xref:System.Windows.Media.FormattedText> 개체를 사용 하 여 사용자 지정 텍스트 서식 지정을 위한 하위 수준 서비스를 제공 합니다. 에서 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 텍스트를 렌더링 하는 가장 효율적인 방법은 및 <xref:System.Windows.Media.GlyphRun>를 사용 하 여 <xref:System.Windows.Documents.Glyphs> 문자 모양 수준에서 텍스트 콘텐츠를 생성 하는 것입니다. 그러나 이러한 효율성의 비용은 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] <xref:System.Windows.Controls.TextBlock> 및 <xref:System.Windows.Documents.FlowDocument>와 같은 컨트롤의 기본 제공 기능인 서식 있는 텍스트 서식 지정을 사용 하기가 쉽지 않습니다.

<a name="FormattedText_Object"></a>

## <a name="formattedtext-object"></a>FormattedText 개체

<xref:System.Windows.Media.FormattedText> 개체는 각 문자를 텍스트에 서식을 지정할 수 개별적으로 여러 줄 텍스트를 그릴 수 있습니다. 자세한 내용은 [서식 있는 텍스트 그리기](drawing-formatted-text.md)를 참조하세요.

서식 있는 <xref:System.Windows.Media.FormattedText.%23ctor%2A> <xref:System.Windows.Media.FormattedText> 텍스트를 만들려면 생성자를 호출 하 여 개체를 만듭니다. 첫 서식 있는 텍스트 문자열을 만든 다음 다양한 서식 지정 스타일을 적용할 수 있습니다. 응용 프로그램에서 자체 레이아웃을 <xref:System.Windows.Media.FormattedText> 구현 하려는 경우와 <xref:System.Windows.Controls.TextBlock>같은 컨트롤을 사용 하는 것 보다 개체를 선택 하는 것이 좋습니다. <xref:System.Windows.Media.FormattedText> 개체에 대 한 자세한 내용은 서식 있는 [텍스트 그리기](drawing-formatted-text.md) 를 참조 하세요.

개체 <xref:System.Windows.Media.FormattedText> 는 하위 수준 텍스트 서식 지정 기능을 제공 합니다. 하나 이상의 문자에 여러 서식 지정 스타일을 적용할 수 있습니다. 예를 들어 <xref:System.Windows.Media.FormattedText.SetFontSize%2A> 및 <xref:System.Windows.Media.FormattedText.SetForegroundBrush%2A> 메서드를 모두 호출 하 여 텍스트에서 처음 5 개 문자의 형식을 변경할 수 있습니다.

다음 코드 예제에서는 개체를 <xref:System.Windows.Media.FormattedText> 만들어 렌더링 합니다.

[!code-csharp[formattedtextsnippets#FormattedTextSnippets1](~/samples/snippets/csharp/VS_Snippets_Wpf/FormattedTextSnippets/CSharp/Window1.xaml.cs#formattedtextsnippets1)]
[!code-vb[formattedtextsnippets#FormattedTextSnippets1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FormattedTextSnippets/visualbasic/window1.xaml.vb#formattedtextsnippets1)]

<a name="FlowDocument_TextBlock_Label"></a>

## <a name="flowdocument-textblock-and-label-controls"></a>FlowDocument, TextBlock 및 Label 컨트롤

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에서는 화면에 텍스트를 그리는 데 사용하는 여러 컨트롤이 포함되어 있습니다. 각 컨트롤은 다른 시나리오를 대상으로 하며 고유 기능 및 제한 사항 목록을 가지고 있습니다.

### <a name="flowdocument-impacts-performance-more-than-textblock-or-label"></a>FlowDocument가 TextBlock 또는 Label 이외의 성능에 미치는 영향

일반적으로 <xref:System.Windows.Controls.TextBlock> [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]의 간단한 문장 처럼 제한 된 텍스트 지원이 필요한 경우 요소를 사용 해야 합니다. <xref:System.Windows.Controls.Label>최소 텍스트 지원이 필요한 경우에 사용할 수 있습니다. 요소는 풍부한 콘텐츠 프레젠테이션을 지 원하는 문서를 다시 만들기 위한 컨테이너 이므로 <xref:System.Windows.Controls.TextBlock> 또는 <xref:System.Windows.Controls.Label> 컨트롤을 사용 하는 것 보다 성능에 더 큰 영향을 줍니다. <xref:System.Windows.Documents.FlowDocument>

에 대 <xref:System.Windows.Documents.FlowDocument>한 자세한 내용은 [유동 문서 개요](flow-document-overview.md)를 참조 하세요.

### <a name="avoid-using-textblock-in-flowdocument"></a>FlowDocument에서 TextBlock 사용 안 함

요소 <xref:System.Windows.Controls.TextBlock> 는에서 <xref:System.Windows.UIElement>파생 됩니다. 요소 <xref:System.Windows.Documents.Run> 는 파생 개체 보다 <xref:System.Windows.Documents.TextElement> <xref:System.Windows.UIElement>사용 하기에 비용이 저렴 한에서 파생 됩니다. 가능 하면에서 텍스트 <xref:System.Windows.Documents.Run> 콘텐츠를 <xref:System.Windows.Controls.TextBlock> <xref:System.Windows.Documents.FlowDocument>표시 하는 대신를 사용 합니다.

다음 태그 샘플은에서 텍스트 콘텐츠를 설정 하 <xref:System.Windows.Documents.FlowDocument>는 두 가지 방법을 보여 줍니다.

[!code-xaml[Performance#PerformanceSnippet13](~/samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/FlowDocument.xaml#performancesnippet13)]

### <a name="avoid-using-run-to-set-text-properties"></a>텍스트 속성을 설정하여 실행 사용 방지

일반적으로 <xref:System.Windows.Documents.Run> <xref:System.Windows.Documents.Run> 내에서를 사용 하는 것은명시적개체를전혀사용하지않는것보다성능이더좋습니다.<xref:System.Windows.Controls.TextBlock> 텍스트 속성을 설정 하기 <xref:System.Windows.Documents.Run> 위해를 사용 하는 경우에는 <xref:System.Windows.Controls.TextBlock> 에서 직접 해당 속성을 설정 합니다.

다음 태그 예제에서는 텍스트 속성 (이 경우 <xref:System.Windows.Controls.TextBlock.FontWeight%2A> 속성)을 설정 하는 두 가지 방법을 보여 줍니다.

[!code-xaml[Performance#PerformanceSnippet12](~/samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Window1.xaml#performancesnippet12)]

다음 표에서는 명시적 <xref:System.Windows.Controls.TextBlock> <xref:System.Windows.Documents.Run>이 없는 1000 개체를 표시 하는 비용을 보여 줍니다.

|**TextBlock 형식**|**만든 시간(ms)**|**렌더링 시간(ms)**|
|------------------------|------------------------------|----------------------------|
|Run 설정 텍스트 속성|146|540|
|TextBlock 설정 텍스트 속성|43|453|

### <a name="avoid-databinding-to-the-labelcontent-property"></a>Label.Content 속성에 데이터 바인딩 방지

원본에서 자주 업데이트 되는 <xref:System.Windows.Controls.Label> 개체가 있는 시나리오를 가정해 보겠습니다. <xref:System.String> 요소 속성을 <xref:System.String> 소스 개체에 바인딩하는 경우 성능이 저하 될 수 있습니다. <xref:System.Windows.Controls.ContentControl.Content%2A> <xref:System.Windows.Controls.Label> 소스가 <xref:System.String> 업데이트 될 때마다 이전 <xref:System.String> 개체가 삭제 되 고 새 <xref:System.String> 이 다시 생성 됩니다. 개체는 <xref:System.String> 변경할 수 없기 때문에 수정할 수 없습니다. 이렇게 하면 <xref:System.Windows.Controls.ContentPresenter> <xref:System.Windows.Controls.Label> 개체의가 이전 콘텐츠를 삭제 하 고 새 콘텐츠를 다시 생성 하 여 새 <xref:System.String>를 표시 합니다.

이 문제에 대한 해결책은 간단합니다. <xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> <xref:System.Windows.Controls.Label> <xref:System.Windows.Controls.TextBlock> 이 사용자 지정 값으로 설정 되지 않은 경우를로 바꾸고 데이터를 해당 <xref:System.Windows.Controls.TextBlock.Text%2A> 속성을 원본 문자열에 바인딩합니다. <xref:System.Windows.Controls.Label>

|**데이터 바인딩된 속성**|**업데이트 시간(ms)**|
|-----------------------------|----------------------------|
|Label.Content|835|
|TextBlock.Text|242|

<a name="Hyperlink"></a>

## <a name="hyperlink"></a>하이퍼링크

개체 <xref:System.Windows.Documents.Hyperlink> 는 유동 콘텐츠 내에서 하이퍼링크를 호스트 하는 데 사용할 수 있는 인라인 수준의 유동 콘텐츠 요소입니다.

### <a name="combine-hyperlinks-in-one-textblock-object"></a>하나의 TextBlock 개체에 대한 하이퍼링크 결합

<xref:System.Windows.Documents.Hyperlink> 동일한<xref:System.Windows.Controls.TextBlock>내에서 함께 그룹화 하 여 여러 요소의 사용을 최적화할 수 있습니다. 이렇게 하면 애플리케이션에서 만드는 개체의 수를 최소화할 수 있습니다. 예를 들어 다음과 같은 여러 개의 하이퍼링크를 표시할 수 있습니다.

MSN 홈 &#124; 내 MSN

다음 태그 예제에서는 하이퍼링크를 <xref:System.Windows.Controls.TextBlock> 표시 하는 데 사용 되는 여러 요소를 보여 줍니다.

[!code-xaml[Performance#PerformanceSnippet9](~/samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Hyperlink.xaml#performancesnippet9)]

다음 태그 예제에서는 단일 <xref:System.Windows.Controls.TextBlock>를 사용 하 여 하이퍼링크를 표시 하는 보다 효율적인 방법을 보여 줍니다.

[!code-xaml[Performance#PerformanceSnippet10](~/samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Hyperlink.xaml#performancesnippet10)]

### <a name="showing-underlines-on-hyperlinks-only-on-mouseenter-events"></a>MouseEnter 이벤트에만 하이퍼링크에 밑줄 표시

<xref:System.Windows.TextDecoration> 개체는 텍스트에 추가할 수 있는 시각적 장식, 인스턴스화하는 것이 더 나을 수 있습니다. <xref:System.Windows.Documents.Hyperlink> 요소를 광범위 하 게 사용 하는 경우 이벤트 <xref:System.Windows.ContentElement.MouseEnter> 와 같은 이벤트를 트리거할 때만 밑줄을 표시 하는 것이 좋습니다. 자세한 내용은 [하이퍼링크에 밑줄이 그어지는지 여부 지정](how-to-specify-whether-a-hyperlink-is-underlined.md)을 참조하세요.

다음 이미지는 MouseEnter 이벤트가 밑줄이 그어진 하이퍼링크를 트리거하는 방법을 보여 줍니다.

![TextDecoration을 표시하는 하이퍼링크](./media/how-to-specify-whether-a-hyperlink-is-underlined/text-decorations-hyperlinks.png)

다음 태그 샘플은 <xref:System.Windows.Documents.Hyperlink> 와 밑줄 없이 정의 합니다.

[!code-xaml[Performance#PerformanceSnippet11](~/samples/snippets/csharp/VS_Snippets_Wpf/Performance/CSharp/Hyperlink.xaml#performancesnippet11)]

다음 표에서는 밑줄 없이 1000 <xref:System.Windows.Documents.Hyperlink> 요소를 표시 하는 성능 비용을 보여 줍니다.

|**하이퍼링크**|**만든 시간(ms)**|**렌더링 시간(ms)**|
|-------------------|------------------------------|----------------------------|
|밑줄 있음|289|1130|
|밑줄 없음|299|776|

<a name="Text_Formatting_Features"></a>

## <a name="text-formatting-features"></a>텍스트 서식 지정 기능

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]는 자동 하이픈 넣기 등 서식 있는 텍스트 서식 지정 서비스를 제공합니다. 이러한 서비스는 애플리케이션 성능에 영향을 줄 수 있으며 필요한 경우에만 사용해야 합니다.

### <a name="avoid-unnecessary-use-of-hyphenation"></a>불필요한 하이픈 넣기 사용 안 함

자동 하이픈 넣기는 텍스트 줄에 대 한 하이픈 중단점을 검색 하 고 및 <xref:System.Windows.Controls.TextBlock> <xref:System.Windows.Documents.FlowDocument> 개체의 줄에 대해 추가 중단 위치를 허용 합니다. 기본적으로 이러한 개체에서는 자동 하이픈 넣기 기능이 사용하지 않도록 설정됩니다. 개체의 IsHyphenationEnabled 속성을 `true`로 설정하여 이 기능을 사용하도록 설정할 수 있습니다. 그러나이 기능 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 을 사용 하도록 설정 하면에서 COM (구성 요소 개체 모델) 상호 운용성이 시작 되어 응용 프로그램 성능에 영향을 줄 수 있습니다. 꼭 필요한 경우가 아니면 자동 하이픈 넣기를 사용하지 않는 것이 좋습니다.

### <a name="use-figures-carefully"></a>신중하게 그림 사용

요소 <xref:System.Windows.Documents.Figure> 는 콘텐츠 페이지 내에서 절대적으로 배치 될 수 있는 유동 콘텐츠의 일부를 나타냅니다. 일부 경우에는 <xref:System.Windows.Documents.Figure> 해당 위치가 이미 배치 된 콘텐츠와 충돌 하는 경우 전체 페이지의 서식이 자동으로 다시 지정 될 수 있습니다. 서로 다른 요소를 그룹화 <xref:System.Windows.Documents.Figure> 하거나 고정 된 페이지 크기 시나리오에서 콘텐츠의 위쪽에 선언 하 여 불필요 한 서식 다시 서식이 발생할 가능성을 최소화할 수 있습니다.

### <a name="optimal-paragraph"></a>최적 단락

<xref:System.Windows.Documents.FlowDocument> 개체의 최적 단락 기능은 공백을 최대한 균등 하 게 배분 하도록 단락을 배치 합니다. 기본적으로 최적 단락 기능은 사용하지 않도록 설정됩니다. 개체의 <xref:System.Windows.Documents.FlowDocument.IsOptimalParagraphEnabled%2A> 속성을로 설정 하 여이 기능을 `true`사용 하도록 설정할 수 있습니다. 그러나 이 기능을 사용하면 애플리케이션 성능에 영향을 미칩니다. 꼭 필요한 경우가 아니면 최적 단락 기능을 사용하지 않는 것이 좋습니다.

## <a name="see-also"></a>참고자료

- [WPF 응용 프로그램 성능 최적화](optimizing-wpf-application-performance.md)
- [애플리케이션 성능 계획](planning-for-application-performance.md)
- [하드웨어 이용](optimizing-performance-taking-advantage-of-hardware.md)
- [레이아웃 및 디자인](optimizing-performance-layout-and-design.md)
- [2차원 그래픽 및 이미징](optimizing-performance-2d-graphics-and-imaging.md)
- [개체 동작](optimizing-performance-object-behavior.md)
- [응용 프로그램 리소스](optimizing-performance-application-resources.md)
- [데이터 바인딩](optimizing-performance-data-binding.md)
- [기타 성능 권장 사항](optimizing-performance-other-recommendations.md)
