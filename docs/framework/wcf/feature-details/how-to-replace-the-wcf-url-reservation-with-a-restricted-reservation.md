---
title: '방법: WCF URL 예약을 제한된 예약으로 바꾸기'
ms.date: 03/30/2017
ms.assetid: 2754d223-79fc-4e2b-a6ce-989889f2abfa
ms.openlocfilehash: 981c4890b11130b937e176da78f378340c0d3894
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991656"
---
# <a name="how-to-replace-the-wcf-url-reservation-with-a-restricted-reservation"></a>방법: WCF URL 예약을 제한된 예약으로 바꾸기
URL 예약을 사용하여 URL 또는 URL 집합에서 메시지를 수신할 수 있는 사용자를 제한할 수 있습니다. 예약은 URL 템플릿, ACL(액세스 제어 목록) 및 플래그 집합으로 이루어집니다. URL 템플릿은 예약이 영향을 미치는 URL을 정의합니다. URL 템플릿을 처리 하는 방법에 대 한 자세한 내용은 [들어오는 요청 라우팅](https://go.microsoft.com/fwlink/?LinkId=136764)을 참조 하세요. ACL은 지정된 URL에서 메시지를 수신하도록 허용할 사용자 또는 사용자 그룹을 제어합니다. 플래그는 예약이 사용자 또는 그룹에게 URL에서 직접 수신 대기할 수 있는 권한을 제공하는지 또는 일부 다른 프로세스에 수신 대기 권한을 위임할 수 있는 권한을 제공하는지를 나타냅니다.  
  
 기본 운영 체제 구성의 일부로 WCF (Windows Communication Foundation)는 포트 80에 대해 전역적으로 액세스할 수 있는 예약을 만들어 모든 사용자가 이중 통신에 이중 HTTP 바인딩을 사용 하는 응용 프로그램을 실행할 수 있도록 합니다. 이 예약의 ACL은 모든 사용자를 위한 것이므로 관리자는 URL 또는 URL 집합에서 수신 대기할 수 있는 권한을 명시적으로 허용하거나 허용하지 않을 수 없습니다. 이 항목에서는 이 예약을 삭제하고 제한된 ACL로 예약을 다시 만드는 방법에 대해 설명합니다.  
  
 [!INCLUDE[wv](../../../../includes/wv-md.md)] 또는 [!INCLUDE[lserver](../../../../includes/lserver-md.md)]에서는 고급 명령 프롬프트에서 `netsh http show urlacl`을 입력하여 모든 HTTP URL 예약을 볼 수 있습니다.  다음 예제에서는 WCF URL 예약이 무엇 인지를 보여 줍니다.  

```
Reserved URL : http://+:80/Temporary_Listen_Addresses/  
        User: \Everyone  
            Listen: Yes  
            Delegate: No  
            SDDL: D:(A;;GX;;;WD)  
```

 예약은 WCF 응용 프로그램에서 이중 통신에 HTTP 이중 바인딩을 사용 하는 경우 사용 되는 URL 템플릿으로 구성 됩니다. 이 형식의 Url은 WCF 서비스에서 HTTP 이중 바인딩을 통해 통신할 때 WCF 클라이언트로 메시지를 다시 보내는 데 사용 됩니다. 모든 사용자가 URL에서 수신 대기할 수 있지만 다른 프로세스에 수신 권한을 위임할 수는 없습니다. 마지막으로 ACL은 SSDL(Security Descriptor Definition Language) 형식으로 지정됩니다. SSDL에 대 한 자세한 내용은 [ssdl](https://go.microsoft.com/fwlink/?LinkId=136789) 을 참조 하십시오.  
  
## <a name="to-delete-the-wcf-url-reservation"></a>WCF URL 예약을 삭제하려면  
  
1. **시작**을 클릭 하 고 **모든 프로그램**을 가리킨 다음 **보조 프로그램**을 클릭 하 고 **명령 프롬프트** 를 마우스 오른쪽 단추로 클릭 하 고 표시 되는 상황에 맞는 메뉴에서 **관리자 권한으로 실행** 을 클릭 합니다. 계속 하려면 사용 권한을 요청할 수 있는 UAC (사용자 계정 컨트롤) 창에서 **계속** 을 클릭 합니다.  
  
2. 명령 프롬프트 창에서 **netsh http delete urlacl http://+:80/Temporary_Listen_Addresses/ url =** 을 입력 합니다.  
  
3. 예약이 삭제되면 다음 메시지가 표시됩니다. **URL 예약이 삭제 되었습니다.**  
  
## <a name="creating-a-new-security-group-and-new-restricted-url-reservation"></a>새 보안 그룹 및 새 제한된 URL 예약 만들기  
 WCF URL 예약을 제한 된 예약으로 바꾸려면 먼저 새 보안 그룹을 만들어야 합니다. 이 작업은 명령 프롬프트 또는 컴퓨터 관리 콘솔에서 수행할 수 있습니다. 한 가지만 수행하면 됩니다.  
  
### <a name="to-create-a-new-security-group-from-a-command-prompt"></a>명령 프롬프트에서 새 보안 그룹을 만들려면  
  
1. **시작**을 클릭 하 고 **모든 프로그램**을 가리킨 다음 **보조 프로그램**을 클릭 하 고 **명령 프롬프트** 를 마우스 오른쪽 단추로 클릭 하 고 표시 되는 상황에 맞는 메뉴에서 **관리자 권한으로 실행** 을 클릭 합니다. 계속 하려면 사용 권한을 요청할 수 있는 UAC (사용자 계정 컨트롤) 창에서 **계속** 을 클릭 합니다.  
  
2. 명령 프롬프트에서 **net localgroup\<"보안 그룹 이름 >"/comment:\<"보안 그룹 설명 >"/add** 를 입력 합니다. **\<보안 그룹 이름 >** 를 만들려는  **\<** 보안 그룹의 이름으로 바꾸고 보안 그룹 설명 > 보안 그룹에 대 한 적절 한 설명으로 바꿉니다.  
  
3. 보안 그룹이 만들어지면 다음 메시지가 표시됩니다. **명령이 성공적으로 완료 되었습니다.**  
  
### <a name="to-create-a-new-security-group-from-the-computer-management-console"></a>컴퓨터 관리 콘솔에서 새 보안 그룹을 만들려면  
  
1. **시작**, **제어판**, **관리 도구**를 차례로 클릭 한 다음 **컴퓨터 관리** 를 클릭 하 여 컴퓨터 관리 콘솔을 엽니다. 계속 하려면 사용 권한을 요청할 수 있는 UAC (사용자 계정 컨트롤) 창에서 **계속** 을 클릭 합니다.  
  
2. **시스템 도구**, **로컬 사용자 및 그룹**을 차례로 클릭 하 고 **그룹** 폴더를 마우스 오른쪽 단추로 클릭 한 다음 나타나는 상황에 맞는 메뉴에서 **새 그룹** 을 클릭 합니다. 원하는 **그룹 이름**, **설명** 및이 새 보안 그룹의 기타 세부 정보를 입력 하 고 **만들기** 단추를 클릭 하 여 보안 그룹을 만듭니다.  
  
### <a name="to-create-the-restricted-url-reservation"></a>제한된 URL 예약을 만들려면  
  
1. **시작**을 클릭 하 고 **모든 프로그램**을 가리킨 다음 **보조 프로그램**을 클릭 하 고 **명령 프롬프트** 를 마우스 오른쪽 단추로 클릭 하 고 표시 되는 상황에 맞는 메뉴에서 **관리자 권한으로 실행** 을 클릭 합니다. 계속 하려면 사용 권한을 요청할 수 있는 UAC (사용자 계정 컨트롤) 창에서 **계속** 을 클릭 합니다.  
  
2. 명령 프롬프트에서 **netsh http add urlacl url http://+:80/Temporary_Listen_Addresses/ = user =\< "machine name\\ > < 보안 그룹\> 이름** 을 입력 합니다. **\<컴퓨터 이름 >** 를 그룹을 만들어야  **\<** 하는 컴퓨터 이름으로 바꾸고 보안 그룹 이름은 이전에 만든 보안 그룹의 이름으로 > 합니다.  
  
3. 예약이 만들어지면 다음 메시지가 표시됩니다. **URL 예약이 성공적으로 추가**되었습니다.
