---
title: WS-AtomicTransaction 사용
ms.date: 03/30/2017
helpviewer_keywords:
- WS-AT protocol [WCF]
ms.assetid: 04a4c200-0af0-4c5d-a3d9-87cb7339e054
ms.openlocfilehash: e01f5b683bebe1f4cdf282c56aa3049b6da794ee
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64637470"
---
# <a name="using-ws-atomictransaction"></a>WS-AtomicTransaction 사용
WS-AT(WS-AtomicTransaction)는 상호 운용 가능 트랜잭션 프로토콜입니다. 이 프로토콜을 사용하면 웹 서비스 메시지를 통해 분산 트랜잭션 흐름을 만들 수 있고 유형이 다른 트랜잭션 인프라 간에 상호 운용이 가능한 방식으로 이를 조정할 수 있습니다. 그리고 WS-AT에서는 2단계의 커밋 프로토콜을 사용하여 분산 애플리케이션, 트랜잭션 관리자 및 리소스 관리자 간의 원자 단위 결과를 도출합니다.  
  
 Windows Communication Foundation (WCF)를 제공 하는 WS-AT 구현에는 Microsoft Distributed Transaction Coordinator (MSDTC) 트랜잭션 관리자에 내장 된 프로토콜 서비스가 포함 됩니다. WS-AT 사용 하는 WCF 응용 프로그램 타사 기술을 사용 하 여 작성 하는 상호 운용 가능한 웹 서비스를 비롯 한 다른 응용 프로그램에 트랜잭션을 전달할 수 있습니다.  
  
 클라이언트 애플리케이션과 서버 애플리케이션 간에 트랜잭션이 진행될 때, 사용되는 트랜잭션 프로토콜은 클라이언트에서 선택한 엔드포인트에서 서버를 통해 노출된 바인딩에 의해 결정됩니다. 일부 WCF 시스템 제공 바인딩은 기본 지정 하는 `OleTransactions` 다른 기본 WS-AT 지정 하는 동안 트랜잭션 전파 형식으로 프로토콜입니다. 제공된 바인딩 내의 트랜잭션 프로토콜 선택은 프로그래밍 방식으로 수정할 수도 있습니다.  
  
 프로토콜 선택에 따라 다음 사항이 결정됩니다.  
  
- 클라이언트에서 서버로 트랜잭션을 하는 데 사용되는 메시지 헤더의 형식  
  
- 트랜잭션 결과를 확인하기 위해 클라이언트의 트랜잭션 관리자와 서버의 트랜잭션 사이에서 2단계 커밋 프로토콜을 실행하는 데 사용되는 네트워크 프로토콜  
  
 서버와 클라이언트는 WCF를 사용 하 여로 작성 하는 경우 WS-AT 사용할 필요가 없습니다. 대신 활성화된 `NetTcpBinding` 특성을 가진 `TransactionFlow`의 기본 설정을 사용할 수 있습니다. 여기에는 `OleTransactions` 프로토콜이 대신 사용됩니다. 자세한 내용은 [ \<netTcpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/nettcpbinding.md)합니다. 타사 기술을 기반으로 구축한 웹 서비스로 트랜잭션을 이동하는 경우에는 WS-AT를 사용해야 합니다.  
  
## <a name="see-also"></a>참고자료

- [WS-Atomic Transaction 지원 구성](../../../../docs/framework/wcf/feature-details/configuring-ws-atomic-transaction-support.md)
