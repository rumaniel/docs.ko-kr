---
ms.openlocfilehash: 5bbbf9075683b0f124e126b661b4ab85011e6c2e
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72003002"
---
### <a name="change-of-access-for-accessibleobjectruntimeidfirstitem"></a>AccessibleObject에 대한 액세스 변경

.NET Core 3.0 RC1부터 `AccessibleObject.RuntimeIDFirstItem`의 접근성이 `protected`에서 `internal`로 변경되었습니다.

#### <a name="change-description"></a>변경 내용 설명

.NET Core 3.0 Preview 4부터 `AccessibleObject.RuntimeIDFirstItem` 필드는 `protected`가 되었습니다. .NET Core 3.0 RC1부터 .NET Framework의 필드에 대한 접근성에 맞게 `protected`에서 `internal`로 변경되었습니다.

#### <a name="version-introduced"></a>도입된 버전

3.0 RC1

#### <a name="recommended-action"></a>권장 작업

<xref:System.Windows.Forms.AccessibleObject>에서 파생되는 형식을 사용하여 .NET Core 앱을 개발하고 `RuntimeIDFirstItem` 필드에 액세스하는 경우 변경 내용이 영향을 받을 수 있습니다. 이 경우 로컬 상수를 다음과 같이 정의할 수 있습니다.

```csharp
const int RuntimeIDFirstItem = 0x2a;
```

#### <a name="category"></a>범주

Windows Forms

#### <a name="affected-apis"></a>영향을 받는 API

- API 분석을 통해 검색할 수 없습니다.

<!-- 

### Affected APIs

- Not detectable via API analysis.

-->
