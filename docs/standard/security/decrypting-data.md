---
title: 데이터 해독
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data [.NET Framework], decryption
- symmetric decryption
- asymmetric decryption
- decryption
ms.assetid: 9b266b6c-a9b2-4d20-afd8-b3a0d8fd48a0
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 4cf0ffae2c5803324d4941581855d5dc10224e07
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61795228"
---
# <a name="decrypting-data"></a>데이터 해독

암호 해독은 암호화의 반대 작업입니다. 비밀 키 암호화의 경우 데이터를 암호화하는 데 사용된 키 및 IV를 모두 알고 있어야 합니다. 퍼블릭 키 암호화의 경우 퍼블릭 키(프라이빗 키를 사용하여 데이터가 암호화된 경우) 또는 프라이빗 키(퍼블릭 키를 사용하여 데이터가 암호화된 경우)를 알고 있어야 합니다.

## <a name="symmetric-decryption"></a>대칭 암호 해독

대칭 알고리즘을 사용하여 암호화된 데이터의 암호 해독은 대칭 알고리즘을 사용하여 데이터를 암호화하는 데 사용된 프로세스와 비슷합니다. <xref:System.Security.Cryptography.CryptoStream> 클래스는 .NET Framework에서 제공하는 대칭 암호화 클래스와 함께 모든 관리되는 스트림 개체에서 읽은 데이터를 암호 해독하는 데 사용됩니다.

다음 예제에서는 <xref:System.Security.Cryptography.RijndaelManaged> 클래스의 새 인스턴스를 만들고 <xref:System.Security.Cryptography.CryptoStream> 개체에서 암호 해독을 수행하는 데 사용하는 방법을 보여 줍니다. 이 예제에서는 먼저 **RijndaelManaged** 클래스의 새 인스턴스를 만듭니다. 그런 다음 **CryptoStream** 개체를 만들고 `myStream`이라는 관리되는 스트림의 값으로 초기화합니다. **RijndaelManaged** 클래스의 **CreateDecryptor** 메서드에 암호화에 사용된 것과 동일한 키 및 IV가 전달된 후 메서드가 **CryptoStream** 생성자에 전달됩니다. 끝으로, **CryptoStreamMode.Read** 열거형이 **CryptoStream** 생성자에 전달되어 스트림에 대한 읽기 권한을 지정합니다.

```vb
Dim rmCrypto As New RijndaelManaged()
Dim cryptStream As New CryptoStream(myStream, rmCrypto.CreateDecryptor(rmCrypto.Key, rmCrypto.IV), CryptoStreamMode.Read)
```

```csharp
RijndaelManaged rmCrypto = new RijndaelManaged();
CryptoStream cryptStream = new CryptoStream(myStream, rmCrypto.CreateDecryptor(Key, IV), CryptoStreamMode.Read);
```

다음 예제에서는 스트림을 만들고, 스트림을 암호 해독하고, 스트림에서 읽고, 스트림을 닫는 전체 프로세스를 보여 줍니다. 수신 대기하는 개체에 연결할 때 네트워크 스트림을 초기화하는 <xref:System.Net.Sockets.TcpListener> 개체가 생성됩니다. 그런 다음 **CryptoStream** 클래스 및 **RijndaelManaged** 클래스를 사용하여 네트워크 스트림을 암호 해독합니다. 이 예제에서는 키 및 IV 값이 성공적으로 전송되었거나 이전에 합의되었다고 가정합니다. 이러한 값을 암호화 및 전송하는 데 필요한 코드는 표시되지 않습니다.

```vb
Imports System
Imports System.Net.Sockets
Imports System.Threading
Imports System.IO
Imports System.Net
Imports System.Security.Cryptography

Module Module1
    Sub Main()
            'The key and IV must be the same values that were used
            'to encrypt the stream.
            Dim key As Byte() = {&H1, &H2, &H3, &H4, &H5, &H6, &H7, &H8, &H9, &H10, &H11, &H12, &H13, &H14, &H15, &H16}
            Dim iv As Byte() = {&H1, &H2, &H3, &H4, &H5, &H6, &H7, &H8, &H9, &H10, &H11, &H12, &H13, &H14, &H15, &H16}
        Try
            'Initialize a TCPListener on port 11000
            'using the current IP address.
            Dim tcpListen As New TcpListener(IPAddress.Any, 11000)

            'Start the listener.
            tcpListen.Start()

            'Check for a connection every five seconds.
            While Not tcpListen.Pending()
                Console.WriteLine("Still listening. Will try in 5 seconds.")

                Thread.Sleep(5000)
            End While

            'Accept the client if one is found.
            Dim tcp As TcpClient = tcpListen.AcceptTcpClient()

            'Create a network stream from the connection.
            Dim netStream As NetworkStream = tcp.GetStream()

            'Create a new instance of the RijndaelManaged class
            'and decrypt the stream.
            Dim rmCrypto As New RijndaelManaged()

            'Create an instance of the CryptoStream class, pass it the NetworkStream, and decrypt
            'it with the Rijndael class using the key and IV.
            Dim cryptStream As New CryptoStream(netStream, rmCrypto.CreateDecryptor(key, iv), CryptoStreamMode.Read)

            'Read the stream.
            Dim sReader As New StreamReader(cryptStream)

            'Display the message.
            Console.WriteLine("The decrypted original message: {0}", sReader.ReadToEnd())

            'Close the streams.
            sReader.Close()
            netStream.Close()
            tcp.Close()
            'Catch any exceptions.
        Catch
            Console.WriteLine("The Listener Failed.")
        End Try
    End Sub
End Module
```

```csharp
using System;
using System.Net.Sockets;
using System.Threading;
using System.IO;
using System.Net;
using System.Security.Cryptography;

class Class1
{
   static void Main(string[] args)
   {
      //The key and IV must be the same values that were used
      //to encrypt the stream.
      byte[] key = {0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x10, 0x11, 0x12, 0x13, 0x14, 0x15, 0x16};
      byte[] iv = {0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x10, 0x11, 0x12, 0x13, 0x14, 0x15, 0x16};
      try
      {
         //Initialize a TCPListener on port 11000
         //using the current IP address.
         TcpListener tcpListen = new TcpListener(IPAddress.Any, 11000);

         //Start the listener.
         tcpListen.Start();

         //Check for a connection every five seconds.
         while(!tcpListen.Pending())
         {
            Console.WriteLine("Still listening. Will try in 5 seconds.");
            Thread.Sleep(5000);
         }

         //Accept the client if one is found.
         TcpClient tcp = tcpListen.AcceptTcpClient();

         //Create a network stream from the connection.
         NetworkStream netStream = tcp.GetStream();

         //Create a new instance of the RijndaelManaged class
         // and decrypt the stream.
         RijndaelManaged rmCrypto = new RijndaelManaged();

         //Create a CryptoStream, pass it the NetworkStream, and decrypt
         //it with the Rijndael class using the key and IV.
         CryptoStream cryptStream = new CryptoStream(netStream,
            rmCrypto.CreateDecryptor(key, iv),
            CryptoStreamMode.Read);

         //Read the stream.
         StreamReader sReader = new StreamReader(cryptStream);

         //Display the message.
         Console.WriteLine("The decrypted original message: {0}", sReader.ReadToEnd());

         //Close the streams.
         sReader.Close();
         netStream.Close();
         tcp.Close();
      }
      //Catch any exceptions.
      catch
      {
         Console.WriteLine("The Listener Failed.");
      }
   }
}
```

이전 샘플이 작동하려면 수신기에 대한 암호화된 연결이 필요합니다. 연결이 수신기에 사용된 것과 동일한 키, IV 및 알고리즘을 사용해야 합니다. 이러한 연결이 설정되면 메시지가 암호 해독되고 콘솔에 표시됩니다.

## <a name="asymmetric-decryption"></a>비대칭 암호 해독

일반적으로 당사자(당사자 A)는 퍼블릭 키와 프라이빗 키를 둘 다 생성하고 메모리 또는 암호화 키 컨테이너에 키를 저장합니다. 당사자 A가 다른 당사자(당사자 B)에게 공개 키를 보냅니다. 공개 키를 사용 하 여 당사자 B 데이터를 암호화 및 파티 A로 다시 데이터를 보내 파티 A는 데이터를 받은 후 해당 하는 개인 키를 사용 하 여 해독 합니다. 암호 해독은 당사자 A가 당사자 B에서 데이터를 암호화하는 데 사용한 퍼블릭 키에 해당하는 프라이빗 키를 사용하는 경우에만 성공합니다.

나중에 비대칭 키를 검색 하는 방법과 안전한 암호화 키 컨테이너에 있는 비대칭 키를 저장 하는 방법에 대 한 정보에 대 한 참조 [방법: 키 컨테이너에 비대칭 키 저장](../../../docs/standard/security/how-to-store-asymmetric-keys-in-a-key-container.md)합니다.

다음 예제에서는 대칭 키 및 IV를 나타내는 두 바이트 배열의 암호 해독을 보여 줍니다. 제3자에게 쉽게 보낼 수 있는 형식으로 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 개체에서 비대칭 공개 키를 추출하는 방법에 대한 자세한 내용은 [Encrypting Data](../../../docs/standard/security/encrypting-data.md)이라는 관리되는 스트림의 값으로 초기화합니다.

```vb
'Create a new instance of the RSACryptoServiceProvider class.
Dim rsa As New RSACryptoServiceProvider()

' Export the public key information and send it to a third party.
' Wait for the third party to encrypt some data and send it back.

'Decrypt the symmetric key and IV.
symmetricKey = rsa.Decrypt(encryptedSymmetricKey, False)
symmetricIV = rsa.Decrypt(encryptedSymmetricIV, False)
```

```csharp
//Create a new instance of the RSACryptoServiceProvider class.
RSACryptoServiceProvider rsa = new RSACryptoServiceProvider();

// Export the public key information and send it to a third party.
// Wait for the third party to encrypt some data and send it back.

//Decrypt the symmetric key and IV.
symmetricKey = rsa.Decrypt(encryptedSymmetricKey, false);
symmetricIV = rsa.Decrypt(encryptedSymmetricIV , false);
```

## <a name="see-also"></a>참고자료

- [암호화 및 해독용 키 생성](../../../docs/standard/security/generating-keys-for-encryption-and-decryption.md)
- [데이터 암호화](../../../docs/standard/security/encrypting-data.md)
- [Cryptographic Services](../../../docs/standard/security/cryptographic-services.md)
