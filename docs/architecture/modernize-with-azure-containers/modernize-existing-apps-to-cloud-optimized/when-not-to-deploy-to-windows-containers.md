---
title: Windows 컨테이너에 배포하면 안 되는 경우
description: Azure 클라우드와 Windows 컨테이너를 사용하여 기존 .NET 응용 프로그램 최신화 | Windows 컨테이너를 배포하지 않는 경우
ms.date: 04/28/2018
ms.openlocfilehash: 65e793b846b495e9a1be6db9ddfa38bbf0d49445
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/30/2019
ms.locfileid: "69577956"
---
# <a name="when-not-to-deploy-to-windows-containers"></a>Windows 컨테이너에 배포하면 안 되는 경우

일부 Windows 기술은 Windows 컨테이너에서 지원되지 않습니다. 이러한 경우 일반적으로 Windows와 IIS만 사용하여 표준 VM에 마이그레이션해야 합니다.

2018년 5월 기준으로 Windows 컨테이너에서 지원되지 않는 경우는 다음과 같습니다.

- 현재 Microsoft 메시지 큐(MSMQ)는 다른 이전 릴리스에서는 사용할 수 없고 Windows Server v1803 릴리스 기반의 Windows 컨테이너에서만 사용할 수 있습니다.

  - [UserVoice 요청 포럼](https://windowsserver.uservoice.com/forums/304624-containers/suggestions/15719031-create-base-container-image-with-msmq-server)

  - [토론 포럼](https://social.msdn.microsoft.com/Forums/bce99a7d-aa60-44fa-a348-450855650810/msmqserver-is-it-supported?forum=windowscontainers)

- Microsoft Distributed Transaction Coordinator(MSDTC)는 현재 Windows 컨테이너에서 지원되지 않습니다.

  - [GitHub 문제](https://github.com/MicrosoftDocs/Virtualization-Documentation/issues/494)

- 현재 Microsoft Office는 컨테이너를 지원하지 않습니다.

  - [UserVoice 요청 포럼](https://windowsserver.uservoice.com/forums/304624-containers/suggestions/19686220-provide-office-support-for-containers)

- UI 앱(시각적 사용자 인터페이스를 사용한 클라이언트 앱)은 지원되는 시나리오가 아닙니다.

- Windows 인프라 역할(DNS, DHCP, DC, NTP, 인쇄, 파일 서버, IAM 등)은 지원되는 시나리오가 아닙니다.

지원되지 않는 더 많은 시나리오와 커뮤니티의 요청은 다음의 Windows 컨테이너의 UserVoice 포럼을 참조하세요: <https://windowsserver.uservoice.com/forums/304624-containers>

### <a name="additional-resources"></a>추가 자료

- **Virtual machine과 Azure의 컨테이너**

    <https://azure.microsoft.com/overview/containers/>

> [!div class="step-by-step"]
> [이전](deploy-existing-net-apps-as-windows-containers.md)
> [다음](when-to-deploy-windows-containers-in-your-on-premises-iaas-vm-infrastructure.md)
