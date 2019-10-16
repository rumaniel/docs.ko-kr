---
title: 단일 단계 커밋 및 승격 가능한 단일 단계 알림을 사용한 최적화
ms.date: 03/30/2017
ms.assetid: 57beaf1a-fb4d-441a-ab1d-bc0c14ce7899
ms.openlocfilehash: f486315b8a8c90e6616ca95fb6be4b2ae3719b7e
ms.sourcegitcommit: 2d792961ed48f235cf413d6031576373c3050918
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/31/2019
ms.locfileid: "70205903"
---
# <a name="optimization-using-single-phase-commit-and-promotable-single-phase-notification"></a>단일 단계 커밋 및 승격 가능한 단일 단계 알림을 사용한 최적화

이 항목에서는 <xref:System.Transactions> 인프라가 제공하는 성능 최적화 메커니즘에 대해 설명합니다.

## <a name="promotable-single-phase-enlistment"></a>승격 가능한 단일 단계 인리스트먼트

<xref:System.Transactions> 인터페이스는 하나 이하의 지속적인 리소스나 여러 개의 일시적인 리소스와 관련된 단일 애플리케이션 도메인 내부의 트랜잭션을 관리합니다. <xref:System.Transactions> 인프라는 애플리케이션 도메인 간 호출만 사용하므로 최상의 처리량과 성능을 제공합니다.

그러나 동일한 컴퓨터에서 다른 애플리케이션 도메인의 다른 개체(프로세스 및 컴퓨터 경계를 넘는 경우 포함)에 트랜잭션을 제공하려는 경우 또는 다른 지속적인 리소스 관리자를 참여시키려는 경우 <xref:System.Transactions> 인프라가 자동으로 MSDTC에서 관리할 트랜잭션을 에스컬레이션합니다. MSDTC에 의해 관리되는 트랜잭션은 <xref:System.Transactions> 인프라에서 관리되는 트랜잭션만큼 성능이 뛰어나지 않습니다.

성능을 최적화하기 위해 <xref:System.Transactions> 인프라는 다른 애플리케이션 도메인, 프로세스 또는 컴퓨터에 있는 하나의 지속적인 원격 리소스가 MSDTC 트랜잭션으로 에스컬레이션되지 않고도 <xref:System.Transactions> 트랜잭션에 참여할 수 있도록 하는 PSPE(승격 가능한 단일 단계 인리스트먼트)를 제공합니다. 이 RM(리소스 관리자)은 트랜잭션을 호스팅하고 "소유"할 수 있으며, 필요한 경우 나중에 해당 트랜잭션을 분산 트랜잭션(또는 MSDTC 트랜잭션)으로 에스컬레이션할 수 있습니다. 이 경우 MSDTC를 사용할 가능성이 줄어듭니다.

이 특정 리소스 관리자에는 일반적으로 분산되지 않은 고유한 내부 트랜잭션이 있으며, 런타임에 해당 트랜잭션을 분산 트랜잭션으로 변환하는 기능을 지원해야 합니다. 예를 들어 SQL Server 2005가 이러한 리소스 관리자입니다. 이 경우 <xref:System.Transactions> 인프라는 에스컬레이션할 필요가 있는지 트랜잭션을 모니터링만 하여 수동적인 관리 역할을 수행합니다. <xref:System.Transactions> 인프라와 리소스 관리자 간의 상호 작용을 지원하려면 리소스 관리자에서 <xref:System.Transactions.IPromotableSinglePhaseNotification> 인터페이스를 구현해야 합니다.

<xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A> 메서드는 나중에 에스컬레이션할 수 있는 하나의 지속적인 리소스를 참여시키는 데 사용됩니다. 이 메서드를 사용하면 필요에 따라 인리스트먼트를 에스컬레이션할 수 있습니다. 인리스트먼트가 성공하면 RM은 내부 트랜잭션을 만들어 <xref:System.Transactions> 트랜잭션과 연결합니다. PSPE 인리스트먼트가 실패하면 대신 RM에서 <xref:System.Transactions.Transaction.EnlistDurable%2A> 메서드를 사용하여 참여시켜야 합니다. 트랜잭션이 이미 분산 트랜잭션인 경우 또는 다른 RM에서 PSPE 인리스트먼트를 수행한 경우 PSPE의 인리스트먼트가 실패할 수도 있습니다.

참여되고 나면 <xref:System.Transactions> 트랜잭션을 커밋하거나 중단하는 클라이언트 호출이 각각 <xref:System.Transactions.IPromotableSinglePhaseNotification.SinglePhaseCommit%2A> 메서드나 <xref:System.Transactions.IPromotableSinglePhaseNotification.Rollback%2A>을 호출하여 리소스 관리자 호출로 변환됩니다.

<xref:System.Transactions> 트랜잭션에 에스컬레이션이 필요하지 않는 경우 트랜잭션을 커밋하면 RM이 <xref:System.Transactions.IPromotableSinglePhaseNotification.SinglePhaseCommit%2A> 알림을 받습니다. 그런 다음 처음에 만들어진 내부 트랜잭션을 커밋할 수 있습니다.

<xref:System.Transactions> 트랜잭션을 워크플로 인스턴스해야 하는 경우(예: 여러 RM을 지원하기 위해) <xref:System.Transactions>는 <xref:System.Transactions.ITransactionPromoter.Promote%2A> 인터페이스가 파생되는 <xref:System.Transactions.ITransactionPromoter> 인터페이스에서 <xref:System.Transactions.IPromotableSinglePhaseNotification> 메서드를 호출하여 리소스 관리자에 알립니다. 그런 다음 리소스 관리자는 로깅이 필요하지 않은 로컬 트랜잭션에서 DTC 트랜잭션에 참여할 수 있는 트랜잭션 개체로 트랜잭션을 내부적으로 변환하고 이미 수행된 작업과 연결합니다. 트랜잭션을 커밋하도록 요청된 경우에도 트랜잭션 관리자는 리소스 관리자에게 <xref:System.Transactions.IPromotableSinglePhaseNotification.SinglePhaseCommit%2A> 알림을 보내며, 리소스 관리자가 에스컬레이션 중에 만든 분산 트랜잭션을 커밋합니다.

> [!NOTE]
> 에스컬레이션 된 트랜잭션에서 커밋이 호출 될 때 생성 되는 **Transactioncommitted** 추적은 DTC 트랜잭션의 작업 ID를 포함 합니다.

관리 에스컬레이션에 대 한 자세한 내용은 [트랜잭션 관리 에스컬레이션](transaction-management-escalation.md)을 참조 하십시오.

## <a name="transaction-management-escalation-scenario"></a>트랜잭션 관리 에스컬레이션 시나리오

다음 시나리오에서는 <xref:System.Data> 네임스페이스를 리소스 관리자의 '프록시'로 사용하여 분산 트랜잭션으로 에스컬레이션하는 과정을 보여 줍니다. 이 시나리오에서는 트랜잭션에 관련된 CN1 데이터베이스에 대한 <xref:System.Data> 연결이 이미 있으며 애플리케이션이 다른 <xref:System.Data> 연결인 CN2를 관련시키려 한다고 가정합니다. 완전히 분산된 2단계 커밋 트랜잭션으로 트랜잭션을 DTC로 에스컬레이션해야 합니다.

이 시나리오에서는 다음 작업이 수행됩니다.

1. CN1이 트랜잭션에 참여할 <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A> 메서드를 호출합니다. 그런 후에도 트랜잭션은 여전히 로컬이며 트랜잭션에 승격 가능한 다른 인리스트먼트가 없으므로 <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A> 호출이 성공합니다.

2. 두 번째 연결인 CN2가 <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A>를 호출할 경우 승격 가능한 다른 인리스트먼트가 관련되어 있으므로 호출이 실패합니다. 이 때문에 CN2는 SQL로 전달하기 위해 DTC 트랜잭션을 가져와야 합니다. 이렇게 하려면 <xref:System.Transactions.TransactionInterop> 클래스가 제공하는 메서드 중 하나를 사용하여 SQL에 제공할 수 있는 트랜잭션 형식을 만듭니다.

3. <xref:System.Transactions>는 CN1이 구현하는 <xref:System.Transactions.ITransactionPromoter.Promote%2A> 인터페이스에서 <xref:System.Transactions.ITransactionPromoter> 메서드를 호출합니다.

4. 이때 CN1은 SQL 2005 및 <xref:System.Data>와 관련된 메커니즘을 사용하여 트랜잭션을 에스컬레이션합니다.

5. <xref:System.Transactions.ITransactionPromoter.Promote%2A> 메서드의 반환 값은 트랜잭션에 대한 전파 토큰을 포함하는 바이트 배열입니다. <xref:System.Transactions>는이 전파 토큰을 사용 하 여 로컬 트랜잭션에 통합할 수 있는 DTC 트랜잭션을 만듭니다.

6. 이때 CN2는 <xref:System.Transactions.TransactionInterop>에 의해 메서드 중 하나를 호출하여 받은 데이터를 사용하여 트랜잭션을 SQL로 전달할 수 있습니다.

7. 이제 둘 다 DTC 분산 트랜잭션에 참여합니다.

## <a name="single-phase-commit-optimization"></a>단일 단계 커밋 최적화

단일 단계 커밋 프로토콜은 모든 업데이트가 명시적 코디네이션 없이 수행되므로 런타임에 보다 효율적입니다. 이 최적화를 활용하려면 리소스에 대해 <xref:System.Transactions.ISinglePhaseNotification> 인터페이스를 사용하는 리소스 관리자를 구현하고 <xref:System.Transactions.Transaction.EnlistDurable%2A> 또는 <xref:System.Transactions.Transaction.EnlistVolatile%2A> 메서드를 사용하여 트랜잭션에 참여해야 합니다. 특히 *EnlistmentOptions* 매개 변수는 단일 단계 커밋이 <xref:System.Transactions.EnlistmentOptions.None> 수행 되도록와 같아야 합니다.

<xref:System.Transactions.ISinglePhaseNotification> 인터페이스는 <xref:System.Transactions.IEnlistmentNotification> 인터페이스에서 파생되므로 RM이 단일 단계 커밋을 수행할 수 없는 경우에도 2단계 커밋 알림을 받을 수 있습니다. RM은 TM에서 <xref:System.Transactions.ISinglePhaseNotification.SinglePhaseCommit%2A> 알림을 받을 경우 커밋하는 데 필요한 작업을 수행하고 <xref:System.Transactions.SinglePhaseEnlistment.Committed%2A> 매개 변수에서 <xref:System.Transactions.SinglePhaseEnlistment.Aborted%2A>, <xref:System.Transactions.SinglePhaseEnlistment.InDoubt%2A> 또는 <xref:System.Transactions.SinglePhaseEnlistment> 메서드를 호출하여 트랜잭션이 커밋 또는 롤백됨을 트랜잭션 관리자에게 적절하게 알려야 합니다. 이 단계에서 인리스트먼트에 대한 <xref:System.Transactions.Enlistment.Done%2A> 응답은 ReadOnly 의미 체계를 나타냅니다. 따라서 다른 모든 메서드와 마찬가지로 <xref:System.Transactions.Enlistment.Done%2A>을 응답하면 안 됩니다.

Volatile 인 리스트 먼 트가 하나 뿐 이며 내구성이 없는 인 리스트 먼 트가 있는 경우에는 volatile 참여가 SPC 알림을 받습니다. 일시적 인 리스트 먼 트와 하나의 지 속성 인 리스트 먼 트만 있으면, volatile 인 리스트 먼 트는 2PC를 수신 합니다. 완료되면 지속적인 인리스트먼트가 SPC를 받습니다.

## <a name="see-also"></a>참고자료

- [리소스를 트랜잭션에 참가 요소로 등록](enlisting-resources-as-participants-in-a-transaction.md)
- [단일 단계 및 다단계 트랜잭션 커밋](committing-a-transaction-in-single-phase-and-multi-phase.md)
