---
ms.openlocfilehash: 6d9f4b630e95d9a63393da3ae0ecd83c2b994712
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67859367"
---
### <a name="rsacng-now-correctly-loads-rsa-keys-of-non-standard-key-size"></a>이제 RSACng가 비표준 키 크기의 RSA 키를 올바르게 로드함

|   |   |
|---|---|
|세부 정보|4\.6.2 이전의 .NET Framework 버전의 경우, RSA 인증서의 비표준 키 크기를 가진 고객은 <xref:System.Security.Cryptography.X509Certificates.RSACertificateExtensions.GetRSAPublicKey(System.Security.Cryptography.X509Certificates.X509Certificate2)?displayProperty=name> 및 <xref:System.Security.Cryptography.X509Certificates.RSACertificateExtensions.GetRSAPrivateKey(System.Security.Cryptography.X509Certificates.X509Certificate2)?displayProperty=name> 확장 메서드를 통해 해당 키에 액세스할 수 없습니다.  &quot;요청한 키 크기가 지원되지 않습니다&quot; 메시지와 함께 <xref:System.Security.Cryptography.CryptographicException?displayProperty=name>이 throw됩니다. .NET Framework 4.6.2에서 이 문제가 해결되었습니다. 마찬가지로, <xref:System.Security.Cryptography.RSA.ImportParameters(System.Security.Cryptography.RSAParameters)> 및 <xref:System.Security.Cryptography.RSACng.ImportParameters(System.Security.Cryptography.RSAParameters)>은 <xref:System.Security.Cryptography.CryptographicException?displayProperty=name>을 throw하지 않고 비표준 키 크기로 작업합니다.|
|제안|비표준 키 크기가 사용될 때 <xref:System.Security.Cryptography.CryptographicException?displayProperty=name>이 throw되는 이전 동작에 의존하는 예외 처리 논리가 있는 경우 논리 제거를 고려하세요.|
|범위|Microsoft Edge|
|버전|4.6.2|
|형식|대상 변경|
|영향을 받는 API|<ul><li><xref:System.Security.Cryptography.RSA.ImportParameters(System.Security.Cryptography.RSAParameters)?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.RSACng.ImportParameters(System.Security.Cryptography.RSAParameters)?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.X509Certificates.RSACertificateExtensions.GetRSAPrivateKey(System.Security.Cryptography.X509Certificates.X509Certificate2)?displayProperty=nameWithType></li><li><xref:System.Security.Cryptography.X509Certificates.RSACertificateExtensions.GetRSAPublicKey(System.Security.Cryptography.X509Certificates.X509Certificate2)?displayProperty=nameWithType></li></ul>|

