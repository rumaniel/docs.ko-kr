---
title: Asynchronous Communication
ms.date: 03/30/2017
ms.assetid: 128dc092-9eb2-4e33-9470-9a7f62b60df6
ms.openlocfilehash: b5cf788ce4587dacb5a7642e25cb1b5b1e6f3e3c
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70044359"
---
# <a name="asynchronous-communication"></a>Asynchronous Communication
이 샘플에서는 두 개의 다른 WF (Windows Workflow Foundation) 서비스 간 통신이 기본적으로 비동기적으로 수행 되는 방법을 보여 줍니다.  
  
## <a name="demonstrates"></a>세부 항목  
 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 서비스 간의 비동기 통신  
  
## <a name="discussion"></a>토론  
 이 샘플에서는 .NET Framework에서 제공되는 메시징 활동을 통해 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 애플리케이션 간의 통신이 비동기적으로 이루어지는 방식을 보여 줍니다.  
  
 이 샘플은 다음 세 개의 프로젝트로 구성되어 있습니다.  
  
 CreditCheckService  
 이 서비스는 특정 개인의 신용 점수나 승인할 품목의 가치를 받은 다음 해당 개인에게 신용을 부여할지 여부를 결정합니다.  
  
 RentalApprovalService  
 이 서비스는 신용 거래를 필요로 하는 개인으로부터 신청을 받습니다. 이 서비스는 `CreditCheckService`와 비동기적으로 통신하여 신용 거래 신청이 유효한지 여부를 결정합니다.  
  
 클라이언트  
 클라이언트는 `RentalApprovalService`와 동기적으로 통신하여 신용 거래가 승인되었는지 여부를 확인합니다.  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. **AsynchronousCommunication** 솔루션을 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다.  
  
2. **공용 속성**에서 **시작 프로젝트**를 선택 하 고 **여러 개의 시작 프로젝트**를 선택 합니다.  
  
3. **RentalApprovalService** 를 목록의 첫 번째 위치로 이동 하 고 그 뒤에 **CreditCheckService**를 오고 **클라이언트**를 이동 합니다. 세 프로젝트 모두에 대해 **시작** 동작을 설정 합니다.  
  
4. **확인**을 클릭 하 고 f5 키를 눌러 샘플을 실행 합니다.  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\Services\AsynchronousCommunication`
