---
title: '방법: WCF 웹 HTTP 프로그래밍 모델을 사용하여 임의의 데이터를 반환하는 서비스 만들기'
ms.date: 03/30/2017
ms.assetid: 0283955a-b4ae-458d-ad9e-6fbb6f529e3d
ms.openlocfilehash: 6c7dd0debb5c491bca84ea9a4845f46b6b57b4a3
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64586239"
---
# <a name="how-to-create-a-service-that-returns-arbitrary-data-using-the-wcf-web-http-programming-model"></a>방법: WCF 웹 HTTP 프로그래밍 모델을 사용하여 임의의 데이터를 반환하는 서비스 만들기
서비스 작업에서 데이터가 반환되는 방법을 개발자가 완전히 제어해야 하는 경우가 있습니다. 이 경우 서비스 작업을 WCF에서 지원 되지 않습니다 형식으로 데이터를 반환 해야 합니다. 이 항목에서는 이러한 서비스를 만들려면 WCF 웹 HTTP 프로그래밍 모델을 사용 하 여 설명 합니다. 이 서비스에는 스트림을 반환하는 하나의 작업이 있습니다.  
  
### <a name="to-implement-the-service-contract"></a>서비스 계약을 구현하려면  
  
1. 서비스 계약을 정의합니다. 이 계약은 이름이 `IImageServer`이며 `GetImage`을 반환하는 <xref:System.IO.Stream>라는 하나의 메서드를 가집니다.  
  
    ```  
    [ServiceContract]  
        public interface IImageServer  
        {  
            [WebGet]  
            Stream GetImage(int width, int height);  
        }  
    ```  
  
     메서드 반환 하므로 <xref:System.IO.Stream>WCF 작업에는 서비스 작업에서 반환 되는 바이트를 완전히 제어 하는 것으로 가정 하 고 반환 되는 데이터를 서식 없이 적용 됩니다.  
  
2. 서비스 계약을 구현합니다. 이 계약에는 하나의 작업(`GetImage`)만 있습니다. 이 메서드는 비트맵을 생성하여 <xref:System.IO.MemoryStream>에 .jpg 형식으로 저장합니다. 그런 다음 이 작업은 해당 스트림을 호출자에 반환합니다.  
  
    ```  
    public class Service : IImageServer  
       {  
           public Stream GetImage(int width, int height)  
           {  
               Bitmap bitmap = new Bitmap(width, height);  
               for (int i = 0; i < bitmap.Width; i++)  
               {  
                   for (int j = 0; j < bitmap.Height; j++)  
                   {  
                       bitmap.SetPixel(i, j, (Math.Abs(i - j) < 2) ? Color.Blue : Color.Yellow);  
                   }  
               }  
               MemoryStream ms = new MemoryStream();  
               bitmap.Save(ms, System.Drawing.Imaging.ImageFormat.Jpeg);  
               ms.Position = 0;  
               WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";  
               return ms;  
           }  
       }  
    ```  
  
     밑에서 두 번째에 있는 코드 줄 `WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";`를 보십시오.  
  
     이 콘텐츠 형식 헤더를 설정 합니다 `"image/jpeg"`합니다. 이 샘플에서는 .jpg 파일을 반환하는 방법을 보여 주지만 코드를 수정하여 필요한 모든 종류의 데이터를 원하는 형식으로 반환할 수 있습니다. 이 작업은 데이터를 검색 또는 생성한 다음 스트림에 작성해야 합니다.  
  
### <a name="to-host-the-service"></a>서비스를 호스트하려면  
  
1. 서비스를 호스트할 콘솔 애플리케이션을 만듭니다.  
  
    ```  
    class Program  
    {  
        static void Main(string[] args)  
        {  
        }   
    }  
    ```  
  
2. `Main` 메서드 내에 서비스의 기본 주소를 저장할 변수를 만듭니다.  
  
    ```  
    string baseAddress = "http://" + Environment.MachineName + ":8000/Service";  
    ```  
  
3. 서비스 클래스 및 기본 주소를 지정하는 서비스에 대한 <xref:System.ServiceModel.ServiceHost> 인스턴스를 만듭니다.  
  
    ```  
    ServiceHost host = new ServiceHost(typeof(Service), new Uri(baseAddress));  
    ```  
  
4. <xref:System.ServiceModel.WebHttpBinding> 및 <xref:System.ServiceModel.Description.WebHttpBehavior>를 사용하여 엔드포인트를 추가합니다.  
  
    ```  
    host.AddServiceEndpoint(typeof(IImageServer), new WebHttpBinding(), "").Behaviors.Add(new WebHttpBehavior());  
    ```  
  
5. 서비스 호스트를 엽니다.  
  
    ```  
    host.Open()  
    ```  
  
6. 사용자가 Enter 키를 눌러 서비스를 종료할 때까지 기다립니다.  
  
    ```  
    Console.WriteLine("Service is running");  
    Console.Write("Press ENTER to close the host");  
    Console.ReadLine();  
    host.Close();  
    ```  
  
### <a name="to-call-the-raw-service-using-internet-explorer"></a>Internet Explorer를 사용하여 원시 서비스를 호출하려면  
  
1. 서비스를 실행하면 다음과 같은 서비스 출력이 표시됩니다. `Service is running Press ENTER to close the host`  
  
2. Internet Explorer를 열고 `http://localhost:8000/Service/GetImage?width=50&height=40`을 입력하면 파란 대각선이 중앙을 통과하는 노란 사각형이 표시됩니다.  
  
## <a name="example"></a>예제  
 다음은 이 항목에 해당되는 전체 코드 목록입니다.  
  
```  
using System;  
using System.Collections.Generic;  
using System.Text;  
using System.ServiceModel;  
using System.ServiceModel.Web;  
using System.ServiceModel.Description;  
using System.IO;  
using System.Drawing;  
  
namespace RawImageService  
{  
    // Define the service contract  
    [ServiceContract]  
    public interface IImageServer  
    {  
        [WebGet]  
        Stream GetImage(int width, int height);  
    }  
  
    // implement the service contract  
    public class Service : IImageServer  
    {  
        public Stream GetImage(int width, int height)  
        {  
            // Although this method returns a jpeg, it can be  
            // modified to return any data you want within the stream  
            Bitmap bitmap = new Bitmap(width, height);  
            for (int i = 0; i < bitmap.Width; i++)  
            {  
                for (int j = 0; j < bitmap.Height; j++)  
                {  
                    bitmap.SetPixel(i, j, (Math.Abs(i - j) < 2) ? Color.Blue : Color.Yellow);  
                }  
            }  
            MemoryStream ms = new MemoryStream();  
            bitmap.Save(ms, System.Drawing.Imaging.ImageFormat.Jpeg);  
            ms.Position = 0;  
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";  
            return ms;  
        }  
    }  
  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            string baseAddress = "http://" + Environment.MachineName + ":8000/Service";  
            ServiceHost host = new ServiceHost(typeof(Service), new Uri(baseAddress));  
            host.AddServiceEndpoint(typeof(IImageServer), new WebHttpBinding(), "").Behaviors.Add(new WebHttpBehavior());  
            host.Open();  
            Console.WriteLine("Service is running");  
            Console.Write("Press ENTER to close the host");  
            Console.ReadLine();  
            host.Close();  
  
        }  
    }  
}  
```  
  
## <a name="compiling-the-code"></a>코드 컴파일  
  
- 샘플 코드를 컴파일할 때 System.ServiceModel.dll 및 System.ServiceModel.Web.dll을 참조합니다.  
  
## <a name="see-also"></a>참고자료

- [WCF 웹 HTTP 프로그래밍 모델](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)
