---
ms.openlocfilehash: 02a3c1b5a9693535feeab56d9b0f7c9d360749ff
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59804516"
---
### <a name="pageloadcomplete-event-no-longer-causes-systemwebuiwebcontrolsentitydatasource-control-to-invoke-data-binding"></a>Page.LoadComplete 이벤트는 데이터 바인딩을 호출하기 위해 더 이상 System.Web.UI.WebControls.EntityDataSource 컨트롤을 발생시키지 않습니다

|   |   |
|---|---|
|세부 정보|<xref:System.Web.UI.Page.LoadComplete> 이벤트로 인해 더 이상 <xref:System.Web.UI.WebControls.EntityDataSource?displayProperty=name> 컨트롤에서 매개 변수 생성/업데이트/삭제를 위해 변경 내용에 대한 데이터 바인딩을 호출하지 않습니다. 이러한 변경으로 인해 데이터베이스에 대한 불필요한 이동이 제거되고 컨트롤 값이 다시 설정되는 것을 방지하며 <xref:System.Web.UI.WebControls.SqlDataSource?displayProperty=name> 및 <xref:System.Web.UI.WebControls.ObjectDataSource?displayProperty=name> 같은 다른 데이터 컨트롤과 일관된 동작을 발생시킵니다. 이러한 변경으로 인해 드물게 애플리케이션에서 <xref:System.Web.UI.Page.LoadComplete> 이벤트의 데이터 바인딩 호출을 사용하는 경우 다른 동작이 발생합니다.|
|제안 해결 방법|데이터 바인딩이 필요한 경우 앞부분에 다시 게시된 이벤트에서 데이터 바인딩을 수동으로 호출합니다.|
|범위|Microsoft Edge|
|버전|4.5|
|형식|런타임|
