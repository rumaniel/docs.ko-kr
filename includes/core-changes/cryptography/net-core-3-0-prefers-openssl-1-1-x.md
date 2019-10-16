---
ms.openlocfilehash: b49b2f88b130bb952b77964d5bf38374dc606385
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71216342"
---
### <a name="net-core-30-prefers-openssl-11x-to-openssl-10x"></a>.NET Core 3.0은 OpenSSL 1.0.x보다 OpenSSL 1.1.x를 권장합니다.

여러 Linux 배포판에서 작동하는 Linux용 .NET Core는 OpenSSL 1.0.x와 OpenSSL 1.1.x를 모두 지원합니다.  .NET Core 2.1 및 .NET Core 2.2는 먼저 1.0.x를 찾은 다음 1.1.x로 대체합니다. .NET Core 3.0은 1.1.x부터 찾습니다. 이 변경은 새로운 암호화 표준에 대한 지원을 추가하기 위해 실시된 것입니다.

이 변경이 .NET Core에서 OpenSSL 특정 상호 작용 형식으로 플랫폼 상호 작용을 수행하는 라이브러리나 애플리케이션에 영향을 줄 수 있습니다.

#### <a name="change-description"></a>변경 내용 설명

.NET Core 2.2 버전 이하에서 런타임은 OpenSSL 1.0.x보다 1.1.x를 우선적으로 로드합니다. 이는 OpenSSL과 상호 작용을 위한 <xref:System.IntPtr> 및 <xref:System.Runtime.InteropServices.SafeHandle> 형식이 기본적으로 libcrypto.so.1.0.0 / libcrypto.so.1.0 / libcrypto.so.10에 사용된다는 의미입니다.

.Net Core 3.0부터 런타임은 OpenSSL 1.0.x보다 OpenSSL 1.1.x를 우선적으로 로드하므로 OpenSSL과 상호 작용을 위한 <xref:System.IntPtr> 및 <xref:System.Runtime.InteropServices.SafeHandle> 형식이 기본적으로 ibcrypto.so.1.1 / libcrypto.so.11 / libcrypto.so.1.1.0 / libcrypto.so.1.1.1에 사용됩니다. 따라서 OpenSSL과 직접 상호 운용되는 라이브러리 및 애플리케이션은 .NET Core 2.1 또는 .NET Core 2.2에서 업그레이드할 경우 .NET Core에 노출된 값과 호환되지 않는 포인터를 가질 수 있습니다.

#### <a name="version-introduced"></a>도입된 버전

3.0

#### <a name="recommended-action"></a>권장 작업

OpenSSL을 사용하여 직접 작업을 수행하는 라이브러리 및 애플리케이션은 .NET Core 런타임과 동일한 버전의 OpenSSL을 사용하고 있는지 확인해야 합니다.

OpenSSL을 사용하여 직접 .NET Core 암호화 형식에서 <xref:System.IntPtr> 또는 <xref:System.Runtime.InteropServices.SafeHandle> 값을 사용하는 모든 라이브러리 또는 애플리케이션은사용하는 라이브러리 버전을 새 <xref:System.Security.Cryptography.SafeEvpPKeyHandle.OpenSslVersion?displayProperty=nameWithType> 속성과 비교하여 포인터가 호환되는지 확인 해야 합니다.

#### <a name="category"></a>범주

암호화

#### <a name="affected-apis"></a>영향을 받는 API

- <xref:System.Security.Cryptography.SafeEvpPKeyHandle.%23ctor%2A?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.RSAOpenSsl.%23ctor(System.IntPtr)?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.RSAOpenSsl.%23ctor(System.Security.Cryptography.SafeEvpPKeyHandle)?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.RSAOpenSsl.DuplicateKeyHandle?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.DSAOpenSsl.%23ctor(System.IntPtr)?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.DSAOpenSsl.%23ctor(System.Security.Cryptography.SafeEvpPKeyHandle)?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.DSAOpenSsl.DuplicateKeyHandle?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.ECDsaOpenSsl.%23ctor(System.IntPtr)?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.ECDsaOpenSsl.%23ctor(System.Security.Cryptography.SafeEvpPKeyHandle)?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.ECDsaOpenSsl.DuplicateKeyHandle?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.ECDiffieHellmanOpenSsl.%23ctor(System.IntPtr)?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.ECDiffieHellmanOpenSsl.%23ctor(System.Security.Cryptography.SafeEvpPKeyHandle)?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.ECDiffieHellmanOpenSsl.DuplicateKeyHandle?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.X509Certificates.X509Certificate.Handle?displayProperty=nameWithType>

<!--

### Affected APIs

- `Overload:System.Security.Cryptography.SafeEvpPKeyHandle.#ctor`
- `M:System.Security.Cryptography.RSAOpenSsl.#ctor(System.IntPtr)`
- `M:System.Security.Cryptography.RSAOpenSsl.#ctor(System.Security.Cryptography.SafeEvpPKeyHandle)`
- `M:System.Security.Cryptography.RSAOpenSsl.DuplicateKeyHandle`
- `M:System.Security.Cryptography.DSAOpenSsl.#ctor(System.IntPtr)`
- `M:System.Security.Cryptography.DSAOpenSsl.#ctor(System.Security.Cryptography.SafeEvpPKeyHandle)`
- `M:System.Security.Cryptography.DSAOpenSsl.DuplicateKeyHandle`
- `M:System.Security.Cryptography.ECDsaOpenSsl.#ctor(System.IntPtr)`
- `M:System.Security.Cryptography.ECDsaOpenSsl.#ctor(System.Security.CryptographySafeEvpPKeyHandle)`
- `M:System.Security.Cryptography.ECDsaOpenSsl.DuplicateKeyHandle`
- `M:System.Security.Cryptography.ECDiffieHellmanOpenSsl.#ctor(System.IntPtr)`
- `M:System.Security.Cryptography.ECDiffieHellmanOpenSsl.#ctor(System.Security.Cryptography.SafeEvpPKeyHandle)`
- `M:System.Security.Cryptography.ECDiffieHellmanOpenSsl.DuplicateKeyHandle`
- `P:System.Security.Cryptography.X509Certificates.X509Certificate.Handle`

-->
