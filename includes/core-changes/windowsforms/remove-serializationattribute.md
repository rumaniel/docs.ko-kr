---
ms.openlocfilehash: d48ced9d0201a33f9149aba155ddd3d8bc04c93f
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71216926"
---
### <a name="serializableattribute-removed-from-some-windows-forms-types"></a>일부 Windows Forms 형식에서 SerializableAttribute 제거됨

알려진 이진 serialization 시나리오가 없는 일부 Windows Forms 클래스에서 <xref:System.SerializableAttribute>가 제거되었습니다.

#### <a name="change-description"></a>변경 내용 설명

.NET Framework에서는 다음 형식이 <xref:System.SerializableAttribute>로 데코레이트되지만, .NET Core에서는 이 특성이 제거되었습니다.

- `System.InvariantComparer`
- <xref:System.ComponentModel.Design.ExceptionCollection?displayProperty=nameWithType>
- <xref:System.ComponentModel.Design.Serialization.CodeDomSerializerException?displayProperty=nameWithType>
- `System.ComponentModel.Design.Serialization.CodeDomComponentSerializationService.CodeDomSerializationStore`
- <xref:System.Drawing.Design.ToolboxItem?displayProperty=nameWithType>
- `System.Resources.ResXNullRef`
- `System.Resources.ResXDataNode`
- `System.Resources.ResXFileRef`
- <xref:System.Windows.Forms.Cursor?displayProperty=nameWithType>
- `System.Windows.Forms.NativeMethods.MSOCRINFOSTRUCT`
- `System.Windows.Forms.NativeMethods.MSG`

지금까지 이 serialization 메커니즘의 유지 관리 및 보안과 관련된 우려 사항이 많았습니다. 형식의 `SerializableAttribute`를 유지 관리하려면, 버전 간 serialization 변경 및 잠재적인 프레임워크 간 serialization 변경에 대해 해당 형식을 테스트해야 합니다. 따라서 이러한 형식의 발전이 더 어려워지며, 유지 관리 비용이 많이 들 수 있습니다. 이 형식에는 알려진 이진 serialization 시나리오가 없으므로, 특성 제거로 인한 영향이 최소화됩니다.

자세한 내용은 [이진 Serialization](~/docs/standard/serialization/binary-serialization.md)을 참조하세요.

#### <a name="version-introduced"></a>도입된 버전

3.0 미리 보기 9

#### <a name="recommended-action"></a>권장 작업

이러한 형식이 직렬화 가능으로 표시되어야 하는 코드를 모두 업데이트합니다.

#### <a name="category"></a>범주

Windows Forms

#### <a name="affected-apis"></a>영향을 받는 API

- 없음

<!--

### Affected APIs

- Not detectable via API analysis

-->
