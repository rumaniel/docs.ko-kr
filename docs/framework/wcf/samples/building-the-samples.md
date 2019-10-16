---
title: Windows Communication Foundation 샘플 빌드
ms.date: 03/30/2017
ms.assetid: 2899e7a5-9cb2-4e8d-b8d2-f31391549198
ms.openlocfilehash: 021f17778bc019828d00fbd8e93cbc319de3047a
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70990147"
---
# <a name="building-the-windows-communication-foundation-samples"></a>Windows Communication Foundation 샘플 빌드

WCF (Windows Communication Foundation) 샘플은 Visual Studio IDE를 사용 하거나 명령줄에서 **msbuild** 명령을 사용 하 여 빌드할 수 있습니다. 이 항목에서는 이 두 절차를 모두 설명합니다.

> [!NOTE]
> WCF 샘플을 빌드하거나 실행 하기 전에 [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)를 수행 했는지 확인 합니다.

## <a name="to-build-the-sample-using-a-command-prompt"></a>명령 프롬프트를 사용하여 샘플을 빌드하려면

1. Visual Studio에 대 한 개발자 명령 프롬프트를 열고 샘플을 설치한 디렉터리 위치 아래의 언어별 하위 디렉터리로 이동 합니다.

2. 명령줄 `msbuild` 에를 입력 합니다. 클라이언트 프로그램 파일은 *client\bin* 에 빌드되고 서비스 프로그램 파일은 *service\bin*에 빌드됩니다. 인터넷 정보 서비스 (IIS)에서 서비스를 호스팅하는 경우 서비스 프로그램 파일도 *servicemodelsamples* 디렉터리와 *\bin* 하위 디렉터리에 복사 됩니다.

> [!NOTE]
> *%Systemdrive%\inetpub\wwwroot* 에서 acl을 설정 하 여를 실행 하는 계정에 대 한 수정 권한을 부여 해야 합니다. 그러지 않으면 일부 빌드 후 이벤트가 실패합니다. 또는 ACL을 그대로 두고 관리자로 SDK 명령 프롬프트를 실행할 수도 있습니다.

## <a name="to-build-the-sample-using-visual-studio"></a>Visual Studio를 사용하여 샘플을 빌드하려면

1. Visual Studio의 **파일** 메뉴에서**프로젝트/솔루션** **열기** > 를 선택 합니다. 샘플을 설치한 디렉터리 아래의 언어별 하위 디렉터리로 이동 하 고 .sln 파일 아이콘을 두 번 클릭 하 여 Visual Studio에서 솔루션을 엽니다.

1. **빌드** 메뉴에서 **솔루션 다시 빌드**를 선택 합니다.

   클라이언트 프로그램 파일이 client\bin에 빌드되고 서비스 프로그램 파일이 service\bin에 빌드됩니다. 서비스가 IIS에서 호스트 되는 경우 서비스 프로그램 파일도 *servicemodelsamples* 디렉터리와 *\bin* 하위 디렉터리에 복사 됩니다.

> [!NOTE]
> 실행에 사용하는 계정에 수정 권한을 부여하도록 %systemdrive%\inetpub\wwwroot의 ACL을 설정해야 합니다. 그러지 않으면 일부 빌드 후 이벤트가 실패합니다. 또는 ACL을 그대로 두고 관리자로 SDK 명령 프롬프트 또는 Visual Studio를 실행할 수도 있습니다. ASP.NET 작업자 프로세스에 디버거를 연결하는 등의 일부 Visual Studio 작업을 수행하는 데에도 관리자 권한이 필요합니다.

## <a name="setup-batch-files-and-scripts"></a>배치 파일 및 스크립트 설치
 Setup.exe 및 정리가 배치 파일 및 스크립트는 Visual Studio 용 개발자 명령 프롬프트에서 실행 해야 합니다. 일부 설치 및 정리 파일은 관리자 권한이 필요한 작업을 수행하므로 관리자 권한으로 실행해야 합니다.

## <a name="important-security-information-about-metadata-endpoints"></a>메타데이터 엔드포인트에 대한 중요한 보안 정보
 잠재적으로 중요 한 서비스 메타 데이터가 실수로 공개 되지 않도록 하기 위해 WCF (Windows Communication Foundation) 서비스의 기본 구성에서는 메타 데이터 게시를 사용 하지 않도록 설정 합니다. 이 동작은 기본적으로 안전하지만 구성에서 서비스의 메타데이터 게시 동작이 명시적으로 사용하도록 설정되어 있지 않은 경우 Svcutil.exe 등의 메타데이터 가져오기 도구를 사용하여 서비스를 호출하는 데 필요한 클라이언트 코드를 생성할 수 없습니다. 샘플로 보다 쉽게 작업할 수 있도록 거의 모든 샘플에서는 보안되지 않은 메타데이터 게시 엔드포인트를 노출합니다. 이러한 엔드포인트는 인증되지 않은 익명의 소비자가 사용할 수 있으므로 이러한 엔드포인트를 배포하기 전에 서비스의 메타데이터를 공개하는 것이 적절한지 주의를 기울여야 합니다. 서비스 메타 데이터 게시에 대 한 자세한 내용은 [메타 데이터 게시 동작](../../../../docs/framework/wcf/samples/metadata-publishing-behavior.md) 샘플을 참조 하세요. 메타 데이터 끝점에 보안을 설정 하는 샘플은 [사용자 지정 보안 메타 데이터 끝점](../../../../docs/framework/wcf/samples/custom-secure-metadata-endpoint.md) 샘플을 참조 하세요.

## <a name="exception-handling"></a>예외 처리
 일반적으로 이러한 샘플에는 코드가 샘플의 주제 위주로 작동하도록 예외 처리가 포함되어 있지 않습니다. 예외 처리에 대 한 자세한 내용은 예상 된 [예외](../../../../docs/framework/wcf/samples/expected-exceptions.md) 샘플을 참조 하세요.

## <a name="regenerating-clients-and-configuration-with-svcutil"></a>Svcutil을 사용하여 클라이언트 및 구성 다시 생성
 [ServiceModel Metadata 유틸리티 도구 (svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 를 사용 하 여 대부분의 샘플에 대 한 클라이언트 코드 및 구성을 다시 생성할 수 있습니다. 일부 샘플에서는 구성을 수동으로 편집해야 합니다. 예를 들어, Svcutil.exe를 사용하여 클라이언트 인증서 자격 증명을 사용하는 샘플의 구성을 다시 생성하는 경우 이전에 구성된 자격 증명을 수동으로 지정해야 합니다. 일부 샘플에서는 생성된 코드에 영향을 주기 위해 특정 Svcutil.exe 옵션을 사용하며, 이러한 옵션은 특정 샘플 항목에 지정되어 있습니다.

### <a name="to-regenerate-the-client-and-configuration-files"></a>클라이언트 및 구성 파일을 다시 생성하려면

1. SDK 명령 프롬프트를 열고 샘플을 설치한 디렉터리 위치 아래의 언어별 하위 디렉터리로 이동합니다.

2. 웹 호스팅 서비스의 경우 다음 명령을 사용합니다.

    ```console
    svcutil.exe /n:"http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples" http://localhost/servicemodelsamples/service.svc/mex /out:generatedClient.cs
    ```

     자체 호스팅 서비스의 경우 다음 명령을 입력합니다.

    ```console
    svcutil.exe /n:"http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples" http://localhost:8000/servicemodelsamples/service.svc/mex /out:generatedClient.cs
    ```

     을 `http://localhost:8000/ServiceModelSamples/service.svc/mex` 자체 호스팅 서비스의 mex 끝점 주소로 바꿉니다.

     Visual Basic 형식에서 클라이언트를 생성하려면 다음 명령을 사용합니다.

    ```console
    svcutil.exe /n:"http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples" http://localhost/servicemodelsamples/service.svc/mex /l:vb /out:generatedClient.vb
    ```

     자체 호스팅 서비스의 경우 다음 명령을 사용합니다.

    ```console
    svcutil.exe /n:"http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples" http://localhost:8000/servicemodelsamples/service.svc/mex /l:vb /out:generatedClient.vb
    ```

    > [!NOTE]
    > 클라이언트 구성의 생성을 건너뛰려면 **/Noconfig** 옵션을 추가 합니다.

## <a name="see-also"></a>참고자료

- [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)
- [ServiceModel Metadata 유틸리티 도구(Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)
