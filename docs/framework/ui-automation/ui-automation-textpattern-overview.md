---
title: UI 자동화 TextPattern 개요
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, TextPattern class
- TextPattern class
- classes, TextPattern
ms.assetid: 41787927-df1f-4f4a-aba3-641662854fc4
ms.openlocfilehash: 15638e7da99ef15be58052849bf0675cc21941c9
ms.sourcegitcommit: dfd612ba454ce775a766bcc6fe93bc1d43dfda47
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2019
ms.locfileid: "72180171"
---
# <a name="ui-automation-textpattern-overview"></a>UI 자동화 TextPattern 개요

> [!NOTE]
> 이 설명서는 <xref:System.Windows.Automation> 네임스페이스에 정의된 관리되는 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 클래스를 사용하려는 .NET Framework 개발자를 위한 것입니다. @No__t-0에 대 한 최신 정보는 [Windows Automation API를 참조 하세요. UI 자동화 @ no__t-0.

이 개요에서는 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 을 사용하여 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]이 지원되는 플랫폼에 있는 텍스트 컨트롤의 텍스트 콘텐츠(형식 및 스타일 특성 포함)를 노출하는 방법을 설명합니다. 이러한 컨트롤에는 Microsoft .NET 프레임 워크 <xref:System.Windows.Controls.TextBox> 및 <xref:System.Windows.Controls.RichTextBox>과 해당 [!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)]와 동일 하 게 포함 됩니다.

컨트롤의 텍스트 콘텐츠 노출은 텍스트 컨테이너의 내용을 텍스트 스트림으로 나타내는 <xref:System.Windows.Automation.TextPattern> 컨트롤 패턴을 사용하여 수행됩니다. 다시, <xref:System.Windows.Automation.TextPattern> 을 사용하려면 형식 및 스타일 특성을 노출하는 <xref:System.Windows.Automation.Text.TextPatternRange> 클래스를 지원해야 합니다. <xref:System.Windows.Automation.Text.TextPatternRange>는 <xref:System.Windows.Automation.Text.TextPatternRangeEndpoint.Start> 및 <xref:System.Windows.Automation.Text.TextPatternRangeEndpoint.End> 엔드포인트 컬렉션을 사용하여 텍스트 컨테이너의 연속 텍스트 범위나 여러 비연속 텍스트 범위를 나타내 <xref:System.Windows.Automation.TextPattern>을 지원합니다. <xref:System.Windows.Automation.Text.TextPatternRange> 는 선택, 비교, 검색 및 탐색 등의 기능을 지원합니다.

> [!NOTE]
> <xref:System.Windows.Automation.TextPattern> 클래스는 텍스트를 삽입하거나 수정할 수 있는 방법을 제공하지 않습니다. 그러나 컨트롤에 따라 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] <xref:System.Windows.Automation.ValuePattern> 또는 직접 키보드 입력을 통해 이 작업을 수행할 수 있습니다. 예제는 [TextPattern Insert Text Sample](https://github.com/Microsoft/WPF-Samples/tree/master/Accessibility/InsertText) 을 참조하세요.

이 개요에 설명된 기능은 보조 기술 공급업체 및 최종 사용자에게 중요합니다. 보조 기술은 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 를 사용하여 사용자에 대한 전체 텍스트 형식 정보를 수집하고 <xref:System.Windows.Automation.Text.TextUnit> (문자, 단어, 줄 또는 단락)별로 텍스트의 프로그래밍 방식 탐색 및 선택 기능을 제공합니다.

<a name="UI_Automation_TextPattern_vs__Cicero"></a>

## <a name="ui-automation-textpattern-vs-text-services-framework"></a>UI 자동화 TextPattern과 텍스트 서비스 프레임워크 비교

TSF (텍스트 서비스 프레임 워크)는 데스크톱 및 응용 프로그램 내에서 자연어 서비스 및 고급 텍스트 입력을 사용할 수 있게 해 주는 간단 하 고 확장 가능한 시스템 프레임 워크입니다. 애플리케이션에서 해당 텍스트 저장소를 노출하는 인터페이스를 제공할 뿐 아니라 해당 텍스트 저장소에 대한 메타데이터를 지원합니다.

그러나 TSF는 컨텍스트 인식 시나리오에 입력을 삽입 해야 하는 응용 프로그램용으로 설계 되었지만 <xref:System.Windows.Automation.TextPattern>은 화면 판독기 및 브라유 점자 용 텍스트 저장소에 최적화 된 액세스를 제공 하기 위한 읽기 전용 솔루션 (위에서 언급 한 제한 된 해결 방법 포함)입니다. 디바이스가.

간단히 말해서, 텍스트 저장소에 대 한 읽기 전용 액세스가 필요한 액세스 가능 기술은 <xref:System.Windows.Automation.TextPattern>을 사용할 수 있지만 컨텍스트 인식 입력의 경우 TSF의 더 복잡 한 기능이 필요 합니다.

<a name="Control_Types"></a>

## <a name="control-types"></a>컨트롤 형식

### <a name="text"></a>텍스트

텍스트 컨트롤은 화면에 텍스트 부분을 나타내는 기본 요소입니다.

독립 실행형 텍스트 컨트롤을 폼의 레이블 또는 정적 텍스트로 사용할 수 있습니다. 텍스트 컨트롤을 <xref:System.Windows.Automation.ControlType.ListItem>, <xref:System.Windows.Automation.ControlType.TreeItem> 또는 <xref:System.Windows.Automation.ControlType.DataItem>의 구조 내에 포함할 수도 있습니다.

> [!NOTE]
> @No__t-0 트리의 콘텐츠 뷰에는 텍스트 컨트롤이 나타나지 않을 수 있습니다 ( [UI 자동화 트리 개요](ui-automation-tree-overview.md)참조). 이는 텍스트 컨트롤이 대개 다른 컨트롤의 Name 속성을 통해 표시되기 때문입니다. 예를 들어 편집 컨트롤의 레이블을 지정하는 데 사용되는 텍스트는 편집 컨트롤의 Name 속성을 통해 노출됩니다. 편집 컨트롤이 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리의 콘텐츠 뷰에 있기 때문에 텍스트 요소 자체가 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 트리의 해당 뷰에 있을 필요는 없습니다. 콘텐츠 뷰에 표시되는 텍스트는 중복 정보가 아닌 텍스트뿐입니다. 이렇게 하면 보조 기술이 사용자에게 필요한 정보 부분만 신속하게 필터링할 수 있습니다.

### <a name="edit"></a>편집

편집 컨트롤을 통해 사용자는 텍스트 한 줄을 보고 편집할 수 있습니다.

> [!NOTE]
> 특정 레이아웃 시나리오에서는 텍스트 한 줄이 줄 바꿈될 수도 있습니다.

### <a name="document"></a>문서

문서 컨트롤을 통해 사용자는 여러 텍스트 페이지를 탐색하고 정보를 가져올 수 있습니다.

<a name="TextPattern_Client_API_s"></a>

## <a name="textpattern-client-apis"></a>TextPattern Client Api

|||
|-|-|
|`System.Windows.Automation.TextPattern Class`|[!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 텍스트 모델에 대한 진입점입니다.<br /><br /> 또한 이 클래스에는 두 개의 <xref:System.Windows.Automation.TextPattern> 이벤트 수신기인 <xref:System.Windows.Automation.TextPattern.TextSelectionChangedEvent> 및 <xref:System.Windows.Automation.TextPattern.TextChangedEvent>가 포함됩니다.|
|`System.Windows.Automation.Text.TextPatternRange Class`|<xref:System.Windows.Automation.TextPattern>을 지원하는 텍스트 컨테이너 내의 텍스트 범위 표현입니다.<br /><br /> UI 자동화 클라이언트는 <xref:System.Windows.Automation.Text.TextPatternRange>를 사용하여 만든 텍스트 범위의 현재 유효성에 대해 주의해야 합니다. 텍스트 컨트롤의 원래 텍스트가 새 텍스트로 완전히 대체된 경우 현재 텍스트 범위는 유효하지 않게 됩니다. 그러나 원래 텍스트의 일부만 변경되고 내부 텍스트 컨트롤이 절대 문자 위치 지정 대신 앵커(또는 엔드포인트)로 텍스트 "포인터"를 관리하는 경우 텍스트 범위에 여전히 실행 가능성이 있을 수 있습니다.<br /><br /> 클라이언트는 <xref:System.Windows.Automation.TextPattern.TextChangedEvent> 에서 작업 중인 텍스트 내용에 대한 변경 알림을 수신 대기할 수 있습니다.|
|`System.Windows.Automation.AutomationTextAttribute Class`|텍스트 범위의 형식 특성을 식별하는 데 사용됩니다.|

<a name="TextPattern_Provider_API_s"></a>

## <a name="textpattern-provider-apis"></a>TextPattern 공급자 Api

기본적으로 또는 <xref:System.Windows.Automation.TextPattern> 프록시를 통해 <xref:System.Windows.Automation.Provider.ITextProvider> 및 <xref:System.Windows.Automation.Provider.ITextRangeProvider> 인터페이스를 구현하여 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 을 지원하는 UI 요소나 컨트롤은 강력한 탐색 기능을 제공하는 것 외에도 포함된 텍스트에 대한 자세한 특성 정보를 노출할 수 있습니다.

컨트롤이 특정 특성을 지원하지 않는 경우에는 <xref:System.Windows.Automation.TextPattern> 공급자가 일부 텍스트 특성을 지원하지 않아도 됩니다.

컨트롤이 텍스트 영역 내에서 텍스트 선택이나 텍스트 커서(또는 시스템 캐럿) 배치를 지원하는 경우 <xref:System.Windows.Automation.TextPattern> 공급자가 <xref:System.Windows.Automation.TextPattern.GetSelection%2A> 및 <xref:System.Windows.Automation.Text.TextPatternRange.Select%2A> 함수를 지원해야 합니다. 컨트롤이 이 기능을 지원하지 않는 경우에는 이러한 메서드 중 하나를 지원하지 않아도 됩니다. 그러나 컨트롤은 <xref:System.Windows.Automation.Provider.ITextProvider.SupportedTextSelection%2A> 속성을 구현하여 지원하는 텍스트 선택 유형을 노출해야 합니다.

<xref:System.Windows.Automation.TextPattern> 공급자는 항상 <xref:System.Windows.Automation.Text.TextUnit> 상수인 <xref:System.Windows.Automation.Text.TextUnit.Character> 및 <xref:System.Windows.Automation.Text.TextUnit.Document> 뿐 아니라 지원할 수 있는 다른 <xref:System.Windows.Automation.Text.TextUnit> 상수를 지원해야 합니다.

> [!NOTE]
> 공급자는 <xref:System.Windows.Automation.Text.TextUnit> , <xref:System.Windows.Automation.Text.TextUnit> , <xref:System.Windows.Automation.Text.TextUnit.Character>, <xref:System.Windows.Automation.Text.TextUnit.Format>, <xref:System.Windows.Automation.Text.TextUnit.Word>, <xref:System.Windows.Automation.Text.TextUnit.Line>및 <xref:System.Windows.Automation.Text.TextUnit.Paragraph>순서로 지원되는 다음 가장 큰 <xref:System.Windows.Automation.Text.TextUnit.Page>로 지연하여 특정 <xref:System.Windows.Automation.Text.TextUnit.Document>에 대한 지원을 건너뛸 수 있습니다.

|||
|-|-|
|`ITextProvider Interface`|<xref:System.Windows.Automation.TextPattern> 을 지원하는 메서드, 속성 및 특성을 클라이언트 애플리케이션에 노출합니다( <xref:System.Windows.Automation.Provider.ITextProvider>참조).|
|`ITextRangeProvider Interface`|텍스트 공급자의 텍스트 범위를 나타냅니다( <xref:System.Windows.Automation.Provider.ITextRangeProvider>참조).|
|`System.Windows.Automation.TextPatternIdentifiers Class`|텍스트 공급자의 식별자로 사용되는 값을 포함합니다( <xref:System.Windows.Automation.TextPatternIdentifiers>참조).|

<a name="Security"></a>

## <a name="security"></a>보안

@No__t-0 아키텍처는 보안을 염두에 두면 설계 되었습니다 ( [UI 자동화 보안 개요](ui-automation-security-overview.md)참조). 그러나 이 개요에 설명된 TextPattern 클래스에는 특정 보안 고려 사항이 일부 필요합니다.

- [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 텍스트 공급자는 읽기 전용 인터페이스를 제공하며 컨트롤의 기존 텍스트를 변경하는 기능을 제공하지 않습니다.

- UI 자동화 클라이언트는 완전히 "신뢰할 수 있는" 경우에만 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 을 사용할 수 있습니다. 이러한 예로 알려져 있고 신뢰할 수 있는 애플리케이션만 실행할 수 있는 보호된 로그온 화면이 있습니다.

- UI 자동화 공급자의 개발자는 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 을 통해 해당 컨트롤에 노출하도록 선택한 모든 정보가 기본적으로 공용이며 다른 코드에서 완전히 액세스할 수 있음을 알아야 합니다. [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 에서 UI 자동화 클라이언트를 신뢰할 수 있는지 확인하지 않으므로 UI 자동화 공급자는 보호된 콘텐츠나 중요한 텍스트 정보(예: 암호 필드)를 노출하면 안 됩니다.

- [!INCLUDE[TLA#tla_winvista](../../../includes/tlasharptla-winvista-md.md)] 보안에서 가장 중요한 변경 내용 중 하나를 광범위하게 "안전한 입력"이라고 하며, LUA(최소 권한 (또는 제한됨) 사용자 계정) 및 UIPI(UI 권한 수준 격리)와 같은 기술을 포함합니다.

  - UIPI는 프로그램이 보다 "권한 있는” 다른 프로그램을 제어 및/또는 모니터링할 수 없도록 차단하여 사용자 입력을 스푸핑하는 크로스 프로세스 창 메시지 공격을 방지합니다.

  - LUA는 Administrators 그룹의 사용자가 실행하는 애플리케이션의 권한에 제한을 설정합니다. 애플리케이션에 관리자 권한이 반드시 필요한 것은 아니며 필요한 최소 권한으로 실행됩니다. 결과적으로 LUA 시나리오에서는 몇 가지 제한 사항이 적용될 수 있습니다. 가장 주목할 만한 사항은 문자열 잘림(TextPattern 문자열 포함)입니다. 이 경우 애플리케이션을 사용할 수 없게 되는 지점까지 강제로 메모리를 할당하지 않아도 되도록 관리자 수준 애플리케이션에서 검색되는 문자열의 크기를 제한해야 할 수도 있습니다.

<a name="Performance"></a>

## <a name="performance"></a>성능

TextPattern은 대부분의 기능에 크로스 프로세스 호출을 사용하므로 콘텐츠를 처리할 때 성능을 향상시키기 위한 캐싱 메커니즘을 제공하지 않습니다. 이는 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 또는 <xref:System.Windows.Automation.AutomationElement.GetCachedPattern%2A> 메서드를 사용하여 액세스할 수 있는 <xref:System.Windows.Automation.AutomationElement.TryGetCachedPattern%2A> 의 컨트롤 패턴과는 다릅니다.

성능 향상을 위한 한 가지 방법은 <xref:System.Windows.Automation.Text.TextPatternRange.GetText%2A>를 사용하여 UI 자동화 클라이언트가 적절한 크기의 텍스트 블록을 검색하도록 하는 것입니다. 예를 들어 GetText(1) 호출은 각 문자에 대한 크로스 프로세스 적중을 발생시키고 반면 GetText(-1) 호출은 하나의 크로스 프로세스 적중을 발생시키지만 텍스트 공급자 크기에 따라 대기 시간이 높을 수 있습니다.

<a name="Glossary"></a>

## <a name="textpattern-terminology"></a>TextPattern 용어

**특성**\
텍스트 범위의 형식 특성(예: <xref:System.Windows.Automation.TextPattern.IsItalicAttribute> 또는 <xref:System.Windows.Automation.TextPattern.FontNameAttribute>)입니다.

**중복 제거 범위**\
중복 제거 범위는 비어 있거나 0자 텍스트 범위입니다. TextPattern 컨트롤 패턴의 목적을 위해 텍스트 삽입 지점(또는 시스템 캐럿)은 중복 제거 범위로 간주됩니다. 선택한 텍스트가 없는 경우 <xref:System.Windows.Automation.TextPattern.GetSelection%2A>은 중복 제거 범위를 텍스트 삽입 지점에 반환하고 <xref:System.Windows.Automation.TextPattern.RangeFromPoint%2A>는 중복 제거 범위를 시작 엔드포인트로 반환합니다. 텍스트 공급자가 지정된 조건과 일치하는 텍스트 범위를 찾을 수 없는 경우<xref:System.Windows.Automation.TextPattern.RangeFromChild%2A> 및 <xref:System.Windows.Automation.TextPattern.GetVisibleRanges%2A> 에서 중복 제거 범위를 반환할 수도 있습니다. 이 중복 제거 범위는 텍스트 공급자 내에서 시작 엔드포인트로 사용될 수 있습니다. <xref:System.Windows.Automation.Text.TextPatternRange.FindText%2A> 및 <xref:System.Windows.Automation.Text.TextPatternRange.FindAttribute%2A>은 null 참조 (Microsoft Visual Basic .NET의 `Nothing`)를 반환 하 여 검색 된 범위와 중복 제거 범위가 혼동 되지 않도록 합니다.

**포함 개체**\
[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 텍스트 모델에는 두 가지 유형의 포함 개체가 있습니다. 하이퍼링크 또는 테이블과 같은 텍스트 기반 콘텐츠 요소와 이미지 및 단추와 같은 컨트롤 요소로 구성됩니다. 자세한 내용은 [Access Embedded Objects Using UI Automation](access-embedded-objects-using-ui-automation.md)를 참조하세요.

**끝점**\
텍스트 컨테이너 내에서 텍스트 범위의 절대 <xref:System.Windows.Automation.Text.TextPatternRangeEndpoint.Start> 또는 <xref:System.Windows.Automation.Text.TextPatternRangeEndpoint.End> 지점입니다.

![TextPatternRangeEndpoints &#40;을 시작 하&#41;고 종료 합니다.](./media/uia-textpattern-endpoints.PNG "UIA_TextPattern_Endpoints") 다음은 시작점과 끝점 집합을 보여 줍니다.

**TextRange**\
연결된 모든 특성 및 기능을 포함하여 시작점과 끝점을 사용한 텍스트 컨테이너 내의 텍스트 범위에 대한 표현입니다.

<xref:System.Windows.Automation.Text.TextUnit>\
텍스트 범위의 논리적 세그먼트를 탐색하는 데 사용되는 미리 정의된 텍스트 단위(문자, 단어, 줄 또는 단락)입니다.

## <a name="see-also"></a>참조

- [클라이언트용 UI 자동화 컨트롤 패턴](ui-automation-control-patterns-for-clients.md)
- [UI 자동화 컨트롤 패턴 개요](ui-automation-control-patterns-overview.md)
- [UI 자동화 트리 개요](ui-automation-tree-overview.md)
- [UI 자동화의 캐싱 사용](use-caching-in-ui-automation.md)
- [UI 자동화 공급자의 컨트롤 패턴 지원](support-control-patterns-in-a-ui-automation-provider.md)
- [UI 자동화 클라이언트에 대한 컨트롤 패턴 매핑](control-pattern-mapping-for-ui-automation-clients.md)
- [텍스트 서비스 프레임워크 비교](/windows/desktop/api/_tsf/)
