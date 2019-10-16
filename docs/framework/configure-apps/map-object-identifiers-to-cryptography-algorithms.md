---
title: 개체 식별자를 암호화 알고리즘에 매핑
ms.date: 03/30/2017
helpviewer_keywords:
- digital signatures
- identifiers, mapping object identifiers
- cryptographic algorithms
- mapping object identifiers
- cryptography, mapping object identifiers
ms.assetid: c9673f81-bf9e-47fd-bc6f-6bc1c1c4c15e
ms.openlocfilehash: a5aebac2d392d4540581dfe7c7afff0819968ac0
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69912537"
---
# <a name="mapping-object-identifiers-to-cryptography-algorithms"></a>개체 식별자를 암호화 알고리즘에 매핑
디지털 서명은 한 프로그램에서 다른 프로그램으로 전송 될 때 데이터가 변조 되지 않도록 합니다. 일반적으로 디지털 서명은 서명할 데이터의 해시에 수치 연산 함수를 적용 하 여 계산 됩니다. 서명할 해시 값의 형식을 지정할 때 일부 디지털 서명 알고리즘은 서식 지정 작업의 일부로 asn.1 (개체 식별자)을 추가 합니다. OID는 해시를 계산 하는 데 사용 된 알고리즘을 식별 합니다. 알고리즘을 개체 식별자에 매핑하여 암호화 메커니즘을 확장 하 여 사용자 지정 알고리즘을 사용할 수 있습니다. 다음 예제에서는 새 해시 알고리즘에 개체 식별자를 매핑하는 방법을 보여 줍니다.  
  
```xml  
<configuration>  
   <mscorlib>  
      <cryptographySettings>  
         <cryptoNameMapping>  
            <cryptoClasses>  
               <cryptoClass MyNewHash="MyNewHashClass, MyAssembly  
                  Culture='en', PublicKeyToken=a5d015c7d5a0b012,  
                  Version=1.0.0.0"/>  
            </cryptoClasses>  
            <nameEntry name="NewHash" class="MyNewHash"/>  
         </cryptoNameMapping>  
         <oidMap>  
            <oidEntry OID="1.3.14.33.42.46"  name="NewHash"/>  
         </oidMap>  
      </cryptographySettings>  
   </mscorlib>  
</configuration>  
```  
  
 [ \<Y > 요소](./file-schema/cryptography/oidentry-element.md) 는 두 가지 특성을 포함 합니다. **OID** 특성은 개체 식별자 번호입니다. **Name** 특성은 [ \<nameentry > 요소의](./file-schema/cryptography/nameentry-element.md) **name** 특성 값입니다. 개체 식별자를 단순 이름에 매핑하기 전에 알고리즘 이름에서 클래스로 매핑되어야 합니다.  
  
## <a name="see-also"></a>참고자료

- [암호화 클래스 구성](configure-cryptography-classes.md)
- [Cryptographic Services](../../standard/security/cryptographic-services.md)
