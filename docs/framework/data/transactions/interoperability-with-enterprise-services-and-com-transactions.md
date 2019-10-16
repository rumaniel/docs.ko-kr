---
title: 엔터프라이즈 서비스 및 COM+ 트랜잭션과의 상호 운용성
ms.date: 03/30/2017
ms.assetid: d0fd0d26-fe86-443b-b208-4d57d39fa4aa
ms.openlocfilehash: 98890c4c054a5063f91e429b13cfd6bab9f3dc15
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64596865"
---
# <a name="interoperability-with-enterprise-services-and-com-transactions"></a>엔터프라이즈 서비스 및 COM+ 트랜잭션과의 상호 운용성
<xref:System.Transactions> 네임스페이스는 이 네임스페이스를 사용하여 만든 트랜잭션 개체와 COM+를 통해 만든 트랜잭션 간의 상호 운용성을 지원합니다.  
  
 새 <xref:System.Transactions.EnterpriseServicesInteropOption> 인스턴스를 만들어 COM+와의 상호 운용성 수준을 지정하는 경우 <xref:System.Transactions.TransactionScope> 열거를 사용할 수 있습니다.  
  
 응용 프로그램 코드는 정적 확인할 때 기본적으로 <xref:System.Transactions.Transaction.Current%2A> 속성인 <xref:System.Transactions> 그렇지 않을 경우 현재 트랜잭션에 대 한 찾으려고 또는 <xref:System.Transactions.TransactionScope> 개체를 결정 하는 <xref:System.Transactions.Transaction.Current%2A> 는 **null**. 찾을 수 없으면 <xref:System.Transactions>에서 트랜잭션에 대해 COM+ 컨텍스트를 쿼리합니다. <xref:System.Transactions>는 COM+ 컨텍스트에서 트랜잭션을 찾을 수 있는 경우에도 <xref:System.Transactions>의 기본 트랜잭션을 선호합니다.  
  
## <a name="interoperability-levels"></a>상호 운용성 수준  
 <xref:System.Transactions.EnterpriseServicesInteropOption> 열거는 <xref:System.Transactions.EnterpriseServicesInteropOption.None>, <xref:System.Transactions.EnterpriseServicesInteropOption.Full> 및 <xref:System.Transactions.EnterpriseServicesInteropOption.Automatic>의 상호 운용성 수준을 정의합니다.  
  
 <xref:System.Transactions.TransactionScope> 클래스는 <xref:System.Transactions.EnterpriseServicesInteropOption>을 매개 변수로 받아들이는 생성자를 제공합니다.  
  
 <xref:System.Transactions.EnterpriseServicesInteropOption.None>이름에서 알 수 있듯이 있다는 것을 의미 하지 상호 운용성 간의 <xref:System.EnterpriseServices> 컨텍스트와 트랜잭션 범위입니다. <xref:System.Transactions.TransactionScope>을 사용하여 <xref:System.Transactions.EnterpriseServicesInteropOption.None> 개체를 만든 후 <xref:System.Transactions.Transaction.Current%2A>를 변경하면 COM+ 컨텍스트에 변경 내용이 반영되지 않습니다. 마찬가지로 COM+ 컨텍스트에서 트랜잭션을 변경하면 <xref:System.Transactions.Transaction.Current%2A>에 변경 내용이 반영되지 않습니다. 추가 동기화 작업이 필요하지 않으므로 이는 <xref:System.Transactions>에 대한 가장 빠른 작업 모드입니다. <xref:System.Transactions.EnterpriseServicesInteropOption.None>은 <xref:System.Transactions.TransactionScope>을 매개 변수로 받아들이지 않는 모든 생성자와 관련해서 <xref:System.Transactions.EnterpriseServicesInteropOption>가 사용하는 기본값입니다.  
  
 <xref:System.EnterpriseServices> 트랜잭션을 앰비언트 트랜잭션과 결합하려면 <xref:System.Transactions.EnterpriseServicesInteropOption.Full> 또는 <xref:System.Transactions.EnterpriseServicesInteropOption.Automatic>을 사용해야 합니다. 두 개의 값은 모두 구성 요소가 없는 서비스라는 기능을 사용하므로 사용 시 Windows XP 서비스 팩 2 또는 Windows Server 2003에서 실행해야 합니다.  
  
 <xref:System.Transactions.EnterpriseServicesInteropOption.Full>은 <xref:System.Transactions> 및 <xref:System.EnterpriseServices>에 대한 앰비언트 트랜잭션이 항상 같도록 지정합니다. 그 결과 새 <xref:System.EnterpriseServices> 트랜잭션 컨텍스트를 만들고 <xref:System.Transactions.TransactionScope>에 대한 최신 트랜잭션을 적용하여 해당 컨텍스트의 최신 상태가 되도록 합니다. 이 경우 <xref:System.Transactions.Transaction.Current%2A>의 트랜잭션이 <xref:System.EnterpriseServices.ContextUtil.Transaction%2A>의 트랜잭션과 완전히 동기화됩니다. 이 값을 사용하면 새 COM+ 컨텍스트를 만들어야 할 수 있으므로 성능이 저하됩니다.  
  
 <xref:System.Transactions.EnterpriseServicesInteropOption.Automatic> 다음 요구 사항을 지정합니다.  
  
- <xref:System.Transactions.Transaction.Current%2A>를 선택하면 <xref:System.Transactions>에서 기본 컨텍스트가 아닌 컨텍스트에서 실행 중인 COM+ 컨텍스트의 트랜잭션을 지원해야 합니다. 기본 컨텍스트에는 트랜잭션이 포함될 수 없습니다. 따라서 기본 컨텍스트에서는 <xref:System.Transactions.EnterpriseServicesInteropOption.Automatic>을 사용하는 경우에도 <xref:System.Transactions>에 대해 <xref:System.Transactions.Transaction.Current%2A>가 사용하는 스레드 로컬 스토리지에 저장된 트랜잭션이 반환됩니다.  
  
- 기본 컨텍스트가 아닌 컨텍스트에서 새 <xref:System.Transactions.TransactionScope> 개체를 만드는 경우 <xref:System.Transactions.TransactionScope> 개체에 대한 최신 트랜잭션이 COM+에 반영되어야 합니다. 이 경우 <xref:System.Transactions.EnterpriseServicesInteropOption.Automatic>은 새 COM+ 컨텍스트를 만든다는 점에서 <xref:System.Transactions.EnterpriseServicesInteropOption.Full>처럼 동작합니다.  
  
 또한 <xref:System.Transactions.Transaction.Current%2A>가 <xref:System.Transactions.EnterpriseServicesInteropOption.Full> 및 <xref:System.Transactions.EnterpriseServicesInteropOption.Automatic>에서 모두 설정된 경우 두 모드에서 <xref:System.Transactions.Transaction.Current%2A>를 직접 설정할 수 없음을 의미합니다.  <xref:System.Transactions.Transaction.Current%2A>를 만드는 것 외에 <xref:System.Transactions.TransactionScope>를 직접 설정하려고 하면 <xref:System.InvalidOperationException>이 발생합니다. <xref:System.Transactions.EnterpriseServicesInteropOption> 열거형 값은 사용할 값을 명시적으로 지정하지 않는 새 트랜잭션 범위에 의해 상속됩니다. 예를 들어 <xref:System.Transactions.TransactionScope>을 사용하여 새 <xref:System.Transactions.EnterpriseServicesInteropOption.Full> 개체를 만든 다음 두 번째 <xref:System.Transactions.TransactionScope> 개체를 만드는 경우 <xref:System.Transactions.EnterpriseServicesInteropOption> 값을 지정하지 않으면 두 번째 <xref:System.Transactions.TransactionScope> 개체에도 <xref:System.Transactions.EnterpriseServicesInteropOption.Full>이 설정됩니다.  
  
 요약하면 새 트랜잭션 범위를 만드는 경우 다음 규칙이 적용됩니다.  
  
1. <xref:System.Transactions.Transaction.Current%2A> 확인 트랜잭션이 있는지 확인 합니다. 이 검사로 인해 다음 작업이 수행됩니다.  
  
    - 범위가 있는지 확인하기 위해 검사됩니다.  
  
    - 범위가 있으면 처음에 범위를 만들 때 전달된 <xref:System.Transactions.EnterpriseServicesInteropOption> 열거형 값이 검사됩니다.  
  
    - <xref:System.Transactions.EnterpriseServicesInteropOption> 열거가 <xref:System.Transactions.EnterpriseServicesInteropOption.Automatic>으로 설정된 경우 COM+ 트랜잭션(<xref:System.EnterpriseServices> 트랜잭션)이 관리되는 스레드 로컬 스토리지의 <xref:System.Transactions> 트랜잭션보다 우선합니다.  
  
         값이 <xref:System.Transactions.EnterpriseServicesInteropOption.None>으로 설정된 경우 관리되는 스레드 로컬 스토리지의 <xref:System.Transactions> 트랜잭션이 우선합니다.  
  
         값이 <xref:System.Transactions.EnterpriseServicesInteropOption.Full>로 설정된 경우 COM+ 트랜잭션 하나만 있습니다.  
  
2. <xref:System.Transactions.TransactionScopeOption> 생성자가 전달한 <xref:System.Transactions.TransactionScope> 열거형 값이 검사됩니다. 이 값에 따라 새 트랜잭션을 만들지 여부가 결정됩니다.  
  
3. 새 트랜잭션을 만드는 경우 <xref:System.Transactions.EnterpriseServicesInteropOption>의 값에 따라 다음 작업이 수행됩니다.  
  
    - <xref:System.Transactions.EnterpriseServicesInteropOption.Full>: COM+ 컨텍스트와 연결된 트랜잭션이 만들어집니다.  
  
    - <xref:System.Transactions.EnterpriseServicesInteropOption.None>:는 <xref:System.Transactions> 트랜잭션이 만들어집니다.  
  
    - <xref:System.Transactions.EnterpriseServicesInteropOption.Automatic>: COM+ 컨텍스트가 있는 경우 트랜잭션이 만들어져 컨텍스트에 연결됩니다.  
  
 다음 표에서는 <xref:System.Transactions.EnterpriseServicesInteropOption> 열거를 사용하는 트랜잭션이 필요한 트랜잭션 범위 및 ES(Enterprise Services) 컨텍스트를 보여 줍니다.  
  
|ES 컨텍스트|없음|자동|모든|  
|----------------|----------|---------------|----------|  
|기본 컨텍스트|기본 컨텍스트|기본 컨텍스트|새로 만들기 <br />트랜잭션 컨텍스트|  
|기본값이 아닌 컨텍스트|클라이언트 컨텍스트 유지|새 트랜잭션 컨텍스트 생성|새 트랜잭션 컨텍스트 생성|  
  
 다음 표에서는 <xref:System.EnterpriseServices> 열거형을 사용하는 트랜잭션이 필요한 트랜잭션 범위 및 특정 <xref:System.Transactions.EnterpriseServicesInteropOption> 컨텍스트가 지정된 경우의 앰비언트 트랜잭션을 보여 줍니다.  
  
|ES 컨텍스트|없음|자동|모든|  
|----------------|----------|---------------|----------|  
|기본 컨텍스트|ST|ST|ES|  
|기본값이 아닌 컨텍스트|ST|ES|ES|  
  
 앞의 표에서 각 항목은 다음을 나타냅니다.  
  
- ST는 범위의 앰비언트 트랜잭션이 존재할 수 있는 <xref:System.Transactions> 컨텍스트의 트랜잭션과 구분되는 <xref:System.EnterpriseServices>에 의해 관리됨을 의미합니다.  
  
- ES는 범위의 앰비언트 트랜잭션이 <xref:System.EnterpriseServices> 컨텍스트의 트랜잭션과 같음을 의미합니다.
