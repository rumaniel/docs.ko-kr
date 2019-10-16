---
ms.openlocfilehash: e2bca42daebd25667ab2f312d5e59089b986503c
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59774447"
---
### <a name="multi-line-aspnet-textbox-spacing-changed-when-using-antixssencoder"></a>AntiXSSEncoder를 사용할 때 여러 줄 ASP.Net TextBox 간격이 변경됨

|   |   |
|---|---|
|세부 정보|.NET Framework 4.0에서 <xref:System.Web.Security.AntiXss.AntiXssEncoder?displayProperty=name>을 사용하는 경우 추가 줄은 포스트백에서 여러 줄 텍스트 상자의 줄 사이에 삽입되었습니다. .NET Framework 4.5에서는 웹 응용 프로그램이 .NET Framework 4.5를 대상으로 하는 경우를 제외하고 이러한 추가 줄 바꿈이 포함되지 않습니다.|
|제안 해결 방법|.NET Framework 4.5로 대상이 다시 지정된 4.0 웹 응용 프로그램에는 더 이상 추가 줄 바꿈을 삽입하지 않도록 개선된 여러 줄 텍스트 상자가 있을 수 있습니다. 이것이 필요 없는 경우 응용 프로그램은 .NET Framework 4.0을 대상으로 하여 .NET Framework 4.5에서 실행하는 경우 이전 동작을 할 수 있습니다.|
|범위|부|
|버전|4.5|
|형식|대상 변경|
