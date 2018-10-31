---
title: 워크플로 보안
ms.date: 03/30/2017
helpviewer_keywords:
- programming [WF], workflow security
ms.assetid: d712a566-f435-44c0-b8c0-49298e84b114
ms.openlocfilehash: 2979f8e50b7fc0d0fab419a89e708517fd271be8
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50199203"
---
# <a name="workflow-security"></a>워크플로 보안
Windows WF (Workflow Foundation)는 Microsoft SQL Server 및 Windows Communication Foundation (WCF)와 같은 몇 가지 다른 기술과 통합 되어 있습니다. 이러한 기술과 잘못 상호 작용하면 워크플로에 보안 문제가 발생할 수 있습니다.

## <a name="persistence-security-concerns"></a>지속성 보안 고려 사항

1.  <xref:System.Activities.Statements.Delay> 활동 및 지속성을 사용하는 워크플로는 서비스로 다시 활성화해야 합니다. Windows AppFabric은 WMS(워크플로 관리 서비스)를 사용하여 만료된 타이머로 워크플로를 다시 활성화합니다. WMS는 <xref:System.ServiceModel.WorkflowServiceHost>를 만들어 다시 활성화된 워크플로를 호스트합니다. WMS 서비스가 중지된 경우 타이머가 만료되면 지속된 워크플로는 다시 활성화되지 않습니다.

2.  지속적인 인스턴스에 대한 액세스는 응용 프로그램 도메인 외부의 악의적인 엔터티로부터 보호되어야 합니다. 또한 지속적인 인스턴스 코드와 같은 응용 프로그램 도메인에서 개발자는 악의적인 코드를 실행할 수 없는지 확인해야 합니다.

3.  지속적인 인스턴스는 높은(관리자) 권한으로 실행해서는 안 됩니다.

4.  응용 프로그램 도메인 외부에서 처리되는 데이터는 보호해야 합니다.

5.  보안 격리가 필요한 응용 프로그램은 스키마 추상화의 같은 인스턴스를 공유해서는 안 됩니다. 이런 응용 프로그램은 다른 저장소 공급자 또는 다른 저장소 인스턴스를 사용하도록 구성된 저장소 공급자를 사용해야 합니다.

## <a name="sql-server-security-concerns"></a>SQL Server 보안 고려 사항

-   많은 수의 자식 활동, 위치, 책갈피, 호스트 확장 또는 범위를 사용하거나 매우 큰 페이로드가 있는 책갈피를 사용할 때는 메모리가 부족하거나 유지 중에 과도한 양의 데이터베이스 공간이 할당될 수 있습니다. 개체 수준 및 데이터베이스 수준 보안을 사용하여 이 문제를 완화할 수 있습니다.

-   <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>를 사용할 때는 인스턴스 저장소를 보호해야 합니다. 자세한 내용은 [SQL Server에 대 한 유용한 정보](https://go.microsoft.com/fwlink/?LinkId=164972)합니다.

-   인스턴스 저장소의 중요 데이터를 암호화해야 합니다. 자세한 내용은 [SQL 보안 암호화](https://go.microsoft.com/fwlink/?LinkId=164976)합니다.

-   데이터베이스 연결 문자열은 종종 구성 파일에 포함되기 때문에 Windows 수준 보안(ACL)을 사용하여 구성 파일(대개 Web.Config)이 안전한지, 로그인과 암호 정보가 연결 문자열에 포함되어 있지 않은지 확인해야 합니다. 대신 데이터베이스와 웹 서버 사이에는 Windows 인증을 사용해야 합니다.

## <a name="considerations-for-workflowservicehost"></a>WorkflowServiceHost에 대한 고려 사항

-   워크플로에서 사용 되는 Windows Communication Foundation (WCF) 끝점을 보호 되어야 합니다. 자세한 내용은 [WCF 보안 개요](https://go.microsoft.com/fwlink/?LinkID=164975)합니다.

-   <xref:System.ServiceModel.ServiceAuthorizationManager>를 사용하여 호스트 수준 권한 부여를 구현할 수 있습니다. 참조 [방법: 서비스에 대 한 사용자 지정 권한 부여 관리자 만들기](https://go.microsoft.com/fwlink/?LinkId=192228) 세부 정보에 대 한 합니다.

-   들어오는 메시지에 대한 ServiceSecurityContext는 OperationContext에 액세스하여 워크플로 내에서도 사용할 수 있습니다.

## <a name="wf-security-pack-ctp"></a>WF Security Pack CTP
 Microsoft WF Security Pack CTP 1은 활동 및 해당 구현에 따라 집합의 첫 번째 community technology preview (CTP) 릴리스 [Windows Workflow Foundation](https://msdn.microsoft.com/netframework/aa663328.aspx)에 [.NET Framework 4](https://msdn.microsoft.com/netframework/default.aspx) (WF 4) 인데 [Windows Identity Foundation (WIF)](https://msdn.microsoft.com/security/aa570351.aspx)합니다.  Microsoft WF Security Pack CTP 1에는 다음과 같은 워크플로를 사용하여 다양한 보안 관련 시나리오를 손쉽게 사용하는 방법을 보여 주는 활동과 디자이너가 모두 포함되어 있습니다.

1.  워크플로에서 클라이언트 ID 가장

2.  PrincipalPermission 및 클레임의 유효성 검사 같은 워크플로 내 인증

3.  사용자 이름/암호 또는 STS(보안 토큰 서비스)에서 검색한 토큰 같은 워크플로에 지정된 ClientCredentials을 사용하여 인증된 메시징

4.  WS-Trust ActAs를 사용하여 클라이언트 보안 토큰이 백엔드 서비스로 이동(클레임 기반 위임)

자세한 내용은 및 WF Security Pack CTP 다운로드를 참조 하세요. [WF Security Pack CTP](https://wf.codeplex.com/releases/view/48114)