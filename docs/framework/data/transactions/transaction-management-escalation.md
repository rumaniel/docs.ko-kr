---
title: 트랜잭션 관리 에스컬레이션
ms.date: 03/30/2017
ms.assetid: 1e96331e-31b6-4272-bbbd-29ed1e110460
ms.openlocfilehash: d2f027f8a94ee8f0cd23d0f0909ecc9137873bc2
ms.sourcegitcommit: 2d792961ed48f235cf413d6031576373c3050918
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/31/2019
ms.locfileid: "70205849"
---
# <a name="transaction-management-escalation"></a>트랜잭션 관리 에스컬레이션
Windows는 트랜잭션 관리자를 구성하는 서비스 및 모듈 집합을 호스팅합니다. 트랜잭션 관리 에스컬레이션은 트랜잭션 관리자의 구성 요소 중 하나에서 다른 구성 요소로 트랜잭션을 마이그레이션하는 프로세스에 대해 설명합니다.  
  
 <xref:System.Transactions>에는 최대 하나의 내구성이 있는 리소스나 여러 휘발성 리소스를 포함 하는 트랜잭션을 조정 하는 트랜잭션 관리자 구성 요소가 있습니다. 트랜잭션 관리자는 워크플로 인스턴스 간 도메인 호출만 사용하므로 최상의 성능을 제공합니다. 개발자가 직접 트랜잭션 관리자와 상호 작용할 필요는 없습니다. 대신 인터페이스, 일반 동작 및 도우미 클래스를 정의하는 공통 인프라가 <xref:System.Transactions> 네임스페이스에 의해 제공됩니다.  
  
 동일한 컴퓨터에서 다른 응용 프로그램 도메인의 개체 (프로세스 및 컴퓨터 경계를 넘어)에 트랜잭션을 제공 하려는 경우 인프라에서 자동으로 해당 트랜잭션을 <xref:System.Transactions> Microsoft에서 관리할 수 있도록 에스컬레이션 합니다. DTC(Distributed Transaction Coordinator) (MSDTC). 다른 지속적인 리소스 관리자를 참여시키는 경우에도 에스컬레이션이 발생합니다. 에스컬레이션되면 트랜잭션이 완료될 때까지 높은 권한 상태에서 관리됩니다.  
  
 <xref:System.Transactions> 트랜잭션과 MSDTC 트랜잭션 사이에는 PSPE(승격 가능한 단일 단계 인리스트먼트)를 통해 사용할 수 있는 중간 형식의 트랜잭션이 있습니다. PSPE는 성능을 최적화하기 위한 <xref:System.Transactions>의 다른 중요한 메커니즘입니다. PSPE를 사용하면 다른 애플리케이션 도메인, 프로세스 또는 컴퓨터에 있는 지속적인 원격 리소스가 MSDTC 트랜잭션으로 에스컬레이션되지 않고도 <xref:System.Transactions> 트랜잭션에 참여할 수 있습니다. PSPE에 대 한 자세한 내용은 [트랜잭션에 참여자로 리소스 참여](enlisting-resources-as-participants-in-a-transaction.md)를 참조 하세요.  
  
## <a name="how-escalation-is-initiated"></a>에스컬레이션 시작 방법  
 MSDTC는 별도 프로세스에 있고 트랜잭션을 MSDTC로 에스컬레이션하는 경우 메시지가 프로세스 간에 전송되므로 트랜잭션 에스컬레이션을 사용하면 성능이 저하됩니다. 성능을 향상 시키려면 MSDTC로의 에스컬레이션을 연기 하거나 방지 해야 합니다. 따라서 에스컬레이션이 시작 되는 방법 및 시기를 알고 있어야 합니다.  
  
 <xref:System.Transactions> 인프라에서 임시적인 리소스와 단일 단계 알림을 지원하는 하나 이하의 지속적인 리소스를 처리하는 한 트랜잭션은 <xref:System.Transactions> 인프라의 소유로 유지됩니다. 트랜잭션 관리자는 동일한 애플리케이션 도메인에 있고 로깅(트랜잭션 출력을 디스크에 쓰는 작업)이 필요하지 않은 리소스에만 사용할 수 있습니다. <xref:System.Transactions> 인프라가 트랜잭션 소유권을 MSDTC로 넘기게 되는 에스컬레이션은 다음과 같은 경우에 발생합니다.  
  
- 단일 단계 알림을 지원하지 않는 지속적인 리소스가 하나 이상 트랜잭션에 참여하는 경우  
  
- 단일 단계 알림을 지원하는 지속적인 리소스가 두 개 이상 트랜잭션에 참여하는 경우. 예를 들어 SQL Server 2005를 사용 하 여 단일 연결을 등록 하면 트랜잭션이 승격 되지 않습니다. 그러나 데이터베이스를 등록 하는 SQL Server 2005 데이터베이스에 대 한 두 번째 연결을 열 때마다 인프라에서는 <xref:System.Transactions> 해당 데이터베이스가 트랜잭션에서 두 번째 지속형 리소스인 것을 감지 하 여 MSDTC 트랜잭션으로 에스컬레이션 합니다.  
  
- 트랜잭션을 다른 애플리케이션 도메인이나 다른 프로세스로 &quot;마샬링&quot;하는 요청이 호출됩니다. 예를 들어 애플리케이션 도메인 경계를 넘어 트랜잭션 개체가 serialize됩니다. 트랜잭션 개체는 값으로 마샬링되므로 동일한 프로세스인 경우에도 애플리케이션 도메인 경계를 넘어 전달하려고 하면 트랜잭션 개체의 serialization이 발생합니다. <xref:System.Transactions.Transaction>을 매개 변수로 사용하는 원격 메서드를 호출하여 트랜잭션 개체를 전달하거나 트랜잭션에서 처리된 구성 요소에 액세스할 수 있습니다. 이 경우 트랜잭션 개체가 serialize되어 트랜잭션이 애플리케이션 도메인에서 serialize될 때와 마찬가지로 에스컬레이션이 발생합니다. 트랜잭션 개체가 분산되어 로컬 트랜잭션 관리자가 더 이상 적합하지 않습니다.  
  
 다음 표에서는 에스컬레이션 중에 throw될 수 있는 모든 가능한 예외를 보여 줍니다.  
  
|예외 형식|조건|  
|--------------------|---------------|  
|<xref:System.InvalidOperationException>|<xref:System.Transactions.IsolationLevel.Snapshot>과 동일한 격리 수준으로 트랜잭션을 에스컬레이션하려는 경우입니다.|  
|<xref:System.Transactions.TransactionAbortedException>|트랜잭션 관리자가 다운된 경우입니다.|  
|<xref:System.Transactions.TransactionException>|에스컬레이션이 실패하고 애플리케이션이 중단된 경우입니다.|
