---
title: 컨테이너 기반 응용 프로그램용 Azure 계산 플랫폼 선택
description: Azure 클라우드와 Windows 컨테이너를 사용하여 기존 .NET 응용 프로그램 최신화 | 컨테이너 기반 응용 프로그램용 Azure 계산 플랫폼 선택
ms.date: 05/04/2018
ms.openlocfilehash: 2262d2cf4e69e19e8b78c07c239602dd5dccc3cd
ms.sourcegitcommit: 628e8147ca10187488e6407dab4c4e6ebe0cac47
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72318674"
---
# <a name="choosing-azure-compute-platforms-for-container-based-applications"></a>컨테이너 기반 응용 프로그램용 Azure 계산 플랫폼 선택

앞선 절에서 Azure는 여러 가지를 선택할 수 있는 개방형 클라우드라는 것을 알 수 있었습니다. 요구 사항에 맞는 적합한 선택은 가능하더라도 컨테이너화된 응용 프로그램에 어떤 제품이나 기술을 사용해야 할 것인지 의문이 생길 수 있습니다.

*기본적인* 권장 사항으로, 이 설명서에서 권장하는 주요 기준은 다음과 같습니다.

- **단일 모놀리식 앱:** Azure App Service를 선택합니다.
- **N 계층 앱:** AKS (Azure Kubernetes Service)와 같은 orchestrator를 선택 하거나, 하나 이상의 백 엔드 서비스가 있는 경우 App Service를 선택 합니다.
- **마이크로 서비스** 컨테이너에 대해 AKS 또는 Azure Web Apps 선택
- **서버리스 functions 및 이벤트 처리기:** Azure 함수를 선택합니다
- **대규모 일괄 처리:** Azure Batch를 선택합니다.

그러나 제품의 선택은 특정 응용 프로그램의 요구 사항 및 특성에 따라 달라 지므로 이러한 권장 사항은 솔트를 사용 하 여 수행 해야 합니다. 처음에는 비슷한 형식으로 보일지라도 모든 응용 프로그램이 동일하지는 않습니다.

응용 프로그램의 요구사항을 심층적으로 분석한 후에 선택한 제품이 다를 수 있습니다. 그러나 출발점으로 특정 우선 순위에 따라 테스트하거나 측청할 수 있는 초기 지침을 갖는 것은 좋습니다.

그림 1에서 다양 한 종류의 앱과 이상적인 Azure 호스팅 시나리오에 대 한 분석을 볼 수 있습니다.

![그림 1](./media/image8.5.png)

> [!div class="step-by-step"]
> [이전](when-to-deploy-windows-containers-to-azure-container-service-kubernetes.md)
> [다음](build-resilient-services-ready-for-the-cloud-embrace-transient-failures-in-the-cloud.md)
