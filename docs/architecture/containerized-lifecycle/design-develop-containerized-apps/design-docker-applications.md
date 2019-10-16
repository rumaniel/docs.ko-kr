---
title: Docker 애플리케이션 설계
description: 이 가이드에서 자세히 설명하지 않은 주제이므로, 여기에서 마이크로서비스 아키텍처에 대한 심층적인 안내서를 참조하세요.
ms.date: 02/15/2019
ms.openlocfilehash: b9539ff4edf405ab890d83be59a248ffa2360c99
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68674040"
---
# <a name="design-docker-applications"></a>Docker 애플리케이션 설계

1장에서는 컨테이너 및 Docker에 대한 기본 개념을 소개했습니다. 해당 정보는 시작하는 데 필요한 기본적인 정보 수준입니다. 그러나 엔터프라이즈 애플리케이션은 단일 서비스나 컨테이너 대신 여러 서비스로 구성되어 복잡할 수 있습니다. 이러한 선택적 사용 사례의 경우 SOA(Service-Oriented Architecture), 고급 마이크로서비스 개념 및 컨테이너 오케스트레이션 개념과 같은 설계에 대한 추가 접근 방식을 알아야 합니다. 이 문서의 범위는 마이크로서비스에 국한되지 않고 모든 Docker 애플리케이션 수명 주기에 적용되므로 심층적으로 마이크로서비스 아키텍처를 탐색하지 않습니다. 컨테이너 및 Docker를 일반적인 SOA, 백그라운드 작업 또는 모놀리식 애플리케이션 배포 방법으로도 사용할 수 있기 때문입니다.

**추가 정보** 엔터프라이즈 애플리케이션 및 마이크로서비스 아키텍처에 대한 자세한 내용을 알아보려면 <https://aka.ms/MicroservicesEbook>에서 다운로드할 수도 있는 NET 마이크로서비스: 컨테이너화된 .NET 애플리케이션을 위한 아키텍처](../../microservices/index.md)를 참조하세요.

그러나 애플리케이션 수명 주기 및 DevOps를 시작하기 전에 애플리케이션을 설계하고 구성하는 방법과 디자인 선택 방법을 파악하는 것이 중요합니다.

>[!div class="step-by-step"]
>[이전](index.md)
>[다음](common-container-design-principles.md)
