---
title: WPF 콘텐츠 모델
ms.date: 03/30/2017
helpviewer_keywords:
- UIElement class [WPF], displaying content
- content model [WPF], controls
- controls [WPF], displaying text
- content display [WPF], controls
- controls [WPF], formatting text
- displaying content [WPF]
- arbitrary content classes [WPF], content model
- ContentControl class [WPF], displaying content
ms.assetid: 214da5ef-547a-4cf8-9b07-4aa8a0e52cdd
ms.openlocfilehash: 652a8b831d29c8da8dc651558351a5bd4ff5ce84
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64665177"
---
# <a name="wpf-content-model"></a>WPF 콘텐츠 모델
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)]는 다양한 형식의 콘텐츠를 표시하는 것을 기본 용도로 하는 많은 컨트롤 형식 및 컨트롤과 유사한 형식을 제공하는 프레젠테이션 플랫폼입니다. 사용할 컨트롤이나 파생시킬 컨트롤을 결정하려면 특정 컨트롤이 가장 잘 표시할 수 있는 개체 유형을 이해해야 합니다.  
  
 이 항목에서는 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 컨트롤 형식 및 컨트롤과 비슷한 형식에 대한 콘텐츠 모델을 요약하여 보여 줍니다. 콘텐츠 모델은 컨트롤에 사용될 수 있는 컨트롤에 대해 설명합니다. 또한 이 항목에서는 각 컨트롤 모델에 대한 콘텐츠 속성을 보여 줍니다. 콘텐츠 속성은 개체의 콘텐츠를 저장하는 데 사용되는 속성입니다.  

<a name="classes_that_contain_arbitrary_content"></a>   
## <a name="classes-that-contain-arbitrary-content"></a>임의의 콘텐츠가 들어 있는 클래스  
 일부 컨트롤 문자열 등 모든 형식의 개체를 포함할 수 있습니다는 <xref:System.DateTime> 개체 또는 <xref:System.Windows.UIElement> 추가 항목에 대 한 컨테이너입니다. 예를 들어, 한 <xref:System.Windows.Controls.Button> 이미지 및 일부 텍스트를 포함할 수 있습니다 또는 <xref:System.Windows.Controls.CheckBox> 의 값을 포함할 수 있습니다 <xref:System.DateTime.Now%2A?displayProperty=nameWithType>합니다.  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]에는 임의의 콘텐츠가 들어 있는 네 개의 클래스가 있습니다. 다음 표에 클래스에서 상속 하는 <xref:System.Windows.Controls.Control>합니다.  
  
|임의의 콘텐츠가 들어 있는 클래스|콘텐츠|  
|-------------------------------------------|-------------|  
|<xref:System.Windows.Controls.ContentControl>|임의의 단일 개체입니다.|  
|<xref:System.Windows.Controls.HeaderedContentControl>|헤더 및 단일 항목이며 둘 모두 임의의 개체입니다.|  
|<xref:System.Windows.Controls.ItemsControl>|임의 개체의 컬렉션입니다.|  
|<xref:System.Windows.Controls.HeaderedItemsControl>|헤더와 항목 컬렉션이며 모두 임의의 개체입니다.|  
  
 이러한 클래스에서 상속하는 컨트롤은 동일한 형식의 콘텐츠를 포함하며 콘텐츠를 동일한 방식으로 처리할 수 있습니다. 다음 그림에서는 일부 텍스트와 이미지를 포함 하는 각 콘텐츠 모델에서 하나의 컨트롤을 보여 줍니다.  
  
 ![각 콘텐츠 모델에서 네 가지 다른 컨트롤을 보여 주는 스크린샷.](./media/wpf-content-model/control-content-model-image-text.png)  
  
### <a name="controls-that-contain-a-single-arbitrary-object"></a>임의의 단일 개체가 들어 있는 컨트롤  
 <xref:System.Windows.Controls.ContentControl> 클래스에는 하나의 임의의 콘텐츠가 포함 되어 있습니다. 해당 콘텐츠 속성은 <xref:System.Windows.Controls.ContentControl.Content%2A>합니다. 다음 컨트롤에서 상속 <xref:System.Windows.Controls.ContentControl> 하며 해당 콘텐츠 모델을 사용 합니다.  
  
- <xref:System.Windows.Controls.Button>  
  
- <xref:System.Windows.Controls.Primitives.ButtonBase>  
  
- <xref:System.Windows.Controls.CheckBox>  
  
- <xref:System.Windows.Controls.ComboBoxItem>  
  
- <xref:System.Windows.Controls.ContentControl>  
  
- <xref:System.Windows.Controls.Frame>  
  
- <xref:System.Windows.Controls.GridViewColumnHeader>  
  
- <xref:System.Windows.Controls.GroupItem>  
  
- <xref:System.Windows.Controls.Label>  
  
- <xref:System.Windows.Controls.ListBoxItem>  
  
- <xref:System.Windows.Controls.ListViewItem>  
  
- <xref:System.Windows.Navigation.NavigationWindow>  
  
- <xref:System.Windows.Controls.RadioButton>  
  
- <xref:System.Windows.Controls.Primitives.RepeatButton>  
  
- <xref:System.Windows.Controls.ScrollViewer>  
  
- <xref:System.Windows.Controls.Primitives.StatusBarItem>  
  
- <xref:System.Windows.Controls.Primitives.ToggleButton>  
  
- <xref:System.Windows.Controls.ToolTip>  
  
- <xref:System.Windows.Controls.UserControl>  
  
- <xref:System.Windows.Window>  
  
 4 다음 그림에 표시 된 단추 <xref:System.Windows.Controls.ContentControl.Content%2A> 문자열로 설정 됩니다는 <xref:System.DateTime> 개체를 <xref:System.Windows.Shapes.Rectangle>, 및 <xref:System.Windows.Controls.Panel> 를 포함 하는 <xref:System.Windows.Shapes.Ellipse> 및 <xref:System.Windows.Controls.TextBlock>:  
  
 ![서로 다른 내용 유형 사용 하 여 네 개의 단추를 보여 주는 스크린샷.](./media/wpf-content-model/control-content-model-buttons.png)  
  
 설정 하는 방법의 예는 <xref:System.Windows.Controls.ContentControl.Content%2A> 속성 참조 <xref:System.Windows.Controls.ContentControl>합니다.  
  
### <a name="controls-that-contain-a-header-and-a-single-arbitrary-object"></a>헤더와 임의의 단일 개체가 들어 있는 컨트롤  
 합니다 <xref:System.Windows.Controls.HeaderedContentControl> 클래스에서 상속 <xref:System.Windows.Controls.ContentControl> 헤더를 사용 하 여 콘텐츠를 표시 합니다. 콘텐츠 속성을 상속 <xref:System.Windows.Controls.ContentControl.Content%2A>에서 <xref:System.Windows.Controls.ContentControl> 정의 합니다 <xref:System.Windows.Controls.HeaderedContentControl.Header%2A> 형식의 속성 <xref:System.Object>하므로 임의의 개체 일 수 있습니다.  
  
 다음 컨트롤에서 상속 <xref:System.Windows.Controls.HeaderedContentControl> 하며 해당 콘텐츠 모델을 사용 합니다.  
  
- <xref:System.Windows.Controls.Expander>  
  
- <xref:System.Windows.Controls.GroupBox>  
  
- <xref:System.Windows.Controls.TabItem>  
  
 다음 그림에서는 두 <xref:System.Windows.Controls.TabItem> 개체입니다. 첫 번째 <xref:System.Windows.Controls.TabItem> 했습니다 <xref:System.Windows.UIElement> 개체로 합니다 <xref:System.Windows.Controls.HeaderedContentControl.Header%2A> 및 <xref:System.Windows.Controls.ContentControl.Content%2A>합니다. <xref:System.Windows.Controls.HeaderedContentControl.Header%2A> 로 설정 되어를 <xref:System.Windows.Controls.StackPanel> 를 포함 하는 <xref:System.Windows.Shapes.Ellipse> 및 <xref:System.Windows.Controls.TextBlock>합니다. <xref:System.Windows.Controls.ContentControl.Content%2A> 로 설정 되어를 <xref:System.Windows.Controls.StackPanel> 를 포함 하는 <xref:System.Windows.Controls.TextBlock> 및 <xref:System.Windows.Controls.Label>. 두 번째 <xref:System.Windows.Controls.TabItem> 문자열에는 <xref:System.Windows.Controls.HeaderedContentControl.Header%2A> 와 <xref:System.Windows.Controls.TextBlock> 에 <xref:System.Windows.Controls.ContentControl.Content%2A>합니다.  
  
 ![헤더 속성에 다른 형식을 사용 하는 TabControl 합니다.](./media/wpf-content-model/control-content-model-tab.png)  
  
 만드는 방법의 예로 <xref:System.Windows.Controls.TabItem> 개체를 참조 하세요. <xref:System.Windows.Controls.HeaderedContentControl>합니다.  
  
### <a name="controls-that-contain-a-collection-of-arbitrary-objects"></a>임의 개체의 컬렉션을 포함하는 컨트롤  
 합니다 <xref:System.Windows.Controls.ItemsControl> 클래스에서 상속 <xref:System.Windows.Controls.Control> 하며 문자열, 개체 또는 다른 요소와 같은 여러 항목을 포함할 수 있습니다. 콘텐츠 속성은 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 고 <xref:System.Windows.Controls.ItemsControl.Items%2A>입니다. <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> 일반적으로 채우는 데 사용 되는 <xref:System.Windows.Controls.ItemsControl> 데이터 컬렉션을 사용 하 여 합니다. 경우 원하지 않는 컬렉션을 채우는 데 사용할 합니다 <xref:System.Windows.Controls.ItemsControl>를 사용 하 여 항목을 추가할 수 있습니다는 <xref:System.Windows.Controls.ItemsControl.Items%2A> 속성입니다.  
  
 다음 컨트롤에서 상속 <xref:System.Windows.Controls.ItemsControl> 하며 해당 콘텐츠 모델을 사용 합니다.  
  
- <xref:System.Windows.Controls.Menu>  
  
- <xref:System.Windows.Controls.Primitives.MenuBase>  
  
- <xref:System.Windows.Controls.ContextMenu>  
  
- <xref:System.Windows.Controls.ComboBox>  
  
- <xref:System.Windows.Controls.ItemsControl>  
  
- <xref:System.Windows.Controls.ListBox>  
  
- <xref:System.Windows.Controls.ListView>  
  
- <xref:System.Windows.Controls.TabControl>  
  
- <xref:System.Windows.Controls.TreeView>  
  
- <xref:System.Windows.Controls.Primitives.Selector>  
  
- <xref:System.Windows.Controls.Primitives.StatusBar>  
  
 다음 그림에 표시 된 <xref:System.Windows.Controls.ListBox> 이러한 유형의 항목을 포함 하는:  
  
- 문자열  
  
- <xref:System.DateTime> 개체입니다.  
  
- <xref:System.Windows.UIElement>  
  
- A <xref:System.Windows.Controls.Panel> 를 포함 하는 <xref:System.Windows.Shapes.Ellipse> 및 <xref:System.Windows.Controls.TextBlock>합니다.  
  
 ![네 형식의 콘텐츠가 있는 ListBox를 보여주는 스크린샷.](./media/wpf-content-model/control-content-model-listbox.png)  
  
### <a name="controls-that-contain-a-header-and-a-collection-of-arbitrary-objects"></a>헤더와 임의 개체의 컬렉션을 포함하는 컨트롤  
 합니다 <xref:System.Windows.Controls.HeaderedItemsControl> 클래스에서 상속 <xref:System.Windows.Controls.ItemsControl> 헤더 문자열, 개체 또는 다른 요소 등의 여러 항목을 포함할 수 있습니다. 상속 된 <xref:System.Windows.Controls.ItemsControl> 콘텐츠 속성을 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A>, 및 <xref:System.Windows.Controls.ItemsControl.Items%2A>, 정의 및는 <xref:System.Windows.Controls.HeaderedItemsControl.Header%2A> 임의의 개체가 될 수 있는 속성.  
  
 다음 컨트롤에서 상속 <xref:System.Windows.Controls.HeaderedItemsControl> 하며 해당 콘텐츠 모델을 사용 합니다.  
  
- <xref:System.Windows.Controls.MenuItem>  
  
- <xref:System.Windows.Controls.ToolBar>  
  
- <xref:System.Windows.Controls.TreeViewItem>  
  
<a name="classes_that_contain_a_collection_of_uielement_objects"></a>   
## <a name="classes-that-contain-a-collection-of-uielement-objects"></a>UIElement 개체 컬렉션을 포함하는 클래스  
 합니다 <xref:System.Windows.Controls.Panel> 클래스를 배치 하 고 자식 정렬 <xref:System.Windows.UIElement> 개체입니다. 해당 콘텐츠 속성은 <xref:System.Windows.Controls.Panel.Children%2A>합니다.  
  
 다음 클래스에서 상속 된 <xref:System.Windows.Controls.Panel> 클래스 및 해당 콘텐츠 모델을 사용 합니다.  
  
- <xref:System.Windows.Controls.Canvas>  
  
- <xref:System.Windows.Controls.DockPanel>  
  
- <xref:System.Windows.Controls.Grid>  
  
- <xref:System.Windows.Controls.Primitives.TabPanel>  
  
- <xref:System.Windows.Controls.Primitives.ToolBarOverflowPanel>  
  
- <xref:System.Windows.Controls.Primitives.ToolBarPanel>  
  
- <xref:System.Windows.Controls.Primitives.UniformGrid>  
  
- <xref:System.Windows.Controls.StackPanel>  
  
- <xref:System.Windows.Controls.VirtualizingPanel>  
  
- <xref:System.Windows.Controls.VirtualizingStackPanel>  
  
- <xref:System.Windows.Controls.WrapPanel>  
  
 자세한 내용은 [패널 개요](panels-overview.md)를 참조하세요.  
  
<a name="classes_that_affects_the_appearance_of_a_uielement"></a>   
## <a name="classes-that-affect-the-appearance-of-a-uielement"></a>UIElement의 모양에 영향을 주는 클래스  
 합니다 <xref:System.Windows.Controls.Decorator> 또는 단일 자식 그 주위에 시각적 효과 적용 하는 클래스 <xref:System.Windows.UIElement>합니다. 해당 콘텐츠 속성은 <xref:System.Windows.Controls.Decorator.Child%2A>합니다. 다음 클래스에서 상속 <xref:System.Windows.Controls.Decorator> 하며 해당 콘텐츠 모델을 사용 합니다.  
  
- <xref:System.Windows.Documents.AdornerDecorator>  
  
- <xref:System.Windows.Controls.Border>  
  
- <xref:System.Windows.Controls.Primitives.BulletDecorator>  
  
- <xref:Microsoft.Windows.Themes.ButtonChrome>  
  
- <xref:Microsoft.Windows.Themes.ClassicBorderDecorator>  
  
- <xref:System.Windows.Controls.InkPresenter>  
  
- <xref:Microsoft.Windows.Themes.ListBoxChrome>  
  
- <xref:Microsoft.Windows.Themes.SystemDropShadowChrome>  
  
- <xref:System.Windows.Controls.Viewbox>  
  
 다음 그림에 표시를 <xref:System.Windows.Controls.TextBox> 있는 (으로 데코 레이트 된)을 <xref:System.Windows.Controls.Border> 묶습니다.  
  
 ![검은색 테두리가 있는 TextBox](./media/layout-border-around-textbox.png "Layout_Border_around_TextBox")  
테두리가 있는 TextBlock  
  
<a name="classes_that_provides_visual_feedback_about_a_uielement"></a>   
## <a name="classes-that-provide-visual-feedback-about-a-uielement"></a>UIElement에 대한 시각적 피드백을 제공하는 클래스  
 <xref:System.Windows.Documents.Adorner> 클래스는 사용자에 게 시각 신호를 제공 합니다. 예를 들어, 사용 하 여는 <xref:System.Windows.Documents.Adorner> 요소에 기능 핸들을 추가 하거나 컨트롤에 대 한 상태 정보를 제공 합니다. <xref:System.Windows.Documents.Adorner> 클래스는 사용자 고유의 표시기 (adorner)를 만들 수 있도록 프레임 워크를 제공 합니다. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]는 구현된 표시기를 제공하지 않습니다. 자세한 내용은 [표시기 개요](adorners-overview.md)를 참조하세요.  
  
<a name="classes_that_enable_users_to_enter_text"></a>   
## <a name="classes-that-enable-users-to-enter-text"></a>사용자가 텍스트를 입력할 수 있는 클래스  
 WPF는 사용자가 텍스트를 입력할 수 있는 세 개의 기본 컨트롤을 제공합니다. 각 컨트롤에는 텍스트가 다르게 표시됩니다. 다음 표에서는 이 세 가지 텍스트 관련 컨트롤과 텍스트를 표시할 때의 기능 및 컨트롤 텍스트를 포함하는 속성을 보여 줍니다.  
  
|컨트롤|텍스트 표시|콘텐츠 속성|  
|-------------|--------------------------|----------------------|  
|<xref:System.Windows.Controls.TextBox>|일반 텍스트|<xref:System.Windows.Controls.TextBox.Text%2A>|  
|<xref:System.Windows.Controls.RichTextBox>|서식 있는 텍스트|<xref:System.Windows.Controls.RichTextBox.Document%2A>|  
|<xref:System.Windows.Controls.PasswordBox>|숨겨진 텍스트(문자가 마스킹됨)|<xref:System.Windows.Controls.PasswordBox.Password%2A>|  
  
<a name="classes_that_display_text"></a>   
## <a name="classes-that-display-your-text"></a>텍스트를 표시하는 클래스  
 여러 클래스를 사용하여 일반 텍스트나 서식이 지정된 텍스트를 표시할 수 있습니다. 사용할 수 있습니다 <xref:System.Windows.Controls.TextBlock> 적은 양의 텍스트를 표시 합니다. 많은 양의 텍스트를 표시 하려는 경우 사용 합니다 <xref:System.Windows.Controls.FlowDocumentReader>, <xref:System.Windows.Controls.FlowDocumentPageViewer>, 또는 <xref:System.Windows.Controls.FlowDocumentScrollViewer> 컨트롤입니다.  
  
 합니다 <xref:System.Windows.Controls.TextBlock> 두 개의 콘텐츠 속성이: <xref:System.Windows.Controls.TextBlock.Text%2A> 및 <xref:System.Windows.Controls.TextBlock.Inlines%2A>합니다. 일관 된 서식을 사용 하는 텍스트를 표시 하려는 경우는 <xref:System.Windows.Controls.TextBlock.Text%2A> 속성 하는 가장 좋은 경우가 많습니다. 텍스트 전체에서 다른 형식을 사용 하려는 경우 사용 된 <xref:System.Windows.Controls.TextBlock.Inlines%2A> 속성입니다. 합니다 <xref:System.Windows.Controls.TextBlock.Inlines%2A> 속성의 컬렉션인 <xref:System.Windows.Documents.Inline> 텍스트 서식을 지정 하는 방법을 지정 하는 개체입니다.  
  
 다음 표에서 콘텐츠 속성을 <xref:System.Windows.Controls.FlowDocumentReader>, <xref:System.Windows.Controls.FlowDocumentPageViewer>, 및 <xref:System.Windows.Controls.FlowDocumentScrollViewer> 클래스입니다.  
  
|컨트롤|콘텐츠 속성|콘텐츠 속성 형식|  
|-------------|----------------------|---------------------------|  
|<xref:System.Windows.Controls.FlowDocumentPageViewer>|문서|<xref:System.Windows.Documents.IDocumentPaginatorSource>|  
|<xref:System.Windows.Controls.FlowDocumentReader>|문서|<xref:System.Windows.Documents.FlowDocument>|  
|<xref:System.Windows.Controls.FlowDocumentScrollViewer>|문서|<xref:System.Windows.Documents.FlowDocument>|  
  
 <xref:System.Windows.Documents.FlowDocument> 구현 합니다 <xref:System.Windows.Documents.IDocumentPaginatorSource> 인터페이스; 따라서 세 클래스 모두 수행할 수는 <xref:System.Windows.Documents.FlowDocument> 콘텐츠로 합니다.  
  
<a name="classes_that_format_text"></a>   
## <a name="classes-that-format-your-text"></a>텍스트 서식을 지정하는 클래스  
 <xref:System.Windows.Documents.TextElement> 및 관련된 클래스를 사용 하면 텍스트 형식을 지정 합니다. <xref:System.Windows.Documents.TextElement> 개체가 포함 되 고 텍스트 서식 지정 <xref:System.Windows.Controls.TextBlock> 고 <xref:System.Windows.Documents.FlowDocument> 개체입니다. 두 가지 기본 유형이 <xref:System.Windows.Documents.TextElement> 개체가 <xref:System.Windows.Documents.Block> 요소 및 <xref:System.Windows.Documents.Inline> 요소입니다. <xref:System.Windows.Documents.Block> 요소는 단락 또는 목록과 같은 텍스트 블록을 나타냅니다. <xref:System.Windows.Documents.Inline> 요소 블록에서 텍스트의 일부를 나타냅니다. 많은 <xref:System.Windows.Documents.Inline> 클래스 적용 되는 텍스트의 서식을 지정 합니다. 각 <xref:System.Windows.Documents.TextElement> 에 자체 콘텐츠 모델이 있습니다. 자세한 내용은 [TextElement 콘텐츠 모델 개요](../advanced/textelement-content-model-overview.md)를 참조하세요.  
  
## <a name="see-also"></a>참고자료

- [고급](../advanced/index.md)
