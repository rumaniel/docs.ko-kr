---
title: '방법: WCF에 액세스할 수 있는 X.509 인증서 만들기'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- X.509 certificates [WCF]
- certificates [WCF], making X.509 certificates accessible to WCF
- X.509 certificates [WCF], making accessible to WCF
ms.assetid: a54e407c-c2b5-4319-a648-60e43413664b
ms.openlocfilehash: 401371bf01a62a20f2834cb76df19d9ddaacf83d
ms.sourcegitcommit: 7b1ce327e8c84f115f007be4728d29a89efe11ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70972349"
---
# <a name="how-to-make-x509-certificates-accessible-to-wcf"></a>방법: WCF에 액세스할 수 있는 X.509 인증서 만들기
Windows Communication Foundation (WCF)에서 x.509 인증서에 액세스할 수 있도록 하려면 응용 프로그램 코드에서 인증서 저장소 이름 및 위치를 지정 해야 합니다. 상황에 따라, X.509 인증서와 연결된 프라이빗 키를 포함하는 파일에 대한 액세스가 프로세스 ID에 필요할 수 있습니다. 인증서 저장소에 있는 x.509 인증서와 연결 된 개인 키를 가져오려면 WCF에서이 작업을 수행할 수 있는 권한이 있어야 합니다. 기본적으로 소유자와 시스템 계정에서만 인증서의 프라이빗 키에 액세스할 수 있습니다.  
  
### <a name="to-make-x509-certificates-accessible-to-wcf"></a>WCF에서 X.509 인증서에 액세스할 수 있도록 설정하려면  
  
1. WCF가 실행 중인 계정에 x.509 인증서와 연결 된 개인 키가 포함 된 파일에 대 한 읽기 액세스 권한을 부여 합니다.  
  
    1. WCF에 x.509 인증서의 개인 키에 대 한 읽기 권한이 필요한 지 여부를 결정 합니다.  
  
         다음 표에는 X.509 인증서를 사용하는 경우 프라이빗 키를 사용할 수 있어야 하는지 여부가 자세히 표시되어 있습니다.  
  
        |X.509 인증서 사용|프라이빗 키|  
        |---------------------------|-----------------|  
        |아웃바운드 SOAP 메시지 디지털 서명.|예|  
        |인바운드 SOAP 메시지 서명 확인.|아니요|  
        |아웃바운드 SOAP 메시지 암호화.|아니요|  
        |인바운드 SOAP 메시지 암호 해독.|예|  
  
    2. 인증서가 저장되는 인증서 저장소 위치와 이름을 확인합니다.  
  
         인증서가 저장되는 인증서 스토리지는 애플리케이션 코드 또는 구성에 지정됩니다. 예를 들어, 다음 예에서는 인증서 위치를 이름이 `CurrentUser`인 `My` 인증서 저장소로 지정합니다.  
  
         [!code-csharp[x509Accessible#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/x509accessible/cs/source.cs#1)]
         [!code-vb[x509Accessible#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/x509accessible/vb/source.vb#1)]  
  
    3. [FindPrivateKey](../../../../docs/framework/wcf/samples/findprivatekey.md) 도구를 사용 하 여 컴퓨터에서 인증서에 대 한 개인 키가 있는 위치를 확인 합니다.  
  
         [FindPrivateKey](../../../../docs/framework/wcf/samples/findprivatekey.md) 도구에는 인증서 저장소 이름, 인증서 저장소 위치 및 인증서를 고유 하 게 식별 하는 항목이 필요 합니다. 도구에서는 인증서의 제목 이름이나 지문을 고유 식별자로 사용합니다. 인증서의 지문을 확인 하는 방법에 대 한 자세한 내용은 [방법: 인증서](../../../../docs/framework/wcf/feature-details/how-to-retrieve-the-thumbprint-of-a-certificate.md)의 지문을 검색 합니다.  
  
         다음 코드 예제에서는 [FindPrivateKey](../../../../docs/framework/wcf/samples/findprivatekey.md) 도구를 사용 하 여의 `My` `46 dd 0e 7a ed 0b 7a 31 9b 02 a3 a0 43 7a d8 3f 60 40 92 9d`지문이 인의 `CurrentUser` 저장소에 있는 인증서에 대 한 개인 키의 위치를 확인 합니다.  
  
        ```console
        findprivatekey.exe My CurrentUser -t "46 dd 0e 7a ed 0b 7a 31 9b 02 a3 a0 43 7a d8 3f 60 40 92 9d" -a  
        ```  
  
    4. WCF가 실행 되 고 있는 계정을 확인 합니다.  
  
         다음 표에서는 지정 된 시나리오에 대해 WCF가 실행 되는 계정에 대해 자세히 설명 합니다.  
  
        |시나리오|프로세스 ID|  
        |--------------|----------------------|  
        |클라이언트(콘솔 또는 WinForms 애플리케이션).|현재 로그인한 사용자.|  
        |자체 호스팅된 서비스.|현재 로그인한 사용자.|  
        |IIS 6.0([!INCLUDE[ws2003](../../../../includes/ws2003-md.md)]) 또는 IIS 7.0([!INCLUDE[wv](../../../../includes/wv-md.md)])에서 호스팅되는 서비스.|NETWORK SERVICE|  
        |IIS 5.X([!INCLUDE[wxp](../../../../includes/wxp-md.md)])에서 호스팅되는 서비스.|Machine.config 파일의 `<processModel>` 요소로 제어됩니다. 기본 계정은 ASPNET입니다.|  
  
    5. Icacls와 같은 도구를 사용 하 여 개인 키가 포함 된 파일에 대 한 읽기 권한을 WCF가 실행 중인 계정에 부여 합니다.  
  
         다음 코드 예제에서는 지정 된 파일에 대 한 DACL (임의 액세스 제어 목록)을 편집 하 여 네트워크 서비스 계정에 파일에 대 한 읽기 (: R) 액세스 권한을 부여 합니다.  
  
        ```console 
        icacls.exe "C:\Documents and Settings\All Users\Application Data\Microsoft\Crypto\RSA\MachineKeys\8aeda5eb81555f14f8f9960745b5a40d_38f7de48-5ee9-452d-8a5a-92789d7110b1" /grant "NETWORK SERVICE":R  
        ```  
  
## <a name="see-also"></a>참고자료

- [FindPrivateKey](../../../../docs/framework/wcf/samples/findprivatekey.md)
- [방법: 인증서의 지문을 검색 합니다.](../../../../docs/framework/wcf/feature-details/how-to-retrieve-the-thumbprint-of-a-certificate.md)
- [인증서 작업](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)
