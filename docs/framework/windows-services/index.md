---
title: Windows 서비스 애플리케이션 개발
ms.date: 03/30/2017
helpviewer_keywords:
- ServiceInstaller class, Windows Service applications
- Service class, Windows Service applications
- Windows Service applications
- Windows NT services
- ServiceProcessInstaller class, Windows Service applications
- services
- .NET applications, Windows applications
ms.assetid: ba72d648-9553-4849-b829-069ad5ea014b
author: ghogen
ms.openlocfilehash: 61f969c22ac06bd6ed20ccfa9124db3bb35d0692
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053550"
---
# <a name="develop-windows-service-apps"></a>Windows 서비스 앱 개발

Visual Studio 또는 .NET Framework SDK를 사용하면 서비스로 설치되는 애플리케이션을 만들어 서비스를 쉽게 만들 수 있습니다. 이 유형의 애플리케이션을 Windows 서비스라고 합니다. 프레임워크 기능을 사용하여 서비스를 만들고 설치하고 시작 및 중지할 수 있으며 서비스 동작을 제어할 수도 있습니다.

> [!NOTE]
> Visual Studio에서는 필요한 경우 기존 C++ 코드와 상호 운용될 수 있는 Visual C# 또는 Visual Basic의 관리 코드에서 서비스를 만들 수 있습니다. 또는 [ATL 프로젝트 마법사](/cpp/atl/reference/atl-project-wizard)를 사용하여 네이티브 C++에서 Windows 서비스를 만들 수 있습니다.

## <a name="in-this-section"></a>단원 내용

[Windows 서비스 애플리케이션 소개](introduction-to-windows-service-applications.md)

Windows 서비스 애플리케이션, 서비스 수명 및 서비스 애플리케이션이 다른 일반적인 프로젝트 유형과 다른 점에 대해 간략히 설명합니다.

[연습: 구성 요소 디자이너에서 Windows 서비스 애플리케이션 만들기](walkthrough-creating-a-windows-service-application-in-the-component-designer.md)

Visual Basic 및 Visual C#에서 서비스를 만드는 예제를 제공합니다.

[서비스 애플리케이션 프로그래밍 아키텍처](service-application-programming-architecture.md)

서비스 프로그래밍에서 사용되는 언어 요소에 대해 설명합니다.

[방법: Windows 서비스 만들기](how-to-create-windows-services.md)

Windows 서비스 프로젝트 템플릿을 사용하여 Windows 서비스를 만들고 구성하는 프로세스에 대해 설명합니다.

## <a name="related-sections"></a>관련 단원

<xref:System.ServiceProcess.ServiceBase> - 서비스를 만드는 데 사용되는 <xref:System.ServiceProcess.ServiceBase> 클래스의 주요 기능에 대해 설명합니다.

<xref:System.ServiceProcess.ServiceProcessInstaller> - 서비스를 설치 및 제거하기 위해 <xref:System.ServiceProcess.ServiceInstaller> 클래스와 함께 사용되는 <xref:System.ServiceProcess.ServiceProcessInstaller> 클래스의 기능에 대해 설명합니다.

<xref:System.ServiceProcess.ServiceInstaller> - 서비스를 설치 및 제거하기 위해 <xref:System.ServiceProcess.ServiceProcessInstaller> 클래스와 함께 사용되는 <xref:System.ServiceProcess.ServiceInstaller> 클래스의 기능에 대해 설명합니다.

[템플릿에서 프로젝트 만들기](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/0fyc0azh(v=vs.120)) - 이 챕터에서 사용되는 프로젝트 유형과 이들 유형 중에서 선택하는 방법을 설명합니다.
