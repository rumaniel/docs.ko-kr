---
title: '방법: WCF 활성화 구성 요소 설치 및 구성'
ms.date: 03/30/2017
helpviewer_keywords:
- HTTP activation [WCF]
ms.assetid: 33a7054a-73ec-464d-83e5-b203aeded658
ms.openlocfilehash: 70eab39e4bb24dfd1cdd6abc5216e50126ef1f4c
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972190"
---
# <a name="how-to-install-and-configure-wcf-activation-components"></a>방법: WCF 활성화 구성 요소 설치 및 구성

이 항목에서는의 [!INCLUDE[wv](../../../../includes/wv-md.md)] WAS (Windows Process Activation Service)를 HTTP 네트워크 프로토콜을 통해 통신 하지 않는 WCF (Windows Communication Foundation) 서비스에 설정 하는 데 필요한 단계에 대해 설명 합니다. 다음 단원에서는 이 구성 단계에 대해 간략히 설명합니다.

- WCF 활성화 구성 요소를 설치 하거나 설치를 확인 합니다.

- HTTP가 아닌 프로토콜을 지원하도록 WAS를 구성합니다. 다음 절차에서는 TCP 활성화를 위해 [!INCLUDE[wv](../../../../includes/wv-md.md)]를 구성합니다.

WAS를 설치 및 구성한 후에 [는 방법: Was를 활용 하는 HTTP](../../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-was.md) 가 아닌 끝점을 노출 하는 wcf 서비스를 만드는 절차를 위해에서 wcf 서비스를 호스팅합니다.

## <a name="to-install-the-wcf-non-http-activation-components"></a>WCF Non-HTTP Activation 구성 요소를 설치하려면

1. **시작** 단추를 클릭 한 다음 **제어판**을 클릭 합니다.

2. **프로그램**을 클릭 한 다음 **프로그램 및 기능**을 클릭 합니다.

3. **작업** 메뉴에서 **Windows 기능 사용/사용 안 함**을 클릭 합니다.

4. WinFX 노드를 찾아 선택한 다음 확장 합니다.

5. **WCF 비 Http 활성화 구성 요소** 상자를 선택 하 고 설정을 저장 합니다.

## <a name="to-configure-the-was-to-support-tcp-activation"></a>TCP 활성화를 지원하도록 WAS를 구성하려면

1. net.tcp 활성화를 지원하려면 먼저 기본 웹 사이트를 net.tcp 포트에 바인딩해야 합니다. IIS 7.0 관리 도구 집합과 함께 설치 되는 Appcmd.exe를 사용 하 여이 작업을 수행할 수 있습니다. 관리자 수준 명령 프롬프트 창에서 다음 명령을 실행합니다.

    ```console
    %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site" -+bindings.[protocol='net.tcp',bindingInformation='808:*']
    ```

    > [!NOTE]
    > 이 명령은 줄 바꿈 없이 한 줄로 입력해야 합니다. 이 명령은 임의의 호스트 이름을 사용하여 TCP 포트 808에서 수신 대기하는 기본 웹 사이트에 net.tcp 사이트 바인딩을 추가합니다.

2. 사이트 내의 모든 애플리케이션이 공통된 net.tcp 바인딩을 공유하지만 각 애플리케이션에서 개별적으로 net.tcp 지원을 사용하도록 설정할 수 있습니다. 애플리케이션에 대해 net.tcp를 사용하도록 설정하려면 관리자 수준 명령 프롬프트에서 다음 명령을 실행합니다.

    ```console
    %windir%\system32\inetsrv\appcmd.exe set app
    "Default Web Site/<WCF Application>" /enabledProtocols:http,net.tcp
    ```

    > [!NOTE]
    > 이 명령은 줄 바꿈 없이 한 줄로 입력해야 합니다. 이 명령을 사용 하면\< `http://localhost/<WCF Application>` 및`net.tcp://localhost/<WCF Application>`를 사용 하 여 응용*프로그램 > 응용 프로그램에*액세스할 수 있습니다.

     이 샘플에 대해 추가한 net.tcp 사이트 바인딩을 제거합니다.

     편의를 위해 다음 두 단계는 샘플 디렉터리에 있는 RemoveNetTcpSiteBinding.cmd라는 배치 파일에서 구현됩니다.

    1. 관리자 수준 명령 프롬프트 창에서 다음 명령을 실행하여 사용하도록 설정된 프로토콜 목록에서 net.tcp를 제거합니다.

        ```console
        %windir%\system32\inetsrv\appcmd.exe set app
        "Default Web Site/servicemodelsamples<WCF Application>" " /enabledProtocols:http
        ```

        > [!NOTE]
        > 이 명령은 줄 바꿈 없이 한 줄로 입력해야 합니다.

    2. 고급 명령 프롬프트 창에서 다음 명령을 실행하여 net.tcp 사이트 바인딩을 제거합니다.

        ```console
        %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site"
        --bindings.[protocol='net.tcp',bindingInformation='808:*']
        ```

        > [!NOTE]
        > 이 명령은 줄 바꿈 없이 한 줄로 입력해야 합니다.

## <a name="to-remove-nettcp-from-the-list-of-enabled-protocols"></a>사용하도록 설정된 프로토콜 목록에서 net.tcp를 제거하려면

1. 사용하도록 설정된 프로토콜 목록에서 net.tcp를 제거하려면 관리자 수준 명령 프롬프트 창에서 다음 명령을 실행합니다.

    ```console
    %windir%\system32\inetsrv\appcmd.exe set app "Default Web Site/servicemodelsamples<WCF Application>" " /enabledProtocols:http
    ```

    > [!NOTE]
    > 이 명령은 줄 바꿈 없이 한 줄로 입력해야 합니다.

## <a name="to-remove-the-nettcp-site-binding"></a>net.tcp 사이트 바인딩을 제거하려면

1. net.tcp 사이트 바인딩을 제거하려면 관리자 수준 명령 프롬프트 창에서 다음 명령을 실행합니다.

    ```console
    %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site"
    -bindings.[protocol='net.tcp',bindingInformation='808:*']
    ```

    > [!NOTE]
    > 이 명령은 줄 바꿈 없이 한 줄로 입력해야 합니다.

## <a name="see-also"></a>참고자료

- [TCP 활성화](../../../../docs/framework/wcf/samples/tcp-activation.md)
- [MSMQ 활성화](../../../../docs/framework/wcf/samples/msmq-activation.md)
- [NamedPipe 활성화](../../../../docs/framework/wcf/samples/namedpipe-activation.md)
- [Windows Server App Fabric 호스팅 기능](https://go.microsoft.com/fwlink/?LinkId=201276)
