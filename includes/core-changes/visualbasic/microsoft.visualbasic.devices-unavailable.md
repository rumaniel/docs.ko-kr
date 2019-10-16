---
ms.openlocfilehash: dae4afa92b8833f326b4eacd00b36bb3e1199cc1
ms.sourcegitcommit: dfd612ba454ce775a766bcc6fe93bc1d43dfda47
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2019
ms.locfileid: "72237409"
---
### <a name="types-in-microsoftvisualbasicdevices-namespace-not-available"></a>Microsoft.VisualBasic.Devices 네임스페이스의 형식을 사용할 수 없음

<xref:Microsoft.VisualBasic.Devices?displayProperty=fullName> 네임스페이스의 형식을 사용할 수 없습니다.

#### <a name="version-introduced"></a>도입된 버전

.NET Core 3.0 미리 보기 8

#### <a name="change-description"></a>변경 내용 설명

일부 .NET Core 3.0 미리 보기 릴리스에서는 <xref:Microsoft.VisualBasic.Devices?displayProperty=fullName> 네임스페이스의 형식을 사용할 수 있었습니다. .NET Core 3.0 미리 보기 9부터는 해당 형식을 더 이상 사용할 수 없습니다.

후속 릴리스에서 불필요한 어셈블리 종속성이나 호환성이 손상되는 변경을 방지하기 위해 형식을 제거했습니다.
 
#### <a name="recommended-action"></a>권장 작업

코드에서 <xref:Microsoft.VisualBasic.Devices> 형식과 해당 멤버를 사용해야 하는 경우, .NET 클래스 라이브러리의 해당 형식이나 멤버를 사용할 수 있습니다. 예를 들어 <xref:Microsoft.VisualBasic.Devices.Clock?displayProperty=nameWithType> 클래스와 동등한 기능은 <xref:System.DateTime?displayProperty=nameWithType> 및 <xref:System.Environment?displayProperty=nameWithType> 형식에서 제공되고, <xref:Microsoft.VisualBasic.Devices.Ports?displayProperty=nameWithType> 클래스와 동등한 기능은 <xref:System.IO.Ports?displayProperty=nameWithType> 네임스페이스의 형식에서 제공됩니다.

#### <a name="category"></a>범주

Visual Basic

#### <a name="affected-apis"></a>영향을 받는 API

- <xref:Microsoft.VisualBasic.Devices?displayProperty=fullName>

<!--

### Affected APIs

- `N:Microsoft.VisualBasic.Devices`

-- >

