---
ms.openlocfilehash: 2fb980c8b75e25ba347c56ccc1c90f2959e83e21
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71216338"
---
### <a name="minimum-size-for-rsaopenssl-key-generation-has-increased"></a>RSAOpenSsl 키 생성 최소 크기가 증가

Linux에서 새 RSA 키를 생성하기 위한 최소 크기가 384비트에서 512비트로 증가했습니다.

#### <a name="change-description"></a>변경 내용 설명

.NET Core 3.0부터는 Linux의 <xref:System.Security.Cryptography.RSA.Create%2A?displayProperty=nameWithType>, <xref:System.Security.Cryptography.RSAOpenSsl.%23ctor%2A?displayProperty=nameWithType> 및 <xref:System.Security.Cryptography.RSACryptoServiceProvider.%23ctor%2A?displayProperty=nameWithType>에서 RSA 인스턴스의 `LegalKeySizes` 속성이 보고하는 합법적인 최소 키 크기가 384에서 512로 증가했습니다.

따라서 .NET Core 2.2 버전 이하에서는 `RSA.Create(384)` 같은 메서드 호출이 성공합니다. .Net Core 3.0 버전 이상에서 메서드 호출 `RSA.Create(384)`는 크기가 너무 작음을 나타내는 예외를 throw합니다.

이 변경은 Linux에서 암호화 작업을 수행하는 OpenSSL이 버전 1.0.2와 1.1.0 간에 최소값을 상향했기 때문에 적용된 것입니다. .NET Core 3.0은 OpenSSL 1.0.x보다 1.1.x를 기본으로 적용하고, 이 높아진 새 종속성 제한을 반영하기 위해 보고된 최소 버전이 상향되었습니다.

#### <a name="version-introduced"></a>도입된 버전

3.0

#### <a name="recommended-action"></a>권장 작업

영향을 받는 API를 호출하는 경우 생성된 키의 크기가 공급자 최소값보다 작지 않은지 확인하세요.

> [!NOTE]
> 384비트 RSA는 이미 안전하지 않은 것으로 간주됩니다(512비트 RSA도 마찬가지). [NIST 특별 간행물 800-57 1부 수정 버전 4](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r4.pdf)와 같은 최신 권장 사항은 새로 생성된 키에 대한 최소 크기로 2048 비트를 제안합니다.

#### <a name="category"></a>범주

암호화

#### <a name="affected-apis"></a>영향을 받는 API

- <xref:System.Security.Cryptography.AsymmetricAlgorithm.LegalKeySizes?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.RSA.Create%2A?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.RSAOpenSsl.%23ctor%2A?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.RSACryptoServiceProvider.%23ctor%2A?displayProperty=nameWithType>

<!--
### Affected APIs

- `P:System.Security.Cryptography.AsymmetricAlgorithm.LegalKeySizes`
- `Overload:System.Security.Cryptography.RSA.Create`
- `Overload:System.Security.Cryptography.RSAOpenSsl.#ctor`
- `Overload:System.Security.Cryptography.RSACryptoServiceProvider.#ctor`

-->
