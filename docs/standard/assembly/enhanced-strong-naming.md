---
title: 향상된 강력한 이름 지정
ms.date: 08/20/2019
helpviewer_keywords:
- strong-named assemblies
- strong naming [.NET Framework], enhanced
ms.assetid: 6cf17a82-62a1-4f6d-8d5a-d7d06dec2bb5
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1ab1087a840fe41b9fac7779c73797c470899408
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834888"
---
# <a name="enhanced-strong-naming"></a>향상된 강력한 이름 지정
강력한 이름 시그니처는 어셈블리를 식별하기 위한 .NET Framework의 ID 메커니즘입니다. 일반적으로 작성기(서명자)에서 수신자(검증 도구)로 전달되는 데이터의 무결성을 검사하는 데 사용되는 공개 키 디지털 시그니처입니다. 이 시그니처는 어셈블리의 고유 ID로 사용되고 어셈블리에 대한 참조가 모호하지 않은지 확인합니다. 어셈블리는 빌드 프로세스의 일부로 서명되고 나서 로드 시 확인됩니다.  
  
 강력한 이름 시그니처를 사용하면 악의적인 당사자가 어셈블리를 변조하고 나서 원래 서명자의 키로 어셈블리에 다시 서명하지 못하게 할 수 있습니다. 하지만 강력한 이름 키에는 게시자에 대한 신뢰할 수 있는 정보가 포함되지 않고 인증서 계층 구조도 포함되지 않습니다. 강력한 이름 시그니처는 어셈블리에 서명한 개인의 신뢰성을 보장하거나 해당 개인이 키의 적법한 소유자였는지 여부를 표시하지 않습니다. 키 소유자가 어셈블리에 서명했다는 것만 표시합니다. 따라서 강력한 이름 시그니처를 타사 코드를 신뢰하기 위한 보안 유효성 검사기로 사용하지 않는 것이 좋습니다. Microsoft Authenticode는 코드를 인증하는 권장 방법입니다.  
  
## <a name="limitations-of-conventional-strong-names"></a>기존 강력한 이름의 제한 사항  
 .NET Framework 4.5 이전 버전에서 사용된 강력한 이름 지정 기술에는 다음과 같은 단점이 있습니다.  
  
- 키가 계속해서 공격을 받고 향상된 기술과 하드웨어를 통해 퍼블릭 키에서 프라이빗 키를 쉽게 유추할 수 있습니다. 공격을 방지하기 위해 더 큰 키가 필요합니다. .NET Framework 4.5 이전 .NET Framework 버전은 크기 키(기본 크기는 1024비트)로 서명하는 기능을 제공하지만, 새 키로 어셈블리에 서명하면 어셈블리의 이전 ID를 참조하는 모든 이진 파일이 중단됩니다. 따라서 호환성을 유지하려는 경우 서명 키의 크기를 업그레이드하기가 매우 어렵습니다.  
  
- 강력한 이름 서명은 SHA-1 알고리즘만 지원합니다. SHA-1은 최근에 보안 해시 애플리케이션에는 부적절한 것으로 확인되었습니다. 따라서 더 강력한 알고리즘(SHA-256 이상)이 필요합니다. SHA-1에서 FIPS 규격 순위가 손실되어 FIPS 규격 소프트웨어 및 알고리즘만 사용하도록 선택한 사용자에게 문제가 발생할 수 있습니다.  
  
## <a name="advantages-of-enhanced-strong-names"></a>향상된 강력한 이름의 장점  
 향상된 강력한 이름의 주요 장점은 기존 강력한 이름과의 호환성 및 하나의 ID가 다른 ID와 일치하도록 요구하는 기능입니다.  
  
- 기존의 서명된 어셈블리가 있는 개발자는 이전 ID를 참조하는 어셈블리와의 호환성을 유지하면서 자신의 ID를 SHA-2 알고리즘으로 마이그레이션할 수 있습니다.  
  
- 새 어셈블리를 만들고 기존의 강력한 이름 시그니처와 관련이 없는 개발자는 더 안전한 SHA-2 알고리즘을 사용하고 이전과 같은 방법으로 어셈블리에 서명할 수 있습니다.  
  
## <a name="use-enhanced-strong-names"></a>향상된 강력한 이름 사용  
 강력한 이름 키는 시그니처 키 및 ID 키로 구성됩니다. 어셈블리는 시그니처 키로 서명되고 ID 키로 식별됩니다. .NET Framework 4.5 이전에는 이러한 두 가지 키가 동일했습니다. .NET Framework 4.5부터 ID 키는 이전 .NET Framework 버전과 동일하게 유지되지만, 시그니처 키는 더 강력한 해시 알고리즘을 사용하여 향상되었습니다. 또한 시그니처 키는 ID 키로 서명되어 연대 시그니처를 만듭니다.  
  
 <xref:System.Reflection.AssemblySignatureKeyAttribute> 특성을 사용하면 어셈블리 메타데이터가 어셈블리 ID에 기존 공개 키를 사용할 수 있으므로 이전 어셈블리 참조가 계속 작동할 수 있습니다.  <xref:System.Reflection.AssemblySignatureKeyAttribute> 특성은 연대 시그니처를 사용하여 새 시그니처 키의 소유자가 이전 ID 키의 소유자와 일치하는지 확인합니다.  
  
### <a name="sign-with-sha-2-without-key-migration"></a>키 마이그레이션 없이 SHA-2로 서명  
 강력한 이름 서명을 마이그레이션하지 않고 어셈블리에 서명하려면 명령 프롬프트에서 다음 명령을 실행합니다.  
  
1. 새 ID 키를 생성합니다(필요한 경우).  
  
    ```console  
    sn -k IdentityKey.snk  
    ```  
  
2. ID 공개 키를 추출하고 이 키로 서명할 때 SHA-2 알고리즘이 사용되도록 지정합니다.  
  
    ```console  
    sn -p IdentityKey.snk IdentityPubKey.snk sha256  
    ```  
  
3. ID 공개 키 파일을 사용하여 어셈블리 서명을 연기합니다.  
  
    ```console  
    csc MyAssembly.cs /keyfile:IdentityPubKey.snk /delaySign+  
    ```  
  
4. 전체 ID 키 쌍으로 어셈블리에 다시 서명합니다.  
  
    ```console  
    sn -Ra MyAssembly.exe IdentityKey.snk  
    ```  
  
### <a name="sign-with-sha-2-with-key-migration"></a>키 마이그레이션을 사용하여 SHA-2로 서명  
 마이그레이션된 강력한 이름 서명을 사용하여 어셈블리에 서명하려면 명령 프롬프트에서 다음 명령을 실행합니다.  
  
1. ID 및 시그니처 키 쌍을 생성합니다(필요한 경우).  
  
    ```console  
    sn -k IdentityKey.snk  
    sn -k SignatureKey.snk  
    ```  
  
2. 시그니처 공개 키를 추출하고 이 키로 서명할 때 SHA-2 알고리즘이 사용되도록 지정합니다.  
  
    ```console  
    sn -p SignatureKey.snk SignaturePubKey.snk sha256  
    ```  
  
3. 연대 시그니처를 생성하는 해시 알고리즘을 확인하는 ID 공개 키를 추출합니다.  
  
    ```console  
    sn -p IdentityKey.snk IdentityPubKey.snk  
    ```  
  
4. <xref:System.Reflection.AssemblySignatureKeyAttribute> 특성에 대한 매개 변수를 생성하고 특성을 어셈블리에 연결합니다.  
  
    ```console  
    sn -a IdentityPubKey.snk IdentityKey.snk SignaturePubKey.snk  
    ```  

    이 명령은 다음과 비슷한 출력을 생성합니다.

    ```output
    Information for key migration attribute.
    (System.Reflection.AssemblySignatureKeyAttribute):
    publicKey=
    002400000c80000094000000060200000024000052534131000400000100010005a3a81ac0a519
    d96244a9c589fc147c7d403e40ccf184fc290bdd06c7339389a76b738e255a2bce1d56c3e7e936
    e4fc87d45adc82ca94c716b50a65d39d373eea033919a613e4341c66863cb2dc622bcb541762b4
    3893434d219d1c43f07e9c83fada2aed400b9f6e44ff05e3ecde6c2827830b8f43f7ac8e3270a3
    4d153cdd

    counterSignature=
    e3cf7c211678c4d1a7b8fb20276c894ab74c29f0b5a34de4d61e63d4a997222f78cdcbfe4c91eb
    e1ddf9f3505a32edcb2a76f34df0450c4f61e376b70fa3cdeb7374b1b8e2078b121e2ee6e8c6a8
    ed661cc35621b4af53ac29c9e41738f199a81240e8fd478c887d1a30729d34e954a97cddce66e3
    ae5fec2c682e57b7442738
    ```

    그런 다음, 이 출력을 AssemblySignatureKeyAttribute로 변환할 수 있습니다.

    ```
    [assembly:System.Reflection.AssemblySignatureKeyAttribute(
    "002400000c80000094000000060200000024000052534131000400000100010005a3a81ac0a519d96244a9c589fc147c7d403e40ccf184fc290bdd06c7339389a76b738e255a2bce1d56c3e7e936e4fc87d45adc82ca94c716b50a65d39d373eea033919a613e4341c66863cb2dc622bcb541762b43893434d219d1c43f07e9c83fada2aed400b9f6e44ff05e3ecde6c2827830b8f43f7ac8e3270a34d153cdd",
    "e3cf7c211678c4d1a7b8fb20276c894ab74c29f0b5a34de4d61e63d4a997222f78cdcbfe4c91ebe1ddf9f3505a32edcb2a76f34df0450c4f61e376b70fa3cdeb7374b1b8e2078b121e2ee6e8c6a8ed661cc35621b4af53ac29c9e41738f199a81240e8fd478c887d1a30729d34e954a97cddce66e3ae5fec2c682e57b7442738"
    )]
    ```
  
5. ID 공개 키를 사용하여 어셈블리 서명을 연기합니다.  
  
    ```console  
    csc MyAssembly.cs /keyfile:IdentityPubKey.snk /delaySign+  
    ```  
  
6. 시그니처 키 쌍으로 어셈블리에 완전히 서명합니다.  
  
    ```console  
    sn -Ra MyAssembly.exe SignatureKey.snk  
    ```  
  
## <a name="see-also"></a>참고 항목

- [강력한 이름의 어셈블리 만들기 및 사용](create-use-strong-named.md)
