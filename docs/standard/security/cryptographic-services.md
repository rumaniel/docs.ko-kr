---
title: 암호화 서비스
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- cryptography [.NET Framework]
- pattern of derived class inheritance
- digital signatures
- asymmetric cryptographic algorithms
- digital signatures, public-key systems
- public keys
- decryption [.NET Framework]
- private keys
- MAC algorithms
- cryptographic algorithms
- private keys, overview
- encryption [.NET Framework]
- security [.NET Framework], encryption
- cryptographic services
- symmetric cryptographic algorithms
- hash
- message authentication codes
- derived class inheritance
- cryptography [.NET Framework], about
- random number generation
ms.assetid: f96284bc-7b73-44b5-ac59-fac613ad09f8
author: mairaw
ms.author: mairaw
ms.openlocfilehash: c026174e881768af245860d1b719184dc47f1798
ms.sourcegitcommit: d6e27023aeaffc4b5a3cb4b88685018d6284ada4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67663993"
---
# <a name="cryptographic-services"></a>암호화 서비스

<a name="top"></a> 인터넷과 같은 공용 네트워크에서는 엔터티 간의 보안 통신 수단을 제공하지 않습니다. 이러한 네트워크를 통한 통신은 권한이 없는 제3자가 읽거나 심지어는 수정하기도 쉽습니다. 암호화는 데이터를 볼 수 없도록 보호하며 데이터가 수정되었는지 감지하는 방법을 제공하며 기타 보안상 위험한 채널을 통한 안전한 통신 수단 제공을 지원합니다. 예를 들어 데이터를 암호화된 상태로 전송하고 나중에 의도된 당사자가 해독하는 암호화 알고리즘을 사용하여 데이터를 암호화할 수 있습니다. 제3자가 암호화된 데이터를 가로채는 경우 해독하기 어렵습니다.

.NET Framework에서 <xref:System.Security.Cryptography?displayProperty=nameWithType> 네임스페이스의 클래스는 고유한 여러 암호화 세부 정보를 관리합니다. 이러한 클래스 중 일부는 관리되지 않는 Microsoft CryptoAPI(암호화 API)에 대한 래퍼이지만, 나머지는 완전하게 관리되는 구현 클래스입니다. 이러한 클래스를 사용하기 위해 암호화 전문가가 될 필요는 없습니다. 암호화 알고리즘 클래스 중 하나의 새 인스턴스를 만들 경우 키가 사용 편의를 위해 자동으로 생성되며, 기본 속성은 가능한 한 안전합니다.

이 개요에는 암호화 메서드 및 ClickOnce 매니페스트, Suite B 및.NET Framework 3.5에 도입 된 CNG Cryptography Next Generation () 지원을 포함 하 여.NET Framework에서 지 원하는 사례 개요를 제공 합니다.

이 개요는 다음과 같은 단원으로 구성됩니다.

- [암호화 기본](#primitives)

- [비밀 키 암호화](#secret_key)

- [공개 키 암호화](#public_key)

- [Digital Signatures](#digital_signatures)

- [해시 값](#hash_values)

- [Random Number Generation](#random_numbers)

- [ClickOnce 매니페스트](#clickonce)

- [Suite B 지원](#suite_b)

- [관련 항목](#related_topics)

Microsoft 서비스, 구성 요소 및 애플리케이션에 암호화 보안을 추가할 수 있도록 하는 도구 및 암호화에 대한 자세한 내용은 이 설명서의 Win32 및 COM 개발, 보안 섹션을 참조하세요.

<a name="primitives"></a>

## <a name="cryptographic-primitives"></a>암호화 기본

암호화가 사용되는 일반적인 상황에서 두 당사자(Alice와 Bob)는 보안상 위험한 채널을 통해 통신하고 있습니다. Alice와 Bob은 통신을 수신할 수도 있는 다른 사용자가 계속해서 둘 간의 통신을 이해할 수 없도록 하려고 합니다. 게다가 Alice와 Bob은 원격 위치에 있으므로 Alice는 Bob으로부터 받은 정보가 전송 중 다른 사용자에 의해 수정되지 않았는지 확인해야 합니다. 또한 그녀는 정보가 Bob을 가장하는 사람이 아니라 실제로 Bob에서 온 것임을 확인해야 합니다.

암호화는 다음과 같은 목표를 달성하기 위해 사용됩니다.

- 기밀성: 사용자의 id 또는 데이터를 읽지 못하게 보호할 수 있습니다.

- 데이터 무결성: 데이터를에서 보호 하기 위해 다음을 변경 합니다.

- 인증: 데이터가 특정 당사자 로부터 온 것임을 확인 합니다.

- 부인 방지: 특정 파티를 메시지 보낸 사실을 부인 하지 못하도록 합니다.

이러한 목표를 달성하기 위해 암호화 기본이라고 알려진 알고리즘과 방법을 결합하여 암호화 체계를 만들 수 있습니다. 다음 표는 암호화 기본 및 해당 기능 목록을 보여 줍니다.

|암호화 기본|사용|
|-----------------------------|---------|
|비밀 키 암호화(대칭 암호화)|데이터에서 변환을 수행하여 제3자가 읽지 못하게 합니다. 이 유형의 암호화는 공유된 하나의 비밀 키를 사용하여 데이터를 암호화하고 해독합니다.|
|공개 키 암호화(비대칭 암호화)|데이터에서 변환을 수행하여 제3자가 읽지 못하게 합니다. 이 유형의 암호화는 퍼블릭/프라이빗 키 쌍을 사용하여 데이터를 암호화하고 해독합니다.|
|암호화 서명|특정 당사자에 고유한 디지털 서명을 만들어 데이터가 해당 당사자로부터 온 것임을 확인할 수 있도록 지원합니다. 또한 이 프로세스는 해시 함수도 사용합니다.|
|암호화 해시|데이터를 임의 길이에서 고정 길이의 바이트 시퀀스로 매핑합니다. 해시는 통계적으로 고유합니다. 서로 다른 2바이트 시퀀스는 같은 값으로 해시하지 않습니다.|

[맨 위로 이동](#top)

<a name="secret_key"></a>

## <a name="secret-key-encryption"></a>비밀 키 암호화

비밀 키 암호화 알고리즘은 하나의 비밀 키를 사용하여 데이터를 암호화하고 해독합니다. 키를 가진 사람은 누구나 키를 사용하여 데이터를 해독하거나 자신의 데이터를 암호화한 다음 출처를 가장할 수 있으므로 권한이 없는 다른 사용자가 키에 액세스할 수 없도록 보호해야 합니다.

또한 비밀 키 암호화는 동일한 키가 암호화 및 해독에 사용되므로 대칭 암호화라고도 합니다. 비밀 키 암호화 알고리즘은 공개 키 알고리즘과 비교하여 매우 빠르며, 대규모 데이터 스트림에 대해 암호화 변환을 수행하는 데 매우 적합합니다. RSA와 같은 비대칭 암호화 알고리즘은 암호화할 수 있는 데이터 양에 있어 수학적으로 제한됩니다. 일반적으로 대칭 암호화 알고리즘에는 이러한 문제가 없습니다.

블록 암호라고 하는 비밀 키 알고리즘의 유형은 한 번에 한 데이터 블록을 암호화하는 데 사용합니다. DES(데이터 암호화 표준), TripleDES 및 AES(Advanced Encryption Standard)와 같은 블록 암호는 *n* 바이트의 입력 블록을 암호화된 바이트의 출력 블록으로 암호화하여 변환합니다. 바이트 시퀀스를 암호화하거나 해독하려는 경우 작업을 블록 단위로 수행해야 합니다. *n* 이 작기(DES 및 TripleDES의 경우 8바이트, AES의 경우 16바이트[기본값], 24바이트 또는 32바이트) 때문에 *n* 보다 큰 데이터 값은 한 번에 한 블록씩 암호화되어야 합니다. *n* 보다 작은 데이터 값은 처리하려면 *n* 으로 확장해야 합니다.

블록 암호의 한 가지 간단한 형태는 ECB(Electronic CodeBook) 모드라고 합니다. ECB 모드는 첫 번째 일반 텍스트 블록을 초기화하는 데 초기화 벡터를 사용하지 않으므로 안전하지 않은 것으로 간주됩니다. 비밀 키 *k*가 주어진 경우 초기화 벡터를 사용하지 않는 단순 블록 암호는 일반 텍스트의 동일한 입력 블록을 암호 텍스트의 동일한 출력 블록으로 암호화합니다. 따라서 입력 일반 텍스트 스트림에 중복된 블록이 있는 경우 출력 암호 텍스트 스트림에도 중복된 블록이 생성됩니다. 이러한 중복 출력 블록을 통해 권한이 없는 사용자가 취약한 암호화 알고리즘이 사용되었다는 사실과 가능한 공격 방식을 알게 됩니다. 따라서 ECB 암호화 모드는 분석에 매우 취약하므로 키가 노출될 수 있습니다.

기본 클래스 라이브러리에 제공되는 블록 암호 클래스에서는 CBC(Cipher Block Chaining)라는 기본 체인 모드를 사용하며, 필요에 따라 이 기본 모드를 변경할 수 있습니다.

CBC 암호화에서는 IV(Initialization Vector)를 사용하여 일반 텍스트의 첫 번째 블록을 암호화함으로써 ECB 암호화와 관련된 문제를 해결합니다. 일반 텍스트의 각 후속 블록은 암호화되기 전에 이전 암호 텍스트 블록과 배타적 비트 OR(`XOR`) 연산을 수행합니다. 따라서 각 암호 텍스트 블록은 이전 모든 블록에 종속됩니다. 이 시스템을 사용하는 경우 권한이 없는 사용자에게 알려질 수 있는 일반적인 메시지 헤더를 사용해서는 키를 리버스 엔지니어링할 수 없습니다.

CBC 암호화로 암호화된 데이터를 손상시킬 수 있는 한 가지 방법은 가능한 모든 키에 대해 철저한 검색을 수행하는 것입니다. 암호화 수행에 사용된 키의 크기에 따라 가장 빠른 컴퓨터를 사용해도 이러한 철저한 검색에는 많은 시간이 걸리므로 이 방법은 실제로 불가능합니다. 키 크기가 클수록 해독이 더 어려워집니다. 이론적으로 암호화를 통해 악의적 사용자가 암호화된 데이터를 검색할 수 없도록 할 수는 있지만, 그러면 비용이 증가합니다. 며칠 동안만 유용한 데이터를 검색하기 위해 3개월에 걸쳐 철저한 검색을 수행한다면 철저한 검색 방법은 실용적이지 않습니다.

비밀 키 암호화의 단점은 두 당사자가 키 및 IV에 대해 동의하고 해당 값을 통신했다고 추정하는 것입니다. IV는 비밀로 간주되지 않으며 메시지와 함께 일반 텍스트로 전송할 수 있습니다. 그러나 키는 권한이 없는 사용자에게 비밀로 유지되어야 합니다. 이러한 문제 때문에 비밀 키 암호화는 키와 IV의 값을 비밀리에 교환하는 공개 키 암호화와 함께 사용되는 경우가 많습니다.

Alice와 bob은 안전 하지 않은 채널을 통해 통신 하려는 두 당사자가 가정 같이 비밀 키 암호화를 사용할 수 있습니다. Alice와 bob은 특정 키와 IV를 사용 하 여 하나의 특정 알고리즘 (예: AES)을 사용 하도록 동의 합니다. Alice는 메시지를 작성 하 고를 메시지를 보낼 네트워크 스트림 (아마도 명명 된 파이프 또는 네트워크 메일)를 만듭니다. 그런 다음 키와 IV를 사용하여 텍스트를 암호화하고 인트라넷을 통해 Bob에게 암호화된 메시지와 IV를 전송합니다. Bob은 암호화된 텍스트를 수신하고 IV와 미리 동의한 키를 사용하여 텍스트를 해독합니다. 악의적 사용자가 이러한 전송을 중간에 가로채도 키를 알 수 없으므로 원본 메시지를 복구할 수 없습니다. 이 시나리오에서는 키만 비밀로 유지하면 됩니다. 실제 시나리오에서는 Alice 또는 Bob 중 한 사람이 비밀 키를 생성하고 공개 키(비대칭) 암호화를 사용하여 비밀(대칭) 키를 상대방에게 전송합니다. 공개 키 암호화에 대한 자세한 내용은 다음 섹션을 참조하세요.

.NET Framework는 비밀 키 암호화 알고리즘을 구현 하는 다음 클래스를 제공 합니다.

- <xref:System.Security.Cryptography.AesManaged> (.NET Framework 3.5에 도입 됨).

- <xref:System.Security.Cryptography.DESCryptoServiceProvider>.

- <xref:System.Security.Cryptography.HMACSHA1> (비밀 키와 결합된 암호화 해시 함수를 사용하여 계산된 메시지 인증 코드를 나타내므로 기술적으로 비밀 키 알고리즘입니다. 이 항목의 뒷부분에 있는 [해시 값](#hash_values)을 참조하세요.)

- <xref:System.Security.Cryptography.RC2CryptoServiceProvider>.

- <xref:System.Security.Cryptography.RijndaelManaged>.

- <xref:System.Security.Cryptography.TripleDESCryptoServiceProvider>.

[맨 위로 이동](#top)

<a name="public_key"></a>

## <a name="public-key-encryption"></a>공개 키 암호화

퍼블릭 키 암호화에서는 권한이 없는 사용자에게 비밀로 유지되어야 하는 프라이빗 키와 모든 사람에게 퍼블릭될 수 있는 퍼블릭 키를 사용합니다. 퍼블릭 키와 프라이빗 키는 수학적으로 연결되어 있습니다. 퍼블릭 키로 암호화된 데이터는 해당 프라이빗 키로만 해독할 수 있으며, 프라이빗 키로 서명된 데이터는 해당 퍼블릭 키로만 확인할 수 있습니다. 퍼블릭 키는 모든 사람이 사용할 수 있습니다. 퍼블릭 키는 프라이빗 키의 보유자에게 보낼 데이터를 암호화하는 데 사용됩니다. 공개 키 암호화 알고리즘은 데이터를 암호화하는 데 필요한 키와 해독하는 데 필요한 키가 서로 다르므로 비대칭 알고리즘이라고도 합니다. 기본적인 암호화 규칙은 키 재사용을 금지하며, 두 키가 모두 각 통신 세션에 고유해야 합니다. 그러나 실제로는, 일반적으로 비대칭 키가 수명이 깁니다.

두 당사자 (Alice와 Bob)는 공개 키 암호화를 다음과 같이 사용 될 수 있습니다. 먼저 alice가 공개/개인 키 쌍을 생성합니다. Bob은 Alice에게 암호화된 메시지를 보내려는 경우 Alice의 공개 키를 묻습니다. Alice는 안전하지 않은 네트워크를 통해 Bob에게 공개 키를 보내고 Bob은 이 키를 사용하여 메시지를 암호화합니다. Bob은 암호화된 메시지를 Alice에게 보내고 Alice는 자신의 프라이빗 키를 사용하여 메시지를 해독합니다. Bob이 공용 네트워크와 같은 안전하지 않은 채널을 통해 Alice의 키를 받은 경우 Bob은 메시지 가로채기(man-in-the-middle) 공격에 노출될 수 있습니다. 따라서 Bob은 자신이 공개 키의 정확한 복사본을 가졌는지 Alice에게 확인해야 합니다.

Alice의 공개 키를 전송하는 동안 권한이 없는 제3자가 키를 가로챌 수 있습니다. 또한 동일한 제3자가 Bob으로부터 암호화된 메시지를 가로챌 수도 있습니다. 그러나 제3자는 공개 키를 사용하여 메시지를 해독할 수 없습니다. 전송되지 않은 Alice의 프라이빗 키를 사용해서만 메시지를 해독할 수 있습니다. Alice는 Bob에게 보내는 회신 메시지를 암호화하는 데 자신의 프라이빗 키를 사용하지 않습니다. 퍼블릭 키를 가진 사람이 해당 메시지를 해독할 수 있기 때문입니다. Alice가 Bob에게 메시지를 다시 보내려는 경우 Bob에게 그의 공개 키를 묻고 해당 공개 키를 사용하여 메시지를 암호화합니다. 그러면 Bob은 자신의 연결된 프라이빗 키를 사용하여 메시지를 해독합니다.

이 시나리오에서 Alice와 Bob은 공개 키(비대칭) 암호화를 사용하여 비밀(대칭) 키를 전송하고 나머지 세션에 비밀 키 암호화를 사용합니다.

다음은 공개 키와 비밀 키 암호화 알고리즘을 비교한 목록입니다.

- 공개 키 암호화 알고리즘에서는 고정 버퍼 크기를 사용하는 반면 비밀 키 암호화 알고리즘에서는 가변 길이 버퍼를 사용합니다.

- 공개 키 알고리즘에서는 적은 양의 데이터만 암호화할 수 있으므로 비밀 키 알고리즘과 같이 데이터를 스트림으로 결합하는 데 사용할 수는 없습니다. 따라서 비대칭 작업에서는 대칭 작업에서와 동일한 스트리밍 모델을 사용하지 않습니다.

- 공개 키 암호화는 비밀 키 암호화보다 키 공간(키에 사용할 수 있는 값의 범위)이 훨씬 큽니다. 따라서 공개 키 암호화는 가능한 모든 키를 시도하는 철저한 공격에 덜 취약합니다.

- 보낸 사람의 ID를 확인할 방법이 몇 가지 있다면 공개 키는 보호할 필요가 없으므로 손쉽게 배포할 수 있습니다.

- 디지털 서명을 생성하는 데 일부 공개 키 알고리즘(예: RSA 및 DSA 단, Diffie-Hellman 제외)을 사용하면 데이터를 보낸 사람의 ID를 확인할 수 있습니다.

- 공개 키 알고리즘은 비밀 키 알고리즘과 비교하면 매우 느리므로 대규모 데이터를 암호화할 때는 적합하지 않습니다. 공개 키 알고리즘은 매우 적은 양의 데이터를 전송하는 데만 유용합니다. 일반적으로 공개 키 암호화는 비밀 키 알고리즘에서 사용하는 키 및 IV를 암호화하는 데 사용합니다. 키 및 IV가 전송되면 비밀 키 암호화가 나머지 세션에서 사용됩니다.

.NET Framework는 공개 키 암호화 알고리즘을 구현 하는 다음 클래스를 제공 합니다.

- <xref:System.Security.Cryptography.DSACryptoServiceProvider>

- <xref:System.Security.Cryptography.RSACryptoServiceProvider>

- <xref:System.Security.Cryptography.ECDiffieHellman> (기본 클래스)

- <xref:System.Security.Cryptography.ECDiffieHellmanCng>

- <xref:System.Security.Cryptography.ECDiffieHellmanCngPublicKey> (기본 클래스)

- <xref:System.Security.Cryptography.ECDiffieHellmanKeyDerivationFunction> (기본 클래스)

- <xref:System.Security.Cryptography.ECDsaCng>

RSA는 암호화 및 서명에서 모두 사용할 수 있지만, DSA는 서명에만 사용할 수 있고 Diffie-Hellman은 키 생성에만 사용할 수 있습니다. 일반적으로 퍼블릭 키 알고리즘은 비밀 키 알고리즘보다 용도가 제한됩니다.

[맨 위로 이동](#top)

<a name="digital_signatures"></a>

## <a name="digital-signatures"></a>디지털 서명

공개 키 알고리즘은 디지털 서명을 만드는 데도 사용할 수 있습니다. 디지털 서명은 보낸 사람의 공개 키를 신뢰하는 경우 보낸 사람의 ID를 인증하고, 데이터 무결성 보호를 지원합니다. Alice의 데이터를 받는 사람은 Alice가 생성한 공개 키를 사용하여 해당 디지털 서명을 Alice의 데이터 및 공개 키와 비교함으로써 Alice가 해당 데이터를 보냈는지 확인할 수 있습니다.

공개 키 암호화를 사용하여 메시지에 디지털 서명을 추가하기 위해 Alice는 먼저 메시지에 해시 알고리즘을 적용하여 메시지 다이제스트를 만듭니다. 이 메시지 다이제스트는 데이터의 압축된 고유 표현입니다. 그런 다음 Alice는 자신의 프라이빗 키를 사용하여 메시지 다이제스트를 암호화하고 자신의 개인 서명을 만듭니다. Bob은 메시지와 서명을 받으면 Alice의 공개 키를 사용하여 서명을 해독하고 메시지 다이제스트를 복구하고 Alice가 사용한 것과 동일한 해시 알고리즘을 사용하여 메시지를 해시합니다. Bob이 계산한 메시지 다이제스트가 Alice로부터 받은 메시지 다이제스트와 정확히 일치하면 Bob은 해당 메시지가 프라이빗 키의 소유자로부터 왔으며 데이터가 수정되지 않았음을 확인할 수 있습니다. Bob이 프라이빗 키의 소유자가 Alice임을 신뢰하는 경우 해당 메시지를 Alice가 보냈음을 알게 됩니다.

> [!NOTE]
> 보낸 사람의 공개 키는 공개된 정보이고 일반적으로 디지털 서명 형식에 포함되므로 누구나 서명을 확인할 수 있습니다. 이 방법이 메시지의 기밀성을 유지하지는 않으므로 메시지의 기밀을 위해서는 메시지에 대한 암호화도 수행해야 합니다.

.NET Framework는 디지털 서명 알고리즘을 구현 하는 다음 클래스를 제공 합니다.

- <xref:System.Security.Cryptography.DSACryptoServiceProvider>

- <xref:System.Security.Cryptography.RSACryptoServiceProvider>

- <xref:System.Security.Cryptography.ECDsa> (기본 클래스)

- <xref:System.Security.Cryptography.ECDsaCng>

 [맨 위로 이동](#top)

<a name="hash_values"></a>

## <a name="hash-values"></a>해시 값

해시 알고리즘은 임의 길이의 이진 값을 해시 값으로 알려진 고정된 길이의 더욱 작은 이진 값에 매핑합니다. 해시 값은 데이터 부분을 숫자로 나타낸 값입니다. 일반 텍스트 단락을 해시하고 단락의 한 문자만 변경해도 그다음 해시는 다른 값을 생성합니다. 해시가 강력하게 암호화되면 해당 값이 크게 변경됩니다. 예를 들어 메시지 중 1비트만 변경되어도 강력한 해시 함수는 50%까지 다른 출력을 생성할 수 있습니다. 여러 입력 값이 동일한 출력 값으로 해시될 수 있습니다. 그러나 동일한 값으로 해시되는 두 개의 고유한 입력을 찾는 것은 계산상 불가능합니다.

두 당사자, Alice와 Bob은 해시 함수를 사용하여 메시지 무결성을 보장할 수 있습니다. 이를 위해 메시지에 서명할 해시 알고리즘을 선택합니다. Alice는 메시지를 작성한 후 선택한 알고리즘을 사용하여 해당 메시지의 해시를 만듭니다. 그런 다음 아래 방법 중 하나를 따릅니다.

- Alice는 일반 텍스트 메시지와 해시된 메시지(디지털 서명)를 Bob에게 보냅니다. Bob은 메시지를 받아 해시하고 자신의 해시 값과 Alice로부터 받은 해시 값을 비교합니다. 해시 값이 동일하면 메시지가 변경되지 않은 것입니다. 값이 동일하지 않으면 Alice가 메시지를 작성한 후 해당 메시지가 변경된 것입니다.

  하지만 이 방법이 보낸 사람의 신뢰성을 보장하지는 않습니다. 다른 사람이 Alice를 가장하여 Bob에게 메시지를 보낼 수도 있습니다. Alice와 Bob이 동일한 해시 알고리즘을 사용하여 메시지에 서명할 수 있는데 이때 Bob은 메시지와 해당 서명이 일치한다는 사실만 확인하면 됩니다. 이는 메시지 가로채기(man-in-the-middle) 공격의 한 가지 형태입니다. 자세한 내용은 [세대 CNG (Cryptography Next) 보안 통신 예제](https://docs.microsoft.com/previous-versions/cc488018(v=vs.100))합니다.

- Alice가 비보안 공용 채널을 통해 Bob에게 일반 텍스트 메시지를 보냅니다. 그리고 보안 개인 채널을 통해 Bob에게 해시된 메시지를 보냅니다. Bob은 일반 텍스트 메시지를 받아 해시하고, 이 해시를 개인 채널로 교환된 해시와 비교합니다. 해시가 일치하면 Bob은 다음 두 가지 사실을 알게 됩니다.

  - 메시지가 변경되지 않았습니다.

  - 메시지를 보낸 사람(Alice)이 인증되었습니다.

  이 시스템이 작동되려면 Alice가 Bob을 제외한 모든 사람에게 원본 해시 값을 숨겨야 합니다.

- Alice가 비보안 공용 채널을 통해 Bob에게 일반 텍스트 메시지를 보내고 공개적으로 볼 수 있는 자신의 웹 사이트에 해시된 메시지를 게시합니다.

  이 방법을 사용하면 아무도 해시 값을 수정할 수 없으므로 메시지 변조를 방지할 수 있습니다. 메시지와 해당 해시를 아무나 읽을 수 있지만, 해시 값은 Alice만 변경할 수 있습니다. Alice를 가장하려는 공격자는 Alice의 웹 사이트에 액세스할 수 있어야 합니다.

이러한 방법 중 어떠한 방법을 사용해도 일반 텍스트로 전송되는 Alice의 메시지를 다른 사람이 읽지 못하게 할 수는 없습니다. 일반적으로 완벽한 보안을 구현하려면 디지털 서명(메시지 서명)과 암호화가 필요합니다.

.NET Framework는 해시 알고리즘을 구현 하는 다음 클래스를 제공 합니다.

- <xref:System.Security.Cryptography.HMACSHA1>.

- <xref:System.Security.Cryptography.MACTripleDES>.

- <xref:System.Security.Cryptography.MD5CryptoServiceProvider>.

- <xref:System.Security.Cryptography.RIPEMD160>.

- <xref:System.Security.Cryptography.SHA1Managed>.

- <xref:System.Security.Cryptography.SHA256Managed>.

- <xref:System.Security.Cryptography.SHA384Managed>.

- <xref:System.Security.Cryptography.SHA512Managed>.

- 모든 SHA(Secure Hash Algorithm), MD5(Message Digest 5) 및 RIPEMD-160 알고리즘의 HMAC 변형

- 모든 SHA 알고리즘의 CryptoServiceProvider 구현(관리 코드 래퍼)

- 모든 MD5 및 SHA 알고리즘의 CNG(Cryptography Next Generation) 구현

> [!NOTE]
> 1996년에 MD5 디자인 결함이 발견되었으므로 대신 SHA-1을 사용하는 것이 좋습니다. 2004년에 결함이 추가로 발견되어 MD5 알고리즘은 더 이상 안전한 것으로 간주되지 않습니다. SHA-1 알고리즘에서도 보안 결함이 발견되었으므로 이제는 SHA-2를 대신 사용하는 것이 좋습니다.

[맨 위로 이동](#top)

<a name="random_numbers"></a>

## <a name="random-number-generation"></a>난수 생성

난수 생성은 여러 암호화 작업에 필수적입니다. 예를 들어 암호화 키는 재현이 불가능하도록 가능한 한 무작위적이어야 합니다. 암호화 난수 생성기는 계산상 1/2 이상의 확률로 예측할 수 없는 출력을 생성해야 합니다. 따라서 어떠한 다음 출력 비트 예측 방법도 임의 추측보다 더 잘 예측할 수 없어야 합니다. .NET Framework의 클래스는 난수 생성기를 사용 하 여 암호화 키를 생성 합니다.

<xref:System.Security.Cryptography.RNGCryptoServiceProvider> 클래스는 난수 생성기 알고리즘을 구현한 것입니다.

[맨 위로 이동](#top)

<a name="clickonce"></a>

## <a name="clickonce-manifests"></a>ClickOnce 매니페스트

.NET Framework 3.5에서는 다음과 같은 암호화 클래스 가져오고 사용 하 여 배포 된 응용 프로그램 매니페스트 서명에 대 한 정보를 확인할 수 있습니다 [ClickOnce 기술을](/visualstudio/deployment/clickonce-security-and-deployment):

- <xref:System.Security.Cryptography.ManifestSignatureInformation> 클래스의 <xref:System.Security.Cryptography.ManifestSignatureInformation.VerifySignature%2A> 메서드 오버로드를 사용할 경우 매니페스트 서명에 대한 정보를 가져올 수 있습니다.

- <xref:System.Security.ManifestKinds> 열거형을 사용하여 확인할 매니페스트를 지정할 수 있습니다. 확인 결과는 <xref:System.Security.Cryptography.SignatureVerificationResult> 열거형 값 중 하나입니다.

- <xref:System.Security.Cryptography.ManifestSignatureInformationCollection> 클래스는 확인된 서명의 읽기 전용 <xref:System.Security.Cryptography.ManifestSignatureInformation> 개체 컬렉션을 제공합니다.

 또한 다음 클래스는 특정 서명 정보를 제공합니다.

- <xref:System.Security.Cryptography.StrongNameSignatureInformation> 은 매니페스트의 강력한 이름 서명 정보를 보유합니다.

- <xref:System.Security.Cryptography.X509Certificates.AuthenticodeSignatureInformation> 은 매니페스트의 Authenticode 서명 정보를 나타냅니다.

- <xref:System.Security.Cryptography.X509Certificates.TimestampInformation> 에는 Authenticode 서명의 타임스탬프에 대한 정보가 있습니다.

- <xref:System.Security.Cryptography.X509Certificates.TrustStatus> 는 Authenticode 서명을 신뢰할 수 있는지 확인할 수 있는 간단한 방법을 제공합니다.

[맨 위로 이동](#top)

<a name="suite_b"></a>

## <a name="suite-b-support"></a>Suite B 지원

.NET Framework 3.5에서 NSA National Security Agency ()를 게시 하는 암호화 알고리즘의 Suite B 집합을 지원 합니다. Suite B에 대한 자세한 내용은 [NSA Suite B Cryptography Fact Sheet](https://www.nsa.gov/what-we-do/information-assurance/)를 참조하세요.

다음 알고리즘이 포함되어 있습니다.

- 암호화의 경우 키 크기가 128, 192 및 256비트인 AES(Advanced Encryption Standard) 알고리즘

- 해시의 경우 SHA(Secure Hash Algorithm)-1, SHA-256, SHA-384 및 SHA-512. 일반적으로 마지막 세 알고리즘을 함께 묶어 SHA-2라고 합니다.

- 서명의 경우 256비트, 384비트 및 521비트 소수법 곡선을 사용하는 ECDSA(Elliptic Curve Digital Signature Algorithm). NSA 문서에서는 이러한 곡선을 구체적으로 정의하여 P-256, P-384 및 P-521로 호칭합니다. 이 알고리즘은 <xref:System.Security.Cryptography.ECDsaCng> 클래스에서 제공합니다. 이를 통해 프라이빗 키로 서명하고 퍼블릭 키로 서명을 확인할 수 있습니다.

- 키 교환 및 비밀 계약의 경우 256비트, 384비트 및 521비트 소수법 곡선을 사용하는 ECDH(Elliptic Curve Diffie-Hellman) 알고리즘. 이 알고리즘은 <xref:System.Security.Cryptography.ECDiffieHellmanCng> 클래스에서 제공합니다.

AES, SHA-256, SHA-384 및 SHA-512 구현에 대한 FIPS(Federal Information Processing Standard) 인증 구현의 관리 코드 래퍼는 새로운 <xref:System.Security.Cryptography.AesCryptoServiceProvider>, <xref:System.Security.Cryptography.SHA256CryptoServiceProvider>, <xref:System.Security.Cryptography.SHA384CryptoServiceProvider>및 <xref:System.Security.Cryptography.SHA512CryptoServiceProvider> 클래스에서 사용할 수 있습니다.

[맨 위로 이동](#top)

<a name="cng"></a>

## <a name="cryptography-next-generation-cng-classes"></a>CNG(Cryptography Next Generation) 클래스

CNG(Cryptography Next Generation) 클래스는 네이티브 CNG 함수 관련 관리 래퍼를 제공합니다. CNG는 CryptoAPI를 대체합니다. 이러한 클래스의 이름에는 "Cng"가 포함되어 있습니다. CNG 래퍼 클래스의 핵심은 CNG 키의 스토리지 및 사용을 추상화하는 <xref:System.Security.Cryptography.CngKey> 키 컨테이너 클래스입니다. 이 클래스를 통해 키 쌍 또는 공개 키를 안전하게 저장하고 간단한 문자열 이름을 사용하여 참조할 수 있습니다. 타원 곡선 기반 <xref:System.Security.Cryptography.ECDsaCng> 서명 클래스 및 <xref:System.Security.Cryptography.ECDiffieHellmanCng> 암호화 클래스는 <xref:System.Security.Cryptography.CngKey> 개체를 사용할 수 있습니다.

<xref:System.Security.Cryptography.CngKey> 클래스는 키 열기, 생성, 삭제, 내보내기 등의 다양한 추가 작업에 사용됩니다. 또한 네이티브 함수를 직접 호출할 때 사용할 기본 키 핸들에 대한 액세스를 제공합니다.

.NET Framework 3.5에는 다양 한 지원 CNG 클래스는 다음과 같은 포함 됩니다.

- <xref:System.Security.Cryptography.CngProvider> 는 키 저장소 공급자를 유지 관리합니다.

- <xref:System.Security.Cryptography.CngAlgorithm> 은 CNG 알고리즘을 유지 관리합니다.

- <xref:System.Security.Cryptography.CngProperty> 는 자주 사용되는 키 속성을 유지 관리합니다.

[맨 위로 이동](#top)

<a name="related_topics"></a>

## <a name="related-topics"></a>관련 항목

|제목|설명|
|-----------|-----------------|
|[암호화 모델](../../../docs/standard/security/cryptography-model.md)|기본 클래스 라이브러리에서 암호화가 구현되는 방식에 대해 설명합니다.|
|[연습: 암호화 응용 프로그램 만들기](../../../docs/standard/security/walkthrough-creating-a-cryptographic-application.md)|기본 암호화 및 해독 작업을 보여 줍니다.|
|[암호화 클래스 구성](../../../docs/framework/configure-apps/configure-cryptography-classes.md)|암호화 클래스에 알고리즘 이름을 매핑하고 암호화 알고리즘에 개체 식별자를 매핑하는 방법에 대해 설명합니다.|
