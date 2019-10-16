---
title: Azure Container Service(즉, Kubernetes)에 Windows 컨테이너를 배포하는 경우
description: Azure 클라우드와 Windows 컨테이너를 사용하여 기존 .NET 응용 프로그램 최신화 | Azure Container Service(즉, Kubernetes)에 Windows 컨테이너를 배포하는 경우
ms.date: 04/30/2018
ms.openlocfilehash: 903082deba635dd0dfc22d0186fbc589f8d05b92
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "69577946"
---
# <a name="when-to-deploy-windows-containers-to-azure-container-service-that-is-kubernetes"></a>Azure Container Service(즉, Kubernetes)에 Windows 컨테이너를 배포하는 경우

Azure Container Service는 특히 Azure용으로 인기 있는 오픈 소스 도구 및 기술의 구성을 최적화합니다. 컨테이너와 응용 프로그램 구성에 대한 이식성이 제공되는 개방형 솔루션을 갖게 됩니다. 크기와 호스트 수 및 오케스트레이터 도구를 선택할 수 있습니다. Azure Container Service에서 인프라를 처리합니다.

이미 Kubernetes나 Docker Swarm, DC/OS와 같은 오픈 소스 오케스트레이터를 사용하여 작업하고 있는 경우, 컨테이너 워크로드를 클라우드로 변경하기 위해 기존 관리 방법을 변경할 필요가 없습니다. 이미 익숙한 기존의 응용 프로그램 관리 도구를 사용하고, 사용자가 선택한 오케스트레이터 표준 API 끝점을 통해 연결합니다.

Linux Docker 컨테이너를 사용하는 경우에는 이러한 오케스트레이터가 모두 완성도가 높은 상태지만, Windows 컨테이너를 사용하는 경우에는 미리 보기 상태일 수 있습니다.

예를 들어, kubernetes에서 컨테이너 지원은 기본 클래스(일급 객체)이므로 kubernetes에서 Windows 컨테이너를 사용하는 것도 효과적입니다(2018년 초 ACS 미리 보기의 경우).

중요 참고 사항: Kubernetes의 진화되고 '자세한 PaaS' ACS(Azure Container Service)의 버전은 AKS(Azure Kubernetes Service)입니다. Windows 컨테이너는 2018년 2분기에도 여전히 지원되지 않고 있지만 곧 지원될 예정입니다.

>[!div class="step-by-step"]
>[이전](when-to-deploy-windows-containers-to-azure-container-instances-ACI.md)
>[다음](choosing-azure-compute-options-for-container-based-applications.md)
