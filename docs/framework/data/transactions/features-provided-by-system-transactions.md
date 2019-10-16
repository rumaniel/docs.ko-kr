---
title: System.Transactions에서 제공하는 기능
ms.date: 03/30/2017
ms.assetid: e458cef9-63b5-4401-b448-1536dcd9d9e5
ms.openlocfilehash: c3ef924edf34ae19be9eace85aaee5340025de7d
ms.sourcegitcommit: 2d792961ed48f235cf413d6031576373c3050918
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/31/2019
ms.locfileid: "70205968"
---
# <a name="features-provided-by-systemtransactions"></a>System.Transactions에서 제공하는 기능
이 섹션에서는 <xref:System.Transactions> 네임스페이스에서 제공하는 기능을 사용하여 고유한 트랜잭션 애플리케이션과 리소스 관리자를 작성하는 방법에 대해 설명합니다. 특히 이 섹션에서는 하나 또는 여러 참석자가 있는 트랜잭션(로컬 또는 분산)을 만들고 이에 참여하는 방법에 대해 설명합니다.  
  
## <a name="overview-of-systemtransactions"></a>System.Transactions 개요  
 <xref:System.Transactions> 네임스페이스의 클래스가 제공하는 인프라는 SQL Server, ADO.NET, MSMQ(메시지 큐) 및 MSDTC(Microsoft Distributed Transaction Coordinator)에서 시작된 트랜잭션을 지원하여 트랜잭션 프로그래밍을 단순하고 효율적으로 만듭니다. <xref:System.Transactions> 네임스페이스는 <xref:System.Transactions.Transaction> 클래스 기반의 명시적 프로그래밍 모델과 <xref:System.Transactions.TransactionScope> 클래스를 사용하는 암시적 프로그래밍 모델을 둘 다 제공합니다. 후자의 경우 인프라에서 자동으로 트랜잭션을 관리합니다. 이러한 두 모델을 사용 하 여 트랜잭션 응용 프로그램을 만드는 방법에 대 한 자세한 내용은 [트랜잭션 응용 프로그램 작성](writing-a-transactional-application.md)을 참조 하세요.  
  
 <xref:System.Transactions> 네임스페이스는 리소스 관리자를 구현하는 데 사용할 수 있는 형식도 제공합니다. 리소스 관리자는 트랜잭션에 사용되는 영구적 데이터나 일시적 데이터를 관리하고 트랜잭션 관리자와 함께 작업하여 애플리케이션에 원자성 및 격리를 보장합니다. <xref:System.Transactions> 인프라에서 제공하는 트랜잭션 관리자는 여러 개의 일시적인 리소스나 하나의 지속적인 리소스와 관련된 트랜잭션을 지원합니다. 리소스 관리자를 구현 하는 방법에 대 한 자세한 내용은 [리소스 관리자 구현](implementing-a-resource-manager.md)을 참조 하세요.  
  
 또한 트랜잭션 관리자는 영속적 리소스 관리자가 추가로 트랜잭션에 참여하는 경우 DTC와 같은 디스크 기반 트랜잭션 관리자를 통해 조정하여 로컬 트랜잭션을 분산 트랜잭션으로 투명하게 에스컬레이션합니다. <xref:System.Transactions> 인프라에서 성능을 향상시키는 두 가지 주요 방법은 다음과 같습니다.  
  
- 트랜잭션이 분산된 여러 리소스에 걸쳐 있는 경우 <xref:System.Transactions> 인프라에서 MSDTC만 사용하도록 하는 동적 에스컬레이션. 동적 에스컬레이션에 대한 자세한 내용은 [트랜잭션 관리 에스컬레이션](transaction-management-escalation.md) 항목을 참조 하세요.  
  
- 데이터베이스 등의 리소스가 트랜잭션에 참가한 유일한 엔터티인 경우 트랜잭션을 소유할 수 있게 해 주는 승격 가능한 인리스트먼트입니다. 필요한 경우 나중에 <xref:System.Transactions> 인프라에서 트랜잭션 관리를 MSDTC로 에스컬레이션할 수 있습니다. 이 방법을 사용하면 MSDTC를 사용할 가능성이 더 줄어듭니다. 승격 가능한 참여는[단일 단계 커밋 및 승격 가능한 단일 단계 알림을 사용한 최적화](optimization-spc-and-promotable-spn.md)항목에서 자세히 설명 합니다.  
  
 <xref:System.Transactions> 네임스페이스는 노출하는 리소스 형식에 대한 액세스를 제한하는 세 가지 신뢰 수준인 AllowPartiallyTrustedCallers(APTCA), DistributedTransactionPermission(DTP) 및 완전 신뢰를 정의합니다. 다양 한에 대 한 자세한 내용은 신뢰 수준, 참조 [리소스 액세스의 보안 신뢰 수준](security-trust-levels-in-accessing-resources.md)합니다.  
  
## <a name="in-this-section"></a>단원 내용  
  
### <a name="writing-a-transactional-application"></a>트랜잭션 애플리케이션 작성  
 <xref:System.Transactions> 네임스페이스에서는 트랜잭션 애플리케이션을 만드는 두 가지 모델을 제공합니다. [트랜잭션 범위를 사용 하 여 암시적 트랜잭션 구현](implementing-an-implicit-transaction-using-transaction-scope.md) 에서는 <xref:System.Transactions> 네임 스페이스가 클래스를 <xref:System.Transactions.TransactionScope> 사용 하 여 암시적 트랜잭션 생성을 지 원하는 방법을 설명 합니다.  
  
 [CommittableTransaction를 사용 하 여 명시적 트랜잭션 구현](implementing-an-explicit-transaction-using-committabletransaction.md) 에서는 <xref:System.Transactions> 네임 스페이스가 클래스를 <xref:System.Transactions.CommittableTransaction> 사용 하 여 명시적 트랜잭션을 만드는 방법을 설명 합니다.  
  
 트랜잭션 응용 프로그램 작성에 대 한 추가 항목은 [트랜잭션 응용 프로그램 작성](writing-a-transactional-application.md)을 참조 하세요.  
  
### <a name="implementing-a-resource-manager"></a>리소스 관리자 구현  
 트랜잭션에 참여할 수 있는 리소스 관리자를 구현 하려면 [리소스 관리자 구현](implementing-a-resource-manager.md)을 참조 하세요. 이 섹션에서는 리소스 인리스트먼트, 트랜잭션 커밋, 오류 후 복구 및 최선의 최적화 구현 방법에 대해 설명합니다.
