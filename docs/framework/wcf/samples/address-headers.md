---
title: 주소 헤더
ms.date: 03/30/2017
ms.assetid: b0c94d4a-3bde-4b4d-bb6d-9f12bc3a6940
ms.openlocfilehash: 4ccb309178251b32068d6cdbb81874322f991bb9
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62002952"
---
# <a name="address-headers"></a>주소 헤더

Address Headers 샘플은 클라이언트 Windows Communication Foundation (WCF)를 사용 하 여 서비스에 대 한 참조 매개 변수를 전달 하는 방법 하는 방법을 보여 줍니다.

> [!NOTE]
> 이 샘플의 설치 절차 및 빌드 지침은 이 항목의 끝부분에 나와 있습니다.

WS-Addressing 사양은 특성 웹 서비스 엔드포인트의 주소를 지정하는 방법으로 엔드포인트 참조의 개념을 정의합니다. Wcf에서 끝점 참조를 사용 하 여 모델링 됩니다 합니다 `EndpointAddress` 클래스- `EndpointAddress` 의 주소 필드의 형식인는 `ServiceEndpoint` 클래스입니다.

엔드포인트 참조 모델의 일부에서 각 참조는 추가 식별 정보를 추가하는 일부 참조 매개 변수를 전달할 수 있습니다. Wcf에서 이러한 참조 매개 변수는의 인스턴스로 모델링 됩니다 `AddressHeader` 클래스입니다.

이 샘플에서 클라이언트는 클라이언트 엔드포인트의 `EndpointAddress`에 참조 매개 변수를 추가합니다. 서비스는 이 참조 매개 변수를 찾아서 "Hello" 서비스 작업의 논리에 해당 값을 사용합니다.

## <a name="client"></a>클라이언트

클라이언트는 참조 매개 변수를 보내려면 `AddressHeader`의 `EndpointAddress`에 `ServiceEndpoint`를 추가해야 합니다. `EndpointAddress` 클래스를 변경할 수 없으므로 엔드포인트 주소 수정은 `EndpointAddressBuilder` 클래스를 사용하여 수행해야 합니다. 다음 코드에서는 해당 메시지의 일부로 참조 매개 변수를 보내도록 클라이언트를 초기화합니다.

```csharp
HelloClient client = new HelloClient();
EndpointAddressBuilder builder =
    new EndpointAddressBuilder(client.Endpoint.Address);
AddressHeader header =
    AddressHeader.CreateAddressHeader(IDName, IDNamespace, "John");
builder.Headers.Add(header);
client.Endpoint.Address = builder.ToEndpointAddress();
```

이 코드는 원래 `EndpointAddressBuilder`를 초기 값으로 사용하여 `EndpointAddress`를 만듭니다. 그런 다음 새로 만든된 주소 헤더를 추가 에 대 한 호출 `CreateAddressHeader` 특정 이름, 네임 스페이스 및 값을 사용 하 여 헤더를 만듭니다. 여기서 값은 "John"입니다. 헤더가 작성기에 추가되고 나면 `ToEndpointAddress()` 메서드는 변경할 수 있는 작성기를 변경할 수 없는 엔드포인트 주소로 다시 변환하고 이 주소는 클라이언트 엔드포인트의 주소 필드에 할당됩니다.

이제 클라이언트가 `Console.WriteLine(client.Hello());`를 호출하면 클라이언트의 결과 출력에 나온 것처럼 서비스는 이 주소 매개 변수의 값을 가져올 수 있습니다.

`Hello, John`

## <a name="server"></a>서버

서비스 작업 `Hello()`의 구현에서는 현재 `OperationContext`를 사용하여 들어오는 메시지에서 헤더 값을 검사합니다.

```csharp
string id = null;
// look at headers on incoming message
for (int i = 0;
     i < OperationContext.Current.IncomingMessageHeaders.Count;
     ++i)
{
    MessageHeaderInfo h = OperationContext.Current.IncomingMessageHeaders[i];
    // for any reference parameters with the correct name & namespace
    if (h.IsReferenceParameter &&
        h.Name == IDName &&
        h.Namespace == IDNamespace)
    {
        // read the value of that header
        XmlReader xr = OperationContext.Current.IncomingMessageHeaders.GetReaderAtHeader(i);
        id = xr.ReadElementContentAsString();
    }
}
return "Hello, " + id;
```

이 코드는 들어오는 메시지의 모든 헤더를 반복하여 특정 이름을 가진 참조 매개 변수인 헤더를 찾습니다. 매개 변수가 발견되면 매개 변수의 값을 읽고 "id" 변수에 저장합니다.

#### <a name="to-set-up-build-and-run-the-sample"></a>샘플을 설치, 빌드 및 실행하려면

1. 수행 했는지 확인 합니다 [Windows Communication Foundation 샘플에 대 한 일회성 설치 절차](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)합니다.

2. C# 또는 Visual Basic .NET 버전의 솔루션을 빌드하려면 [Building the Windows Communication Foundation Samples](../../../../docs/framework/wcf/samples/building-the-samples.md)의 지침을 따릅니다.

3. 단일 또는 다중 컴퓨터 구성에서 샘플을 실행 하려면의 지침을 따릅니다 [Windows Communication Foundation 샘플 실행](../../../../docs/framework/wcf/samples/running-the-samples.md)합니다.

> [!IMPORTANT]
> 컴퓨터에 이 샘플이 이미 설치되어 있을 수도 있습니다. 계속하기 전에 다음(기본) 디렉터리를 확인하세요.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 이 디렉터리가 없으면로 이동 [Windows Communication Foundation (WCF) 및.NET Framework 4 용 Windows WF (Workflow Foundation) 샘플](https://go.microsoft.com/fwlink/?LinkId=150780) 모든 Windows Communication Foundation (WCF)를 다운로드 하 고 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 샘플. 이 샘플은 다음 디렉터리에 있습니다.
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Client\AddressHeaders`
