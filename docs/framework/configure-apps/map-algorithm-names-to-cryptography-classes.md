---
title: 알고리즘 이름을 암호화 클래스에 매핑
ms.date: 03/30/2017
helpviewer_keywords:
- mapping algorithm names
- cryptography, mapping algorithm names
- cryptographic algorithms
- names [.NET Framework], algorithm mapping
ms.assetid: 01327c69-c5e1-4ef6-b73f-0a58351f0492
ms.openlocfilehash: 513000169504473aa6dd46feaca214f58502ffd0
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69912862"
---
# <a name="mapping-algorithm-names-to-cryptography-classes"></a>알고리즘 이름을 암호화 클래스에 매핑
개발자가 Windows SDK를 사용 하 여 암호화 개체를 만들 수 있는 네 가지 방법이 있습니다.  
  
- **New** 연산자를 사용 하 여 개체를 만듭니다.  
  
- 해당 알고리즘의 추상 클래스에서 **create** 메서드를 호출 하 여 특정 암호화 알고리즘을 구현 하는 개체를 만듭니다.  
  
- 메서드를 <xref:System.Security.Cryptography.CryptoConfig.CreateFromName%2A?displayProperty=nameWithType> 호출 하 여 특정 암호화 알고리즘을 구현 하는 개체를 만듭니다.  
  
- 해당 알고리즘 형식 (예: <xref:System.Security.Cryptography.SymmetricAlgorithm>)에 대 한 추상 클래스에서 **Create** 메서드를 호출 하 여 대칭 블록 암호화와 같은 암호화 알고리즘의 클래스를 구현 하는 개체를 만듭니다.  
  
 예를 들어 개발자가 바이트 집합의 SHA1 해시를 계산 하려고 한다고 가정 합니다. <xref:System.Security.Cryptography> 네임 스페이스에는 완전히 관리 되는 구현과 CryptoAPI를 래핑하는 SHA1 알고리즘의 두 가지 구현이 포함 되어 있습니다. 개발자는 <xref:System.Security.Cryptography.SHA1Managed> **new** 연산자를 호출 하 여와 같은 특정 SHA1 구현을 인스턴스화할 수 있습니다. 그러나 클래스가 SHA1 해시 알고리즘을 구현 하는 한 공용 언어 런타임에서 로드 하는 클래스가 중요 하지 않은 경우 개발자는 메서드를 <xref:System.Security.Cryptography.SHA1.Create%2A?displayProperty=nameWithType> 호출 하 여 개체를 만들 수 있습니다. 이 메서드는 SHA1 해시 알고리즘의 구현을 반환 해야 하는 **CryptoConfig ("system.web**. s s i s. s. s. s. s")를 호출 합니다.  
  
 기본적으로 .NET Framework에서 제공 되는 알고리즘에 대 한 짧은 이름을 포함 하기 때문에 개발자는 **CryptoConfig ("SHA1")** 를 호출할 수도 있습니다.  
  
 사용 되는 해시 알고리즘에 상관 없이 개발자는 해시 변환을 구현 하는 개체 <xref:System.Security.Cryptography.HashAlgorithm.Create%2A?displayProperty=nameWithType> 를 반환 하는 메서드를 호출할 수 있습니다.  
  
## <a name="mapping-algorithm-names-in-configuration-files"></a>구성 파일에서 알고리즘 이름 매핑  
 기본적으로 런타임은 네 가지 시나리오 모두 <xref:System.Security.Cryptography.SHA1CryptoServiceProvider> 에 대해 개체를 반환 합니다. 그러나 컴퓨터 관리자는 마지막 두 시나리오의 메서드가 반환 하는 개체의 유형을 변경할 수 있습니다. 이렇게 하려면 컴퓨터 구성 파일 (machine.config)에서 사용 하려는 클래스에 친숙 한 알고리즘 이름을 매핑해야 합니다.  
  
 다음 예제에서는 CryptoConfig, HashAlgorithm **("SHA1")** 및 **를 구성 하 여 런타임을 구성 하는 방법을 보여 줍니다 .이 예제에서는를 만듭니다.** 개체를 `MySHA1HashClass` 반환 합니다.  
  
```xml  
<configuration>  
   <!-- Other configuration settings. -->  
   <mscorlib>  
      <cryptographySettings>  
         <cryptoNameMapping>  
            <cryptoClasses>  
               <cryptoClass MySHA1Hash="MySHA1HashClass, MyAssembly  
                  Culture='en', PublicKeyToken=a5d015c7d5a0b012,  
                  Version=1.0.0.0"/>  
            </cryptoClasses>  
            <nameEntry name="SHA1" class="MySHA1Hash"/>  
            <nameEntry name="System.Security.Cryptography.SHA1"  
                       class="MySHA1Hash"/>  
            <nameEntry name="System.Security.Cryptography.HashAlgorithm"  
                       class="MySHA1Hash"/>  
         </cryptoNameMapping>  
      </cryptographySettings>  
   </mscorlib>  
</configuration>  
```  
  
 [< Cryptoclass\> 요소](./file-schema/cryptography/cryptoclass-element.md) 에서 특성의 이름을 지정할 수 있습니다. 이전 예제에서는 특성 `MySHA1Hash`의 이름을 지정 합니다. Cryptoclass > 요소에 있는  **\<** 특성의 값은 공용 언어 런타임에서 클래스를 찾는 데 사용 하는 문자열입니다. 정규화 된 [형식 이름 지정](../reflection-and-codedom/specifying-fully-qualified-type-names.md)에 지정 된 요구 사항을 충족 하는 모든 문자열을 사용할 수 있습니다.  
  
 많은 알고리즘 이름을 동일한 클래스에 매핑할 수 있습니다. [ \<Nameentry > 요소](./file-schema/cryptography/nameentry-element.md) 는 클래스를 친숙 한 알고리즘 이름에 매핑합니다. **Name** 특성은 **CryptoConfig** 메서드를 호출할 때 사용 되는 문자열 이거나 <xref:System.Security.Cryptography> 네임 스페이스에 있는 추상 암호화 클래스의 이름일 수 있습니다. **Class** 특성의 값은  **\<cryptoclass >** 요소에 있는 특성의 이름입니다.  
  
> [!NOTE]
> 또는 **CryptoConfig ("sha1")** 메서드를 <xref:System.Security.Cryptography.SHA1.Create%2A?displayProperty=nameWithType> 호출 하 여 SHA1 알고리즘을 가져올 수 있습니다. 각 메서드는 SHA1 알고리즘을 구현 하는 개체만 반환 하도록 보장 합니다. 알고리즘의 각 식별 이름을 구성 파일의 동일한 클래스에 매핑할 필요가 없습니다.  
  
 기본 이름 및 매핑되는 클래스 목록은를 참조 <xref:System.Security.Cryptography.CryptoConfig>하십시오.  
  
## <a name="see-also"></a>참고자료

- [Cryptographic Services](../../standard/security/cryptographic-services.md)
- [암호화 클래스 구성](configure-cryptography-classes.md)
