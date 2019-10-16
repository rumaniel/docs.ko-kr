---
title: Custom Binding Security
ms.date: 03/30/2017
ms.assetid: a6383dff-4308-46d2-bc6d-acd4e18b4b8d
ms.openlocfilehash: b0b293c58e13f7add6f2cb49ea3c108a86292691
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70990004"
---
# <a name="custom-binding-security"></a>Custom Binding Security

이 샘플에서는 사용자 지정 바인딩을 사용하여 보안을 구성하는 방법을 보여 줍니다. 여기서는 사용자 지정 바인딩을 사용하여 메시지를 안전하게 전송하고 메시지 수준 보안을 가능하게 하는 방법을 보여 줍니다. 이러한 방법은 클라이언트와 서비스 간에 메시지를 전송하는 데 보안 전송이 요구되면서 동시에 메시지가 메시지 수준에서 보호되어야 하는 경우에 유용합니다. 이 구성은 시스템 제공 바인딩에서는 지원되지 않습니다.

이 샘플은 클라이언트 콘솔 프로그램(EXE) 및 서비스 콘솔 프로그램(EXE)으로 구성됩니다. 서비스는 이중 계약을 구현합니다. 계약은 수학 연산(Add, Subtract, Multiply 및 Divide)을 노출시키는 `ICalculatorDuplex` 인터페이스에 의해 정의됩니다. `ICalculatorDuplex` 인터페이스를 사용하여 클라이언트는 수학 연산을 수행하고 세션 도중 실행 결과를 계산할 수 있습니다. 서비스는 독립적으로 `ICalculatorDuplexCallback` 인터페이스에서 결과를 반환할 수 있습니다. 클라이언트와 서비스 간에 전송되는 메시지 집합을 서로 연결하기 위해 컨텍스트를 설정해야 하므로 이중 계약에는 세션이 필요합니다. 이중 통신을 지원하는 보안된 사용자 지정 바인딩이 정의됩니다.

> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.

서비스 구성에서는 다음을 지원하는 사용자 지정 바인딩을 정의합니다.

- TLS/SSL 프로토콜을 사용하여 보호되는 TCP 통신

- Windows 메시지 보안

사용자 지정 바인딩 구성은 메시지 수준 보안을 동시에 사용하도록 하여 보안 전송을 가능하게 합니다. 바인딩 요소의 순서는 사용자 지정 바인딩을 정의 하는 데 중요 합니다. 각는 채널 스택의 계층을 나타냅니다 ( [사용자 지정 바인딩](../../../../docs/framework/wcf/extending/custom-bindings.md)참조). 다음 샘플 구성과 같이 사용자 지정 바인딩은 서비스 및 클라이언트 구성 파일에 정의합니다.

```xml
<bindings>
  <!-- Configure a custom binding. -->
  <customBinding>
    <binding name="Binding1">
      <security authenticationMode="SecureConversation"
                 requireSecurityContextCancellation="true">
      </security>
      <textMessageEncoding messageVersion="Soap12WSAddressing10" writeEncoding="utf-8"/>
      <sslStreamSecurity requireClientCertificate="false"/>
      <tcpTransport/>
    </binding>
  </customBinding>
</bindings>
```

사용자 지정 바인딩은 서비스 인증서를 사용하여 전송 수준에서 서비스를 인증하고 클라이언트와 서비스 간 전송 시 메시지를 보호합니다. 이러한 작업은 `sslStreamSecurity` 바인딩 요소에 의해 수행됩니다. 다음 샘플 구성과 같이 서비스의 인증서는 서비스 동작을 사용하여 구성됩니다.

```xml
<behaviors>
    <serviceBehaviors>
    <behavior name="CalculatorServiceBehavior">
        <serviceMetadata />
        <serviceDebug includeExceptionDetailInFaults="False" />
        <serviceCredentials>
        <serviceCertificate findValue="localhost" storeLocation="LocalMachine" storeName="My" x509FindType="FindBySubjectName"/>
        </serviceCredentials>
    </behavior>
    </serviceBehaviors>
</behaviors>
```

또한 사용자 지정 바인딩은 기본 자격 증명 형식인 Windows 자격 증명 형식의 메시지 보안을 사용합니다. 이러한 작업은 `security` 바인딩 요소에 의해 수행됩니다. Kerberos 인증 메커니즘이 사용 가능한 경우 클라이언트 및 서비스는 모두 메시지 수준 보안을 사용하여 인증됩니다. Active Directory 환경에서 샘플이 실행될 경우 이 방법이 사용됩니다. Kerberos 인증 메커니즘을 사용할 수 없는 경우에는 NTLM 인증이 사용됩니다. NTLM은 서비스에 대해 클라이언트를 인증하지만 클라이언트에 대해 서비스를 인증하지는 않습니다. `security` 바인딩 요소는 `SecureConversation` `authenticationType`을 사용하도록 구성됩니다. 이렇게 하면 클라이언트와 서비스 모두에 보안 세션이 만들어집니다. 이러한 구성은 서비스의 이중 계약을 사용할 때 필요합니다.

샘플을 실행하면 작업 요청 및 응답이 클라이언트 콘솔 창에 표시됩니다. 클라이언트를 종료하려면 클라이언트 창에서 Enter 키를 누릅니다.

```console
Press <ENTER> to terminate client.
Result(100)
Result(50)
Result(882.5)
Result(441.25)
Equation(0 + 100 - 50 * 17.65 / 2 = 441.25)
```

샘플을 실행하면 서비스에서 전송된 콜백 인터페이스에서 클라이언트에 반환된 메시지를 볼 수 있습니다. 각 중간 결과가 표시된 다음 모든 작업이 완료되면 전체 수식이 표시됩니다. 클라이언트를 종료하려면 Enter 키를 누릅니다.

포함된 Setup.bat 파일을 사용하면 인증서 기반 보안이 필요한 호스팅된 응용 프로그램을 실행하도록 관련 서비스 인증서가 있는 클라이언트와 서버를 구성할 수 있습니다. 다중 컴퓨터 구성이나 호스트되지 않는 환경에서 이 배치 파일을 사용하려면 배치 파일을 수정해야 합니다.

다음 부분에는 이 샘플에 적용되는 배치 파일을 적절한 구성에서 실행하도록 수정하는 데 도움이 되는 여러 관련 단원의 간략한 개요가 소개되어 있습니다.

- 서버 인증서 만들기

  Setup.bat 파일에서 다음 줄은 사용할 서버 인증서를 만듭니다. `%SERVER_NAME%`변수는 서버 이름을 지정합니다. 이 변수를 변경하여 고유의 서버 이름을 지정합니다. 이 배치 파일에서 서버 이름의 기본값은 localhost입니다.

  인증서는 웹 호스팅 서비스에 대한 CurrentUser 저장소에 저장됩니다.

  ```bat
  echo ************
  echo Server cert setup starting
  echo %SERVER_NAME%
  echo ************
  echo making server cert
  echo ************
  makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe
  ```

- 클라이언트의 신뢰할 수 있는 인증서 저장소에 서버 인증서 설치

  Setup.bat 파일에서 다음 줄은 클라이언트의 신뢰할 수 있는 사용자 저장소로 서버 인증서를 복사합니다. 이 단계는 Makecert.exe에서 생성한 인증서를 클라이언트 컴퓨터에서 절대적으로 신뢰하지는 않기 때문에 필요합니다. Microsoft에서 발급한 인증서와 같이 클라이언트가 신뢰할 수 있는 루트 인증서를 기반으로 하는 인증서가 이미 있는 경우 클라이언트 인증서 저장소를 서버 인증서로 채우는 이 단계를 수행할 필요가 없습니다.

  ```console
  certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople
  ```

  > [!NOTE]
  > Setup.bat 배치 파일은 Visual Studio 2010 명령 프롬프트에서 실행되도록 디자인되었습니다. MSSDK 환경 변수는 SDK가 설치되는 디렉터리를 가리켜야 합니다. 이 환경 변수는 Visual Studio 2010 명령 프롬프트 내에서 자동으로 설정됩니다.

### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면

1. [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.

2. C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.

3. 단일 컴퓨터 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)의 지침을 따르세요.

### <a name="to-run-the-sample-on-the-same-computer"></a>단일 컴퓨터 구성에서 샘플을 실행하려면

1. 관리자 권한으로 Visual Studio 창에 대 한 개발자 명령 프롬프트를 열고 샘플 설치 폴더에서 Setup.exe를 실행 합니다. 이 작업은 샘플 실행에 필요한 모든 인증서를 설치합니다.

    > [!NOTE]
    > 설치 .bat 배치 파일은 Visual Studio 2012 명령 프롬프트에서 실행 되도록 디자인 되었습니다. Visual Studio 2012 명령 프롬프트 내에서 설정 된 PATH 환경 변수는 Setup. .bat 스크립트에 필요한 실행 파일을 포함 하는 디렉터리를 가리킵니다.

2. \service\bin에서 Service.exe를 실행합니다.

3. \client\bin에서 Client.exe를 실행합니다. 클라이언트 콘솔 애플리케이션에 클라이언트 동작이 표시됩니다.

4. 클라이언트와 서비스가 통신할 수 없는 경우 [WCF 샘플에 대 한 문제 해결 팁](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))을 참조 하세요.

### <a name="to-run-the-sample-across-computers"></a>다중 컴퓨터 구성에서 샘플을 실행하려면

1. 서비스 컴퓨터에서 다음을 수행합니다.

    1. 서비스 컴퓨터에서 servicemodelsamples라는 가상 디렉터리를 만듭니다.

    2. \inetpub\wwwroot\servicemodelsamples에서 서비스 컴퓨터의 가상 디렉터리로 서비스 프로그램 파일을 복사합니다. \bin 하위 디렉터리에 파일을 복사해야 합니다.

    3. Setup.bat 및 Cleanup.bat 파일을 서비스 컴퓨터로 복사합니다.

    4. 관리자 권한 `Setup.bat service`으로 연 Visual Studio 용 개발자 명령 프롬프트에서 다음 명령을 실행 합니다. 이렇게 하면 배치 파일이 실행된 컴퓨터의 이름과 일치하는 주체 이름을 가진 서비스 인증서가 만들어집니다.

        > [!NOTE]
        > Setup.bat 배치 파일은 Visual Studio 2010 명령 프롬프트에서 실행되도록 디자인되었습니다. PATH 환경 변수는 SDK가 설치되는 디렉터리를 가리켜야 합니다. 이 환경 변수는 Visual Studio 2010 명령 프롬프트 내에서 자동으로 설정됩니다.

    5. 이전 단계에서 생성 된 인증서의 주체 이름을 반영 하도록 [ serviceCertificate파일내에서>를변경합니다.\<](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md)

    6. 명령 프롬프트에서 Service.exe를 실행합니다.

2. 클라이언트 컴퓨터에서 다음을 수행합니다.

    1. \client\bin\ 폴더에서 클라이언트 컴퓨터로 클라이언트 프로그램 파일을 복사합니다. Cleanup.bat 파일도 복사합니다.

    2. Cleanup.bat를 실행하여 이전 샘플에서 이전의 모든 인증서를 제거합니다.

    3. 관리자 권한으로 Visual Studio에 대 한 개발자 명령 프롬프트를 열고 서비스 컴퓨터에서 다음 명령을 실행 하 여 서비스의 인증서를 내보냅니다 (여기서는 `%SERVER_NAME%` 컴퓨터의 정규화 된 이름으로 대체 합니다. 서비스가 실행 되 고 있습니다.):

        ```console
        certmgr -put -r LocalMachine -s My -c -n %SERVER_NAME% %SERVER_NAME%.cer
        ```

    4. %SERVER_NAME%.cer을 클라이언트 컴퓨터에 복사합니다. %SERVER_NAME%은 서비스가 실행되고 있는 컴퓨터의 정규화된 이름으로 바꿉니다.

    5. 관리자 권한으로 Visual Studio에 대 한 개발자 명령 프롬프트를 열고 클라이언트 컴퓨터에서 다음 명령을 실행 하 여 서비스의 인증서를 가져옵니다 (%% s '을 (를) 사용 하는 컴퓨터의 정규화 된 이름으로 바꿉니다. 서비스가 실행 되 고 있습니다.):

        ```console
        certmgr.exe -add -c %SERVER_NAME%.cer -s -r CurrentUser TrustedPeople
        ```

        신뢰할 수 있는 발급자에 의해 인증서가 발급된 경우 c, d 및 e 단계는 필요하지 않습니다.

    6. 클라이언트의 App.config 파일을 다음과 같이 수정합니다.

        ```xml
        <client>
            <endpoint name="default"
                address="net.tcp://ReplaceThisWithServiceMachineName:8000/ServiceModelSamples/Service"
                binding="customBinding"
                bindingConfiguration="Binding1"
                contract="Microsoft.ServiceModel.Samples.ICalculatorDuplex"
                behaviorConfiguration="CalculatorClientBehavior" />
        </client>
        ```

    7. 도메인 환경에서 NetworkService 또는 LocalSystem 계정이 아닌 계정으로 서비스가 실행 중이면 서비스를 실행하는 데 사용되는 해당 계정에 기초하여 적절한 UPN 또는 SPN을 설정하기 위해 클라이언트의 App.config 파일에서 서비스 엔드포인트에 대한 엔드포인트 ID를 수정해야 할 수 있습니다. 끝점 id에 대 한 자세한 내용은 [서비스 id 및 인증](../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md) 항목을 참조 하세요.

    8. 명령 프롬프트에서 Client.exe를 실행합니다.

### <a name="to-clean-up-after-the-sample"></a>샘플 실행 후 정리를 수행하려면

- 샘플 실행을 완료한 후 샘플 폴더에서 Cleanup.bat를 실행합니다.
