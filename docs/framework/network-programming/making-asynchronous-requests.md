---
title: 비동기 요청 수행
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Internet, asynchronous access
- Networking
- asynchronous requests, Internet resources
- Network Resources
- WebRequest class, asynchronous access
ms.assetid: 735d3fce-f80c-437f-b02c-5c47f5739674
ms.openlocfilehash: 38ebe2d53bf2f22f6d28452dbc8763247382cc54
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50197166"
---
# <a name="making-asynchronous-requests"></a>비동기 요청 수행
<xref:System.Net> 클래스에서는 인터넷 리소스에 비동기적으로 액세스하기 위해 .NET Framework의 표준 비동기 프로그래밍 모델을 사용합니다. <xref:System.Net.WebRequest> 클래스의 <xref:System.Net.WebRequest.BeginGetResponse%2A> 및 <xref:System.Net.WebRequest.EndGetResponse%2A> 메서드를 통해 인터넷 리소스의 비동기 요청을 시작하고 완료합니다.  
  
> [!NOTE]
>  비동기 콜백 메서드에서 동기 호출을 사용하면 심각한 성능 저하가 발생할 수 있습니다. **WebRequest** 및 해당 종속 항목을 사용하는 인터넷 요청에서는 <xref:System.IO.Stream.BeginRead%2A?displayProperty=nameWithType>을 사용하여 <xref:System.Net.WebResponse.GetResponseStream%2A?displayProperty=nameWithType> 매서드에서 반환한 스트림을 읽어야 합니다.  
  
 다음 샘플 코드는 **WebRequest** 클래스에서 비동기 호출을 사용하는 방법을 보여 줍니다. 이 샘플은 명령줄에서 URI를 받아 URI에서 리소스를 요청한 다음 인터넷에서 수신하는 동시에 콘솔에 데이터를 인쇄하는 콘솔 프로그램입니다.  
  
 이 프로그램은 자체 용도로 두 개의 클래스를 정의합니다. 즉, 비동기 호출 전체에 데이터를 전달하는 **RequestState** 클래스와 인터넷 리소스에 비동기 요청을 구현하는 **ClientGetAsync** 클래스입니다.  
  
 **RequestState** 클래스는 요청을 처리하는 비동기 메서드 호출 전체에서 요청 상태를 유지합니다. 현재 리소스 요청과 응답으로 받은 스트림을 포함하는 **WebRequest** 및 <xref:System.IO.Stream> 인스턴스, 인터넷 리소스에서 현재 수신한 데이터를 포함하는 버퍼 및 전체 응답을 포함하는 <xref:System.Text.StringBuilder>가 포함되어 있습니다. <xref:System.AsyncCallback> 메서드를 **WebRequest.BeginGetResponse**에 등록하면 **RequestState**가 *state* 매개 변수로 전달됩니다.  
  
 **ClientGetAsync** 클래스에서 인터넷 리소스에 대한 비동기 요청을 구현하고 결과적으로 받은 응답을 콘솔에 씁니다. 다음 목록에 설명되어 있는 메서드와 속성이 포함되어 있습니다.  
  
-   `allDone` 속성에는 요청 완료를 알리는 <xref:System.Threading.ManualResetEvent> 클래스의 인스턴스가 있습니다.  
  
-   `Main()` 메서드에서 명령줄을 읽고 지정된 인터넷 리소스의 요청을 시작합니다. **WebRequest** `wreq` 및 **RequestState** `rs`를 만들고 **BeginGetResponse**를 호출하여 요청 처리를 시작한 다음 `allDone.WaitOne()` 메서드를 호출합니다. 그러면 콜백이 완료될 때까지 응용 프로그램이 종료되지 않습니다. 인터넷 리소스에서 응답을 읽은 다음 `Main()`에서 콘솔에 응답을 쓰고 응용 프로그램이 종료됩니다.  
  
-   `showusage()` 메서드를 통해 콘솔에 예제 명령줄을 씁니다. 명령줄에 URI가 제공되지 않으면 `Main()`을 통해 호출합니다.  
  
-   `RespCallBack()` 메서드에서 인터넷 요청의 비동기 콜백 메서드를 구현합니다. 인터넷 리소스에서 응답을 포함하는 **WebResponse** 인스턴스를 만들고, 응답 스트림을 가져온 다음, 스트림에서 비동기식으로 데이터 읽기를 시작합니다.  
  
-   `ReadCallBack()` 메서드에서는 응답 스트림을 읽는 비동기 콜백 메서드를 구현합니다. 인터넷 리소스에서 받은 데이터를 **RequestState** 인스턴스의 **ResponseData** 속성으로 전송한 다음, 데이터가 더 이상 반환되지 않을 때까지 응답 스트림의 또 다른 비동기 읽기를 시작합니다. 모든 데이터를 읽고 나면 `ReadCallBack()`에서 응답 스트림을 닫고 `allDone.Set()` 메서드를 호출하여 **ResponseData**에 전체 응답이 있음을 표시합니다.  
  
    > [!NOTE]
    >  모든 네트워크 스트림을 닫는 것이 중요합니다. 각 응답과 스트림을 닫지 않으면 응용 프로그램이 서버에 대한 연결을 모두 사용하여 추가 요청을 처리하지 못하게 될 수 있습니다.  
  
```csharp  
using System;  
using System.Net;  
using System.Threading;  
using System.Text;  
using System.IO;  
  
// The RequestState class passes data across async calls.  
public class RequestState  
{  
   const int BufferSize = 1024;  
   public StringBuilder RequestData;  
   public byte[] BufferRead;  
   public WebRequest Request;  
   public Stream ResponseStream;  
   // Create Decoder for appropriate enconding type.  
   public Decoder StreamDecode = Encoding.UTF8.GetDecoder();  
  
   public RequestState()  
   {  
      BufferRead = new byte[BufferSize];  
      RequestData = new StringBuilder(String.Empty);  
      Request = null;  
      ResponseStream = null;  
   }       
}  
  
// ClientGetAsync issues the async request.  
class ClientGetAsync   
{  
   public static ManualResetEvent allDone = new ManualResetEvent(false);  
   const int BUFFER_SIZE = 1024;  
  
   public static void Main(string[] args)   
   {  
      if (args.Length < 1)   
      {  
         showusage();  
         return;  
      }  
  
      // Get the URI from the command line.  
      Uri httpSite = new Uri(args[0]);  
  
      // Create the request object.  
      WebRequest wreq = WebRequest.Create(httpSite);  
  
      // Create the state object.  
      RequestState rs = new RequestState();  
  
      // Put the request into the state object so it can be passed around.  
      rs.Request = wreq;  
  
      // Issue the async request.  
      IAsyncResult r = (IAsyncResult) wreq.BeginGetResponse(  
         new AsyncCallback(RespCallback), rs);  
  
      // Wait until the ManualResetEvent is set so that the application   
      // does not exit until after the callback is called.  
      allDone.WaitOne();  
  
      Console.WriteLine(rs.RequestData.ToString());  
   }  
  
   public static void showusage() {  
      Console.WriteLine("Attempts to GET a URL");  
      Console.WriteLine("\r\nUsage:");  
      Console.WriteLine("   ClientGetAsync URL");  
      Console.WriteLine("   Example:");  
      Console.WriteLine("      ClientGetAsync http://www.contoso.com/");  
   }  
  
   private static void RespCallback(IAsyncResult ar)  
   {  
      // Get the RequestState object from the async result.  
      RequestState rs = (RequestState) ar.AsyncState;  
  
      // Get the WebRequest from RequestState.  
      WebRequest req = rs.Request;  
  
      // Call EndGetResponse, which produces the WebResponse object  
      //  that came from the request issued above.  
      WebResponse resp = req.EndGetResponse(ar);           
  
      //  Start reading data from the response stream.  
      Stream ResponseStream = resp.GetResponseStream();  
  
      // Store the response stream in RequestState to read   
      // the stream asynchronously.  
      rs.ResponseStream = ResponseStream;  
  
      //  Pass rs.BufferRead to BeginRead. Read data into rs.BufferRead  
      IAsyncResult iarRead = ResponseStream.BeginRead(rs.BufferRead, 0,   
         BUFFER_SIZE, new AsyncCallback(ReadCallBack), rs);   
   }  
  
   private static void ReadCallBack(IAsyncResult asyncResult)  
   {  
      // Get the RequestState object from AsyncResult.  
      RequestState rs = (RequestState)asyncResult.AsyncState;  
  
      // Retrieve the ResponseStream that was set in RespCallback.   
      Stream responseStream = rs.ResponseStream;  
  
      // Read rs.BufferRead to verify that it contains data.   
      int read = responseStream.EndRead( asyncResult );  
      if (read > 0)  
      {  
         // Prepare a Char array buffer for converting to Unicode.  
         Char[] charBuffer = new Char[BUFFER_SIZE];  
  
         // Convert byte stream to Char array and then to String.  
         // len contains the number of characters converted to Unicode.  
      int len =   
         rs.StreamDecode.GetChars(rs.BufferRead, 0, read, charBuffer, 0);  
  
         String str = new String(charBuffer, 0, len);  
  
         // Append the recently read data to the RequestData stringbuilder  
         // object contained in RequestState.  
         rs.RequestData.Append(  
            Encoding.ASCII.GetString(rs.BufferRead, 0, read));           
  
         // Continue reading data until   
         // responseStream.EndRead returns –1.  
         IAsyncResult ar = responseStream.BeginRead(   
            rs.BufferRead, 0, BUFFER_SIZE,   
            new AsyncCallback(ReadCallBack), rs);  
      }  
      else  
      {  
         if(rs.RequestData.Length>0)  
         {  
            //  Display data to the console.  
            string strContent;                    
            strContent = rs.RequestData.ToString();  
         }  
         // Close down the response stream.  
         responseStream.Close();           
         // Set the ManualResetEvent so the main thread can exit.  
         allDone.Set();                             
      }  
      return;  
   }      
}  
```  
  
```vb  
Imports System  
Imports System.Net  
Imports System.Threading  
Imports System.Text  
Imports System.IO  
  
' The RequestState class passes data across async calls.  
Public Class RequestState  
  
      Public RequestData As New StringBuilder("")  
      Public BufferRead(1024) As Byte  
      Public Request As HttpWebRequest  
      Public ResponseStream As Stream  
      ' Create Decoder for appropriate encoding type.  
      Public StreamDecode As Decoder = Encoding.UTF8.GetDecoder()  
  
      Public Sub New  
         Request = Nothing  
         ResponseStream = Nothing  
      End Sub  
End Class  
  
' ClientGetAsync issues the async request.  
Class ClientGetAsync  
   Shared allDone As New ManualResetEvent(False)  
      Const BUFFER_SIZE As Integer = 1024  
  
    Shared Sub Main()  
        Dim Args As String() = Environment.GetCommandLineArgs()  
  
        If Args.Length < 2 Then  
            ShowUsage()  
            Return  
        End If  
  
      ' Get the URI from the command line.  
        Dim HttpSite As Uri = New Uri(Args(1))  
  
      ' Create the request object.  
        Dim wreq As HttpWebRequest = _  
           CType(WebRequest.Create(HttpSite), HttpWebRequest)  
  
      ' Create the state object.  
      Dim rs As RequestState = New RequestState()  
  
      ' Put the request into the state so it can be passed around.  
      rs.Request = wreq  
  
      ' Issue the async request.  
        Dim r As IAsyncResult = _  
           CType(wreq.BeginGetResponse( _  
           New AsyncCallback(AddressOf RespCallback), rs), IAsyncResult)  
  
      ' Wait until the ManualResetEvent is set so that the application  
      ' does not exit until after the callback is called.  
        allDone.WaitOne()  
    End Sub  
  
    Shared Sub ShowUsage()  
        Console.WriteLine("Attempts to GET a URI")  
        Console.WriteLine()  
        Console.WriteLine("Usage:")  
        Console.WriteLine("ClientGetAsync URI")  
        Console.WriteLine("Examples:")  
        Console.WriteLine("ClientGetAsync http://www.contoso.com/")  
    End Sub  
  
    Shared Sub RespCallback(ar As IAsyncResult)  
       ' Get the RequestState object from the async result.  
       Dim rs As RequestState = CType(ar.AsyncState, RequestState)  
  
       ' Get the HttpWebRequest from RequestState.  
       Dim req As HttpWebRequest= rs.Request  
  
       ' Call EndGetResponse, which returns the HttpWebResponse object  
       ' that came from the request issued above.  
       Dim resp As HttpWebResponse = _  
           CType(req.EndGetResponse(ar), HttpWebResponse)  
  
       ' Start reading data from the respons stream.  
       Dim ResponseStream As Stream = resp.GetResponseStream()  
  
       ' Store the reponse stream in RequestState to read  
       ' the stream asynchronously.  
       rs.ResponseStream = ResponseStream  
  
       ' Pass rs.BufferRead to BeginRead. Read data into rs.BufferRead.  
       Dim iarRead As IAsyncResult = _  
          ResponseStream.BeginRead(rs.BufferRead, 0, BUFFER_SIZE, _  
          New AsyncCallback(AddressOf ReadCallBack), rs)  
    End Sub  
  
   Shared Sub ReadCallBack(asyncResult As IAsyncResult)  
      ' Get the RequestState object from the AsyncResult.  
      Dim rs As RequestState = CType(asyncResult.AsyncState, RequestState)  
  
      ' Retrieve the ResponseStream that was set in RespCallback.  
      Dim responseStream As Stream = rs.ResponseStream  
  
      ' Read rs.BufferRead to verify that it contains data.  
      Dim read As Integer = responseStream.EndRead( asyncResult )  
      If read > 0 Then  
         ' Prepare a Char array buffer for converting to Unicode.  
         Dim charBuffer(1024) As Char  
  
         ' Convert byte stream to Char array and then String.  
         ' len contains the number of characters converted to Unicode.  
         Dim len As Integer = _  
           rs.StreamDecode.GetChars(rs.BufferRead, 0, read, charBuffer, 0)  
         Dim str As String = new String(charBuffer, 0, len)      
  
         ' Append the recently read data to the RequestData stringbuilder   
         ' object contained in RequestState.  
         rs.RequestData.Append( _  
            Encoding.ASCII.GetString(rs.BufferRead, 0, read))  
  
         ' Continue reading data until responseStream.EndRead  
         ' returns –1.  
         Dim ar As IAsyncResult = _  
            responseStream.BeginRead(rs.BufferRead, 0, BUFFER_SIZE, _  
            New AsyncCallback(AddressOf ReadCallBack), rs)  
      Else  
          If rs.RequestData.Length > 1 Then  
            ' Display data to the console.  
            Dim strContent As String  
            strContent = rs.RequestData.ToString()  
            Console.WriteLine(strContent)  
         End If  
  
         ' Close down the response stream.  
         responseStream.Close()  
  
         ' Set the ManualResetEvent so the main thread can exit.  
         allDone.Set()  
      End If  
  
      Return  
   End Sub  
End Class  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터 요청](../../../docs/framework/network-programming/requesting-data.md)
