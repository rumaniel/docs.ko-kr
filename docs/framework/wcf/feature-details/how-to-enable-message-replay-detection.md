---
title: '방법: 메시지 재생 검색 사용'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF security
- replay detection [WCF]
- WCF, custom bindings
- WCF, security
ms.assetid: 8b847e91-69a3-49e1-9e5f-0c455e50d804
ms.openlocfilehash: a41c53e87d82452eac8d7535a422b7aa4bd4e270
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64626887"
---
# <a name="how-to-enable-message-replay-detection"></a>방법: 메시지 재생 검색 사용
공격자가 두 당사자 간에 메시지 스트림을 복사하고 하나 이상의 당사자에게 스트림을 재생하는 경우 재생 공격이 발생합니다. 완화되지 않은 경우 공격을 받기 쉬운 컴퓨터는 스트림을 올바른 메시지로 처리하여 항목에 대한 중복 주문과 같은 잘못된 결과의 범위에 있게 됩니다.  
  
 메시지 재생을 검색 하는 방법에 대 한 자세한 내용은 참조 하십시오 [Message Replay Detection](https://go.microsoft.com/fwlink/?LinkId=88536)합니다.  
  
 다음 절차는 Windows Communication Foundation (WCF)를 사용 하 여 재생 검색을 제어 하는 데 사용할 수 있는 다양 한 속성을 보여 줍니다.  
  
### <a name="to-control-replay-detection-on-the-client-using-code"></a>코드를 사용하여 클라이언트에서 재생 검색을 제어하려면  
  
1. <xref:System.ServiceModel.Channels.SecurityBindingElement>에서 사용할 <xref:System.ServiceModel.Channels.CustomBinding>를 만듭니다. 자세한 내용은 [방법: SecurityBindingElement를 사용 하 여 사용자 지정 바인딩을 만들려면](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)합니다. 다음 예제에서는 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> 클래스의 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateKerberosBindingElement%2A>를 사용하여 만든 <xref:System.ServiceModel.Channels.SecurityBindingElement>를 사용합니다.  
  
2. <xref:System.ServiceModel.Channels.SecurityBindingElement.LocalClientSettings%2A> 속성을 사용하여 <xref:System.ServiceModel.Channels.LocalClientSecuritySettings> 클래스에 대한 참조를 반환하고 다음 속성을 적절히 설정합니다.  
  
    1. `DetectReplay`. 부울 값입니다. 이 값은 클라이언트가 서버로부터 재생을 검색해야 하는지 여부를 제어합니다. 기본값은 `true`입니다.  
  
    2. `MaxClockSkew`. <xref:System.TimeSpan> 값입니다. 재생 메커니즘이 클라이언트와 서버 간에 허용하는 오차 횟수를 제어합니다. 보안 메커니즘은 보낸 타임스탬프를 검사하고 보낸 시간이 아주 오래되었는지 여부를 확인합니다. 기본값은 5분입니다.  
  
    3. `ReplayWindow`. `TimeSpan` 값입니다. 이 값은 매개자를 통해 서버에서 메시지를 보낸 후 클라이언트에 도달하기까지 메시지가 네트워크에 있을 수 있는 시간을 제어합니다. 클라이언트는 재생 검색을 위해 최신 `ReplayWindow` 내에서 보낸 메시지 서명을 추적합니다.  
  
    4. `ReplayCacheSize`. 정수 값입니다. 클라이언트는 캐시에 메시지 서명을 저장합니다. 이 설정은 캐시에서 저장할 수 있는 서명 수를 지정합니다. 최신 재생 창 내에서 보낸 메시지 수가 캐시 한계에 도달하면 가장 오래 전에 캐시된 서명이 시간 제한에 도달할 때까지 새 메시지가 거부됩니다. 기본값은 500000입니다.  
  
### <a name="to-control-replay-detection-on-the-service-using-code"></a>코드를 사용하여 서비스에서 재생 검색을 제어하려면  
  
1. <xref:System.ServiceModel.Channels.SecurityBindingElement>에서 사용할 <xref:System.ServiceModel.Channels.CustomBinding>를 만듭니다.  
  
2. <xref:System.ServiceModel.Channels.SecurityBindingElement.LocalServiceSettings%2A> 속성을 사용하여 <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings> 클래스에 대한 참조를 반환하고 앞에서 설명한 대로 속성을 설정합니다.  
  
### <a name="to-control-replay-detection-in-configuration-for-the-client-or-service"></a>클라이언트나 서비스에 대한 구성에서 재생 검색을 제어하려면  
  
1. 만들기는 [ \<customBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)합니다.  
  
2. `<security>` 요소를 만듭니다.  
  
3. 만들기는 [ \<localClientSettings >](../../../../docs/framework/configure-apps/file-schema/wcf/localclientsettings-element.md) 하거나 [ \<localServiceSettings >](../../../../docs/framework/configure-apps/file-schema/wcf/localservicesettings-element.md)합니다.  
  
4. `detectReplays`, `maxClockSkew`, `replayWindow` 및 `replayCacheSize` 특성 값을 적절히 설정합니다. 다음 예제에서는 `<localServiceSettings>` 및`<localClientSettings>` 요소 모두의 특성을 설정합니다.  
  
    ```xml  
    <customBinding>  
      <binding name="NewBinding0">  
       <textMessageEncoding />  
        <security>  
         <localClientSettings   
          replayCacheSize="800000"   
          maxClockSkew="00:03:00"  
          replayWindow="00:03:00" />  
         <localServiceSettings   
          replayCacheSize="800000"   
          maxClockSkew="00:03:00"  
          replayWindow="00:03:00" />  
        <secureConversationBootstrap />  
       </security>  
      <httpTransport />  
     </binding>  
    </customBinding>  
    ```  
  
## <a name="example"></a>예제  
 다음 예제에서는 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> 메서드를 사용하여 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateKerberosBindingElement%2A>를 만들고 바인딩의 재생 속성을 설정합니다.  
  
 [!code-csharp[c_ReplayDetection#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_replaydetection/cs/source.cs#1)]
 [!code-vb[c_ReplayDetection#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_replaydetection/vb/source.vb#1)]  
  
## <a name="scope-of-replay-message-security-only"></a>재생 범위: 메시지 보안만  
 다음 프로시저는 메시지 보안 모드에만 적용됩니다. 전송 모드 및 메시지 자격 증명을 사용한 전송 모드에서 전송 메커니즘은 재생을 검색합니다.  
  
## <a name="secure-conversation-notes"></a>보안 대화 참고 사항  
 보안 대화를 사용하는 바인딩에서 보안 대화 부트스트랩 바인딩뿐만 아니라 애플리케이션 채널에 대해 이러한 설정을 조정할 수 있습니다. 예를 들면 애플리케이션 채널에 대해 재생을 해제할 수 있지만 보안 대화를 설정하는 부트스트랩 채널에 대해서는 재생을 사용하도록 설정할 수 있습니다.  
  
 보안 대화 세션을 사용하지 않는 경우에는 서버 팜 시나리오에서, 그리고 프로세스가 재활용되는 경우 재생 검색이 작동하지 않을 수도 있습니다. 이 내용은 다음과 같은 시스템 제공 바인딩에 적용됩니다.  
  
- <xref:System.ServiceModel.BasicHttpBinding>.  
  
- <xref:System.ServiceModel.WSHttpBinding> 속성이 <xref:System.ServiceModel.NonDualMessageSecurityOverHttp.EstablishSecurityContext%2A>로 설정된 `false`  
  
## <a name="compiling-the-code"></a>코드 컴파일  
  
- 코드를 컴파일하려면 다음 네임스페이스가 필요합니다.  
  
- <xref:System>  
  
- <xref:System.ServiceModel>  
  
- <xref:System.ServiceModel.Channels>  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Channels.LocalClientSecuritySettings>
- <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings>
- [보안 대화 및 보안 세션](../../../../docs/framework/wcf/feature-details/secure-conversations-and-secure-sessions.md)
- [\<localClientSettings>](../../../../docs/framework/configure-apps/file-schema/wcf/localclientsettings-element.md)
- [방법: SecurityBindingElement를 사용 하 여 사용자 지정 바인딩 만들기](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)
