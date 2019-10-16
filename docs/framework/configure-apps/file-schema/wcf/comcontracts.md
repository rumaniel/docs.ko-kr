---
title: <comContracts>
ms.date: 03/30/2017
ms.assetid: 42e74148-223d-4888-a8ed-1d928527eb09
ms.openlocfilehash: d061d48374a8745dc61e1ca156e4fcbbccee5ef7
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69919483"
---
# <a name="comcontracts"></a>\<comContracts>
`comContracts` 구성 섹션에는 COM+ 통합 서비스 계약의 다양한 속성을 지정할 수 있게 해 주는 요소가 포함되어 있습니다.  
  
## <a name="specifying-namespace-and-contract"></a>네임스페이스 및 계약 지정  
 Com + 통합 서비스 계약은 현재 `http://tempuri.org` 네임 스페이스로 제한 되며, 계약 이름은 지원 COM 인터페이스에서 파생 됩니다. 그러나 구성 파일에서 `comContracts` 섹션을 사용하여 대안을 지정할 수 있습니다.  
  
 예를 들어 다음 구성을 사용하여 서비스 계약의 네임스페이스 및 계약 이름과 세션 바인딩에 사용법을 적용할 옵션을 지정할 수 있습니다.  
  
```xml  
<comContracts>
  <comContract contract="{5163B1E7-F0CF-4B6A-9A02-4AB654F34284}"
               namespace="http://tempuri.org/5163B1E7-F0CF-4B6A-9A02-4AB654F34284"
               name="_Broker"
               requireSession="true">
  </comContract>
</comContracts>
```  
  
 지정된 네임스페이스와 계약 이름은 서비스가 초기화될 때 생성된 서비스 설명에 적용됩니다.  
  
 이 섹션이 비어 있으면 서비스 초기화에서는 지원 COM 인터페이스 ID에서 가져온 기본 네임스페이스 및 계약 이름을 적용합니다.  
  
 또한 [ \<exposedMethod >](exposedmethod.md) 요소를 사용 하 여 com + 구성 요소의 인터페이스가 웹 서비스로 노출 될 때 노출 되는 com + 메서드를 지정할 수 있습니다. 또한 [ \<persistabletypes >](persistabletypes.md) 를 사용 하 여 통합에 사용 되는 지속 형식을 지정할 수 있습니다. 마지막으로 [ \<userDefinedType >](userdefinedtype.md) 요소를 사용 하 여 서비스 계약에 포함할 UDT (사용자 정의 형식)를 포함할 수 있습니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Configuration.ComContractElementCollection>
- <xref:System.ServiceModel.Configuration.ComContractElement>
- [\<exposedMethod>](exposedmethod.md)
- [\<persistableTypes>](persistabletypes.md)
- [\<userDefinedType>](userdefinedtype.md)
- [\<comContract>](comcontract.md)
- [COM+ 애플리케이션과 통합](../../../wcf/feature-details/integrating-with-com-plus-applications.md)
- [방법: COM + 서비스 설정 구성](../../../wcf/feature-details/how-to-configure-com-service-settings.md)
