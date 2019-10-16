---
title: '방법: FTP를 사용하여 파일 업로드'
description: 이 아티클에서는 FTP 서버로 파일을 업로드하는 방법의 샘플을 보여줍니다.
ms.date: 06/26/2018
dev_langs:
- csharp
- vb
ms.assetid: e40f17c5-dd12-4c62-9dbf-00ab491382dc
ms.openlocfilehash: 670bbc65078e6530cffbcfa7d324c36238014ffb
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65632815"
---
# <a name="how-to-upload-files-with-ftp"></a>방법: FTP를 사용하여 파일 업로드

이 샘플은 파일을 FTP 서버에 업로드하는 방법을 보여 줍니다.

## <a name="example"></a>예제

```csharp
using System;
using System.IO;
using System.Net;
using System.Text;

namespace Examples.System.Net
{
    public class WebRequestGetExample
    {
        public static void Main ()
        {
            // Get the object used to communicate with the server.
            FtpWebRequest request = (FtpWebRequest)WebRequest.Create("ftp://www.contoso.com/test.htm");
            request.Method = WebRequestMethods.Ftp.UploadFile;

            // This example assumes the FTP site uses anonymous logon.
            request.Credentials = new NetworkCredential("anonymous", "janeDoe@contoso.com");

            // Copy the contents of the file to the request stream.
            byte[] fileContents;
            using (StreamReader sourceStream = new StreamReader("testfile.txt"))
            {
                fileContents = Encoding.UTF8.GetBytes(sourceStream.ReadToEnd());
            }

            request.ContentLength = fileContents.Length;

            using (Stream requestStream = request.GetRequestStream())
            {
                requestStream.Write(fileContents, 0, fileContents.Length);
            }

            using (FtpWebResponse response = (FtpWebResponse)request.GetResponse())
            {
                Console.WriteLine($"Upload File Complete, status {response.StatusDescription}");
            }
        }
    }
}
```

```vb
Imports System.IO
Imports System.Net
Imports System.Text

Namespace Examples.System.Net
    Public Module WebRequestGetExample
        Public Sub Main()
            ' Get the object used to communicate with the server.
            Dim request As FtpWebRequest = CType(WebRequest.Create("ftp://www.contoso.com/test.htm"), FtpWebRequest)
            request.Method = WebRequestMethods.Ftp.UploadFile

            ' This example assumes the FTP site uses anonymous logon.
            request.Credentials = New NetworkCredential("anonymous", "janeDoe@contoso.com")

            ' Copy the contents of the file to the request stream.
            Dim fileContents As Byte()

            Using sourceStream As StreamReader = New StreamReader("testfile.txt")
                fileContents = Encoding.UTF8.GetBytes(sourceStream.ReadToEnd())
            End Using

            request.ContentLength = fileContents.Length

            Using requestStream As Stream = request.GetRequestStream()
                requestStream.Write(fileContents, 0, fileContents.Length)
            End Using

            Using response As FtpWebResponse = CType(request.GetResponse(), FtpWebResponse)
                Console.WriteLine($"Upload File Complete, status {response.StatusDescription}")
            End Using
        End Sub
    End Module
End Namespace
```
