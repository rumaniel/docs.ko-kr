---
ms.openlocfilehash: 07527c247e6ccd53d2a77793946ffc796c3e1cbb
ms.sourcegitcommit: 3ac05b2c386c8cc5e73f4c7665f6c0a7ed3da1bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/20/2019
ms.locfileid: "71181725"
---
### <a name="switchsystemwindowsformsuselegacyimages-compatibility-switch-not-supported"></a>Switch.System.Windows.Forms.UseLegacyImages 호환성 스위치가 지원되지 않음

.NET Framework 4.8에서 도입된 `Switch.System.Windows.Forms.UseLegacyImages` 호환성 스위치는 .NET Core 3.0의 Windows Forms에서 지원되지 않습니다.

#### <a name="change-description"></a>변경 내용 설명

.NET Framework 4.8부터는 `Switch.System.Windows.Forms.UseLegacyImages` 호환성 스위치가 높은 DPI 환경의 ClickOnce 시나리오에서 가능한 이미지 크기 조정 문제를 해결했습니다. `true`로 설정하면, 사용자가 이 스위치를 통해 배율이 100%보다 큰 값으로 설정된 높은 DPI 디스플레이에서 레거시 이미지 크기 조정을 복원할 수 있습니다. 자세한 내용은 GitHub에서 [.NET Framework 4.8 릴리스 정보](https://github.com/microsoft/dotnet/blob/master/releases/net48/dotnet48-changes.md#clickonce)를 참조하세요.

.NET Core에서는 `Switch.System.Windows.Forms.UseLegacyImages` 스위치가 지원되지 않습니다.

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
