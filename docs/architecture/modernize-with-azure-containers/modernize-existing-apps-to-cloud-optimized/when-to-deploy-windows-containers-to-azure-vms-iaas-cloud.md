---
title: Azure VM(IaaS 클라우드)에 Windows 컨테이너를 배포하는 경우
description: Azure 클라우드와 Windows 컨테이너를 사용하여 기존 .NET 응용 프로그램 최신화 | Azure VM(IaaS 클라우드)에 Windows 컨테이너를 배포하는 경우
ms.date: 04/28/2018
ms.openlocfilehash: e9a2903662306b607977a7751018e24161ab80ab
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "69577906"
---
# <a name="when-to-deploy-windows-containers-to-azure-vms-iaas-cloud"></a>Azure VM(IaaS 클라우드)에 Windows 컨테이너를 배포하는 경우

조직에서 Azure VM을 사용한다면, Windows 컨테이너 또한 사용한다 해도 IaaS 사용하는 것입니다. 이는 부하 분산 인프라에 있는 여러 VM에 배포가 필요한 경우, 확장성이 뛰어난 응용 프로그램에 대한 인프라 운영과 VM OS 패치, 인프라 복잡성을 처리한다는 의미입니다. Azure VM에서 Windows 컨테이너를 사용하는 주요 시나리오는 다음과 같습니다.

- **개발/테스트 환경**: 클라우드의 VM은 클라우드에서의 개발과 테스트에 적합합니다. 필요에 따라 환경을 신속하게 만들고 중지할 수도 있습니다.

- **소규모 및 중간 규모의 확장성 요구**: 프로덕션 환경에 몇 개의 VM만 필요한 시나리오에서는 오케스트레이터와 같은 고급 PaaS 환경으로 옮기기 전까지 적은 수의 VM을 관리할 수 있습니다.

- **기존 배포 도구의 프로덕션 환경**: 복잡한 배포를 위해 도구에 투자한 온-프레미스 환경에서 VM이나 베어 메탈 서버(예 : 퍼핏 또는 유사한 도구)로 넘어갈 수 있습니다. 프로덕션 환경의 배포 절차의 변경을 최소화하면서 클라우드로 넘어가려면 해당 도구를 계속 사용하여 Azure VM에 배포할 수 있습니다. 하지만 Windows 컨테이너를 배포 단위로 사용하여 배포 환경을 개선하고자 할 것입니다.

>[!div class="step-by-step"]
>[이전](when-to-deploy-windows-containers-in-your-on-premises-iaas-vm-infrastructure.md)
>[다음](when-to-deploy-windows-containers-to-azure-container-instances-ACI.md)
