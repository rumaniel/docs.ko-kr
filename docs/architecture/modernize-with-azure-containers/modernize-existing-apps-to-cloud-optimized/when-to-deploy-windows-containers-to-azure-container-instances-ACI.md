---
title: Windows 컨테이너를 Azure ACI(Container Instances)에 배포하는 경우
description: Azure 클라우드와 Windows 컨테이너를 사용하여 기존 .NET 응용 프로그램 최신화 | Windows 컨테이너를 Azure ACI(Container Instances)에 배포하는 경우
ms.date: 04/29/2018
ms.openlocfilehash: 3b6ae1ced9c4e01f5ab400e2575947a396064ebd
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "69577936"
---
# <a name="when-to-deploy-windows-containers-to-azure-container-instances-aci"></a>Windows 컨테이너를 Azure ACI(Container Instances)에 배포하는 경우

Azure Container Instances에 주된 가치는 바로 컨테이너를 ACI에 배포할 수 있으며 환경을 유지할 필요가 없다는 것입니다. 기본 운영 체제나 VM을 업그레이드하거나 패치할 필요가 없습니다. 모든 것이 투명하며 즉시 사용할 수 있는 환경에 컨테이너를 배포하면 됩니다.

ACI를 사용하는 이유와 시나리오는 Azure VM을 컨테이너와 함께 사용할 때의 주요 시나리오와 유사하며, 기본적으로 Azure 컨테이너 인스턴스를 사용하는 주요 시나리오는 다음과 같습니다.

- **개발/테스트 시나리오**
- **작업 자동화**
- **CI/CD 에이전트**
- **작거나 규모 있는 배치 처리**
- **간단한 웹 앱**

간단한 웹 응용 프로그램 시나리오는 ACI에 대한 적절한 시나리오이지만 ACI에서는 컨테이너 이미지 당 하나의 컨테이너 인스턴스만 가질 수 있기 때문에 가용성이 높지 않고 확장성이 제한적이라는 것을 고려해야 합니다.

그러나 ACI가 단일 컨테이너 인스턴스를 제공하므로 인프라로 보더라도 Windows Server를 사용하는 일반 Azure VM과 비교하면 큰 이점이 있습니다. ACI를 사용하면 자체 관리 환경에 컨테이너를 배포하고 단지 그 컨테이너의 비용을 지불하면 됩니다. VM을 유지/업데이트/패치할 필요가 없으므로 컨테이너가 있는 VM을 사용하는 대부분의 시나리오에서 훨씬 더 나은 플랫폼입니다. ACI를 사용하면 컨테이너를 배포하기만 하면 되고, 컨테이너를 배포하는 VM 환경을 만들 필요가 없습니다.

ACI (Azure Container Instances)의 주요 이점은 다음과 같습니다.

- 서버를 관리 하지 않고 컨테이너 실행
- 주문형 컨테이너를 사용 하 여 민첩성 향상
- 전에 없던 단순성과 속도로 클라우드에 컨테이너를 단일 명령을 통해 배포
- 하이퍼바이저 격리를 통한 응용 프로그램 보안

즉, ACI를 사용하면 VM을 관리하거나 새로운 도구를 배울 필요 없이 빠르게 앱을 개발할 수 있습니다. 이 앱은 클라우드에서 동작하는 하나의 컨테이너 내에 존재합니다.

> [!div class="step-by-step"]
> [이전](when-to-deploy-windows-containers-to-azure-vms-iaas-cloud.md)
> [다음](when-to-deploy-windows-containers-to-azure-container-service-kubernetes.md)
