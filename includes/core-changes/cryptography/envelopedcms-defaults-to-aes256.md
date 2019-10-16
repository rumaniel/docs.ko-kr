---
ms.openlocfilehash: f9000b19997201c2d3de0643669f9029ff1ca31c
ms.sourcegitcommit: dfd612ba454ce775a766bcc6fe93bc1d43dfda47
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2019
ms.locfileid: "72237411"
---
### <a name="envelopedcms-defaults-to-aes-256-encryption"></a>EnvelopedCms를 기본적으로 AES-256 암호화로 설정

`EnvelopedCms`에서 사용하는 기본 대칭 암호화 알고리즘이 TripleDES에서 AES-256으로 변경되었습니다.

#### <a name="change-description"></a>변경 내용 설명

.Net Core 미리 보기 7 버전 이하에서 생성자 오버로드를 통해 대칭 암호화 알고리즘을 지정하지 않고 <xref:System.Security.Cryptography.Pkcs.EnvelopedCms>가 데이터를 암호화하는 데 사용되는 경우 데이터가 TripleDES/3des/3DEA/DES3 알고리즘을 사용하여 암호화되었습니다.

.Net Core 3.0 미리 보기 8부터( [System.Security.Cryptography.Pkcs](https://www.nuget.org/packages/System.Security.Cryptography.Pkcs/) NuGet 패키지의 버전 4.6.0을 통해) 기본 알고리즘이 현대화 알고리즘용 AES-256으로 변경되어 보안 기본 옵션을 개선합니다. 메시지 받는 사람 인증서에 (EC가 아닌) Diffie-Hellman 공개 키가 있는 경우 기본 플랫폼의 제한 사항으로 인해 <xref:System.Security.Cryptography.CryptographicException>에서 암호화 작업이 실패할 수 있습니다.

다음 샘플 코드에서는 .NET Core 3.0마미리 보기 7 이전 버전에서 실행되는 경우 데이터가 TripleDES로 암호화됩니다. .NET Core 3.0 미리 보기 8 이상에서 실행되는 경우 데이터가 AES-256로 암호화됩니다.

```csharp
EnvelopedCms cms = new EnvelopedCms(content);
cms.Encrypt(recipient);
return cms.Encode();
```

#### <a name="version-introduced"></a>도입된 버전

3.0 미리 보기 8

#### <a name="recommended-action"></a>권장 작업

이 변경으로 부정적인 영향을 받는 경우 다음과 같이 <xref:System.Security.Cryptography.Pkcs.AlgorithmIdentifier> 형식의 매개 변수를 포함하는 <xref:System.Security.Cryptography.Pkcs.EnvelopedCms> 생성자에서 암호화 알고리즘 식별자를 명시적으로 지정하여 TripleDES 암호화를 복원할 수 있습니다.

```csharp
Oid tripleDesOid = new Oid("1.2.840.113549.3.7", null);
AlgorithmIdentifier tripleDesIdentifier = new AlgorithmIdentifier(tripleDesOid);
EnvelopedCms cms = new EnvelopedCms(content, tripleDesIdentifier);

cms.Encrypt(recipient);
return cms.Encode()l
```

#### <a name="category"></a>범주

암호화

#### <a name="affected-apis"></a>영향을 받는 API

- <xref:System.Security.Cryptography.Pkcs.EnvelopedCms.%23ctor?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.Pkcs.EnvelopedCms.%23ctor(System.Security.Cryptography.Pkcs.ContentInfo)?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.Pkcs.EnvelopedCms.%23ctor(System.Security.Cryptography.Pkcs.SubjectIdentifierType,System.Security.Cryptography.Pkcs.ContentInfo)?displayProperty=nameWithType>

<!--

### Affected APIs

- `M:System.Security.Cryptography.Pkcs.EnvelopedCms.#ctor`
- `M:System.Security.Cryptography.Pkcs.EnvelopedCms.#ctor(System.Security.Cryptography.Pkcs.ContentInfo)`
- `M:System.Security.Cryptography.Pkcs.EnvelopedCms.%23ctor(System.Security.Cryptography.Pkcs.SubjectIdentifierType,System.Security.Cryptography.Pkcs.ContentInfo)`

-->
