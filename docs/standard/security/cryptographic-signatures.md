---
title: 암호화 서명
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- digital signatures
- cryptography [.NET Framework], signatures
- digital signatures, XML signing
- signatures, cryptographic
- digital signatures, generating
- verifying signatures
- generating signatures
- digital signatures, about
- encryption [.NET Framework], signatures
- security [.NET Framework], signatures
- XML signing
- digital signatures, verifying
- signing XML
ms.assetid: aa87cb7f-e608-4a81-948b-c9b8a1225783
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 862d520073dde1b935510bc7c68782c1204c6111
ms.sourcegitcommit: 09d699aca28ae9723399bbd9d3d44aa0cbd3848d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68331646"
---
# <a name="cryptographic-signatures"></a>암호화 서명

<a name="top"></a> 암호화 디지털 서명은 public 키 알고리즘을 사용하여 데이터 무결성을 제공합니다. 디지털 서명으로 데이터에 서명하면 다른 사용자가 서명을 확인하고 데이터가 원래 서명자로부터 시작되고 서명자가 서명한 이후 변경되지 않았음을 증명할 수 있습니다. 디지털 서명에 대한 자세한 내용은 [Cryptographic Services](../../../docs/standard/security/cryptographic-services.md)를 참조하세요.

이 항목에서는 <xref:System.Security.Cryptography?displayProperty=nameWithType> 네임스페이스의 클래스를 사용하여 디지털 서명을 생성 및 확인하는 방법을 설명합니다.

- [서명 생성](#generate)

- [서명 확인](#verify)

<a name="generate"></a>

## <a name="generating-signatures"></a>서명 생성

일반적으로 디지털 서명은 더 큰 데이터를 나타내는 해시 값에 적용됩니다. 다음 예제에서는 해시 값에 디지털 서명을 적용합니다. 먼저 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 클래스의 새 인스턴스는 public/private 키 쌍을 생성합니다. 다음으로 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 는 <xref:System.Security.Cryptography.RSAPKCS1SignatureFormatter> 클래스의 새 인스턴스에 전달됩니다. 실제로 디지털 서명을 수행하는 <xref:System.Security.Cryptography.RSAPKCS1SignatureFormatter>에 private 키를 전달합니다. 해시 코드에 서명하기 전에 사용할 해시 알고리즘을 지정해야 합니다. 이 예제에서는 SHA1 알고리즘을 사용합니다. 마지막으로 <xref:System.Security.Cryptography.AsymmetricSignatureFormatter.CreateSignature%2A> 메서드가 호출되어 서명을 수행합니다.

S h a 1의 충돌 문제로 인해 s h a 1 이상을 권장 합니다.

```vb
Imports System
Imports System.Security.Cryptography

Module Module1
    Sub Main()
        'The hash value to sign.
        Dim hashValue As Byte() = {59, 4, 248, 102, 77, 97, 142, 201, 210, 12, 224, 93, 25, 41, 100, 197, 213, 134, 130, 135}

        'The value to hold the signed value.
        Dim signedHashValue() As Byte

        'Generate a public/private key pair.
        Dim rsa As New RSACryptoServiceProvider()

        'Create an RSAPKCS1SignatureFormatter object and pass it
        'the RSACryptoServiceProvider to transfer the private key.
        Dim rsaFormatter As New RSAPKCS1SignatureFormatter(rsa)

        'Set the hash algorithm to SHA1.
        rsaFormatter.SetHashAlgorithm("SHA1")

        'Create a signature for hashValue and assign it to
        'signedHashValue.
        signedHashValue = rsaFormatter.CreateSignature(hashValue)
    End Sub
End Module
```

```csharp
using System;
using System.Security.Cryptography;

class Class1
{
   static void Main()
   {
      //The hash value to sign.
      byte[] hashValue = {59,4,248,102,77,97,142,201,210,12,224,93,25,41,100,197,213,134,130,135};

      //The value to hold the signed value.
      byte[] signedHashValue;

      //Generate a public/private key pair.
      RSACryptoServiceProvider rsa = new RSACryptoServiceProvider();

      //Create an RSAPKCS1SignatureFormatter object and pass it the
      //RSACryptoServiceProvider to transfer the private key.
      RSAPKCS1SignatureFormatter rsaFormatter = new RSAPKCS1SignatureFormatter(rsa);

      //Set the hash algorithm to SHA1.
      rsaFormatter.SetHashAlgorithm("SHA1");

      //Create a signature for hashValue and assign it to
      //signedHashValue.
      signedHashValue = rsaFormatter.CreateSignature(hashValue);
   }
}
```

### <a name="signing-xml-files"></a>XML 파일에 서명

.NET Framework는 XML에 서명하는 데 사용되는 <xref:System.Security.Cryptography.Xml> 네임스페이스를 제공합니다. XML이 특정 소스에서 시작되는지 확인하려면 XML에 서명해야 합니다. 예를 들어 XML을 사용하는 주식 시세 서비스를 이용하고 있다면 서명된 XML의 소스를 확인할 수 있습니다.

이 네임스페이스의 클래스는 World Wide Web 컨소시엄의 [XML 서명 구문 및 처리 권장 사항](https://www.w3.org/TR/xmldsig-core/) 을 따릅니다.

[맨 위로 이동](#top)

<a name="verify"></a>

## <a name="verifying-signatures"></a>서명 확인

특정 당사자가 데이터에 서명했는지 확인하려면 다음 정보가 있어야 합니다.

- 데이터에 서명한 당사자의 public 키입니다.

- 디지털 서명입니다.

- 서명된 데이터입니다.

- 서명자가 사용한 해시 알고리즘입니다.

<xref:System.Security.Cryptography.RSAPKCS1SignatureFormatter> 클래스로 서명된 서명을 확인하려면 <xref:System.Security.Cryptography.RSAPKCS1SignatureDeformatter> 클래스를 사용합니다. <xref:System.Security.Cryptography.RSAPKCS1SignatureDeformatter> 클래스에는 서명자의 public 키가 제공되어야 합니다. public 키를 지정하려면 모듈러스 및 지수의 값이 필요합니다. public/private 키 쌍을 생성한 당사자가 이들 값을 제공해야 합니다. 먼저 서명을 확인할 public 키를 저장할 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 개체를 만들고 <xref:System.Security.Cryptography.RSAParameters> 구조체를 공개 키를 지정하는 모듈러스 및 지수 값으로 초기화합니다.

다음 코드는 <xref:System.Security.Cryptography.RSAParameters> 구조체를 만드는 방법을 보여 줍니다. `Modulus` 속성은 `modulusData` 바이트 배열 값으로 설정되고 `Exponent` 속성은 `exponentData`바이트 배열 값으로 설정됩니다.

```vb
Dim rsaKeyInfo As RSAParameters
rsaKeyInfo.Modulus = modulusData
rsaKeyInfo.Exponent = exponentData
```

```csharp
RSAParameters rsaKeyInfo;
rsaKeyInfo.Modulus = modulusData;
rsaKeyInfo.Exponent = exponentData;
```

<xref:System.Security.Cryptography.RSAParameters> 개체를 만든 후에 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 클래스의 새 인스턴스를 <xref:System.Security.Cryptography.RSAParameters>에 지정된 값으로 초기화할 수 있습니다. <xref:System.Security.Cryptography.RSACryptoServiceProvider> 가 다시 <xref:System.Security.Cryptography.RSAPKCS1SignatureDeformatter> 의 생성자에 전달되어 키를 전송합니다.

다음 예제에서는 이 프로세스를 보여 줍니다. 이 예제에서 `hashValue` 및 `signedHashValue` 는 원격 당사자가 제공한 바이트 배열입니다. 원격 당사자는 `hashValue` 를 생성하는 SHA1 알고리즘을 사용하여 `signedHashValue`에 서명했습니다. 메서드 <xref:System.Security.Cryptography.RSAPKCS1SignatureDeformatter.VerifySignature%2A?displayProperty=nameWithType> 는 디지털 서명이 유효 하 고에 `hashValue`서명 하는 데 사용 되었는지 확인 합니다.

```vb
Dim rsa As New RSACryptoServiceProvider()
rsa.ImportParameters(rsaKeyInfo)
Dim rsaDeformatter As New RSAPKCS1SignatureDeformatter(rsa)
rsaDeformatter.SetHashAlgorithm("SHA1")
If rsaDeformatter.VerifySignature(hashValue, signedHashValue) Then
   Console.WriteLine("The signature is valid.")
Else
   Console.WriteLine("The signature is not valid.")
End If
```

```csharp
RSACryptoServiceProvider rsa = new RSACryptoServiceProvider();
rsa.ImportParameters(rsaKeyInfo);
RSAPKCS1SignatureDeformatter rsaDeformatter = new RSAPKCS1SignatureDeformatter(rsa);
rsaDeformatter.SetHashAlgorithm("SHA1");
if(rsaDeformatter.VerifySignature(hashValue, signedHashValue))
{
   Console.WriteLine("The signature is valid.");
}
else
{
   Console.WriteLine("The signature is not valid.");
}
```

이 코드 조각은 서명이 유효하면 "`The signature is valid`"를 표시하고, 유효하지 않으면 "`The signature is not valid`"를 표시합니다.

## <a name="see-also"></a>참고자료

- [Cryptographic Services](../../../docs/standard/security/cryptographic-services.md)
