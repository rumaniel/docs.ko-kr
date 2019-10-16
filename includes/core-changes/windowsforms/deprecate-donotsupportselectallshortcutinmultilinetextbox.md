---
ms.openlocfilehash: a9d0fe3516ade04bc38b804268a9d989f6891d80
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/23/2019
ms.locfileid: "71181857"
---
### <a name="switchsystemwindowsformsdonotsupportselectallshortcutinmultilinetextbox-compatibility-switch-not-supported"></a>Switch.System.Windows.Forms.DoNotSupportSelectAllShortcutInMultilineTextBox 호환성 스위치가 지원되지 않음

.NET Framework 4.6.1에서 도입된 `Switch.System.Windows.Forms.DoNotSupportSelectAllShortcutInMultilineTextBox` 호환성 스위치는 .NET Core 3.0의 Windows Forms에서 지원되지 않습니다.

#### <a name="change-description"></a>변경 내용 설명

.NET Framework 4.6.1부터 <xref:System.Windows.Forms.TextBox> 컨트롤에서 <kbd>Ctrl</kbd> + <kbd>A</kbd> 바로 가기 키를 선택하면 모든 텍스트가 선택되었습니다. .NET Framework 4.6 및 이전 버전에서는 [Textbox.ShortcutsEnabled](xref:System.Windows.Forms.TextBoxBase.ShortcutsEnabled) 및 <xref:System.Windows.Forms.TextBox.Multiline?displayProperty=nameWithType> 속성이 모두 `true`로 설정된 경우, <kbd>Ctrl</kbd> + <kbd>A</kbd> 바로 가기 키를 선택해도 모든 텍스트가 선택되지 않았습니다. `Switch.System.Windows.Forms.DoNotSupportSelectAllShortcutInMultilineTextBox` 호환성 스위치는 원래 동작을 유지하기 위해 .NET Framework 4.6.1에서 도입되었습니다. 자세한 내용은 <xref:System.Windows.Forms.TextBox.ProcessCmdKey%2A?displayProperty=nameWithType>를 참조하세요.

.NET Core에서는 `Switch.System.Windows.Forms.DoNotSupportSelectAllShortcutInMultilineTextBox` 스위치가 지원되지 않습니다.

#### <a name="version-introduced"></a>도입된 버전

3.0 미리 보기 9

#### <a name="recommended-action"></a>권장 작업

스위치를 제거합니다. 이 스위치는 지원되지 않으며, 사용 가능한 대체 기능이 없습니다.

#### <a name="category"></a>범주

Windows Forms

#### <a name="affected-apis"></a>영향을 받는 API

- 없음

<!-- 

### Affected APIs

- Not detectable via API analysis

-->
