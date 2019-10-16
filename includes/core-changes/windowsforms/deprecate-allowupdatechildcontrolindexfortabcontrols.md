---
ms.openlocfilehash: 1d01de4b978309e05a6036953f2a6909628a2480
ms.sourcegitcommit: 3ac05b2c386c8cc5e73f4c7665f6c0a7ed3da1bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/20/2019
ms.locfileid: "71181807"
---
### <a name="switchsystemwindowsformsallowupdatechildcontrolindexfortabcontrols-compatibility-switch-not-supported"></a>Switch.System.Windows.Forms.AllowUpdateChildControlIndexForTabControls 호환성 스위치가 지원되지 않음

`Switch.System.Windows.Forms.AllowUpdateChildControlIndexForTabControls` 호환성 스위치는 .NET Framework 4.6 이상 버전의 Windows Forms에서 지원되지만, .NET Core 3.0부터 Windows Forms에서 지원되지 않습니다.

#### <a name="change-description"></a>변경 내용 설명

.NET Framework 4.6 이상 버전에서 탭을 선택하면 해당 컨트롤 컬렉션이 다시 정렬됩니다. 이 동작을 사용하지 않으려는 경우, `Switch.System.Windows.Forms.AllowUpdateChildControlIndexForTabControls` 호환성 스위치를 통해 애플리케이션에서 다시 정렬을 건너뛸 수 있습니다.

.NET Core에서는 `Switch.System.Windows.Forms.AllowUpdateChildControlIndexForTabControls` 스위치가 지원되지 않습니다.

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
