---
ms.openlocfilehash: e6bb1d53cbe1883b8faef75bd22942bd4f65a5e6
ms.sourcegitcommit: 3ac05b2c386c8cc5e73f4c7665f6c0a7ed3da1bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/20/2019
ms.locfileid: "71181711"
---
### <a name="switchsystemwindowsformsenablevisualstylevalidation-compatibility-switch-not-supported"></a>Switch.System.Windows.Forms.EnableVisualStyleValidation 호환성 스위치가 지원되지 않음

`Switch.System.Windows.Forms.EnableVisualStyleValidation` 호환성 스위치는 .NET Core 3.0의 Windows Forms에서 지원되지 않습니다.

#### <a name="change-description"></a>변경 내용 설명

.NET Framework에서는 애플리케이션이 `Switch.System.Windows.Forms.EnableVisualStyleValidation` 호환성 스위치를 통해 숫자 형태로 제공된 시각적 개체 스타일의 유효성 검사를 옵트아웃할 수 있었습니다. 

.NET Core에서는 `Switch.System.Windows.Forms.EnableVisualStyleValidation` 스위치가 지원되지 않습니다.

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
