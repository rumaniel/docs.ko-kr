---
ms.openlocfilehash: a9b6af31b68c25ab58c52757f48ed23cca3f5a35
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2019
ms.locfileid: "71263329"
---
### <a name="better-argument-validation-in-the-pkcs8privatekeyinfo-constructor"></a>Pkcs8PrivateKeyInfo 생성자의 인수 유효성 검사를 개선

.Net Core 3.0 미리 보기 9부터 `Pkcs8PrivateKeyInfo` 생성자는 `algorithmParameters` 매개 변수의 유효성을 BER 인코딩된 단일 값으로 검사합니다.

#### <a name="change-description"></a>변경 내용 설명

.Net Core 3.0 미리 보기 9 이전에는 [`Pkcs8PrivateKeyInfo` 생성자](xref:System.Security.Cryptography.Pkcs.Pkcs8PrivateKeyInfo.%23ctor(System.Security.Cryptography.Oid,System.Nullable%7BSystem.ReadOnlyMemory%7BSystem.Byte%7D%7D,System.ReadOnlyMemory%7BSystem.Byte%7D,System.Boolean))가 `algorithmParameters`인수의 유효성을 검사하지 않았습니다.  이 인수가 잘못된 값을 나타내는 경우 생성자는 성공하지만 <xref:System.Security.Cryptography.Pkcs.Pkcs8PrivateKeyInfo.Encode>, <xref:System.Security.Cryptography.Pkcs.Pkcs8PrivateKeyInfo.TryEncode%2A>, <xref:System.Security.Cryptography.Pkcs.Pkcs8PrivateKeyInfo.Encrypt%2A> 또는 <xref:System.Security.Cryptography.Pkcs.Pkcs8PrivateKeyInfo.TryEncrypt%2A> 메서드를 호출할 경우 허용되지 않은 인수(`preEncodedValue`)에 대한 <xref:System.ArgumentException> 또는 <xref:System.Security.Cryptography.CryptographicException>이 throw됩니다.

미리 보기 9 이전의 .NET Core 3.0을 사용하여 실행하는 경우 <xref:System.Security.Cryptography.Pkcs.Pkcs8PrivateKeyInfo.Encode> 메서드를 호출하는 경우에만 다음 코드에서 예외를 throw합니다.

```csharp
byte[] algorithmParameters = { 0x05, 0x00, 0x05, 0x00 };

var info = new Pkcs8PrivateKeyInfo(algorithmId, algorithmParameters, privateKey);
// This line throws an ArgumentException for `preEncodedValue`:
byte[] encoded = info.Encode();
```

.NET Core 3.0 미리 보기 9부터 생성자가 인수의 유효성을 검사하여 값이 잘못된 경우 메서드가 <xref:System.Security.Cryptography.CryptographicException>을 throw합니다. 이 변경으로 인해 예외는 데이터 오류 소스에 보다 가까워집니다. 예:

```csharp
byte[] algorithmParameters = { 0x05, 0x00, 0x05, 0x00 };

// This line throws a CryptographicException
var info = new Pkcs8PrivateKeyInfo(algorithmId, algorithmParameters, privateKey);
```

#### <a name="version-introduced"></a>도입된 버전

3.0 미리 보기 9

#### <a name="recommended-action"></a>권장 작업

유효한 `algorithmParameters` 값만 제공하고 예외 처리가 필요한 경우 <xref:System.ArgumentException> 및 <xref:System.Security.Cryptography.CryptographicException> 모두에 대해 `Pkcs8PrivateKeyInfo` 생성자 테스트가 호출되도록 합니다.

### <a name="category"></a>범주

암호화

### <a name="affected-apis"></a>영향을 받는 API

- [Pkcs8PrivateKeyInfo 생성자](xref:System.Security.Cryptography.Pkcs.Pkcs8PrivateKeyInfo.%23ctor(System.Security.Cryptography.Oid,System.Nullable%7BSystem.ReadOnlyMemory%7BSystem.Byte%7D%7D,System.ReadOnlyMemory%7BSystem.Byte%7D,System.Boolean))

<!--

### Affected APIs

- `M:System.Security.Cryptography.Pkcs.Pkcs8PrivateKeyInfo.#ctor(System.Security.Cryptography.Oid,System.Nullable{System.ReadOnlyMemory{System.Byte}},System.ReadOnlyMemory{System.Byte},System.Boolean))

-->
