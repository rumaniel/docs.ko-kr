---
ms.openlocfilehash: 6c2c6422ca4d426fcc2ff5827a2387abb5578e3d
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59234836"
---
### <a name="systemuri-parsing-adheres-to-rfc-3987"></a>System.Uri 구문 분석이 RFC 3987을 준수

|   |   |
|---|---|
|세부 정보|.NET Framework 4.5에서 URI 구문 분석은 여러 방법으로 변경되었습니다. 단, 이러한 변경 내용은 .NET Framework 4.5를 대상으로 하는 코드에 영향을 줍니다. 이진 파일이 .NET Framework 4.0을 대상으로 하는 경우, 이전 동작이 관찰됩니다. .NET Framework 4.5의 URI 구문 분석 변경 내용은 다음을 포함합니다.<ul><li>URI 구문 분석은 RFC 3987의 최신 IRI 규칙에 따라 정규화 및 문자 검사를 수행합니다.</li><li>유니코드 정규화 형식 C는 URI의 호스트 부분에서만 수행됩니다.</li><li>잘못된 mailto: URI가 예외를 발생시킵니다.</li><li>이제 패스 세그먼트 끝의 후행 점이 유지됩니다.</li><li><code>file://</code> URI는 <code>?</code> 문자를 이스케이프하지 않습니다.</li><li>유니코드 제어 문자 <code>U+0080</code>에서 <code>U+009F</code>는 지원되지 않습니다.</li><li>쉼표 문자 <code>,</code> 또는 <code>%2c</code>는 자동으로 이스케이프가 해제되지 않습니다.</li></ul>|
|제안 해결 방법|이전 .NET Framework 4.0 URI 구문 분석 의미 체계가 필요한 경우(주로 필요하지 않음) .NET Framework 4.0을 대상으로 하여 사용할 수 있습니다. 이것은 어셈블리에서 <xref:System.Runtime.Versioning.TargetFrameworkAttribute?displayProperty=name>를 사용하거나 '프로젝트 속성' 페이지에서 Visual Studio의 프로젝트 시스템 UI를 통해 수행할 수 있습니다.|
|범위|주요함|
|버전|4.5|
|형식|대상 변경|
|영향을 받는 API|<ul><li><xref:System.Uri.%23ctor(System.String)?displayProperty=nameWithType></li><li><xref:System.Uri.%23ctor(System.String,System.Boolean)?displayProperty=nameWithType></li><li><xref:System.Uri.%23ctor(System.String,System.UriKind)?displayProperty=nameWithType></li><li><xref:System.Uri.%23ctor(System.Uri,System.String)?displayProperty=nameWithType></li><li><xref:System.Uri.TryCreate(System.String,System.UriKind,System.Uri@)?displayProperty=nameWithType></li><li><xref:System.Uri.TryCreate(System.Uri,System.String,System.Uri@)?displayProperty=nameWithType></li><li><xref:System.Uri.TryCreate(System.Uri,System.Uri,System.Uri@)?displayProperty=nameWithType></li></ul>|
