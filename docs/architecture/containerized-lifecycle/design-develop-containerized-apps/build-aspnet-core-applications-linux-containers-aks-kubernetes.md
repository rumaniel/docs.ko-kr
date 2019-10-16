---
title: AKS/Kubernetes 클러스터에 Linux 컨테이너로 배포된 ASP.NET Core 2.2 애플리케이션 빌드
description: Microsoft 플랫폼 및 도구를 사용하여 컨테이너화된 Docker 애플리케이션 수명 주기
ms.date: 02/25/2019
ms.openlocfilehash: ab64a0423ceceb8285c159af276d6d97e12379d8
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70848746"
---
# <a name="build-aspnet-core-22-applications-deployed-as-linux-containers-into-an-akskubernetes-orchestrator"></a>AKS/Kubernetes 오케스트레이터에 Linux 컨테이너로 배포된 ASP.NET Core 2.2 애플리케이션 빌드

AKS(Azure Kubernetes Service)는 컨테이너 배포 및 관리를 간소화하는 Azure의 관리형 Kubernetes 오케스트레이션 서비스입니다.

AKS의 주요 기능은 다음과 같습니다.

- Azure에서 호스팅하는 제어 평면
- 자동화된 업그레이드
- 자동 복구
- 사용자 구성 가능 크기 조정
- 개발자와 클러스터 운영자 모두에게 더 간단한 사용자 환경.

다음 예제에서는 Visual Studio 2017을 사용하여 개발이 수행되는 동안 Linux에서 실행하고 Azure의 AKS 클러스터에 배포되는 ASP.NET Core 2.2 애플리케이션을 만들어 봅니다.

## <a name="creating-the-aspnet-core-22-project-using-visual-studio-2017"></a>Visual Studio 2017을 사용하여 ASP.NET Core 2.2 프로젝트 만들기

ASP.NET Core는 Microsoft 및 GitHub의 .NET 커뮤니티에서 유지 관리하는 범용 개발 플랫폼입니다. Windows, macOS 및 Linux 플랫폼 간 교차 사용을 지원하며 디바이스, 클라우드 및 포함/IoT 시나리오에서 사용할 수 있습니다.

이 예제에서는 Visual Studio 웹 API 템플릿 기반의 간단한 프로젝트를 사용하므로 샘플을 만들기 위한 추가 지식은 필요하지 않습니다. ASP.NET Core 2.2 기술을 사용하여 REST API를 통해 작은 프로젝트를 실행하기 위한 모든 요소가 포함된 표준 템플릿을 사용하여 프로젝트를 만들기만 하면 됩니다.

![Visual Studio에서 ASP.NET Core 웹 애플리케이션을 선택하는 새 프로젝트 창을 추가합니다.](media/create-aspnet-core-application.png)

**그림 4-36**. ASP.NET Core 애플리케이션 만들기

Visual Studio에서 샘플 프로젝트를 만들려면 **파일** > **새로 만들기** > **프로젝트**를 선택하고 왼쪽 창에서 **웹** 프로젝트 형식을 선택한 후 **ASP.NET Core 웹 애플리케이션**을 선택합니다.

Visual Studio에 웹 프로젝트용 템플릿이 나열됩니다. 이 예제에서는 **API**를 선택하여 ASP.NET 웹 API 애플리케이션을 만듭니다.

ASP.NET Core 2.2를 프레임워크로 선택했는지 확인합니다. .NET Core 2.2는 Visual Studio 2017의 최신 버전에 포함되어 Visual Studio 2017을 설치하면 자동으로 설치되고 구성됩니다.

![API 옵션이 선택된 상태에서 ASP.NET Core 웹 애플리케이션 유형을 선택하기 위한 Visual Studio 대화 상자](media/create-web-api-application.png)

**그림 4-37**. ASP.NET CORE 2.2 및 웹 API 프로젝트 형식 선택

이전 버전의 .NET Core를 보유한 경우 <https://dotnet.microsoft.com/download>에서 2.2 버전을 다운로드하여 설치할 수 있습니다.

프로젝트를 만들 때 또는 그 후에 Docker 지원을 추가할 수 있으므로 언제든지 프로젝트를 "Docker화"할 수 있습니다. 프로젝트를 만든 후 Docker 지원을 추가하려면 솔루션 탐색기에서 프로젝트 노드를 마우스 오른쪽 단추로 클릭하고 바로 가기 메뉴에서 **추가** > **Docker 지원**을 선택합니다.

![기존 프로젝트에 Docker 지원을 추가하는 바로 가기 메뉴 옵션: (프로젝트에서)마우스 오른쪽 단추를 클릭 > 추가 > Docker 지원](media/add-docker-support-to-project.png)

**그림 4-38**. 기존 프로젝트에 Docker 지원 추가

Docker 지원 추가를 완료하려면 Windows 또는 Linux를 선택할 수 있습니다. AKS는 Windows 컨테이너를 지원하지 않으므로(2018년 말 현재) 이 경우 **Linux**를 선택합니다.

![Dockerfile에 대한 대상 OS를 선택하는 옵션 대화 상자](media/select-linux-docker-support.png)

**그림 4-39**. Linux 컨테이너 선택

이 간단한 단계를 수행하면 Linux 컨테이너에서 실행하는 ASP.NET Core 2.2 애플리케이션을 갖게 됩니다.

보다시피 Visual Studio 2017과 Docker는 개발자의 생산성을 최대한 높이는 방법으로 통합되었습니다.

이제 **F5** 키를 누르거나 **재생** 단추를 사용하여 애플리케이션을 실행할 수 있습니다.

프로젝트를 실행한 후 `docker images` 명령을 사용하여 이미지를 나열할 수 있습니다. Visual Studio 2017을 통해 프로젝트를 자동 배포하여 만든 `mssampleapplication` 이미지가 보일 것입니다.

```console
docker images
```

![Docker 이미지 명령의 콘솔 출력에 다음 정보를 포함하는 목록이 표시됩니다. 리포지토리, 태그, 이미지 ID, 만든 날짜 및 크기](media/docker-images-command.png)

**그림 4-40**. Docker 이미지 보기

## <a name="register-the-solution-in-the-azure-container-registry"></a>Azure Container Registry에 솔루션 등록

이미지를 [ACR(Azure Container Registry)](https://azure.microsoft.com/services/container-registry/) 또는 Docker Hub와 같은 Docker 레지스트리에 업로드하여 해당 레지스트리에서 이미지를 AKS 클러스터에 배포할 수 있도록 합니다. 이 경우 이미지를 Azure Container Registry에 업로드합니다.

### <a name="create-the-image-in-release-mode"></a>릴리스 모드에서 이미지 만들기

이제 그림 4-41과 같이 **릴리스**로 변경하고 이전과 같은 방법으로 애플리케이션을 실행하여 **릴리스** 모드에서 (프로덕션 준비가 완료된) 이미지를 만듭니다.

![릴리스 모드에서 빌드하기 위한 VS의 도구 모음 옵션](media/select-release-mode.png)

**그림 4-41**. 릴리스 모드 선택

`docker image` 명령을 실행하면 만들어진 이미지 두 개(`debug`에 대한 이미지와 `release` 모드에 대한 이미지)가 모두 보입니다.

### <a name="create-a-new-tag-for-the-image"></a>이미지에 대한 새 태그 만들기

각 컨테이너 이미지에 레지스트리의 `loginServer` 이름으로 태그를 지정해야 합니다. 이 태그는 컨테이너 이미지를 이미지 레지스트리에 밀어넣을 때 라우팅에 사용됩니다.

Azure Portal에서 `loginServer` 이름을 보고 Azure Container Registry에서 정보를 가져올 수 있습니다.

![브라우저 오른쪽 위의 Azure 컨테이너 레지스트리 이름 보기](media/loginServer-name.png)

**그림 4-42**. 레지스트리의 이름 보기

또는 다음 명령을 실행하여 이름을 봅니다.

```console
az acr list --resource-group MSSampleResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

![위 명령의 콘솔 출력](media/az-cli-loginServer-name.png)

**그림 4-43**. PowerShell을 사용하여 레지스트리의 이름 가져오기

두 경우 모두 이름을 가져옵니다. 이 예제의 경우 이름은 `mssampleacr.azurecr.io`입니다.

이제 다음 명령을 사용하여 이미지에 태그를 지정하고 최신 이미지를 가져올 수 있습니다.

```console
docker tag mssampleaksapplication:latest mssampleacr.azurecr.io/mssampleaksapplication:v1
```

`docker tag` 명령을 실행한 후 `docker images` 명령을 사용하여 이미지를 나열하면 새 태그가 지정된 이미지가 보일 것입니다.

![Docker 이미지 명령의 콘솔 출력](media/tagged-docker-images-list.png)

**그림 4-44**. 태그가 지정된 이미지 보기

### <a name="push-the-image-into-the-azure-acr"></a>Azure ACR에 이미지 푸시

Azure Container Registry에 로그인합니다.

```console
az acr login --name mssampleacr
```

다음 명령을 사용하여 이미지를 Azure ACR에 푸시합니다.

```console
docker push mssampleacr.azurecr.io/mssampleaksapplication:v1
```

이 명령은 이미지를 업로드하는 동안 다소 시간이 걸리지만 프로세스와 관련된 피드백을 제공합니다.

![Docker 푸시 명령의 콘솔 출력: 각 레이어에 대한 문자 기반 진행률 표시줄을 보여줍니다.](media/uploading-image-to-acr.png)

**그림 4-45**. ACR에 이미지 업로드

프로세스가 완료될 때 얻는 결과를 아래에서 확인할 수 있습니다.

![Docker 푸시 명령의 콘솔 출력, 완료된 상태이며 모든 레이어 또는 노드를 보여줍니다.](media/uploading-docker-images-complete.png)

**그림 4-46**. 노드 보기

다음으로 컨테이너를 AKS Kubernetes 클러스터에 배포합니다. 이 단계를 위해 다음을 포함하는 파일( **.yml 배포 파일**)이 필요합니다.

```yml
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: mssamplesbook
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: mssample-kub-app
    spec:
      containers:
        - name: mssample-services-app
          image: mssampleacr.azurecr.io/mssampleaksapplication:v1
          ports:
            - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
    name: mssample-kub-app
spec:
  ports:
    - name: http-port
      port: 80
      targetPort: 80
  selector:
    app: mssample-kub-app
  type: LoadBalancer
```

> [!NOTE]
> Kubernetes를 사용한 배포에 대한 자세한 내용은 <https://kubernetes.io/docs/reference/kubectl/cheatsheet/>를 참조하세요.

이제 **Kubectl**을 사용하여 배포할 준비가 거의 완료되었지만 먼저 이 명령을 사용하여 자격 증명을 AKS 클러스터로 가져와야 합니다.

```console
az aks get-credentials --resource-group MSSampleResourceGroupAKS --name mssampleclusterk801
```

![위 명령의 콘솔 출력: /root/.kube/config의 현재 컨텍스트로 병합된 "MSSampleK8Cluster"](media/getting-aks-credentials.png)

**그림 4-47**. 자격 증명 가져오기

그런 다음, `kubectl create` 명령을 사용하여 배포를 시작합니다.

```console
kubectl create -f mssample-deploy.yml
```

![위 명령의 콘솔 출력: 배포 "mssamplesbook"이 만들어졌습니다. 서비스 "mssample-kub-app"이 만들어졌습니다.](media/kubectl-create-command.png)

**그림 4-48**. Kubernetes에 배포

배포가 완료되면 이 명령을 사용하여 일시적으로 액세스할 수 있는 로컬 프록시를 통해 Kubernetes 콘솔에 액세스할 수 있습니다.

```console
az aks browse --resource-group MSSampleResourceGroupAKS --name mssampleclusterk801
```

그리고 URL `http://127.0.0.1:8001`에 액세스합니다.

![배포, Pod, 복제본 세트 및 서비스를 보여주는 Kubernetes 대시보드의 브라우저 보기](media/kubernetes-cluster-information.png)

**그림 4-49**. Kubernetes 클러스터 정보 보기

지금까지 Linux 컨테이너를 사용하여 Azure 및 AKS Kubernetes 클러스터에 애플리케이션을 배포했습니다. 앱에 액세스하여 Azure Portal에서 가져올 수 있는 서비스의 공용 IP를 탐색할 수 있습니다.

> [!NOTE]
> 이 가이드의 [**AKS(Azure Kubernetes Service)에 배포**](deploy-azure-kubernetes-service.md) 섹션에서 이 샘플에 대한 AKS 클러스터를 만드는 방법을 확인할 수 있습니다.

>[!div class="step-by-step"]
>[이전](set-up-windows-containers-with-powershell.md)
>[다음](../docker-devops-workflow/index.md)
