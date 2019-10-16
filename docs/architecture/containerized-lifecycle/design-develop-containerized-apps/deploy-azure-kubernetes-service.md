---
title: 높은 확장성 및 가용성을 위한 마이크로 서비스 및 다중 컨테이너 애플리케이션 오케스트레이션
description: Azure Kubernetes Service를 사용하여 앱을 배포하는 방법을 알아봅니다.
ms.date: 02/15/2019
ms.openlocfilehash: 0aa2f83fbf8f9a8815d65730002943cca748643d
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/23/2019
ms.locfileid: "71182363"
---
# <a name="deploy-to-azure-kubernetes-service-aks"></a>AKS(Azure Kubernetes Service)에 배포

원하는 클라이언트 운영 체제를 사용하여 AKS와 상호 작용할 수 있으며, 여기서는 Microsoft Windows 및 Windows의 Ubuntu Linux 임베디드 버전에서 Bash 명령을 사용하여 상호 작용하는 방법을 살펴보겠습니다.

AKS를 사용하기 전에 갖추어야 할 필수 구성 요소는 다음과 같습니다.

- Linux 또는 Mac 개발 머신
- Windows 개발 컴퓨터
  - Windows에서 사용하도록 설정된 개발자 모드.
  - Linux용 Windows 하위 시스템
- [Windows, Mac 또는 Linux](https://docs.microsoft.com/cli/azure/install-azure-cli)에 설치된 Azure CLI

> [!NOTE]
> 다음 항목에 대한 전체 정보를 찾으려면 다음을 수행합니다.
>
> Azure-CLI: <https://docs.microsoft.com/cli/azure/index>
>
> Linux용 Windows 하위 시스템: <https://docs.microsoft.com/windows/wsl/about>

## <a name="create-the-aks-environment-in-azure"></a>Azure에서 AKS 환경 만들기

AKS 환경을 만드는 여러 가지 방법이 있습니다. Azure CLI 명령을 사용하는 방법도 있고 Azure Portal을 사용하는 방법도 있습니다.

여기서는 Azure CLI를 사용하여 클러스터를 만들고 Azure Portal에서 결과를 검토하는 예제를 살펴볼 수 있습니다. 개발 머신에 Kubectl 및 Docker도 있어야 합니다.  

## <a name="create-the-aks-cluster"></a>AKS 클러스터 만들기

이 명령을 사용하여 AKS 클러스터를 만듭니다.

```console
az aks create --resource-group MSSampleResourceGroup --name MSSampleClusterK801 --agent-count 1 --generate-ssh-keys --location westus2
```

만들기 작업이 완료되면 Azure Portal에서 AKS가 생성된 것을 확인할 수 있습니다.

리소스 그룹:

![Azure AKS 리소스 그룹의 브라우저 보기.](media/aks-resource-group-view.png)

**그림 4-17**. Azure의 AKS 리소스 그룹 보기.

AKS 클러스터:

![AKS 리소스 그룹의 브라우저 보기.](media/aks-cluster-view.png)

**그림 4-18**. Azure의 AKS 보기.

`Azure-CLI` 및 `Kubectl`을 사용하여 만든 노드를 볼 수도 있습니다.

먼저, 자격 증명을 가져옵니다.

```console
az aks get-credentials --resource-group MSSampleK8ClusterRG --name MSSampleK8Cluster
```

![위 명령의 콘솔 출력: /root/.kube/config의 현재 컨텍스트로 병합된 "MsSampleK8Cluster"](media/get-credentials-command-result.png)

**그림 4-19**. `aks get-credentials` 명령 결과입니다.

다음과 같이 Kubectl에서 노드를 가져옵니다.

```console
kubectl get nodes
```

![위 명령의 콘솔 출력: 상태, 기간(실행된 시간) 및 버전이 있는 노드 목록](media/kubectl-get-nodes-command-result.png)

**그림 4-20**. `kubectl get nodes` 명령 결과입니다.

>[!div class="step-by-step"]
>[이전](orchestrate-high-scalability-availability.md)
>[다음](docker-apps-development-environment.md)
