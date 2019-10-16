---
title: 지수 백오프를 사용하여 다시 시도 구현
description: 지수 백오프를 사용하여 다시 시도를 구현하는 방법을 알아봅니다.
ms.date: 10/16/2018
ms.openlocfilehash: 1b948e399495eeb12016006442ac08d2b04f2e69
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68674540"
---
# <a name="implement-retries-with-exponential-backoff"></a>지수 백오프를 사용하여 다시 시도 구현

[‘지수 백오프를 사용하여 다시 시도’](/azure/architecture/patterns/retry)는 최대 다시 시도 횟수에 도달할 때까지 대기 시간이 기하급수적으로 증가하면서 작업을 다시 시도하는 기술입니다([지수 백오프](https://en.wikipedia.org/wiki/Exponential_backoff)).  이 기술은 클라우드 리소스가 어떤 이유로든 몇 초간 일시적으로 사용할 수 없다는 팩트를 포함합니다. 예를 들어 오케스트레이터는 클러스터에서 부하 분산을 위해 컨테이너를 다른 노드로 이동할 수 있습니다. 이 시간 동안 일부 요청이 실패할 수 있습니다. 또 다른 예로 SQL Azure와 같은 데이터베이스를 들 수 있습니다. SQL Azure에서는 부하 분산을 위해 데이터베이스를 다른 서버로 옮길 수 있으므로 데이터베이스를 몇 초간 사용할 수 없게 됩니다.

지수 백오프를 사용하여 다시 시도 논리를 구현하는 많은 방법이 있습니다.

>[!div class="step-by-step"]
>[이전](partial-failure-strategies.md)
>[다음](implement-resilient-entity-framework-core-sql-connections.md)
