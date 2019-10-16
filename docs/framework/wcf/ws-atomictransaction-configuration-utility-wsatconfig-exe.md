---
title: WS-AtomicTransaction 구성 유틸리티(wsatConfig.exe)
ms.date: 03/30/2017
ms.assetid: 1c56cf98-3963-46d5-a4e1-482deae58c58
ms.openlocfilehash: 6d132abccccdbedf12223af35c314ac949028c19
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69916772"
---
# <a name="ws-atomictransaction-configuration-utility-wsatconfigexe"></a>WS-AtomicTransaction 구성 유틸리티(wsatConfig.exe)
WS-AtomicTransaction 구성 유틸리티는 기본 WS-AtomicTransaction 지원 설정을 구성하는 데 사용됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
wsatConfig [Options]  
```  
  
## <a name="remarks"></a>설명  
 이 명령줄 도구는 로컬 컴퓨터에서만 기본 WS-AT 설정을 구성하는 데 사용할 수 있습니다. 로컬 및 원격 컴퓨터 모두에서 설정을 구성 해야 하는 경우에는 [WS 원자성 트랜잭션 지원 구성](../../../docs/framework/wcf/feature-details/configuring-ws-atomic-transaction-support.md)에 설명 된 대로 MMC 스냅인을 사용 해야 합니다.  
  
 명령줄 도구는 Windows SDK 설치 위치에 있습니다.  
  
 %SystemRoot%\Microsoft.Net\Framework\v3.0\Windows Communication Foundation\wsatConfig.exe  
  
 [!INCLUDE[wxp](../../../includes/wxp-md.md)] 또는 [!INCLUDE[ws2003](../../../includes/ws2003-md.md)]을 실행 중인 경우 WsatConfig.exe를 실행하기 전에 업데이트를 다운로드해야 합니다. 이 업데이트에 대 한 자세한 내용은 [WINDOWS XP COM + 핫픽스 롤업 패키지 13의](https://go.microsoft.com/fwlink/?LinkId=95341) [KB912817 (Commerce Server 2007) 및 가용성에 대 한 업데이트](https://go.microsoft.com/fwlink/?LinkId=95340) 를 참조 하십시오.  
  
 다음 표에서는 WS-AtomicTransaction 구성 유틸리티(wsatConfig.exe)에 사용할 수 있는 옵션을 보여 줍니다.  
  
> [!NOTE]
> 선택한 포트에 대한 SSL 인증서를 설정하는 경우 인증서가 있으면 해당 포트와 연결된 원래 SSL 인증서를 덮어씁니다.  
  
|변수|설명|  
|-------------|-----------------|  
|-계정:\<계정, >|WS-AtomicTransaction에 참여할 수 있는 계정의 쉼표로 구분된 목록을 지정합니다. 이러한 계정의 유효성 검사는 수행되지 않습니다.|  
|-accountsCerts:\<thumb>&#124;"Issuer\SubjectName",>|WS-AtomicTransaction에 참여할 수 있는 인증서의 쉼표로 구분된 목록을 지정합니다. 인증서는 지문이나 Issuer\SubjectName 쌍으로 표시됩니다. 비어 있으면 제목 이름으로 {EMPTY}를 사용하십시오.|  
|-endpointCert:<machine&#124;\<thumb>&#124;"Issuer\SubjectName">|지문 또는 Issuer\SubjectName 쌍으로 지정된 다른 로컬 엔드포인트 인증서 또는 시스템 인증서를 사용합니다. 비어 있으면 제목 이름으로 {EMPTY}를 사용하십시오.|  
|-maxTimeout:\<sec>|최대 제한 시간(초)을 지정합니다. 유효한 값은 0에서 3600 까지입니다.|  
|-network:\<enable&#124;disable>|WS-AtomicTransaction 네트워크 지원을 사용하거나 사용하지 않습니다.|  
|-port:\<portNum>|WS-AtomicTransaction을 위한 HTTPS 포트를 설정합니다.<br /><br /> 이 도구를 실행하기 전에 방화벽을 이미 활성화한 경우 예외 목록에 포트가 자동으로 등록됩니다. 이 도구를 실행하기 전에 방화벽을 비활성화한 경우 방화벽에 대해 추가로 구성되는 사항은 없습니다.<br /><br /> WS-AT를 구성한 후에 방화벽을 활성화하는 경우 이 도구를 다시 실행하고 이 매개 변수를 사용하여 포트 번호를 제공해야 합니다. 구성한 후에 방화벽을 비활성화하는 경우 WS-AT는 추가 입력 없이 계속 작동합니다.|  
|-timeout:\<sec >|기본 제한 시간(초)을 지정합니다. 유효한 값은 1부터 3600까지입니다.|  
|-traceActivity:\<enable&#124;disable>|동작 이벤트의 추적을 사용하거나 사용하지 않습니다.|  
|-traceLevel:\<Off&#124;오류&#124;중요&#124;한&#124;경고&#124; 정보&#124;자세한 정보 표시 모든 >}|추적 수준을 지정합니다.|  
|-tracePII:\<enable&#124;disable>|개인적으로 식별할 수 있는 정보의 추적을 사용하거나 사용하지 않습니다.|  
|-traceProp:\<enable&#124;disable>|전파 이벤트의 추적을 사용하거나 사용하지 않습니다.|  
|-restart|변경 내용을 즉시 활성화하려면 MSDTC를 다시 시작합니다. 이 옵션을 지정하지 않으면 MSDTC를 다시 시작할 때 변경 내용이 적용됩니다.|  
|-show|현재 WS-AtomicTransaction 프로토콜 설정을 표시합니다.|  
|-virtualServer:\<virtualServer>|DTC 리소스 클러스터 이름을 지정합니다.|  
  
## <a name="see-also"></a>참고자료

- [WS-AtomicTransaction 사용](../../../docs/framework/wcf/feature-details/using-ws-atomictransaction.md)
- [WS-Atomic Transaction 지원 구성](../../../docs/framework/wcf/feature-details/configuring-ws-atomic-transaction-support.md)
