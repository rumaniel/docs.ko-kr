---
ms.openlocfilehash: 69b25db88c7580787bbb47fb0902b6bb072f8dde
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59235737"
---
### <a name="assemblies-compiled-with-regexcompiletoassembly-breaks-between-40-and-45"></a>Regex.CompileToAssembly로 컴파일된 어셈블리가 4.0과 4.5 사이에서 중단됩니다.

|   |   |
|---|---|
|세부 정보|컴파일된 정규식의 어셈블리가 .NET Framework 4.5로 빌드되었지만 .NET Framework 4를 대상으로 하는 경우, .NET Framework 4가 설치된 시스템에서 해당 어셈블리의 정규식 중 하나를 사용하려고 하면 예외가 throw됩니다.|
|제안 해결 방법|이 문제를 해결하기 위해서는 다음 중 하나를 수행합니다.<ul><li>.NET Framework 4를 사용하여 정규식이 포함된 어셈블리를 빌드합니다.</li><li>해석된 정규식을 사용합니다.</li></ul>|
|범위|부|
|버전|4.5|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Text.RegularExpressions.Regex.CompileToAssembly(System.Text.RegularExpressions.RegexCompilationInfo[],System.Reflection.AssemblyName)?displayProperty=nameWithType></li><li><xref:System.Text.RegularExpressions.Regex.CompileToAssembly(System.Text.RegularExpressions.RegexCompilationInfo[],System.Reflection.AssemblyName,System.Reflection.Emit.CustomAttributeBuilder[])?displayProperty=nameWithType></li><li><xref:System.Text.RegularExpressions.Regex.CompileToAssembly(System.Text.RegularExpressions.RegexCompilationInfo[],System.Reflection.AssemblyName,System.Reflection.Emit.CustomAttributeBuilder[],System.String)?displayProperty=nameWithType></li></ul>|
