---
title: TextPattern 및 포함 개체 개요
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, TextPattern class
- embedded objects, accessing
- accessing embedded objects
- embedded objects, UI Automation
ms.assetid: 93fdfbb9-0025-4b72-8ca0-0714adbb70d5
ms.openlocfilehash: e577b9d221760544e95b1d6098d0becbf5d776b0
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71042674"
---
# <a name="textpattern-and-embedded-objects-overview"></a>TextPattern 및 포함 개체 개요
> [!NOTE]
> 이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. 에 대 한 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] [최신 정보는 Windows Automation API: UI 자동화](https://go.microsoft.com/fwlink/?LinkID=156746).  
  
 이 개요에서는 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 에서 포함된 개체 또는 자식 요소를 텍스트 문서나 컨테이너 내에서 노출하는 방법을 설명합니다.  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 에서 포함된 개체란 예를 들어 이미지, 하이퍼링크, 테이블 또는 [!INCLUDE[TLA#tla_xl](../../../includes/tlasharptla-xl-md.md)] 스프레드시트나 [!INCLUDE[TLA#tla_winmedia](../../../includes/tlasharptla-winmedia-md.md)] 파일 등의 문서 형식과 같이 텍스트가 아닌 범위를 가진 요소입니다. 이는 요소가 한 애플리케이션에서 만들어져 다른 애플리케이션 내에서 포함 또는 연결되는 표준 정의와 다릅니다. [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]에서는 개체를 원래 응용 프로그램 내에서 편집할 수 있는지 여부가 중요하지 않습니다.  
  
<a name="Embedded_Objects_and_the_UI_Automation_Tree"></a>   
## <a name="embedded-objects-and-the-ui-automation-tree"></a>포함된 개체 및 UI 자동화 트리  
 포함된 개체는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리의 컨트롤 뷰에서 개별 요소로 처리됩니다. 텍스트 컨테이너의 자식으로 노출되어, [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]의 다른 컨트롤과 동일한 모델을 통해 이들 개체에 액세스할 수 있습니다.  
  
 ![텍스트 컨테이너에 이미지가 있는 포함 테이블](./media/uia-textpattern-embedded-objects-overview-example1.png "UIA_TextPattern_Embedded_Objects_Overview_Example1")  
테이블, 이미지, 하이퍼링크 등의 포함된 개체가 있는 텍스트 컨테이너의 예  
  
 ![이전 예제에 대 한 콘텐츠 뷰](./media/uia-textpattern-embedded-objects-overview-example2.PNG "UIA_TextPattern_Embedded_Objects_Overview_Example2")  
이전 텍스트 컨테이너의 일부를 보여 주는 콘텐츠 뷰의 예  
  
<a name="Expose_Embedded_Objects_Using_TextPattern_and"></a>   
## <a name="expose-embedded-objects-using-textpattern-and-textpatternrange"></a>TextPattern 및 TextPatternRange를 사용하여 포함된 개체 노출  
 <xref:System.Windows.Automation.TextPattern> 컨트롤 패턴 클래스와 <xref:System.Windows.Automation.Text.TextPatternRange> 클래스를 함께 사용하면 포함된 개체의 탐색과 쿼리를 돕는 메서드와 속성이 노출됩니다.  
  
 텍스트 컨테이너 및 포함된 개체(예: 하이퍼링크 또는 테이블 셀)의 텍스트 내용(또는 내부 텍스트)은 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리의 컨트롤 뷰와 콘텐츠 뷰에서 지속적인 단일 텍스트 스트림으로 노출됩니다. 개체 경계는 무시됩니다. UI 자동화 클라이언트가 낭독, 해석 또는 분석의 목적으로 텍스트를 특정 방식으로 검색하는 경우 텍스트 내용이나 기타 포함된 개체가 있는 테이블과 같이 특수한 경우가 텍스트 범위에 있는지 확인해야 합니다. 이렇게 하려면 <xref:System.Windows.Automation.Text.TextPatternRange.GetChildren%2A> 을 호출하여 각 포함된 개체에 대한 <xref:System.Windows.Automation.AutomationElement> 를 가져온 다음 <xref:System.Windows.Automation.TextPattern.RangeFromChild%2A> 를 호출하여 각 요소의 텍스트 범위를 가져오면 됩니다. 이 과정은 모든 텍스트 내용이 검색될 때까지 반복적으로 수행됩니다.  
  
 ![포함 된 개체에 의해 확장 되는 텍스트 범위입니다.](./media/uia-textpattern-embeddedobjecttextranges.png "UIA_TextPattern_EmbeddedObjectTextRanges")  
포함된 개체가 있는 텍스트 스트림과 해당 범위의 예  
  
 텍스트 범위의 내용을 이동해야 하는 경우 <xref:System.Windows.Automation.Text.TextPatternRange.Move%2A> 메서드가 성공적으로 실행되려면 백그라운드에서 일련의 단계를 거쳐야 합니다.  
  
1. 텍스트 범위가 정규화됩니다. 다시 말해서, 텍스트 범위가 <xref:System.Windows.Automation.Text.TextPatternRangeEndpoint.Start> 엔드포인트에서 중복 제거 범위로 축소되어 <xref:System.Windows.Automation.Text.TextPatternRangeEndpoint.End> 엔드포인트가 불필요해집니다. 이 단계는 텍스트 범위가 경계를 확장 <xref:System.Windows.Automation.Text.TextUnit> 하는 상황에서 모호성을 제거 하는 데 필요 합니다. 예를 `{The URL https://www.microsoft.com is embedded in text` 들어 "{" 및 "}"는 텍스트 범위 끝점입니다.  
  
2. 결과 범위가 <xref:System.Windows.Automation.TextPattern.DocumentRange%2A> 내에서 뒤쪽으로 옮겨져 요청된 <xref:System.Windows.Automation.Text.TextUnit> 경계의 시작 부분으로 이동하게 됩니다.  
  
3. 범위가 요청된 <xref:System.Windows.Automation.TextPattern.DocumentRange%2A> 경계 수만큼 <xref:System.Windows.Automation.Text.TextUnit> 내에서 앞이나 뒤로 이동합니다.  
  
4. 그런 다음, 요청된 <xref:System.Windows.Automation.Text.TextUnit> 경계 하나만큼 <xref:System.Windows.Automation.Text.TextPatternRangeEndpoint.End> 엔드포인트를 이동하여 중복 제거 범위 상태이던 범위가 확장됩니다.  
  
 ![이동 & ExpandToEnclosingUnit 범위 조정](./media/uia-textpattern-moveandexpand-examples.png "UIA_TextPattern_MoveAndExpand_Examples")  
Move() 및 ExpandToEnclosingUnit()에 따라 텍스트 범위가 조정되는 방법의 예  
  
<a name="Common_Scenarios"></a>   
## <a name="common-scenarios"></a>일반적인 시나리오  
 다음 섹션에서는 포함된 개체와 관련된 가장 일반적인 시나리오의 예를 소개합니다.  
  
 예제의 범례:  
  
 { = <xref:System.Windows.Automation.Text.TextPatternRangeEndpoint.Start>  
  
 } = <xref:System.Windows.Automation.Text.TextPatternRangeEndpoint.End>  
  
### <a name="hyperlink"></a>하이퍼링크  

**예제 1 - 포함된 텍스트 하이퍼링크가 들어 있는 텍스트 범위**
  
`{The URL https://www.microsoft.com is embedded in text}.`
  
|호출되는 메서드|결과|  
|-------------------|------------|  
|<xref:System.Windows.Automation.Text.TextPatternRange.GetText%2A>|`The URL https://www.microsoft.com is embedded in text` 문자열을 반환합니다.|  
|<xref:System.Windows.Automation.Text.TextPatternRange.GetEnclosingElement%2A>|텍스트 범위를 포함하는 가장 안쪽의 <xref:System.Windows.Automation.AutomationElement> 를 반환합니다. 이 예제에서는 텍스트 공급자 자체를 나타내는 <xref:System.Windows.Automation.AutomationElement> 입니다.|  
|<xref:System.Windows.Automation.Text.TextPatternRange.GetChildren%2A>|하이퍼링크 컨트롤을 나타내는 <xref:System.Windows.Automation.AutomationElement> 를 반환합니다.|  
|<xref:System.Windows.Automation.TextPattern.RangeFromChild%2A> 여기서 <xref:System.Windows.Automation.AutomationElement> 는 이전 `GetChildren` 메서드에서 반환되는 개체입니다.|나타내는 범위를 반환 합니다. "https://www.microsoft.com" 입니다.|  
  
 **예제 2 - 포함된 텍스트 하이퍼링크에 부분적으로 걸쳐 있는 텍스트 범위**  
  
 URL `https://{[www]}` 은 텍스트에 포함 되어 있습니다.  
  
|호출되는 메서드|결과|  
|-------------------|------------|  
|<xref:System.Windows.Automation.Text.TextPatternRange.GetText%2A>|문자열 "www"를 반환합니다.|  
|<xref:System.Windows.Automation.Text.TextPatternRange.GetEnclosingElement%2A>|텍스트 범위를 포함하는 가장 안쪽의 <xref:System.Windows.Automation.AutomationElement> 를 반환합니다. 이 예제에서는 하이퍼링크를 컨트롤입니다.|  
|<xref:System.Windows.Automation.Text.TextPatternRange.GetChildren%2A>|텍스트 범위가 전체 URL 문자열로 확장되지 않기 때문에 `null` 을 반환합니다.|  
  
**예 3-텍스트 컨테이너의 내용에 부분적으로 걸쳐 있는 텍스트 범위 텍스트 컨테이너에 텍스트 범위의 일부가 아닌 포함 된 텍스트 하이퍼링크가 있습니다.**  
  
`{The URL} [https://www.microsoft.com](https://www.microsoft.com) is embedded in text.`
  
|호출되는 메서드|결과|  
|-------------------|------------|  
|<xref:System.Windows.Automation.Text.TextPatternRange.GetText%2A>|문자열 "The URL"을 반환합니다.|  
|<xref:System.Windows.Automation.Text.TextPatternRange.GetEnclosingElement%2A>|텍스트 범위를 포함하는 가장 안쪽의 <xref:System.Windows.Automation.AutomationElement> 를 반환합니다. 이 예제에서는 텍스트 공급자 자체를 나타내는 <xref:System.Windows.Automation.AutomationElement> 입니다.|  
|<xref:System.Windows.Automation.Text.TextPatternRange.Move%2A> 매개 변수는 (TextUnit.Word, 1)|하이퍼링크의 텍스트가 개별 단어로 이루어져 있으므로 텍스트 범위를 "http"로 이동합니다. 이 경우 하이퍼링크는 단일 개체로 처리되지 않습니다.<br /><br /> URL {[http]}가 텍스트에 포함 되어 있습니다.|  
  
<a name="Image"></a>   
### <a name="image"></a>이미지  
 **예제 1 - 포함된 이미지가 들어 있는 텍스트 범위**  
  
 {이미지 ![포함 이미지 예](./media/uia-textpattern-embedded-objects-overview-imageexample.PNG "UIA_TextPattern_Embedded_Objects_Overview_ImageExample") 는 text}에 포함 되어 있습니다.  
  
|호출되는 메서드|결과|  
|-------------------|------------|  
|<xref:System.Windows.Automation.Text.TextPatternRange.GetText%2A>|문자열 "The is embedded in text"를 반환합니다. 이미지에 연결된 대체 텍스트는 텍스트 스트림에 포함된다고 기대할 수 없습니다.|  
|<xref:System.Windows.Automation.Text.TextPatternRange.GetEnclosingElement%2A>|텍스트 범위를 포함하는 가장 안쪽의 <xref:System.Windows.Automation.AutomationElement> 를 반환합니다. 이 예제에서는 텍스트 공급자 자체를 나타내는 <xref:System.Windows.Automation.AutomationElement> 입니다.|  
|<xref:System.Windows.Automation.Text.TextPatternRange.GetChildren%2A>|이미지 컨트롤을 나타내는 <xref:System.Windows.Automation.AutomationElement> 를 반환합니다.|  
|<xref:System.Windows.Automation.TextPattern.RangeFromChild%2A> 여기서 <xref:System.Windows.Automation.AutomationElement> 는 이전 <xref:System.Windows.Automation.Text.TextPatternRange.GetChildren%2A> 메서드에서 반환되는 개체입니다.|"![포함 이미지 예](./media/uia-textpattern-embedded-objects-overview-imageexample.PNG "UIA_TextPattern_Embedded_Objects_Overview_ImageExample")"를 나타내는 중복 제거 범위를 반환 합니다.|  
  
 **예 2-텍스트 컨테이너의 내용에 부분적으로 걸쳐 있는 텍스트 범위 텍스트 컨테이너에 텍스트 범위의 일부가 아닌 포함 이미지가 있습니다.**  
  
 {이미지} ![포함 이미지 예제](./media/uia-textpattern-embedded-objects-overview-imageexample.PNG "UIA_TextPattern_Embedded_Objects_Overview_ImageExample") 가 텍스트에 포함 되어 있습니다.  
  
|호출되는 메서드|결과|  
|-------------------|------------|  
|<xref:System.Windows.Automation.Text.TextPatternRange.GetText%2A>|문자열 "The image"를 반환합니다.|  
|<xref:System.Windows.Automation.Text.TextPatternRange.GetEnclosingElement%2A>|텍스트 범위를 포함하는 가장 안쪽의 <xref:System.Windows.Automation.AutomationElement> 를 반환합니다. 이 예제에서는 텍스트 공급자 자체를 나타내는 <xref:System.Windows.Automation.AutomationElement> 입니다.|  
|<xref:System.Windows.Automation.Text.TextPatternRange.Move%2A> 매개 변수는 (TextUnit.Word, 1)|텍스트 범위를 "is "로 이동합니다. 텍스트 기반의 포함된 개체만 텍스트 스트림의 일부로 간주되므로, 이 예제의 이미지는 이동 또는 해당 반환 값(이 경우 1)에 영향을 주지 않습니다.|  
  
<a name="Table"></a>   
### <a name="table"></a>표  
  
### <a name="table-used-for-examples"></a>예제에서 사용되는 테이블  
  
|이미지가 있는 셀|텍스트가 있는 셀|  
|---------------------|--------------------|  
|![포함 이미지 예제](./media/uia-textpattern-embedded-objects-overview-imageexample.PNG "UIA_TextPattern_Embedded_Objects_Overview_ImageExample")|X|  
|![포함 이미지 예 2](./media/uia-textpattern-embedded-objects-overview-imageexample2.PNG "UIA_TextPattern_Embedded_Objects_Overview_ImageExample2")|Y|  
|![포함 이미지 예제 3](./media/uia-textpattern-embedded-objects-overview-imageexample3.PNG "UIA_TextPattern_Embedded_Objects_Overview_ImageExample3")<br /><br /> Z의 이미지|Z|  
  
 **예제 1 - 셀의 내용에서 텍스트 컨테이너 가져오기**  
  
|호출되는 메서드|결과|  
|-------------------|------------|  
|<xref:System.Windows.Automation.GridPattern.GetItem%2A> 매개 변수는 (0, 0)|테이블 셀의 내용을 나타내는 <xref:System.Windows.Automation.AutomationElement> 를 반환합니다. 이 예제에서 요소는 텍스트 컨트롤입니다.|  
|<xref:System.Windows.Automation.TextPattern.RangeFromChild%2A> 여기서 <xref:System.Windows.Automation.AutomationElement> 는 이전 `GetItem` 메서드에서 반환되는 개체입니다.|이미지 ![포함 이미지 예제](./media/uia-textpattern-embedded-objects-overview-imageexample.PNG "UIA_TextPattern_Embedded_Objects_Overview_ImageExample")에 걸쳐 있는 범위를 반환 합니다.|  
|이전<xref:System.Windows.Automation.Text.TextPatternRange.GetEnclosingElement%2A> 메서드에서 반환되는 개체에 대한 `RangeFromChild` 입니다.|테이블 셀을 나타내는 <xref:System.Windows.Automation.AutomationElement> 를 반환합니다. 이 예제에서 요소는 TableItemPattern을 지원하는 텍스트 컨트롤입니다.|  
|이전 `GetEnclosingElement` 메서드에서 반환되는 개체에 대한 <xref:System.Windows.Automation.Text.TextPatternRange.GetEnclosingElement%2A>입니다.|테이블을 나타내는 <xref:System.Windows.Automation.AutomationElement> 를 반환합니다.|  
|이전<xref:System.Windows.Automation.Text.TextPatternRange.GetEnclosingElement%2A> 메서드에서 반환되는 개체에 대한 `GetEnclosingElement` 입니다.|텍스트 공급자 자체를 나타내는 <xref:System.Windows.Automation.AutomationElement> 를 반환합니다.|  
  
 **예제 2 - 셀의 텍스트 콘텐츠 가져오기**  
  
|호출되는 메서드|결과|  
|-------------------|------------|  
|<xref:System.Windows.Automation.GridPattern.GetItem%2A> 매개 변수는 (1,1)|테이블 셀의 내용을 나타내는 <xref:System.Windows.Automation.AutomationElement>를 반환합니다. 이 예제에서 요소는 텍스트 컨트롤입니다.|  
|<xref:System.Windows.Automation.TextPattern.RangeFromChild%2A> 여기서 <xref:System.Windows.Automation.AutomationElement>는 이전 `GetItem` 메서드에서 반환되는 개체입니다.|"Y"를 반환합니다.|  
  
## <a name="see-also"></a>참고자료

- <xref:System.Windows.Automation.TextPattern>
- <xref:System.Windows.Automation.Text.TextPatternRange>
- <xref:System.Windows.Automation.Provider.ITextProvider>
- <xref:System.Windows.Automation.Provider.ITextRangeProvider>
- [UI 자동화를 사용하여 포함 개체에 액세스](access-embedded-objects-using-ui-automation.md)
- [UI 자동화를 사용하여 표의 콘텐츠 노출](expose-the-content-of-a-table-using-ui-automation.md)
- [UI 자동화를 사용하여 텍스트 이동](traverse-text-using-ui-automation.md)
- [TextPattern 검색 및 선택 샘플](https://github.com/Microsoft/WPF-Samples/tree/master/Accessibility/FindText)
