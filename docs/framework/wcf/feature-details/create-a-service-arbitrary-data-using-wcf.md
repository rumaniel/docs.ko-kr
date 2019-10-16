---
title: '방법: WCF REST 프로그래밍 모델을 사용하여 임의의 데이터를 허용하는 서비스 만들기'
ms.date: 03/30/2017
ms.assetid: e566c15a-b600-4e4a-be3a-4af43e767dae
ms.openlocfilehash: a1c30491f6c5b0a91f93a6f26417f9dc2b996a48
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64614793"
---
# <a name="how-to-create-a-service-that-accepts-arbitrary-data-using-the-wcf-rest-programming-model"></a>방법: WCF REST 프로그래밍 모델을 사용하여 임의의 데이터를 허용하는 서비스 만들기
서비스 작업에서 데이터가 반환되는 방법을 개발자가 완전히 제어해야 하는 경우가 있습니다. 이 경우 데이터 형식에서 지원 되지 않습니다. byWCF 서비스 작업을 반환 해야 합니다. 이 항목에서는 WCF REST 프로그래밍 모델을 사용 하 여 임의의 데이터를 받는 서비스를 만드는 것을 설명 합니다.  
  
### <a name="to-implement-the-service-contract"></a>서비스 계약을 구현하려면  
  
1. 서비스 계약을 정의합니다. 임의의 데이터를 받는 작업에는 <xref:System.IO.Stream> 형식의 매개 변수가 있어야 합니다. 또한 이 매개 변수는 요청 본문에서 전달된 유일한 매개 변수여야 합니다. 다음 예제에서 설명하는 작업은 파일 이름 매개 변수도 사용합니다. 이 매개 변수는 요청 URL 내에서 전달됩니다. <xref:System.UriTemplate>에서 <xref:System.ServiceModel.Web.WebInvokeAttribute>을 지정하여 URI 내에서 매개 변수가 전달되도록 지정할 수 있습니다. URI를 호출 하는 데이 경우이 메서드는 "UploadFile/Some-filename"에서 종료 합니다. URI 템플릿의 "{filename}" 부분은 작업을 호출 하는 데 사용 하는 URI 내에서 작업의 파일 이름 매개 변수가 전달 되도록 지정 합니다.  
  
    ```csharp  
     [ServiceContract]  
    public interface IReceiveData  
    {  
        [WebInvoke(UriTemplate = "UploadFile/{fileName}")]  
        void UploadFile(string fileName, Stream fileContents);  
    }  
    ```  
  
2. 서비스 계약을 구현합니다. 계약에는 스트림의 임의의 데이터 파일을 받는 `UploadFile`메서드만 있습니다. 작업은 읽은 바이트 수를 계산하는 스트림을 읽고 나서 파일 이름과 읽은 바이트 수를 표시합니다.  
  
    ```csharp  
    public class RawDataService : IReceiveData  
    {  
        public void UploadFile(string fileName, Stream fileContents)  
        {  
            byte[] buffer = new byte[10000];  
            int bytesRead, totalBytesRead = 0;  
            do  
            {  
                bytesRead = fileContents.Read(buffer, 0, buffer.Length);  
                totalBytesRead += bytesRead;  
            } while (bytesRead > 0);  
            Console.WriteLine("Service: Received file {0} with {1} bytes", fileName, totalBytesRead);  
        }  
    }  
    ```  
  
### <a name="to-host-the-service"></a>서비스를 호스트하려면  
  
1. 서비스를 호스트할 콘솔 애플리케이션을 만듭니다.  
  
    ```csharp  
    class Program  
    {  
       static void Main(string[] args)  
       {  
       }  
    }  
    ```  
  
2. `Main` 메서드 내에 서비스의 기본 주소를 저장할 변수를 만듭니다.  
  
    ```csharp  
    string baseAddress = "http://" + Environment.MachineName + ":8000/Service";  
    ```  
  
3. 서비스 클래스 및 기본 주소를 지정하는 서비스에 대한 <xref:System.ServiceModel.ServiceHost> 인스턴스를 만듭니다.  
  
    ```csharp  
    ServiceHost host = new ServiceHost(typeof(RawDataService), new Uri(baseAddress));  
    ```  
  
4. <xref:System.ServiceModel.WebHttpBinding>및 <xref:System.ServiceModel.Description.WebHttpBehavior>계약을 지정하는 엔드포인트를 추가합니다.  
  
    ```csharp  
    host.AddServiceEndpoint(typeof(IReceiveData), new WebHttpBinding(), "").Behaviors.Add(new WebHttpBehavior());  
    ```  
  
5. 서비스 호스트를 엽니다. 이제 서비스에서 요청을 받을 준비가 되었습니다.  
  
    ```csharp  
    host.Open();  
    Console.WriteLine("Host opened");  
    ```  
  
### <a name="to-call-the-service-programmatically"></a>서비스를 프로그래밍 방식으로 호출하려면  
  
1. 서비스를 호출하는 데 사용되는 URI를 사용하여 <xref:System.Net.HttpWebRequest>를 만듭니다. 이 코드에서 기본 주소는 `"/UploadFile/Text"`와 결합됩니다. URI의 `"UploadFile"` 부분은 호출할 작업을 지정합니다. URI의 `"Test.txt"` 부분은 `UploadFile` 작업에 전달할 파일 이름 매개 변수를 지정합니다. 이러한 항목 모두 작업 계약에 적용된 <xref:System.UriTemplate>에 매핑됩니다.  
  
    ```csharp  
    HttpWebRequest req = (HttpWebRequest)HttpWebRequest.Create(baseAddress + "/UploadFile/Test.txt");  
    ```  
  
2. <xref:System.Net.HttpWebRequest.Method%2A>의 <xref:System.Net.HttpWebRequest> 속성을 `POST`로 설정하고 <xref:System.Net.HttpWebRequest.ContentType%2A> 속성을 `"text/plain"`으로 설정합니다. 이렇게 하면 코드가 데이터를 보내고 있으며 데이터가 일반 텍스트 형식이라는 사실을 서비스에게 알립니다.  
  
    ```csharp  
    req.Method = "POST";  
    req.ContentType = "text/plain";  
    ```  
  
3. <xref:System.Net.HttpWebRequest.GetRequestStream%2A>을 호출하여 요청 스트림을 가져오고, 읽을 데이터를 만들고, 해당 데이터를 요청 스트림에 작성하고, 스트림을 닫습니다.  
  
    ```csharp  
    Stream reqStream = req.GetRequestStream();  
    byte[] fileToSend = new byte[12345];  
    for (int i = 0; i < fileToSend.Length; i++)  
       {  
           fileToSend[i] = (byte)('a' + (i % 26));  
       }  
    reqStream.Write(fileToSend, 0, fileToSend.Length);  
    reqStream.Close();  
    ```  
  
4. <xref:System.Net.HttpWebRequest.GetResponse%2A>를 호출하여 서비스에서 요청을 가져오고 응답 데이터를 콘솔에 표시합니다.  
  
    ```csharp  
    HttpWebResponse resp = (HttpWebResponse)req.GetResponse();  
    Console.WriteLine("Client: Receive Response HTTP/{0} {1} {2}", resp.ProtocolVersion, (int)resp.StatusCode, resp.StatusDescription);  
    ```  
  
5. 서비스 호스트를 닫습니다.  
  
    ```csharp  
    host.Close();  
    ```  
  
## <a name="example"></a>예제  
 다음은 이 예제에 해당되는 전체 코드 목록입니다.  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.Text;  
using System.ServiceModel;  
using System.ServiceModel.Web;  
using System.ServiceModel.Description;  
using System.IO;  
using System.Net;  
  
namespace ReceiveRawData  
{  
    [ServiceContract]  
    public interface IReceiveData  
    {  
        [WebInvoke(UriTemplate = "UploadFile/{fileName}")]  
        void UploadFile(string fileName, Stream fileContents);  
    }  
    public class RawDataService : IReceiveData  
    {  
        public void UploadFile(string fileName, Stream fileContents)  
        {  
            byte[] buffer = new byte[10000];  
            int bytesRead, totalBytesRead = 0;  
            do  
            {  
                bytesRead = fileContents.Read(buffer, 0, buffer.Length);  
                totalBytesRead += bytesRead;  
            } while (bytesRead > 0);  
            Console.WriteLine("Service: Received file {0} with {1} bytes", fileName, totalBytesRead);  
        }  
    }  
  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            string baseAddress = "http://" + Environment.MachineName + ":8000/Service";  
            ServiceHost host = new ServiceHost(typeof(RawDataService), new Uri(baseAddress));  
            host.AddServiceEndpoint(typeof(IReceiveData), new WebHttpBinding(), "").Behaviors.Add(new WebHttpBehavior());  
            host.Open();  
            Console.WriteLine("Host opened");  
  
            HttpWebRequest req = (HttpWebRequest)HttpWebRequest.Create(baseAddress + "/UploadFile/Test.txt");  
            req.Method = "POST";  
            req.ContentType = "text/plain";  
            Stream reqStream = req.GetRequestStream();  
            byte[] fileToSend = new byte[12345];  
            for (int i = 0; i < fileToSend.Length; i++)  
            {  
                fileToSend[i] = (byte)('a' + (i % 26));  
            }  
            reqStream.Write(fileToSend, 0, fileToSend.Length);  
            reqStream.Close();  
            HttpWebResponse resp = (HttpWebResponse)req.GetResponse();  
            Console.WriteLine("Client: Receive Response HTTP/{0} {1} {2}", resp.ProtocolVersion, (int)resp.StatusCode, resp.StatusDescription);  
            host.Close();  
  
        }  
    }  
}  
```  
  
## <a name="compiling-the-code"></a>코드 컴파일  
  
- 코드를 컴파일할 때 System.ServiceModel.dll 및 System.ServiceModel.Web.dll을 참조합니다.  
  
## <a name="see-also"></a>참고자료

- [UriTemplate 및 UriTemplateTable](../../../../docs/framework/wcf/feature-details/uritemplate-and-uritemplatetable.md)
- [WCF 웹 HTTP 프로그래밍 모델](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)
- [WCF 웹 HTTP 프로그래밍 모델 개요](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model-overview.md)
