---
title: '방법: SSL 인증서를 사용하여 포트 구성'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- SSL
- WCF, security mode
- WCF, security
ms.assetid: b8abcc8e-a5f5-4317-aca5-01e3c40ab24d
ms.openlocfilehash: 6e21311802b0a3ce4e415b14686b101d31f18035
ms.sourcegitcommit: 5ae5a1a9520b8b8b6164ad728d396717f30edafc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/11/2019
ms.locfileid: "70893305"
---
# <a name="how-to-configure-a-port-with-an-ssl-certificate"></a>방법: SSL 인증서를 사용하여 포트 구성
전송 보안을 사용 하는 <xref:System.ServiceModel.WSHttpBinding> 클래스를 사용 하 여 자체 호스팅 Windows Communication Foundation (WCF) 서비스를 만들 때 x.509 인증서를 사용 하 여 포트를 구성 해야 합니다. 자체 호스트된 서비스를 만들지 않는 경우에는 IIS(인터넷 정보 서비스)에서 서비스를 호스트할 수 있습니다. 자세한 내용은 [HTTP 전송 보안](../../../../docs/framework/wcf/feature-details/http-transport-security.md)을 참조 하세요.  
  
 포트를 구성하려면 컴퓨터에서 실행하는 운영 체제에 따라 다른 도구를 사용해야 합니다.  
  
 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 또는 [!INCLUDE[wxp](../../../../includes/wxp-md.md)]를 실행하는 경우 HttpCfg.exe 도구를 사용합니다. [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)]에는 이 도구가 함께 설치됩니다. 을 [!INCLUDE[wxp](../../../../includes/wxp-md.md)]사용 하 여 [Windows XP 서비스 팩 2 지원 도구](https://go.microsoft.com/fwlink/?LinkId=88606)에서이 도구를 다운로드할 수 있습니다. 자세한 내용은 [Httpcfg.exe 개요](https://go.microsoft.com/fwlink/?LinkId=88605)를 참조 하세요. [Windows 지원 도구 설명서](https://go.microsoft.com/fwlink/?LinkId=94840) 에서는 httpcfg.exe 도구에 대 한 구문을 설명 합니다.  
  
 [!INCLUDE[wv](../../../../includes/wv-md.md)]를 실행하는 경우 이미 설치되어 있는 Netsh.exe 도구를 사용합니다.  
  
 이 항목에서는 다음과 같은 여러 절차를 수행하는 방법에 대해 설명합니다.  
  
- 컴퓨터의 현재 포트 구성 결정  
  
- 인증서의 지문 가져오기(다음 두 절차에 필요)  
  
- SSL 인증서를 포트 구성에 바인딩  
  
- SSL 인증서를 포트 구성에 바인딩 및 클라이언트 인증서 지원  
  
- 포트 번호에서 SSL 인증서 삭제  
  
 컴퓨터에 저장된 인증서를 수정하려면 관리자 권한이 필요합니다.  
  
### <a name="to-determine-how-ports-are-configured"></a>포트의 구성 방법을 확인하려면  
  
1. 또는 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 에서 다음 예제와 같이 httpcfg.exe 도구를 사용 하 여 쿼리 및 ssl 스위치를 사용 하 여 현재 포트 구성을 봅니다. [!INCLUDE[wxp](../../../../includes/wxp-md.md)]  
  
    ```console
    httpcfg query ssl  
    ```  
  
2. [!INCLUDE[wv](../../../../includes/wv-md.md)]에서 다음 예제와 같이 Netsh.exe 도구를 사용하여 현재 포트 구성을 봅니다.  
  
    ```console  
    netsh http show sslcert  
    ```  
  
### <a name="to-get-a-certificates-thumbprint"></a>인증서의 지문을 가져오려면  
  
1. 인증서 MMC 스냅인을 사용하여 클라이언트 인증 용도의 X.509 인증서를 찾습니다. 자세한 내용은 [방법: MMC 스냅인](../../../../docs/framework/wcf/feature-details/how-to-view-certificates-with-the-mmc-snap-in.md)을 사용 하 여 인증서를 봅니다.  
  
2. 인증서의 지문에 액세스합니다. 자세한 내용은 [방법: 인증서](../../../../docs/framework/wcf/feature-details/how-to-retrieve-the-thumbprint-of-a-certificate.md)의 지문을 검색 합니다.  
  
3. 인증서의 지문을 메모장 등의 텍스트 편집기에 복사합니다.  
  
4. 16진수 문자 사이의 모든 공간을 제거합니다. 여기에 사용되는 방법 중 하나는 텍스트 편집기의 찾기 및 바꾸기 기능을 사용하여 각 공간을 null 문자로 바꾸는 것입니다.  
  
### <a name="to-bind-an-ssl-certificate-to-a-port-number"></a>SSL 인증서를 포트 번호에 바인딩하려면  
  
1. [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 또는 [!INCLUDE[wxp](../../../../includes/wxp-md.md)]에서 SSL(Secure Sockets Layer) 저장소에 "set" 모드의 HttpCfg.exe 도구를 사용하여 인증서를 포트 번호에 바인딩합니다. 도구에서는 다음 예제처럼 지문을 사용하여 인증서를 식별합니다.  
  
    ```console  
    httpcfg set ssl -i 0.0.0.0:8012 -h 0000000000003ed9cd0c315bbb6dc1c08da5e6  
    ```  
  
    - **-I** 스위치에는의 `IP`구문이 있습니다.`port` 및는 컴퓨터의 포트 8012에 인증서를 설정 하도록 도구에 지시 합니다. 선택적으로, 번호 앞에 있는 4개의 0을 컴퓨터의 실제 IP 주소로 대체할 수 있습니다.  
  
    - **-H** 스위치는 인증서의 지문을 지정 합니다.  
  
2. [!INCLUDE[wv](../../../../includes/wv-md.md)]에서 다음 예제와 같이 Netsh.exe 도구를 사용합니다.  
  
    ```console  
    netsh http add sslcert ipport=0.0.0.0:8000 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}   
    ```  
  
    - **Certhash** 매개 변수는 인증서의 지문을 지정 합니다.  
  
    - **Ipport** 매개 변수는 IP 주소 및 포트를 지정 하 고 설명 된 httpcfg.exe 도구의 **-i** 스위치와 마찬가지로 작동 합니다.  
  
    - **Appid** 매개 변수는 소유 응용 프로그램을 식별 하는 데 사용할 수 있는 GUID입니다.  
  
### <a name="to-bind-an-ssl-certificate-to-a-port-number-and-support-client-certificates"></a>SSL 인증서를 포트 번호에 바인딩하고 클라이언트 인증서를 지원하려면  
  
1. [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 또는 [!INCLUDE[wxp](../../../../includes/wxp-md.md)]에서 전송 계층에 X.509 인증서를 사용하여 인증하는 클라이언트를 지원하려면 위의 절차를 수행하되 다음 예제처럼 추가 명령줄 매개 변수를 HttpCfg.exe에 전달합니다.  
  
    ```console  
    httpcfg set ssl -i 0.0.0.0:8012 -h 0000000000003ed9cd0c315bbb6dc1c08da5e6 -f 2  
    ```  
  
     **-F** 스위치에는 구문이 `n` 있습니다. 여기서 n은 1에서 7 사이의 숫자입니다. 위의 예제와 같이 값 2를 사용하면 전송 계층에서 클라이언트 인증서가 활성화됩니다. 값 3을 사용하면 클라이언트 인증서가 활성화되고 해당 인증서가 Windows 계정에 매핑됩니다. 다른 값의 동작에 대한 자세한 내용은 HttpCfg.exe 도움말을 참조하세요.  
  
2. [!INCLUDE[wv](../../../../includes/wv-md.md)]에서 전송 계층에서 X.509 인증서를 사용하여 인증하는 클라이언트를 지원하려면 위의 절차를 수행하되 다음 예제처럼 추가 매개 변수를 사용합니다.  
  
    ```console  
    netsh http add sslcert ipport=0.0.0.0:8000 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF} clientcertnegotiation=enable  
    ```  
  
### <a name="to-delete-an-ssl-certificate-from-a-port-number"></a>포트 번호에서 SSL 인증서를 삭제하려면  
  
1. HttpCfg.exe 또는 Netsh.exe 도구를 사용하여 컴퓨터에 있는 모든 바인딩의 포트와 지문을 표시합니다. 정보를 디스크에 인쇄 하려면 다음 예제와 같이 리디렉션 문자 ">"을 사용 합니다.  
  
    ```console  
    httpcfg query ssl>myMachinePorts.txt  
    ```
  
2. 또는 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 에서는 delete 및 ssl 키워드와 함께 httpcfg.exe 도구를 사용 합니다. [!INCLUDE[wxp](../../../../includes/wxp-md.md)] **-I** 스위치를 사용 하 여 `IP`:`port` 번호를 지정 하 고 **-h** 스위치를 사용 하 여 지문을 지정 합니다.  
  
    ```console  
    httpcfg delete ssl -i 0.0.0.0:8005 -h 0000000000003ed9cd0c315bbb6dc1c08da5e6  
    ```  
  
3. [!INCLUDE[wv](../../../../includes/wv-md.md)]에서 다음 예제와 같이 Netsh.exe 도구를 사용합니다.  
  
    ```console  
    Netsh http delete sslcert ipport=0.0.0.0:8005  
    ```  
  
## <a name="example"></a>예제  
 다음 코드에서는 전송 보안에 설정된 <xref:System.ServiceModel.WSHttpBinding> 클래스를 사용하여 자체 호스트된 서비스를 만드는 방법을 보여 줍니다. 애플리케이션을 만들 때에는 주소에 포트 번호를 지정합니다.  
  
 [!code-csharp[c_WsHttpService#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wshttpservice/cs/source.cs#3)]
 [!code-vb[c_WsHttpService#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wshttpservice/vb/source.vb#3)]  
  
## <a name="see-also"></a>참고자료

- [HTTP 전송 보안](../../../../docs/framework/wcf/feature-details/http-transport-security.md)
