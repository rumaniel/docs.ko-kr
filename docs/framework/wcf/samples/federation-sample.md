---
title: Federation 샘플
ms.date: 03/30/2017
ms.assetid: 7e9da0ca-e925-4644-aa96-8bfaf649d4bb
ms.openlocfilehash: d3a326f08e78edb79908485361f161c1b6da6625
ms.sourcegitcommit: 581ab03291e91983459e56e40ea8d97b5189227e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2019
ms.locfileid: "70044973"
---
# <a name="federation-sample"></a>Federation 샘플
이 샘플에서는 연결된 보안을 보여 줍니다.  
  
## <a name="sample-details"></a>샘플 세부 정보  
 WCF (Windows Communication Foundation)는을 `wsFederationHttpBinding`통해 페더레이션 보안 아키텍처를 배포 하기 위한 지원을 제공 합니다. `wsFederationHttpBinding`에서는 요청/회신 통신의 기본 전송 메커니즘으로 HTTP를 사용하고, 인코딩 통신 형식으로 텍스트/XML을 사용하는, 안전하고 안정적이며 상호 운용 가능한 바인딩을 제공합니다. WCF의 페더레이션에 대 한 자세한 내용은 [페더레이션](../../../../docs/framework/wcf/feature-details/federation.md)을 참조 하세요.  
  
 이 시나리오는 네 부분으로 구성되어 있습니다.  
  
- BookStore 서비스  
  
- BookStore STS  
  
- HomeRealm STS  
  
- BookStore 클라이언트  
  
 BookStore 서비스는 `BrowseBooks`와 `BuyBook`의 두 작업을 지원합니다. `BrowseBooks` 작업에 대해서는 익명 액세스를 허용하지만, `BuyBooks` 작업에 액세스하려면 인증 액세스가 필요합니다. 인증은 BookStore STS에서 발급한 토큰의 형태로 이루어집니다. BookStore 서비스의 구성 파일은 `wsFederationHttpBinding`을 사용하여 클라이언트를 BookStore STS로 연결합니다.  
  
```xml  
<wsFederationHttpBinding>  
<!-- This is the Service binding for the BuyBooks endpoint. It redirects clients to the BookStore STS -->  
    <binding name='BuyBookBinding'>  
        <security mode="Message">  
            <message>  
                <issuerMetadata  
  address='http://localhost/FederationSample/BookStoreSTS/STS.svc/mex' >  
                    <identity>  
                        <dns value ='BookStoreSTS.com'/>  
                    </identity>  
                </issuerMetadata>  
            </message>  
        </security>  
    </binding>  
</wsFederationHttpBinding>  
```  
  
 그러면 BookStore STS는 클라이언트에게 HomeRealm STS에서 발급한 토큰을 사용하여 인증하도록 지시합니다. BookStore STS의 구성 파일도 `wsFederationHttpBinding`을 사용하여 클라이언트를 HomeRealm STS로 연결합니다.  
  
```xml  
<wsFederationHttpBinding>  
 <!-- This is the binding for the clients requesting tokens from this STS. It redirects clients to the HomeRealm STS -->  
    <binding name='BookStoreSTSBinding'>  
        <security mode='Message'>  
            <message>  
                <issuerMetadata  
 address='http://localhost/FederationSample/HomeRealmSTS/STS.svc/mex' >  
                    <identity>  
                        <dns value ='HomeRealmSTS.com' />  
                    </identity>  
                </issuerMetadata>  
            </message>  
        </security>  
    </binding>  
</wsFederationHttpBinding>  
```  
  
 `BuyBook` 작업에 액세스할 때의 이벤트 순서는 다음과 같습니다.  
  
1. 클라이언트는 Windows 자격 증명을 사용하여 HomeRealm STS에 대해 인증합니다.  
  
2. HomeRealm STS는 BookStore STS에 대한 인증에 사용할 수 있는 토큰을 발급합니다.  
  
3. 클라이언트는 HomeRealm STS에서 발급한 토큰을 사용하여 BookStore STS에 대해 인증합니다.  
  
4. BookStore STS가 BookStore 서비스에 대한 인증에 사용할 수 있는 토큰을 발급합니다.  
  
5. 클라이언트는 BookStore STS에서 발급한 토큰을 사용하여 BookStore 서비스에 대해 인증합니다.  
  
6. 클라이언트가 `BuyBook` 작업에 액세스합니다.  
  
 이 샘플의 설치 및 실행 방법에 대해서는 다음 지침을 참조하십시오.  
  
> [!NOTE]
> 이 샘플을 실행 하려면 **wwwroot** 디렉터리에 대 한 쓰기 권한이 있어야 합니다.  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면  
  
1. SDK 명령 창을 엽니다. 샘플 경로에서 Setup.bat를 실행합니다. 그러면 샘플에 필요한 가상 디렉터리가 만들어지고 적절한 권한과 함께 필요한 인증서가 설치됩니다.  
  
    > [!NOTE]
    > Setup.bat 배치 파일은 Windows SDK 명령 프롬프트에서 실행되도록 디자인되었습니다. MSSDK 환경 변수는 SDK가 설치되는 디렉터리를 가리켜야 합니다. 이 환경 변수는 Windows SDK 명령 프롬프트 내에서 자동으로 설정됩니다. 설치에서 IIS 관리자 스크립트를 사용하므로 [!INCLUDE[wv](../../../../includes/wv-md.md)]에서 IIS 6.0 관리 호환성이 설치되었는지 확인해야 합니다. [!INCLUDE[wv](../../../../includes/wv-md.md)]에서 설치 스크립트를 실행하려면 관리자 권한이 필요합니다.  
  
2. Visual Studio에서 FederationSample을 열고 **빌드** 메뉴에서 **솔루션 빌드** 를 선택 합니다. 그러면 일반 프로젝트 파일, Bookstore 서비스, Bookstore STS 및 HomeRealm STS를 빌드하고 IIS에 배포합니다. 또한 Bookstore 클라이언트 애플리케이션도 빌드하며, BookStoreClient.exe 실행 파일을 FederationSample\BookStoreClient\bin\Debug 폴더에 배치합니다.  
  
3. BookStoreClient.exe를 두 번 클릭합니다. BookStoreClient 창이 표시됩니다.  
  
4. **찾아보기 서적**을 클릭 하면 서 면에서 사용할 수 있는 책을 찾아볼 수 있습니다.  
  
5. 특정 책을 구입 하려면 목록에서 책을 선택 하 고 **구매 서적**을 클릭 합니다. 애플리케이션이 시작되고 Windows 인증과 HomeRealm 보안 토큰 서비스를 사용하여 인증합니다.  
  
     이 샘플은 사용자가 가격이 $15 이하인 책을 구입할 수 있도록 구성되었습니다. $15보다 비싼 책을 구입하려고 하면 클라이언트는 Book Store 서비스로부터 액세스 거부 메시지를 받습니다.  
  
    > [!NOTE]
    > 이 샘플은 구입 후 사용자의 신용 한도를 업데이트하지 않습니다. 사용자의 (고정)신용 한도 내에서 책을 반복하여 구입할 수 있습니다.  
  
#### <a name="to-clean-up"></a>정리하려면  
  
1. Cleanup.bat를 실행합니다. 그러면 설치 과정에 만들어졌던 가상 디렉터리를 삭제하며 설치되었던 인증서도 제거합니다.  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WCF\Scenario\Federation`  
