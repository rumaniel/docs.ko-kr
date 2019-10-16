---
title: <oidMap> 요소
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#oidMap
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/mscorlib/cryptographySettings/oidMap
helpviewer_keywords:
- <oidMap> element
- oidMap element
ms.assetid: 7f0c2246-c070-4748-b96a-2f66a296c539
ms.openlocfilehash: eec2c4745ad5a0492ccf04c8f23b901275f23c01
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71698440"
---
# <a name="oidmap-element"></a>\<oidMap > 요소
클래스에 대 한 OID (개체 식별자) 매핑을 포함 합니다.  
  
[ **\<configuration>** ](../configuration-element.md)  
&nbsp; @ no__t[ **\<mscorlib >** ](mscorlib-element-for-cryptography-settings.md)  
&nbsp; @ no__t-1 @ no__t @ no__t[ **\<cryptographySettings >** ](cryptographysettings-element.md)  
&nbsp; @ no__t-1 @ no__t @ no__t @ @ no__t-4 @ no__t-5 **\<oidMap >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<oidMap>   
</oidMap>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
 없음  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<oidEntry>](oidentry-element.md)|ASN OID를 친숙 한 이름에 매핑합니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|  
|`cryptographySettings`|암호화 설정이 포함되어 있습니다.|  
|`mscorlib`|요소를 `cryptographySettings` 포함 합니다.|  
  
## <a name="example"></a>예제  
 다음 예제에서는 **\<oidMap >** 요소를 사용 하 여 해당 해시 알고리즘의 구현에 RIPEMD-160 해시 알고리즘에 대 한 OID 매핑을 포함 하는 방법을 보여 줍니다.  
  
```xml  
<configuration>  
   <mscorlib>  
      <cryptographySettings>  
         <cryptoNameMapping>  
            <cryptoClasses>  
               <cryptoClass   MyCrypto="MyCryptoClass, MyAssembly  
                  Culture=neutral, PublicKeyToken=a5d015c7d5a0b012,  
                  Version=1.0.0.0"/>  
            </cryptoClasses>  
            <nameEntry name="RIPEMD-160" class="MyCrypto"/>  
         </cryptoNameMapping>  
         <oidMap>  
            <oidEntry OID="1.3.36.3.2.1"  name="MyCryptoClass"/>  
         </oidMap>  
      </cryptographySettings>  
   </mscorlib>  
</configuration>  
```  
  
## <a name="see-also"></a>참조

- [구성 파일 스키마](../index.md)
- [암호화 설정 스키마](index.md)
- [Cryptographic Services](../../../../standard/security/cryptographic-services.md)
- [암호화 클래스 구성](../../configure-cryptography-classes.md)
- [개체 식별자를 암호화 알고리즘에 매핑](../../map-object-identifiers-to-cryptography-algorithms.md)
