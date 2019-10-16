---
title: '방법: 관리형 애플리케이션에서 WCF 서비스 호스트'
ms.date: 09/17/2018
dev_langs:
- csharp
- vb
ms.assetid: 5eb29db0-b6dc-4e77-8c68-0a62f79d743b
ms.openlocfilehash: b6d1c9c38e2cc5f1b1b7b5538af0339987563de6
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65637587"
---
# <a name="how-to-host-a-wcf-service-in-a-managed-app"></a>방법: 관리 되는 앱에서 WCF 서비스 호스팅

관리되는 애플리케이션 내에서 서비스를 호스팅하려면 관리되는 애플리케이션 코드 내에 서비스에 대한 코드를 포함하고, 코드에서 명령적으로, 구성을 통해 선언적으로 또는 기본 엔드포인트를 사용해 서비스에 대한 엔드포인트를 정의한 다음 <xref:System.ServiceModel.ServiceHost>의 인스턴스를 만듭니다.

메시지 받기를 시작하려면 <xref:System.ServiceModel.ICommunicationObject.Open%2A>에서 <xref:System.ServiceModel.ServiceHost>을 호출합니다. 이렇게 하면 서비스에 대한 수신기가 만들어지고 열립니다. 관리되는 응용 프로그램이 호스팅 작업을 직접 수행하므로 이런 방식으로 서비스를 호스팅하는 것을 "자체 호스팅"이라고 합니다. 서비스를 닫으려면 <xref:System.ServiceModel.Channels.CommunicationObject.Close%2A?displayProperty=nameWithType>에서 <xref:System.ServiceModel.ServiceHost>를 호출합니다.

서비스는 관리되는 Windows 서비스, IIS(인터넷 정보 서비스) 또는 WAS(Windows Process Activation Service)에서 호스팅될 수도 있습니다. 호스팅 서비스에 대 한 옵션에 대 한 자세한 내용은 참조 하세요. [호스팅 서비스](../../../docs/framework/wcf/hosting-services.md)합니다.

관리되는 애플리케이션에서 서비스를 호스팅할 경우 최소한의 배포 인프라를 필요로 하기 때문에 가장 유연한 옵션입니다. 관리 되는 응용 프로그램에서 서비스를 호스트 하는 방법에 대 한 자세한 내용은 참조 하세요. [관리 되는 응용 프로그램에서 호스팅](../../../docs/framework/wcf/feature-details/hosting-in-a-managed-application.md)합니다.

다음 절차에서는 콘솔 애플리케이션에서 자체 호스팅된 서비스를 구현하는 방법을 보여 줍니다.

## <a name="create-a-self-hosted-service"></a>자체 호스팅된 서비스 만들기

1. 새 콘솔 응용 프로그램을 만듭니다.

   1. Visual Studio를 열고 선택 **새로 만들기** > **프로젝트** 에서 합니다 **파일** 메뉴.

   2. 에 **설치 된 템플릿** 목록에서 **Visual C#** 또는 **Visual Basic**를 선택한 후 **Windows Desktop**합니다.

   3. 선택 된 **콘솔 앱** 템플릿. 형식 `SelfHost` 에 **이름** 확인란을 선택한 다음 **확인**합니다.

2. 마우스 오른쪽 단추로 클릭 **SelfHost** 에 **솔루션 탐색기** 선택한 **참조 추가**합니다. 선택 **System.ServiceModel** 에서 합니다 **.NET** 탭을 선택한 다음 **확인**합니다.

    > [!TIP]
    > 경우는 **솔루션 탐색기** 창이 표시, 선택 되지 않으면 **솔루션 탐색기** 에서 합니다 **뷰** 메뉴.

3. 두 번 클릭 **Program.cs** 하거나 **Module1.vb** 에서 **솔루션 탐색기** 열려 있지 않으면 코드 창에서 엽니다. 파일의 맨 위에 다음 문을 추가 합니다.

     [!code-csharp[CFX_SelfHost4#1](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_selfhost4/cs/program.cs#1)]
     [!code-vb[CFX_SelfHost4#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/cfx_selfhost4/vb/module1.vb#1)]

4. 서비스 계약을 정의 및 구현합니다. 이 예제에서는 서비스에 대한 입력을 기준으로 메시지를 반환하는 `HelloWorldService`를 정의합니다.

     [!code-csharp[CFX_SelfHost4#2](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_selfhost4/cs/program.cs#2)]
     [!code-vb[CFX_SelfHost4#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/cfx_selfhost4/vb/module1.vb#2)]

    > [!NOTE]
    > 정의 및 서비스 인터페이스를 구현 하는 방법에 대 한 자세한 내용은 참조 하세요. [방법: 서비스 계약을 정의](../../../docs/framework/wcf/how-to-define-a-wcf-service-contract.md) 고 [방법: 서비스 계약을 구현](../../../docs/framework/wcf/how-to-implement-a-wcf-contract.md)합니다.

5. 서비스의 기본 주소를 사용하여 `Main` 메서드 맨 위에 <xref:System.Uri> 클래스의 인스턴스를 만듭니다.

     [!code-csharp[CFX_SelfHost4#3](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_selfhost4/cs/program.cs#3)]
     [!code-vb[CFX_SelfHost4#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/cfx_selfhost4/vb/module1.vb#3)]

6. <xref:System.ServiceModel.ServiceHost> 클래스의 인스턴스를 만들어 서비스 형식 및 기본 주소 URI(Uniform Resource Identifier)를 나타내는 <xref:System.Type>을 <xref:System.ServiceModel.ServiceHost.%23ctor%28System.Type%2CSystem.Uri%5B%5D%29>에 전달합니다. 메타데이터 게시를 사용하도록 설정한 다음 <xref:System.ServiceModel.ICommunicationObject.Open%2A>에서 <xref:System.ServiceModel.ServiceHost> 메서드를 호출하여 서비스를 초기화하고 메시지를 받도록 서비스를 준비합니다.

     [!code-csharp[CFX_SelfHost4#4](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_selfhost4/cs/program.cs#4)]
     [!code-vb[CFX_SelfHost4#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/cfx_selfhost4/vb/module1.vb#4)]

    > [!NOTE]
    > 이 예제에서는 기본 엔드포인트를 사용하며, 이 서비스에는 구성 파일이 필요하지 않습니다. 엔드포인트를 구성하지 않으면 런타임이 서비스에서 구현되는 각 서비스 계약의 각 기본 주소에 대해 엔드포인트를 하나씩 만듭니다. 기본 끝점에 대 한 자세한 내용은 참조 하세요. [Simplified Configuration](../../../docs/framework/wcf/simplified-configuration.md) 하 고 [Simplified Configuration for WCF Services](../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md)합니다.

7. 키를 눌러 **Ctrl**+**Shift**+**B** 솔루션을 빌드합니다.

## <a name="test-the-service"></a>서비스 테스트

1. 키를 눌러 **Ctrl**+**F5** 서비스를 실행 합니다.

2. 오픈 **WCF 테스트 클라이언트**합니다.

    > [!TIP]
    > 열려는 **WCF 테스트 클라이언트**, Visual Studio 용 개발자 명령 프롬프트를 열고 및 실행 **WcfTestClient.exe**합니다.

3. 선택 **추가 서비스** 에서 합니다 **파일** 메뉴.

4. 형식 `http://localhost:8080/hello` 주소 상자에 클릭 **확인**합니다.

    > [!TIP]
    > 서비스가 실행 중인지 확인하십시오. 그렇지 않으면 이 단계는 실패합니다. 코드에서 기본 주소를 변경한 경우에는 이 단계에서 수정된 기본 주소를 사용하십시오.

5. 두 번 클릭 **SayHello** 아래의 합니다 **내 서비스 프로젝트** 노드. 에 사용자 이름을 입력 합니다 **값** 열에는 **요청** 목록 및 클릭 **Invoke**합니다.

   회신 메시지에 표시 합니다 **응답** 목록입니다.

## <a name="example"></a>예제

다음 예제에서는 <xref:System.ServiceModel.ServiceHost> 개체를 만들어 `HelloWorldService` 형식의 서비스를 호스팅한 다음 <xref:System.ServiceModel.ICommunicationObject.Open%2A>에서 <xref:System.ServiceModel.ServiceHost> 메서드를 호출합니다. 기본 주소는 코드에서 제공되고 메타데이터 게시가 사용하도록 설정되며 기본 엔드포인트가 사용됩니다.

[!code-csharp[CFX_SelfHost4#5](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_selfhost4/cs/program.cs#5)]
[!code-vb[CFX_SelfHost4#5](../../../samples/snippets/visualbasic/VS_Snippets_CFX/cfx_selfhost4/vb/module1.vb#5)]

## <a name="see-also"></a>참고자료

- <xref:System.Uri>
- <xref:System.Configuration.ConfigurationManager.AppSettings%2A>
- <xref:System.Configuration.ConfigurationManager>
- [방법: IIS에서 WCF 서비스 호스팅](../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-iis.md)
- [자체 호스팅](../../../docs/framework/wcf/samples/self-host.md)
- [서비스 호스팅](../../../docs/framework/wcf/hosting-services.md)
- [방법: 서비스 계약 정의](../../../docs/framework/wcf/how-to-define-a-wcf-service-contract.md)
- [방법: 서비스 계약 구현](../../../docs/framework/wcf/how-to-implement-a-wcf-contract.md)
- [ServiceModel Metadata 유틸리티 도구(Svcutil.exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)
- [바인딩을 사용하여 서비스 및 클라이언트 구성](../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)
- [시스템 제공 바인딩](../../../docs/framework/wcf/system-provided-bindings.md)
