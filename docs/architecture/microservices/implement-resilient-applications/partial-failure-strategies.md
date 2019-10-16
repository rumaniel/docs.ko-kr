---
title: 부분 실패 처리 전략
description: 부분 실패를 정상적으로 처리하기 위한 여러 전략을 알아봅니다.
ms.date: 10/16/2018
ms.openlocfilehash: e96fe99ab44b924460e01abaad30aa3e2432117a
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68674510"
---
# <a name="strategies-to-handle-partial-failure"></a>부분 실패 처리 전략

부분 실패 처리 전략은 다음을 포함합니다.

**내부 마이크로 서비스 전체에 걸친 비동기 통신(예를 들어, 메시지 기반 통신) 사용**. 잘못된 디자인은 결국 잘못된 중단의 결정적 원인이 되기 때문에 내부 마이크로 서비스 전역에 걸쳐 동기 HTTP 호출의 긴 체인을 만들지 않는 것이 바람직합니다. 반대로, 클라이언트 애플리케이션과 첫 번째 수준의 마이크로 서비스 또는 세분화된 API 게이트웨이 간의 프런트 엔드 통신을 제외하고 내부 마이크로 서비스 전역에 걸쳐 초기 요청/응답 주기를 넘어서 비동기(메시지 기반) 통신만 한 번 사용하는 것이 좋습니다. 결과적 일관성 및 이벤트 기반 아키텍처는 파급 효과를 최소화하는 데 도움이 됩니다. 이런 접근법은 높은 수준의 마이크로 서비스 자율성을 시행하고 따라서 여기서 지적된 문제를 예방할 수 있습니다.

**지수 백오프를 사용하여 다시 시도 사용**. 이 기법은 해당 서비스가 단기간만 사용할 수 없을 경우 호출 다시 시도를 여러 번 수행함으로써 단기간의 일시적인 오류를 막는 데 도움이 됩니다. 이런 현상은 마이크로 서비스/컨테이너를 클러스터의 다른 노드로 이동할 경우 또는 일시적인 네트워크 문제로 인해 발생할 수 있습니다. 그러나 이러한 재시도가 회로 차단기를 사용해 적절히 계획되지 않은 경우 그 파급 효과는 악화되고 결국 [서비스 거부(DoS)](https://en.wikipedia.org/wiki/Denial-of-service_attack)를 초래할 수 있습니다.

**네트워크 시간 제한의 해결 방법**. 일반적으로 클라이언트는 응답을 기다릴 때 항상 시간 제한을 사용하되 무기한 차단하지 않도록 설계되어야 합니다. 시간 제한의 사용은 리소스가 절대 무기한으로 묶여 있지 않게 합니다.

**회로 차단기 패턴 사용**. 이 방법에서 클라이언트 프로세스는 실패한 요청 횟수를 추적합니다. 오류율이 설정된 제한을 초과하는 경우 “회로 차단기”가 작동해 더 이상의 시도는 즉시 실패합니다. (많은 요청이 실패 하는 경우 서비스가 사용할 수 없게 되고 요청 전송이 무의미하다는 것을 의미합니다.) 제한 시간 경과 후 해당 클라이언트는 다시 시도해야 하며 새 요청이 성공하는 경우 회로 차단기를 닫습니다.

**대체 제공**. 이 방법에서 클라이언트 프로세스는 캐시된 데이터 또는 기본값 반환처럼 요청이 실패한 경우 대체 논리를 수행 합니다. 이 방법은 쿼리에 적합하며 업데이트나 명령에 관해서는 더욱 복잡합니다.

**큐에 대기 중인 요청 수 제한**. 클라이언트는 클라이언트 마이크로 서비스가 특정 서비스에 보낼 수 있는 대기 중인 요청 수에 대한 상한값을 입력해야 합니다. 제한치에 도달한 경우 추가 요청을 하는 것은 무의미하며 이런 시도는 즉각 실패합니다. 구현 관점에서 Polly [Bulkhead 격리](https://github.com/App-vNext/Polly/wiki/Bulkhead) 정책은 이 요구 사항을 충족하는 데 사용할 수 있습니다. 이 방법은 기본적으로 <xref:System.Threading.SemaphoreSlim>을 구현으로 사용하는 병렬화 제한입니다. 또한 Bulkhead 외부에 "큐"를 허용합니다. 실행 전에도 과부하를 미리 줄일 수 있습니다(예를 들어, 용량이 가득찼다고 여겨지기 때문에). 이렇게 하면 특정 오류 시나리오에 대한 응답이 회로 차단기보다 더 빠르게 됩니다. 회로 차단기는 오류를 대기하기 때문입니다. [Polly](http://www.thepollyproject.org/)의 BulkheadPolicy 개체는 Bulkhead와 큐가 얼마나 차 있는지 드러내며 오버플로에 대한 이벤트를 제공하므로 자동화된 수평 확장에 사용될 수 있습니다.

## <a name="additional-resources"></a>추가 자료

- **복원력 패턴**\
  [https://docs.microsoft.com/azure/architecture/patterns/category/resiliency](/azure/architecture/patterns/category/resiliency)

- **복원력 추가 및 성능 최적화**\
  <https://docs.microsoft.com/previous-versions/msp-n-p/jj591574(v=pandp.10)>

- **Bulkhead.** GitHub 리포지토리. Polly 정책 구현.\
  <https://github.com/App-vNext/Polly/wiki/Bulkhead>

- **Azure용 복원력 있는 애플리케이션 디자인**\
  [https://docs.microsoft.com/azure/architecture/resiliency/](/azure/architecture/resiliency/)

- **일시적인 오류 처리**\
  [https://docs.microsoft.com/azure/architecture/best-practices/transient-faults](/azure/architecture/best-practices/transient-faults)

>[!div class="step-by-step"]
>[이전](handle-partial-failure.md)
>[다음](implement-retries-exponential-backoff.md)
