---
title: '방법: Windows 자격 증명을 사용하여 서비스 보호'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF, security
ms.assetid: d171b5ca-96ef-47ff-800c-c138023cf76e
ms.openlocfilehash: 19ac9da94ce6e405632293a7d569698c9d866bef
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70856057"
---
# <a name="how-to-secure-a-service-with-windows-credentials"></a>방법: Windows 자격 증명을 사용하여 서비스 보호

이 항목에서는 Windows 도메인에 있고 동일한 도메인의 클라이언트에 의해 호출 되는 WCF (Windows Communication Foundation) 서비스에서 전송 보안을 사용 하도록 설정 하는 방법을 보여 줍니다. 이 시나리오에 대 한 자세한 내용은 [Windows 인증을 사용 하 여 전송 보안](../../../docs/framework/wcf/feature-details/transport-security-with-windows-authentication.md)을 참조 하세요. 샘플 응용 프로그램은 [WSHttpBinding](../../../docs/framework/wcf/samples/wshttpbinding.md) 샘플을 참조 하세요.

이 항목에서는 사용자의 기존 계약 인터페이스 및 구현이 이미 정의되어 있다고 가정하고 여기에 더 추가합니다. 사용자는 기존 서비스 및 클라이언트를 수정할 수도 있습니다.

Windows 자격 증명을 사용하여 코드로 완전하게 서비스의 보안을 설정할 수 있습니다. 또는 구성 파일을 사용하여 일부 코드를 생략할 수 있습니다. 이 항목에서는 이 두 방법을 모두 보여 줍니다. 그러나 실제로는 이 두 방법 중 하나만 사용해야 합니다.

처음 세 개의 프로시저에서는 코드를 사용하여 서비스의 보안을 설정하는 방법을 보여 줍니다. 네 번째 및 다섯 번째 프로시저에서는 구성 파일을 사용하여 이 작업을 수행하는 방법을 보여 줍니다.

## <a name="using-code"></a>코드 사용

서비스 및 클라이언트에 대한 전체 코드는 이 항목 끝부분의 예제 단원에 나와 있습니다.

첫 번째 프로시저에서는 코드로 <xref:System.ServiceModel.WSHttpBinding> 클래스를 만들고 구성하는 과정을 보여 줍니다. 바인딩은 HTTP 전송을 사용합니다. 클라이언트에도 동일한 바인딩이 사용됩니다.

#### <a name="to-create-a-wshttpbinding-that-uses-windows-credentials-and-message-security"></a>Windows 자격 증명과 메시지 보안을 사용하는 WSHttpBinding을 만들려면

1. 이 프로시저 코드는 예제 단원의 서비스 코드에 있는 `Run`클래스에 대한 `Test` 메서드의 시작 부분에 삽입됩니다.

2. <xref:System.ServiceModel.WSHttpBinding> 클래스의 인스턴스를 만듭니다.

3. <xref:System.ServiceModel.WSHttpSecurity.Mode%2A> 클래스의 <xref:System.ServiceModel.WSHttpSecurity> 속성을 <xref:System.ServiceModel.SecurityMode.Message>로 설정합니다.

4. <xref:System.ServiceModel.MessageSecurityOverHttp.ClientCredentialType%2A> 클래스의 <xref:System.ServiceModel.MessageSecurityOverHttp> 속성을 <xref:System.ServiceModel.MessageCredentialType.Windows>로 설정합니다.

5. 이 프로시저에 대한 코드는 다음과 같습니다.

    [!code-csharp[c_SecureWindowsService#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewindowsservice/cs/secureservice.cs#1)]
    [!code-vb[c_SecureWindowsService#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewindowsservice/vb/secureservice.vb#1)]

### <a name="using-the-binding-in-a-service"></a>서비스에 바인딩 사용

이는 두 번째 프로시저로, 자체 호스트된 서비스에 바인딩을 사용하는 방법을 보여 줍니다. 서비스 호스팅에 대 한 자세한 내용은 [호스팅 서비스](../../../docs/framework/wcf/hosting-services.md)를 참조 하세요.

##### <a name="to-use-a-binding-in-a-service"></a>서비스에 바인딩을 사용하려면

1. 앞의 프로시저 코드 뒤에 이 프로시저 코드를 삽입합니다.

2. <xref:System.Type>이라는 `contractType` 변수를 만들어 인터페이스(`ICalculator`)의 형식을 할당합니다. Visual Basic 사용 하는 `GetType` 경우 연산자를 사용 합니다 .를 사용 하 `typeof` C#는 경우 키워드를 사용 합니다.

3. <xref:System.Type>이라는 두 번째 `serviceType` 변수를 만들어 구현된 계약(`Calculator`)의 형식을 할당합니다.

4. 서비스의 기본 주소를 사용하여 <xref:System.Uri>라는 `baseAddress` 클래스의 인스턴스를 만듭니다. 기본 주소에는 전송과 일치하는 체계가 있어야 합니다. 이 경우 전송 스키마는 HTTP이 고 주소에는 특수 한 URI (Uniform Resource Identifier) "localhost" 및 포트 번호 (8036) 뿐만 아니라 기본 끝점 주소 ("serviceModelSamples/) `http://localhost:8036/serviceModelSamples/`가 포함 됩니다.

5. <xref:System.ServiceModel.ServiceHost> 및 `serviceType` 변수를 사용하여 `baseAddress` 클래스의 인스턴스를 만듭니다.

6. `contractType`, 바인딩 및 엔드포인트 이름(secureCalculator)을 사용하여 엔드포인트를 서비스에 추가합니다. 클라이언트는 서비스에 대한 호출을 시작할 때 기본 주소와 엔드포인트 이름을 연결해야 합니다.

7. <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A> 메서드를 호출하여 서비스를 시작합니다. 이 프로시저에 대한 코드는 다음과 같습니다.

    [!code-csharp[c_SecureWindowsService#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewindowsservice/cs/secureservice.cs#2)]
    [!code-vb[c_SecureWindowsService#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewindowsservice/vb/secureservice.vb#2)]

### <a name="using-the-binding-in-a-client"></a>클라이언트에 바인딩 사용

이 프로시저에서는 서비스와 통신하는 프록시를 생성하는 방법을 보여 줍니다. 프록시는 서비스 메타 데이터를 사용 하 여 프록시를 만드는 [ServiceModel Metadata 유틸리티 도구 (svcutil.exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 를 사용 하 여 생성 됩니다.

또한 이 프로시저에서는 서비스와 통신하는 <xref:System.ServiceModel.WSHttpBinding> 클래스의 인스턴스를 만든 다음 서비스를 호출합니다.

이 예제에서는 코드만 사용하여 클라이언트를 만듭니다. 또는 이 프로시저 다음의 단원에 나오는 구성 파일을 사용할 수 있습니다.

##### <a name="to-use-a-binding-in-a-client-with-code"></a>코드를 통해 클라이언트에 바인딩을 사용하려면

1. SvcUtil.exe 도구를 사용하여 서비스의 메타데이터에서 프록시 코드를 생성합니다. 자세한 내용은 [방법: 클라이언트](../../../docs/framework/wcf/how-to-create-a-wcf-client.md)를 만듭니다. 생성 된 프록시 코드는 <xref:System.ServiceModel.ClientBase%601> 클래스에서 상속 하 여 모든 클라이언트에 WCF 서비스와 통신 하는 데 필요한 생성자, 메서드 및 속성이 있는지 확인 합니다. 이 예제에서 생성된 코드에는 `CalculatorClient` 인터페이스를 구현하는 `ICalculator` 클래스가 포함되어 서비스 코드와의 호환성을 지원합니다.

2. 이 프로시저의 코드는 클라이언트 프로그램에 대한 `Main` 메서드의 시작 부분에 삽입됩니다.

3. <xref:System.ServiceModel.WSHttpBinding> 클래스의 인스턴스를 만들고 보안 모드를 `Message`로, 클라이언트 자격 증명 형식을 `Windows`로 설정합니다. 이 예제에서는 변수 이름을 `clientBinding`으로 지정합니다.

4. <xref:System.ServiceModel.EndpointAddress>라는 `serviceAddress` 클래스의 인스턴스를 만듭니다. 기본 주소를 엔드포인트 이름과 연결하여 인스턴스를 초기화합니다.

5. `serviceAddress` 및 `clientBinding` 변수를 사용하여 생성된 클라이언트 클래스의 인스턴스를 만듭니다.

6. 다음 코드와 같이 <xref:System.ServiceModel.ClientBase%601.Open%2A> 메서드를 호출합니다.

7. 서비스를 호출하고 결과를 표시합니다.

    [!code-csharp[c_secureWindowsClient#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewindowsclient/cs/secureclient.cs#1)]
    [!code-vb[c_secureWindowsClient#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewindowsclient/vb/secureclient.vb#1)]

## <a name="using-the-configuration-file"></a>구성 파일 사용

프로시저 코드를 사용하여 바인딩을 만드는 대신 구성 파일의 바인딩 섹션에 대해 표시된 다음 코드를 사용할 수 있습니다.

아직 서비스를 정의 하지 않은 경우 [서비스 디자인 및 구현](../../../docs/framework/wcf/designing-and-implementing-services.md)및 [서비스 구성](../../../docs/framework/wcf/configuring-services.md)을 참조 하세요.

> [!NOTE]
> 이 구성 코드는 서비스 및 클라이언트 구성 파일에서 모두 사용 됩니다.

#### <a name="to-enable-transfer-security-on-a-service-in-a-windows-domain-using-configuration"></a>구성을 사용하여 Windows 도메인의 서비스에서 전송 보안을 활성화하려면

1. WsHttpBinding > 요소를 구성 파일의 [ \<바인딩 >](../../../docs/framework/configure-apps/file-schema/wcf/bindings.md) 요소 섹션에 추가 합니다. [ \<](../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md)

2. <`binding``WSHttpBinding` >요소에<>요소를추가하고특성을응용프로그램에적합한값`configurationName` 으로 설정 합니다.

3. <`security`> 요소를 추가 하 고 `mode` 특성을 Message로 설정 합니다.

4. <`message`> 요소를 추가 하 고 `clientCredentialType` 특성을 Windows로 설정 합니다.

5. 서비스의 구성 파일에서 `<bindings>` 섹션을 다음 코드로 바꿉니다. 서비스 구성 파일이 아직 없는 경우 [바인딩을 사용 하 여 서비스 및 클라이언트 구성](../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)을 참조 하세요.

    ```xml
    <bindings>
      <wsHttpBinding>
       <binding name = "wsHttpBinding_Calculator">
         <security mode="Message">
           <message clientCredentialType="Windows"/>
         </security>
        </binding>
      </wsHttpBinding>
    </bindings>
    ```

### <a name="using-the-binding-in-a-client"></a>클라이언트에 바인딩 사용

이 프로시저에서는 두 파일인 서비스와 통신하는 프록시 및 구성 파일을 생성하는 방법을 보여 줍니다. 또한 클라이언트에 사용된 세 번째 파일인 클라이언트 프로그램에 대한 변경 내용에 대해 설명합니다.

##### <a name="to-use-a-binding-in-a-client-with-configuration"></a>구성을 통해 클라이언트에 바인딩을 사용하려면

1. SvcUtil.exe 도구를 사용하여 서비스의 메타데이터에서 프록시 코드 및 구성 파일을 생성합니다. 자세한 내용은 [방법: 클라이언트](../../../docs/framework/wcf/how-to-create-a-wcf-client.md)를 만듭니다.

2. 생성 된 구성 파일의 [ \<바인딩 >](../../../docs/framework/configure-apps/file-schema/wcf/bindings.md) 섹션을 이전 섹션의 구성 코드로 바꿉니다.

3. 프로시저 코드는 클라이언트 프로그램에 대한 `Main` 메서드의 시작 부분에 삽입됩니다.

4. 바인딩 이름을 구성 파일에 입력 매개 변수로 전달하는 생성된 클라이언트 클래스의 인스턴스를 만듭니다.

5. 다음 코드와 같이 <xref:System.ServiceModel.ClientBase%601.Open%2A> 메서드를 호출합니다.

6. 서비스를 호출하고 결과를 표시합니다.

    [!code-csharp[c_secureWindowsClient#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewindowsclient/cs/secureclient.cs#2)]

## <a name="example"></a>예제

[!code-csharp[c_SecureWindowsService#0](../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewindowsservice/cs/secureservice.cs#0)]

[!code-csharp[c_SecureWindowsClient#0](../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewindowsclient/cs/secureclient.cs#0)]
[!code-vb[c_SecureWindowsClient#0](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewindowsclient/vb/secureclient.vb#0)]

## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.WSHttpBinding>
- [ServiceModel Metadata 유틸리티 도구(Svcutil.exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)
- [방법: 클라이언트 만들기](../../../docs/framework/wcf/how-to-create-a-wcf-client.md)
- [서비스에 보안 설정](../../../docs/framework/wcf/securing-services.md)
- [보안 개요](../../../docs/framework/wcf/feature-details/security-overview.md)
