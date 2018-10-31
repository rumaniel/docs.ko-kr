---
title: 일반적인 컨테이너 설계 원칙
description: Microsoft 플랫폼 및 도구를 사용하여 컨테이너화된 Docker 응용 프로그램 수명 주기
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 09/22/2017
ms.openlocfilehash: 3af174279e8b6f56a10413817b05ef68cfcabea5
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50202180"
---
# <a name="common-container-design-principles"></a>일반적인 컨테이너 설계 원칙

계속 해 서 개발 프로세스에 가져오는 경우 컨테이너를 사용 하는 방법에 대해 언급할 몇 가지 기본 개념

## <a name="container-equals-a-process"></a>컨테이너 프로세스 같음

컨테이너 모델 컨테이너는 단일 프로세스를 나타냅니다. 컨테이너를 프로세스 경계로 정의 하면 눈금 또는 일괄 처리 오프, 프로세스에 사용 되는 기본 형식 만들기를 시작 합니다. Docker 컨테이너를 실행 하는 경우 표시 됩니다는 [ENTRYPOINT](https://docs.docker.com/engine/reference/builder/#/entrypoint) 정의 합니다. 프로세스 및 컨테이너의 수명을 정의합니다. 프로세스가 완료 되 면 컨테이너 수명 주기가 종료 됩니다. 웹 서버 및 Microsoft Azure로 구현 했을 수 있는 일괄 작업과 같은 단기 실행 프로세스와 같은 장기 실행 프로세스가 [WebJobs](https://azure.microsoft.com/documentation/articles/websites-webjobs-resources/)합니다. 프로세스에 실패할 경우 컨테이너가 종료되며 조정자가 이어서 프로세스를 진행합니다. 오 케 스트레이 터를 실행 하는 5 개의 인스턴스를 유지 하도록 지정 된 하나에 오류가 발생 하는 경우는 오 케 스트레이 터는 실패 한 프로세스를 바꾸려면 다른 컨테이너를 만듭니다. 일괄 작업에서 프로세스는 매개 변수와 함께 시작됩니다. 프로세스가 완료되면 작업이 완료됩니다.

여러 프로세스를 단일 컨테이너에서 실행 하려는 경우를 확인할 수 있습니다. 아키텍처 문서에서 되지 않습니다는 "never," 항상 새로운 기술이 나는 "항상"입니다. 여러 프로세스를 요구 하는 시나리오에 대 한 일반적인 패턴을 사용 하는 것 [감독자](http://supervisord.org/)합니다.


>[!div class="step-by-step"]
[이전](design-docker-applications.md)
[다음](monolithic-applications.md)
