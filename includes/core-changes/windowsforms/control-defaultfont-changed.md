---
ms.openlocfilehash: 843007ac6467584fbe6350b6ea19ef67609d73e2
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71216914"
---
### <a name="controldefaultfont-changed-to-segoe-ui-9pt"></a>`Control.DefaultFont`를 `Segoe UI 9pt`로 변경

#### <a name="change-description"></a>변경 내용 설명

.NET Framework에서는 <xref:System.Windows.Forms.Control.DefaultFont?displayProperty=nameWithType> 속성이 `Microsoft Sans Serif 8pt`로 설정되었습니다. 다음 그림에서는 기본 글꼴을 사용하는 창을 보여 줍니다.

![.NET Framework의 기본 컨트롤 글꼴](~/docs/images/core-changes/windowsforms/control-defaultfont-changed/defaultfont-framework.png)

.NET Core에서는 .Net core 3.0부터 이 글꼴이 `Segoe UI 9pt`로 설정됩니다(<xref:System.Drawing.SystemFonts.MessageBoxFont?displayProperty=nameWithType>와 동일한 글꼴). 이 변경으로 인해 양식 및 컨트롤의 크기가 새 기본 글꼴의 더 큰 크기를 고려하여 약 27% 커집니다. 예:

![.NET Core의 기본 컨트롤 글꼴](~/docs/images/core-changes/windowsforms/control-defaultfont-changed/defaultfont-core.png)

이 변경은 [Windows UX 지침](https://docs.microsoft.com/windows/win32/uxguide/vis-fonts#fonts-and-colors)에 따라 실시된 것입니다.

#### <a name="version-introduced"></a>도입된 버전

3.0

#### <a name="recommended-action"></a>권장 작업

양식 및 컨트롤의 크기가 변경되므로 애플리케이션이 올바르게 렌더링되는지 확인합니다.

원래 글꼴을 유지하려면 양식의 기본 글꼴을 `Microsoft Sans Serif 8pt`로 설정합니다. 예:

```csharp
public MyForm()
{
    InitializeComponent();
    Font = new Font(new FontFamily("Microsoft Sans Serif"), 8f);
}
```

#### <a name="category"></a>범주

- Windows Forms

#### <a name="affected-apis"></a>영향을 받는 API

없음

<!--

### Affected APIs

- Not detectable via API analysis

-->
