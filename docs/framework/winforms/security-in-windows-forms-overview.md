---
title: Windows Forms의 보안 개요
ms.date: 03/30/2017
helpviewer_keywords:
- code access security [Windows Forms], Windows Forms
- permissions [Windows Forms], Windows Forms
- Windows Forms, security
- security [Windows Forms], about security
- access control [Windows Forms], Windows Forms
ms.assetid: 4810dc9f-ea23-4ce1-8ea1-657f0ff1d820
ms.openlocfilehash: 08c80eccee395d9141978a7d4594205af1a51ed9
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972137"
---
# <a name="security-in-windows-forms-overview"></a>Windows Forms의 보안 개요

.NET Framework 릴리스 전에 사용자의 컴퓨터에서 실행 되는 모든 코드에는 컴퓨터의 사용자에 게 있는 리소스에 액세스 하는 것과 동일한 권한 또는 사용 권한이 있었습니다. 예를 들어 사용자가 파일 시스템에 액세스할 수 있는 경우 코드에서 파일 시스템에 액세스할 수 있었습니다. 사용자가 데이터베이스에 액세스할 수 있는 경우 코드에서 해당 데이터베이스에 액세스할 수 있었습니다. 이러한 권한 또는 사용 권한은 사용자가 명시적으로 로컬 컴퓨터에 설치한 실행 파일의 코드에는 적합할 수 있지만 인터넷 또는 로컬 인트라넷에서 들어오는 잠재적 악성 코드에는 적합하지 않을 수 있습니다. 이 코드는 권한 없이 사용자의 컴퓨터 리소스에 액세스할 수 없어야 합니다.

.NET Framework 코드 액세스 보안 이라는 인프라를 도입 하 여 해당 코드에 사용자가 보유 한 권한 또는 권한을 구별할 수 있도록 합니다. 기본적으로 인터넷 및 인트라넷에서 들어오는 코드는 부분 신뢰에서만 실행할 수 있습니다. 부분 신뢰에서는 애플리케이션에 일련의 제한이 적용됩니다. 특히, 애플리케이션의 로컬 하드 디스크 액세스가 제한되며 비관리 코드를 실행할 수 없습니다. .NET Framework는 해당 코드의 id를 기반으로 코드에 액세스할 수 있는 리소스를 제어 합니다. 여기에는 해당 코드의 출처, [강력한 이름의 어셈블리가](../../standard/assembly/strong-named.md)있는지 여부, 인증서로 서명 되었는지 여부 등이 포함 됩니다.

Windows Forms 응용 프로그램을 배포 하는 데 사용 하는 ClickOnce 기술은 부분 신뢰, 완전 신뢰 또는 높은 권한으로 부분 신뢰에서 실행 되는 응용 프로그램을 보다 쉽게 개발할 수 있도록 도와줍니다. ClickOnce는 권한 상승 및 신뢰할 수 있는 응용 프로그램 배포와 같은 기능을 제공 하므로 응용 프로그램이 책임 방식으로 로컬 사용자 로부터 완전 신뢰 또는 높은 권한을 요청할 수 있습니다.

## <a name="understanding-security-in-the-net-framework"></a>.NET Framework의 보안 이해

코드 액세스 보안을 통해 코드 발생 위치 및 코드 ID의 다른 측면에 따라 다양한 수준으로 코드를 신뢰할 수 있습니다. 공용 언어 런타임에서 보안 정책을 결정하는 데 사용하는 증거에 대한 자세한 내용은 [증거](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/7y5x1hcd(v=vs.100))를 참조하세요. 악성 코드로부터 컴퓨터 시스템을 보호하고 의도적으로 또는 실수로 보안이 손상되지 않도록 신뢰할 수 있는 코드를 보호합니다. 코드 액세스 보안을 통해 애플리케이션에 필요한 권한만 지정할 수 있으므로 애플리케이션이 수행할 수 있는 작업에 대한 제어도 강화됩니다. 코드 액세스 보안은 코드에서 단일 코드 액세스 보안 권한 검사를 수행하지 않는 경우에도 공용 언어 런타임을 대상으로 하는 모든 관리 코드에 영향을 줍니다. .NET Framework 보안에 대 한 자세한 내용은 [주요 보안 개념](../../standard/security/key-security-concepts.md) 및 [코드 액세스 보안 기본 사항](../misc/code-access-security-basics.md)을 참조 하세요.

사용자가 웹 서버 또는 파일 공유에서 직접 Windows Forms 실행 파일을 실행하는 경우 애플리케이션에 부여되는 신뢰 수준은 코드가 상주하는 위치 및 시작 방법에 따라 달라집니다. 애플리케이션이 실행되면 자동으로 평가되고 공용 언어 런타임으로부터 명명된 권한 집합을 받습니다. 기본적으로 로컬 컴퓨터의 코드에는 완전 신뢰 권한 집합이 부여되고, 로컬 네트워크의 코드에는 로컬 인트라넷 권한 집합이 부여되며, 인터넷의 코드에는 인터넷 권한 집합이 부여됩니다.

> [!NOTE]
> .NET Framework 버전 1.0 서비스 팩 1 및 서비스 팩 2에서는 인터넷 영역 코드 그룹이 Nothing 권한 집합을 받습니다. .NET Framework의 다른 모든 릴리스에서는 인터넷 영역 코드 그룹이 인터넷 권한 집합을 받습니다.
>
> 각 권한 집합에 부여되는 기본 권한은 [기본 보안 정책](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/03kwzyfc(v=vs.100)) 항목에 나열됩니다. 받는 권한에 따라 애플리케이션이 올바르게 실행되거나 보안 예외를 생성합니다.
>
> 많은 Windows Forms 응용 프로그램은 ClickOnce를 사용 하 여 배포 됩니다. ClickOnce 배포를 생성 하는 데 사용 되는 도구는 앞에서 설명한 것과 다른 보안 기본값을 갖습니다. 자세한 내용은 다음 설명을 참조하세요.

보안 정책을 수정할 수 있기 때문에 애플리케이션에 부여되는 실제 권한은 기본값과 다를 수 있습니다. 즉, 컴퓨터에 따라 애플리케이션의 권한이 다를 수 있습니다.

## <a name="developing-a-more-secure-windows-forms-application"></a>보다 안전한 Windows Forms 애플리케이션 개발

보안은 애플리케이션 개발의 모든 단계에서 중요합니다. 먼저 [보안 코딩 지침](../../standard/security/secure-coding-guidelines.md)을 검토하고 따릅니다.

그런 다음 애플리케이션을 완전 신뢰로 실행해야 하는지 여부 또는 부분 신뢰로 실행해야 하는지 여부를 결정합니다. 완전 신뢰에서 애플리케이션을 실행하면 로컬 컴퓨터의 리소스에 더 쉽게 액세스할 수 있지만 보안 코딩 지침 항목에 따라 엄격하게 애플리케이션을 디자인 및 개발하지 않을 경우 애플리케이션 및 해당 사용자가 높은 보안 위험에 노출됩니다. 부분 신뢰로 애플리케이션을 실행하면 보다 안전한 애플리케이션을 쉽게 개발할 수 있고 많은 위험이 감소하지만 특정 기능을 구현하는 방법에서 추가 계획이 필요합니다.

부분 신뢰(즉, 인터넷 또는 로컬 인트라넷 권한 집합)를 선택하는 경우 이 환경에서 원하는 애플리케이션의 동작 방식을 결정합니다. Windows Forms는 부분 신뢰 환경에서 기능을 구현하는 보다 안전한 대체 방법을 제공합니다. 데이터 액세스와 같은 애플리케이션의 특정 부분을 부분 신뢰 및 완전 신뢰 환경 둘 다에 대해 다르게 디자인 및 작성할 수 있습니다. 애플리케이션 설정과 같은 일부 Windows Forms 기능은 부분 신뢰로 작동하도록 설계되었습니다. 자세한 내용은 [애플리케이션 설정 개요](./advanced/application-settings-overview.md)를 참조하세요.

애플리케이션에 부분 신뢰에서 허용하는 것보다 많은 권한이 필요하지만 완전 신뢰로 실행하지 않으려는 경우 필요한 추가 권한만 어설션하는 동시에 부분 신뢰로 실행할 수 있습니다. 예를 들어 부분 신뢰로 실행하지만 사용자의 파일 시스템에 있는 디렉터리에 대한 읽기 전용 액세스 권한을 응용 프로그램에 부여해야 경우 해당 디렉터리에 대해서만 <xref:System.Security.Permissions.FileIOPermission>을 요청할 수 있습니다. 올바르게 사용할 경우 이 접근 방식은 애플리케이션의 기능을 증가시키며 사용자의 보안 위험을 최소화할 수 있습니다.

부분 신뢰로 실행되는 애플리케이션을 개발할 때는 애플리케이션이 실행해야 하는 권한 및 애플리케이션이 선택적으로 사용할 수 있는 권한을 추적합니다. 모든 권한을 알고 난 후 애플리케이션 수준에서 권한에 대한 선언적 요청을 해야 합니다. 권한 요청은 응용 프로그램에 필요한 권한 및 특별히 원하지 않는 권한에 대 한 .NET Framework 실행 시간을 알려 줍니다. 권한 요청에 대한 자세한 내용은 [권한 요청](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/yd267cce(v=vs.100))을 참조하세요.

선택적 권한을 요청할 때는 애플리케이션에서 부여되지 않은 권한이 필요한 작업을 수행하는 경우 생성되는 보안 예외를 처리해야 합니다. <xref:System.Security.SecurityException>을 적절히 처리하면 응용 프로그램이 계속 작동할 수 있습니다. 애플리케이션은 예외를 사용하여 사용자에 대해 기능을 사용할 수 없도록 설정할지 여부를 결정할 수 있습니다. 예를 들어 필요한 파일 권한이 부여되지 않은 경우 애플리케이션에서 **저장** 메뉴 옵션을 사용할 수 없습니다.

적절한 권한을 모두 어설션했는지 확인하기 어려운 경우도 있습니다. 예를 들어 화면에서 무해한 것처럼 보이는 메서드 호출이 실행 중 특정 지점에서 파일 시스템에 액세스할 수도 있습니다. 필요한 모든 권한으로 애플리케이션을 배포하지 않을 경우 데스크톱에서 디버그할 때는 정상적으로 테스트되지만 배포 시 실패할 수 있습니다. .NET Framework 2.0 SDK 및 Visual Studio 2005 모두에는 응용 프로그램에 필요한 권한을 계산 하기 위한 도구인 MT.EXE 명령줄 도구와 Visual Studio의 권한 계산 기능이 각각 포함 되어 있습니다.

다음 항목에서는 추가 Windows Forms 보안 기능을 설명합니다.

|항목|설명|
|-----------|-----------------|
|- [Windows Forms의 파일 및 데이터 액세스 추가 보안](more-secure-file-and-data-access-in-windows-forms.md)|부분 신뢰 환경에서 파일 및 데이터에 액세스하는 방법을 설명합니다.|
|- [Windows Forms의 인쇄 추가 보안](more-secure-printing-in-windows-forms.md)|부분 신뢰 환경에서 인쇄 기능에 액세스하는 방법을 설명합니다.|
|- [Windows Forms의 추가 보안 고려 사항](additional-security-considerations-in-windows-forms.md)|창 조작 수행, 클립보드 사용 및 부분 신뢰 환경에서 비관리 코드 호출을 설명합니다.|

### <a name="deploying-an-application-with-the-appropriate-permissions"></a>적절한 권한으로 애플리케이션 배포

클라이언트 컴퓨터에 Windows Forms 응용 프로그램을 배포 하는 가장 일반적인 방법은 응용 프로그램을 실행 하는 데 필요한 모든 구성 요소를 설명 하는 배포 기술인 ClickOnce를 사용 하는 것입니다. ClickOnce는 매니페스트 라는 XML 파일을 사용 하 여 응용 프로그램을 구성 하는 어셈블리 및 파일과 응용 프로그램에 필요한 권한을 설명 합니다.

ClickOnce에는 클라이언트 컴퓨터에서 상승 된 권한을 요청 하는 두 가지 기술이 있습니다. 두 기술은 모두 Authenticode 인증서를 사용합니다. 인증서는 애플리케이션이 신뢰할 수 있는 소스에서 제공되었다는 일부 보증을 사용자에게 제공합니다.

다음 표에서는 이러한 기술을 설명합니다.

|높은 권한 기술|설명|
|------------------------------------|-----------------|
|권한 상승|애플리케이션을 처음 실행할 때 사용자에게 보안 대화 상자를 표시합니다. **권한 상승** 대화 상자는 사용자가 추가 신뢰를 부여할지 여부에 대해 합리적인 결정을 내릴 수 있도록 응용 프로그램을 게시한 사람을 사용자에게 알립니다.|
|신뢰할 수 있는 애플리케이션 배포|시스템 관리자가 클라이언트 컴퓨터에서 게시자 Authenticode 인증서의 일회성 설치를 수행해야 합니다. 이때부터 인증서로 서명된 애플리케이션은 신뢰할 수 있는 것으로 간주되며, 추가 확인 메시지 없이 로컬 컴퓨터에서 완전 신뢰로 실행될 수 있습니다.|

선택하는 기술은 배포 환경에 따라 달라집니다. 자세한 내용은 [ClickOnce 배포 전략 선택](/visualstudio/deployment/choosing-a-clickonce-deployment-strategy)을 참조하세요.

기본적으로 Visual Studio 또는 .NET Framework SDK 도구 (Mage.exe 및 Mageui.exe) 중 하나를 사용 하 여 배포 된 ClickOnce 응용 프로그램은 완전 신뢰가 있는 클라이언트 컴퓨터에서 실행 되도록 구성 됩니다. 부분 신뢰를 사용하거나 일부 추가 권한만 사용하여 애플리케이션을 배포하는 경우 이 기본값을 변경해야 합니다. 배포를 구성할 때 Visual Studio 또는 .NET Framework SDK 도구 Mageui.exe를 사용 하 여이 작업을 수행할 수 있습니다. Mageui.exe를 사용 하는 방법에 대 한 자세한 내용은 [연습: ClickOnce 응용 프로그램](/visualstudio/deployment/walkthrough-manually-deploying-a-clickonce-application)을 수동으로 배포 합니다.  자세한 내용은 [다음을 참조 하세요. ClickOnce 응용 프로그램](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2012/hafybdaa(v=vs.110)) 에 대 한 사용자 지정 [권한 설정 또는 방법: ClickOnce 응용 프로그램](/visualstudio/deployment/how-to-set-custom-permissions-for-a-clickonce-application)에 대 한 사용자 지정 권한을 설정 합니다.

ClickOnce 및 권한 상승의 보안 측면에 대 한 자세한 내용은 [Clickonce 응용 프로그램 보안](/visualstudio/deployment/securing-clickonce-applications)을 참조 하세요. 신뢰할 수 있는 애플리케이션 배포에 대한 자세한 내용은 [신뢰할 수 있는 애플리케이션 배포 개요](/visualstudio/deployment/trusted-application-deployment-overview)를 참조하세요.

### <a name="testing-the-application"></a>애플리케이션 테스트

Visual Studio를 사용 하 여 Windows Forms 응용 프로그램을 배포한 경우 개발 환경에서 부분 신뢰 또는 제한 된 권한 집합으로 디버깅을 사용 하도록 설정할 수 있습니다.  자세한 내용은 [다음을 참조 하세요. 제한된 권한으로 ClickOnce 애플리케이션 디버그](/visualstudio/deployment/how-to-debug-a-clickonce-application-with-restricted-permissions)를 참조하세요.

## <a name="see-also"></a>참고자료

- [Windows Forms 보안](windows-forms-security.md)
- [코드 액세스 보안 기본 사항](../misc/code-access-security-basics.md)
- [ClickOnce 보안 및 배포](/visualstudio/deployment/clickonce-security-and-deployment)
- [신뢰할 수 있는 응용 프로그램 배포 개요](/visualstudio/deployment/trusted-application-deployment-overview)
- [Mage.exe(매니페스트 생성 및 편집 도구)](../tools/mage-exe-manifest-generation-and-editing-tool.md)
- [MageUI.exe(매니페스트 생성 및 편집 도구, 그래픽 클라이언트)](../tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client.md)
