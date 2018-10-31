---
title: 어셈블리 섀도 복사
ms.date: 03/30/2017
helpviewer_keywords:
- assemblies [.NET Framework], shadow copying
- application domains, shadow copying assemblies
- shadow copying assemblies
ms.assetid: de8b8759-fca7-4260-896b-5a4973157672
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 572291fa5674c541136e587bc40818da85f71a65
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2018
ms.locfileid: "50192735"
---
# <a name="shadow-copying-assemblies"></a>어셈블리 섀도 복사
섀도 복사를 사용하면 응용 프로그램 도메인을 언로드하지 않고 응용 프로그램 도메인에서 사용되는 어셈블리를 업데이트할 수 있습니다. 특히 이 기능은 ASP.NET 사이트와 같이 지속적으로 제공되어야 하는 응용 프로그램에 유용합니다.  
  
> [!IMPORTANT]
>  섀도 복사는 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 응용 프로그램에서 지원되지 않습니다.  
  
 어셈블리가 로드될 때 공용 언어 런타임은 어셈블리 파일을 잠그므로 어셈블리가 언로드될 때까지 파일을 업데이트할 수 없습니다. 응용 프로그램 도메인에서 어셈블리를 언로드하는 유일한 방법은 응용 프로그램 도메인을 언로드하는 것이므로 일반적인 환경에서는 어셈블리를 사용 중인 모든 응용 프로그램 도메인이 언로드될 때까지 디스크에서 어셈블리를 업데이트할 수 없습니다.  
  
 섀도 복사 파일에 대한 응용 프로그램 도메인을 구성하면 응용 프로그램 경로의 어셈블리가 다른 위치로 복사되고 해당 위치에서 로드됩니다. 복사본이 잠기지만 원래 어셈블리 파일은 잠금 해제되므로 업데이트할 수 있습니다.  
  
> [!IMPORTANT]
>  섀도 복사될 수 있는 유일한 어셈블리는 응용 프로그램 도메인이 구성될 때 <xref:System.AppDomainSetup.ApplicationBase%2A> 및 <xref:System.AppDomainSetup.PrivateBinPath%2A> 속성으로 지정된 응용 프로그램 디렉터리나 하위 디렉터리에 저장된 어셈블리입니다. 전역 어셈블리 캐시에 저장된 어셈블리는 섀도 복사되지 않습니다.  
  
 이 자료에는 다음과 같은 섹션이 포함되어 있습니다.  
  
-   [섀도 복사 설정 및 사용](#EnablingAndUsing)에서는 섀도 복사에 대해 사용할 수 있는 기본 사용 및 옵션에 대해 설명합니다.  
  
-   [시작 성능](#StartupPerformance)에서는 시작 성능을 개선하려고 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)]에서 섀도 복사에 적용된 변경 내용과 이전 버전의 동작으로 되돌리는 방법을 설명합니다.  
  
-   [사용되지 않는 메서드](#ObsoleteMethods)에서는 [!INCLUDE[dnprdnlong](../../../includes/dnprdnlong-md.md)]에서 섀도 복사를 제어하는 속성 및 메서드의 변경 내용을 설명합니다.  
  
<a name="EnablingAndUsing"></a>   
## <a name="enabling-and-using-shadow-copying"></a>섀도 복사 설정 및 사용  
 다음과 같이 <xref:System.AppDomainSetup> 클래스의 속성을 사용하여 섀도 복사를 사용하도록 응용 프로그램을 구성할 수 있습니다.  
  
-   <xref:System.AppDomainSetup.ShadowCopyFiles%2A> 속성을 `"true"` 문자열 값으로 설정하여 섀도 복사를 사용하도록 설정합니다.  
  
     기본적으로 이렇게 설정하면 응용 프로그램 경로의 모든 어셈블리가 로드되기 전에 다운로드 캐시로 복사됩니다. 이는 다른 컴퓨터에서 다운로드된 파일을 저장하도록 공용 언어 런타임에서 유지 관리되는 것과 같은 캐시이고, 공용 언어 런타임에서는 더 이상 필요하지 않을 때 자동으로 파일을 삭제합니다.  
  
-   선택적으로 <xref:System.AppDomainSetup.CachePath%2A> 속성과 <xref:System.AppDomainSetup.ApplicationName%2A> 속성을 사용하여 섀도 복사된 파일의 사용자 지정 위치를 설정합니다.  
  
     위치의 기본 경로는 <xref:System.AppDomainSetup.ApplicationName%2A> 속성을 <xref:System.AppDomainSetup.CachePath%2A> 속성에 연결하여 하위 디렉터리로 생성됩니다. 어셈블리는 기본 경로 자체가 아니라 이 경로의 하위 디렉터리로 섀도 복사됩니다.  
  
    > [!NOTE]
    >  <xref:System.AppDomainSetup.ApplicationName%2A> 속성이 설정되지 않으면 <xref:System.AppDomainSetup.CachePath%2A> 속성이 무시되고 다운로드 캐시가 사용됩니다. 예외가 throw되지 않습니다.  
  
     사용자 지정 위치를 지정하면 더 이상 필요하지 않은 디렉터리 및 복사된 파일을 정리해야 합니다. 이들 항목은 자동으로 삭제되지 않습니다.  
  
     섀도 복사된 파일의 사용자 지정 위치를 설정해야 하는 할 수 있는 몇 가지 이유가 있습니다. 응용 프로그램에서 많은 복사본을 생성하면 섀도 복사된 파일의 사용자 지정 위치를 설정해야 할 수 있습니다. 다운로드 캐시는 수명이 아니라 크기별로 제한되므로 공용 언어 런타임이 사용 중인 파일을 삭제하려고 시도할 수 있습니다. 사용자 지정 위치를 설정하는 또 다른 이유는 응용 프로그램을 실행하는 사용자가 공용 언어 런타임에서 다운로드 캐시에 사용하는 디렉터리 위치에 대한 쓰기 권한이 없는 경우입니다.  
  
-   선택적으로 <xref:System.AppDomainSetup.ShadowCopyDirectories%2A> 속성을 사용하여 섀도 복사되는 어셈블리를 제한합니다.  
  
     응용 프로그램 도메인에 대해 섀도 복사를 사용하도록 설정하면 기본적으로 응용 프로그램 경로(<xref:System.AppDomainSetup.ApplicationBase%2A> 및 <xref:System.AppDomainSetup.PrivateBinPath%2A> 속성을 통해 지정된 디렉터리)의 모든 어셈블리가 복사됩니다. 섀도 복사할 디렉터리만 포함된 문자열을 만들고 문자열을 <xref:System.AppDomainSetup.ShadowCopyDirectories%2A> 속성에 할당하여 복사를 선택된 디렉터리로 제한할 수 있습니다. 디렉터리는 세미콜론으로 구분합니다. 선택된 디렉터리의 어셈블리만 섀도 복사됩니다.  
  
    > [!NOTE]
    >  <xref:System.AppDomainSetup.ShadowCopyDirectories%2A> 속성에 문자열을 할당하거나 이 속성을 `null`로 설정하면 <xref:System.AppDomainSetup.ApplicationBase%2A> 및 <xref:System.AppDomainSetup.PrivateBinPath%2A> 속성을 통해 지정된 디렉터리의 모든 어셈블리가 섀도 복사됩니다.  
  
    > [!IMPORTANT]
    >  세미콜론은 구분 기호 문자이므로 디렉터리 경로에 세미콜론을 포함하면 안 됩니다. 세미콜론에 대한 이스케이프 문자는 없습니다.  
  
<a name="StartupPerformance"></a>   
## <a name="startup-performance"></a>시작 성능  
 섀도 복사를 사용하는 응용 프로그램 도메인이 시작될 때 응용 프로그램 디렉터리의 어셈블리가 섀도 복사 디렉터리로 복사되거나 이미 해당 위치에 있는지 확인되는 동안 지연이 발생합니다. [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] 이전에는 모든 어셈블리가 임시 디렉터리로 복사되었습니다. 각 어셈블리를 열어 어셈블리 이름을 확인하고 강력한 이름의 유효성을 검사했습니다. 각 어셈블리가 섀도 복사 디렉터리의 복사본보다 더 최근에 업데이트되었는지를 확인했습니다. 그럴 경우 섀도 복사 디렉터리로 복사되었습니다. 마지막으로 임시 복사본이 삭제되었습니다.  
  
 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)]부터 기본 시작 동작은 응용 프로그램 디렉터리에 있는 각 어셈블리의 파일 날짜 및 시간을 섀도 복사 디렉터리에 있는 복사본의 파일 날짜 및 시간과 직접 비교하는 것입니다. 어셈블리가 업데이트되었으면 .NET Framework의 이전 버전에서와 같은 절차를 사용하여 복사되고, 그러지 않으면 섀도 복사 디렉터리의 복사본이 로드됩니다.  
  
 어셈블리가 자주 변경되지 않고 대개 어셈블리의 작은 하위 집합에서 변경이 발생하는 응용 프로그램에 대한 결과 성능 향상이 가장 큽니다. 응용 프로그램의 대부분 어셈블리가 자주 변경되면 새로운 기본 동작 때문에 성능이 저하될 수 있습니다. 이 경우 `enabled="false"`로 [\<shadowCopyVerifyByTimestamp> 요소](../../../docs/framework/configure-apps/file-schema/runtime/shadowcopyverifybytimestamp-element.md)를 구성 파일에 추가하여 이전 버전 .NET Framework의 시작 동작을 되돌릴 수 있습니다.  
  
<a name="ObsoleteMethods"></a>   
## <a name="obsolete-methods"></a>사용되지 않는 메서드  
 <xref:System.AppDomain> 클래스에는 응용 프로그램 도메인에서 섀도 복사를 제어하는 데 사용될 수 있는 <xref:System.AppDomain.SetShadowCopyFiles%2A> 및 <xref:System.AppDomain.ClearShadowCopyPath%2A>와 같은 여러 가지 메서드가 있지만 이들 메서드는 .NET Framework 버전 2.0에서 사용되지 않는 것으로 표시되었습니다. 섀도 복사를 사용하도록 응용 프로그램 도메인을 구성할 경우 <xref:System.AppDomainSetup> 클래스의 속성을 사용하는 것이 좋습니다.  
  
## <a name="see-also"></a>참고 항목  
- <xref:System.AppDomainSetup.ShadowCopyFiles%2A?displayProperty=nameWithType>  
- <xref:System.AppDomainSetup.CachePath%2A?displayProperty=nameWithType>  
- <xref:System.AppDomainSetup.ApplicationName%2A?displayProperty=nameWithType>  
- <xref:System.AppDomainSetup.ShadowCopyDirectories%2A?displayProperty=nameWithType>  
- [\<shadowCopyVerifyByTimestamp> 요소](../../../docs/framework/configure-apps/file-schema/runtime/shadowcopyverifybytimestamp-element.md)
