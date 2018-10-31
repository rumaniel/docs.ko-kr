---
title: '&lt;nameEntry&gt; 요소'
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#nameEntry
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/mscorlib/cryptographySettings/cryptoNameMapping/nameEntry
helpviewer_keywords:
- <nameEntry> element
- nameEntry element
ms.assetid: 7d7535e9-4b4a-4b8c-82e2-e40dff5a7821
author: mcleblanc
ms.author: markl
ms.openlocfilehash: f5d53debd746ba031e39215354c391d288016b6b
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/28/2018
ms.locfileid: "50201361"
---
# <a name="ltnameentrygt-element"></a>&lt;nameEntry&gt; 요소
클래스 이름을 알고리즘 이름에 매핑하며, 이를 통해 하나의 클래스가 여러 이름을 가질 수 있습니다.  
  
 \<configuration>  
\<mscorlib >  
\<cryptographySettings >  
\<cryptoNameMapping >  
\<m t r y >  
  
## <a name="syntax"></a>구문  
  
```xml  
<nameEntry name="friendly name" Class="class name" />  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|**name**|필수 특성입니다.<br /><br /> 암호화 클래스를 구현 하는 알고리즘의 이름을 지정 합니다.|  
|**class**|필수 특성입니다.<br /><br /> 에 대 한 값을 지정 합니다 **이름** 특성을 [ \<cryptoClass >](../../../../../docs/framework/configure-apps/file-schema/cryptography/cryptoclass-element.md) 요소입니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|`configuration`|공용 언어 런타임 및 .NET Framework 응용 프로그램에서 사용하는 모든 구성 파일의 루트 요소입니다.|  
|`system.web`|ASP.NET 구성 섹션의 루트 요소를 지정합니다.|  
  
## <a name="remarks"></a>설명  
 **이름을** 특성에 있는 추상 클래스 중 하나의 이름을 수는 <xref:System.Security.Cryptography> 네임 스페이스입니다. 호출 하는 경우는 **만들기** 추상 암호화 클래스에 메서드를 추상 클래스 이름에 전달 되는 <xref:System.Security.Cryptography.CryptoConfig.CreateFromName%2A> 메서드. **CreateFromName** 하 여 지정 된 형식의 인스턴스를 반환 합니다 **클래스** 특성입니다. 경우는 **이름** 특성은 약식 이름, RSA와 같은 이름을 사용할 수 있습니다는 호출 하는 경우를 **CreateFromName** 메서드.  
  
## <a name="example"></a>예제  
 다음 예제에서는 사용 하는 방법을 보여 줍니다 합니다  **\<m t r y >** 암호화 클래스를 참조 하 고 런타임 구성 요소입니다. "RSA" 문자열을 전달할 수 있습니다는 <xref:System.Security.Cryptography.CryptoConfig.CreateFromName%2A?displayProperty=nameWithType> 메서드 및 사용법을 <xref:System.Security.Cryptography.AsymmetricAlgorithm.Create%2A> 반환 하는 방법을 `MyCryptoRSAClass` 개체입니다.  
  
```xml  
<configuration>  
   <mscorlib>  
      <cryptographySettings>  
         <cryptoNameMapping>  
            <cryptoClasses>  
               <cryptoClass   MyCryptoRSA="MyCryptoRSAClass, MyAssembly  
                  Culture=neutral, PublicKeyToken=a5d015c7d5a0b012,  
                  Version=1.0.0.0"/>  
            </cryptoClasses>  
            <nameEntry name="RSA" class="MyCryptoRSA"/>  
            <nameEntry name="System.Security.Cryptography.AsymmetricAlgorithm"  
                       class="MyCryptoRSA"/>  
         </cryptoNameMapping>  
      </cryptographySettings>  
   </mscorlib>  
</configuration>  
```  
  
## <a name="see-also"></a>참고 항목  
- [구성 파일 스키마](../../../../../docs/framework/configure-apps/file-schema/index.md)  
- [암호화 설정 스키마](../../../../../docs/framework/configure-apps/file-schema/cryptography/index.md)  
- [Cryptographic Services](../../../../../docs/standard/security/cryptographic-services.md)  
- [암호화 클래스 구성](../../../../../docs/framework/configure-apps/configure-cryptography-classes.md)
