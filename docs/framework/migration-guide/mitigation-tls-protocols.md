---
title: '완화: TLS 프로토콜'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 33f97d13-3022-43da-8b18-cdb5c88df9c2
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: e98b447028ef9fa96233a71133aa82184d83cec8
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/07/2019
ms.locfileid: "70779161"
---
# <a name="mitigation-tls-protocols"></a>완화: TLS 프로토콜
.NET Framework 4.6부터 <xref:System.Net.ServicePointManager?displayProperty=nameWithType> 및 <xref:System.Net.Security.SslStream?displayProperty=nameWithType> 클래스에서 다음 세 개의 프로토콜 중 하나를 사용할 수 있습니다. Tls1.0, Tls1.1 또는 Tls 1.2. SSL3.0 프로토콜 및 RC4 암호화는 지원되지 않습니다.  
  
## <a name="impact"></a>영향  
 이러한 변경 내용은 다음 앱에 영향을 줍니다.  
  
- HTTPS 서버 또는 <xref:System.Net.Http.HttpClient>, <xref:System.Net.HttpWebRequest>, <xref:System.Net.FtpWebRequest>, <xref:System.Net.Mail.SmtpClient> 및 <xref:System.Net.Security.SslStream> 유형 중 하나를 사용하는 소켓 서버와 통신하는 데 SSL을 사용하는 모든 앱  
  
- Tls1.0, Tls1.1 또는 Tls 1.2를 지원하기 위해 업그레이드할 수 없는 모든 서버 쪽 앱  
  
## <a name="mitigation"></a>완화  
 권장되는 완화 방법은 Tls1.0, Tls1.1 또는 Tls 1.2로 서버 쪽 앱을 업그레이드하는 것입니다. 이 작업이 불가능하거나 클라이언트 앱이 손상된 경우 <xref:System.AppContext> 클래스를 사용하여 다음 두 방법 중 하나로 이 기능을 옵트아웃(opt out)할 수 있습니다.  
  
- 다음과 같은 코드 조각을 사용하여 프로그래밍 방식으로  
  
     [!code-csharp[AppCompat.SSLProtocols#1](../../../samples/snippets/csharp/VS_Snippets_CLR/appcompat.sslprotocols/cs/program.cs#1)]
     [!code-vb[AppCompat.SSLProtocols#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/appcompat.sslprotocols/vb/module1.vb#1)]  
  
     <xref:System.Net.ServicePointManager> 개체는 한 번만 초기화되므로 먼저 애플리케이션에서 이러한 호환성 설정을 정의해야 합니다.  
  
- 다음 줄을 app.config 파일의 [\<runtime>](../configure-apps/file-schema/runtime/runtime-element.md) 섹션에 추가  
  
    ```xml  
    <AppContextSwitchOverrides value="Switch.System.Net.DontEnableSchUseStrongCrypto=true"/>  
    ```  
  
 그러나 애플리케이션 보안 수준이 낮아지므로 기본 동작은 옵트아웃(opt out)하지 않는 것이 좋습니다.  
  
## <a name="see-also"></a>참고 항목

- [대상 다시 지정 변경 내용](retargeting-changes-in-the-net-framework-4-6.md)
