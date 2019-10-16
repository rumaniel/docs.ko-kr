---
title: 고급 텍스트 서식 지정
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- formatting [WPF]
- text [WPF]
- typography [WPF], text formatting
ms.assetid: f0a7986e-f5b2-485c-a27d-f8e922022212
ms.openlocfilehash: 469c62691ff38a8c5a01bec3ddfd7b324bab7eca
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69969061"
---
# <a name="advanced-text-formatting"></a>고급 텍스트 서식 지정
WPF (Windows Presentation Foundation)는 응용 프로그램에 텍스트를 포함 하기 위한 강력한 Api 집합을 제공 합니다. 과 같은 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]레이아웃 및 api는 <xref:System.Windows.Controls.TextBlock>텍스트 표시에 가장 일반적이 고 일반적으로 사용 되는 요소를 제공 합니다. <xref:System.Windows.Media.GlyphRunDrawing> 및<xref:System.Windows.Media.FormattedText>등의 그리기 api를 사용 하면 서식 있는 텍스트를 드로잉에 포함할 방법이 제공 됩니다. 가장 고급 수준 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 에서는 텍스트 저장소 관리, 텍스트 실행 서식 관리, 포함 된 개체 관리 등 텍스트 표현의 모든 측면을 제어 하는 확장 가능한 텍스트 서식 엔진을 제공 합니다.  
  
 이 항목에서는 텍스트 서식 지정 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 에 대해 소개 합니다. 클라이언트 구현 및 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 텍스트 서식 엔진 사용에 중점을 둘 수 있습니다.  
  
> [!NOTE]
> 이 문서 내의 모든 코드 예제는 [고급 텍스트 서식 지정 샘플](https://go.microsoft.com/fwlink/?LinkID=159965)에서 찾을 수 있습니다.  

<a name="prereq"></a>   
## <a name="prerequisites"></a>전제 조건  
 이 항목에서는 사용자가 텍스트 프레젠테이션에 사용 되는 더 높은 수준의 Api에 대해 잘 알고 있다고 가정 합니다. 대부분의 사용자 시나리오에는이 항목에서 설명 하는 고급 텍스트 서식 지정 Api가 필요 하지 않습니다. 다른 텍스트 Api에 대 한 소개는 [WPF의 문서](documents-in-wpf.md)를 참조 하세요.  
  
<a name="section1"></a>   
## <a name="advanced-text-formatting"></a>고급 텍스트 서식 지정  
 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 의[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 텍스트 레이아웃 및 컨트롤은 응용 프로그램에 서식 있는 텍스트를 쉽게 포함할 수 있도록 하는 서식 속성을 제공 합니다. 이러한 컨트롤은 텍스트의 표현을 처리하는 다양한 속성을 표시하며 서체, 크기 및 색을 포함합니다. 일반적인 상황에서 이러한 컨트롤은 애플리케이션에서 대부분의 텍스트 표현을 처리할 수 있습니다. 그러나 일부 고급 시나리오는 텍스트 표현 뿐만 아니라 텍스트 스토리지 컨트롤이 필요합니다. [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]는 이러한 목적으로 확장 가능한 텍스트 서식 지정 엔진을 제공합니다.  
  
 에 있는 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 고급 텍스트 서식 지정 기능은 텍스트 서식 지정 엔진, 텍스트 저장소, 텍스트 실행 및 서식 속성으로 구성 됩니다. 텍스트 서식 지정 엔진인 <xref:System.Windows.Media.TextFormatting.TextFormatter>는 프레젠테이션에 사용할 텍스트 줄을 만듭니다. 이렇게 하려면 줄 서식 지정 프로세스를 시작 하 고 텍스트 포맷터 <xref:System.Windows.Media.TextFormatting.TextFormatter.FormatLine%2A>를 호출 합니다. 텍스트 포맷터는 저장소의 <xref:System.Windows.Media.TextFormatting.TextSource.GetTextRun%2A> 메서드를 호출 하 여 텍스트 저장소에서 텍스트 실행을 검색 합니다. 그런 <xref:System.Windows.Media.TextFormatting.TextRun> 다음 개체는 텍스트 포맷터 <xref:System.Windows.Media.TextFormatting.TextLine> 에 의해 개체로 구성 되 고 검사 또는 표시를 위해 응용 프로그램에 제공 됩니다.  
  
<a name="section2"></a>   
## <a name="using-the-text-formatter"></a>텍스트 포맷터 사용  
 <xref:System.Windows.Media.TextFormatting.TextFormatter>[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 는 텍스트 서식 지정 엔진 이며 텍스트 줄의 서식 지정 및 줄 바꿈 서비스를 제공 합니다. 텍스트 포맷터는 다양한 텍스트 문자 서식과 단락 스타일을 처리할 수 있으며 국제 텍스트 레이아웃에 대한 지원을 포함합니다.  
  
 기존 텍스트 API와 달리는 <xref:System.Windows.Media.TextFormatting.TextFormatter> 콜백 메서드 집합을 통해 텍스트 레이아웃 클라이언트와 상호 작용 합니다. 구현에서 이러한 메서드를 제공 하기 위해 클라이언트 필요는 <xref:System.Windows.Media.TextFormatting.TextSource> 클래스입니다. 다음 다이어그램에서는 클라이언트 응용 프로그램과 <xref:System.Windows.Media.TextFormatting.TextFormatter>간의 텍스트 레이아웃 상호 작용을 보여 줍니다.  
  
 ![텍스트 레이아웃 클라이언트 및 TextFormatter의 다이어그램](./media/advanced-text-formatting/text-layout-textformatter-interaction.png)  
  
 텍스트 포맷터는의 <xref:System.Windows.Media.TextFormatting.TextSource>구현인 텍스트 저장소에서 서식이 지정 된 텍스트 줄을 검색 하는 데 사용 됩니다. 이 작업은 먼저 메서드를 <xref:System.Windows.Media.TextFormatting.TextFormatter.Create%2A> 사용 하 여 텍스트 포맷터의 인스턴스를 만듭니다. 이 메서드는 텍스트 포맷터의 인스턴스를 생성하고 최대 선 높이 및 너비 값을 설정합니다. 텍스트 포맷터의 인스턴스가 생성 되는 즉시 메서드를 <xref:System.Windows.Media.TextFormatting.TextFormatter.FormatLine%2A> 호출 하 여 줄 만들기 프로세스가 시작 됩니다. <xref:System.Windows.Media.TextFormatting.TextFormatter>텍스트 소스를 다시 호출 하 여 줄을 구성 하는 텍스트의 실행에 대 한 텍스트 및 형식 지정 매개 변수를 검색 합니다.  
  
 다음 예제에서는 텍스트 저장소의 서식 지정 프로세스가 표시됩니다. 개체 <xref:System.Windows.Media.TextFormatting.TextFormatter> 는 텍스트 저장소에서 텍스트 줄을 검색 한 다음에 그릴 <xref:System.Windows.Media.DrawingContext>텍스트 줄의 서식을 지정 하는 데 사용 됩니다.  
  
 [!code-csharp[TextFormatterExample#100](~/samples/snippets/csharp/VS_Snippets_Wpf/TextFormatterExample/CSharp/Window1.xaml.cs#100)]
 [!code-vb[TextFormatterExample#100](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextFormatterExample/VisualBasic/Window1.xaml.vb#100)]  
  
<a name="section3"></a>   
## <a name="implementing-the-client-text-store"></a>클라이언트 텍스트 저장소 구현  
 텍스트 서식 지정 엔진을 확장하는 경우 텍스트 저장소의 모든 측면을 구현하고 관리해야 합니다. 간단한 작업이 아닙니다. 텍스트 저장소는 텍스트 실행 속성, 단락 속성, 포함된 개체 및 이와 비슷한 콘텐츠를 추적합니다. 또한 텍스트 포맷터에서 개체를 만드는 <xref:System.Windows.Media.TextFormatting.TextRun> <xref:System.Windows.Media.TextFormatting.TextLine> 데 사용 하는 개별 개체를 텍스트 포맷터에 제공 합니다.  
  
 텍스트 저장소의 가상화를 처리 하려면 텍스트 저장소가에서 <xref:System.Windows.Media.TextFormatting.TextSource>파생 되어야 합니다. <xref:System.Windows.Media.TextFormatting.TextSource>텍스트 포맷터가 텍스트 저장소에서 텍스트 실행을 검색 하는 데 사용 하는 메서드를 정의 합니다. <xref:System.Windows.Media.TextFormatting.TextSource.GetTextRun%2A>텍스트 포맷터에서 줄 서식 지정에 사용 된 텍스트 실행을 검색 하는 데 사용 하는 방법입니다. 다음 조건 중 <xref:System.Windows.Media.TextFormatting.TextSource.GetTextRun%2A> 하나에 해당 하는 경우에 대 한 호출은 텍스트 포맷터에 의해 반복적으로 수행 됩니다.  
  
- <xref:System.Windows.Media.TextFormatting.TextEndOfLine> 또는 하위 클래스가 반환 됩니다.  
  
- 텍스트 실행의 누적 된 너비가 텍스트 포맷터를 만드는 호출 또는 텍스트 포맷터의 <xref:System.Windows.Media.TextFormatting.TextFormatter.FormatLine%2A> 메서드에 대 한 호출에 지정 된 최대 선 두께를 초과 합니다.  
  
- "CF", "LF" 또는 "CRLF"와 같은 줄바꿈시퀀스가반환됩니다.[!INCLUDE[TLA#tla_unicode](../../../../includes/tlasharptla-unicode-md.md)]  
  
<a name="section4"></a>   
## <a name="providing-text-runs"></a>텍스트 실행 제공  
 텍스트 서식 지정 프로세스의 핵심은 텍스트 포맷터와 텍스트 저장소 간의 상호 작용입니다. 의 <xref:System.Windows.Media.TextFormatting.TextSource> 구현은 텍스트 포맷터 <xref:System.Windows.Media.TextFormatting.TextRun> 에 텍스트의 서식을 지정 하는 데 사용할 개체 및 속성을 제공 합니다. 이 상호 작용은 텍스트 포맷터 <xref:System.Windows.Media.TextFormatting.TextSource.GetTextRun%2A> 에 의해 호출 되는 메서드에 의해 처리 됩니다.  
  
 다음 표에서는 미리 정의 <xref:System.Windows.Media.TextFormatting.TextRun> 된 개체 중 일부를 보여 줍니다.  
  
|TextRun 유형|사용|  
|------------------|-----------|  
|<xref:System.Windows.Media.TextFormatting.TextCharacters>|문자 모양의 표현을 텍스트 포맷터로 다시 전달하는 데 사용된 특수 텍스트 실행.|  
|<xref:System.Windows.Media.TextFormatting.TextEmbeddedObject>|측정, 적중 테스트 및 그리기가 텍스트 내 이미지나 단추에서와 같이 전체적으로 수행되는 컨텐츠를 제공하는 데 사용된 특수 텍스트 실행.|  
|<xref:System.Windows.Media.TextFormatting.TextEndOfLine>|선의 끝을 표시하는 데 사용되는 특수 텍스트 실행.|  
|<xref:System.Windows.Media.TextFormatting.TextEndOfParagraph>|단락의 끝을 표시하는 데 사용되는 특수 텍스트 실행.|  
|<xref:System.Windows.Media.TextFormatting.TextEndOfSegment>|이전 <xref:System.Windows.Media.TextFormatting.TextModifier> 실행의 영향을 받는 범위를 종료 하는 등 세그먼트의 끝을 표시 하는 데 사용 되는 특수 텍스트 실행입니다.|  
|<xref:System.Windows.Media.TextFormatting.TextHidden>|숨겨진 문자 범위를 표시하는 데 사용된 특수 텍스트 실행.|  
|<xref:System.Windows.Media.TextFormatting.TextModifier>|해당 범위에서 텍스트 실행의 속성을 수정하는 데 사용된 특수 텍스트 실행. 범위는 다음에 일치 <xref:System.Windows.Media.TextFormatting.TextEndOfSegment> 하는 텍스트 실행 <xref:System.Windows.Media.TextFormatting.TextEndOfParagraph>으로 확장 됩니다.|  
  
 미리 정의 <xref:System.Windows.Media.TextFormatting.TextRun> 된 개체 중 하나를 서브클래싱 할 수 있습니다. 이렇게 하면 텍스트 소스가 사용자 지정 데이터를 포함하는 텍스트 포맷터와 텍스트 실행을 제공할 수 있습니다.  
  
 다음 예제에서는 메서드를 <xref:System.Windows.Media.TextFormatting.TextSource.GetTextRun%2A> 보여 줍니다. 이 텍스트 저장소는 <xref:System.Windows.Media.TextFormatting.TextRun> 처리를 위해 텍스트 포맷터에 개체를 반환 합니다.  
  
 [!code-csharp[TextFormatterExample#101](~/samples/snippets/csharp/VS_Snippets_Wpf/TextFormatterExample/CSharp/CustomTextSource.cs#101)]
 [!code-vb[TextFormatterExample#101](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextFormatterExample/VisualBasic/CustomTextSource.vb#101)]  
  
> [!NOTE]
> 이 예제에서 텍스트 저장소는 모든 텍스트에 동일한 텍스트 속성을 제공합니다. 고급 텍스트 저장소는 자신의 범위 관리를 구현하여 개별 문자가 다른 속성을 가질 수 있도록 해야 합니다.  
  
<a name="section5"></a>   
## <a name="specifying-formatting-properties"></a>서식 속성 지정  
 <xref:System.Windows.Media.TextFormatting.TextRun>개체는 텍스트 저장소에서 제공 하는 속성을 사용 하 여 형식이 지정 됩니다. 이러한 속성은 <xref:System.Windows.Media.TextFormatting.TextParagraphProperties> 및 <xref:System.Windows.Media.TextFormatting.TextRunProperties>라는 두 가지 형식으로 제공 됩니다. <xref:System.Windows.Media.TextFormatting.TextParagraphProperties><xref:System.Windows.TextAlignment> 및 등의 단락 포함 속성을 <xref:System.Windows.FlowDirection>처리 합니다. <xref:System.Windows.Media.TextFormatting.TextRunProperties>는 전경 브러시, <xref:System.Windows.Media.Typeface>및 글꼴 크기와 같이 단락 내의 각 텍스트 실행에 대해 서로 다를 수 있는 속성입니다. 사용자 지정 단락 및 사용자 지정 텍스트 실행 속성 형식을 구현 하려면 응용 프로그램에서 각각 및 <xref:System.Windows.Media.TextFormatting.TextParagraphProperties> <xref:System.Windows.Media.TextFormatting.TextRunProperties> 에서 파생 되는 클래스를 만들어야 합니다.  
  
## <a name="see-also"></a>참고자료

- [WPF의 입력 체계](typography-in-wpf.md)
- [WPF의 문서](documents-in-wpf.md)
