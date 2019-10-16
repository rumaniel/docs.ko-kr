---
ms.openlocfilehash: 01bbc49cb0febc5a29dafc7c311b848387a4094a
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67803506"
---
### <a name="add-selectiontextbrush-public-property-to-textboxpasswordbox-non-adorner-selection"></a>TextBox/PasswordBox 비표시기 선택 영역에 SelectionTextBrush 공용 속성 추가

|   |   |
|---|---|
|세부 정보|<xref:System.Windows.Controls.TextBox> 및 <xref:System.Windows.Controls.PasswordBox>에 대해 [비표시기 기반 텍스트 선택](https://github.com/Microsoft/dotnet/blob/master/Documentation/compatibility/wpf-TextBox-PasswordBox-text-selection-does-not-follow-system-colors.md)을 사용하는 WPF 애플리케이션에서 개발자는 이제 새로 추가된 SelectionTextBrush 속성을 설정하여 선택한 텍스트의 렌더링을 변경할 수 있습니다.  기본적으로 이 색은 <xref:System.Windows.SystemColors.HighlightTextBrushKey>와 함께 변경됩니다.  비표시기 기반 텍스트 선택 영역이 활성화되지 않은 경우 이 속성은 아무 작업도 수행하지 않습니다.|
|제안|비표시기 기반 텍스트 선택이 활성화되면 <xref:System.Windows.Controls.PasswordBox.SelectionTextBrush?displayProperty=nameWithType> 및 <xref:System.Windows.Controls.Primitives.TextBoxBase.SelectionTextBrush> 속성을 사용하여 선택한 텍스트의 모양을 변경할 수 있습니다. 이는 XAML을 사용하여 달성할 수 있습니다.<pre><code class="lang-xaml">&lt;TextBox SelectionBrush=&quot;Red&quot; SelectionTextBrush=&quot;White&quot;  SelectionOpacity=&quot;0.5&quot;&#13;&#10;Foreground=&quot;Blue&quot; CaretBrush=&quot;Blue&quot;&gt;&#13;&#10;This is some text.&#13;&#10;&lt;/TextBox&gt;&#13;&#10;</code></pre>|
|범위|주요함|
|버전|4.8|
|Type|대상 변경|
|영향을 받는 API|<ul><li><xref:System.Windows.Controls.Primitives.TextBoxBase.SelectionTextBrushProperty?displayProperty=nameWithType></li><li><xref:System.Windows.Controls.Primitives.TextBoxBase.SelectionTextBrush?displayProperty=nameWithType></li><li>[System.Windows.Controls.TextBox](xref:System.Windows.Controls.TextBox)</li><li>[System.Windows.Controls.PasswordBox](xref:System.Windows.Controls.PasswordBox)</li></ul>|

