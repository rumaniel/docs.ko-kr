---
title: '방법: 서비스 시작'
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Service applications, starting
- services, starting
ms.assetid: 9ea77955-2d96-4c3d-913c-14db7604cdad
author: ghogen
ms.openlocfilehash: 75fd3aba88bdffbe536ad5dab14996913d0a9d22
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053565"
---
# <a name="how-to-start-services"></a>방법: 서비스 시작

서비스가 설치되면 서비스를 시작해야 합니다. 시작하면 서비스 클래스의 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 메서드가 호출됩니다. 일반적으로 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 메서드는 서비스가 수행할 유용한 정의합니다. 시작된 후 서비스는 수동으로 일시 중지하거나 중지할 때까지 활성 상태로 유지됩니다.

자동 또는 수동으로 시작하도록 서비스를 설정할 수 있습니다. 자동으로 시작하는 서비스는 설치된 컴퓨터가 재부팅되거나 처음으로 켜질 때 시작합니다. 수동으로 시작하는 서비스는 사용자가 시작해야 합니다.

> [!NOTE]
> 기본적으로 Visual Studio에서 만드는 서비스는 수동으로 시작하도록 설정됩니다.

서비스를 수동으로 시작할 수 있는 방법은 **서버 탐색기**나 **서비스 제어 관리자**에서 시작하거나 <xref:System.ServiceProcess.ServiceController>라는 구성 요소를 사용하는 코드에서 시작하는 등 여러 가지가 있습니다.

<xref:System.ServiceProcess.ServiceInstaller> 클래스의 <xref:System.ServiceProcess.ServiceInstaller.StartType%2A> 속성을 설정하여 서비스를 수동으로 시작할지 자동으로 시작할지를 지정할 수 있습니다.

### <a name="to-specify-how-a-service-should-start"></a>서비스 시작 방식을 지정하려면

1. 서비스를 만든 후 서비스에 필요한 설치 관리자를 추가합니다. 자세한 내용은 [방법: 서비스 애플리케이션에 설치 관리자 추가](how-to-add-installers-to-your-service-application.md)를 참조하세요.

2. 디자이너에서 작업 중인 서비스에 대한 서비스 설치 관리자를 클릭합니다.

3. **속성** 창에서 <xref:System.ServiceProcess.ServiceInstaller.StartType%2A> 속성을 다음 중 하나로 설정합니다.

    |서비스 설치 시기|설정 값|
    |----------------------------------|--------------------|
    |컴퓨터가 다시 시작될 때|**자동**|
    |명시적 사용자 작업으로 서비스가 시작될 때|**수동**|

    > [!TIP]
    > 서비스가 시작되지 않게 하려면 <xref:System.ServiceProcess.ServiceInstaller.StartType%2A> 속성을 **사용 안 함**으로 설정할 수 있습니다. 서버를 여러 번 재부팅할 경우 이렇게 설정하면 통상 시작되는 서비스가 시작되지 않도록 하여 시간을 절약할 수 있습니다.

    > [!NOTE]
    > 이러한 속성과 기타 속성을 서비스가 설치된 후 변경할 수 있습니다.

    <xref:System.ServiceProcess.ServiceInstaller.StartType%2A> 프로세스가 **수동**으로 설정된 서비스를 시작하는 방법은 **서버 탐색기**, **Windows 서비스 제어 관리자**, 코드 등 여러 가지가 있습니다. 이러한 방법 중 일부는 실제로 **서비스 제어 관리자**의 컨텍스트에서 서비스를 시작하지 않습니다. **서버 탐색기** 및 서비스를 시작하는 프로그래밍 방법은 실제로 컨트롤러를 조작합니다.

### <a name="to-manually-start-a-service-from-server-explorer"></a>서버 탐색기에서 서비스를 수종으로 시작하려면

1. **서버 탐색기**에서 원하는 서버가 아직 나열되지 않는 경우 추가합니다. 자세한 내용은 방법: 서버 탐색기/데이터베이스 탐색기 액세스 및 초기화를 참조하세요.

2. **서비스** 노드를 확장한 다음 시작할 서비스를 찾습니다.

3. 서비스 이름을 마우스 오른쪽 단추로 클릭하고 **시작**을 클릭합니다.

### <a name="to-manually-start-a-service-from-services-control-manager"></a>서비스 제어 관리자에서 서비스를 수동으로 시작하려면

1. 다음 중 하나를 수행하여 **서비스 제어 관리자**를 엽니다.

    - Windows XP 및 2000 Professional의 경우 바탕 화면에서 **내 컴퓨터**를 마우스 오른쪽 단추로 클릭한 다음, **관리**를 클릭합니다. 대화 상자가 나타나면 **서비스 및 애플리케이션** 노드를 확장합니다.

      \- 또는 -

    - Windows Server 2003 및 Windows 2000 Server에서 **시작**을 클릭하여 **프로그램**을 가리키고 **관리 도구**를 클릭한 다음, **서비스**를 클릭합니다.

      > [!NOTE]
      > Windows NT 버전 4.0의 경우 **제어판**에서 이 대화 상자를 열 수 있습니다.

    이제 창의 **서비스** 섹션에 서비스가 나타납니다.

2. 목록에서 서비스를 선택하고 마우스 오른쪽 단추로 클릭한 다음, **시작**을 클릭합니다.

### <a name="to-manually-start-a-service-from-code"></a>코드에서 서비스를 수동으로 시작하려면

1. <xref:System.ServiceProcess.ServiceController> 클래스의 인스턴스를 만들고 관리할 서비스와 상호 작용하도록 구성합니다.

2. <xref:System.ServiceProcess.ServiceController.Start%2A> 메서드를 호출하여 서비스를 시작합니다.

## <a name="see-also"></a>참고 항목

- [Windows 서비스 애플리케이션 소개](introduction-to-windows-service-applications.md)
- [방법: Windows 서비스 만들기](how-to-create-windows-services.md)
- [방법: 서비스 애플리케이션에 설치 관리자 추가](how-to-add-installers-to-your-service-application.md)
