---
ms.openlocfilehash: 1654d58651bf14b0e7c21de2afa827634b7db858
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59235662"
---
### <a name="systemuri-escaping-now-supports-rfc-3986"></a>이제 System.Uri 이스케이프가 RFC 3986을 지원합니다.

|   |   |
|---|---|
|세부 정보|.NET Framework 4.5에서 URI 이스케이프가 [RFC 3986](https://tools.ietf.org/html/rfc3986)을 지원하도록 변경되었습니다. 특정 변경 내용은 다음을 포함합니다.<ul><li><xref:System.Uri.EscapeDataString(System.String)?displayProperty=name>은 RFC 3986을 기반으로 하는 예약된 문자를 이스케이프합니다.</li><li><xref:System.Uri.EscapeUriString(System.String)?displayProperty=name>은 예약된 문자를 이스케이프하지 않습니다.</li><li><xref:System.Uri.UnescapeDataString(System.String)?displayProperty=name>은 잘못된 이스케이프 시퀀스가 발생하는 경우 예외를 throw하지 않습니다.</li><li>예약되지 않은 이스케이프된 문자는 이스케이프 해제됩니다.</li></ul>|
|제안 해결 방법|<ul><li>잘못된 이스케이프 시퀀스의 경우 throw하여 애플리케이션이 <xref:System.Uri.UnescapeDataString(System.String)?displayProperty=name>을 의존하지 않도록 업데이트합니다. 이제 이러한 시퀀스를 직접 발견해야 합니다.</li><li>마찬가지로, 이스케이프되거나 이스케이프되지 않은 URI 및 데이터 문자열이 .NET Framework 4.0과 .NET Framework 4.5에서 달라질 수 있으며 .NET 버전 간에 직접 비교되지 않아야 합니다. 대신 어떤 비교도 실행되기 전에 단일 .NET 버전에 구문 분석되고 표준화되어야 합니다.</li></ul>|
|범위|부|
|버전|4.5|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Uri.EscapeDataString(System.String)?displayProperty=nameWithType></li><li><xref:System.Uri.EscapeUriString(System.String)?displayProperty=nameWithType></li><li><xref:System.Uri.UnescapeDataString(System.String)?displayProperty=nameWithType></li></ul>|
