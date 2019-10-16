---
title: 트랜잭션 처리
ms.date: 03/30/2017
ms.assetid: effdc8e6-accf-41eb-98a5-431603ba218b
ms.openlocfilehash: de88247e5916ab6e080c4de361efecee0b193e18
ms.sourcegitcommit: 2d792961ed48f235cf413d6031576373c3050918
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/31/2019
ms.locfileid: "70205914"
---
# <a name="transaction-processing"></a>트랜잭션 처리
온라인 서점에서 책을 구입하는 경우 책과 교환하여 신용 지불 형식으로 돈을 지불합니다. 신용이 좋으면 일련의 관련된 작업을 통해 책을 구입할 수 있으며 서점은 돈을 받을 수 있습니다. 그러나 교환 중에 시리즈 중 하나의 작업이 실패하면 전체 교환이 실패합니다. 책을 구입할 수 없고 서점도 돈을 받을 수 없습니다.  
  
 이러한 교환의 균형과 예측 가능성을 유지하는 기술을 트랜잭션 처리라고 합니다. 트랜잭션은 트랜잭션 단위 내의 모든 작업이 성공적으로 완료될 때까지 데이터 지향 리소스가 영구적으로 업데이트되지 않도록 합니다. 관련된 작업 집합을 완전히 성공하거나 완전히 실패하는 하나의 단위로 결합하면 오류 복구를 단순화하고 애플리케이션의 안정성을 높일 수 있습니다.  
  
 트랜잭션 처리 시스템은 업무 수행에 필요한 일상적인 트랜잭션을 수행하는 트랜잭션 지향 애플리케이션을 호스팅하는 컴퓨터 하드웨어 및 소프트웨어로 구성됩니다. 예를 들어 판매 주문 항목, 항공권 예약, 급여, 직원 레코드, 제조 및 운송을 관리하는 시스템이 있습니다.  
  
 이 섹션에서는 트랜잭션 처리에 대한 일반 정보와 Microsoft .NET Framework를 사용하여 트랜잭션 애플리케이션과 리소스 관리자를 작성하는 방법과 관련된 정보를 모두 제공합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [트랜잭션 기본 사항](transaction-fundamentals.md)  
 기본적인 트랜잭션 처리 용어와 개념을 소개합니다.  
  
 [System.Transactions에서 제공하는 기능](features-provided-by-system-transactions.md)  
 System.Transactions의 기능을 사용하여 고유한 트랜잭션 애플리케이션을 작성하는 방법에 대해 설명합니다.  
  
## <a name="reference"></a>참조  
 <xref:System.Transactions>  
 코드가 트랜잭션에 참여할 수 있도록 하는 클래스를 제공합니다. 이 클래스는 분산된 여러 참가자, 여러 단계의 알림 및 지속적인 인리스트먼트가 있는 트랜잭션을 지원합니다.
