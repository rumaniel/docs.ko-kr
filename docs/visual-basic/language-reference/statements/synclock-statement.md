---
title: SyncLock 문 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.SyncLock
- SyncLock
helpviewer_keywords:
- threading [Visual Basic], locks
- SyncLock statement [Visual Basic]
- locks, threads
ms.assetid: 14501703-298f-4d43-b139-c4b6366af176
ms.openlocfilehash: a2bd6ca11072113d8acff78032c19d48c30933c3
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64615122"
---
# <a name="synclock-statement"></a>SyncLock 문
블록을 실행 하기 전에 문 블록에 대 한 배타적 잠금을 획득 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
SyncLock lockobject  
    [ block ]  
End SyncLock  
```  
  
## <a name="parts"></a>요소  
 `lockobject`  
 필수 요소. 개체 참조로 계산 되는 식입니다.  
  
 `block`  
 선택 사항입니다. 잠금을 획득할 때 실행 하는 문 블록입니다.  
  
 `End SyncLock`  
 종료는 `SyncLock` 블록입니다.  
  
## <a name="remarks"></a>설명  
 `SyncLock` 문을 사용 하면 여러 스레드가 동시에 문 블록을 실행 하지 않도록 합니다. `SyncLock` 블록을 입력 하 고 다른 스레드에서 실행 될 때까지 각 스레드를 방지 합니다.  
  
 가장 일반적인 사용 `SyncLock` 둘 이상의 스레드에서 동시에 업데이트할 데이터를 보호 하는 것입니다. 데이터를 조작 하는 문을 중단 없이 완료로 이동 해야 하는 경우 배치 안에 `SyncLock` 블록입니다.  
  
 배타적 잠금으로 보호 된 문 블록이 라고도 함은 *임계*합니다.  
  
## <a name="rules"></a>규칙  
  
- 분기 합니다. 으로 분기할 수 없습니다는 `SyncLock` 블록 외부에서 차단 합니다.  
  
- 잠금 개체 값입니다. 변수의 `lockobject` 일 수 없습니다 `Nothing`합니다. 사용 하기 전에 잠금 개체를 만들어야을 `SyncLock` 문입니다.  
  
     값을 변경할 수 없습니다 `lockobject` 실행 하는 동안는 `SyncLock` 블록입니다. 메커니즘은 잠금 개체 그대로 유지 하는 필요 합니다.  
  
- 사용할 수 없습니다는 [Await](../../../visual-basic/language-reference/operators/await-operator.md) 연산자를 `SyncLock` 블록입니다.  
  
## <a name="behavior"></a>동작  
  
- 메커니즘입니다. 스레드에 도달 하면 합니다 `SyncLock` 평가 문을 `lockobject` 식 식에서 반환 되는 개체에 대 한 배타적 잠금을 가져올 때까지 실행을 일시 중단 합니다. 다른 스레드가 도달 하면 합니다 `SyncLock` 문에서 가져오지 않습니다 잠금을 첫 번째 스레드가 실행 될 때까지 `End SyncLock` 문.  
  
- 보호 된 데이터입니다. 경우 `lockobject` 은 `Shared` 변수는 배타적 잠금을 설정 하면 스레드 클래스의 모든 인스턴스에서 실행 합니다 `SyncLock` 다른 스레드가 실행 되는 동안 차단 합니다. 이 모든 인스턴스 간에 공유 되는 데이터를 보호 합니다.  
  
     경우 `lockobject` 인스턴스 변수는 (되지 `Shared`), 잠금을 방지 실행의 현재 인스턴스에서 실행 하는 스레드는 `SyncLock` 동일한 인스턴스에 있는 다른 스레드와 동시에 블록입니다. 이 개별 인스턴스에 의해 유지 관리 하는 데이터를 보호 합니다.  
  
- 획득 및 해제 합니다. `SyncLock` 블록 처럼를 `Try...Finally` 는 생성 된 `Try` 블록에서 배타적 잠금을 획득 `lockobject` 및 `Finally` 차단 해제 합니다. 이 인해는 `SyncLock` 블록은 블록을 종료 하는 방법에 관계 없이 잠금 해제 합니다. 예외가 처리 되지 않은 경우에 마찬가지입니다.  
  
- 프레임 워크를 호출 합니다. `SyncLock` 블록 획득 하 고 호출 하 여 배타적 잠금이 해제 합니다 `Enter` 및 `Exit` 의 메서드를 `Monitor` 클래스는 <xref:System.Threading> 네임 스페이스입니다.  
  
## <a name="programming-practices"></a>프로그래밍 방법  
 `lockobject` 식은 클래스에 단독으로 속해 있는 개체에 항상 평가 해야 합니다. 선언 해야 합니다는 `Private` 현재 인스턴스에 속한 데이터를 보호 하기 위해 개체 변수 또는 `Private Shared` 모든 인스턴스에 공통 된 데이터를 보호 하기 위해 개체 변수입니다.  
  
 사용 하지 않아야 합니다 `Me` 잠금을 제공 하는 키워드는 예를 들어 개체 데이터입니다. 에 대 한 잠금 개체로 해당 참조를 사용할 수 클래스 외부 코드에 클래스의 인스턴스에 대 한 참조 하는 경우는 `SyncLock` 입장을 완전히 다른 블록 다양 한 데이터를 보호 합니다. 이러한 방식으로 다른 클래스와 클래스 차단할 수 서로 관련 없는 실행 `SyncLock` 블록입니다. 잠그는 경우 문자열에 동일한 문자열을 사용 하는 프로세스의 다른 코드가 같은 잠금을 공유 하므로 문제가 될 수 있습니다.  
  
 사용 하지도 말아야 합니다 `Me.GetType` 공유 데이터에 대 한 잠금 개체를 제공 하는 방법입니다. 왜냐하면 `GetType` 항상 동일한 반환 `Type` 지정된 된 클래스 이름에 대 한 개체입니다. 외부 코드를 호출할 수 `GetType` 클래스에서 사용 하는 동일한 잠금 개체를 가져옵니다. 두 개의 클래스에서 서로 차단 합니다. 따라서 해당 `SyncLock` 블록입니다.  
  
## <a name="examples"></a>예제  
  
### <a name="description"></a>설명  
 다음 예제에서는 메시지의 단순 목록을 유지 관리 하는 클래스를 보여 줍니다. 메시지 배열에 포함 하 고 마지막 변수에 해당 배열의 요소를 사용 합니다. `addAnotherMessage` 프로시저 마지막 요소를 증가 시키고 새 메시지를 저장 합니다. 이러한 두 작업으로 보호 되는 `SyncLock` 및 `End SyncLock` 문을 마지막 요소가 증가 된 후에 다른 스레드가 마지막 요소를 다시 증가 수 전에 새 메시지를 저장 해야 하기 때문에 있습니다.  
  
 경우는 `simpleMessageList` 클래스가 단일 모든 인스턴스에서 해당 변수는 메시지 목록을 공유 `messagesList` 하 고 `messagesLast` 로 선언 됩니다 `Shared`합니다. 이 예에서 변수 `messagesLock` 역시 `Shared`모든 인스턴스에 사용 되는 단일 잠금 개체가 있을 수 있도록 합니다.  
  
### <a name="code"></a>코드  
 [!code-vb[VbVbalrThreading#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrThreading/VB/Class1.vb#1)]  
  
### <a name="description"></a>설명  
 다음 예제에서는 스레드 및 `SyncLock`합니다. 으로 `SyncLock` 문이 있으면 문 블록은 임계 영역이 및 `balance` 음수 되지 됩니다. 주석으로 처리 합니다 `SyncLock` 및 `End SyncLock` 문을 생략의 효과 확인 하려면를 `SyncLock` 키워드입니다.  
  
### <a name="code"></a>코드  
 [!code-vb[VbVbalrThreading#21](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrThreading/VB/class2.vb#21)]  
  
### <a name="comments"></a>설명  
  
## <a name="see-also"></a>참고자료

- <xref:System.Threading.Monitor?displayProperty=nameWithType>
- <xref:System.Threading.Interlocked?displayProperty=nameWithType>
- [동기화 기본 형식 개요](../../../standard/threading/overview-of-synchronization-primitives.md)
