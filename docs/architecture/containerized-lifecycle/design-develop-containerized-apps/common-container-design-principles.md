---
title: 일반적인 컨테이너 설계 원칙
description: 적절한 컨테이너 디자인의 기본적인 원리를 알아봅니다. 이는 컨테이너를 하나의 프로세스만 호스팅해야 한다는 것입니다.
ms.date: 02/15/2019
ms.openlocfilehash: 69f3ff6c9303f0c4082695d861a8c90031295b6a
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68672500"
---
# <a name="common-container-design-principles"></a>일반적인 컨테이너 설계 원칙

개발 프로세스를 시작하기 전에 컨테이너를 사용하는 방법과 관련하여 언급할 가치가 있는 몇 가지 기본 개념이 있습니다.

## <a name="container-equals-a-process"></a>컨테이너는 프로세스와 같음

컨테이너 모델에서 컨테이너는 단일 프로세스를 나타냅니다. 컨테이너를 프로세스 경계로 정의하면 프로세스를 확장하거나 일괄 처리하는 데 사용되는 기본 형식을 만들기 시작합니다. Docker 컨테이너를 실행하면 [ENTRYPOINT](https://docs.docker.com/engine/reference/builder/#/entrypoint) 정의가 표시됩니다. 이는 컨테이너의 프로세스와 수명을 정의합니다. 프로세스가 완료되면 컨테이너 수명 주기가 종료됩니다. 웹 서버와 같이 장기간 실행되는 프로세스와 일괄 처리 작업과 같은 단기 실행 프로세스가 있습니다. 이는 Microsoft Azure [WebJobs](https://azure.microsoft.com/documentation/articles/websites-webjobs-resources/)로 구현되었을 수도 있습니다. 프로세스에 실패할 경우 컨테이너가 종료되며 조정자가 이어서 프로세스를 진행합니다. 오케스트레이터가 5개의 인스턴스를 계속 실행하도록 지시받은 경우, 한 인스턴스가 실패하면 오케스트레이터는 실패한 프로세스를 대체할 컨테이너를 만듭니다. 일괄 작업에서 프로세스는 매개 변수와 함께 시작됩니다. 프로세스가 완료되면 작업이 완료됩니다.

여러 프로세스를 단일 컨테이너에서 실행하려는 시나리오를 찾을 수 있습니다. 모든 아키텍처 문서에는 "never"는 절대 없고 "always"도 항상 없습니다. 여러 프로세스가 필요한 시나리오의 경우 일반적인 패턴은 [Supervisor](http://supervisord.org/)를 사용하는 것입니다.

>[!div class="step-by-step"]
>[이전](design-docker-applications.md)
>[다음](monolithic-applications.md)
