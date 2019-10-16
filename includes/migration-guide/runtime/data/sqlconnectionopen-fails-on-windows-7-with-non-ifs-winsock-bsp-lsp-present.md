---
ms.openlocfilehash: a7f61ad42305377331a7f65fb91d49d709d1b728
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67803235"
---
### <a name="sqlconnectionopen-fails-on-windows-7-with-non-ifs-winsock-bsp-or-lsp-present"></a>비 IFS Winsock BSP 또는 LSP가 있는 Windows 7에서 SqlConnection.Open이 실패합니다.

|   |   |
|---|---|
|세부 정보|비 IFS Winsock BSP 또는 LSP가 있는 Windows 7 컴퓨터에서 실행 중인 .NET Framework 4.5에서 <xref:System.Data.SqlClient.SqlConnection.Open> 및 <xref:System.Data.SqlClient.SqlConnection.OpenAsync(System.Threading.CancellationToken)>가 실패합니다. 비 IFS BSP 또는 LSP가 설치되어 있는지 여부를 확인하려면 <code>netsh WinSock Show Catalog</code> 명령을 사용하고 반환되는 모든 <code>Winsock Catalog Provider Entry</code> 항목을 검사합니다. 서비스 플래그 값이 <code>0x20000</code> 비트 집합을 가진 경우, 공급자는 IFS 핸들을 사용하고 올바르게 작동합니다. <code>0x20000</code> 비트가 지우기인 경우(집합 아님) 비 IFS BSP 또는 LSP입니다.|
|제안|이 버그는 .NET Framework 4.5.2에서 수정되었으므로 .NET Framework를 업그레이드하여 방지할 수 있습니다. 또는 설치된 모든 비 IFS Winsock LSP를 제거하여 방지할 수 있습니다.|
|범위|부|
|버전|4.5|
|형식|런타임|
|영향을 받는 API|<ul><li><xref:System.Data.SqlClient.SqlConnection.Open?displayProperty=nameWithType></li><li><xref:System.Data.SqlClient.SqlConnection.OpenAsync(System.Threading.CancellationToken)?displayProperty=nameWithType></li></ul>|

