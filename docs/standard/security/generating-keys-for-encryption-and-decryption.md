---
title: 암호화 및 해독용 키 생성
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- keys, encryption and decryption
- keys, asymmetric
- keys, symmetric
- encryption [.NET Framework], keys
- symmetric keys
- asymmetric keys [.NET Framework]
- cryptography [.NET Framework], keys
ms.assetid: c197dfc9-a453-4226-898d-37a16638056e
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 52ec268df38a12dfe7dac469eed9901d7c0646a1
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67769610"
---
# <a name="generating-keys-for-encryption-and-decryption"></a>암호화 및 해독용 키 생성
키 만들기 및 관리는 암호화 프로세스의 중요한 부분입니다. 대칭 알고리즘을 사용할 때는 키와 IV(Initialization Vector)를 만들어야 합니다. 키는 데이터를 암호 해독해서는 안 되는 사람이 알 수 없도록 해야 합니다. IV는 기밀이어야 할 필요는 없지만 각 세션에서 변경되어야 합니다. 비대칭 알고리즘에서는 퍼블릭 키와 프라이빗 키를 만들어야 합니다. 퍼블릭 키는 모든 사용자에게 퍼블릭될 수 있는 반면, 프라이빗 키는 퍼블릭 키로 암호화된 데이터를 암호 해독하는 당사자만 알고 있어야 합니다. 이 섹션에서는 대칭 및 비대칭 알고리즘에 대한 키를 생성 및 관리하는 방법을 설명합니다.  
  
## <a name="symmetric-keys"></a>대칭 키  
 .NET Framework에서 제공하는 대칭 암호화 클래스가 데이터를 암호화 및 암호 해독하려면 키와 새 IV(초기화 벡터)가 필요합니다. 매개 변수가 없는 생성자를 사용 하 여 관리 되는 대칭 암호화 클래스 중 하나의 새 인스턴스를 만들 때마다 새 키와 IV 자동으로 만들어집니다. 데이터를 암호 해독할 수 있도록 허용하는 모든 사용자는 동일한 키와 IV를 소유하고 동일한 알고리즘을 사용해야 합니다. 일반적으로 새 키와 IV는 각 세션에 대해 생성되어야 하며, 이후 세션을 위해 키와 IV를 저장하면 안 됩니다.  
  
 대칭 키와 IV를 위치상 떨어져 있는 사용자에게 전달하려면 대개 비대칭 암호화를 사용하여 대칭 키를 암호화합니다. 이 키를 암호화하지 않은 상태로 보안되지 않은 네트워크를 통해 보내면 다른 사람이 이 키 및 IV를 가로채어 데이터를 암호 해독할 수 있기 때문에 안전하지 않습니다. 암호화를 사용하여 데이터를 교환하는 방법에 대한 자세한 내용은 [암호화 체계 만들기](../../../docs/standard/security/creating-a-cryptographic-scheme.md)를 참조하세요.  
  
 다음 예제에서는 TripleDES 알고리즘을 구현하는 <xref:System.Security.Cryptography.TripleDESCryptoServiceProvider> 클래스의 새 인스턴스를 만드는 과정을 보여 줍니다.  
  
```vb  
Dim tdes As TripleDESCryptoServiceProvider = new TripleDESCryptoServiceProvider()  
```  
  
```csharp  
TripleDESCryptoServiceProvider tdes = new TripleDESCryptoServiceProvider();  
```  
  
 이전 코드를 실행하면 새 키와 IV가 생성되어 **키** 및 **IV** 속성에 각각 배치됩니다.  
  
 여러 키를 생성해야 하는 경우도 있습니다. 이 경우 대칭 알고리즘을 구현하는 클래스의 새 인스턴스를 만든 다음 **GenerateKey** 및 **GenerateIV** 메서드를 호출하여 새 키와 IV를 만들 수 있습니다. 다음 코드 예제에는 대칭 암호화 클래스의 새 인스턴스를 만든 후 새 키와 Iv를 만드는 방법을 보여 줍니다.  
  
```vb  
Dim tdes As TripleDESCryptoServiceProvider = new TripleDESCryptoServiceProvider()  
tdes.GenerateIV()  
tdes.GenerateKey()  
```  
  
```csharp  
TripleDESCryptoServiceProvider tdes = new TripleDESCryptoServiceProvider();  
tdes.GenerateIV();  
tdes.GenerateKey();  
```  
  
 이전 코드를 실행하면 **TripleDESCryptoServiceProvider** 의 새 인스턴스를 만들 때 키와 IV가 생성됩니다. **GenerateKey** 및 **GenerateIV** 메서드를 호출할 때 다른 키와 IV가 생성됩니다.  
  
## <a name="asymmetric-keys"></a>비대칭 키  
 .NET Framework에서는 비대칭 암호화를 위해 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 및 <xref:System.Security.Cryptography.DSACryptoServiceProvider> 클래스를 제공합니다. 이러한 클래스는 매개 변수가 없는 생성자를 사용 하 여 새 인스턴스를 만들 때 공개/개인 키 쌍을 만듭니다. 비대칭 키는 여러 세션에서 사용하기 위해 저장하거나 하나의 세션에 대해서만 생성할 수 있습니다. 퍼블릭 키는 모든 사용자에게 퍼블릭될 수 있는 반면 프라이빗 키는 엄격하게 보호해야 합니다.  
  
 퍼블릭/프라이빗 키 쌍은 비대칭 알고리즘 클래스의 새 인스턴스를 만들 때마다 생성됩니다. 클래스의 새 인스턴스가 생성된 후 다음 두 메서드 중 하나를 사용하여 키 정보를 추출할 수 있습니다.  
  
- <xref:System.Security.Cryptography.RSA.ToXmlString%2A> 메서드 - 키 정보의 XML 표현을 반환합니다.  
  
- <xref:System.Security.Cryptography.RSACryptoServiceProvider.ExportParameters%2A> 메서드 - 키 정보를 보유하는 <xref:System.Security.Cryptography.RSAParameters> 구조체를 반환합니다.  
  
 두 메서드는 퍼블릭 키 정보만 반환할지 또는 퍼블릭 키와 프라이빗 키 정보를 모두 반환할지를 나타내는 부울 값을 허용합니다. **메서드를 사용하여** RSACryptoServiceProvider **클래스를** RSAParameters <xref:System.Security.Cryptography.RSACryptoServiceProvider.ImportParameters%2A> 구조체의 값으로 초기화할 수 있습니다.  
  
 비대칭 프라이빗 키는 로컬 컴퓨터에 축자로 저장하거나 일반 텍스트로 저장해서는 안 됩니다. 프라이빗 키를 저장해야 하는 경우에는 키 컨테이너를 사용해야 합니다. 키 컨테이너에 개인 키를 저장 하는 방법에 자세한 내용은 참조 하세요. [방법: 키 컨테이너에 비대칭 키 저장](../../../docs/standard/security/how-to-store-asymmetric-keys-in-a-key-container.md)합니다.  
  
 다음 코드 예제에서는 퍼블릭/프라이빗 키 쌍을 만들어 **RSACryptoServiceProvider** 클래스의 새 인스턴스를 만들고 퍼블릭 키 정보를 **RSAParameters** 구조체에 저장합니다.  
  
```vb  
'Generate a public/private key pair.  
Dim rsa as RSACryptoServiceProvider = new RSACryptoServiceProvider()  
'Save the public key information to an RSAParameters structure.  
Dim rsaKeyInfo As RSAParameters = rsa.ExportParameters(false)  
```  
  
```csharp  
//Generate a public/private key pair.  
RSACryptoServiceProvider rsa = new RSACryptoServiceProvider();  
//Save the public key information to an RSAParameters structure.  
RSAParameters rsaKeyInfo = rsa.ExportParameters(false);  
```  
  
## <a name="see-also"></a>참고자료

- [데이터 암호화](../../../docs/standard/security/encrypting-data.md)
- [데이터 해독](../../../docs/standard/security/decrypting-data.md)
- [Cryptographic Services](../../../docs/standard/security/cryptographic-services.md)
- [방법: 키 컨테이너에 비대칭 키 저장](../../../docs/standard/security/how-to-store-asymmetric-keys-in-a-key-container.md)
