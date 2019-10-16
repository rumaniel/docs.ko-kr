---
title: 사용자 지정 암호화 알고리즘 지정
ms.date: 03/30/2017
ms.assetid: d662a305-8e09-451d-9a59-b0f12b012f1d
ms.openlocfilehash: 55200732b392c15a25853af28ecdf9e32d092da4
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70849112"
---
# <a name="specifying-a-custom-crypto-algorithm"></a>사용자 지정 암호화 알고리즘 지정
WCF를 통해 데이터를 암호화하거나 디지털 서명을 연산화할 때 사용할 사용자 지정 암호화 알고리즘을 지정할 수 있습니다. 이렇게 하려면 다음 단계를 따릅니다.  
  
1. <xref:System.ServiceModel.Security.SecurityAlgorithmSuite>에서 클래스를 파생시킵니다.  
  
2. 알고리즘을 등록합니다.  
  
3. <xref:System.ServiceModel.Security.SecurityAlgorithmSuite> 파생 클래스로 바인딩을 구성합니다.  
  
## <a name="derive-a-class-from-securityalgorithmsuite"></a>SecurityAlgorithmSuite에서 클래스를 파생시킵니다.  
 <xref:System.ServiceModel.Security.SecurityAlgorithmSuite>는 다양한 보안 관련 작업을 수행할 때 사용할 알고리즘을 지정할 수 있도록 하는 추상 기본 클래스입니다. 예를 들어 디지털 서명의 해시를 계산하거나 메시지를 암호화하는 작업을 수행할 때 활용됩니다. 다음 코드에서는 <xref:System.ServiceModel.Security.SecurityAlgorithmSuite>에서 클래스를 파생하는 방법을 보여 줍니다.  
  
```csharp  
public class MyCustomAlgorithmSuite : SecurityAlgorithmSuite  
    {  
        public override string DefaultAsymmetricKeyWrapAlgorithm  
        {  
            get { return SecurityAlgorithms.RsaOaepKeyWrap; }  
        }  
  
        public override string DefaultAsymmetricSignatureAlgorithm  
        {  
            get { return SecurityAlgorithms.RsaSha1Signature; }  
        }  
  
        public override string DefaultCanonicalizationAlgorithm  
        {  
            get { return SecurityAlgorithms.ExclusiveC14n; ; }  
        }  
  
        public override string DefaultDigestAlgorithm  
        {  
            get { return SecurityAlgorithms.MyCustomHashAlgorithm; }  
        }  
  
        public override string DefaultEncryptionAlgorithm  
        {  
            get { return SecurityAlgorithms.Aes128Encryption; }  
        }  
  
        public override int DefaultEncryptionKeyDerivationLength  
        {  
            get { return 128; }  
        }  
  
        public override int DefaultSignatureKeyDerivationLength  
        {  
            get { return 128; }  
        }  
  
        public override int DefaultSymmetricKeyLength  
        {  
            get { return 128; }  
        }  
  
        public override string DefaultSymmetricKeyWrapAlgorithm  
        {  
            get { return SecurityAlgorithms.Aes128Encryption; }  
        }  
  
        public override string DefaultSymmetricSignatureAlgorithm  
        {  
            get { return SecurityAlgorithms.HmacSha1Signature; }  
        }  
  
        public override bool IsAsymmetricKeyLengthSupported(int length)  
        {  
            return length >= 1024 && length <= 4096;  
        }  
  
        public override bool IsSymmetricKeyLengthSupported(int length)  
        {  
            return length >= 128 && length <= 256;  
        }  
    }  
```  
  
## <a name="register-the-custom-algorithm"></a>사용자 지정 알고리즘을 등록합니다.  
 등록은 구성 파일이나 명령적 코드에서 수행할 수 있습니다. 암호화 서비스 공급자를 구현하는 클래스와 별칭 간의 매핑을 만들어 사용자 지정 알고리즘을 등록합니다. 그런 다음 별칭은 WCF 서비스의 바인딩에서 알고리즘을 지정할 때 사용되는 URI에 매핑됩니다. 다음 구성 코드 조각은 구성에서 사용자 지정 알고리즘을 등록하는 방법을 나타냅니다.  
  
```xml  
<configuration>  
   <mscorlib>  
      <cryptographySettings>  
         <cryptoNameMapping>  
           <cryptoClasses>  
              <cryptoClass SHA256CSP="System.Security.Cryptography.SHA256CryptoServiceProvider, System.Core, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
           </cryptoClasses>  
           <nameEntry name="http://constoso.com/CustomAlgorithms/CustomHashAlgorithm"  
              class="SHA256CSP" />  
           </cryptoNameMapping>  
        </cryptographySettings>  
    </mscorlib>  
</configuration>  
```  
  
 <`cryptoClasses`> 요소 아래에 있는 섹션에서는은 sha256cryptoserviceprovider와 별칭 "SHA256CSP" 사이에 매핑을 만듭니다. <`nameEntry`> 요소는 "SHA256CSP" 별칭과 지정 된 URL (http://constoso.com/CustomAlgorithms/CustomHashAlgorithm ) 사이에 매핑을 만듭니다.  
  
 코드로 사용자 지정 알고리즘을 등록하려면 <xref:System.Security.Cryptography.CryptoConfig.AddAlgorithm(System.Type,System.String[])> 메서드를 사용합니다. 이 메서드는 두 매핑을 모두 만듭니다. 다음 예제에서는 이 메서드를 호출하는 방법을 보여 줍니다.  
  
```csharp
// Register the custom URI string defined for the hashAlgorithm in MyCustomAlgorithmSuite class to create the   
// SHA256CryptoServiceProvider hash algorithm object.  
CryptoConfig.AddAlgorithm(typeof(SHA256CryptoServiceProvider), "http://constoso.com/CustomAlgorithms/CustomHashAlgorithm");  
```  
  
## <a name="configure-the-binding"></a>바인딩 구성  
 다음 코드 조각과 같이 바인딩 설정에서 사용자 지정 <xref:System.ServiceModel.Security.SecurityAlgorithmSuite> 파생 클래스를 지정하여 바인딩을 구성합니다.  
  
```csharp  
WSHttpBinding binding = new WSHttpBinding();  
            binding.Security.Message.AlgorithmSuite = new MyCustomAlgorithmSuite();  
```  
  
 전체 코드 예제를 보려면 [WCF 보안 샘플의 암호화 민첩성](../samples/cryptographic-agility-in-wcf-security.md) 을 참조 하세요.  
  
## <a name="see-also"></a>참고자료

- [서비스 및 클라이언트에 보안 설정](../feature-details/securing-services-and-clients.md)
- [서비스에 보안 설정](../securing-services.md)
- [보안 개요](../feature-details/security-overview.md)
- [보안 개념](../feature-details/security-concepts.md)
