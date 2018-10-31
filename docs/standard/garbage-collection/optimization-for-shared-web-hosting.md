---
title: 공유 웹 호스팅을 위한 최적화
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- garbage collection, Web hosting
- garbage collection, optimizing
- garbage collection, shared Web hosting
ms.assetid: be98c0ab-7ef8-409f-8a0d-cb6e5b75ff20
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 7831e383a3048523909b79ac5a4706f3c1c48371
ms.sourcegitcommit: ea00c05e0995dae928d48ead99ddab6296097b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48033482"
---
# <a name="optimization-for-shared-web-hosting"></a>공유 웹 호스팅을 위한 최적화
여러 소규모 웹 사이트를 호스트하여 공유되는 서버의 관리자인 경우 .NET 디렉터리의 Aspnet.config 파일에서 `runtime` 노드에 ​​다음 `gcTrimCommitOnLowMemory` 설정을 추가하여 성능을 최적화하고 사이트 용량을 늘릴 수 있습니다.  
  
 `<gcTrimCommitOnLowMemory enabled="true|false"/>`  
  
> [!NOTE]
>  이 설정은 공유 웹 호스팅 시나리오에만 권장됩니다.  
  
 가비지 수집기가 향후 할당을 위해 메모리를 유지하므로 커밋된 공간이 엄밀히 필요한 것보다 클 수 있습니다. 시스템 메모리에 과부하가 발생할 때 충분한 공간을 제공하기 위해 이 공간을 줄일 수 있습니다. 커밋된 이 공간을 줄이면 성능이 향상되고 용량이 확장되어 더 많은 사이트를 호스트할 수 있습니다.  
  
 `gcTrimCommitOnLowMemory` 설정을 사용하면 가비지 수집기가 시스템 메모리 로드를 평가하고 로드가 90%에 도달하는 경우 조정(trimming) 모드로 전환됩니다. 그리고 로드가 85% 미만으로 떨어질 때까지 조정 모드가 유지됩니다.  
  
 조건이 허용되는 경우 가비지 수집기는 `gcTrimCommitOnLowMemory` 설정으로 현재 응용 프로그램을 지원하지 않고 무시하도록 결정할 수 있습니다.  
  
## <a name="example"></a>예  
 다음 XML 조각은 `gcTrimCommitOnLowMemory` 설정을 사용하는 방법을 보여줍니다. 줄임표는 `runtime` 노드에 있는 기타 설정을 나타냅니다.  
  
```xml  
<?xml version="1.0" encoding="UTF-8"?>  
<configuration>  
    <runtime>  
    . . .  
    <gcTrimCommitOnLowMemory enabled="true"/>  
    </runtime>  
    . . .  
</configuration>  
```  
  
## <a name="see-also"></a>참고 항목

- [가비지 수집](../../../docs/standard/garbage-collection/index.md)
