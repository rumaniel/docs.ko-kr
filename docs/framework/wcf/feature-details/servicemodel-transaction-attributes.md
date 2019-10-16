---
title: ServiceModel 트랜잭션 특성
ms.date: 03/30/2017
helpviewer_keywords:
- transactions [WCF], ServiceModel attributes
ms.assetid: 1e0d2436-6ae5-439b-9765-a448d6f60000
ms.openlocfilehash: d4b7482431404241577111d8dd3841319b65696e
ms.sourcegitcommit: d6e27023aeaffc4b5a3cb4b88685018d6284ada4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67663690"
---
# <a name="servicemodel-transaction-attributes"></a>ServiceModel 트랜잭션 특성

세 가지 표준에 속성을 제공 하는 Windows Communication Foundation (WCF) <xref:System.ServiceModel> WCF 서비스에 대 한 트랜잭션의 동작을 구성할 수 있도록 하는 특성:

- <xref:System.ServiceModel.TransactionFlowAttribute>

- <xref:System.ServiceModel.ServiceBehaviorAttribute>

- <xref:System.ServiceModel.OperationBehaviorAttribute>

## <a name="transactionflowattribute"></a>TransactionFlowAttribute

<xref:System.ServiceModel.TransactionFlowAttribute> 특성은 클라이언트로부터 들어오는 트랜잭션을 허용하도록 서비스 계약에서 작업의 의지를 지정합니다. 특성 속성을 사용 하 여이 컨트롤을 제공합니다. 트랜잭션을 사용 합니다 <xref:System.ServiceModel.TransactionFlowOption> 들어오는 트랜잭션이 인지 여부를 지정 하는 열거형 <xref:System.ServiceModel.TransactionFlowOption.Mandatory>, <xref:System.ServiceModel.TransactionFlowOption.Allowed>, 또는 <xref:System.ServiceModel.TransactionFlowOption.NotAllowed>합니다.

이 특성은 클라이언트와의 외부 상호 작용에 서비스 작업을 연관시키는 유일한 특성입니다. 다음 단원에서 설명할 특성은 작업 실행 내에서의 트랜잭션 사용과 연관된 특성입니다.

## <a name="servicebehaviorattribute"></a>ServiceBehaviorAttribute

<xref:System.ServiceModel.ServiceBehaviorAttribute> 특성은 서비스 계약 구현의 내부 실행 동작을 지정합니다. 이 특성의 트랜잭션별 속성에는 다음이 포함됩니다.

- <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionAutoCompleteOnSessionClose%2A>는 세션이 닫힐 때 완료되지 않은 트랜잭션을 완료할지 여부를 지정합니다. 이 속성의 기본값은 `false`입니다. 이 속성이 `true`이고 들어오는 세션이 네트워크 또는 클라이언트 오류로 인해 닫히지 않고 올바르게 닫힌 경우, 완료되지 않은 모든 트랜잭션이 완료됩니다. 이와는 반대로, 이 속성이 `false`이거나 세션이 올바르게 닫히지 않은 경우에는 세션이 닫힐 때 완료되지 않은 모든 트랜잭션이 롤백됩니다. 이 속성이 `true`인 경우 들어오는 채널은 세션 기반이어야 합니다.

- <xref:System.ServiceModel.ServiceBehaviorAttribute.ReleaseServiceInstanceOnTransactionComplete%2A>은 기본 서비스 인스턴스가 트랜잭션 완료 시 해제되는지 여부를 지정합니다. 이 속성의 기본값은 `true`입니다. 다음 인바운드 메시지는 이전 인스턴스의 트랜잭션별 상태를 무시하면서 새 기본 인스턴스를 만듭니다. 서비스 인스턴스를 릴리스하는 것은 서비스가 수행하는 내부 작업이며, 클라이언트가 설정한 기존 연결 또는 세션에는 영향을 주지 않습니다. 이 기능은 COM+가 제공하는 Just-In-Time 활성화 기능에 해당합니다. 속성이 `true`이면 <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A>는 <xref:System.ServiceModel.ConcurrencyMode.Single>과 같아야 합니다. 그렇지 않으면 서비스는 시작하는 동안 유효하지 않은 구성의 유효성 검사 예외를 throw합니다.

- <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionIsolationLevel%2A>은 서비스 내의 트랜잭션에 사용하도록 격리 수준을 지정합니다. 이 속성은 <xref:System.Transactions.IsolationLevel> 값 중 하나를 사용합니다. 로컬 격리 수준 속성이 <xref:System.Transactions.IsolationLevel.Unspecified>가 아닌 경우 들어오는 트랜잭션의 격리 수준은 이 로컬 속성의 설정과 일치해야 합니다. 그렇지 않으면 들어오는 트랜잭션은 거부되며 오류가 클라이언트로 보내집니다. <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A>가 `true`이고 이동한 트랜잭션이 없을 경우, 이 속성은 로컬로 만들어진 트랜잭션에 사용할 <xref:System.Transactions.IsolationLevel> 값을 결정합니다. <xref:System.Transactions.IsolationLevel>이 <xref:System.Transactions.IsolationLevel.Unspecified>이면 <xref:System.Transactions.IsolationLevel><xref:System.Transactions.IsolationLevel.Serializable>이 사용됩니다.

- <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionTimeout%2A>은 서비스에서 만들어진 새 트랜잭션이 완료되어야 하는 시간을 지정합니다. 이 시간에 도달했는데도 트랜잭션이 완료되지 않으면 트랜잭션이 중단됩니다. <xref:System.TimeSpan>은 <xref:System.Transactions.TransactionScope>가 <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A>로 설정되고 새 트랜잭션이 만들어진 작업에 대한 `true` 시간 제한으로 사용됩니다. 시간 제한은 트랜잭션을 만든 시점으로부터 2단계 커밋 프로토콜의 1단계를 완료할 때까지의 최대 허용 기간입니다. <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionTimeout%2A> 속성과 `transactionTimeout` 구성 설정 사이에서 항상 더 낮은 값이 시간 제한 값으로 사용됩니다.

## <a name="operationbehaviorattribute"></a>OperationBehaviorAttribute

<xref:System.ServiceModel.OperationBehaviorAttribute> 특성은 서비스 구현에서 메서드의 동작을 지정합니다. 이를 사용하여 작업의 특정 실행 동작을 나타낼 수 있습니다. 이 특성의 속성 서비스 계약의 웹 서비스 설명 언어 (WSDL) 설명 하는 데 영향을 주지 않습니다 되며 순수 하 게 요소의 WCF 프로그래밍 모델을 개발자가 직접 구현 해야 하는 일반적인 기능을 사용할 수 있습니다.

이 특성에는 다음과 같은 트랜잭션별 속성이 있습니다.

- <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A>는 활성 트랜잭션 범위 내에서 메서드를 실행해야 할지 여부를 지정합니다. 기본값은 `false`입니다. 메서드에 <xref:System.ServiceModel.OperationBehaviorAttribute> 특성을 설정하지 않으면 메서드가 트랜잭션에서 실행되지 않습니다. 작업에 트랜잭션 범위가 필요하지 않을 경우, 메시지 헤더 내의 모든 트랜잭션은 활성화되지 않고 <xref:System.ServiceModel.OperationContext.IncomingMessageProperties%2A>의 <xref:System.ServiceModel.OperationContext> 요소로 유지됩니다. 작업에 트랜잭션 범위가 필요한 경우 트랜잭션에 대한 소스는 다음 중 하나에서 파생됩니다.

  - 트랜잭션이 클라이언트로부터 이동해 오는 경우, 메서드는 분산된 해당 트랜잭션을 사용하여 만들어진 트랜잭션 범위에서 실행됩니다.

  - 대기 중인 전송과 함께, 메시지를 큐에서 제거하는 데 사용하는 트랜잭션이 사용됩니다. 이 트랜잭션은 메시지의 원래 발신자가 제공한 것이 아니기 때문에 이동된 트랜잭션이 아닙니다.

  - 사용자 지정 전송은 `TransportTransactionProperty`를 사용하여 트랜잭션을 제공할 수 있습니다.

  - 위의 항목 중 트랜잭션에 대한 외부 소스를 제공하는 항목이 없는 경우, 메서드를 호출하기 전에 새 <xref:System.Transactions.Transaction> 인스턴스가 즉시 만들어집니다.

- <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete%2A>는 처리되지 않은 예외가 throw되지 않을 경우 메서드가 실행하는 트랜잭션을 자동으로 완료할지 여부를 지정합니다. 이 속성이 `true`이면 호출 인프라는 사용자 메서드가 예외를 throw하지 않고 반환할 경우 자동으로 트랜잭션을 "완료됨"으로 표시합니다. 이 속성이 `false`이면 트랜잭션이 인스턴스에 연결된 상태에서, 클라이언트가 이 속성이 `true`로 표시된 후속 메서드를 호출할 경우 또는 후속 메서드가 명시적으로 <xref:System.ServiceModel.OperationContext.SetTransactionComplete%2A>를 호출할 경우에만 "완료됨"으로 표시됩니다. 트랜잭션에서 이러한 결과를 수행하는 데 하나라도 실패하면 "완료됨" 상태가 될 수 없으며, <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionAutoCompleteOnSessionClose%2A> 속성을 `true`로 설정하지 않으면 포함된 작업도 커밋되지 않습니다. 이 속성을 `true`로 설정하면 세션과 함께 채널을 사용해야 하며, <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A>를 <xref:System.ServiceModel.InstanceContextMode.PerSession>으로 설정해야 합니다.
