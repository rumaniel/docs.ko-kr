---
title: .NET Framework 암호화 모델
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- cryptography [.NET Framework], model
- encryption [.NET Framework], model
ms.assetid: 12fecad4-fbab-432a-bade-2f05976a2971
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 42e5c7018f83f3849f46f33e09e09ea1749e7c70
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64753290"
---
# <a name="net-framework-cryptography-model"></a>.NET Framework 암호화 모델

.NET Framework에서는 많은 표준 암호화 알고리즘의 구현을 제공합니다. 이러한 알고리즘은 사용하기 쉽고 가능한 가장 안전한 기본 속성을 포함합니다. 또한 개체 상속, 스트림 디자인 및 구성의 .NET Framework 암호화 모델은 크게 확장할 수 있습니다.

## <a name="object-inheritance"></a>개체 상속

.NET Framework 보안 시스템은 파생 클래스 상속의 확장명 가능한 패턴을 구현합니다. 계층 구조는 다음과 같습니다.

- <xref:System.Security.Cryptography.SymmetricAlgorithm>, <xref:System.Security.Cryptography.AsymmetricAlgorithm> 또는 <xref:System.Security.Cryptography.HashAlgorithm>과 같은 알고리즘 형식 클래스. 이 수준은 추상 클래스입니다.

- 알고리즘 형식 클래스에서 상속되는 알고리즘 클래스. 예를 들어 <xref:System.Security.Cryptography.Aes>, <xref:System.Security.Cryptography.RC2> 또는 <xref:System.Security.Cryptography.ECDiffieHellman>입니다. 이 수준은 추상 클래스입니다.

- 알고리즘 클래스에서 상속되는 알고리즘 클래스의 구현. 예를 들어 <xref:System.Security.Cryptography.AesManaged>, <xref:System.Security.Cryptography.RC2CryptoServiceProvider> 또는 <xref:System.Security.Cryptography.ECDiffieHellmanCng>입니다. 이 수준은 완전히 구현됩니다.

이 패턴의 파생 클래스를 사용하면 새로운 알고리즘 또는 기존 알고리즘의 새 구현을 쉽게 추가할 수 있습니다. 예를 들어 새로운 공용 키 알고리즘을 만들려면 <xref:System.Security.Cryptography.AsymmetricAlgorithm> 클래스에서 상속합니다. 특정 알고리즘의 새 구현을 만들려면 해당 알고리즘의 비추상 파생 클래스를 만듭니다.

## <a name="how-algorithms-are-implemented-in-the-net-framework"></a>.NET Framework에서 알고리즘이 구현되는 방식

알고리즘에 사용할 수 있는 다양한 구현의 예로 대칭 알고리즘을 고려해 보세요. 모든 대칭 알고리즘의 기본은 <xref:System.Security.Cryptography.SymmetricAlgorithm>으로, 다음 알고리즘에 상속됩니다.

1. <xref:System.Security.Cryptography.Aes>

2. <xref:System.Security.Cryptography.DES>

3. <xref:System.Security.Cryptography.RC2>

4. <xref:System.Security.Cryptography.Rijndael>

5. <xref:System.Security.Cryptography.TripleDES>

<xref:System.Security.Cryptography.Aes>는 두 클래스 <xref:System.Security.Cryptography.AesCryptoServiceProvider> 및 <xref:System.Security.Cryptography.AesManaged>에 상속됩니다. <xref:System.Security.Cryptography.AesCryptoServiceProvider> 클래스는 Aes의 Windows CAPI(암호화 API) 구현에 대한 래퍼인 반면, <xref:System.Security.Cryptography.AesManaged> 클래스는 완전히 관리 코드로 작성됩니다. 관리되는 구현 및 CAPI 구현 외에도 세 번째 유형의 구현인 CNG(Cryptography Next Generation)가 있습니다. CNG 알고리즘의 한 예는 <xref:System.Security.Cryptography.ECDiffieHellmanCng>입니다. CNG 알고리즘은 Windows Vista 이상에서 사용할 수 있습니다.

가장 적합한 구현을 선택할 수 있습니다.  관리되는 구현은 .NET Framework를 지원하는 모든 플랫폼에서 사용할 수 있습니다.  CAPI 구현은 이전 운영 체제에서 사용할 수 있으며 더 이상 개발되지 않습니다. CNG는 새로운 개발이 수행되는 최신 구현입니다. 그러나 관리되는 구현은 FIPS(Federal Information Processing Standards)에서 인증되지 않았으며 래퍼 클래스보다 느릴 수 있습니다.

## <a name="stream-design"></a>스트림 디자인

공용 언어 런타임은 대칭 알고리즘 및 해시 알고리즘을 구현하기 위한 스트림 지향 디자인을 사용합니다. 이 디자인의 핵심은 <xref:System.Security.Cryptography.CryptoStream> 클래스로, <xref:System.IO.Stream> 클래스에서 파생됩니다. 스트림 기반 암호화 개체는 개체의 데이터 전송 부분을 처리하는 하나의 표준 인터페이스(`CryptoStream`)를 지원합니다. 모든 개체가 표준 인터페이스를 기반으로 하기 때문에 여러 개체를 함께 연결할 수 있으며(예: 해시 개체 및 암호화 개체를 순서대로 연결), 중간 스토리지 없이 데이터에 대해 여러 작업을 수행할 수 있습니다. 또한 스트리밍 모델을 사용하면 더 작은 개체에서 개체를 빌드할 수 있습니다. 예를 들어 스트림 개체 집합에서 이 개체를 빌드할 수도 있지만 결합된 암호화 및 해시 알고리즘을 단일 스트림 개체로 볼 수 있습니다.

## <a name="cryptographic-configuration"></a>암호화 구성

암호화 구성을 사용하면 알고리즘의 특정 구현을 알고리즘 이름으로 확인하여 .NET Framework 암호화 클래스를 확장할 수 있습니다. 알고리즘의 고유한 하드웨어 또는 소프트웨어 구현을 추가하고 선택한 알고리즘 이름에 해당 구현을 매핑할 수 있습니다. 구성 파일에 알고리즘이 지정되지 않은 경우 기본 설정이 사용됩니다. 암호화 구성에 대 한 자세한 내용은 참조 하세요. [암호화 클래스 구성](../../../docs/framework/configure-apps/configure-cryptography-classes.md)합니다.

## <a name="choosing-an-algorithm"></a>알고리즘 선택

데이터 무결성, 데이터 프라이버시 또는 키 생성과 같은 다양한 이유로 알고리즘을 선택할 수 있습니다. 대칭 및 해시 알고리즘은 무결성(변경 차단) 또는 프라이버시(보기 차단)를 위해 데이터를 보호하는 데 사용됩니다. 해시 알고리즘은 주로 데이터 무결성을 위해 사용됩니다.

애플리케이션에서 권장하는 알고리즘 목록은 다음과 같습니다.

- 데이터 프라이버시:

  - <xref:System.Security.Cryptography.Aes>

- 데이터 무결성:

  - <xref:System.Security.Cryptography.HMACSHA256>

  - <xref:System.Security.Cryptography.HMACSHA512>

- 디지털 서명:

  - <xref:System.Security.Cryptography.ECDsa>

  - <xref:System.Security.Cryptography.RSA>

- 키 교환:

  - <xref:System.Security.Cryptography.ECDiffieHellman>

  - <xref:System.Security.Cryptography.RSA>

- 난수 생성:

  - <xref:System.Security.Cryptography.RNGCryptoServiceProvider>

- 암호에서 키 생성:

  - <xref:System.Security.Cryptography.Rfc2898DeriveBytes>

## <a name="see-also"></a>참고자료

- [Cryptographic Services](../../../docs/standard/security/cryptographic-services.md)
