---
title: <cryptographySettings> 요소
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/mscorlib/cryptographySettings
- http://schemas.microsoft.com/.NetConfiguration/v2.0#cryptographySettings
helpviewer_keywords:
- cryptographySettings element
- <cryptographySettings> element
ms.assetid: 6201b7da-bcb7-49f7-b9f5-ba1fe05573b9
ms.openlocfilehash: 96a8c9accc56274b5cc13dc2a871165857b3a2d9
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71699817"
---
# <a name="cryptographysettings-element"></a>\<cryptographySettings > 요소
암호화 설정이 포함되어 있습니다.  
  
[ **\<configuration>** ](../configuration-element.md)  
&nbsp; @ no__t[ **\<mscorlib >** ](mscorlib-element-for-cryptography-settings.md)  
&nbsp; @ no__t-1 @ no__t @ no__t **\<cryptographySettings >**  
  
## <a name="syntax"></a>구문  
  
```xml  
      <cryptographySettings>   
</cryptographySettings>  
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
 없음  
  
### <a name="child-elements"></a>자식 요소  
  
|요소|설명|  
|-------------|-----------------|  
|[\<cryptoNameMapping>](cryptonamemapping-element.md)|이름에 대한 클래스의 매핑이 포함되어 있습니다.|  
|[\<oidMap>](oidmap-element.md)|클래스에 대 한 OID (개체 식별자) 매핑을 포함 합니다.|  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|설명|  
|-------------|-----------------|  
|`configuration`|공용 언어 런타임 및 .NET Framework 애플리케이션에서 사용하는 모든 구성 파일의 루트 요소입니다.|  
|`mscorlib`|요소를 `cryptographySettings` 포함 합니다.|  
  
## <a name="example"></a>예제  
 다음 예에서는 **\<cryptographySettings >** 요소를 사용 하 여 암호화 이름 매핑과 OID 매핑을 포함 하는 방법을 보여 줍니다. 이 예제에서는 <xref:System.Security.Cryptography.HashAlgorithm.Create%2A?displayProperty=nameWithType>이 `MyHashClass` 개체를 반환 하 고 `MyCryptoClass` 클래스가 개체 식별자 1.3.36.2.1에 매핑되도록 런타임을 구성 합니다.  
  
```xml  
<configuration>  
   <mscorlib>  
      <cryptographySettings>  
         <cryptoNameMapping>  
            <cryptoClasses>  
               <cryptoClass   MyHash="MyHashClass, MyAssembly  
                  Culture=neutral, PublicKeyToken=a5d015c7d5a0b012,  
                  Version=1.0.0.0"/>  
               <cryptoClass   MyCrypto="MyCryptoClass, MyAssembly  
                  Culture=neutral, PublicKeyToken=a5d015c7d5a0b012,  
                  Version=1.0.0.0"/>  
            </cryptoClasses>  
            <nameEntry name="System.Security.Cryptography.HashAlgorithm"  
                       class="MyHash"/>  
         </cryptoNameMapping>  
         <oidMap>  
            <oidEntry OID="1.3.36.3.2.1"   name="MyCryptoClass"/>  
         </oidMap>  
      </cryptographySettings>  
   </mscorlib>  
</configuration>  
```  
  
## <a name="see-also"></a>참조

- [구성 파일 스키마](../index.md)
- [암호화 설정 스키마](index.md)
- [Cryptographic Services](../../../../standard/security/cryptographic-services.md)
