---
title: 워크플로 서비스 등록 도구(WFServicesReg.exe)
ms.date: 03/30/2017
ms.assetid: 9e92c87b-99c5-4e8d-9d53-7944cc2b47d3
ms.openlocfilehash: 0a9cd5039c085f82f5507c93ebe0855cc620825d
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69916832"
---
# <a name="workflow-service-registration-tool-wfservicesregexe"></a>워크플로 서비스 등록 도구(WFServicesReg.exe)
워크플로 서비스 등록 도구(WFServicesReg.exe)는 Windows WF(Workflow Foundation) 서비스의 구성 요소를 추가, 제거 또는 복구하는 데 사용할 수 있는 독립 실행형 도구입니다.  
  
## <a name="syntax"></a>구문  
  
```  
WFServicesReg.exe [-c | -r | -v | -m | -i]  
```  
  
## <a name="remarks"></a>설명  
 이 도구는 [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)] 설치 위치(특히 %windir%\Microsoft.NET\Framework\v3.5) 또는 %windir%\Microsoft.NET\Framework64\v3.5(64비트 시스템의 경우)에 있습니다.  
  
 다음 표에서는 워크플로 서비스 등록 도구(WFServicesReg.exe)에서 사용할 수 있는 옵션에 대해 설명합니다.  
  
|옵션|Description|  
|------------|-----------------|  
|`/c`|Windows Workflow Services를 구성합니다. 설치 및 복구 시나리오에서 사용됩니다.|  
|`/r`|Windows Workflow Services 구성을 제거합니다.|  
|`/v`|구성 또는 제거에 대한 자세한 정보를 인쇄합니다.|  
|`/m`|MSI 로깅 형식을 사용합니다.|  
|`/i`|애플리케이션이 실행될 때 창을 최소화합니다.|  
  
## <a name="registration"></a>등록  
 이 도구는 Web.config 파일을 검사하고 다음을 등록합니다.  
  
- [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)] 참조 어셈블리  
  
- .xoml 파일의 빌드 공급자  
  
- .xoml 및 .rules 파일의 HTTP 처리기  
  
 이 도구는 Machine.config 파일을 검사하고 다음 확장을 등록합니다.  
  
- behaviorExtensions  
  
- bindingElementExtensions  
  
- bindingExtensions  
  
 또한 다음과 같은 클라이언트 메타데이터 가져오기를 등록합니다.  
  
- policyImporters  
  
- wsdlImporters  
  
 이 도구는 또한 IIS 메타베이스에 .xoml과 .rules 스크립트 맵 및 처리기를 등록합니다.  
  
 [!INCLUDE[ws2003](../../../includes/ws2003-md.md)] 및[!INCLUDE[wxp](../../../includes/wxp-md.md)] 컴퓨터 (iis 5.1 및 iis 6.0)에서 하나의 xoml 및. 규칙 스크립트 집합이 등록 됩니다.  
  
 64비트 시스템에서 도구는 `Enable32BitAppOnWin64` 스위치를 사용할 수 있는 경우 WOW 모드 스크립트 맵을 등록하고, `Enable32BitAppOnWin64` 스위치를 사용할 수 없는 경우 네이티브 64비트 스크립트 맵을 등록합니다.  
  
 [!INCLUDE[wv](../../../includes/wv-md.md)] 및 Windows Server 2008 (IIS 7.0 이상) 컴퓨터에서는 두 개의 xoml 및. rules 처리기 집합이 등록 됩니다. 하나는 통합 모드이 고 하나는 클래식 모드입니다.  
  
 64비트 시스템에서는 `Enable32BitAppOnWin64` 스위치의 상태에 관계없이 처리기 집합 세 개가 등록됩니다. 하나는 통합 모드용, 하나는 WOW 클래식 모드용, 하나는 네이티브 64비트 클래식 모드용입니다.  
  
> [!NOTE]
> ServiceModelreg.exe와 달리 WFServicesReg.exe에서는 특정 웹 사이트에 대한 스크립트 맵이나 처리기를 추가, 제거 또는 복구할 수 없습니다. 이러한 문제의 해결 방법에 대해서는 "스크립트 맵 복구" 단원을 참조하십시오.  
  
## <a name="usage-scenarios"></a>사용 시나리오  
  
### <a name="installing-iis-after-net-framework-35-is-installed"></a>.NET Framework 3.5 설치 후 IIS 설치  
 [!INCLUDE[ws2003](../../../includes/ws2003-md.md)] 시스템에서는 IIS 설치 전에 [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)]가 설치됩니다. IIS를 사용할 수 없으므로 .xoml 및 .rules 스크립트 맵을 설치하지 않아도 [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)]가 설치됩니다.  
  
 IIS가 설치된 후에는 `/c` 스위치와 함께 WFServicesReg.exe 도구를 사용하여 이러한 특정 스크립트 맵을 설치할 수 있습니다.  
  
### <a name="repairing-the-scriptmaps"></a>스크립트 맵 복구  
  
#### <a name="scriptmap-deleted-under-web-sites-node"></a>웹 사이트 노드에서 삭제된 스크립트 맵  
 [!INCLUDE[ws2003](../../../includes/ws2003-md.md)] 시스템에서 .xoml이나 .rules가 웹 사이트 노드에서 실수로 삭제된 경우입니다. 이런 경우 `/c` 스위치와 함께 WFServicesReg.exe 도구를 실행하여 복구할 수 있습니다.  
  
#### <a name="scriptmap-deleted-under-a-particular-web-site"></a>특정 웹 사이트에서 삭제된 스크립트 맵  
 [!INCLUDE[ws2003](../../../includes/ws2003-md.md)] 시스템에서 .xoml이나 .rules가 웹 사이트 노드가 아닌 특정 웹 사이트(예: 기본 웹 사이트)에서 실수로 삭제된 경우입니다.  
  
 특정 웹 사이트에 대 한 삭제 된 처리기를 복구 하려면 "Wfservicesreg.exe/r"을 실행 하 여 모든 웹 사이트에서 처리기를 제거한 다음 "Wfservicesreg.exe/c"를 실행 하 여 모든 웹 사이트에 대 한 적절 한 처리기를 만들어야 합니다.  
  
### <a name="configuring-handlers-after-switching-iis-mode"></a>IIS 모드 전환 후 처리기 구성  
 IIS가 공유 구성 모드에 있는 경우 [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)]를 설치하면 IIS 메타베이스가 공유 위치에 구성됩니다. IIS를 비공유 구성 모드로 전환하면 로컬 메타베이스에 필요한 처리기가 포함되지 않습니다. 로컬 메타 베이스를 제대로 구성 하려면 공유 메타 베이스를 local로 가져오거나 로컬 메타 베이스를 구성 하는 "Wfservicesreg.exe/c"를 실행 하면 됩니다.
