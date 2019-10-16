---
title: '완화: 경로 콜론 검사'
ms.date: 03/30/2017
ms.assetid: a0bb52de-d279-419d-8f23-4b12d1a3f36e
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: a74c25a9bf4dd8b9ab86bd280881fe1a7999e1d5
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70789987"
---
# <a name="mitigation-path-colon-checks"></a>완화: 경로 콜론 검사
.NET Framework 4.6.2를 대상으로 하는 앱부터 이전에 지원되지 않던 경로를 지원하도록 여러 가지 변경이 수행되었습니다(길이 및 형식 측면에서). 특히 적절한 드라이브 구분 기호 구문(콜론)에 대한 확인이 좀 더 정확해졌습니다.  
  
## <a name="impact"></a>영향  
 이러한 변경으로 인해 <xref:System.IO.Path.GetDirectoryName%2A?displayProperty=nameWithType> 및 <xref:System.IO.Path.GetPathRoot%2A?displayProperty=nameWithType> 메서드에서 이전에 지원했던 일부 URI 경로가 차단됩니다.  
  
## <a name="mitigation"></a>완화  
 전에는 허용되었지만 <xref:System.IO.Path.GetDirectoryName%2A?displayProperty=nameWithType> 및 <xref:System.IO.Path.GetPathRoot%2A?displayProperty=nameWithType> 메서드로 더 이상 지원되지 않는 경로 문제를 해결하려면 다음을 수행할 수 있습니다.  
  
- URL에서 스키마를 수동으로 제거합니다. 예를 들어 URL에서 `file://`을 제거합니다.  
  
- URI를 <xref:System.Uri> 생성자에 전달하고 <xref:System.Uri.LocalPath%2A?displayProperty=nameWithType> 속성 값을 검색합니다.  
  
- `Switch.System.IO.UseLegacyPathHandling`<xref:System.AppContext> 스위치를 `true`로 설정하여 새 경로 정규화를 취소합니다.  
  
    ```xml  
    <runtime>  
        <AppContextSwitchOverrides value="Switch.System.IO.UseLegacyPathHandling=true" />    
    </runtime>  
    ```  
  
## <a name="see-also"></a>참고 항목

- [대상 다시 지정 변경 내용](retargeting-changes-in-the-net-framework-4-6-2.md)
