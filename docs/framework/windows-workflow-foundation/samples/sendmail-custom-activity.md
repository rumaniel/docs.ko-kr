---
title: SendMail 사용자 지정 활동
ms.date: 03/30/2017
ms.assetid: 947a9ae6-379c-43a3-9cd5-87f573a5739f
ms.openlocfilehash: 5797620c4938d7dcffb1f506b682141336b21eab
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70988988"
---
# <a name="sendmail-custom-activity"></a>SendMail 사용자 지정 활동
이 샘플에서는 워크플로 애플리케이션 내에서 사용하기 위해 <xref:System.Activities.AsyncCodeActivity>로부터 파생되는 사용자 지정 활동을 만들어 SMTP를 사용하여 메일을 보내는 방법을 보여 줍니다. 사용자 지정 작업은의 <xref:System.Net.Mail.SmtpClient> 기능을 사용 하 여 비동기적으로 전자 메일을 보내고 인증을 사용 하 여 메일을 보냅니다. 또한 테스트 모드, 토큰 바꾸기, 파일 템플릿 및 테스트 드롭 경로와 같은 몇 가지 최종 사용자 기능도 제공합니다.  
  
 다음 표에서는 `SendMail` 활동의 인수에 대해 자세히 설명합니다.  
  
|이름|형식|Description|  
|-|-|-|  
|호스트|String|SMTP 서버 호스트의 주소입니다.|  
|포트|String|호스트에 있는 SMTP 서비스의 포트입니다.|  
|EnableSsl|bool|<xref:System.Net.Mail.SmtpClient>에서 SSL(Secure Sockets Layer)을 사용하여 연결을 암호화할지 여부를 지정합니다.|  
|UserName|문자열|보낸 사람의 <xref:System.Net.Mail.SmtpClient.Credentials%2A> 속성을 인증하는 자격 증명을 설정할 사용자 이름입니다.|  
|암호|String|보낸 사람의 <xref:System.Net.Mail.SmtpClient.Credentials%2A> 속성을 인증하는 자격 증명을 설정할 암호입니다.|  
|제목|<xref:System.Activities.InArgument%601>\<string>|메시지 제목입니다.|  
|본문|<xref:System.Activities.InArgument%601>\<string>|메시지 본문입니다.|  
|첨부 파일|<xref:System.Activities.InArgument%601>\<string>|이 전자 메일 메시지에 첨부 된 데이터를 저장 하는 데 사용 되는 첨부 파일 컬렉션입니다.|  
|변경 전|<xref:System.Net.Mail.MailAddress>|이 전자 메일 메시지의 보낸 사람 주소입니다.|  
|변경 후|<xref:System.Activities.InArgument%601>\<<xref:System.Net.Mail.MailAddressCollection>>|이 전자 메일 메시지의 받는 사람이 들어 있는 주소 컬렉션입니다.|  
|CC|<xref:System.Activities.InArgument%601>\<<xref:System.Net.Mail.MailAddressCollection>>|이 전자 메일 메시지에 대 한 CC (참조) 받는 사람이 들어 있는 주소 컬렉션입니다.|  
|BCC|<xref:System.Activities.InArgument%601>\<<xref:System.Net.Mail.MailAddressCollection>>|이 전자 메일 메시지의 BCC (숨은 참조) 받는 사람이 들어 있는 주소 컬렉션입니다.|  
|토큰|<xref:System.Activities.InArgument%601>< IDictionary\<문자열, 문자열 > >|본문에서 바꿀 토큰입니다. 사용자는 이 기능을 통해 나중에 이 속성을 사용하여 제공된 토큰으로 바꿀 수 있는 일부 값을 본문에 지정할 수 있습니다.|  
|BodyTemplateFilePath|문자열|본문에 대한 템플릿의 경로입니다. `SendMail` 활동은 이 파일의 내용을 본문 속성에 복사합니다.<br /><br /> 템플릿에는 토큰 속성의 내용으로 바뀌는 토큰이 포함될 수 있습니다.|  
|TestMailTo|<xref:System.Net.Mail.MailAddress>|이 속성을 설정 하면 모든 메일이 지정 된 주소로 전송 됩니다.<br /><br /> 이 속성은 워크플로를 테스트할 때 사용할 수 있습니다. 예를 들어 실제 받는 사람에 게 전자 메일을 보내지 않고 모든 전자 메일을 보낼지 확인 하려고 합니다.|  
|TestDropPath|String|이 속성이 설정 되 면 모든 전자 메일이 지정 된 파일에도 저장 됩니다.<br /><br /> 이 속성은 워크플로를 테스트 하거나 디버그할 때 발신 전자 메일의 형식과 콘텐츠가 적절 한지 확인 하는 데 사용 됩니다.|  
  
## <a name="solution-contents"></a>솔루션 개념  
 솔루션에는 두 개의 프로젝트가 포함되어 있습니다.  
  
|Project|설명|중요한 파일|  
|-------------|-----------------|---------------------|  
|SendMail|SendMail 활동|1.  SendMail.cs: 기본 활동에 대한 구현<br />2.  SendMailDesigner.xaml 및 SendMailDesigner.xaml.cs: SendMail 활동에 대한 디자이너<br />3.  MailTemplateBody.htm: 보낼 전자 메일에 대한 템플릿|  
|SendMailTestClient|SendMail 활동을 테스트할 클라이언트입니다.  이 프로젝트에서는 SendMail 활동을 호출하는 두 가지 방식, 즉 선언 방식과 프로그래밍 방식을 보여 줍니다.|1.  Sequence1.xaml: SendMail 활동을 호출하는 워크플로입니다.<br />2.  Program.cs: Sequence1을 호출하고 SendMail을 사용하는 워크플로를 프로그래밍 방식으로 만듭니다.|  
  
## <a name="further-configuration-of-the-sendmail-activity"></a>SendMail 활동의 추가 구성  
 샘플에는 표시되지 않지만 사용자는 SendMail 활동의 구성을 추가할 수 있습니다. 다음 세 개의 섹션에서는 이를 수행하는 방법을 보여 줍니다.  
  
### <a name="sending-an-email-using-tokens-specified-in-the-body"></a>본문에 지정된 토큰을 사용하여 전자 메일 보내기  
 이 코드 조각에서는 본문에 토큰이 포함된 전자 메일을 보낼 수 있는 방법을 보여 줍니다. 토큰이 본문 속성에 어떻게 제공되는지 확인합니다. 해당 토큰 값은 토큰 속성에 제공됩니다.  
  
```csharp  
IDictionary<string, string> tokens = new Dictionary<string, string>();  
tokens.Add("@name", "John Doe");  
tokens.Add("@date", DateTime.Now.ToString());  
tokens.Add("@server", "localhost");  
  
new SendMail  
{  
    From = new LambdaValue<MailAddress>(ctx => new MailAddress("john.doe@contoso.com")),  
    To = new LambdaValue<MailAddressCollection>(  
                    ctx => new MailAddressCollection() { new MailAddress("someone@microsoft.com") }),  
    Subject = "Test email",  
    Body = "Hello @name. This is a test email sent from @server. Current date is @date",  
    Host = "localhost",  
    Port = 25,  
    Tokens = new LambdaValue<IDictionary<string, string>>(ctx => tokens)  
};  
```  
  
### <a name="sending-an-email-using-a-template"></a>템플릿을 사용하여 전자 메일 보내기  
 이 조각에서는 본문의 템플릿 토큰을 사용하여 전자 메일을 보내는 방법을 보여 줍니다. `BodyTemplateFilePath` 속성을 설정할 때 Body 속성 값을 제공할 필요가 없습니다. 템플릿 파일의 내용이 본문에 복사되기 때문입니다.  
  
```csharp  
new SendMail  
{    
    From = new LambdaValue<MailAddress>(ctx => new MailAddress("john.doe@contoso.com")),  
    To = new LambdaValue<MailAddressCollection>(  
                    ctx => new MailAddressCollection() { new MailAddress("someone@microsoft.com") }),  
    Subject = "Test email",  
    Host = "localhost",  
    Port = 25,  
    Tokens = new LambdaValue<IDictionary<string, string>>(ctx => tokens),  
    BodyTemplateFilePath = @"..\..\..\SendMail\Templates\MailTemplateBody.htm",   
};  
```  
  
### <a name="sending-mails-in-testing-mode"></a>테스트 모드에서 메일 보내기  
 이 코드 조각에서는 두 개의 테스트 속성을 설정 하는 방법을 보여 `TestMailTo` 줍니다 .를로 설정 하면 모든 `john.doe@contoso.con` 메시지를로 보냅니다. TestDropPath를 설정하면 나가는 모든 전자 메일이 제공된 경로에도 기록됩니다. 이러한 속성은 서로 관련되어 있지 않으므로 독립적으로 설정할 수 있습니다.  
  
```csharp  
new SendMail  
{    
   From = new LambdaValue<MailAddress>(ctx => new MailAddress("john.doe@contoso.com")),  
   To = new LambdaValue<MailAddressCollection>(  
                    ctx => new MailAddressCollection() { new MailAddress("someone@microsoft.com") }),  
   Subject = "Test email",  
   Host = "localhost",  
   Port = 25,  
   Tokens = new LambdaValue<IDictionary<string, string>>(ctx => tokens),  
   BodyTemplateFilePath = @"..\..\..\SendMail\Templates\MailTemplateBody.htm",  
   TestMailTo= new LambdaValue<MailAddress>(ctx => new MailAddress("john.doe@contoso.com")),  
   TestDropPath = @"c:\Samples\SendMail\TestDropPath\",  
};  
```  
  
## <a name="set-up-instructions"></a>설치 지침  
 이 샘플을 실행하려면 SMTP 서버에 액세스해야 합니다.  
  
 SMTP 서버를 설정 하는 방법에 대 한 자세한 내용은 다음 링크를 참조 하십시오.  
  
- [Microsoft Technet](https://go.microsoft.com/fwlink/?LinkId=166060)  
  
- [SMTP 서비스 구성 (IIS 6.0)](https://go.microsoft.com/fwlink/?LinkId=150456)  
  
- [IIS 7.0: SMTP 전자 메일 구성](https://go.microsoft.com/fwlink/?LinkId=150457)  
  
- [SMTP 서비스를 설치 하는 방법](https://go.microsoft.com/fwlink/?LinkId=150458)  
  
 타사에서 제공하는 SMTP 에뮬레이터를 다운로드할 수 있습니다.  
  
##### <a name="to-run-this-sample"></a>이 샘플을 실행하려면  
  
1. Visual Studio 2010을 사용 하 여 SendMail 솔루션 파일을 엽니다.  
  
2. 올바른 SMTP 서버에 액세스할 수 있는 권한이 있는지 확인합니다. 설치 지침을 참조하세요.  
  
3. 서버 주소를 사용 하 여 프로그램을 구성 하 고 및에서 전자 메일 주소로 프로그램을 구성 합니다.  
  
     이 샘플을 올바르게 실행 하려면 Program.cs 및 .xaml에서 전자 메일 주소와 SMTP 서버의 주소에서 값을 구성 해야 할 수 있습니다. 프로그램은 메일을 두 가지 다른 방식으로 보내므로 두 위치에서 모두 주소를 변경해야 합니다.  
  
4. Ctrl+Shift+B를 눌러 솔루션을 빌드합니다.  
  
5. Ctrl+F5를 눌러 솔루션을 실행합니다.  
  
> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> 이 디렉터리가 없는 경우 [.NET Framework 4에 대 한 Windows Communication Foundation (wcf) 및 Windows Workflow Foundation (WF) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 로 이동 하 여 모든 Windows Communication Foundation (wcf) 및 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플을 다운로드 합니다. 이 샘플은 다음 디렉터리에 있습니다.  
>   
> `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\SendMail`
