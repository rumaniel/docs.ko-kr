---
title: <userDefinedType>
ms.date: 03/30/2017
ms.assetid: 0f70ec06-8249-4f0c-9f49-b4df59985fb8
ms.openlocfilehash: 7a76e5a90fe3218bc0302501b71daa9de0b098bc
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854838"
---
# <a name="userdefinedtype"></a>\<userDefinedType>
서비스 계약에 포함될 UDT(사용자 정의 형식)를 나타냅니다.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<System.servicemodel >** ](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<comContracts >** ](comcontracts.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<comContract >** ](comcontract.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<userDefinedTypes >** ](userdefinedtypes.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<userDefinedType >**  
  
## <a name="syntax"></a>구문  
  
```xml  
<comContracts>
  <comContract>
    <userDefinedTypes>
      <userDefinedType name="String"
                       typeLibID="String"
                       typeLibVersion="String"
                       typeDefID="String">
      </userDefinedType>
    </userDefinedTypes>
  </comContract>
</comContracts>
```  
  
## <a name="attributes-and-elements"></a>특성 및 요소  
 다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.  
  
### <a name="attributes"></a>특성  
  
|특성|설명|  
|---------------|-----------------|  
|`name`|읽기 가능한 형식의 이름을 제공하는 문자열이 포함된 선택적 특성입니다. 이 특성은 런타임에서 사용되지 않지만, 판독기에서 형식을 구별할 때 도움이 됩니다.|  
|`TypeDefID`|등록된 형식 라이브러리에 있는 특정 UDT 형식을 식별하는 GUID 문자열입니다.|  
|`TypeLibID`|형식을 정의하는 등록된 형식 라이브러리를 식별하는 GUID 문자열입니다.|  
|`TypeLibVersion`|: 형식을 정의하는 형식 라이브러리 버전을 식별하는 문자열입니다.|  
  
### <a name="child-elements"></a>자식 요소  
 없음  
  
### <a name="parent-elements"></a>부모 요소  
  
|요소|Description|  
|-------------|-----------------|  
|`userDefinedTypes`|`userDefinedType` 요소의 컬렉션입니다.|  
  
## <a name="remarks"></a>설명  
 COM+ 통합 런타임에서는 형식 라이브러리를 검사하여 서비스를 생성합니다. COM+ 구성 요소에 VARIANT를 전달하는 메서드가 포함될 경우 시스템에서 런타임 전에 전달될 실제 형식을 확인할 수 없습니다. 따라서 VARIANT 내에서 UDT(사용자 정의 형식)를 전달하려고 시도하면 알려진 serialization 형식이 아니므로 실패합니다.  
  
 이 문제를 방지하기 위해 UDT를 구성 파일에 추가함으로써 적절한 서비스 계약에 알려진 형식으로 포함되게 할 수 있습니다. 그러기 위해서는 UDT와 계약, 즉 이를 사용하는 원래 COM 인터페이스를 고유하게 식별해야 합니다.  
  
 다음 예제에서는 이러한 목적으로 구성 파일의 <`userDefinedTypes`> 섹션에 특정 UDT 두 개를 추가하는 것을 보여 줍니다.  
  
```xml  
<comContracts>
  <comContract contract="{5163B1E7-F0CF-4B6A-9A02-4AB654F34284}"
               namespace="http://tempuri.org/5163B1E7-F0CF-4B6A-9A02-4AB654F34284"
               name="_Broker"
               requireSession="true">
    <userDefinedTypes>
      <userDefinedType name="CustomerType"
                       typeLibID="{91DC728C-4F1A-45de-A9B6-B538E209CEA6}"
                       typeLibVersion="1.0"
                       typeDefID="{D129765C-F211-434e-825A-9A63198C41F2}">
      </userDefinedType>
      <userDefinedType name="AddressType"
                       typeLibID="{91DC728C-4F1A-45de-A9B6-B538E209CEA6}"
                       typeLibVersion="1.0"
                       typeDefID="{4616AE0D-687A-43B7-BC63-141AE3DFD099}">
      </userDefinedType>
    </userDefinedTypes>
    <exposedMethods>
      <exposedMethod name="BuyStock" />
      <exposedMethod name="SellStock" />
      <exposedMethod name="ExecuteTransaction" />
    </exposedMethods>
  </comContract>
</comContracts>
```  
  
 서비스가 초기화될 때 통합 런타임에서는 지정된 형식을 찾아 지정된 계약의 알려진 형식 컬렉션에 이를 추가합니다.  
  
## <a name="see-also"></a>참고자료

- <xref:System.ServiceModel.Configuration.ComContractElement.UserDefinedTypes%2A>
- <xref:System.ServiceModel.Configuration.ComUdtElementCollection>
- <xref:System.ServiceModel.Configuration.ComUdtElement>
- [\<comContracts>](comcontracts.md)
- [COM+ 애플리케이션과 통합](../../../wcf/feature-details/integrating-with-com-plus-applications.md)
- [방법: COM + 서비스 설정 구성](../../../wcf/feature-details/how-to-configure-com-service-settings.md)
